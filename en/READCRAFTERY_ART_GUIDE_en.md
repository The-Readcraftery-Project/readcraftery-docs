# READCRAFTERY — Art Style Guide
**Version:** 1.5  
**Date:** March 2026  
**Status:** Pre-Production  
**Companion documents:** GDD v1.4 · Architecture Contract v1.3 · Build Guide v1.5

---

> **Language patch note:** This English version was normalized from the current working draft to keep terminology, identifiers, and document roles consistent across the bilingual set. Technical names, class names, routes, JSON keys, and code identifiers were preserved as-is.

---

> **How to read this document**
>
> This document has two audiences:
> - **Developer / artist** — visual direction, character, technical production specs
> - **Modders** — guide to create themes and book packs with compatible visual assets
>
> Sections §1–§7 are for internal production. Section §8 is the public guide for modders.
> This document uses **pixel art with Strategy B** as the definitive style — sprites at
> 64×64 px master draw size for Owlorumo, scaled per context (3× in PassageView, 4× in Library/menu).
> All other sprites at 16–24 px draw size, scaled 4×. Text always at native resolution.
> This decision is closed. The technical sections (§5–§7) reflect this choice.

---

## Table of Contents

1. [Visual References and Philosophy](#1-visual-references-and-philosophy)
2. [Palette and Color Values](#2-palette-and-color-values)
3. [Owlorumo — Character Design](#3-owlorumo--character-design)
4. [The Default Theme — The Sleeping Library](#4-the-default-theme--the-sleeping-library)
5. [Shape Language & Rendering Rules](#5-shape-language--rendering-rules)
6. [UI Readability Doctrine](#6-ui-readability-doctrine)
7. [Technical Production Specifications](#7-technical-production-specifications)
8. [Guide for Modders — Creating a Theme](#8-guide-for-modders--creating-a-theme)
9. [Asset Priority for First Playable](#9-asset-priority-for-first-playable)
10. [Acceptance Criteria Visual](#10-acceptance-criteria-visual)
11. [What Is Still Open](#11-what-is-still-open)

---

## 1. Visual References and Philosophy

### The Two Foundational References

**Choose Your Own Adventure (1979–1998, Bantam Books)**  
The interactive adventure books of the 80s have a specific visual quality we want to capture: illustrations with *narrative weight*, worlds that feel inhabited and slightly dangerous but fascinating, dramatic compositions with strong light contrast, and a warm palette interrupted by flashes of impossible color. Interior illustrations were black and white with great expressiveness of line — each scene suggested a larger world beyond the frame.

What we take: **the sense that each screen is a page of a real book**. The game must feel like being *inside* an illustration from those books.

What we don't take: the dark drama. READCRAFTERY is for children aged 4–9 — the tone is magical and welcoming, not tense.

**Dr. Seuss (Theodor Seuss Geisel, 1937–1991)**  
Seuss's visual universe has very specific rules that make it immediately recognizable and deeply child-like in the best sense:
- **Nothing is perfectly straight.** Towers twist, trees curve, houses lean. There is organic life in every line.
- **Textures are invented.** No real skin, no real wood — textures that only exist in that world.
- **The palette is limited and bold.** Few colors, highly saturated, with strong contrasts. The white of the page (or light background) works as its own color.
- **Characters have exaggerated expressiveness but are never frightening.** Big eyes, theatrical poses, clear emotions from a distance.
- **Typography and illustrations coexist as part of the same visual world.**

What we take: **the line with personality, organic shapes, the bold palette, the invented texture**.

What we don't take: the extreme eccentricity. We want the world to be recognizable — a library is a library — but drawn with that organic warmth.

### The synthesis: Storybook Arcane

The resulting style has its own name in this document: **Storybook Arcane**.

It is a hand-drawn magical library, where:
- Books on shelves have impossible colors and glow softly
- Furniture curves slightly, as if it had grown rather than been built
- Magic is ambient, not explosive — rays of light, motes of golden dust, softly blinking runes
- Everything has tactile texture — grainy paper, woven fabric, grained wood
- Colors are rich and warm, with a deep night-blue counterpoint for magic

### Three words that define the style

**Warm.** The game must feel like a rainy afternoon with a cup of something hot and a good book.  
**Alive.** Nothing is perfectly static. Things breathe softly even at rest.  
**Honest.** The illustration has the deliberate imperfection of something made by hand, not the coldness of a perfect vector.

### What to explicitly avoid

- ❌ **Modern flat design** — textureless icons, minimalist gradients, productivity-app look
- ❌ **Chibi / anime** — Japanese large-head proportions do not fit the reference
- ❌ **Smooth digital illustration** — perfect vectors, soft gradients, no pixel texture
- ❌ **Realism** — correct anatomical proportions, PBR lighting
- ❌ **Dark fantasy** — skulls, claws, unsettling darkness; even the wizard is friendly

### Pixel art — the closed decision

The visual style of READCRAFTERY is **pixel art**, with Strategy B scaling (see §5).

The core reason: text is the product. A 5-year-old needs perfectly sharp text on any screen. Pixel art with Strategy B allows text at native 1080p resolution while sprites and backgrounds live at their natural resolution scaled to 4×. There is no trade-off between visual warmth and text readability.

Pixel art is also consistent with the references: the CYOA books of the 80s are the first books many of us chose to read of our own free will — they have a direct relationship with the pixel art era. And Owlorumo in well-executed pixel art has more personality than in any other style at its level of production complexity.

---

## 2. Palette and Color Values

### Core Palette — The Sleeping Library

These are the color values for the default theme. Modder themes may use completely different palettes, but must maintain the same **functional roles** (see §6).

```text
BACKGROUNDS AND SURFACES
────────────────────────────────────────────────────────────
background          #2C1A0E   Night brown — the color of the darkened library
surface             #4A2E1A   Mahogany brown — shelves, wood panels
surface_light       #6B4226   Warm brown — lit surfaces
parchment           #F5E6C8   Parchment — reading passage background
parchment_shadow    #E8D4A8   Parchment shadow — paper edges, dividers

TEXT
────────────────────────────────────────────────────────────
text_primary        #2C1A0E   On parchment: dark ink
text_primary_light  #F5E6C8   On dark backgrounds: parchment
text_secondary      #8B6914   Golden brown — subtitles, labels, metadata

ACCENT AND MAGIC
────────────────────────────────────────────────────────────
accent              #D4A017   Gold — highlights, selections, restoration cues
accent_warm         #E8721A   Amber — primary buttons, CTA
magic_glow          #7B4FBE   Magic purple — staff crystal, rune glows, support cues
magic_blue          #1E3A5F   Night blue — depth, magical shadows

FEEDBACK
────────────────────────────────────────────────────────────
correct             #4CAF50   Green — word found correctly
incorrect           #E53935   Soft red — error, but never aggressive
hint                #FF9800   Orange — hint available, suggestion
neutral             #9E9E9E   Grey — inactive or disabled elements
```

### Color usage rules

**Rule 1 — Gold is sacred.**  
`accent` (#D4A017) is reserved for meaningful reading feedback, restoration cues, found-word states, and rare reward moments. Using it on decorative filler degrades it. Every time the player sees gold, they must feel that something living responded.

**Rule 2 — Magic is rare.**  
`magic_glow` (#7B4FBE) appears only on Owlorumo's staff crystal, puzzle support effects, and narrative rune glows. Not in routine functional UI.

**Rule 3 — Text on parchment always uses `text_primary`.**  
Never grey text on a light background for children aged 4–9. Minimum WCAG AA contrast on all reading text.

**Rule 4 — `incorrect` is never the aggressive red of an error.**  
It is a soft, momentary red. The game does not punish — it informs. The error animation lasts a maximum of 500ms and the color returns to neutral state.

### Color accessibility notes

- All game text passes minimum WCAG AA (4.5:1 ratio for small text, 3:1 for large text)
- Feedback colors (`correct`, `incorrect`) are never the **only** signal — they are always accompanied by animation, sound, or icon for colorblind users

### Colorblindness palettes ✅ CLOSED (M1)

**Architecture decision:** The game applies automatic palette transformations as a first line of defense. Modders may optionally provide manual palettes in `theme.json` that replace the automatic transformation for their theme. If they do not provide a manual palette, the automatic transformation is applied. This gives compatibility to all themes without extra work from the modder.

**Recommended validation tool:** Color Oracle (free, macOS/Windows/Linux) — simulates all three conditions in real time on any screen.

**Milestone:** Palettes defined and tested in M1. Integrated into `colorblind_mode` in M2. The Preview Tool validates palette compliance from M1.

```text
DEUTERANOPIA (no green cone — most common, ~6% of men)
Main issue: correct (green) and incorrect (red) are indistinguishable.
────────────────────────────────────────────────────────────────────────
Token           Base palette     Deuteranopia palette   Reason for change
correct         #4CAF50         #1E88E5 (blue)        Green invisible
incorrect       #E53935         #E65100 (orange)      Red visible as brown
accent          #D4A017         #D4A017               Gold-yellow: ok
hint            #FF9800         #FF9800               Orange: ok
magic_glow      #7B4FBE         #0288D1 (cyan)        Purple can be confused
────────────────────────────────────────────────────────────────────────

PROTANOPIA (no red cone — ~2% of men)
Main issue: incorrect (red) appears as dark grey.
────────────────────────────────────────────────────────────────────────
Token           Base palette     Protanopia palette     Reason for change
correct         #4CAF50         #4CAF50               Green: legibly distinct
incorrect       #E53935         #FF6F00 (amber)       Red invisible
accent          #D4A017         #D4A017               Gold: ok
hint            #FF9800         #FF9800               Orange: ok
magic_glow      #7B4FBE         #7B4FBE               Purple: ok
────────────────────────────────────────────────────────────────────────

TRITANOPIA (no blue cone — <0.1%, both sexes)
Main issue: blues and yellows are confused.
────────────────────────────────────────────────────────────────────────
Token           Base palette     Tritanopia palette     Reason for change
correct         #4CAF50         #4CAF50               Green: ok
incorrect       #E53935         #E53935               Red: ok
accent          #D4A017         #E040FB (magenta)     Gold confused with green
magic_glow      #7B4FBE         #E91E63 (pink)        Blue-purple invisible
magic_blue      #1E3A5F         #1B5E20 (dark green)  Dark blue invisible
────────────────────────────────────────────────────────────────────────

RULE COMMON TO ALL THREE MODES:
  correct and incorrect ALWAYS accompanied by shape + animation + sound.
  Color is reinforcement, not the sole signal. Never rely on color alone.
```

---

## 3. Owlorumo — Character Design

### The Story of Owlorumo

> Owlorumo was the companion owl of Athena. When the goddess disappeared
> in the ancient era, his power diminished as the world forgot the habit
> of reading. He remains in the library — the last place where wisdom survived.
> Each word a child finds restores a fragment of what was lost.
>
> This story is never told explicitly. It lives in visual details, in Owlorumo's
> expressions, in the progression of his staff crystal and robe runes.
> `state_4` is a deliberate homage to Tolkien's Gandalf the White:
> fulfilled, not replaced. The blue mantle remains visible.
> The moon brooch, belt, and boots are unchanged.
> The transformation is one of light and presence. Never explained. Only discovered.

### Concept and personality

The companion is named **Owlorumo**. This is the official name — not a working title. References to "the Professor" or "the Istari Owl" in earlier drafts refer to this character.

**Visual personality:** Young, curious, kind, slightly clumsy with magic but never with words. Owlorumo is a companion, not a mentor — he discovers things alongside the child rather than explaining from above. His amber eyes are his most expressive feature: wide with wonder, warm with encouragement, never intimidating.

**The central design tension:** He is more wizard than owl, but the bird nature never disappears. The tension between the two is what makes him visually interesting. Unlike older depictions, Owlorumo has no beard — he is too young for one.

### Character Anatomy

> **Reference:** The confirmed concept art establishes Owlorumo's definitive design.
> All pixel art production must match this reference. When in doubt, this image wins.

```text
PROPORTIONS
────────────────────────────────────────────────────────────
Total height:       Compact and slightly chubby — reads as young
Head:               Large, round — owl characteristic
Eyes:               The most expressive feature. Large, circular,
                    bright amber-gold. Independent eyebrows
                    (owls don't have them — Seuss-style)
Beak:               Small, curved, grey. Prominent but not harsh.
No beard:           Owlorumo is young. No beard.

CLOTHING — confirmed from concept art
────────────────────────────────────────────────────────────
Robe:               Navy blue — deep, dark, closer to #1E2A4A
                    than purple. Long sleeves that cover the
                    wings/hands. Fabric has texture — not flat.
                    Slightly oversized, which adds to the
                    young/apprentice feel.
Neck wrap:          Same navy fabric, wrapped loosely as a scarf.
                    Adds volume and warmth to the silhouette.
Lunar brooch:       Crescent moon clasp on the neck wrap.
                    Gold (#D4A017). Identity detail — always present.
Belt:               Worn brown leather, gold buckle. Cinches the
                    robe at the waist. Gives structure to the
                    otherwise loose silhouette.
Hat:                Tall, pointed, slightly bent at the tip.
                    Same navy as the robe. Band with rune engravings.
                    A feather tucked in the band — brown, natural.
                    Small wooden/bone emblem on the band.
Boots:              Short brown leather boots. Cover the talons
                    completely. Slightly oversized — endearing.

STAFF — integral element (see §3 staff section)
────────────────────────────────────────────────────────────
Wood:               Dark, twisted, organic. Darker than the robe.
Crystal:            Purple-white, glowing. Color: magic_glow
                    (#7B4FBE) in idle, brightens in active states.
                    The crystal is the single most recognizable
                    element of Owlorumo's silhouette after the hat.
Grip:               Owlorumo holds the staff in his left hand.
                    The staff reaches above his head.

BIRD NATURE — what remains visible
────────────────────────────────────────────────────────────
Feathers:           Visible at the neck and shoulders above the
                    robe. Base color: brown-grey, soft.
                    Wing tips visible below the sleeves.
Talons:             Hidden under the boots in standard poses.
                    May appear in jump or celebrate animations.
Movement:           Head turns nearly 180° when thinking
                    (real owl behavior). Neck feathers ruffle
                    slightly when excited. Slow blink is a signal
                    of trust — used in idle and hint animations.
```

### Owlorumo — Companion Progression States

Owlorumo has 5 visual states that unlock progressively as the child completes books.
Each state is a separate sprite atlas — same frame layout, different texture.

| State | Crystal | Robe | Eyes | Unlocked after |
|---|---|---|---|---|
| `state_0` | Cracked, dark | Navy, no runes | Normal | Game start |
| `state_1` | Faint glow | Navy, no runes | Normal | First passage |
| `state_2` | Lit, pulsing | Navy, first rune | Normal | First book |
| `state_3` | Bright | Navy, several runes | Occasional soft glow | 3 books |
| `state_4` | White-gold, blinding | **Blue mantle illuminated white-gold; same brooch, belt, boots** | Constant soft glow | First complete arc |

> `state_4` is a homage to Tolkien's Gandalf the White — never explained, only discovered.

**The first crystal ignition (state_0 → state_2):** When the crystal lights up for the
first time, Owlorumo does not celebrate the child. He looks at them. Two seconds of
silence. The child understands — without anyone explaining — that they did this.
This is the most important moment in the game.

**Production note:** All 5 atlases share identical frame layout. The artist delivers
5 PNG files. `state_0` and `state_1` are M2 blockers. `state_2`, `state_3` = M2.
`state_4` = M3. See Asset Contracts §2 for the technical spec.

### Required animation states

Each state is a loop animation or a one-shot animation. The system uses Godot's `AnimationPlayer`.

| State | Type | Description | Trigger |
|---|---|---|---|
| `idle` | Loop | Soft breathing. Occasional slow blink. Staff tip pulses with soft light. | Default |
| `happy` | Loop | Neck feathers gently ruffled. Slight swaying. Half-closed eyes (owl smile). | Word found, positive progress |
| `thinking` | Loop | Slow head turn. One talon scratches the chin (with staff in the other). | During active puzzle, waiting for input |
| `excited` | One-shot | Wings slightly extended. Short hop. Staff crystal flashes. | Strong completion moment, first book completed |
| `hint` | One-shot | Leans forward. Staff gently points toward the puzzle area. Crystal glowing. | When giving hint |
| `reading` | Loop | Holds an open book. Eyes move slowly from side to side. | During passage read-aloud with TTS |
| `celebrate` | One-shot | Wings fully extended (maximum expansion). `magic_glow` motes emerge from the staff crystal. | Completing an entire book |
| `sleepy` | Loop | Slow nodding. Half-closed eyes. For rest screens or inactivity. | Inactivity timeout |
| `wave` | One-shot | Raises one wing in greeting. For onboarding and player return. | First time, returning to session |

#### Animation → feedback protocol mapping

| Pedagogical event | Animation | Duration |
|---|---|---|
| Inactivity > 8s | `thinking` | Loop until interaction |
| Inactivity > 13s + automatic TTS | `hint` | One-shot |
| Correct word | `happy` | One-shot → returns to `idle` |
| Incorrect word | `idle` | No change — do not express failure |
| Puzzle completed | `celebrate` (M1) / `happy` (M0) | One-shot |
| TTS reading passage | `reading` (M1) / `idle` (M0) | While TTS plays |

> **Golden rule:** Owlorumo never expresses frustration, impatience,
> or disappointment. If an animation could be read as negative,
> it is not used in response to the child's errors.

### Unlockable Accessories (M2)

#### Owlorumo's staff — integral element

The staff with the purple crystal is a permanent, integral part of Owlorumo's design. It is present in every animation state, including `idle`. It is never removed or hidden. The staff is not an accessory — it is part of the character's silhouette.

**Visual rule:** Owlorumo's silhouette must always read as "owl with wizard hat and staff." If a frame cannot accommodate the staff legibly at 64×64px, the crystal glow alone is sufficient to imply it.

**Animation note:** The crystal glow (`magic_glow` `#7B4FBE`) pulses at 0.8Hz in `idle`. In `hint` and `cast` states it brightens to full `#A87FE8` and emits particle sparks.

#### Accessories — earned overlays

Accessories are overlays on top of the base sprite. They do not require redrawing the full character — they are accessory layers.

```text
Categories:
  hats/        — Alternative hats, caps, flower crowns
  scarves/     — Scarves, collars, amulets
  staff_tips/  — Different crystals/ornaments for the staff tip
  badges/      — Medallions on the belt, brooches on the robe
```

Accessories are unlocked through restoration milestones, book milestones, or future theme systems — never through visible point-like accumulation.

### What Owlorumo is NOT

- ❌ Not condescending — never has the face of "you should know this"
- ❌ Not perfect — has ink stains on the robe, slightly ruffled feathers
- ❌ Not bulky or threatening — even if tall, its posture is open
- ❌ Does not float in the air — walks, uses the staff for support
- ✅ Owlorumo speaks — speech complexity adapts to `reading_stage` (see GDD §Owlorumo adaptive language)

---

## 4. The Default Theme — The Sleeping Library

### Library Identity Across Restoration

The library keeps the same core identity across the entire game.
It is not replaced by a different world.
Its truth is revealed progressively through restoration.

**Canonical revealed names:**
- **The Sleeping Library** — early state; dormant, veiled, waiting
- **The Reawakened Library** — mid restoration; warmer, more responsive, more inhabited
- **The Library of Beginnings** — deeper revealed identity; not a pristine return, but an opening into renewed continuity

This naming is narrative and atmospheric.
It does not imply three separate levels, maps, or theme packs.
Artists should treat them as progressive states of the same living library-world.

### Core Palette — The Sleeping Library

The default theme is the first face of the living library-world.
It should feel ancient, warm, tactile, and magical — not flat, generic, or modern.
The child discovers the place as dormant rather than dead.

### Library Scene Composition (main screen)

```text
Overall composition:
  A circular or apsidal library. Shelves up to the ceiling on the walls.
  Rolling library ladder (the kind that slides on a rail).
  Round reading table in the center-front, with warm reading light.
  Large window at the back — soft rain or starry night, depending on the time.
  Owlorumo on a perch/lectern at the right, in `idle` or `reading` state.

Books on the shelves:
  Dormant:        Muted, quiet, dusty only in a gentle way. No lock icon.
                  They do not invite interaction yet.
  Awakened:       Saturated colors. A subtle golden shimmer. Breathe softly.
  Restored:       Constant soft presence. Warmer shelf response, calmer glow.
  
Lighting:
  Primary source: chandeliers/oil lamps. Warm light (#D4A017 tinted).
  Secondary source: awakened books themselves. They emit soft light.
  Magic source: Owlorumo's staff crystal. Pulses at 0.8Hz in idle.
  
Parallax layers (for background animation):
  Layer 1 (closest):  Table, chairs, foreground objects
  Layer 2:            Central shelves, Owlorumo
  Layer 3:            Background shelves
  Layer 4 (furthest): Window, sky/rain
```

### PassageView Composition

```text
General rule:
  The passage remains the visual center at all times.
  Puzzle UI supports reading; it never replaces the act of reading.

Screen composition (desktop/tablet landscape):
  Primary area: PassagePanel
    - Background: parchment (#F5E6C8) with slightly irregular edges
    - Subtle paper texture (very soft grain)
    - Book title: UI/title font, text_secondary color
    - Passage text: Andika or reading font, text_primary color
    - Book illustration (if present in the pack): above or integrated with text
    
  Secondary support area: Puzzle support UI
    - Background: surface (#4A2E1A) with soft wood texture
    - The puzzle support scene is instantiated here
    - Owlorumo may appear nearby in a subordinate support position

  Bottom support row / shared support area:
    - Word inventory / bank support UI
    - Hint button: staff crystal icon, discreet counter if used
    - Exit: small door icon

WordGlow-specific rule:
  The full passage stays visible.
  The child finds the word in the text itself.
  The word inventory is support UI, not the primary resolution surface.
```

### The book as a physical object

Each book pack has a `cover_image`. The Library Scene design shows books on the shelf as 3D-ish objects (illustrated with a light isometric perspective). The default for packs without a `cover_image` is a generic book with the spine color generated from the pack's `id` (hash → color in a limited palette).

---

## 5. Shape Language & Rendering Rules

✅ **CLOSED** — these rules define how READCRAFTERY art must look at the pixel level. Without these rules, two different artists will produce inconsistent assets even if both "follow the style". They are the visual contract of the system.

### Philosophy: organic pixel art, not geometric pixel art

READCRAFTERY's pixel art is not the cold, geometric pixel art of retro action games. It is pixel art with **deliberate organic shapes**: shelf corners curve gently, Owlorumo's hat bends to one side, books have slightly irregular spines. The pixel grid is the medium, not the message.

### Outline rules

```text
MANDATORY OUTLINE on all character sprites, objects, and UI tiles.
  Thickness:    1px exact. Never 2px, never 0px.
  Color:        NOT pure black (#000000). Use the _shadow variant of the dominant color
                in the object. E.g.: a brown book has outline #3E1A00,
                no #000000. Pure black outline flattens and kills depth.
  Exception:    Backgrounds have no outline — they are the "world", not objects in it.
                Ground tiles also have no outer outline.

INNER OUTLINE (inner outline / pillow shading):
  Not used. Pillow shading makes sprites look embossed/generic 3D.
  Shape is defined with shadow blocks, not inner outlines.
```

### Shadow and lighting rules

```text
SHADOWS: flat blocks only.
  Number of shadow colors:   maximum 2 per element (shadow, deep_shadow)
  Gradients:                 NO. Never. A shadow is a flat color.
  Light direction:           upper left on all assets.
                             Direction consistency > realism.
  Cast shadow:               not drawn in the sprite — it is a separate
                             scene effect if needed.

HIGHLIGHTS: a single strategic pixel.
  Number of highlight colors:  maximum 1 per element (light)
  Position:                        upper left corner of the curved shape
  Flat wood surfaces:              no specular highlight — only soft shadow
```

### Detail and density rules

```text
MAXIMUM DETAIL DENSITY:
  Fine elements (1–2px):    maximum 20% of sprite area
  The remaining 80%:        flat color masses or with a single transition

  Reason: at 64×64 drawn, every pixel counts. The eye of a 4-year-old
  must be able to read "owl with hat" from the silhouette, without processing detail.

SILHOUETTE FIRST:
  Owlorumo must be recognizable by silhouette alone at native 64×64.
  Test: desaturate the full sprite and reduce to 12×12 px. If it reads
  as "figure with hat and staff", the silhouette is correct.
  If not recognizable: too much detail or the silhouette is ambiguous.

READING HIERARCHY by asset type:
  Character:    silhouette → facial expression → clothing → details
  Book:         spine color → title (if present) → ornament
  UI tile:      shape → state (normal/selected/found) → decoration
  Background:   atmosphere → narrative elements → ambient details
```

### Organic shape rules

```text
CURVES IN PIXEL ART:
  Curves are built with decreasing pixel steps.
  Correct 45° curve:    2px, 1px, 1px, 2px (irregular steps = organic)
  Incorrect curve:      1px, 1px, 1px, 1px (uniform step = mechanical)

CORNERS:
  Living objects (character, creatures, magical books):  rounded corners
  Inanimate objects (wood, stone, UI frame):             straight corners allowed
  Practical rule: if the object could grow, it has curves. If it was built, it may have angles.

ALLOWED ORGANIC DEFORMATION:
  Owlorumo's hat:              can tilt up to 10° on the vertical axis
  Book spines:                 can be 1–2px wider at the center
  Library walls:               can have slight curvature (max 3px in 480px width)
  Functional UI (buttons, tiles):  NO deformation — must be precise rectangles
```

### Anti-alias and dithering rules

```text
MANUAL ANTI-ALIAS: NOT used.
  Do not mix intermediate colors on outline edges.
  The outline is 1px clean. Pure pixel art has no manual AA.

DITHERING: permitted with restrictions.
  Correct use:    transition between two colors of the same family
                  (surface → surface_light in a large area)
  Incorrect use:  simulating gradients, creating a third intermediate color
  Maximum:        2px dithering band between two color zones
  Pattern:        checkerboard — no lines or decorative patterns
```

### Palette rules per sprite

```text
COLORS PER SPRITE:
  Character (full Owlorumo):         maximum 20 colors (from the master palette)
  Individual object (book, button):  maximum 8 colors
  UI icon:                           maximum 4 colors
  Background (full layer):           maximum 32 colors

  All colors must be in the master palette from §2.
  A color outside the master palette in production = error, not style.
```

---

## 6. UI Readability Doctrine

✅ **CLOSED** — these rules protect the pedagogical function of the game. For a child aged 4–9 learning to read, visual cognitive load matters as much as the mechanic. Art must not only be charming; it must make reading easy.

### The fundamental principle

**Text is king.** In any conflict between "looking pretty" and "being readable", readability wins without discussion. The pedagogical function of READCRAFTERY is exactly: to help a child read a word successfully. Everything that competes with that is noise.

### PassageView rules (the most critical screen)

```text
BACKGROUND BEHIND TEXT:
  The parchment panel is the background of the text. It never has:
  - Texture with contrast > 5% over the parchment base color
  - No animation of any kind while the child reads
  - No visible gradients or color drift
  Allowed: very subtle grain (noise < 3% intensity)

DECORATION IN PASSAGEVIEW:
  The support panel may have wood texture.
  The passage panel: no structural decoration. Only the text and the book illustration.
  Book illustrations: occupy maximum 30% of the passage panel. Never overlap text.

ANIMATIONS DURING READING:
  Active reading status (TTS playing or child reading):
    → Owlorumo enters `reading` state (minimal animation, eyes moving)
    → NO other animation active on screen
    → Parallax: stopped or reduced to 10% of normal speed
  Active puzzle status:
    → Owlorumo may be in `thinking`
    → Support tiles: only hover animation on the touched tile, never on others
```

### Visual hierarchy rules in PassageView

```text
HIERARCHY (visual attention order, most to least):
  1. Target word / active reading focus inside the passage
  2. Passage text
  3. Target card / support prompt
  4. Word inventory / support tiles
  5. Book title
  6. Controls (hint button, exit)
  7. Owlorumo (always subordinate to the reading task)
  8. Background decoration

If an element in positions 5–8 visually competes with 1–3, it is a visual bug.

MINIMUM DISTANCE BETWEEN INTERACTIVE ELEMENTS:
  Between support tiles:          8px on screen (2px at draw scale)
  Between tile and panel edge:   16px on screen (4px at draw scale)
  Between hint button and word bank: 24px on screen (6px at draw scale)
  Minimum tap target for children: 96×96 px on screen (24×24 px at draw scale)
```

### Visual feedback rules

```text
FEEDBACK HIERARCHY (most to least visible):
  1. Correct: word found in passage → warm glow → travels to support destination → SFX
  2. Completion: current scene transforms briefly in place
  3. Error: soft red state 500ms maximum → returns to normal state
  4. Hint: Owlorumo points → crystal glows → subtle area cue

DURATION RULE:
  Positive feedback (correct, completed): may last as long as it remains readable
  Negative feedback (error): maximum 500ms. The game does not punish — it informs.
  Completion transformations: never block the child's next action

FEEDBACK CONTRAST RULE:
  The "found" state must be clearly brighter than "normal"
  The "incorrect" state is momentary — does not persist as a visual identity
  States always come with sound AND animation, never color alone
```

### Library Scene rules

```text
VISUAL RICHNESS PERMITTED:
  The Library Scene CAN be visually rich — it is the "cover" of the game
  Active parallax: allowed in idle (no active interaction)
  Ambient animations: books glowing, dust motes, Owlorumo in `idle`
  
LIMITS OF RICHNESS:
  Awakened books must stand out from purely decorative ones
  The difference between "awakened" and "dormant" books must read in 1 second
  Owlorumo never covers interactive books in his resting position

DURING SELECTION:
  When cursor/finger is over a book: everything else reduces brightness to 70%
  Only the selected book and Owlorumo have active animation
```

### Rule of "how alive is too alive"

```text
DISTRACTION TEST:
  Show the screen to an adult for 3 seconds, then cover it.
  Question: "What was most important on that screen?"
  
  In PassageView: correct answer = "the text / the words"
  In Library:     correct answer = "the available books"
  
  If the answer is "the owl" or "the background" or "the animations",
  there is too much movement or decoration competing with the content.
```

---

## 7. Technical Production Specifications

### Scaling strategy — Strategy B (CLOSED)

```text
STYLE:                    Pixel art
STRATEGY:                 B — viewport 1920×1080, sprites scaled 4×
SCALE FACTOR:             4× (single factor, no exceptions)

Godot viewport:           1920 × 1080 px
Stretch mode:             disabled (no stretch — the viewport IS the resolution)
Aspect ratio:             keep (letterbox if needed)
Texture filter:           Nearest (apply in project settings AND per sprite)

  Project Settings → Rendering → Textures → Default Texture Filter → Nearest
  Project Settings → Rendering → 2D → Snap 2D Transforms to Pixel → ON

Text (reading passages, UI labels) lives at native 1080p resolution.
Sprites and backgrounds live at their drawing resolution scaled to 4×.
Never mix Nearest and Bilinear filters in the same scene.
```

### Drawing → screen resolution table

```text
Asset                   Drawn at         Shown at          Factor
────────────────────────────────────────────────────────────────
Owlorumo (PassageView)  64 × 64 px    →  192 × 192 px     3× integer
Owlorumo (Library/menu) 64 × 64 px    →  256 × 256 px     4× integer
Accessories (overlay)   64 × 64 px    →  matches context  same as base sprite
UI icons                16 × 16 px    →   64 ×  64 px     4×
Buttons / tiles         16 × 16 px    →   64 ×  64 px     4×   (NineSlice)
Scene tiles             16 × 16 px    →   64 ×  64 px     4×
Background (layer)     480 × 270 px   → 1920 × 1080 px    4×
Fragments (small)        8 ×  8 px    →   32 ×  32 px     4×
Fragments (large)       16 × 16 px    →   64 ×  64 px     4×
Transformation bg      480 × 270 px   → 1920 × 1080 px    4×
```

All drawing dimensions are **power of 2** or multiples of 16. Godot accepts any size but GPUs prefer POT for atlases.

### Critical pixel art gotchas in Godot (read before drawing the first sprite)

```text
GOTCHA 1 — Texture filter (the most common, the most destructive)
  Godot applies bilinear by default. Silently destroys pixel art.
  Required fix before any sprite import:
    Project Settings → Rendering → Textures → Default Texture Filter → Nearest
  And per sprite individually if it was imported before the fix:
    Inspector → Texture → Filter → Nearest

GOTCHA 2 — Sub-pixel movement (blur in animations)
  Moving a sprite to position 100.7 px causes partial blur even with Nearest.
  Required fix in Project Settings:
    Rendering → 2D → Snap 2D Transforms to Pixel → ON
  And in code if there is manual movement:
    position = position.round()

GOTCHA 3 — Atlas too large
  A 2048×2048 atlas = 16MB in GPU memory, loaded entirely even if unused.
  Rule: ONE ATLAS PER FAMILY. Do not mix Owlorumo with UI tiles.
    atlas_owlorumo.png   — all character frames
    atlas_ui.png         — tiles, buttons, icons
    atlas_fx.png         — effects (fragments, magic particles)
  Maximum 2048×2048 px per atlas.

GOTCHA 4 — Broken master palette
  If each asset uses independent colors, the game looks inconsistent.
  Solution: define the master palette BEFORE drawing any asset.
  See §2 — Palette. All sprites take colors from there, never outside it.
  Manual anti-alias (intermediate colors on edges) NOT used in pure pixel art.
  The outline is the darkest color of the palette, with no anti-aliasing.

GOTCHA 5 — Importing in Godot
  Godot recompresses textures by default. For pixel art:
    Inspector del archivo → Import → Compress → Mode → Lossless
    Inspector del archivo → Import → Mipmaps → OFF
  Do this before the first sprite, or set it in the import preset
  so it applies automatically to all imported PNGs.
```

### Palette — structure for pixel art

The §2 Sleeping Library palette are the **functional tokens**. The production master palette expands them with the light and shadow variants needed for pixel art:

```text
For each base color, 3 values are generated:
  [base]_shadow   — 25% darker (inner shadows, depth outlines)
  [base]          — the value defined in §2
  [base]_light    — 25% lighter (specular highlights)

Example with parchment (#F5E6C8):
  parchment_shadow:  #C9B898   ← secondary text, paper edges
  parchment:         #F5E6C8   ← main text background
  parchment_light:   #FFF5E0   ← highlight on lit corners

Total master palette: ~32 colors (16 tokens × 2 variants + blacks and whites)
Colors outside the master palette: they do not exist.
```

### Character sprites and assets

```text
Owlorumo — sprite atlas:
  Resolution per frame:   64 × 64 px (master draw size — source of truth)
  Frames per state:       4–8 frames (idle: 4, excited: 8, celebrate: 8)
  Drawing format:         PNG-8 (indexed palette) or PNG-24 with alpha
  Export format:          PNG with transparent alpha
  Target atlas:           atlas_owl.png — max 2048 × 2048
  Naming:                 owl_[state]_[frame_2digits].png
  Anchor point:           center-bottom of the sprite (character feet)
  
  Atlas organization (Godot SpriteFrames):
    Each state is an Animation in AnimatedSprite2D
    FPS per state:    idle=4, thinking=4, happy=6, hint=8, excited=8,
                      reading=4, celebrate=8, sleepy=3, wave=6

Accessories (M2):
  Resolution:         64 × 64 px exact — same size as base sprite
  Anchor point:       IDENTICAL to base sprite — pixel-perfect registration
  Target atlas:       atlas_accessories.png (separate from atlas_owlorumo.png)
  Transparency:       100% alpha in areas without accessory
```

### Backgrounds and scenes

```text
Library Scene — 4 layers for parallax:
  Drawing resolution:   480 × 270 px each layer
  Shown at:             1920 × 1080 px (scale 4×)
  Format:               PNG with alpha on layers 1–2, PNG without alpha on 3–4
  Naming:               bg_library_layer_[1-4].png
  
  Layer 4 (background): Sky/window — no parallax, static
  Layer 3:              Background shelves — slow parallax (factor 0.1)
  Layer 2:              Central shelves + Owlorumo — medium parallax (factor 0.3)
  Layer 1 (front):      Table, foreground objects — normal parallax (factor 0.6)

PassageView — backgrounds:
  ParchmentPanel:     tileable 64 × 64 px (repeats at 4× = 256×256 tile)
  WoodPanel:          tileable 64 × 64 px
  Format:             PNG without alpha

Completion transformation:
  Animated background reaction: 480 × 270 px, 1–8 frames as needed
  Naming:             completion_[frame_2digits].png
  Format:             PNG without alpha
```

### UI elements

```text
Word support tiles:
  Drawing size:       variable × 8 px minimum height (NineSlice: 16px wide, 4px margins)
  Shown at:           ×4 = minimum height 32px — but the tile container
                      must have tap target ≥ 96px high with invisible padding
  States:             normal, hover, selected, found, disabled
  Naming:             tile_word_[state].png

Buttons:
  Drawing size:       24 × 24 px minimum (tap target 96×96 on screen)
  Reason:             Apple/Google require 44pt minimum. For 4-year-old fingers
                      with developing motor coordination: 96px on screen
                      is the comfortable minimum. 64px is at the limit — don't use it.
  NineSlice:          4px margins in drawing = 16px on screen
  States:             normal, hover, pressed, disabled

Icons:
  Drawing size:       16 × 16 px
  Shown at:           64 × 64 px on screen
  Format:             PNG with alpha
  Naming:             icon_[name].png

Fragments:
  Drawing size:       8 × 8 px
  Shown at:           32 × 32 px on screen
  States:             soft, medium, bright (optional 4 animation frames)
  Naming:             fragment_[state]_[frame].png
```

### Fonts — text at native resolution

The passage and UI text **is not pixel art**. It lives at native 1080p resolution for maximum readability. The contrast between sharp text and pixelated sprites is intentional — it reinforces that the text is "real" and the magical world is the game.

```text
Reading font (passage text):
  Function:         Maximum readability for children learning to read
  Style:            Clear serif or literacy-safe face with unambiguous letterforms
                    (b/d/p/q clearly distinct — critical for early readers)
  ✅ SELECTED:      Andika (SIL) — OFL — designed specifically for literacy
                    letterforms engineered to minimize b/d/p/q confusion
  Fallback:         OpenDyslexic — for the dyslexia_font mode in settings
  Sizes:            small=18px, medium=22px, large=28px, xl=34px
  NEVER below 18px for passage text

UI font (labels, titles, buttons):
  Style:            Rounded, readable from 14px, evokes illustrated book lettering
  ✅ SELECTED:      Nunito (Google Fonts) — OFL — rounded, friendly, legible at small sizes
  NEVER italic for functional text. NEVER below 14px.

Common rules:
  - OFL license required ✅ (Andika: SIL OFL · Nunito: OFL)
  - Stored in res://fonts/ as .ttf
  - Subsetted if > 500KB (use pyftsubset — instructions in Build Guide)
  - Download: https://fonts.google.com/specimen/Andika
              https://fonts.google.com/specimen/Nunito
```

### GPU memory budget and HTML5 build size

```text
GPU MEMORY — ACTIVE SCREEN TEXTURES
────────────────────────────────────────────────────────────
Character atlas (atlas_owlorumo.png):
  Content:       ~72 frames × 64×64 → fits in 1024×512 px
  In GPU:        1024 × 512 × 4 bytes = 2MB

UI atlas (atlas_ui.png):
  Content:       tiles, buttons, icons, fragments
  Atlas size:    512 × 512 px
  In GPU:        512 × 512 × 4 bytes = 1MB

Backgrounds (4 layers — SEPARATE FILES, never a single atlas):
  Each layer:    480 × 270 × 4 bytes ≈ 500KB
  Total 4 layers: ~2MB
  ⚠️ If the layers were in a 1920×1080 atlas = 8MB in a single texture
   and would exceed the 2048×2048 limit of school Chromebooks. Do not do this.

Total estimated active-screen texture memory: ~5MB

TEXTURE LIMITS BY PLATFORM (HTML5)
────────────────────────────────────────────────────────────
Chrome desktop:            16384×16384  ✅
Chrome Android high-end:    8192×8192   ✅
Chrome Android low-end:     4096×4096   ⚠️  Test
Safari iOS:                16384×16384  ✅
Firefox:                   16384×16384  ✅
School Chromebook:          2048×2048   ⚠️  Critical target — most common hardware in schools

Derived rule: no individual atlas exceeds 2048×2048. Ever.
The 4 background layers are separate PNG files (480×270 each).
A combined layer atlas at 1920×1080 would break on Chromebooks.

HTML5 BUILD SIZE — THE REAL BUDGET
────────────────────────────────────────────────────────────
Target cap:                < 15MB total (defined in Architecture Contract)
Godot runtime (WASM):      ~10MB (fixed — cannot be reduced)
Content budget:            ~5MB for ALL assets

Breakdown of the available 5MB:
  Textures (atlas_owlorumo + atlas_ui + 4 bg layers):  ~5MB uncompressed
  → With real PNG compression:                            ~1.5–2MB ✅
  UI audio (SFX, ambient music):                       ~1MB
  Fonts (2 subsetted fonts):                           ~0.3MB
  Compiled GDScript code:                              ~0.5MB
  First built-in book pack (text + audio):             ~1MB
  Estimated total:                                     ~4–4.5MB ✅ with margin

⚠️ BLOCKER: test HTML5 export on a real Chromebook or with
   Chrome DevTools → More tools → Rendering → Hardware concurrency: 2 cores
   BEFORE end of M0. If the WASM exceeds 10MB in the build, review
   Godot export options (template size, strips debug info).
```

### Formats and limits

```text
Audio (narration):      OGG Vorbis, max 1MB per file
Images (sprites):       PNG with alpha, max 2MB per file
Images (backgrounds):   PNG without alpha, max 2MB per file
Fonts:                  TTF/OTF, max 5MB per file
Any asset:              max 10MB hard cap

Import settings in Godot (apply to all PNG sprite assets):
  Compress → Mode:      Lossless   (preserves exact pixels)
  Mipmaps:              OFF        (mipmaps destroy pixel art)
  Filter:               Nearest    (already defined in Project Settings, confirm per asset)
```

---

## 8. Guide for Modders — Creating a Theme

> This section is the content of `THEME_CREATION.md` that will be distributed publicly.
> Written for an audience of teachers, indie artists, and modders without a deep technical background.

### What is a theme?

A theme is a set of files that changes the visual appearance of the game without touching the code. The content (books, puzzles) and gameplay do not change.

### Themes and the Library's Identity

A theme in READCRAFTERY does not replace the library.
It reinterprets the same living library-world through a different material and atmospheric language.

This world is first encountered as **The Sleeping Library**.
As restoration progresses, it may be understood as **The Reawakened Library**,
and later as **The Library of Beginnings**.

Themes may change palette, materials, decorative motifs, ambient mood, and
specific accessory accents, but they do not change the library's core function
as a place of books, memory, restoration, and new openings.

### Functional Library Anchors Across Themes

A theme in READCRAFTERY is a visual reinterpretation of the same living library-world.
Themes may change mood, palette, materials, decorative motifs, and ambient identity,
but they do not change gameplay structure, reading-first layout, or the functional roles
of library elements and UI.

- Books remain books: readable, inviting carriers of knowledge.
- Shelves, bookcases, and ledges remain the architecture of discovery.
- Reading tables and surfaces remain places of focus, not decoration only.
- Windows remain key sources of light, atmosphere, and world identity.
- Vertical space — ladders, stairs, upper shelves, towers, balconies — continues to suggest hidden knowledge beyond the immediate frame.
- Owlorumo remains integrated into the same library-world in every theme.

A successful theme does not replace the library. It reveals a different face of the same living library-world.

### Override levels — what you can change and when

Not all overrides are equal. The system has three levels of openness:

**Level 1 — Safe overrides (available from M1):**
Changes that cannot break the game or accessibility even if done wrong. The game validates these automatically.
- Color tokens (`theme.json` → `colors`)
- Library Scene backgrounds (4 PNG layers)
- Theme preview image
- UI sounds (clicks, hover) — specified in M2

**Level 2 — Advanced overrides (available from M2):**
Changes that require more care. The Preview Tool gives warnings but does not block.
- Custom fonts (OFL only — the validator checks the license declared in metadata)
- Companion sprites (complete state atlases only — no individual frames)
- UI tiles: word bank, buttons, icons

**Level 3 — Restricted (not available to external modders):**
Changes that touch layout, systemic accessibility, or incomplete features.
- Colorblindness palettes (the game manages these automatically)
- Completion transformation scene (schema still open — see §11)
- RTL visual layout (Architecture Contract §7.2 open)
- Individual companion frame replacements (full atlas only)
- Anything that changes tap target sizes

### Theme pack structure

```text
my_theme/
├── metadata.json         ← REQUIRED — theme description
├── theme.json            ← REQUIRED — color tokens and asset references
├── preview.png           ← Recommended — 640×360 capture for the selector
├── sprites/
│   ├── owl_idle_01.png   ← Optional — replaces Owlorumo sprites
│   └── ...
├── backgrounds/
│   ├── bg_main.png       ← Optional — background for the Library Scene
│   └── ...
├── ui/
│   ├── tile_word_normal.png   ← Optional — word support tiles
│   └── ...
└── fonts/
    └── my_font.ttf       ← Optional — custom font (OFL)
```

### `metadata.json`

```json
{
  "schema_version": "1.0",
  "id": "enchanted_castle",
  "title": "Enchanted Castle",
  "author": "Your Name",
  "version": "1.0.0",
  "description": "A towered library of warm stone, candles, and sleeping corridors of knowledge.",
  "preview": "preview.png",
  "license": "CC BY 4.0",
  "flags": {
    "dark": false,
    "rtl": false
  }
}
```

### `theme.json`

Define colors using the system tokens. **You only need to define the tokens you want to change** — those omitted use The Sleeping Library default values.

```json
{
  "schema_version": "1.0",
  "colors": {
    "background":       "#24140F",
    "surface":          "#4A2B1A",
    "surface_light":    "#6B4025",
    "parchment":        "#F4E8CC",
    "parchment_shadow": "#E3D2A8",
    "text_primary":     "#2A170C",
    "text_primary_light": "#F4E8CC",
    "text_secondary":   "#9A7A3C",
    "accent":           "#D4A017",
    "accent_warm":      "#E8721A",
    "magic_glow":       "#7B4FBE",
    "magic_blue":       "#1E2E4F",
    "correct":          "#4CAF50",
    "incorrect":        "#E53935",
    "hint":             "#FF9800",
    "neutral":          "#8A7B73"
  },
  "backgrounds": {
    "library_layer_1": "backgrounds/castle_layer_1.png",
    "library_layer_2": "backgrounds/castle_layer_2.png",
    "library_layer_3": "backgrounds/castle_layer_3.png",
    "library_layer_4": "backgrounds/castle_sky.png"
  },
  "sprites": {
    "owl_idle":     "sprites/owl_idle_01.png",
    "owl_happy":    "sprites/owl_happy_01.png"
  },
  "fonts": {
    "reading":  "fonts/my_reading_font.ttf",
    "ui":       "fonts/my_ui_font.ttf"
  }
}
```

### Mandatory vs optional color tokens

| Token | Required | Notes |
|---|---|---|
| `background` | ✅ | Main background color |
| `surface` | ✅ | Panels, containers |
| `parchment` | ✅ | Reading text background |
| `text_primary` | ✅ | Text on parchment |
| `text_primary_light` | ✅ | Text on dark backgrounds |
| `accent` | ✅ | Restoration cues, found states, special highlights. **Choose carefully.** Your `accent` must stand out strongly over your `background` (ratio ≥ 3:1). |
| `correct` | ✅ | Positive feedback |
| `incorrect` | ✅ | Error feedback |
| `surface_light` | ❌ | Default: `surface` + 20% luminosity |
| `parchment_shadow` | ❌ | Default: `parchment` - 15% luminosity |
| `text_secondary` | ❌ | Default: `accent` + 30% darker |
| `accent_warm` | ❌ | Default: `accent` with hue +30° |
| `magic_glow` | ❌ | Default: `#7B4FBE` |
| `magic_blue` | ❌ | Default: `#1E3A5F` |
| `hint` | ❌ | Default: `#FF9800` |
| `neutral` | ❌ | Default: `#9E9E9E` |

### Asset specifications for modders

```text
Backgrounds (library layers):
  Drawing resolution:   480 × 270 px per layer (scaled 4× in game)
  Format:               PNG with alpha on layers 1–2, PNG without alpha on 3–4
  Limit:                2MB per file

Owlorumo sprites (optional, Level 2):
  Resolution:           64 × 64 px exact — do NOT scale before exporting
  Format:               PNG with alpha, Filter → Nearest, Mipmaps → OFF
  Anchor point:         center-bottom — must match default pixel-perfect
  Override:             full atlas per state (no individual frame swaps)
  Limit:                100KB per sprite

UI tiles (optional, Level 2):
  Word support tile:    16 × 8 px (NineSlice, 4px margins) — appears 64×32 on screen
  Buttons:              24 × 24 px minimum — appears 96×96 on screen ← tap target for children
  Format:               PNG with alpha
```

### What is NineSlice and how to draw for it?

NineSlice allows a button or tile to stretch to contain text of any length without distorting the corners. It is drawn like this:

```text
┌──┬────────────┬──┐   The 16×16 sprite is divided into 9 zones
│  │            │  │   with 4px margins on each side:
│  │            │  │
├──┼────────────┼──┤   Corners (4px×4px): NEVER stretch
│  │            │  │   Horizontal edges: stretch only in X
│  │   center   │  │   Vertical edges: stretch only in Y
├──┼────────────┼──┤   Center: stretches in X and Y
│  │            │  │
└──┴────────────┴──┘
←4→←────────────→←4→
     (stretches)
```

Practice: draw the 4 corners with your decoration (rounded, ornamented,
whatever fits the theme). The center and the edges can be flat color or simple texture.
In Godot: `NinePatchRect`, `patch_margin_left/right/top/bottom = 4` (in sprite pixels).

### Accessibility rules (automatically validated by the Preview Tool from M1)

A theme that violates these rules will be **blocked** by the Preview Tool — it cannot be published or used:

1. **Minimum contrast:** `text_primary` over `parchment` must have ratio ≥ 4.5:1 (WCAG AA)
2. **Minimum contrast:** `text_primary_light` over `background` must have ratio ≥ 4.5:1
3. **`correct` and `incorrect` cannot be the same color** nor have contrast < 3:1 between them
4. **`accent` must be distinguishable from `background` with ratio ≥ 3:1**

The Preview Tool reports the exact ratio of each failed rule with the value needed to correct it.

---

## 9. Asset Priority for First Playable

✅ Do not produce assets outside M0 until M0 assets are playable and tested in HTML5.

### M0 — First playable passage (absolute minimum)

```text
Character:
  owl_idle_01..04.png        4 frames — Owlorumo exists on screen
  owl_thinking_01..04.png    4 frames — during active puzzle
  owl_hint_01..04.png        4 frames — when giving a hint

Library Scene:
  bg_library_layer_4.png     static background (window/sky) — no parallax yet
  bg_library_layer_3.png     background shelves — no parallax yet
  (layers 1 and 2 can be flat color placeholder in M1)

PassageView:
  parchment_tile.png         64×64 tileable for text background
  wood_tile.png              64×64 tileable for support panel

UI:
  tile_word_normal.png       support tile — base state
  tile_word_selected.png     support tile — selected
  tile_word_found.png        support tile — found
  btn_hint.png               hint button (24×24)
  btn_exit.png               exit button (24×24)
  fragment_soft.png          soft fragment (8×8)
  fragment_bright.png        bright fragment (8×8)
  icon_hint.png              staff crystal icon (16×16)

Completion transformation:
  completion_stub.png        single static frame — placeholder until M1

Total M0: ~20 files. All must be tested in HTML5/Chromebook before M1 art production.
```

### M2 — Complete states and parallax

```text
Character (remaining states):
  owl_happy_01..06.png       6 frames
  owl_excited_01..08.png     8 frames
  owl_reading_01..04.png     4 frames
  owl_celebrate_01..08.png   8 frames
  owl_sleepy_01..04.png      4 frames
  owl_wave_01..06.png        6 frames

Library Scene:
  bg_library_layer_1.png     foreground objects (with alpha)
  bg_library_layer_2.png     central shelves + Owlorumo position (with alpha)
  Active parallax in the 4 layers

UI:
  tile_word_disabled.png     disabled state
  tile_word_hover.png        hover state (desktop)
  btn_*_pressed.png          pressed state for all buttons
  btn_*_disabled.png         disabled state for all buttons
  fragment_pulse_01..04.png  fragment pulse animation (4 frames)
  icon_settings.png, icon_home.png, icon_journal.png (16×16 each)

Completion transformation complete (replaces stub)
```

### M3+ — Accessories, themes, polish

```text
M2:  Owlorumo accessories system (atlas_accessories.png)
     Colorblindness palettes tested and integrated
     First community reference theme

M3+: Rich in-scene completion transformation with particles
     Books as perspective objects on shelf
     RTL assets if Architecture Contract §7.2 is closed
```

---

## 10. Acceptance Criteria Visual

Before considering a milestone visually complete, all checks must pass. These are tests anyone can do — no technical knowledge required.

### Silhouette and readability checks

```text
✓ Owlorumo is recognized as "figure with hat and staff"
  when seeing only the silhouette without color, at native 64×64 px.
  Test: screenshot → desaturate → reduce to 12×12 px → identifiable.

✓ Support tiles read as "words on tiles"
  at 64×32 on screen from 60cm away on a tablet.

✓ An awakened book is distinguishable from a dormant book in < 1 second
  without prior instruction. Test with a 5-year-old child.

✓ Primary action buttons have a touch area ≥ 96×96 px on screen.
  Test: enable Accessibility → Touch → Show Touches on Android, confirm zone.
```

### UI readability checks

```text
✓ Show PassageView 3 seconds to an adult → cover it → ask:
  "What was most important?"
  Correct answer: "the text" or "the words".
  If they say "the owl" or "the background": there is visual noise.

✓ Show Library Scene 3 seconds → cover it → ask:
  "Where would you click to read?"
  Correct answer: points to softly awakened books.
  If they point to Owlorumo or decoration: books do not stand out enough.

✓ Passage text at `small` size (18px) readable from 40cm on a screen
  of a 7-inch tablet. Physical test.

✓ In deuteranopia mode: `correct` and `incorrect` are distinguishable
  without relying only on sound or animation. Test with Color Oracle enabled.
```

### Visual consistency checks

```text
✓ All sprites use colors from the master palette.
  Test: open atlas_owl.png in editor → use eyedropper on 10 random pixels
  → all must be in the master palette from §2.

✓ Owlorumo's outline is exact 1px. No 2px zones, no 0px holes.
  Test: zoom 800% on the sprite → inspect edge.

✓ Light direction is upper left on all sprites.
  Test: verify that shadows are in the lower-right of all assets.

✓ The HTML5 build total is < 15MB (including WASM).
  Test: `du -sh` in the export directory. Blocking if > 15MB.

✓ The game runs at stable 60fps on a mid-range Chromebook.
  Test: Chrome DevTools → Performance → 30 seconds of gameplay.
  If there are drops below 45fps: investigate before continuing.
```

### Storybook warmth checks

```text
✓ Show 3 screenshots of the game to someone who does not know it.
  Question: "Who is this game for?"
  Expected answer: children, reading, magic, warm, library.
  If they say "adults" or "action" or "generic": the style needs work.

✓ The game does NOT look like a productivity app or an education SaaS.
  Subjective check, but important — if it looks like Google Classroom,
  something is wrong with the palette or the shapes.
```

---

## 11. What Is Still Open

⚠️ Do not produce assets in these areas until they are closed.

| Topic | Status | Milestone | Impact |
|---|---|---|---|
| **Style: pixel art, Strategy B** | ✅ Closed | — | — |
| **Colorblindness palettes** | ✅ Closed in architectural decision | Palettes in M1, integration M2 | Test with Color Oracle before M1 |
| **Preview Tool contrast validator** | ✅ Closed — M1 | M1 | — |
| **Specific fonts** | ✅ Closed — Andika (passage) + Nunito (UI) | M0 | Download and commit to `res://fonts/` before building PassageView |
| **Display typography for titles** | ✅ Closed — Nunito (same as UI font) | M0 | Consistent with UI font decision |
| **Owlorumo accessories** | ⚠️ Open — categories defined | M2 | Does not block M0/M1 |
| **Full completion transformation design** | ⚠️ Open — stub in M0 | M1 | Stub sufficient for M0 |
| **Book as perspective object** | ⚠️ Open | M2+ | Can be flat 2D sprite in M0/M1 |
| **RTL visual layout** | 🔴 Blocked — Architecture Contract §7.2 | Post-M3 | Do not produce RTL assets |
| **Visual validation with mock** | ⚠️ Pending | Before end of M0 | 1 Library, 1 PassageView, 1 owl sheet, 1 UI set |

---

*Document: READCRAFTERY Art Style Guide v1.5*  
*Next revision: visual validation mock (before end of M0), colorblindness palettes tested (M1).*
