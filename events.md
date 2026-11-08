# Events & private dining

## Events

**Events → Add event.** Events use a plain form, not the block editor, with everything in one place under the title:

1. A card with the event's **Photo** (click **Choose photo** to pick or upload one) beside a one-line **Summary**.
2. The **Description**.
3. The **Event details**, in groups that open and close.

Fill in as much or as little as you like. Everything past the title and the start time is optional, and a field you leave empty simply does not show. Groups that already have details open by themselves when you edit an event. Events you made earlier open in the same form with their current details, and their descriptions keep their formatting. If you would rather edit events with the block editor, a developer can return them to it (see [Developers](developers.md#filters)).

On the event page the summary is the one-line text under the title, the photo appears small beside the title, and the description sits under **About this event**.

### What you can add

| Group | Fields |
| --- | --- |
| **When & where** | Start and end, doors open, the house, how people attend (in person, online, or both) and an online link, the type, and a **status** (going ahead, postponed, cancelled) |
| **Tickets & registration** | Price, ticket types with their own prices and notes, seats, an availability note, when registration closes, a **tickets or registration link**, a **Facebook event link**, and **Take sign-ups on this page** |
| **About this event** | Hosted by, age or entry, what is included, **performers or guests** (a name, a note and a photo each), extra details (dress code, parking, allergens), refunds and changes, and questions and answers |
| **Menu for the evening** | The courses |

**Performers and guests.** Click **Add performer**, type a name and a short note (for example *Jazz trio, 8 pm*), and click **Choose photo** to pick a picture from the Media Library. The photo shows as a small round picture beside the name on the event page. A row with no photo shows just the name.

### Tickets and sign-ups

- **Tickets on another site (Eventbrite, Facebook, Meetup, Luma, Ticketmaster, DICE and similar).** Paste the link in **Tickets or registration link**. The button is named after the service ("Get tickets on Eventbrite"). Add the **Facebook event link** too and a "View the Facebook event" link appears under it.
- **Sign-ups on your own page.** Tick **Take sign-ups on this page** and leave the tickets link empty. Guests give a name, email, number of guests and any dietary or access needs. It is a request you confirm: nothing is charged, and no confirmation email is sent for you. Each one is emailed to the event's house (or the site admin) and kept under **Messages** as an *Event sign-up*. If you set **Seats**, the page counts the guests who have signed up here and shows "8 seats left", then closes sign-ups when it is full. It does not count tickets sold on another site.
- **Neither.** The card offers *Call the house to book*, or *Reserve a table*, as before.

When an event is **cancelled**, **postponed**, **sold out**, past its **registration closes** time or over, the page says so at the top, the booking button goes away, and the Events page shows a badge. Past events stay on their own page but drop off the list.

### Ask a question and FAQ

Every event page ends with **Questions about this event?** It emails the event's house and keeps the message under **Messages** as an *Event question*. Put the answers you give again and again under **Questions and answers**: they appear as a list that opens on a click or the keyboard.

### Share and calendar

The booking card has **Add to calendar** (Google Calendar, or a file for Apple and Outlook) and **Share this event**. You choose which share buttons show, and whether their names show beside the icons, under **Settings → Theme Settings → Social & sharing**: Facebook, X, WhatsApp, Telegram, Threads, email, copy link, and the phone's own share sheet where there is one. They are plain links: no share script is loaded. Facebook's own documentation no longer lists the simple share link the theme uses, so if it stops working, *Copy link* and the share sheet still do.

### Eventbrite and Facebook

The fields match what those services ask for (title, summary, description, date and doors, venue or online, ticket types, organizer, age, refund policy, FAQ). You can copy each across by hand today. The theme does not import from either service, because both need an account and an access key to read an event.

### Search engines

Each event is described to Google as an Event, including its status, whether it is in person or online, the host, ticket types with prices and the registration deadline, and the Facebook event. This only repeats what the page shows.

### Click tracking

Buttons on an event page send events to the data layer for Google Tag Manager: `event_register_click`, `event_signup_click`, `event_facebook_click`, `event_calendar_add` and `event_share`, each with the event's ID. Form results are not clicks: in GTM use a Page View trigger when the address contains `?signup=sent` or `?question=sent`. See [Click tracking](tracking.md) for the full list and how to set it up.

## Private dining

The **Private dining** block (on the home page in the demo) shows your rooms for groups and an inquiry form: date, guest range, occasion, house, message. Inquiries go to the house’s email and are saved under **Messages**.
