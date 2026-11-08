# FAQ

**Do I need a page builder?** No. Everything is WordPress blocks and the Site Editor. No Elementor, no ACF.

**Can guests pay online?** Not in this version. Table and room bookings are requests you confirm; for deposits, send a payment link. For takeaway, link your online-ordering system (Toast, Square, ChowNow) on each location.

**I only have a bar / only a café. Is it too much?** Sections only appear when you have content for them. No rooms means no Rooms page, no Stay button, no “Stay with us”.

**Several restaurants?** Yes. Add each as a location. Guests choose a house in the header and hours, menus, phone and booking follow.

**Will my content survive a theme change?** Yes. Locations, menus, events, rooms and bookings live in the Cobble & Candle Core plugin and the database.

**Does it work with Yoast or Rank Math?** Yes. Restaurant, menu, event and room data join their schema graph.

**Translations and right-to-left?** Every string is translatable (`.pot` files included, WPML/Polylang compatible) and right-to-left languages are supported.

**Is it accessible?** It’s built and tested for WCAG 2.2 AA (keyboard, screen readers, contrast, 44 px targets, reduced motion). Your own photos, PDFs and colour changes matter too, so no theme can promise legal compliance by itself.

**Which caching plugins work?** LiteSpeed Cache, WP Rocket and host caches. “Open now”, the chosen location and form tokens are handled so cached pages stay correct.

**How do I get updates?** Upload the newer theme zip (WordPress offers to replace the current one). See [Getting started](getting-started.md#updating).

**Can an agency use it for clients?** Yes. Theme and plugin are GPL; see your store licence for support terms.

**Can I have a blog?** Yes. The Journal is a full blog with categories, a featured post, search, press quotes and diner write-ups, reading time, share buttons and a newsletter form. See [The Journal](journal.md).

**Which email services does the newsletter form work with?** Mailchimp directly with an API key; Brevo, MailerLite, Kit, Buttondown and most others through their form address; Constant Contact through its pasted form code or a link to its sign-up page; or keep the list on your site and download it. See [Newsletter, share buttons and social links](newsletter.md).

**Why does a dish, event or room not open in the block editor?** On purpose: those open as a plain form with every detail in one place. Developers can switch it back with the `cobble_classic_form_types` filter.

**Which social icons are used, and do they slow the site?** Simple Icons (CC0, public domain), drawn inline in the page: no icon font and no extra request. Pick your share buttons and profiles under Theme Settings → Social & sharing.
