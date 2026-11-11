# Troubleshooting

## Start with the Status page

**Tools → Cobble & Candle status** checks PHP and WordPress versions, theme and plugin, permalinks, timezone, HTTPS, scheduled jobs, the template cache, error display and failed emails, and shows the last 200 problems. Anything marked **Problem** or **Check** comes with what to do.

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Booking or contact emails don’t arrive | Host mail blocked or going to spam | Install [WP Mail SMTP](https://wordpress.org/plugins/wp-mail-smtp/), then **Send a test email** on the Status page. Requests are still saved under **Messages**. |
| /menu/, /rooms/ or /events/ show “Page not found” | Plain permalinks, or rules not refreshed | Settings → Permalinks → choose *Post name* → **Save** (twice is fine). |
| “Open now” is an hour off | UTC offset instead of a city | Settings → General → Timezone → pick your city. |
| Changes don’t show | Page cache | Purge LiteSpeed / WP Rocket / host cache. |
| Airbnb nights don’t block | Wrong link, or the platform’s feed is down | Use the platform’s **export** link; check the Status page log for “calendar feed could not be read”. |
| Blank page or “There has been a critical error” | PHP below 8.3, or a plugin conflict | Check the Status page and the error log below; temporarily deactivate other plugins. |
| “Cobble & Candle cannot start on this site” in wp-admin, or “was not activated” after you activate | The host runs PHP below 8.3, has a required PHP extension turned off, or the theme was installed from a GitHub “Source code” zip | Do what the message says: ask the host for PHP 8.3 or newer or to enable the listed extensions (json, mbstring, ctype, filter, tokenizer), or install the theme zip from your purchase. |
| A [webhook](webhooks.md) delivery never arrives | The address was not saved (an error showed), WP-Cron is off, or the receiver did not answer with a success code | Check **Settings → Theme Settings → Brand → Connections** still shows the address. Look for “Webhook” lines on the Status page. If the receiver rejects the signature, check it uses the raw request body. |
| Uploading the theme says **413 Request Entity Too Large** | The host’s web server refuses uploads over about 1 MB before WordPress sees them | Install through File Manager or SFTP instead: [steps below](#install-when-the-host-refuses-the-upload). |
| Uploading the theme stops at “Unpacking the package…” with “There has been a critical error” | PHP ran out of time (often 30 seconds) while WordPress copied the theme’s roughly 4,500 files. The error log says “Maximum execution time … exceeded”. A slow disk makes it more likely | Install by extracting the zip instead: [steps below](#install-when-the-host-refuses-the-upload). Or ask the host to raise PHP’s `max_execution_time` (120 seconds or more) and upload again. If a half-copied `wp-content/themes/cobbleandcandle` folder is left without a `style.css`, delete it first. |
| A page looks unstyled after an update | Old cached CSS | Purge the cache; hard-refresh the browser. |
| Dish fields missing | Old version | Update Cobble & Candle Core. Dishes open as a plain form (photo, description, price and sizes, diet and allergens, chef's pick, sold out, served at) under **Food & drink → Add menu item**. |

## Error logs

- **Event log (built in):** Tools → Cobble & Candle status → *Recent problems*. Failed emails (from any plugin), unreadable calendar feeds and import warnings. No guest details are stored.
- **PHP errors:** add to `wp-config.php` (above “That’s all, stop editing”):

  ```php
  define( 'WP_DEBUG', true );
  define( 'WP_DEBUG_LOG', true );      // writes wp-content/debug.log
  define( 'WP_DEBUG_DISPLAY', false ); // never show errors to visitors
  ```

  Reproduce the problem, then read `wp-content/debug.log` (via your host’s file manager). Cobble & Candle problems appear as `[Cobble & Candle] ERROR …`. Turn `WP_DEBUG` off again afterwards.
- **Your host’s error log** (cPanel / hPanel → Logs) catches fatal errors that happen before WordPress loads.
- **[Query Monitor](https://wordpress.org/plugins/query-monitor/)** (free plugin) shows PHP notices, slow queries and HTTP calls for the page you’re on.

## Send errors to Sentry or Slack

Every problem the plugin records fires the `cobble_log` action. Put one of these in a small must-use plugin (`wp-content/mu-plugins/cobble-alerts.php`):

```php
<?php
// Sentry (with the Sentry PHP SDK or the WP Sentry plugin installed).
add_action( 'cobble_log', function ( array $entry ) {
	if ( 'error' === $entry['level'] && function_exists( '\Sentry\captureMessage' ) ) {
		\Sentry\captureMessage( "[{$entry['source']}] {$entry['message']}" );
	}
} );

// Slack incoming webhook: alert on errors only.
add_action( 'cobble_log', function ( array $entry ) {
	if ( 'error' !== $entry['level'] ) {
		return;
	}
	wp_remote_post( 'https://hooks.slack.com/services/XXX/YYY/ZZZ', array(
		'body'     => wp_json_encode( array( 'text' => "Cobble & Candle: {$entry['source']}: {$entry['message']}" ) ),
		'headers'  => array( 'Content-Type' => 'application/json' ),
		'blocking' => false,
	) );
} );
```

Each `$entry` has `time`, `level` (`error`, `warning`, `info`), `source` (`mail`, `ical`, `import`…), `message` and a small `context` array (IDs, HTTP codes). Never personal data.

## The Journal, newsletter and sharing

- **The Journal is a plain list, or its page is missing.** Go to Settings → Reading, choose "A static page", and pick your Journal page as the Posts page. The demo import creates one when your site shows a static front page.
- **Newsletter sign-ups do not reach Mailchimp.** Open Theme Settings → Newsletter and save: it checks your API key and audience ID and shows what Mailchimp answers. The key ends with a dash and a code such as `-us19`; the audience ID is under Audience → Settings → Audience name and defaults. For other services check the form address and field names against the service's form code.
- **The pasted form does not show.** Only administrators who may post unfiltered HTML can save pasted code. A security plugin or `DISALLOW_UNFILTERED_HTML` also blocks it: use the form address or sign-up page link instead.
- **A share button or icon is missing.** Choose them under Theme Settings → Social & sharing. Footer icons show for each profile address you filled in.
- **Demo posts or photos are missing after a re-import.** Run `wp cobbleandcandle seed --update` from the site folder.

## Install when the host refuses the upload

**413 Request Entity Too Large** means the host’s web server (usually nginx) is refusing the file before WordPress or PHP sees it. Its default limit is 1 MB and the theme zip is about 7 MB. No PHP setting and no `.htaccess` file can change that, and some hosts do not let you change it at all, so install by extracting the zip on the server instead.

The same steps fix an upload that runs out of time. WordPress copies the theme’s roughly 4,500 files one at a time while it unpacks the zip, and a host with PHP’s time limit at 30 seconds and a slow disk can run out before it finishes. WordPress then shows “Unpacking the package…” followed by “There has been a critical error”, and the error log (see above) says “Maximum execution time … exceeded”. Extracting the zip on the server does the copying outside PHP, so it has no time limit. You can also ask the host to raise `max_execution_time` to 120 seconds or more and upload again.

**File Manager (for example Hostinger’s hPanel)**

1. Open your host’s File Manager and go to your site’s `wp-content/themes` folder.
2. Upload `cobbleandcandle.zip` there.
3. Extract it there. You should end up with `wp-content/themes/cobbleandcandle/style.css`. Then delete the zip.
4. In WordPress, go to **Appearance → Themes** and activate **Cobble & Candle**.
5. Cobble & Candle Core installs itself when you first open the dashboard. If it does not, click **Install & activate Cobble & Candle Core** in the notice, as in [Getting started](getting-started.md). Either way it installs the copy bundled inside the theme from the server, so the upload limit does not affect it.

**SFTP.** Upload the zip, then extract it with the File Manager or over SSH. You can upload the unzipped folder instead, but the theme has about 5,000 small files, so it is slow. Use binary mode: FTP in text (ASCII) mode silently corrupts a zip. Each release has a `cobbleandcandle.zip.sha256` file so you can check the upload arrived intact (`sha256sum -c cobbleandcandle.zip.sha256`).

**SSH.** `wp theme install /path/to/cobbleandcandle.zip --activate`.

Once the theme is installed, updates are not affected: WordPress downloads them itself, server to server.

**Developers:** to measure a host’s real limit without uploading anything, run `python3 scripts/probe-upload-limit.py yourdomain.com`. It sends only request headers and reports where the web server starts answering 413.

## The theme switches back to my old theme

You activate Cobble & Candle, open another admin page, and your previous theme is active again.

This happens on theme versions before 1.5.1 when the licence key has not been entered yet. Fix it in two steps:

1. Update to 1.5.1 or later: **Appearance → Themes → Add New → Upload Theme**, choose the new `cobbleandcandle.zip`, then **Replace current with uploaded**.
2. Activate the theme, then open **Appearance → Theme licence**. Paste the key from your purchase email and choose **Activate License**.

On 1.5.1 and later the theme stays active while you do this, even if you visit other admin pages first.

## “Cobble & Candle Core needs updating”

This notice means the theme is newer than the Core plugin on your site. Choose **Update Cobble & Candle Core** in the notice; it installs the copy bundled with the theme. If the button is missing (only administrators who can install plugins see it), upload the `cobbleandcandle-core.zip` that came with the theme: **Plugins → Add New → Upload Plugin**, then **Replace current with uploaded**. Your locations, menus, rooms and bookings are kept.

## Still stuck?

Copy the **System report** from the Status page (or the Support tab) and send it with a ticket (**Settings → Theme Settings → Create a ticket**) or by email: see [Support](support.md).
