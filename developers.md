# Developers

Theme: Sage 11 (Acorn, Blade, Tailwind v4, Vite, Alpine.js), namespace `App`, text domain `cobbleandcandle`. Plugin: **Cobble & Candle Core**, WordPress Coding Standards, prefix `cc_`, text domain `cobbleandcandle-core`.

## Content model

| Type | Key | Notes |
| --- | --- | --- |
| Location | `cobble_location` | Public, `/locations/{slug}/`; meta `cobble_street`, `cobble_locality`, `cobble_phone`, `cobble_email`, `cobble_hours`, `cobble_holiday_hours`, `cobble_booking_mode`, `cobble_booking_url`, `cobble_order_url`, `cobble_lat`, `cobble_lng`… |
| Dish | `cobble_menu_item` | Taxonomies `cobble_menu`, `cobble_menu_section`; meta `cobble_price`, `cobble_variants`, `cobble_diet`, `cobble_flag`, `cobble_chef_pick`, `cobble_available_at` |
| Event | `cobble_event` | `/events/{slug}/`; meta `cobble_start`, `cobble_end`, `cobble_location`, `cobble_type`, `cobble_price`, `cobble_availability`, `cobble_booking_url`, `cobble_courses` |
| Room | `cobble_room` | `/rooms/{slug}/`; meta `cobble_price_night`, `cobble_price_weekend`, `cobble_min_nights`, `cobble_max_guests`, `cobble_units`, `cobble_beds`, `cobble_size`, `cobble_location`, `cobble_amenities`, `cobble_ical_import` (edit context only) |
| Booking | `cobble_booking` | Private; Editors+; meta `cobble_room`, `cobble_check_in`, `cobble_check_out`, `cobble_guests`, `cobble_status` (pending/confirmed/cancelled), `cobble_total`, `cobble_dinner` |
| Message | `cobble_message` | Private; Editors+; table requests, inquiries, contact |

All fields are registered post meta (REST-enabled, schema-sanitized) and drive the block-editor panels.

## Filters

| Filter | Default | Purpose |
| --- | --- | --- |
| `cobble_currency` | Settings → Theme Settings → Brand or `USD` | ISO currency for prices and schema |
| `cobble_money` | — | Format a price string |
| `cobble_booking_slot_step` | `30` | Minutes between table slots |
| `cobble_last_seating_offset` | `90` | Minutes before closing for the last table |
| `cobble_form_rate_limit` | `5` (`3` for rooms) | Submissions per IP per 10 minutes, per form |
| `cobble_client_ip` | `REMOTE_ADDR` | IP used for rate limits (see below) |
| `cobble_webhook_payload( $data, $event )` | — | Change a [webhook](webhooks.md) event’s `data`, or return an empty array to skip it |
| `cobble_webhook_max_pending` | `200` | Webhook deliveries that may wait at once |
| `cobble_pending_hold_hours` | `48` | Hours an unanswered room request holds its nights |
| `cobble_room_amenities` | 13 amenities | Amenity keys and labels |
| `cobble_contact_topics` | 5 topics | Contact topics (`sanitize_key`-safe keys → labels) |
| `cobble_current_location_slug` | — | Force the current location |
| `cobble_meta_description` | excerpt / defaults | Fallback meta description |
| `cobble_schema_enabled` | `true` | Turn off the plugin’s JSON-LD |
| `cobble_schema_nodes` | — | Add or change schema nodes on a page |
| `cobble_breadcrumb_trail` | theme crumbs | Breadcrumb items for BreadcrumbList |
| `cobble_room_pending_limit( $limit, $room_id )` | `10` | Unanswered requests a room can hold at once |
| `cobble_schema_restaurant( $node, $location_id )` | — | Change a location’s Restaurant JSON-LD |
| `cobble_event_schema( $schema, $event_id )` | — | Change an event’s Event JSON-LD |
| `cobble_menu_page_id( $id )` | detected menu page | Page used for Restaurant `hasMenu` links (`0` when none) |
| `cobble_seo_plugin_active( $active )` | detected | Treat an SEO plugin as active, which skips the fallback meta tags |
| `cobble_render_block( $html, $name, $attributes, $content, $block )` | `null` | Return a string to replace a Cobble & Candle block’s output; return `null` to let the theme’s Blade view render it |
| `cobbleandcandle/brand` | Settings → Theme Settings → Brand | Theme brand values |
| `cobbleandcandle/page_link` | page with the block | Resolve `/reservations/`, `/menu/`, `/rooms/`… links |

## Actions

| Action | Fires |
| --- | --- |
| `cobble_reservation_requested( $request, $sent, $stored )` | After a table request (keys **and** `*_label` values). `$sent`: the email went out. `$stored`: a copy was kept under Messages. When both are false the guest is shown an error |
| `cobble_room_booking_requested( $booking_id, $sent )` | After a room booking request |
| `cobble_inquiry_requested( $subject, $body, $email, $location )` | After a private dining inquiry was accepted (emailed or kept). Plain text, not HTML-escaped: escape on output |
| `cobble_contact_requested( $subject, $body, $email, $location )` | After a contact message was accepted. Same rules |
| `cobbleandcandle_fs_loaded` | After the licensing SDK has started (not fired when licensing is off) |
| `cobble_log( $entry )` | Every logged problem; hook error trackers here ([examples](troubleshooting.md#send-errors-to-sentry-or-slack)) |

## Editor breakpoints

`theme.json` sets the editor’s responsive previews and block visibility to the theme’s own widths: mobile up to 767 px and tablet up to 1023 px (`settings.viewport`, WordPress 7.1).

## Client IP behind a proxy

Only trust a proxy header when the origin accepts traffic from the proxy alone:

```php
add_filter( 'cobble_client_ip', function ( $ip ) {
	// Cloudflare: verify REMOTE_ADDR is a Cloudflare range before trusting the header.
	return $_SERVER['HTTP_CF_CONNECTING_IP'] ?? $ip; // phpcs:ignore
} );
```

## REST

`GET /wp-json/cobbleandcandle/v1/rooms/{id}/availability?from=YYYY-MM-DD&to=YYYY-MM-DD` (public): booked nights and prices, never guest data.

## WP-CLI

```bash
wp cobbleandcandle seed            # demo locations, menus, events, rooms (skips existing)
wp cobbleandcandle seed --update   # refresh existing demo posts
```

## Build and release

The theme is delivered as a built zip (Composer vendor folder and compiled assets included), so you do not need Node or Composer to use it. The source repository is private.

**The theme and the Core plugin update separately.** An update replaces the theme; the plugin stays as it was until an admin replaces it. When the theme needs a newer plugin than the one installed, wp-admin shows an update notice whose button installs the copy bundled inside the theme. If you call plugin functions from your own code, guard calls to anything new with `function_exists()` so an older plugin degrades instead of failing the page.
