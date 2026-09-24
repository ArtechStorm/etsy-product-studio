# etsy-product-studio# Etsy Product Studio

**A Claude Code skill that turns an idea into a finished, sellable digital product plus its entire Etsy listing, end to end.**

Give it a concept (or a competitor's listing) and it researches the market, builds the actual product file, shoots branded mockups, writes the SEO copy, and proposes what to build next. It was distilled from my own Etsy builds for [ReserveLuxe](https://reserveluxe.etsy.com), then generalized into a repeatable pipeline.

![demo](demo.gif)
<!-- Add a GIF or a strip of 2-3 output images: a gallery mockup, the device-family thumbnail, a rendered dashboard. This is the most convincing thing on the page. -->

## Why I built it
Running my shop solo, every product was the same slow grind: validate the idea, build the file, make it look premium, screenshot it, stage the mockups, then write a title, tags, and a description that actually rank. I turned that whole grind into one skill so I can go from idea to listing-ready in a fraction of the time, and hit the same premium bar every launch.

## What it does
A seven-phase pipeline, product-type-agnostic (spreadsheets, PDF/printable planners, PPTX/Canva template suites, branding kits, digital guides). Each phase also runs on its own:

0. **Recall & align** — pulls prior context on the idea so decisions already made aren't re-litigated and stale ones get re-checked, then confirms scope before spending effort.
1. **Research & validate** — a demand/competition/price check with a go/no-go score, plus teardowns of 3-5 winning competitor listings that reverse-engineer *what actually converts* (thumbnail hook, image order, lead keyword, price ladder). That teardown becomes the brief for the build.
2. **Scope & design** — picks a build track and locks design tokens: a palette and two fonts, to brand.
3. **Build the product** — generates the full artifact from scratch (e.g. Excel via openpyxl: auto-updating dashboard charts, formula-driven rollups, conditional formatting, dropdowns, a nav sidebar, sample data). Idempotent, so every run rebuilds clean.
4. **Listing images & thumbnail** — captures pixel-perfect screenshots, then composes a 15+ image gallery set and a device-family thumbnail with Pillow, to a fixed conversion formula, QA'd image by image.
5. **Listing copy & price** — writes a ready-to-paste 140-char SEO title, 13 tags, a structured description, and a price ladder, all *from the teardown* and inside Etsy's exact constraints.
6. **Launch & expand** — stages the finished product in a pipeline tracker, then proposes one upgrade and 2-3 adjacent products plus a bundle, each with a rationale.

## What makes the output premium
The levers baked in: an auto-updating dashboard as the hero screenshot, gridlines off everywhere, max two fonts and ~six colors, every number a formula, reactive conditional formatting, dropdowns wherever there's a choice, and an instructions tab up front. The difference between a file that reads as $5 and one that reads as $15-50.

## Design principles worth calling out
- **Confirm at the seams.** The skill acts, then checks in at the points where a wrong assumption would be expensive (after research, before building, before finalizing images, before listing), instead of interrogating up front or guessing.
- **Verify by looking.** Formulas that don't error can still be wrong, charts can render blank, formats can silently reset. So the pipeline exports each build to PDF and PNG and actually inspects the render before calling anything done. Fonts are verified from the exported PDF with PyMuPDF because Excel COM silently falls back to a default font.
- **Idempotent builds.** Every build script regenerates the full artifact, so iterating is trivial.
- **The skill improves itself.** When a build teaches a new gotcha or a better recipe, that lesson gets written back into the reference files before close-out.

## Stack
- **Claude Code** (authored as a reusable skill: `SKILL.md` + progressive-disclosure references + scripts)
- **Python** — `openpyxl` (build engine), `Pillow` (mockups), `PyMuPDF` (font/render verification)
- **Excel COM automation** (Windows) — recalcs formulas, exports PDFs, captures screenshots
- **PowerShell** helper scripts for the Excel COM steps
- **Exa + Firecrawl** for market research and competitor teardowns

## What's inside
```
etsy-product-studio/
  SKILL.md                     # the pipeline: 7 phases + prime directives
  references/                  # deep playbooks, loaded only when a phase needs them
    research-validation.md     # demand/price validation + competitor teardown method
    build-tracks.md            # the menu of product types and the engine each reuses
    listing-images.md          # the 15+ image formula, order, and per-image QA gate
    listing-copy.md            # Etsy SEO title/tags/description rules + worked example
    product-build.md           # openpyxl premium patterns, blueprints, verify loop, gotchas
    mockups.md                 # screenshot technique, Pillow composition, fonts
    product-ideas.md           # sibling/bundle ideation + high-converting catalog
  scripts/
    xlsx_design_system.py      # reusable openpyxl build engine
    verify_xlsx.ps1            # Excel COM error scan + PDF export
    shoot_tabs.ps1             # Excel COM tab -> PNG screenshotter
    mockup_kit.py              # Pillow gallery / thumbnail / Canva-base generator
```
The SKILL.md is the spine; the heavy detail lives in `references/` and is pulled in only when a phase needs it, to keep the context lean.

## Honesty note
The skill never fakes bestseller badges, reviews, or ratings, and never invents claims in listing copy. Those are verifiable and faking them violates marketplace policy.

## About me
Built by Sal, an AI builder and operator running [ReserveLuxe](https://reserveluxe.etsy.com) with Claude Code. I turn the systems I use to run a real DTC business into repeatable tools.

## License
MIT — see [LICENSE](LICENSE).
