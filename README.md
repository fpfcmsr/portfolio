# Portfolio

Hugo site (PaperMod theme) deployed to GitHub Pages as a **project site**:
<https://fpfcmsr.github.io/portfolio/>

Single-page personal site in the shape of <https://tylerhillery.com>: a blue bar with the
name (small, links home) and a **Projects** tab on the left, GitHub and the theme toggle
on the right. The body opens with LinkedIn, then About/Background prose beside a
self-image slot, then a Projects list.

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
| `content/projects/` | One page per project; `example-project.md` is a draft template |
| `layouts/home.html` | Home page: LinkedIn line, prose + photo slot, project list |
| `layouts/_partials/header.html` | Header override: brand + tab left, GitHub right |
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

```sh
hugo new content projects/my-project.md   # created as a draft
```

Set `draft: false` to publish. Published projects appear on the home page under
**Projects** (title + `summary`); the section is hidden while none are published.
Each project page keeps the theme's single-page layout with the header name as the
link back home.

## Build

```sh
hugo --gc --minify
```

Output lands in `public/` (git-ignored — CI builds it).

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

Neither license is displayed on the site: the copyright line is hidden
(`params.footer.hideCopyright`) and the license files sit at the repo root, outside
`static/` and `content/`, so Hugo never publishes them.

## Notes

- **baseURL**: changing the repo name, switching to a user site (`<user>.github.io`), or
  adding a custom domain means editing `config/_default/hugo.toml`.
- **Theme**: update with `git submodule update --remote themes/PaperMod`, then rebuild
  and review — `layouts/_partials/header.html` is a copy of the upstream partial and can
  drift.
- **Theme toggle**: kept next to the GitHub icon; set `disableThemeToggle = true` to
  leave only the GitHub link in the header.
- **Bar details**: the bar is filled with `--bar-bg` (a deeper blue in dark mode), text is
  `--bar-fg` / `--bar-fg-dim`; all three live in `custom.css`. The brand is 17 px (15 px
  under 480 px); tabs and icons sit at 85% white and go full white on hover/active.
  `--brand` still tints content links (`LinkedIn` hover). The home page keeps an `h1`
  with the name as screen-reader-only text, since the visible name is the bar's brand
  link.
