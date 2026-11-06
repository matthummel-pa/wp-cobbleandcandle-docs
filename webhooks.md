# Send requests to another system (webhook)

When a guest sends a table request, a private dining inquiry, a contact message or a room booking request, your site can pass it on to another tool the moment it arrives: a CRM, a spreadsheet, a booking system, a chat channel. This is called a webhook. It is off until you set it up, and it does not replace the email you already get or the **Messages** list.

## Set it up

1. In the other tool, create a webhook address. Zapier, Make, n8n and many CRMs can give you one. It must start with `https://`.
2. In WordPress, go to **Settings → Theme Settings → Brand → Connections** and paste it into **Webhook address**.
3. Click **Save Changes**. A **Webhook secret** is made for you. Click **Show** to read it (the button then says **Hide**), and copy it into the other tool if it asks for one. You can also paste in a secret your other tool gave you; it is kept exactly as you type it, apart from spaces at either end. Treat the secret like a password. If you build the receiver yourself, see [Checking the signature](#checking-the-signature).
4. Send a test request through your own site, then open **Tools → Cobble & Candle status**. The log says **Webhook delivered** or why it failed.

If the address is not allowed (for example it starts with `http://`, points at a private network address, or its host cannot be found), WordPress shows an error and keeps the address you had before. Only an empty field switches the webhook off.

## What is sent, and when

| Event | When | What it carries |
| --- | --- | --- |
| `reservation.requested` | A guest sends a table request | House, date, time, party size, seating, occasion, name, phone, email, requests, newsletter choice |
| `inquiry.received` | A guest sends a private dining inquiry | House, subject, email and the full message text |
| `contact.received` | A guest sends a contact message | House, subject, email and the full message text |
| `booking.requested` | A guest sends a room booking request | Booking id, room, dates, guests, name, email, phone, message, total |

For inquiries and contact messages, `message` is the whole text exactly as the email shows it, so the guest's name, date and guest count are inside it, not separate fields.

Only new requests are sent. Changes you make later (confirming a booking, for example) are not.

Each delivery is a JSON message like this:

```json
{
  "id": "202f7988-764d-4287-b68c-ce301c42b27c",
  "event": "reservation.requested",
  "created_at": "2026-12-01T18:30:00+00:00",
  "site": { "name": "Your restaurant", "url": "https://example.com/" },
  "data": {
    "location": { "id": 12, "name": "Chandler's Wharf" },
    "date": "2026-12-05",
    "time": "19:00",
    "party": 4,
    "seating": "Inside",
    "occasion": "Birthday",
    "name": "Ann Guest",
    "phone": "555-0100",
    "email": "ann@example.com",
    "requests": "Window table, please",
    "newsletter": true
  }
}
```

## If something goes wrong

- The site never makes the guest wait. Deliveries are sent a moment later in the background (WP-Cron).
- If the other tool does not answer with a success code, the site tries once more after five minutes. After a second failure the message is dropped, and the log says so. Nothing is sent a third time.
- Up to 200 deliveries can wait at once. If the other tool is down for a long time and the queue fills, new ones are skipped and the log warns you once an hour. Your emails and **Messages** are not affected.
- If you clear the address, waiting deliveries are discarded.
- Deliveries need WP-Cron to run. If your host turned it off (`DISABLE_WP_CRON`), make sure a real scheduled job calls `wp-cron.php`, or deliveries will wait.

## Your guests' privacy

A webhook sends your guests' names, emails, phone numbers and messages to the tool you choose. That tool then holds its own copy. Before you turn it on:

- Add the tool to your privacy policy: what it receives and why.
- If a guest asks you to delete their data, delete it in the other tool as well. WordPress cannot reach copies held there.
- While a delivery is waiting, its details are held in a temporary record. It is deleted as soon as the delivery succeeds or is dropped, and when you deactivate the plugin. Anything left over expires after 24 hours. If your host uses a persistent object cache (Redis or Memcached), that record lives in the cache instead, and a cache flush or restart can remove it before it is sent; the log then says the delivery had expired or was cleared, so you can ask the guest to resend.

This is a practical note, not legal advice.

## For developers

### Checking the signature

Every request carries these headers:

| Header | Value |
| --- | --- |
| `X-Cobble-Event` | The event name, for example `reservation.requested` |
| `X-Cobble-Delivery` | A unique id for this message, the same on the retry |
| `X-Cobble-Timestamp` | Unix time the request was signed |
| `X-Cobble-Signature` | `sha256=` and the hex HMAC-SHA256 of `<timestamp>.<raw body>`, keyed with your secret |

In your receiver:

1. **Use the raw body** exactly as received. Re-encoding the JSON changes the bytes and the signature will not match.
2. **Compare in constant time**, as below.
3. **Reject old timestamps** (five minutes is a good window) so a captured request cannot be replayed.
4. **Skip ids you have already handled.** The first attempt may have worked even if the answer was lost, and the retry carries the same `X-Cobble-Delivery` with a fresh timestamp and signature.
5. **Answer with a 2xx code** once you have stored it. Anything else, including a redirect, counts as a failure.

PHP:

```php
function verify_cobble_webhook( string $secret, string $raw_body, array $headers, int $tolerance = 300 ): bool {
	$timestamp = $headers['X-Cobble-Timestamp'] ?? '';
	$signature = $headers['X-Cobble-Signature'] ?? '';
	if ( ! ctype_digit( $timestamp ) || abs( time() - (int) $timestamp ) > $tolerance ) {
		return false; // Missing or stale: could be a replay.
	}
	$expected = 'sha256=' . hash_hmac( 'sha256', $timestamp . '.' . $raw_body, $secret );
	return hash_equals( $expected, $signature );
}

// $raw_body = file_get_contents( 'php://input' );
```

Header names arrive in different forms depending on your server and framework (`X-Cobble-Timestamp`, `x-cobble-timestamp`, or `HTTP_X_COBBLE_TIMESTAMP` in `$_SERVER`). Pass them in the form the sample expects.

Node (18 or newer; header names arrive in lower case):

```js
import { createHmac, timingSafeEqual } from 'node:crypto';

export function verifyCobbleWebhook( secret, rawBody, headers, toleranceSeconds = 300 ) {
	const timestamp = headers[ 'x-cobble-timestamp' ] ?? '';
	const signature = headers[ 'x-cobble-signature' ] ?? '';
	if ( ! /^\d+$/.test( timestamp ) || Math.abs( Date.now() / 1000 - Number( timestamp ) ) > toleranceSeconds ) {
		return false; // Missing or stale: could be a replay.
	}
	const expected = 'sha256=' + createHmac( 'sha256', secret ).update( timestamp + '.' ).update( rawBody ).digest( 'hex' );
	const a = Buffer.from( expected );
	const b = Buffer.from( signature );
	return a.length === b.length && timingSafeEqual( a, b );
}
```

In Node, pass the raw request body (a `Buffer` or the unparsed string), not the parsed JSON.

### Hooks

| Hook | Purpose |
| --- | --- |
| `cobble_webhook_payload( $data, $event )` filter | Change the `data` of an event, or return an empty array to skip it. Runs before the event is queued. |
| `cobble_webhook_max_pending` filter | How many deliveries may wait at once. Default `200`. |
| `cobble_reservation_requested`, `cobble_inquiry_requested`, `cobble_contact_requested`, `cobble_room_booking_requested` actions | The form hooks the webhook listens to. See [Developers](developers.md#actions). |

### Limits

- One address and one secret for the whole site, and every event goes to it.
- Requests travel over HTTPS and are signed so the receiver can check them. The address must use port 443, 80 or 8080, which are the ports WordPress allows for outgoing requests. A receiver you host yourself on another port (n8n on 5678, for example) is rejected unless you add that port with the `http_allowed_safe_ports` filter, or put it behind a standard port.
- The address is checked when you save it and again when each delivery is sent, so a host that stops resolving later is logged and retried rather than lost.
