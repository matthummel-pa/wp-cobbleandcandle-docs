# Menus

A **menu** (Tasting, À la carte, Cellar, Sunday lunch…) has **sections** (To begin, Mains, Puddings…), and each **dish** belongs to one or more menus and sections.

## Add or edit a dish

**Food & drink → Add menu item** (or **All menu items**, then the dish). It is a plain form, not the block editor, with everything in one place under the name:

- **Photo** (click **Choose photo**; **Remove photo** takes it off) beside the **Description**, the line shown under the dish's name. The photo shows in the *Photos* layout of the menu page.
- **Price**: a price, or **Sizes** (glass and bottle, starter and main), each with its own price.
- **Diet and allergens**:
  - **Dietary**: vegetarian, vegan, gluten-free, spicy. These drive the menu filters and the key.
  - **Contains (allergens)**: tick the major allergens in the dish: milk, eggs, fish, shellfish, tree nuts, peanuts, wheat, soy, sesame (the nine named by the US FDA). They show under the dish as “Contains milk, shellfish” and drive the **Hide dishes containing…** filter. **A dish with nothing ticked has no allergen information; it is not a promise that it is allergen-free.** Always keep your allergy note on the menu, and tell staff to ask guests about allergies.
  - **Calories**: optional. Shown on each dish when you turn on *Show calories* in the Full Menu block's settings.
- **On the menu**:
  - **Flag**: a short badge such as *Chef’s pick* or *Popular*.
  - **Show in Chef’s picks**: adds the dish to the Chef’s picks cards at the top of the menu page and to the Signature dishes block.
  - **Sold out today**: dims the dish's price and adds a “Sold out today” label until you untick it. It also tells search engines the dish is out of stock.
  - **Served at**: limit a dish to some houses (none ticked = every house).
  - **Order in its section**: lower numbers come first; dishes with the same number are listed by name.

In the right-hand column, tick the **Menus** and **Menu sections** the dish belongs to (add new ones there too).

## Import a whole menu from a spreadsheet

**Food & drink → Import / export.**

1. Click **Download a sample file** (or **Export menus** to start from what you have).
2. Edit it in Excel, Numbers or Google Sheets. Columns: `menu, section, name, description, price, sizes, diet, flag, chef_pick, menu_intro, allergens, calories, sold_out, menu_served, menu_order_url`. Only **section** and **name** are required (plus **menu**, unless every dish goes in one menu).
   - `sizes`: `Glass: $12 | Bottle: $48`
   - `diet`: `v, vg, gf, spicy`, or words like `vegan, gluten-free`
   - `allergens`: `milk, eggs, tree nuts`
   - `chef_pick`, `sold_out`: `yes` / `no`
   - `menu_intro`, `menu_served`, `menu_order_url` describe the whole menu; one row per menu is enough.
   - **Spreadsheets from another system:** common headings are understood (`category` or `categories` for section, `item` or `item name` for name, `dietary` for diet, `cal` or `kcal` for calories, and similar). With no `menu` column, every dish goes into a menu called *Menu*. Check the preview before you import: it lists anything it could not read.
3. Save as CSV and upload. You’ll see a **preview**: which dishes are new, which will update, and any rows with problems.
4. Click **Import these dishes**.

Dishes are matched by **name within the same menu and section**. Nothing is ever deleted. Columns you leave out of the file are left alone on existing dishes, and unpublished dishes stay unpublished. Tick *Leave existing dishes as they are* to only add new ones.

## Menu details

**Food & drink → Menus → (a menu)** has three fields:

- **Intro**: one line under the menu's name.
- **Served**: when it is available, for example “Brunch · Sat and Sun, 10 am to 2 pm”.
- **Order this menu online**: a link just for this menu (a takeout or catering menu on Toast, ChowNow, DoorDash and so on). It shows as a button named after the service. Leave it empty to use each location's ordering links.

## What guests can do on the menu page

- **Search** by dish or ingredient.
- **Filter by diet** (all chosen diets must match) and **Hide dishes containing…** an allergen. Dishes with no allergen details stay on the list, and the page tells guests to ask their server.
- Switch between **List** and **Photos**. Photos shows each dish's featured image on a card (dishes with no photo stay as text cards). The choice is remembered on that device.
- **Print this menu** or **Print all menus**: a clean black-and-white page with your name, the location, sections in two columns, the key, your allergy note and “Menu updated” date. The site header, footer, filters and buttons are left off, and Chef's picks are not repeated. Guests can also “Save as PDF” from the print window.
- **Order online** at the top and in the order card at the bottom, using the location's ordering links.

## Customise the Full Menu block

In the page editor, select the **Full Menu** block. In the sidebar you can choose the layout the page opens in (list or photos), 1 or 2 columns in the list layout, and turn each of these on or off: search, the allergen filter, the List / Photos switch, the print buttons, the Order online button at the top, calories, and “Menu updated”.

## Ordering online

The theme links to your ordering service; it does not take orders itself. Add links on each location (**Locations → (location) → Reservations & ordering**) or on a single menu. It recognises Toast, Square, ChowNow, Olo, Slice, MenuDrive, Popmenu, Clover, Revel, Owner.com, Menufy, SpotOn, DoorDash, Uber Eats, Grubhub and Tock and names the button after them (“Order on Toast”). Any other link shows as “Order online”. A developer can add more services with the `cobble_providers` filter.

## A menu feed for apps and screens

`/wp-json/cobbleandcandle/v1/menus` is a public, read-only JSON feed of your menus: dishes, prices, sizes, dietary tags, allergens, calories, photos and sold-out state, with each menu's served hours and ordering link. Add `?location=chandlers-wharf` to get only what one house serves. It carries what the menu page already shows to anyone, so it needs no login. Ordering apps, digital menu boards, kiosks and search tools can read it. Search engines also get the menu as structured data (diets, prices, calories, and sold-out dishes marked out of stock).

## Adding a dish

**Food & drink → Add menu item** is a plain form, not the page editor. Type the dish's name, click **Choose photo** to pick or upload its picture (you see it right there; **Remove photo** takes it off), write a short description, then fill in price, diet and allergens. Tick the dish's **Menu** and **Menu section** on the right. The **All menu items** list shows each dish's photo and price.
