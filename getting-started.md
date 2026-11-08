# Getting started

## Requirements

- WordPress **6.6+** and PHP **8.3+** (ask your host; most offer 8.3).
- “Post name” permalinks and a city timezone (Settings → General). The setup wizard reminds you.
- An email setup that works. Install [WP Mail SMTP](https://wordpress.org/plugins/wp-mail-smtp/) if your host’s mail is unreliable.

## Install

1. **Appearance → Themes → Add New → Upload Theme** → choose `cobbleandcandle.zip` → **Install** → **Activate**. If the upload fails with **413 Request Entity Too Large**, your host’s web server refuses big uploads: follow [Install when the host refuses the upload](troubleshooting.md#install-when-the-host-refuses-the-upload) instead. The same steps help if the upload stops at “Unpacking the package…” with a critical error: the host ran out of PHP time while copying the theme’s files.
2. Cobble & Candle Core installs itself the first time you open the dashboard after activating, and takes you to the setup wizard. The plugin is bundled inside the theme; it holds your locations, menus, events, rooms and bookings so they survive a theme change. If your host does not let WordPress install it automatically, a notice appears instead: click **Install & activate Cobble & Candle Core**.
3. You land in the **setup wizard**.

## Theme Settings (Settings → Theme Settings)

The menu down the left has three groups.

**Set up your site** takes a new site from install to open. Each step saves and leads to the next, and the progress bar counts them. You can stop and come back, and re-running a step never duplicates pages or menu links.

| Step | What you do |
| --- | --- |
| **Brand** | Your name, one-line description, what you run (restaurant, bar or tavern, rooms) and your timezone (pick your city so "Open now" and booking times are right and follow daylight saving). Below that, your logo, brand line (“Tavern & kitchen”), year established, cuisine, price range, currency, the optional address that receives new requests, a webhook for other systems, and the data options. At the bottom, **Back up, move or reset**: download your settings as a file, load that file on another copy of the site, or put the theme’s own settings back to their defaults. The file holds your place, brand fields, style and clock, and which blocks show; it never holds content, images, the webhook, service connections, newsletter settings (they include your API key) or the uninstall switch. A reset asks you to tick a box first. One Save button for the whole page. |
| **Look** | Pick a style (Lampwright, Ember & Arch, Ashlar & Iron, Daylight) and the 12 or 24-hour clock. Under each style is a **Colours** panel with a picker for every kind of colour, a readability list, and the **announcement bar**: one short line above the header for holiday hours or a closure, with an optional link and dates. |
| **Fonts** | Optional. Use fonts from the Google Fonts library for headings and text; your site downloads them once, so visitors never contact Google. See [Fonts](fonts.md). |
| **Content** | **Import the demo** (3 houses, 4 menus with photos, events, 4 rooms, a Journal with sample posts, a gallery, and Tavern and Bed & Breakfast home pages) to see everything working, or **Start with my own location**. |
| **Pages & menus** | One click creates the pages you need (Home, Menu, Reservations, Gallery, Our story, Contact, Private dining, and a Tavern or Bed & Breakfast page) and adds menu links. Pages you already have are never changed. **Customize pages and menus** lets you choose pages, sections and text first, or create the pages as drafts. |
| **Checklist** | A live list of what is finished and what is still to do, with a **Fix this** link for each item: what is needed before you go live (name and description, timezone, a location with hours, a menu, your pages and header menu, clean links, a clean health check) and what is worth doing (logo, a way to book or call, cuisine and price range, a social profile, a first journal post, a newsletter sign-up, https). It also has a **Where things live** table that says which screen to open for each job. |

**Features and services** are not steps. Open them in any order, whenever you need them. **Save** keeps you on the tab and says “Saved.”; they do not affect the setup progress.

| Tab | What you do |
| --- | --- |
| **Blocks** | Choose which of the theme's blocks show in the editor's block picker. See [Blocks](blocks.md). |
| **Connect services** | Paste your Eventbrite token to bring in your events. Booking and ordering links are set on each location. |
| **Newsletter** | Choose where sign-ups go (Mailchimp with an API key, any service's form address, a pasted Mailchimp or Constant Contact form, a sign-up page link, or a list kept on your site) and edit the form's text and fields. See [Newsletter, share buttons and social links](newsletter.md). |
| **Social & sharing** | Pick the share buttons for posts and events, and add your profile links for 21 networks. |

**Support** holds an overview (how to get help, what to try first, common questions, install notes and the system report) and the guides, which open on the right without reloading. **Create a ticket** under the menu opens a support form: it saves a ticket on your site with a reference number and emails it to support. The group that holds the tab you are on opens by itself; the others stay closed until you open them.

## Your first hour

- [ ] **Locations**: set opening hours and holiday hours for each house ([guide](locations-and-hours.md)).
- [ ] **Menus**: import your menu from a spreadsheet: Food & drink → Import / export ([guide](menus.md)).
- [ ] **Settings → Theme Settings → Brand**: upload your logo and check currency. Add your profile links under **Social & sharing**.
- [ ] **Tools → Cobble & Candle status**: send a test email; fix anything marked *Problem*.
- [ ] **Posts**: write your first Journal post, and choose the Journal page under Settings → Reading → Posts page ([guide](journal.md)).
- [ ] **Newsletter**: connect Mailchimp, Constant Contact or another service ([guide](newsletter.md)).
- [ ] **Rooms** (if you have them): set prices and paste your Airbnb / Booking.com calendar links ([guide](rooms-and-stays.md)).
- [ ] Replace demo photos with your own (Media → Add New, then set each dish, room or page photo).
- [ ] Delete the demo content you don’t need (Locations, Food & drink, Events, Rooms, and the Tavern and Bed & Breakfast pages).

## Licence and updates

The theme is sold with a licence key. Updates and support come with an active licence; if it expires, the theme and your site keep working, you just stop receiving updates and support. When you first activate the theme, enter the key from your purchase email on the licence screen that appears.

## Updating

With an active licence, updates are offered in the usual place (**Dashboard → Updates**, or **Appearance → Themes**). You can also upload the newer `cobbleandcandle.zip` the same way as the first install; WordPress offers **Replace current with uploaded**. Your content is untouched. Purge your page cache afterwards.
