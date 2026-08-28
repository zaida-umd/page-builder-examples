# Page Builder Examples

Demo and client-review pages built with the [design-system page builder](https://github.com/zaida-umd/design-system-page-builder), which is vendored here as the `page-builder/` submodule.

## Layout

| What | Where |
|---|---|
| Example pages | `<slug>/index.html` |
| Page-specific images | `images/projects/<slug>/` |
| Shared image library, components, rules | `page-builder/` (submodule) |

Example pages reference their own images as `../images/projects/<slug>/...` and the shared library as `../page-builder/images/...`.

**Legacy layout.** The eight original pages still live at `examples/<name>.html`.
That is one level below the repo root, exactly like `<slug>/index.html`, so their
relative paths resolve identically and there is no rush to move them — but new
pages use `<slug>/index.html`, which is what the page-builder commands write.
Migrating the old ones is a pure `git mv` with no path edits.

## Building new examples

The page-builder slash commands (`/build-landing-page`, `/build-interior-page`, `/recreate-page`) write their output here. Real design projects (admissions, belonging, strategic-plan) live in their own repos — this repo is only for demos, experiments, and recreations.

Do not commit video files; use a poster image for video heroes.

## Setup

```sh
git clone --recurse-submodules git@github.com:zaida-umd/page-builder-examples.git
python3 -m http.server 4177   # then open http://localhost:4177/examples/
```
