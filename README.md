# PickMyProtein

A free website that helps people in India work out their daily protein and calorie target and pick a protein powder.
It is **plain HTML, CSS and JavaScript**. There is nothing to install and no build step.

## What is in this folder

```
index.html              Home page with the quiz
about.html, contact.html, privacy.html, disclosure.html
guides.html             List of all guides
guide-*.html            One page per guide (10 guides)
js/products.js          DATA: your Amazon products, powder types and settings  <- you edit this most
js/quiz.js              CODE: the quiz, the calculations and the results page
css/theme.css           COLOURS and small style tweaks                          <- you edit this for looks
css/tailwind.css        Ready-made layout styles (please do not edit)
img/                    Product pictures (named after the Amazon code, e.g. B079SZJJDR.jpg)
templates/              guide-template.html, for adding a new guide
tools/check.js          Optional safety check
sitemap.xml, robots.txt For Google
favicon.svg, favicon.ico  The small orange "P" icon
```

## See it on your computer

1. Unzip the folder.
2. Double-click `index.html`. It opens in your browser and the quiz works.

(For a closer match to the live site you can also open a terminal in the folder and run `python3 -m http.server 8000`, then visit http://localhost:8000.)

## Common changes

### Change the Amazon associate ID
Open `js/products.js`, find `associateTag` at the top and change the value.

### Add or change a product
1. Open `js/products.js` and find the block for the powder type, for example `"whey-concentrate": [ ... ]`.
2. Copy one product block (from `{` to `}`) and paste it under the last one. Add a comma between blocks.
3. Fill in the fields:

| Field | What to write |
|---|---|
| `brand` | Brand name, for example `"MuscleBlaze"` (shown in capital letters) |
| `name` | Product name as it should appear on the card |
| `flavour` | `"raw"` for unflavoured, or `"flavoured"` |
| `flavourLabel` | Text shown on the card, for example `"Unflavoured"` or `"Chocolate"` |
| `asin` | The 10-character product code from the Amazon link (see below) |
| `linkId` | The `linkId` from your SiteStripe link (see below) |
| `image` | Picture file name inside `img/`, or `""` for none |

**Finding `asin` and `linkId`:** sign in to Amazon Associates, open the product on amazon.in, click **Get link** in the SiteStripe bar and choose **Full Link**. In the link:
- the 10 letters/numbers after `/dp/` are the `asin`,
- the letters/numbers after `linkId=` are the `linkId`.

4. To remove a product, delete its block. The order in the file is the order shown.
5. Run `node tools/check.js` (optional) or open `index.html` and finish the quiz to see the result.

### Product pictures
Put a picture in the `img/` folder (square works best, about 320 x 320 pixels) and write its file name in `image`.
Amazon's Associates rules generally allow its product pictures only through its own tools (for example the SiteStripe Image option), so check the Operating Agreement before using pictures taken from Amazon pages.
To hide all pictures at once, set `showImages: false` in `js/products.js`.

### Change the colours
Open `css/theme.css`. The first block has five colours (`--brand`, `--brand-dark`, `--ink`, `--cream`, `--mint`). Change the colour codes and the whole site follows.

### Change the wording on a page
Open the page (for example `about.html`) in any text editor and edit the text between the tags. Do not remove the `<` `>` parts.

### Change the quiz questions or the powder matching
- Button names and small texts: `OPTIONS` near the top of `js/quiz.js`.
- Which powder wins for each answer: the `scores`, `goalBonus` and `flavourFit` numbers for each type in `js/products.js`. Higher numbers = a better match.
- Protein and calorie formulas: the "4. CALCULATIONS" section of `js/quiz.js`.

### Add a new guide
1. Copy `templates/guide-template.html` into the main folder and rename it, for example `guide-creatine-basics.html`.
2. Open it and replace the text that says `YOUR GUIDE TITLE`, the description line and the example paragraphs.
3. Open `guides.html`, copy one of the `<a href="guide-...">` card blocks, paste it at the end and change the link, title and description.
4. Open `sitemap.xml`, copy one `<url>` block, and change the address (no `.html` at the end) and the date.
5. Run `node tools/check.js` to check the links (optional).

## Put it on GitHub

1. Create a free account at github.com and click **New repository**. Name it `pickmyprotein` and choose **Public** (or Private).
2. On the new repository page click **uploading an existing file**.
3. Open the unzipped folder, select **everything inside it** (not the folder itself) and drag it into the browser window. Make sure the `css`, `js`, `img`, `templates` and `tools` folders are included.
4. Click **Commit changes**.
5. To edit later: open a file on GitHub, click the pencil icon, change it and click **Commit changes**.

## Publish the site

**Cloudflare (what the live site uses).** Upload the contents of the folder as a zip (with `index.html` at the top level) using **New deployment**, or connect the GitHub repository from the Cloudflare dashboard. Cloudflare's menus change, so follow their on-screen steps.

**GitHub Pages (free alternative).** In the repository open **Settings > Pages**, set **Source** to **Deploy from a branch**, choose `main` and `/ (root)`, and save. The site appears at `https://YOUR-NAME.github.io/pickmyprotein/`. All links in this project are relative, so it works at that address. For your own domain, add a file named `CNAME` containing `pickmyprotein.com` and follow GitHub's custom-domain steps (your DNS records would then have to point to GitHub, not Cloudflare).

## Before you publish changes
- Keep the Amazon statement in the footer ("As an Amazon Associate, I earn from qualifying purchases") and the Affiliate Disclosure page as long as you use affiliate links.
- Do not show product prices (they change often).
- Keep the "not medical advice" notes. The calorie figure is only a rough estimate.
- Open the site in a private browser window and finish the quiz once to check the results page.
