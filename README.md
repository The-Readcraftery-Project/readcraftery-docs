# readcraftery-docs

> 🌐 **Public repository** — Design documentation for Readcraftery.

This repository contains the public-facing design documents for **Readcraftery** — a fantasy literacy game for children ages 4–9, built around word puzzles and community-created book packs.

These documents are intended for modders, illustrators, teachers evaluating the game for classroom use, and anyone interested in how the game was designed. They are not build instructions — for that, see the internal dev-docs repo.

---

## Documents

Each document exists in two language versions under `en/` and `es/`.

### Game Design Document (GDD)
`en/READCRAFTERY_GDD_en.md` · `es/READCRAFTERY_GDD_es.md`

**Version:** 1.2 — **Status:** Pre-Production Spec

The definitive description of what Readcraftery is: game vision, puzzle system, the Reading Owl companion, progression, monetization model, platform strategy, and all major design decisions. This is the right starting point for anyone new to the project.

### Art Style Guide
`en/READCRAFTERY_ART_GUIDE_en.md` · `es/READCRAFTERY_ART_GUIDE_es.md`

**Version:** 1.2 — **Status:** Pre-Production

Visual identity specification for the game. Covers color palettes, illustration style, UI design language, typography candidates, and guidelines for creating Themes (visual mods). Essential reading for any artist contributing a Theme Pack or book pack illustrations.

### Asset Contracts
`en/READCRAFTERY_ASSET_CONTRACTS_en.md` · `es/READCRAFTERY_ASSET_CONTRACTS_es.md`

**Version:** 1.0 — **Status:** Pre-Production

Technical specification for every sprite, node, and asset the game expects. Defines exact filenames, dimensions, formats, and export requirements. Use this alongside the Art Style Guide when producing art assets for the official game or for a community mod.

### Modding Guide
*Coming in M3.* Will document how to create and distribute Book Packs and Theme Packs using the public SDK.

---

## Repository structure

```
readcraftery-docs/
├── en/
│   ├── READCRAFTERY_GDD_en.md
│   ├── READCRAFTERY_ART_GUIDE_en.md
│   └── READCRAFTERY_ASSET_CONTRACTS_en.md
└── es/
    ├── READCRAFTERY_GDD_es.md
    ├── READCRAFTERY_ART_GUIDE_es.md
    └── READCRAFTERY_ASSET_CONTRACTS_es.md
```

---

## Who this is for

| Audience | Recommended reading |
|---|---|
| **Modder** creating a Book Pack | GDD §11 (modding model) · Asset Contracts · Modding Guide (M3) |
| **Illustrator** creating a Theme or book art | Art Style Guide · Asset Contracts |
| **Teacher** evaluating the game | GDD §1–§3, §14 (monetization) |
| **Press / collaborator** | GDD §1–§3 |

---

## Related repositories

| Repo | Visibility | Purpose |
|---|---|---|
| [`readcraftery`](https://github.com/The-Readcraftery-Project/readcraftery) | 🔒 Private | Engine + official content. Full Godot project. |
| [`readcraftery-docs`](https://github.com/The-Readcraftery-Project/readcraftery-docs) | 🌐 Public | This repo. GDD, Art Guide, Asset Contracts, Modding Guide. |
| [`readcraftery-dev-docs`](https://github.com/The-Readcraftery-Project/readcraftery-dev-docs) | 🔒 Private | Architecture Contract + Build Guide. Internal engine docs. |
| [`readcraftery-SDK`](https://github.com/The-Readcraftery-Project/readcraftery-SDK) | 🌐 Public | Book pack / theme schemas, Preview Tool (M3), examples. |

---

## License

The documents in this repository are licensed under [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/).

You may read, share, adapt, and translate them freely — including as reference for creating mods — as long as you give attribution and do not use them for commercial purposes.

This license covers the documentation only. The Readcraftery engine, official content, and assets in other repositories are governed by separate terms.

---

*Part of the [The-Readcraftery-Project](https://github.com/The-Readcraftery-Project) organization.*
