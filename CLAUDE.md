# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project state

This folder currently contains a single deliverable, `index.html` — a self-contained, static slide-deck HTML presentation ("Who I am" / "What I do" / "What I'm looking for" / a dummy placeholder slide). There is no build tooling, package manager, framework, or test suite. Do not invent build/lint/test commands — none exist. If the project grows (e.g. a real portfolio site is scaffolded here), update this file to describe the new tooling and structure.

The project is a git repository (GitHub: `SarahBoening/my-portfolio`, branch `main`) linked to Vercel (team `dl-school`, project `my-portfolio`) with git-push deploys: every push to `main` auto-deploys to production at https://my-portfolio-dl-school.vercel.app. `vercel.json` holds a permanent redirect from the deck's old filename (`/sarah-boening-intro-slides.html`) to `/`, since the file was renamed to `index.html` so it serves at the site root. `.vercel/` and `.env.local` are gitignored (local Vercel project link + OIDC token) — never commit them.

## Working with the slide deck

`index.html` is entirely self-contained: all CSS and JS are inline in the file, fonts are loaded from Google Fonts (Inter), and the one image (a personal avatar) is embedded as a base64 `data:` URI. There is no build step — just open the file directly in a browser to view it.

Structure inside the file:
- A `1920x1080` fixed-size `.stage` holds three `.slide` sections stacked absolutely; a `resize()` function scales `.stage` with `transform: scale()` to fit the actual viewport, so the design is authored in absolute pixel values against a 1920×1080 reference canvas rather than in responsive units.
- Navigation (prev/next buttons, dot indicators, arrow-key handling) is plain vanilla JS at the bottom of the file — no framework, no external JS dependencies.
- CSS custom properties at the top of the `<style>` block hold the design tokens (colors, spacing, radii, font sizes) pulled from Notion's brand system (deep navy `--navy`, signature purple `--purple`, pastel card tints, Inter/Notion-Sans typography). Reuse these tokens rather than hardcoding new colors/sizes if editing or extending slides.
- A small "SB" monogram badge (bottom-left on every slide) acts as the personal identity mark in place of a company logo.

To preview changes, open the file directly in a browser (e.g. `open sarah-boening-intro-slides.html` on macOS); no local server is required for normal viewing, though loading it via `file://` inside Claude's own browser-preview tooling has shown restrictions in the past — serving it over a quick local HTTP server (e.g. `python3 -m http.server`) is a reliable fallback for automated/browser-tool verification.
