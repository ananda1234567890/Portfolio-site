# Ananda Paramanick — Portfolio Site

Single-file static site. Everything (CSS, JS, SVG icons) is embedded in `index.html`.
Only external requests are Google Fonts, YouTube thumbnails/player, your Cloudinary
images, and Calendly.

---

## BEFORE YOU PUBLISH — checklist

Search `index.html` for the word `REPLACE`. Every item below is one of those hits.

### 1. The one required setting

- [ ] **Calendly link.** Near the bottom of the file, in the JavaScript block:
      `const CALENDLY_URL = "REPLACE_WITH_YOUR_CALENDLY_LINK";`
      Paste your real link, e.g. `https://calendly.com/ananda/growth-audit`.
      This single change does three things automatically:
      the inline calendar loads in the booking section, every
      "Book a Free Growth Audit" button opens the Calendly popup, and the
      placeholder instruction panel disappears. Nothing else to wire up.

### 2. Images (Cloudinary URLs)

- [ ] `REPLACE_WITH_CLOUDINARY_HEADSHOT` — hero portrait. Portrait crop (~4:5),
      min 900px wide. Note: the hero applies a purple duotone treatment, so a
      clean, high-contrast headshot works best.
- [ ] `REPLACE_WITH_CLOUDINARY_RANDY_GAGE_HEADSHOT` — featured testimonial photo
- [ ] `REPLACE_WITH_CLOUDINARY_RANDY_GAGE_AVATAR` — small square avatar (same person)
- [ ] `REPLACE_WITH_CLOUDINARY_TESTIMONIAL_2` / `_3` / `_4` — testimonial avatars
- [ ] `REPLACE_WITH_CLOUDINARY_ANANDA_AT_MONITORS` — landscape, "Why Ananda" section
- [ ] `REPLACE_WITH_CLOUDINARY_ANANDA_PORTRAIT` — square-ish, "Meet Ananda" box
- [ ] `REPLACE_WITH_CLOUDINARY_SCREENSHOT_1` / `_2` / `_3` — analytics screenshots
      (these appear **twice each** — once in `src`, once in `data-img` for the
      click-to-zoom lightbox. Update both.)
- [ ] `REPLACE_WITH_CLOUDINARY_OG_IMAGE_1200x630` — social share preview image

Any image left unreplaced hides itself and falls back to a purple gradient block,
so a half-finished site still looks intentional. But finish them.

### 3. Videos (YouTube)

Paste a full YouTube URL or the bare 11-character ID into `data-yt`.
The thumbnail is fetched automatically (maxres, falling back to hq) and clicking
opens the video in the lightbox player.

- [ ] `REPLACE_YOUTUBE_URL_1` … `_6` — client work grid
- [ ] `REPLACE_YOUTUBE_TESTIMONIAL_URL_1` … `_3` — video testimonials
- [ ] For each card, also replace the title (`REPLACE — video / client name`)
      and the result line (`REPLACE — the result`). The result line is the
      highest-value text on that card — make it a number, not an adjective.

Delete any card block you don't need. To add more, copy a whole
`<button class="vcard">…</button>` block.

### 4. Copy still marked REPLACE

- [ ] Testimonial 2, 3, and 4 quotes + names + titles.
      The Randy Gage testimonial is already in full and needs nothing.
- [ ] Screenshot captions ("REPLACE — what this screenshot proves")

### 5. Contact + links

- [ ] `REPLACE@YOUREMAIL.com` — appears twice (booking section + footer)
- [ ] `https://youtube.com/@REPLACE` — appears twice (side rail + footer)
- [ ] `https://linkedin.com/in/REPLACE` — appears twice
- [ ] `https://instagram.com/REPLACE` — appears twice
- [ ] `https://REPLACE-WITH-YOUR-DOMAIN.com` — the `og:url` meta tag
- [ ] Remove any social link you don't actually use — an empty profile costs trust

### 6. Final pass

- [ ] `grep -c REPLACE index.html` should return `0`
- [ ] Open on a real phone, not just a narrow browser window
- [ ] Click every "Book a Free Growth Audit" button and confirm Calendly opens
- [ ] Play one video from each grid
- [ ] Confirm the stat row numbers are still true (15K/wk, 25K subscribers)

---

## Deploying

**Recommendation: GitHub + Netlify**, not drag-and-drop.

Drag-and-drop is fine for a first look, but you will be editing this — swapping
videos as new client work lands, adding testimonials, updating the stat row.
With drag-and-drop, every change means re-uploading by hand and you have no
history to roll back to. With Git, you edit, commit, push, and Netlify rebuilds
in about ten seconds. You also get deploy previews and one-click rollback if you
break something.

```bash
cd "Portfolio website"
git init
git add .
git commit -m "Portfolio site"
gh repo create ananda-portfolio --private --source=. --push
```

Then in Netlify: **Add new site → Import an existing project → GitHub → pick the repo.**
Leave the build command empty and set the publish directory to `/` (there is no
build step — it's one static file).

**If you want the fast path instead:** drag this whole folder onto
[app.netlify.com/drop](https://app.netlify.com/drop). It works immediately.
You can connect it to Git later without losing the URL.

Either way, add your custom domain under **Domain settings**. HTTPS is automatic.

---

## Local preview

```bash
cd "Portfolio website"
python3 -m http.server 8123
```

Then open http://localhost:8123

Use a server rather than opening the file directly — `file://` can behave
differently with fonts and iframes.
