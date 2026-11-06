# Booking, ordering and other services

Cobble & Candle works with the booking, ordering and room services most restaurants, taverns and inns already pay for. You do not need an API key or a partner account. You paste the link each service gives you, and the theme names the button after the service, shows the booking page in a frame when the service allows it, and sends guests to the service's own page when it does not.

## Where you set it up

Open a location (**Locations → the house**) and find **Reservations & ordering** in the sidebar.

| Field | What to paste |
| --- | --- |
| **How guests book** | Pick the way this house takes bookings (below). |
| **Booking page link** | The page guests book on at your reservation service. |
| **Order online link** | Your main ordering page. |
| **More ordering links** | Add one row for each other service: a second ordering system, DoorDash, Uber Eats, Grubhub. |
| **Menu PDF link** | A PDF menu, if you keep one. |

## How guests book

- **Booking form on this site.** The theme's own request form with real time slots. You confirm each request.
- **OpenTable widget** and **Resy widget.** Paste the booking page link. It loads only when a guest taps **Check availability**.
- **Another booking system.** For SevenRooms, Tock, Yelp, Toast, Tablein, Quandoo, TheFork, Eat App, ResDiary and any other service. Paste the booking page link. The button reads "Book via SevenRooms" (or the service the link belongs to).
- **Bookings by phone.** Shows your number and email.

### Frame or link?

Some services do not allow their booking page to be shown inside another site. After you save a booking link, the theme checks the page once, in the background. If the service allows framing, guests book on your page. If it does not, the card shows a clear **Book on {service}** button and your phone number instead of a blank frame. You do not have to do anything. If the check cannot reach the page, the theme tries to frame it and always shows a link beside it.

## Online ordering and delivery

Add your main link under **Order online link**, then any others under **More ordering links**. Each button is named after its service ("Order on Toast", "Order on DoorDash") unless you type your own button text. The menu page shows every button for the house the guest has chosen, and the header and mobile bar use the main link. Google also learns about each link: they are added to your page's structured data as ordering actions.

## Rooms and stays

Room calendars sync both ways with Airbnb, Booking.com, Vrbo and any other service that offers an iCal link. See [Rooms & stays](rooms-and-stays.md).

## Services the theme recognises

Anything not on this list still works as a plain link.

| Kind | Services |
| --- | --- |
| Reservations | OpenTable, Resy, SevenRooms, Tock, Yelp, Tablein, Quandoo, TheFork, Eat App, ResDiary, Toast |
| Ordering | Toast, Square, ChowNow, Olo, Slice, MenuDrive, Popmenu, Clover, Revel, Tock |
| Delivery | DoorDash, Uber Eats, Grubhub |
| Hotel and inn booking | Cloudbeds, Little Hotelier, Lodgify, Beds24, Sirvoy, Mews, Guesty, Hostaway, Airbnb, Booking.com, Vrbo |
| Tickets and private events | Eventbrite, Ticket Tailor, Tripleseat, Tock, SevenRooms |

## Connect Eventbrite

Eventbrite is the one service you can connect with a key, so your events appear on the site without retyping them.

1. Open **Settings → Theme Settings → Connect services**.
2. In your Eventbrite account, open the API keys page and copy your **private token**.
3. Paste it and choose **Connect and import events**.

Your upcoming events arrive in **Events** as **drafts**. Check each one, add a photo and menu if you like, then publish. Each event's booking link is its Eventbrite page. After that, the date, time, link and seats follow Eventbrite every day (or when you choose **Sync now**). Your title, description and price are never changed, and cancelled events are skipped.

The connection is read-only: the site never creates or edits anything in Eventbrite. **Disconnect** removes the token from this site and your imported events stay. To cancel the token completely, also delete it on your Eventbrite API keys page.

## What this does not do

- It does not read live availability from a service. Guests see availability on the service's own page.
- It does not copy your menu from a service. Export your menu from the service as a spreadsheet and use the [menu import](menus.md).
- Brand names belong to their owners. Cobble & Candle is not affiliated with these services.

## For developers

- `cobble_providers` filter: add, remove or rename a service. Each has a label, its kinds and the hosts that identify it.
- `cobble_reservation_requested` action: send native table requests to a CRM or booking system. To pass requests on without code, use a [webhook](webhooks.md).
- `cobble_provider_for_url( $url )` returns the service for a link. `cobble_order_links( $location_id )` returns a house's ordering links.
