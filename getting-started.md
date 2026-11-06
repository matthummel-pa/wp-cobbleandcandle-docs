# Getting started

## Requirements

- WordPress **6.6+** and PHP **8.3+** (ask your host; most offer 8.3).
- “Post name” permalinks and a city timezone (Settings → General). The setup wizard reminds you.
- An email setup that works. Install [WP Mail SMTP](https://wordpress.org/plugins/wp-mail-smtp/) if your host’s mail is unreliable.

## Install

1. **Appearance → Themes → Add New → Upload Theme** → choose `cobbleandcandle.zip` → **Install** → **Activate**. If the upload fails with **413 Request Entity Too Large**, your host’s web server refuses big uploads: follow [Install when the host refuses the upload](troubleshooting.md#install-when-the-host-refuses-the-upload) instead. The same steps help if the upload stops at “Unpacking the package…” with a critical error: the host ran out of PHP time while copying the theme’s files.
2. Cobble & Candle Core installs itself the first time you open the dashboard after activating, and takes you to the setup wizard. The plugin is bundled inside the theme; it holds your locations, menus, events, rooms and bookings so they survive a theme change. If your host does not let WordPress install it automatically, a notice appears instead: click **Install & activate Cobble & Candle Core**.
3. You land in the **setup wizard**.

## The setup wizard (Settings → Theme Settings)

| Step | What you do |
| --- | --- |
| **Brand** | Your name, one-line description, what you run (restaurant, bar or tavern, rooms) and your timezone (pick your city so "Open now" and booking times are right and follow daylight saving). Below that, your logo, brand line (“Tavern & kitchen”), year established, cuisine, price range, currency, social profiles, the optional address that receives new requests, and the data options. At the bottom, **Back up, move or reset**: download your settings as a file, load that file on another copy of the site (a staging copy, a rebuild), or put the theme’s own settings back to their defaults. The file holds your place, brand fields, style and clock, and which blocks show. It never holds content, images, the webhook, service connections or the uninstall switch, and a file can’t change those either. When you load a file you tick which parts to apply. A reset clears the brand fields and logo, goes back to the default style and shows every block again, and asks you to tick a box first; your name, description, timezone, content and connections are kept. One Save button for the whole page. |
| **Look** | Pick a style (Lampwright, Ember & Arch, Ashlar & Iron, Daylight) and the 12 or 24-hour clock. Under each style is a **Colours** panel with a colour picker for every kind of colour: page background, cards, text, muted text, accent, secondary colour, hero background and text, menu board background and text, and footer background and text. Leave a box empty to keep the style’s own colour; **Reset** puts one back. A small preview and a readability list update as you pick (easy to read, hard to read when small, or too faint). A colour that would make text too faint to read is not saved, and nothing is saved until every colour is right. Shades that depend on your choices are worked out for you: button text is black or white, and the hero, footer, focus ring and small labels stay readable on their backgrounds. It also has the **announcement bar**: one short line above the header for holiday hours, a special or a closure, with an optional link, an optional start and end date (both days included, in your timezone) and a close button for visitors. It shows only while it is live, hides itself after the end date even on a cached page, and comes back for everyone when you change the message. Leave the message empty for no bar. |
| **Fonts** | Optional. Use fonts from the Google Fonts library for headings and text. Your site downloads them once, so visitors never contact Google. See [Fonts](fonts.md). |
| **Content** | **Import the demo** (3 houses, 4 menus, events, 4 rooms, plus Tavern and Bed & Breakfast home pages) to see everything working, or **start with your own location**. |
| **Pages & menus** | One click. A short summary says what will happen (which pages are created, which are already there, which menu links are added), and **Create pages and menus** does it. Pages you already have are never changed, and menus only gain the links they are missing. To change anything first, open **Customize pages and menus**: tick which pages to create (Home, Menu, Reservations, Gallery, Our story, Contact, Private dining, and a Tavern or Bed & Breakfast page), choose the sections of each new page and type your own heading, intro and text, create the pages as drafts to read first, and see what each menu will get. Afterwards a summary lists what was created, kept and added, with links to edit each page. |
| **Blocks** | Choose which of the theme's blocks show in the editor's block picker, one group at a time. Optional; see [Blocks](blocks.md). |
| **Connect services** | Optional. Paste your Eventbrite token to bring in your events, or jump to Locations to paste booking and ordering links. |
| **Done** | A live checklist of what is finished and what is still to do, with a **Fix this** link for each item. It is worked out from your site as it is now, so it stays right when you change something elsewhere. It is split into what is needed before you go live (name and description, timezone, a location with opening hours, a menu, your pages and header menu, clean links, and a clean health check) and what is worth doing (logo, a way to book or call, cuisine and price range, a social profile, https). |

Each step saves on its own; you can stop and come back. Re-running it never duplicates pages or menu links.

Settings → Theme Settings has a menu down the left with two toggles, **Set up your site** (the eight steps above) and **Support**. Both start closed; each shows where you are. **Support** holds an overview (how to get help, what to try first, install notes and the system report) and the guides, which are read from the documentation site and open on the right without reloading the page. Under the toggles, **Create a ticket** opens a support form: it saves a ticket on your site with a reference number and emails it to support, and replies come to the address you give.

## Your first hour

- [ ] **Locations**: set opening hours and holiday hours for each house ([guide](locations-and-hours.md)).
- [ ] **Menus**: import your menu from a spreadsheet: Food & drink → Import / export ([guide](menus.md)).
- [ ] **Settings → Theme Settings → Brand**: upload your logo, add social profiles, check currency.
- [ ] **Tools → Cobble & Candle status**: send a test email; fix anything marked *Problem*.
- [ ] **Rooms** (if you have them): set prices and paste your Airbnb / Booking.com calendar links ([guide](rooms-and-stays.md)).
- [ ] Replace demo photos with your own (Media → Add New, then set each dish, room or page photo).
- [ ] Delete the demo content you don’t need (Locations, Food & drink, Events, Rooms, and the Tavern and Bed & Breakfast pages).

## Licence and updates

The theme is sold with a licence key. Updates and support come with an active licence; if it expires, the theme and your site keep working, you just stop receiving updates and support. When you first activate the theme, enter the key from your purchase email on the licence screen that appears.

## Updating

With an active licence, updates are offered in the usual place (**Dashboard → Updates**, or **Appearance → Themes**). You can also upload the newer `cobbleandcandle.zip` the same way as the first install; WordPress offers **Replace current with uploaded**. Your content is untouched. Purge your page cache afterwards.
