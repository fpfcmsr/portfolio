# Portfolio

Hugo site (PaperMod theme) deployed to GitHub Pages as a **project site**:
<https://fpfcmsr.github.io/portfolio/>

Single-page personal site: name and LinkedIn at the top, self-image slot beside them,
About/Background prose, then a Projects list. The header carries a GitHub link in the
top-right corner and nothing else.

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
| `layouts/home.html` | Home page: hero, prose, project list |
| `layouts/_partials/header.html` | Header override: GitHub link only, no nav menu |
| `assets/css/extended/custom.css` | Hero, photo slot, header icon, project list styling |
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
