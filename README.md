# Personal site

Plain HTML and CSS. No build step, no framework, no dependencies, no tracking.

| File | What it is |
| --- | --- |
| `index.html` | All the content and structure. |
| `styles.css` | All the styling, including the light/dark themes. |
| `favicon.svg` | The browser-tab icon (a geometric "E"). |

## Structure

The page is one file with four **views**, switched by the tabs in the header:

| Tab | View id | Holds |
| --- | --- | --- |
| About & now | `#home` | About + Now (the landing view) |
| Experiences | `#experience` | a plain "Role @ Organization" list |
| Interests | `#interests` | a list of interests; Music / Movies expand, Photography links out |
| Reading & podcasts | `#reading` | `.list-group` sub-lists of books and podcasts |

Switching is done in the browser by a small script that shows one `.view` at a
time and keeps it in sync with the URL hash, so each view is a shareable link
(`…/#experience`) and the back button works. With JavaScript disabled, all four
views are shown stacked and the tabs act as plain in-page anchors.

To add or move content, edit the `<div class="view" id="…">` blocks in
`index.html`. To rename a tab, change both the tab text in `<nav class="tabs">`
and nothing else (the `href` must keep matching the view `id`).

## Preview locally

Open `index.html` in a browser — that's enough. To serve it over HTTP (closer to
how it runs in production):

```
python -m http.server 8000
# visit http://localhost:8000
```

## Fill in your content

Everything that needs changing is marked `TODO` in `index.html`. Search the file
for `TODO` and work top to bottom:

- **Tagline** — one or two plain sentences under your name.
- **Links** — the `.links` nav under your name. Add an `<a>` per profile, with a
  `<span class="sep" aria-hidden="true">·</span>` between each.
- **About** — two or three plain lines on the `#home` view. Short.
- **Now** — a one-line "As of <month>:" plus a short `simple-list` of what has
  your attention. Add or remove `<li>` rows.
- **Experiences** (`#experience` view) — a `simple-list` of "Role @ Organization",
  newest first. No dates, no descriptions. The `@ …` part sits in
  `<span class="dim">` to grey it, and the organization name is a link. Add or
  remove `<li>` rows.
- **Interests** (`#interests` view) — a `.interests` list. A plain `<li>` is
  just text. Wrap the text in `<a href="…">` to make it a link (Photography).
  For a row that expands, use `<li><details class="drop"><summary>Label</summary>
  <p class="drop__body">comma, separated, list</p></details></li>` (Music,
  Movies). Add or remove `<li>` rows.
- **`<head>`** — the `<title>`, `<meta name="description">`, and the Open Graph
  tags. Set `og:url` to your real domain once you've picked one.
- **Footer year.**

To restyle, the values worth touching first are the custom properties at the top
of `styles.css` (`--accent`, `--measure` for column width, the theme colors).

To change the favicon, edit the letter rectangles or the `fill` colors in
`favicon.svg`.

## Deploy

No build command. The publish directory is the project root.

- **GitHub Pages** — push these files to a repo, then Settings → Pages → "Deploy
  from a branch" → `main` / root. For a custom domain, add a file named `CNAME`
  containing just `yourdomain.com`, then set the DNS records GitHub shows you.
- **Netlify / Vercel / Cloudflare Pages** — "Add new site", connect the repo (or
  drag the folder onto the dashboard). Leave the build command empty; set the
  output/publish directory to the root.

## Notes

- The theme follows the visitor's system setting. The footer toggle overrides it
  and remembers the choice in `localStorage`.
- The page is fully readable with JavaScript disabled: all three views show
  stacked. The two scripts are the view switcher and the theme toggle.
