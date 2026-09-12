# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal academic homepage of the repo owner, GVS Mothish (PhD student, CDS, IISc Bangalore) — the person you're working with. Content requests ("add my new paper", "update my year") are edits to their own bio/publications. Served by GitHub Pages at `https://gvsmothish.github.io/` straight from the `main` branch. The owner wants it hosted **only on GitHub Pages** — don't propose or publish to other hosts.

Plain static HTML/CSS: no build step, package manager, framework, linter, or test suite. Pushing to `main` is the deploy.

To preview locally: `python3 -m http.server 8000` from the repo root, then open `http://localhost:8000`, or open `index.html` directly. Firefox on this machine is a snap and cannot read `/tmp`; for headless screenshots, write to a dir under `~/snap/firefox/common/`: `firefox --headless --no-remote --profile <dir>/prof --window-size=1280,3600 --screenshot <dir>/shot.png file://$PWD/index.html` (the profile dir must exist).

## Structure

- `index.html` — all content, as one single-page layout: sticky nav → hero (bio, Google PhD Fellow badge, link buttons, photo) → Research interests → Publications → Awards & honors → footer. Nav links target section `id`s (`publications`, `awards`). The owner removed the News and Projects sections on purpose; don't re-add them unasked.
- `stylesheet.css` — all styling. Colors are CSS custom properties on `:root`, redefined for dark mode both under `prefers-color-scheme: dark` (unless `data-theme="light"`) and under `:root[data-theme="dark"]`; the ◐ button in the nav sets `data-theme` and saves it to `localStorage`. Use the variables (`--fg`, `--muted`, `--accent`, …) rather than hard-coded colors so dark mode keeps working. `index.html` links it as `stylesheet.css?v=<date>`: bump that date whenever the CSS changes, or returning visitors' browsers will pair new HTML with a cached old stylesheet.
- `images/` — publication thumbnails, profile photo (`insta_icml.jpeg`), `icc_steps.mp4` (BiRoDiff autoplay loop).
- `data/gvsmothishcv.pdf` — the CV linked from the hero. Replace this file in place to update the CV.

## Adding content

Copy an adjacent entry in the same section:

- **Publication** — `<article class="pub">`: a `.thumb` (an `<img>`, a `<video muted autoplay loop playsinline>`, or `<div class="thumb gen">NAME</div>` as a stand-in when there's no figure), then a venue label `<span class="venue v-icml|v-iclr|v-ieee|v-acm">`, `<h3>` title, `.authors` with the owner wrapped in `<span class="me">`, a one-sentence `.tldr`, and `.plinks`. New venue colors go in `stylesheet.css` next to the existing `.v-*` classes. Order is newest first; `*` marks equal contribution.
- **Award** — `<li>` with the title, `.org` (optionally linked), and `.yr`.

## Notes

- Several files in `images/` (old project/award photos, `logo.jpeg`, and the ~31 MB `final_video_UHD (1) (1).mp4`) and `data_cache/` are no longer referenced by `index.html`. Keep new media small and use filenames without spaces.
- Commit messages in this repo are short tags like `website_upd_<date>` or `phd_year_upd`.
