# Cong Xu's Academic Homepage

Personal academic website (static HTML/CSS/JS), deployed via GitHub Pages.

**Live site:** https://helenxu.github.io (after you create the `helenxu.github.io` repository)

---

## Directory structure

```
.
├── index.html                      # Homepage
├── cv.html                         # CV
├── teaching.html                   # Teaching (course cards)
├── teaching/
│   ├── course-sta219.html          # STA219 Probability and Statistics for Engineering
│   ├── course-ma405.html           # MA405 Survival Analysis (in preparation)
│   ├── img/                        # Textbook cover images (used by the cards)
│   ├── slides/sta219/              # Lecture slides (PDF)
│   └── notebooks/sta219/           # Jupyter notebooks (.ipynb)
├── assets/
│   ├── css/style.css               # All styles (colors, fonts, layout)
│   ├── js/main.js                  # Mobile nav toggle
│   ├── img/photo.jpg               # Profile photo
│   └── cv/cv.pdf                   # Downloadable CV
├── .nojekyll                       # Tells GitHub Pages to serve files as-is
└── README.md
```

---

## Preview locally

Because pages use relative paths (e.g. `../assets/css/style.css`), open the site
through a local web server started at the **site root** — opening the HTML files
directly from Finder works too, but a server is safer for link checking:

```bash
# from this directory
python3 -m http.server 8123
# then visit http://127.0.0.1:8123/
```

---

## Deploy to GitHub Pages (first time)

1. Create a new **public** repository named exactly `helenxu.github.io`
   (GitHub Pages user sites must use the `<username>.github.io` name).
2. Push this folder as the repository root:

```bash
git init
git add .
git commit -m "Initial commit: academic homepage"
git branch -M main
git remote add origin https://github.com/helenxu/helenxu.github.io.git
git push -u origin main
```

3. In the repository: **Settings → Pages → Build and deployment**
   → Source: *Deploy from a branch* → Branch: `main`, folder: `/ (root)` → Save.
4. Wait 1–2 minutes, then open https://helenxu.github.io.

> The `.nojekyll` file is important: it stops GitHub from running Jekyll on upload,
> so the site is served byte-for-byte as you see it locally.

### Using a project site instead?

If you put this site in a repository with another name (e.g. `homepage`),
the URL becomes `https://helenxu.github.io/homepage/`.
In that case add `{{ site.baseurl }}`-style prefixes — or simply keep all links
relative, as they are now, and it will still work.

---

## Updating content

| What | How |
|---|---|
| Profile / bio / research interests | edit `index.html`, "About Me" and "Research Interests" sections |
| News | edit the `<ul class="news-list">` in `index.html` (newest first) |
| CV | edit `cv.html`; replace `assets/cv/cv.pdf` for the downloadable version |
| Add a course | copy the commented card block in `teaching.html`, then copy any file in `teaching/` as the new course page |
| Add slides | drop PDFs into `teaching/slides/<course>/`, then add `<li>` links in the course page |
| Add notebooks | drop `.ipynb` into `teaching/notebooks/<course>/`, then add `<li>` links |
| Course cover image | put the image in `teaching/img/` and replace the `<img src>` in the card |

### Keeping files small

Lecture PDFs were compressed with Ghostscript (≈10× smaller). For new PDFs:

```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.5 -dPDFSETTINGS=/ebook \
   -dNOPAUSE -dQUIET -dBATCH -sOutputFile=out.pdf in.pdf
```

Use `-dPDFSETTINGS=/printer` if you need higher resolution (larger file).

---

## Design notes

- Fonts: **Roboto** (body) and **Roboto Slab** (headings), loaded from Google Fonts.
- Theme colour: `#b509ac`, text `#000`, muted text `#828282` — matching the
  [al-folio](https://github.com/alshedivat/al-folio) theme used by the reference site.
- All colours and fonts live in `:root` at the top of `assets/css/style.css`;
  change them there and the whole site updates.

---

© 2026 Cong Xu · xuc6@sustech.edu.cn
