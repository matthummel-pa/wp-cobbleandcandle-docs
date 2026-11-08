# The Journal (blog)

The Journal is your news and stories page: new menus, people in the kitchen, recipes, event write-ups, press and diner reviews. It uses ordinary WordPress **Posts**, so scheduling, categories, tags, comments, revisions and an RSS feed all work.

## Writing a post

**Posts → Add New**. Give it a title, a short **Excerpt** (shown on cards and under the title), a **Featured image** and a category. Write the body in the editor: headings, lists, images and quotes all work. The page shows the reading time, your name, the date, share links, tags, an author box (add a short bio under **Users → Profile**), newer and older posts, and more from the same category.

Tick **Stick to the top of the blog** (in the post's Summary panel) to make it the featured post at the top of the Journal.

## Categories

The demo starts with: News, Menu and seasons, Behind the pass, Events, Recipes, In the press and Diner write-ups. Add or rename them under **Posts → Categories**. The Journal shows each one as a filter chip with its post count.

## Press and diner reviews

On any post, open **Press or diner review (optional)** in the sidebar and add who said it (a publication, or a diner's first name), a pull quote, a rating out of 5 and a link to the full review. Posts in **In the press** and **Diner write-ups** appear as quote cards with stars on the Journal and the Story page, and the quote shows at the top of the post. Always ask a guest before you use their words.

## Sidebar, sharing and newsletter

On a post, the sidebar holds an **In this post** list of links (from your headings, when there are three or more), the share buttons, and the newsletter form. On a phone these move to the end of the post. Choose the share buttons under **Settings → Theme Settings → Social & sharing**, and the newsletter service and the form's wording under **Newsletter** ([guide](newsletter.md)).

## What guests can do

Search the journal, filter by category, switch between newest and oldest, page through older posts, subscribe by RSS and share a post. Category, tag, author and search pages use the same design.

## Setting it up

Import demo content to add a Journal page and sample posts, or create a page called Journal and choose it under **Settings → Reading → Posts page**. Add it to your menu. The Story page can show press quotes, diner write-ups and your latest posts with the **Press and Diner Quotes** and **Latest from the Journal** blocks.

## For developers

`cobble_journal_categories` filters the starting categories. `cobble_journal_post( $post )` returns a post's card data. `cobble_schema_post( $id )` makes the BlogPosting structured data.

## Search engines and sharing

Every post gets, without a plugin: a search title and description, a canonical address, Open Graph and Twitter tags (with the photo's size and description) and article details (published and updated time, section, tags, author). It also gets BlogPosting structured data (headline, photos, author, publisher, word count, reading time, keywords) and breadcrumbs (Home, Journal, category, post). If Yoast, Rank Math or All in One SEO is active, they take over the titles, descriptions and sharing tags and the theme only adds its own details.

Open **Search and sharing (optional)** in a post's sidebar to write your own search title (about 60 characters) and description (up to 155). Leave them empty to use the post title and the excerpt. Good habits: one clear question or promise in the title, the answer in the first paragraph, a photo with descriptive alt text, headings (h2, h3) that read like the questions people ask, and two or three links to your menu, events or other posts.

## On the post page

A thin progress bar, a photo with its caption, an **In this post** list of links built from your h2 and h3 headings (shown when there are three or more), share links, a Reserve a table card (turn it off or change its words in the Journal Post block's settings), the author, newer and older posts, and more from the same category.
