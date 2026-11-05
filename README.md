# Portfolio

Hugo site (PaperMod theme) deployed to GitHub Pages as a **project site**:
<https://fpfcmsr.github.io/portfolio/>

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

## Content

| Path | Purpose |
|---|---|
| `config/_default/hugo.toml` | Site config: baseURL, title, menus, profile landing page, social icons |
| `config/development/hugo.toml` | Dev-only `baseURL` so links stay on localhost |
| `content/about.md` | About page |
| `content/projects/` | One page per project; `example-project.md` is a draft template |
| `static/` | Favicons (`favicon.ico`, PNGs, `safari-pinned-tab.svg`) |
| `layouts/_partials/index_profile.html` | Site override of the theme partial (see below) |

New project page:

```sh
hugo new content projects/my-project.md
```

It is created as a draft; publish by setting `draft: false`.

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

## Notes

- **Theme**: pinned submodule at `themes/PaperMod`. Update with
  `git submodule update --remote themes/PaperMod`, then rebuild and review.
- **Partial override**: upstream `index_profile.html` emits `profileMode` button URLs
  verbatim, so `url = '/projects/'` resolves to the domain root and 404s on a project
  site. The local copy re-prefixes button URLs with the site path (Hugo's `relURL` leaves
  leading-slash paths untouched, hence the `strings.TrimPrefix`). Re-check it after
  theme updates.
- **baseURL**: `https://fpfcmsr.github.io/portfolio/` in `config/_default`. Changing the
  repo name, switching to a user site (`<user>.github.io`), or adding a custom domain
  means editing this one line.
