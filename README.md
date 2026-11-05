# Portfolio

Hugo site (PaperMod theme) deployed to GitHub Pages as a **project site**:
<https://fpfcmsr.github.io/portfolio/>

Single-page personal site in the shape of <https://tylerhillery.com>: an ocean-blue bar
with the name (small, links home) and a **Projects** tab on the left, GitHub and the theme
toggle on the right. The body repeats the name at 2.5 rem in black, then LinkedIn, then
About/Background prose beside a self-image slot, then a Projects list.

## Requirements

- Hugo extended ≥ 0.169 (`hugo version`)
- Git with submodule support

## Local development

```sh
git clone --recurse-submodules https://github.com/fpfcmsr/portfolio.git
# already cloned without submodules?
git submodule update --init --recursive

hugo server            # http://localhost:1313/portfolio/
hugo server -D         # include drafts
```

## Layout

| Path | Purpose |
|---|---|
| `config/_default/hugo.toml` | Site config: baseURL, title, `params.links`, params |
| `config/development/hugo.toml` | Dev-only `baseURL` so links stay on localhost |
| `content/_index.md` | Home page body — About Me, Background |
| `archetypes/projects.md` | Skeleton for new project pages |
| `content/projects/` | One page bundle per project; `example-project/` is a draft sample |
| `layouts/home.html` | Home page: large name, LinkedIn line, prose + photo slot, project list |
| `layouts/_partials/header.html` | Header override: brand + tab left, GitHub right |
| `layouts/_partials/footer.html` | Footer override: copyright only, theme credit removed |
| `assets/css/extended/custom.css` | Bar, brand colour, photo slot, project list styling |
| `static/` | Favicons (`favicon.ico`, PNGs, `safari-pinned-tab.svg`) |
| `themes/PaperMod` | Theme, pinned submodule |

Links live in config, not templates:

```toml
[params.links]
  github = 'https://github.com/fpfcmsr'
  linkedin = 'https://www.linkedin.com/in/fpfcmsr/'
```

The LinkedIn value above mirrors the GitHub handle and has **not** been verified against
a real profile — correct it before publishing.

## Self image

Drop the photo at `assets/self.jpg` (or `.jpeg`, `.png`, `.webp`). It is cropped to
400×500 and rendered 200 px wide to the right of the name (132 px, below it, on narrow
screens). With no file present the slot is omitted and the hero is text-only — no
placeholder is generated.

## Projects

Projects are page bundles, so each one keeps its images next to its text:

```sh
hugo new content projects/my-project/index.md   # creates the bundle, as a draft
hugo server -D                                  # view drafts while filling them in
```

The file lands with `archetypes/projects.md` front matter and body:

```toml
title   = 'My Project'    # derived from the directory name
date    = '<now>'
draft   = true            # flip to false to publish
summary = ''              # one line, shown in the home list
tags    = []
```

Body sections are `Overview`, `Problem`, `Approach`, `Stack`, `Results`, `Links`,
`Notes` — prompts, not fixed markup; change them per project.

- **Images**: drop `cover.jpg` in the bundle and uncomment the `[cover]` block
  (`image`, `alt`). PaperMod resizes it for the list card and the page header.
- **Ordering**: newest `date` first, on `/projects/` and on the home list.
- **Visibility**: published pages appear on the home page under **Projects** (title +
  `summary`); the section stays hidden while nothing is published.
- **Plain file**: `hugo new content projects/my-project.md` also works if a project
  needs no images.

## Build

```sh
hugo --gc --minify
```

Output lands in `public/` (git-ignored — CI builds it). If you have been running
`hugo server -D`, draft output stays in `public/`; add `--cleanDestinationDir` when
building locally so published output matches CI.

## Deploy

`.github/workflows/hugo.yaml` builds and publishes on every push to `main`.

One-time setup in the repository: **Settings → Pages → Build and deployment → Source:
GitHub Actions**. No `gh-pages` branch is used.

The workflow installs Hugo 0.169.0 (keep `HUGO_VERSION` in sync with local), checks out
the theme submodule recursively, and passes `--baseURL` from `actions/configure-pages`,
so a custom domain or repo rename needs no config change.

## License

| Scope | License |
|---|---|
| Code: `layouts/`, `assets/`, `config/`, workflow | [MPL-2.0](LICENSE) |
| Content: `content/`, images, site text | [CC BY 4.0](LICENSE-CONTENT) |
| Theme (`themes/PaperMod` submodule) | MIT, see `themes/PaperMod/LICENSE` |

No license text is displayed on the site: the footer carries only the copyright
(`© 2026 Francesco Fortunelli`), and the license files sit at the repo root, outside
`static/` and `content/`, so Hugo never publishes them.

## Notes

- **baseURL**: changing the repo name, switching to a user site (`<user>.github.io`), or
  adding a custom domain means editing `config/_default/hugo.toml`.
- **Theme**: update with `git submodule update --remote themes/PaperMod`, then rebuild
  and review — `layouts/_partials/header.html` is a copy of the upstream partial and can
  drift.
- **Theme toggle**: kept next to the GitHub icon; set `disableThemeToggle = true` to
  leave only the GitHub link in the header.
- **Footer credit**: PaperMod's "Powered by Hugo & PaperMod" line is removed in
  `layouts/_partials/footer.html` (upstream asks you to keep it — restore that `<span>`
  if you'd rather credit it). Everything else in the partial, including the theme
  toggle, copy-button and scroll-to-top scripts, is upstream code; re-check it on theme
  updates along with the header override.
- **TOML table order**: in `config/_default/hugo.toml` every key after a `[params.x]`
  header belongs to that table. Keep scalar `params` first and `[params.links]` last, or
  flags like `ShowCodeCopyButtons` silently end up under `params.links` and stop applying.
- **Bar and name colours**: the bar is filled with `--bar-bg` — ocean blue
  `rgb(15, 76, 105)` in light mode, `rgb(13, 63, 87)` in dark — with text at
  `--bar-fg` / `--bar-fg-dim`; all in `custom.css`. The brand is 17 px (15 px under
  480 px); tabs and icons sit at 85% white and go full white on hover/active.
- **Hero name**: `.home-name` is 2.5 rem (2 rem under 640 px), black via `--hero-name`
  in light mode — dark mode switches it to near-white `rgb(232, 237, 240)` since black
  would disappear on the dark background.
