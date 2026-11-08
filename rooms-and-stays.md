# Rooms & stays

Turn on rooms by adding one under **Rooms & stays → Add room**. The *Rooms* page, the home-page **Stay with us** section and the mobile **Stay** button appear automatically when you have rooms.

## A room

**Rooms & stays → Add room** is a plain form, not the block editor. At the top, the room's **Photo** and a one-line **Summary**; then the **Description**; then groups that open and close. Anything you leave empty does not show on the page.

- **Rates & capacity**: price per night, an optional Friday & Saturday price, minimum nights, maximum guests, **how many rooms of this kind** (3 identical doubles = 3; the calendar only shows a night as booked when all are taken), beds, size and the house.
- **At a glance**: check-in and check-out times, bathroom, view, and a short list of what makes the room special.
- **Amenities**: tick what the room has (ensuite, bath, breakfast, fireplace, step-free and more).
- **Photos**: add pictures with captions. They show as a mosaic under the room's name and open in a full-screen viewer.
- **Breakfast and policies**: breakfast details, house rules (one per line) and your cancellation policy.
- **Nearby and questions**: places guests walk to, and answers to what they usually ask (parking, check-in, dogs, dinner).
- **Calendar sync**: see below.

On the room page guests see the photos, an at-a-glance strip, the details above, and the booking calendar and request form beside them.

## How booking works

1. The guest picks dates on the calendar (only free nights can be chosen; minimum stay and weekend prices are applied), sees the total, adds an optional **dinner on the first night**, and sends a **request**.
2. Those nights are held as **pending**. You get an email; the guest gets “We have your request”.
3. In **Rooms & stays → Bookings**, hover the booking and click **Confirm** (emails the guest “Your stay is confirmed”) or **Cancel** (emails a polite decline).
4. A request you don’t answer within **48 hours** lapses and frees the nights.
5. A room holds at most **10 unanswered requests** at once. After that, new requests show “Too many requests from this connection. Please wait a few minutes or call us.” until you confirm, cancel or let some lapse. This stops fake requests from blocking your calendar. Developers can change the number: see [Developers](developers.md#filters).

No card is taken. Ask for a deposit by phone or a payment link if you need one.

**Phone bookings:** Bookings → Add booking. If the nights clash, it’s saved as *Pending* with a warning.

## Sync with Airbnb, Booking.com and Vrbo

- **Their bookings → your site:** on the room, under **Calendar sync**, click *Add calendar* and paste each platform’s **export** iCal link. They’re checked every hour; those nights show as booked here.
- **Your bookings → their calendars:** copy the **Calendar export** link from the room’s sidebar and paste it into each platform’s *import calendar* setting.
- If a platform’s feed can’t be read, its last known nights stay blocked (and the problem shows on the Status page).
- Keep these links private: they contain secret keys.
- Only **Editors and Administrators** can add or change a calendar link, because the site fetches those links every hour.

## Prices on Google

Room pages tell search engines the room, occupancy, bed and nightly price (HotelRoom + Offer).
