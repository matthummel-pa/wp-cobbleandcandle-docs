# Click tracking

The theme can tell Google Tag Manager (or any tag tool) what visitors click, without loading any analytics code of its own. It does two things when someone clicks a tracked button or link:

1. It adds a message to the page's `dataLayer` (the list Google Tag Manager reads): `{ event: "event_calendar_add", method: "google", event_id: "47" }`.
2. It fires a `cobble:track` event on the page, so a developer can listen for it with `document.addEventListener( 'cobble:track', ... )`.

Nothing is sent anywhere by the theme, and the values hold only ids, names and places: never a name, email or any guest detail. You still need Google Tag Manager or Google Analytics installed (for example with Site Kit or a GTM plugin) for the messages to go anywhere.

## What is tracked

| Event name | When | Values sent with it |
| --- | --- | --- |
| `event_register_click` | A visitor clicks "Get tickets on…" (Eventbrite, Meetup and similar) on an event page or the featured event | `provider`, `event_id`, `placement` |
| `event_signup_click` | A visitor clicks the button that jumps to the sign-up form | `event_id`, `placement` |
| `event_facebook_click` | A visitor clicks "View the Facebook event" | `event_id`, `placement` |
| `event_calendar_add` | A visitor clicks Google Calendar or the Apple and Outlook file | `method` (`google` or `ics`), `event_id` |
| `event_share` | A visitor uses a share button on an event | `method` (`facebook`, `x`, `whatsapp`, `telegram`, `threads`, `email`, `copy_link`, `native`), `event_id` |
| `post_share` | A visitor uses a share button on a journal post | `method` (as above), `event_id` (the post's ID) |
| `location_call` | A visitor taps the phone number on an event page | `location_slug`, `placement` |
| `newsletter_signup` | A visitor signs up through our own newsletter form (Mailchimp with an API key, or the list kept on this site) | `placement` (`post`, `journal` or `band`) |

## Form results

A form that sends the visitor back to the page cannot be counted as a click. Watch the address instead:

| Form | Address contains | Meaning |
| --- | --- | --- |
| Event sign-up | `?signup=sent` | A sign-up was sent |
| Event question | `?question=sent` | A question was sent |
| Newsletter (JavaScript off) | `?newsletter=ok` | A sign-up worked |

## Set it up in Google Tag Manager

1. **Variables**: create *Data Layer Variable* variables for the values you want (for example `event_id`, `method`, `provider`).
2. **Trigger**: create a *Custom Event* trigger. In *Event name* type the name from the table (for example `event_calendar_add`). To catch all of a family at once, tick *Use regex matching* and type `event_.*_click|event_calendar_add|event_share`.
3. **Tag**: create a *Google Analytics: GA4 Event* tag, use the same name as the event, add the variables as parameters, and attach the trigger.
4. Use GTM's *Preview* mode to click through your pages and watch the messages arrive before you publish.

For form results, use a *Page View* trigger with a condition *Page URL contains* `?signup=sent`.

## Privacy

The messages carry no personal data. Check your own consent setup (for example Google consent mode) decides whether the tags that receive them run.
