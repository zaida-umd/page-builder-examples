# Page Builder Examples

Demo and client-review pages built with the [design-system page builder](https://github.com/zaida-umd/design-system-page-builder), which is vendored here as the `page-builder/` submodule.

Published, behind the sign-in gate, at **https://zaida-umd.github.io/page-builder-examples/**.

## Layout

| What | Where |
|---|---|
| Example pages | `<slug>/index.html` |
| Index of every example | `index.html` (add a row for each new page) |
| Page-specific images | `images/projects/<slug>/` |
| Site-wide `<head>` meta (noindex) and access gate | `shared/head-meta.html`, `shared/gate.html` |
| Pages deploy | `.github/workflows/pages.yml` |
| Shared image library, scripts, components, rules | `page-builder/` (submodule) |

Example pages reference their own images as `../images/projects/<slug>/...` and the shared library as `../page-builder/images/...` and `../page-builder/scripts/...`.

## Building new examples

The page-builder slash commands (`/build-landing-page`, `/build-interior-page`, `/recreate-page`) write their output here. Real design projects (admissions, belonging, strategic-plan) live in their own repos — this repo is only for demos, experiments, component reviews, and recreations.

After adding a page, splice in the noindex meta and the gate, then add the page to `index.html`:

```sh
python3 page-builder/tools/build-chrome.py --pages .
```

`--pages .` is safe here: the tool skips the `page-builder/` submodule and `shared/`. Only the `head-meta` and `gate` regions exist in `shared/`, so each page keeps its own header and footer.

Do not commit video files; use a poster image for video heroes.

## Access gate

Every page is blank until a reviewer signs in. Manage accounts with the commands below. The tool prompts for the password; never type one into the file:

```sh
python3 page-builder/tools/gate.py --write shared/gate.html
python3 page-builder/tools/build-chrome.py --pages .
```

The gate keeps casual visitors and crawlers out; it is **not** access control. The repo is public (Pages needs that on the Free plan), so page source is readable on GitHub. Put nothing here that would matter if it leaked. See `page-builder/scripts/gate.js`.

## Publishing

Every push to `main` deploys through `.github/workflows/pages.yml`, which trims the page builder's own `test/`, `qa/` and design-system source out of the artifact. After bumping the `page-builder` submodule, commit the new pointer so the deploy picks it up.

## Setup

```sh
git clone --recurse-submodules git@github.com:zaida-umd/page-builder-examples.git
python3 -m http.server 4177   # then open http://localhost:4177/
```
