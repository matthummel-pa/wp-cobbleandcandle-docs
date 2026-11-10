# Locations & hours

Each **location** (“house”) has its own address, phone, email, hours, booking mode and map. With more than one, guests pick a house in the header and the whole site follows: hours, phone, directions and the booking form.

## Add or edit a location

**Locations → Add location.** In the editor's right-hand settings panel (the sidebar), open:

- **Address & contact**: street, town, phone, bookings email (requests for this house go here), map coordinates (optional; used for Google’s map pin).
- **Opening hours**: open and close per day, or *Closed* (closing after midnight, such as 01:00, is fine), and **holiday hours**: specific dates that override the week (Christmas Eve 17:00–21:00, New Year’s Day closed).
- **Reservations & ordering**: *Booking form on this site*, *OpenTable widget*, *Resy widget* or *Bookings by phone*, plus booking and online-ordering links.
- **Getting there**: parking, transit and accessibility notes shown on the location page and Reservations.
- **Payments accepted**: what this house takes, if it differs from the site-wide list ([below](#payments-accepted)).

## Payments accepted

Each location can say what it takes: edit the location and open **Payments accepted** in the sidebar. Tick the methods that house accepts and, if useful, add a short note (“Cards only, no cash”). They show on that location's page and in its tab on the Locations page, as plain text under the hours and notes, and in its search listing.

Leave every box empty and the location shows the list from **Settings → Theme Settings → Brand → Payments** instead, so a site where every house takes the same payments only has to set it once. A location with its own list shows exactly that list and its own note (the site-wide note is not borrowed).

## “Open now”

The header shows *Open · closes 11pm*, *Closing soon*, or *Closed · opens 5:30pm*. It’s worked out in the visitor’s browser from your hours and your site timezone, so it stays correct even on cached pages. Times follow **Settings → General → Time format** (12- or 24-hour).

**Wrong day or time?** Set a city (not a UTC offset) under Settings → General → Timezone.

## Table slots

The native booking form offers times from opening until **90 minutes before closing**, every 30 minutes. Developers can change both (see [Developers](developers.md)).
