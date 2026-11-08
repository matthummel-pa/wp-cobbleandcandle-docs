# Newsletter sign-ups

**Settings → Theme Settings → Newsletter** adds a subscribe form to every journal post (in the sidebar on a computer, at the end of the post on a phone), to the Journal page, and anywhere you add the **Newsletter Sign-up** block (a page, the home page, the footer). Everything about it is set on that tab.

## Where sign-ups go

- **Mailchimp: connect with an API key.** Our form adds people straight to your audience. In Mailchimp open your profile menu, Extras, API keys, and create a key; then Audience, Settings, Audience name and defaults, and copy the Audience ID. Paste both, save, and the page tells you the audience name if it connected. Leave "Ask people to confirm by email" on if your country requires it. The key stays on your site and is never shown on a page.
- **Any service: send our form to its form address.** Open your service's embedded or HTML form option and copy the form's address (the `action`) and the name of the email field. For Mailchimp that is the address with `list-manage.com`, the field `EMAIL`, and the hidden fields `u`, `id` and the one starting with `b_` (the spam trap). This also works for Brevo, MailerLite, Kit and Buttondown.
- **Paste a form made in Mailchimp or Constant Contact.** In Mailchimp use Audience, Signup forms, Embedded forms. In Constant Contact use Contacts, Sign-up forms, then publish and choose the embed code. Paste it in. The form then looks and works the way the service made it, so the text and field settings do not apply. Only administrators who may post unfiltered HTML can paste code, because it can contain scripts.
- **Link to a sign-up page.** A button to your hosted sign-up page (Constant Contact's share link, or Mailchimp's hosted form).
- **Keep the list on this site.** Addresses are collected here. Download them as a CSV to import wherever you send email, and only email people who agreed. They can be exported or erased with WordPress's privacy tools.

## Sign-ups from the reservation form

A guest who ticks the newsletter box on the table request form is added to your list too when you use *Mailchimp with an API key* or *Keep the list on this site*. See [Reservations](reservations.md#the-newsletter-tick-box).

## Tracking

When someone signs up through one of our own forms (Mailchimp API or this site), the page pushes `newsletter_signup` to the data layer for Google Tag Manager. With JavaScript off the page reloads with `?newsletter=ok` in the address. See [Click tracking](tracking.md).

## The form's text and fields

Change the heading, short text, button, thank-you message, problem message, field labels and the agreement text. Turn first name, last name and the agreement box on or off. Choose to show it in post sidebars and on the Journal page.

## Good to know

- Our own forms (Mailchimp API and this site) send without reloading the page, and fall back to a normal form if JavaScript is off. They block spam with a hidden field and a limit on sign-ups from one connection.
- A person must tick the agreement box if you turn it on. Mention your privacy policy in its text.
- You are responsible for emailing only people who agreed, and for including an unsubscribe link in what you send.

## Share buttons and social profiles

**Settings → Theme Settings → Social & sharing** lets you choose which share buttons appear on journal posts and events (Facebook, X, WhatsApp, Telegram, Threads, Email, Copy link and the phone's own share button), and whether the network names show beside the icons. The same tab holds the web address of each social profile you use, in 21 networks. Filled ones are linked with their icon in the footer. Icons are drawn in the page itself (Simple Icons, CC0), so nothing extra loads. The logos belong to their brands: use them to link to your own profiles or to share, as each brand's guidelines allow.
