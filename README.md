# DriveTrain Trading — Website Operator's Guide

> **Audience:** whoever on the Drivetrain team is maintaining this site after launch. You do **not** need to be a web developer to use this guide. If you can edit a Google Doc, you can update this website.

---

## What you have

Three files, sitting in one folder:

```
drivetrain-website/
├── index.html      ← the page itself (text, buttons, structure)
├── styles.css      ← colors, fonts, spacing
└── README.md       ← this guide
```

Everything lives in these files. No databases, no plugins, no subscriptions required.

---

## 1. How to put this site on the internet

You have two simple options. Both are **free**.

### Option A — GitHub Pages (recommended, matches your existing setup)

You already use GitHub for the Drivetrain Suite. Same workflow here.

1. Go to your GitHub account → **New repository** → name it something like `drivetrain-website` (or use your existing `drivetraintradinguae` account and create a new repo).
2. Upload **all three files** (`index.html`, `styles.css`, `README.md`).
3. Repository → **Settings** → **Pages** → set **Source = main branch / root**.
4. Wait 30 seconds. GitHub will show you a URL like `https://drivetraintradinguae.github.io/drivetrain-website/`.
5. Visit that URL — you're live.

**Pointing your real domain at it:** once you own `drivetraintrading.com` (or whichever domain), follow GitHub's [custom domain guide](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site) — it's a one-time DNS setting.

### Option B — Netlify Drop (fastest, zero account needed to test)

1. Open [app.netlify.com/drop](https://app.netlify.com/drop).
2. Drag the entire `drivetrain-website` folder onto the page.
3. Netlify gives you a live URL in under 10 seconds.
4. Create a free Netlify account to keep the URL or attach your domain.

---

## 2. Things you MUST change before going live

Open `index.html` in any text editor (TextEdit on Mac, Notepad on Windows, or a free editor like [VS Code](https://code.visualstudio.com/)). Use **Find** (Cmd/Ctrl + F) to locate each item.

| Find this | Replace with |
|---|---|
| `971000000000` | Your real WhatsApp number in international format, **no `+`**, **no spaces** (e.g. `971501234567`) |
| `info@drivetraintrading.com` | Your real email |
| `+971 00 000 0000` | Your real phone, formatted for display |
| `drivetraintrading.com` | Your real domain (appears in meta tags and schema) |

`971000000000` appears in **four places** — replace them all. A global find-and-replace in your editor does it in one click.

---

## 3. How to edit page content (text, buttons, sections)

Open `index.html`. It's written in HTML but you don't need to learn HTML — just follow these rules:

1. **Look for big comment blocks that look like this:**
   ```html
   <!-- ========== HERO ========== -->
   ```
   Each section of the page is marked this way.

2. **Edit only the text between the `>` and `<` characters.**
   Example — to change the hero headline:
   ```html
   <h1 class="hero__title">
     Used Auto Parts.<br />
     <span class="hero__title--accent">Export Prices.</span><br />
     Global Shipping.
   </h1>
   ```
   You can safely change `Used Auto Parts.`, `Export Prices.`, `Global Shipping.` — those are just text.
   Don't touch `<h1>`, `<br />`, `<span class="...">` — those are structure.

3. **Duplicating a block (e.g. adding a new inventory item):** copy everything between `<article class="inv-card">` and the matching `</article>`. Paste below. Edit the new copy's text. Done.

4. **Save the file**, re-upload to GitHub / Netlify, the site updates in under a minute.

### Sections you'll edit most often

| Section | What to edit |
|---|---|
| **Hero** | Headline, subhead, CTAs |
| **Trust bar** | `500+`, `5`, `100%`, `FZE` stats — keep them factual |
| **Inventory** | Add/remove `.inv-card` blocks weekly as stock changes |
| **Shipping** | Transit times per country |
| **Contact** | Phone, email, office address |
| **Footer** | Company lines, social links |

---

## 4. Adding real inventory photos

Right now the inventory section uses colored placeholder tiles. When you have real photos:

1. Create a folder called `images/` next to `index.html`.
2. Drop your photos in — e.g. `images/engine-01.jpg`. Keep them under 500 KB each (use [tinyjpg.com](https://tinyjpg.com) to compress).
3. In `index.html`, find the inventory card you want to update, e.g.:
   ```html
   <div class="inv-card__media inv-card__media--eng" role="img" aria-label="Used engine placeholder image">
     <span>ENGINE</span>
   </div>
   ```
4. Replace the entire `<div>` with:
   ```html
   <img src="images/engine-01.jpg" alt="Used Toyota 2.5L engine" class="inv-card__media" loading="lazy">
   ```
5. Save, upload, refresh.

**Tip:** always write a descriptive `alt="..."` — it's how Google Images finds your parts and it's how translate tools read them.

---

## 5. Installing marketing pixels (Meta, TikTok, Google)

You were right to want this easy. Here's the easiest way.

### The 10-minute setup: Google Tag Manager

**Why GTM?** Install it once here. After that, you add, remove, or edit every pixel (Meta, TikTok, Google Ads, GA4) from GTM's web dashboard — without ever touching this website's code again. Perfect for a non-technical marketing team.

1. Go to [tagmanager.google.com](https://tagmanager.google.com) and create an account.
2. Create a container → pick **Web** → name it `DriveTrain`.
3. GTM will show you two code snippets labeled **"Head"** and **"Body"**.
4. Open `index.html`. Find this block:
   ```html
   <!-- ===== GOOGLE TAG MANAGER (head) — paste between markers ===== -->
   <!-- START GTM HEAD -->
   <!-- END GTM HEAD -->
   ```
   Paste the **Head** snippet between `START` and `END`.
5. Find:
   ```html
   <!-- START GTM BODY -->
   <!-- END GTM BODY -->
   ```
   Paste the **Body** snippet between those two markers.
6. Save and re-upload. Done forever on the HTML side.

**After that, in GTM's web dashboard:**

- **To add Meta Pixel:** Templates → `Facebook Pixel` → paste your Pixel ID → Publish.
- **To add TikTok Pixel:** Templates → `TikTok Pixel` → paste your Pixel ID → Publish.
- **To add GA4:** Built-in tag → paste your Measurement ID → Publish.

Every change happens in GTM's UI. The website itself never needs editing for pixels again.

### If you'd rather paste pixels directly (skip GTM)

Each pixel provider gives you a snippet. The HTML already has placeholders:

```html
<!-- ===== META (FACEBOOK) PIXEL — paste between markers ===== -->
<!-- START META PIXEL -->
<!-- END META PIXEL -->
```

Paste the code Meta gives you between the `START` and `END` lines. Same for TikTok and GA4.

---

## 6. Language translation

The top bar has a Google Translate dropdown. It already offers **Russian, Ukrainian, Arabic, Georgian**.

- It works on the fly — visitors pick their language and Google translates the page for them. Zero maintenance.
- **Known limitation:** machine translation isn't perfect. For the most important pages you may eventually want to commission a proper human translation and publish a dedicated `index-ru.html`, `index-ar.html` etc. The current setup is fine for launch.
- **To offer more languages:** in `index.html`, find `includedLanguages: 'ru,uk,ar,ka'` and add language codes (e.g. `'ru,uk,ar,ka,tr,fa'` to add Turkish and Persian).

---

## 7. SEO — what's already done for you

Built-in:

- Proper page title, meta description, keywords targeting your 5 markets
- Open Graph tags for link previews (Facebook, WhatsApp, LinkedIn)
- Structured data (Schema.org `AutoPartsStore`) telling Google you're a UAE auto parts store serving RU/UA/IQ/GE/JO
- Semantic headings so Google can read the page structure
- Mobile-optimised (Google ranks mobile-first)
- Fast — no heavy frameworks

### What you should do once the site is live

1. Submit your site to [Google Search Console](https://search.google.com/search-console) — tells Google your site exists.
2. Create a Google Business Profile if the Dubai office has walk-in or pickup traffic.
3. Get listed on [OpenCorporates](https://opencorporates.com/) and UAE business directories for credibility signals.
4. Ask early customers to leave a review somewhere public (even a WhatsApp status screenshot works for social proof).

---

## 8. Changing colors and fonts

Open `styles.css`. The very first block is:

```css
:root {
  --red:        #b91c1c;
  --ink:        #0f172a;
  ...
}
```

Change the hex codes (the `#xxxxxx` values) and **every matching color on the site updates automatically**. You never have to hunt through the CSS.

To use [Coolors](https://coolors.co) or similar to pick new colors, grab the hex code and paste it in.

---

## 9. Launch checklist

Before you announce the site, tick all of these:

- [ ] Replaced `971000000000` with your real WhatsApp number (4 places)
- [ ] Replaced `info@drivetraintrading.com` with your real email
- [ ] Replaced `+971 00 000 0000` display phone with real number
- [ ] Replaced domain references with your real domain
- [ ] Verified inventory cards match current stock (or swapped in real photos)
- [ ] Tested the **Request Quote** form on a phone — confirm it opens WhatsApp with the message pre-filled
- [ ] Tested the floating WhatsApp button on mobile
- [ ] Tested language translation (try Arabic and Russian)
- [ ] Installed Google Tag Manager with at least GA4 active (for traffic data)
- [ ] Submitted the site to Google Search Console
- [ ] Added the site URL to your email signature and WhatsApp Business profile
- [ ] Added a favicon (save a 32×32 `favicon.ico` next to `index.html`)

---

## 10. Known limitations (and when to fix them)

These are intentional v1 choices. Name them now so no one is surprised:

| Limitation | When to address it |
|---|---|
| One page, not a full site | When inventory volume >100 live items, split into a dedicated `inventory.html` |
| Inquiry-by-WhatsApp, not full e-commerce checkout | When you have stable SKUs and prices, switch to a Shopify, WooCommerce, or custom cart |
| Google-translated (not professionally translated) | When Russian/Arabic traffic becomes >30% of visits, commission human translations |
| Placeholder product tiles | Replace with real photos as inventory is photographed (do the top 6 first) |
| No customer login / saved quotes | Not needed until repeat buyer base justifies it |

---

## 11. Where to get help

- **HTML / CSS questions:** [MDN Web Docs](https://developer.mozilla.org/) is the definitive plain-English reference.
- **Pixel setup questions:** each platform has a verification browser extension:
  - Meta Pixel Helper (Chrome)
  - TikTok Pixel Helper (Chrome)
  - Google Tag Assistant (Chrome)
  Install, load your site, they tell you if pixels are firing correctly.
- **For structural changes** (new sections, new pages, e-commerce integration) — that's where you loop the designer/developer back in.

---

**Launch small. Iterate fast. Update weekly.** The site is yours to maintain — keep the inventory fresh and the WhatsApp replies fast, and the rest takes care of itself.
