# readcraftery-docs

> 🌐 **Public repository** — Public design and art documentation for Readcraftery.

This repository contains the public-facing design documents for **Readcraftery** — a reading-centered educational fantasy game for children ages 4–9, built around the idea that **reading is a power that changes the world**.

These documents are intended for modders, illustrators, teachers evaluating the game for classroom use, and anyone interested in how the game was designed. They are not engine build instructions. For internal technical implementation documents, see [`readcraftery-dev-docs`](https://github.com/The-Readcraftery-Project/readcraftery-dev-docs).

---

## Documents

Each document exists in two language versions under `en/` and `es/`.

### Game Design Document (GDD)
`en/READCRAFTERY_GDD_en.md` · `es/READCRAFTERY_GDD_es.md`

**Version:** 1.4 — **Status:** Pre-Production Spec

The definitive public-facing description of what Readcraftery is: game vision, reading-first puzzle structure, progression, Owlorumo's role, platform strategy, monetization model, and major design decisions.

This is the best starting point for anyone new to the project.

### Art Style Guide
`en/READCRAFTERY_ART_GUIDE_en.md` · `es/READCRAFTERY_ART_GUIDE_es.md`

**Version:** 1.5 — **Status:** Pre-Production

Visual identity specification for the game. Covers palette roles, Storybook Arcane visual doctrine, Owlorumo's visual anchors, readability-first UI art rules, library-world identity, and theme guidance for future-compatible visual variations.

Essential reading for any artist contributing official art, a Theme Pack, or book pack illustrations.

### Asset Contracts
`en/READCRAFTERY_ASSET_CONTRACTS_en.md` · `es/READCRAFTERY_ASSET_CONTRACTS_es.md`

**Version:** 1.3 — **Status:** Pre-Production

Technical specification for the visual assets the game expects. Defines node types, filenames, dimensions, export expectations, and production-facing asset states for UI, books, backgrounds, and companion assets.

Use this alongside the Art Style Guide when producing art assets for the official game or for compatible community content.

### Modding Guide
*Planned as a future public document / SDK-facing guide.*

Book Pack and Theme Pack creation is currently described across the GDD, Art Style Guide, Asset Contracts, and the public SDK repository.

---

## Repository structure

```text
readcraftery-docs/
├── en/
│   ├── READCRAFTERY_GDD_en.md
│   ├── READCRAFTERY_ART_GUIDE_en.md
│   └── READCRAFTERY_ASSET_CONTRACTS_en.md
└── es/
    ├── READCRAFTERY_GDD_es.md
    ├── READCRAFTERY_ART_GUIDE_es.md
    └── READCRAFTERY_ASSET_CONTRACTS_es.md
