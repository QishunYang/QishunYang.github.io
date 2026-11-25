# Qishun Yang - academic homepage

Three static pages: Main, Publications, Services. Plain HTML + CSS, no build
step, no dependencies. Everything renders by opening `index.html` directly; the
same files deploy to GitHub Pages unchanged.

## Structure

```
index.html                     Main: about, research interests, research experience
publications.html              Publications: one card per paper
services.html                  Academic services
assets/css/style.css           shared styling (design tokens at the top)
assets/img/avatar.svg          monogram placeholder - replace with a photo
assets/img/pubs/               teaser figures taken from the papers themselves
assets/img/favicon.svg         browser tab icon
.nojekyll                      stops GitHub Pages from running Jekyll
```

Every page repeats the same shell: navigation bar, author card, black footer.
Editing a nav item or the author card means editing it in all three files.

Page anatomy:

```
.navigation-wrapper   site name (left column) + MAIN / PUBLICATIONS / SERVICES
#main                 12% gutter | 14% author card | 53% text column | 12% gutter
  .article-author-top 100px portrait + italic contact links
  article              h2 sections separated by <hr>
.footer-wrap          full-width black bar, pinned to the viewport bottom
```

The current page is marked by `class="top-navigation-current"` on its nav link,
which draws the overline seen on the reference site.

## Preview locally

Double-click `index.html`. Relative links between the three pages work over
`file://`.

## Deploy to GitHub Pages

1. Create a repository named `<your-username>.github.io`.
2. Push the contents of this folder to its default branch (`main`):

   ```bash
   git init
   git add .
   git commit -m "academic homepage"
   git branch -M main
   git remote add origin git@github.com:<your-username>/<your-username>.github.io.git
   git push -u origin main
   ```

3. Repository **Settings → Pages**: Source = *Deploy from a branch*,
   Branch = `main`, Folder = `/ (root)`.
4. Wait for the first build, then open `https://<your-username>.github.io`.

## What still needs your input

| Where | What |
|---|---|
| all three pages, author card | `GitHub` link is `href="#"` with class `is-todo` - replace with your profile URL and drop the class |
| `assets/img/avatar.svg` | casual portrait, square, at least 400x400; save as `avatar.jpg` and update `src` |
| all three pages, footer | `Last updated` date |

The CV is not linked from this site.

## Design provenance

- **Layout and typography** are reproduced from <http://caihanlin.com/>: serif
  text (LXGW WenKai, the same webfont the reference loads from cdnjs), 92%-wide
  grid, 14% author card on the left, 53% text column, uppercase top navigation
  with the current item marked by an overline, `<hr>` between sections, square
  list bullets, full-width black footer. Column widths and the responsive
  `font-size` steps (90 / 95 / 100 / 112.5%) are copied from its compiled CSS.
- **Publication list** takes the thumbnail-per-paper card from
  <https://luost.me/>: 32% thumbnail column, title, authors, venue, one-line
  summary.
- **Colour and weight emphasis** are the deliberate departure from the
  reference's single-colour text, following <https://meng-ding.github.io/>:
  colour-coded venue labels (accepted / findings / under review), blue body
  links with hairline underlines, bold self-author.

If the webfont cannot load, the stack falls back to Georgia and then to the
system CJK serif, so the page stays serif rather than dropping to a sans face.

## Content policy

- Included: about, research interests, research experience, publications,
  academic services.
- Excluded on purpose: **Education**, **Awards & Honors**, **Skills**.
- Academic services are written with venue abbreviations (EMNLP, DMLR,
  IEEE WoWMoM), the way most academic homepages list them.

## Editing notes

- Colours, spacing and the font stack live in `:root` at the top of `style.css`.
- A publication is one `<div class="pub">` with five children in this order:
  `a.pub-thumb`, `p.pub-title`, `p.pub-authors`, `p.pub-venue`, `p.pub-note`.
  The grid gives the thumbnail `grid-row: 1 / span 4`, so keep the element order.
- Venue colour comes from the class on the inner span: `venue--oral`,
  `venue--findings`, `venue--review`.
- News items use the [MM/YYYY] prefix in red, one line each.
- Breakpoints: 600px (author card moves above the text, thumbnails go
  full-width), 768px and 992px (base font-size steps).
