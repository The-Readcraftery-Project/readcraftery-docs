# READCRAFTERY — Art Style Guide
**Version:** 1.2  
**Date:** March 2026  
**Status:** Pre-Production  
**Companion documents:** GDD v1.2 · Architecture Contract v1.1 · Build Guide v1.3  

---

> **Language patch note:** This English version was normalized from the current working draft to keep terminology, identifiers, and document roles consistent across the bilingual set. Technical names, class names, routes, JSON keys, and code identifiers were preserved as-is.

---


> **How to read this document**
>
> This document has two audiences:
> - **Developer / artist** — visual direction, character, technical production specs
> - **Modders** — guide to create themes and book packs with compatible visual assets
>
> Sections §1–§5 are for internal production. Section §6 is the public guide for modders.
> This document uses **pixel art with Strategy B** as the definitive style — sprites at
> 48×48 px scaled 4× in a 1920×1080 viewport, text always at native resolution.
> This decision is closed. The technical sections (§4–§5) reflect this choice.

---

## Table of Contents

1. [Visual References and Philosophy](#1-visual-references-and-philosophy)
2. [Palette and Color Values](#2-palette-and-color-values)
3. [The Istari Owl — Character Design](#3-the-istari-owl--character-design)
4. [The Default Theme — Cozy Library](#4-the-default-theme--cozy-library)
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
The interactive adventure books of the 80s have a specific visual quality we want to capture: illustrations with *narrative weight*, worlds that feel inhabited and slightly dangerous but fascinating, dramatic compositions with strong light contrast, and a warm palette interrupted by flashes of impossible color (the glowing portal, the luminous creature). Interior illustrations were black and white with great expressiveness of line — each scene suggested a larger world beyond the frame.

What we take: **the sense that each screen is a page of a real book**. The game must feel like being *inside* an illustration from those books.

What we don't take: the dark drama. READCRAFTERY is for children aged 4–9 — the tone is magical and welcoming, not tense.

**Dr. Seuss (Theodor Seuss Geisel, 1937–1991)**  
Seuss's visual universe has very specific rules that make it immediately recognizable and deeply child-like in the best sense:
- **Nothing is perfectly straight.** Towers twist, trees curve, houses lean. There is organic life in every line.
- **Textures are invented.** No real skin, no real wood — textures that only exist in that world.
- **The palette is limited and bold.** Few colors, highly saturated, with strong contrasts. The white of the page (or light background) works as its own color.
- **Characters have exaggerated expressiveness but are never frightening.** Big eyes, theatrical poses, clear emotions desde lejos.
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

Pixel art is also consistent with the references: the CYOA books of the 80s are the first books many of us chose to read of our own free will — they have a direct relationship with the pixel art era. And the Istari Owl in well-executed pixel art has more personality than in any other style at its level of production complexity.

---

## 2. Palette and Color Values

### Palette principal — Cozy Library

These are the color values for the default theme. Modder themes may use completely different palettes, butro deben mantener los mismos **roles funcionales** (ver §6).

```
FONDOS Y SUPERFICIES
────────────────────────────────────────────────────────────
background          #2C1A0E   Night brown — the color of the darkened library
surface             #4A2E1A   Mahogany brown — shelves, wood panels
surface_light       #6B4226   Warm brown — lit surfaces
parchment           #F5E6C8   Pergamino — fondo de pasajes de texto
parchment_shadow    #E8D4A8   Pergamino sombra — bordes de papel, separadores

TEXTO
────────────────────────────────────────────────────────────
text_primary        #2C1A0E   Sobre parchment: tinta oscura
text_primary_light  #F5E6C8   Sobre fondos oscuros: pergamino
text_secondary      #8B6914   Golden brown — subtitles, labels, metadata

ACENTO Y MAGIA
────────────────────────────────────────────────────────────
accent              #D4A017   Dorado — highlights, selecciones, estrellas
accent_warm         #E8721A   Amber — primary buttons, CTA
magic_glow          #7B4FBE   Magic purple — Owlorumo staff crystal, rune glows, puzzle highlights
magic_blue          #1E3A5F   Night blue — depth, magical shadows

FEEDBACK
────────────────────────────────────────────────────────────
correct             #4CAF50   Verde — palabra encontrada correctamente
incorrect           #E53935   Rojo suave — error, pero nunca agresivo
hint                #FF9800   Naranja — pista disponible, sugerencia
neutral             #9E9E9E   Gris — elementos inactivos o deshabilitados
```

### Rules de uso de color

**Rule 1 — Gold is sacred.**  
`accent` (#D4A017) is reserved for achievements, found words, earned stars. Using it on decorative elements degrades it. Every time the player sees gold, they must feel they earned something.

**Rule 2 — Magic is rare.**  
`magic_glow` (#7B4FBE) appears only on Owlorumo's staff crystal, puzzle highlight effects, and narrative rune glows. Not in functional UI.

**Rule 3 — Text on parchment always uses `text_primary`.**  
Never grey text on a light background for children aged 4–9. Minimum WCAG AA contrast on all reading text.

**Rule 4 — `incorrect` is never the aggressive red of an error.**  
It is a soft, momentary red. The game does not punish — it informs. The error animation lasts a maximum of 500ms and the color returns to neutral state.

### Color accessibility notes

- All game text passes minimum WCAG AA (4.5:1 ratio for small text, 3:1 for large text)
- Feedback colors (`correct`, `incorrect`) are never the **only** signal — they are always accompanied by animation, sound, or icon for colorblind users

### Paletas para modos de daltonismo ✅ CLOSED (M1)

**Architecture decision:** The game applies automatic palette transformations as a first line of defense. Modders may optionally provide manual palettes in `theme.json` that replace the automatic transformation for their theme. If they do not provide a manual palette, the automatic transformation is applied. This gives compatibility to all themes without extra work from the modder.

**Recommended validation tool:** Color Oracle (free, macOS/Windows/Linux) — simulates all three conditions in real time on any screen.

**Milestone:** Palettes defined and tested in M1. Integrated into `colorblind_mode` in M2. The Preview Tool validates againstste de paleta desde M1.

```
DEUTERANOPIA (no green cone — most common, ~6% of men)
Problema principal: correct (verde) e incorrect (rojo) son indistinguibles.
────────────────────────────────────────────────────────────────────────
Token           Base palette     Deuteranopia palette   Reason for change
correct         #4CAF50         #1E88E5 (azul)        Verde invisible
incorrect       #E53935         #E65100 (orange)      Red visible as brown
accent          #D4A017         #D4A017               Dorado-amarillo: ok
hint            #FF9800         #FF9800               Naranja: ok
magic_glow      #7B4FBE         #0288D1 (cyan)        Purple can be confused
────────────────────────────────────────────────────────────────────────

PROTANOPIA (sin cono rojo — ~2% hombres)
Problema principal: incorrect (rojo) aparece como gris oscuro.
────────────────────────────────────────────────────────────────────────
Token           Base palette     Protanopia palette     Reason for change
correct         #4CAF50         #4CAF50               Verde: legiblemente distinto
incorrect       #E53935         #FF6F00 (amber)       Rojo invisible
accent          #D4A017         #D4A017               Dorado: ok
hint            #FF9800         #FF9800               Naranja: ok
magic_glow      #7B4FBE         #7B4FBE               Purple: ok
────────────────────────────────────────────────────────────────────────

TRITANOPIA (sin cono azul — <0.1%, ambos sexos)
Problema principal: azules y amarillos se confunden.
────────────────────────────────────────────────────────────────────────
Token           Base palette     Tritanopia palette     Reason for change
correct         #4CAF50         #4CAF50               Verde: ok
incorrect       #E53935         #E53935               Rojo: ok
accent          #D4A017         #E040FB (magenta)     Dorado confundible con verde
magic_glow      #7B4FBE         #E91E63 (pink)        Blue-purple invisible
magic_blue      #1E3A5F         #1B5E20 (verde oscuro) Azul oscuro invisible
────────────────────────────────────────────────────────────────────────

RULE COMMON TO ALL THREE MODES:
  correct and incorrect ALWAYS accompanied by shape + animation + sound.
  Color is reinforcement, not the sole signal. Never rely on color alone.
```

---

## 3. The Istari Owl — Character Design

### Concepto y personalidad

The Istari Owl companion is named **Owlorumo**. This is the official name — not a working title. References to "the Professor" in earlier drafts refer to this character.

**Visual personality:** Young, curious, kind, slightly clumsy with magic but never with words. Owlorumo is a companion, not a mentor — he discovers things alongside the child rather than explaining from above. His amber eyes are his most expressive feature: wide with wonder, warm with encouragement, never intimidating.

**The central design tension:** He is more wizard than owl, but the bird nature never disappears. The tension between the two is what makes him visually interesting. Unlike older depictions, Owlorumo has no beard — he is too young for one.

### Character Anatomy

> **Reference:** The confirmed concept art establishes Owlorumo's definitive design.
> All pixel art production must match this reference. When in doubt, this image wins.

```
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

### Required animation states (M1)

Each state is a loop animation or a one-shot animation. The system uses Godot's `AnimationPlayer`.

| Status | Tipo | Description | Trigger |
|---|---|---|---|
| `idle` | Loop | Soft breathing. Occasional slow blink. Staff tip pulses with soft light. | Default |
| `happy` | Loop | Neck feathers gently ruffled. Slight swaying. Half-closed eyes (owl smile). | Word found, positive progress |
| `thinking` | Loop | Slow head turn. One talon scratches the chin (with staff in the other). | During active puzzle, waiting for input |
| `excited` | One-shot | Wings slightly extended. Short hop. Staff crystal flashes. | 3 stars, first book completed |
| `hint` | One-shot | Leans forward. Staff gently points toward the puzzle area. Crystal glowing. | When giving hint |
| `reading` | Loop | Holds an open book. Eyes move slowly from side to side. | During passage read-aasaje con TTS |
| `celebrate` | One-shot | Wings fully extended (maximum expansion). `magic_glow` magic motes emerge. | Completing an entire book |
| `sleepy` | Loop | Slow nodding. Half-closed eyes. For rest screens or inactivity. | Inactivity timeouad |
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

> **Golden rule:** the Owl never expresses frustration, impatience,
> or disappointment. If an animation could be read as negative,
> it is not used in response to the child's errors.

### Accesorios desbloqueables (M2)

#### Owlorumo's staff — integral element

The staff with the purple crystal is a permanent, integral part of Owlorumo's design. It is present in every animation state, including `idle`. It is never removed or hidden. The staff is not an accessory — it is part of the character's silhouette.

**Visual rule:** Owlorumo's silhouette must always read as "owl with wizard hat and staff." If a frame cannot accommodate the staff legibly at 48×48px, the crystal glow alone is sufficient to imply it.

**Animation note:** The crystal glow (`magic_glow` `#7B4FBE`) pulses at 0.8Hz in `idle`. In `hint` and `cast` states it brightens to full `#A87FE8` and emits particle sparks.

---

#### Accessories — earned overlays

Accessories are overlays on top of the base sprite. They do not require redrawing the full character — they are layereder de accesorios.

```
Categories:
  hats/        — Sombreros alternativos, gorros, coronas de flores
  scarves/     — Bufandas, collares, amuletos
  staff_tips/  — Different crystals/ornaments for the staff tip
  badges/      — Medallions on the belt, brooches on the robe
```

Accessories are earned with accumulated stars. Design in v1.1.

### Lo que NO es el Istari Owl

- ❌ Not condescending — never has the face of "you should know this"
- ❌ Not perfect — has ink stains on the robe, slightly ruffled feathers
- ❌ Not bulky or threatening — even if tall, its posture is open
- ❌ Does not float in the air — walks (with talons), uses the staff for support
- ✅ Owlorumo speaks — speech complexity adapts to `reading_stage` (see GDD §Owlorumo adaptive language)

---

## 4. The Default Theme — Cozy Library

### Library Scene Composition (main screen)

```
Vista general:
  A circular or apsidal library. Shelves up to the ceiling on the walls.
  Escalera de biblioteca con ruedas (la que se desliza en el riel).
  Mesa de lectura redonda en el centro-frente, con un candelabro.
  Large window at the back — soft rain or starry night, depending on the time.
  El Istari Owl en una percha/atril a la right, en estado `idle` o `reading`.

Libros en los estantes:
  Locked:         Covered in dust. Muted colors. Small golden lock.
  Disponibles:    Colores saturados. Un sutil shimmer dorado. "Respiran" levemente.
  Completed:      Constant soft glow. Small stars floating nearby.
  
Lighting:
  Primary source: chandeliers/oil lamps. Warm light (#D4A017 tinted).
  Source secundaria: los propios libros disponibles. Emiten light suave.
  Magic source: Owlorumo's staff crystal. Pulses at 0.8Hz in idle.
  
Parallax layers (for background animation):
  Layer 1 (closest):  Table, chairs, foreground objects
  Layer 2:                Estantes centrales, El Profesor
  Layer 3:                Estantes del fondo
  Layer 4 (furthest): Window, sky/rain
```

### PassageView Composition

```
Screen division (desktop/tablet landscape):
  60% left:  PassagePanel
    - Fondo: parchment (#F5E6C8) con bordes ligeramente irregulares
    - Textura de papel sutil (grain muy suave)
    - Book title: serif font, text_secondary color
    - Texto del pasaje: fuente serif legible, color text_primary
    - Book illustration (if present in the pack): above or integrated with text
    
  40% right:    PuzzlePanel
    - Fondo: surface (#4A2E1A) con textura de madera suave
    - The puzzle is instantiated here
    - Small Professor portrait in top corner — in `thinking` state

  Bottom bar:
    - Word bank: fichas de pergamino con borde dorado
    - Hint button: staff crystal (icon), numeric counter
    - Exit: small door (icon)
```

### The book as a physical object

Each book pack has a `cover_image`. The Library Scene design shows books on the shelf as 3D-ish objects (illustrated with a light isometric perspective). The default for packs without a cover_image is a generic book with the spine color generated from the pack's `id` (hash → color in a limited palette).

---

## 5. Shape Language & Rendering Rules

✅ **CLOSED** — these rules define how READCRAFTERY art must look at the pixel level. Without these rules, two different artists will produce inconsistent assets even if both "follow the style". They are the visual contract of the system.

### Philosophy: organic pixel art, not geometric pixel art

READCRAFTERY's pixel art is not the cold, geometric pixel art of retro action games. It is pixel art with **deliberate organic shapes**: shelf corners curve gently, Owlorumo's hat bends to one side, books have slightly irregular spines. The pixel grid is the medium, not the message. Seuss's warmth can be achieved in pixel art — Stardew Valley and Celeste prove it.

### Rules de outline

```
OUTLINE OBLIGATORIO en todos los sprites de personaje, objetos y UI tiles.
  Grosor:       1px exacto. Nunca 2px, nunca 0px.
  Color:        NO negro puro (#000000). Usar la variante _shadow del color
                dominant in the object. E.g.: a brown book has outline #3E1A00,
                no #000000. Outline negro puro aplana y mata la profundidad.
  Exception:    Backgrounds have no outline — they are the "world", not objects in it.
                Tiles de terreno tampoco tienen outline exterior.

OUTLINE INTERIOR (inner outline / pillow shading):
  Not used. Pillow shading makes sprites look embossed/generic 3D.
  La forma se define con bloque de sombra, no con outline interior.
```

### Shadow and lighting rules

```
SHADOWS: flat blocks only.
  Number of shadow colors:   maximum 2 per element (shadow, deep_shadow)
  Gradientes:                    NO. Nunca. Una sombra es un color plano.
  Light direction:               upper left on all assets.
                                 Direction consistency > realism.
  Sombra proyectada:             no se dibuja en el sprite — es un efecto
                                 de scene separado si se necesita.

HIGHLIGHTS: a single strategic pixel.
  Number of highlight colors:  maximum 1 per element (light)
  Position:                        upper left corner of the curved shape
  Superficies planas/madera:       sin highlight especular — solo sombra suave
```

### Rules de detalle y densidad

```
MAXIMUM DETAIL DENSITY:
  Fine elements (1–2px):    maximum 20% of sprite area
  The remaining 80%:        flat color masses or with a single transition

  Reason: at 48×48 drawn, every pixel counts. The eye of a 4-year-old
  must be able to read "owl with hat" from the silhouette, without processing detail.

SILUETA PRIORITARIA:
  The Istari Owl must be recognizable by silhouette alone at native 48×48.
  Test: desaturate the full sprite and reduce to 12×12 px. If it reads
  as "figure with hat and staff", the silhouette is correct.
  Si no se reconoce, hay demasiado detalle o la silueta es ambigua.

READING HIERARCHY by asset type:
  Character:    silhouette → facial expression → clothing → details
  Book:         spine color → title (if present) → ornament
  UI tile:      shape → state (normal/selected/found) → decoration
  Background:   atmosphere → narrative elements → ambient details
```

### Organic shape rules

```
CURVAS EN PIXEL ART:
  Las curvas se construyen con escalones de pixel decrecientes.
  Correct 45° curve:    2px, 1px, 1px, 2px (irregular steps = organic)
  Incorrect curve:      1px, 1px, 1px, 1px (uniform step = mechanical)

ESQUINAS:
  Living objects (character, creatures, magical books):  rounded corners
  Objetos inanimados (madera, piedra, marco de UI):       esquinas rectas permitidas
  Practical rule: if the object could grow, it has curves. If it was built, it may have angles.

ALLOWED ORGANIC DEFORMATION:
  El sombrero del Profesor:   puede inclinarse hasta 10° sobre el eje vertical
  Book spines:    can be 1–2px wider at the center
  Las paredes de la biblioteca: pueden tener ligera curvatura (max 3px en 480px de ancho)
  Functional UI (buttons, tiles):  NO deformation — must be precise rectangles
```

### Rules de anti-alias y dithering

```
ANTI-ALIAS MANUAL: NO se usa.
  No mezclar colores intermedios en los bordes del outline.
  El outline es 1px limpio. El pixel art puro no tiene AA manual.

DITHERING: permitido con restricciones.
  Correct use:   transition between two colors of the same family
                  (surface → surface_light in a large area)
  Uso incorrecto: simular gradientes, crear un tercer color intermedio
  Maximum:        2px dithering band between two color zones
  Pattern:        checkerboard — no lines or decorative patterns
```

### Rules de paleta por sprite

```
COLORES POR SPRITE:
  Character (full Istari Owl):   maximum 20 colors (from the master palette)
  Individual object (book, button):  maximum 8 colors
  UI icon:                           maximum 4 colors
  Background (full layer):           maximum 32 colors

  Todos los colores deben estar en la master palette de §2.
  A color outside the master palette in production = error, not style.
```

---

## 6. UI Readability Doctrine

✅ **CLOSED** — these rules protect the pedagogical function of the game. For a child aged 4–9 learning to read, visual cognitive load matters as much as the mechanic. Art must not only be charming; it must make reading easy.

### The fundamental principle

**Text is king.** In any conflict between "looking pretty" and "being readable", readability wins without discussion. The pedagogical function of READCRAFTERY is exactly: to help a child read a word successfully. Everything that competes with that is noise.

### PassageView rules (the most critical screen)

```
BACKGROUND BEHIND TEXT:
  El parchment panel es el fondo del texto. Nunca tiene:
  - Textura con contraste > 5% sobre el color base de parchment
  - No animation of any kind while the child reads
  - Gradientes o variaciones de color visibles
  Permitido: grain muy sutil (noise < 3% de intensidad)

DECORATION IN PASSAGEVIEW:
  El puzzle panel puede tener textura de madera.
  The passage panel: no structural decoration. Only the text and the book illustration.
  Book illustrations: occupy maximum 30% of the passage panel. Never overlap text.

ANIMACIONES DURANTE LECTURA:
  Active reading status (TTS playing or child reading):
    → The Istari Owl enters `reading` state (minimal animation, eyes moving)
    → NO other animation active on screen
    → Parallax: detenido o reducido a 10% de velocidad normal
  Status activo de puzzle:
    → El Profesor puede estar en `thinking`
    → Word bank tiles: only hover animation on the touched tile, never on others
```

### Visual hierarchy rules in PassageView

```
HIERARCHY (visual attention order, most to least):
  1. Target word in the passage (glow, soft pulse)
  2. Word bank tiles activos
  3. Texto del pasaje
  4. Book title
  5. Controles (hint button, exit)
  6. El Istari Owl (siempre subordinado al contenido)
  7. Background decoration

If an element in position 5–7 visually competes with 1–3, it is a visual bug.

MINIMUM DISTANCE BETWEEN INTERACTIVE ELEMENTS:
  Entre tiles del word bank:    8px en pantalla (2px en dibujo)
  Entre tile y borde del panel: 16px en pantalla (4px en dibujo)
  Entre hint button y word bank: 24px en pantalla (6px en dibujo)
  Minimum tap target for children: 96×96 px on screen (24×24 px in drawing)
```

### Rules de feedback visual

```
FEEDBACK HIERARCHY (most to least visible):
  1. Correcto: palabra encontrada → glow dorado → vuela al word bank → SFX
  2. Completado: todas las palabras → celebration scene completa
  3. Error: soft red tile 500ms maximum → returns to normal state
  4. Hint: Owlorumo points → crystal glows → subtle highlight in area

DURATION RULE:
  Feedback positivo (correcto, completado): puede durar todo lo necesario
  Negative feedback (error): maximum 500ms. The game does not punish — it informs.
  Celebration animations: never block the child's next action

REGLA DE CONTRASTE DE FEEDBACK:
  The "found" state of a tile must be clearly brighter than "normal"
  The "incorrect" state is momentary — does not persist as a visual state
  Both states always come with sound AND animation, never color alone
```

### Rules de la Library Scene

```
RIQUEZA VISUAL PERMITIDA:
  The Library Scene CAN be visually rich — it is the "cover" of the game
  Active parallax: allowed in idle (no active interaction)
  Animaciones ambient: libros brillando, motas de polvo, el Profesor en `idle`
  
LIMITS OF RICHNESS:
  Los libros interactivos (disponibles) deben destacar sobre los decorativos
  La diferencia entre libro "disponible" y "bloqueado" debe leerse en 1 segundo
  The Professor never covers interactive books in his resting position

DURING SELECTION:
  When cursor/finger is over a book: everything else reduces brightness to 70%
  Only the selected book and Owlorumo have active animation
```

### Rule of "how alive is too alive"

```
DISTRACTION TEST:
  Mostrar la pantalla a un adulto 3 segundos, luego taparla.
  Question: "What was most important on that screen?"
  
  En PassageView: respuesta correcta = "el texto / las palabras"
  En Library: respuesta correcta = "los libros disponibles"
  
  If the answer is "the owl" or "the background" or "the animations",
  there is too much movement or decoration competing with the content.
```

---

## 7. Technical Production Specifications

### Estrategia de escalado — Estrategia B (CLOSED)

```
ESTILO:                   Pixel art
STRATEGY:                 B — viewport 1920×1080, sprites scaled 4×
SCALE FACTOR:             4× (single factor, no exceptions)

Godot viewport:           1920 × 1080 px
Stretch mode:             disabled (no stretch — the viewport IS the resolution)
Aspect ratio:             keep (letterbox si necesario)
Texture filter:           Nearest (TODO — proyecto y por sprite)

  Project Settings → Rendering → Textures → Default Texture Filter → Nearest
  Project Settings → Rendering → 2D → Snap 2D Transforms to Pixel → ON

Text (reading passages, UI labels) lives at native 1080p resolution.
Sprites and backgrounds live at their drawing resolution scaled to 4×.
Nunca mezclar filtro Nearest con Bilinear en la misma scene.
```

### Tabla de resoluciones de dibujo → pantalla

```
Asset                   Dibujado en      Se muestra en    Factor
────────────────────────────────────────────────────────────────
Istari Owl (sprite)     48 × 48 px    →  192 × 192 px     4×
Accessories (overlay)   48 × 48 px    →  192 × 192 px     4×
UI icons                16 × 16 px    →   64 ×  64 px     4×
Buttons / tiles         16 × 16 px    →   64 ×  64 px     4×   (NineSlice)
Scene tiles            16 × 16 px    →   64 ×  64 px     4×
Background (layer)     480 × 270 px   → 1920 × 1080 px    4×
Stars (small)           8 ×  8 px    →   32 ×  32 px     4×
Stars (large)           16 × 16 px    →   64 ×  64 px     4×
Celebration bg         480 × 270 px   → 1920 × 1080 px    4×
```

All drawing dimensions are **power of 2** or multiples of 16. Godot accepts any size but GPUs prefer POT for atlases.

### Critical pixel art gotchas in Godot (read before drawing the first sprite)

```
GOTCHA 1 — Texture filter (the most common, the most destructive)
  Godot aplica bilinear por defecto. Destruye el pixel art silenciosamente.
  Fix OBLIGATORIO antes de cualquier import de sprite:
    Project Settings → Rendering → Textures → Default Texture Filter → Nearest
  Y por sprite individualmente si se importa antes del fix:
    Inspector → Texture → Filter → Nearest

GOTCHA 2 — Sub-pixel movement (blur en animaciones)
  Moving a sprite to position 100.7 px causes partial blur even with Nearest.
  Fix OBLIGATORIO en Project Settings:
    Rendering → 2D → Snap 2D Transforms to Pixel → ON
  And in code if there is manual movement:
    position = position.round()

GOTCHA 3 — Atlas demasiado grande
  A 2048×2048 atlas = 16MB in GPU memory, loaded entirely even if unused.
  Regla: UN ATLAS POR FAMILIA. No mezclar Istari Owl con UI tiles.
    atlas_owl.png        — todos los frames del personaje
    atlas_ui.png         — tiles, botones, iconos
    atlas_fx.png         — effects (stars, magic particles)
  Maximum 2048×2048 px per atlas.

GOTCHA 4 — Master palette rota
  Si cada asset usa colores independientes, el juego se ve inconsistente.
  Solution: define the master palette BEFORE drawing any asset.
  See §2 — Palette. All sprites take colors from there, never outside it.
  Anti-alias manual (colores intermedios en bordes) NO se usa en pixel art puro.
  The outline is the darkest color of the palette, with no anti-aliasing.

GOTCHA 5 — Importing in Godot
  Por defecto Godot recomprime las texturas. Para pixel art:
    Inspector del archivo → Import → Compress → Mode → Lossless
    Inspector del archivo → Import → Mipmaps → OFF
  Hacer esto antes del primer sprite, o hacerlo en el preset de import
  so it applies automatically to all imported PNGs.
```

### Palette — estructura para pixel art

The §2 Cozy Library palette are the **functional tokens**. The production master palette expands them with the light and shadow variants needed for pixel art:

```
Por cada color base, se generan 3 valores:
  [base]_shadow   — 25% darker (inner shadows, depth outlines)
  [base]          — el valor definido en §2
  [base]_light    — 25% lighter (specular highlights)

Ejemplo con parchment (#F5E6C8):
  parchment_shadow:  #C9B898   ← texto secundario, bordes de papel
  parchment:         #F5E6C8   ← fondo principal del texto
  parchment_light:   #FFF5E0   ← highlight en esquinas iluminadas

Total master palette: ~32 colors (16 tokens × 2 variants + blacks and whites)
Colores fuera de la master palette: no existen.
```

### Sprites y assets del personaje

```
Istari Owl — sprite atlas:
  Resolution per frame:   48 × 48 px
  Frames por estado:      4–8 frames (idle: 4, excited: 8, celebrate: 8)
  Formato de dibujo:      PNG-8 (paleta indexada) o PNG-24 con alpha
  Formato de export:      PNG con alpha transparente
  Target atlas:           atlas_owl.png — max 2048 × 2048
  Naming:                 owl_[estado]_[frame_2digits].png
  Punto de anclaje:       centro-base del sprite (pies del personaje)
  
  Atlas organization (Godot SpriteFrames):
    Cada estado es una Animation en AnimationSprite2D
    FPS por estado:   idle=4, thinking=4, happy=6, hint=8, excited=8,
                      reading=4, celebrate=8, sleepy=3, wave=6

Accesorios (M2):
  Resolution:         48 × 48 px exact — same size as base sprite
  Anchor point:       IDENTICAL to base sprite — pixel-perfect registration
  Atlas destino:      atlas_accessories.png (separado de atlas_owl.png)
  Transparency:       100% alpha in areas without accessory
```

### Backgrounds y scenes

```
Library Scene — 4 layers para parallax:
  Drawing resolution:   480 × 270 px each layer
  Shown at:               1920 × 1080 px (scale 4×)
  Formato:                PNG con alpha en layers 1–2, PNG sin alpha en 3–4
  Naming:                 bg_library_layer_[1-4].png
  
  Layer 4 (background): Sky/window — no parallax, static
  Layer 3:            Estantes del fondo — parallax lento (factor 0.1)
  Layer 2:            Estantes centrales + Profesor — parallax medio (factor 0.3)
  Layer 1 (frente):   Mesa, objetos primer plano — parallax normal (factor 0.6)

PassageView — fondos:
  ParchmentPanel:     tileable 64 × 64 px (repeats at 4× = 256×256 tile)
  WoodPanel:          tileable 64 × 64 px
  Format:             PNG without alpha

Celebration scene:
  Animated background: 480 × 270 px, 8–12 frames
  Naming:             celebration_[frame_2digits].png
  Format:             PNG without alpha
```

### UI elements

```
Word Bank tiles:
  Drawing size:   variable × 8 px minimum height (NineSlice: 16px wide, 4px margins)
  Shown at:           ×4 = minimum height 32px — but the tile container
                      debe tener tap target ≥ 96px alto con padding invisible
  Statuss:            normal, hover, selected, found, disabled
  Naming:             tile_word_[estado].png

Botones:
  Drawing size:   24 × 24 px minimum (tap target 96×96 on screen)
  Reason:             Apple/Google require 44pt minimum. For 4-year-old fingers
                      with developing motor coordination: 96px on screen
                      is the comfortable minimum. 64px is at the limit — don't use it.
  NineSlice:          4px margins in drawing = 16px on screen
  Statuss:            normal, hover, pressed, disabled

Iconos:
  Drawing size:   16 × 16 px
  Shown at:           64 × 64 px on screen
  Formato:            PNG con alpha
  Naming:             icon_[nombre].png

Estrellas:
  Drawing size:   8 × 8 px
  Shown at:           32 × 32 px on screen
  States:             empty, filled, shimmer (4 animation frames)
  Naming:             star_[estado]_[frame].png
```

### Fonts — text at native resolution

The passage and UI text **is not pixel art**. It lives at native 1080p resolution for maximum readability. The contrast between sharp text and pixelated sprites is intentional — it reinforces that the text is "real" and the magical world is the game.

```
Source de lectura (pasajes de texto):
  Function:         Maximum readability for children learning to read
  Style:            Clear serif with unambiguous letterforms
                    (b/d/p/q clearly distinct — critical for early readers)
  ✅ SELECTED:      Andika (SIL) — OFL — designed specifically for literacy
                    letterforms engineered to minimize b/d/p/q confusion
  Fallback:         OpenDyslexic — for the dyslexia_font mode in settings
  Sizes:            small=18px, medium=22px, large=28px, xl=34px
  NUNCA menos de 18px para texto de pasaje

UI font (labels, titles, buttons):
  Estilo:           Rounded, readable from 14px, evokes illustrated book lettering
  ✅ SELECTED:      Nunito (Google Fonts) — OFL — rounded, friendly, legible at small sizes
  NUNCA cursiva para texto funcional. NUNCA menos de 14px.

Rules comunes:
  - Licencia OFL obligatoria ✅ (Andika: SIL OFL · Nunito: OFL)
  - Guardadas en res://fonts/ como .ttf
  - Subsetted si > 500KB (usar pyftsubset — instrucciones en Build Guide)
  - Download: https://fonts.google.com/specimen/Andika
              https://fonts.google.com/specimen/Nunito
```

### Presupuesto de memoria GPU y build size HTML5

```
MEMORIA GPU — TEXTURAS EN PANTALLA ACTIVA
────────────────────────────────────────────────────────────
Atlas personaje (atlas_owl.png):
  Content:       ~72 frames × 48×48 → fits in 1024×512 px
  In GPU:        1024 × 512 × 4 bytes = 2MB

Atlas UI (atlas_ui.png):
  Contenido:     tiles, botones, iconos, estrellas
  Atlas size:  512 × 512 px
  In GPU:        512 × 512 × 4 bytes = 1MB

Backgrounds (4 layers — ARCHIVOS SEPARADOS, nunca un atlas):
  Each layer:    480 × 270 × 4 bytes ≈ 500KB
  Total 4 layers: ~2MB
  ⚠️ If the layers were in a 1920×1080 atlas = 8MB in a single texture
     and would exceed the 2048×2048 limit of school Chromebooks. Do not do this.

Total estimado en pantalla activa: ~5MB de texturas en GPU

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

BUILD SIZE HTML5 — EL PRESUPUESTO REAL
────────────────────────────────────────────────────────────
Cap objetivo:              < 15MB total (definido en Architecture Contract)
Godot runtime (WASM):      ~10MB (fijo — no se puede reducir)
Presupuesto para contenido: ~5MB para TODOS los assets

Desglose de los 5MB disponibles:
  Texturas (atlas_owl + atlas_ui + 4 bg layers):  ~5MB sin comprimir
  → With real PNG compression:                       ~1.5–2MB ✅
  UI Audio (SFX, ambient music):                 ~1MB
  Fuentes (2 fuentes subsetted):                   ~0.3MB
  Compiled GDScript code:                        ~0.5MB
  Primer book pack builtin (texto + audio):        ~1MB
  Total estimado:                                  ~4–4.5MB ✅ con margen

⚠️ BLOQUEADOR: testear export HTML5 en Chromebook real o con
   Chrome DevTools → More tools → Rendering → Hardware concurrency: 2 cores
   BEFORE end of M0. If the WASM exceeds 10MB in the build, review
   opciones de export de Godot (template size, strips debug info).
```

### Formats and limits

```
Audio (narration):      OGG Vorbis, max 1MB per file
Images (sprites):       PNG with alpha, max 2MB per file
Images (backgrounds):   PNG without alpha, max 2MB per file
Fuentes:                TTF/OTF, max 5MB por archivo
Cualquier asset:        max 10MB hard cap

Import settings en Godot (aplicar a todos los PNG de sprites):
  Compress → Mode:      Lossless   (preserva pixels exactos)
  Mipmaps:              OFF        (mipmaps destruyen pixel art)
  Filter:               Nearest    (ya definido en Project Settings, confirmar por asset)
```

---

## 8. Guide for Modders — Creating a Theme

> This section is the content of `THEME_CREATION.md` that will be distributed publicly.
> Written for an audience of teachers, indie artists, and modders without a deep technical background.

### ¿What is a theme?

A theme is a set of files that changes the visual appearance of the game without touching the code. The content (books, puzzles) and gameplay do not change.

### Override levels — what you can change and when

Not all overrides are equal. The system has three levels of openness:

**Nivel 1 — Safe overrides (disponible desde M1):**
Changes that cannot break the game or accessibility even if done wrong. The game validates these automatically.
- Color tokens (`theme.json` → `colors`)
- Library Scene backgrounds (4 PNG layers)
- Theme preview image
- UI sounds (clicks, hover) — specified in M2

**Nivel 2 — Advanced overrides (disponible desde M2):**
Changes that require more care. The Preview Tool gives warnings but does not block.
- Custom fonts (OFL only — the validator checks the license declared in metadata)
- Companion sprites (complete state atlases only — no individual frames)
- UI tiles: word bank, botones, iconos

**Level 3 — Restricted (not available to external modders):**
Changes that touch layout, systemic accessibility, or incomplete features.
- Colorblindness palettes (the game manages these automatically)
- Celebration scene (schema still open — see §11)
- Layout RTL visual (Architecture Contract §7.2 abierto)
- Individual companion frame replacements (full atlas only)
- Anything that changes tap target sizes

### Estructura de un theme pack

```
mi_theme/
├── metadata.json         ← REQUIRED — theme description
├── theme.json            ← OBLIGATORIO — tokens de color y referencias a assets
├── preview.png           ← Recommended — 640×360 capture for the selector
├── sprites/
│   ├── owl_idle_01.png   ← Optional — reemplaza sprites del Profesor
│   └── ...
├── backgrounds/
│   ├── bg_main.png       ← Optional — fondo de la Library Scene
│   └── ...
├── ui/
│   ├── tile_word_normal.png   ← Optional — tiles del word bank
│   └── ...
└── fonts/
    └── mi_fuente.ttf     ← Optional — fuente custom (licencia OFL)
```

### `metadata.json`

```json
{
  "schema_version": "1.0",
  "id": "enchanted_forest",
  "title": "Enchanted Forest",
  "author": "Tu Nombre",
  "version": "1.0.0",
  "description": "A magical forest for reading among trees and glowing mushrooms.",
  "preview": "preview.png",
  "license": "CC BY 4.0",
  "flags": {
    "dark": false,
    "rtl": false
  }
}
```

### `theme.json`

Define colors using the system tokens. **You only need to define the tokens you want to change** — those omitas usan los valores del Cozy Library por defecto.

```json
{
  "schema_version": "1.0",
  "colors": {
    "background":       "#0D1F0A",
    "surface":          "#1A3311",
    "surface_light":    "#2A5218",
    "parchment":        "#E8F0D4",
    "parchment_shadow": "#D0E0B0",
    "text_primary":     "#1A0F00",
    "text_primary_light": "#E8F0D4",
    "text_secondary":   "#4A7A2A",
    "accent":           "#8BC34A",
    "accent_warm":      "#FF9800",
    "magic_glow":       "#00BCD4",
    "magic_blue":       "#0A1F15",
    "correct":          "#4CAF50",
    "incorrect":        "#E53935",
    "hint":             "#FF9800",
    "neutral":          "#607D4A"
  },
  "backgrounds": {
    "library_layer_1": "backgrounds/forest_layer_1.png",
    "library_layer_2": "backgrounds/forest_layer_2.png",
    "library_layer_3": "backgrounds/forest_layer_3.png",
    "library_layer_4": "backgrounds/forest_sky.png"
  },
  "sprites": {
    "owl_idle":     "sprites/owl_idle_01.png",
    "owl_happy":    "sprites/owl_happy_01.png"
  },
  "fonts": {
    "reading":  "fonts/mi_fuente_lectura.ttf",
    "ui":       "fonts/mi_fuente_ui.ttf"
  }
}
```

### Tokens de color obligatorios vs opcionales

| Token | Required | Notas |
|---|---|---|
| `background` | ✅ | Color de fondo principal |
| `surface` | ✅ | Paneles, contenedores |
| `parchment` | ✅ | Fondo del texto de lectura |
| `text_primary` | ✅ | Texto sobre parchment |
| `text_primary_light` | ✅ | Texto sobre fondos oscuros |
| `accent` | ✅ | Stars, achievements, highlights. **Choose carefully: the game uses this to reward the child.** Your `accent` must stand out strongly over your `background` (ratio ≥ 3:1). In a cyberpunk theme, neon pink is the new "sacred gold" — use it only for victories. |
| `correct` | ✅ | Feedback positivo |
| `incorrect` | ✅ | Feedback de error |
| `surface_light` | ❌ | Default: `surface` + 20% luminosidad |
| `parchment_shadow` | ❌ | Default: `parchment` - 15% luminosidad |
| `text_secondary` | ❌ | Default: `accent` + 30% oscuridad |
| `accent_warm` | ❌ | Default: `accent` con hue +30° |
| `magic_glow` | ❌ | Default: `#7B4FBE` |
| `magic_blue` | ❌ | Default: `#1E3A5F` |
| `hint` | ❌ | Default: `#FF9800` |
| `neutral` | ❌ | Default: `#9E9E9E` |

### Especificaciones de assets para modders

```
Backgrounds (layers de biblioteca):
  Drawing resolution:   480 × 270 px per layer (scaled 4× in game)
  Formato:      PNG con alpha en layers 1–2, PNG sin alpha en 3–4
  Limit:        2MB per file

Sprites del Profesor (opcionales, Nivel 2):
  Resolution:   48 × 48 px exact — do NOT scale before exporting
  Formato:      PNG con alpha, Filter → Nearest, Mipmaps → OFF
  Punto de anclaje: centro-base — debe coincidir pixel-perfect con default
  Override:     atlas completo por estado (no frames sueltos)
  Limit:        100KB per sprite

UI tiles (opcionales, Nivel 2):
  Word bank tile: 16 × 8 px (NineSlice, 4px margins) — appears 64×32 on screen
  Buttons:        24 × 24 px minimum — appears 96×96 on screen ← tap target for children
  Formato:        PNG con alpha
```

### What is NineSlice and how to draw for it?

NineSlice allows a button or tile to stretch to contain text of any length without distorting the corners. It is drawn like this:

```
┌──┬────────────┬──┐   The 16×16 sprite is divided into 9 zones
│  │            │  │   with 4px margins on each side:
│  │            │  │
├──┼────────────┼──┤   Corners (4px×4px): NEVER stretch
│  │            │  │   Bordes H (top/bottom): se estiran solo en X
│  │   centro   │  │   Bordes V (left/right): se estiran solo en Y
├──┼────────────┼──┤   Centro: se estira en X e Y
│  │            │  │
└──┴────────────┴──┘
←4→←────────────→←4→
     (se estira)

Practice: draw the 4 corners with your decoration (rounded, ornamented,
lo que sea). El centro y los bordes pueden ser color plano o textura simple.
En Godot: NinePatchRect, patch_margin_left/right/top/bottom = 4 (en px del sprite).
```

### Accessibility rules (automatically validated by the Preview Tool from M1)

A theme that violates these rules will be **blocked** by the Preview Tool — it cannot be published or used:

1. **Minimum contrast:** `text_primary` over `parchment` must have ratio ≥ 4.5:1 (WCAG AA)
2. **Minimum contrast:** `text_primary_light` over `background` must have ratio ≥ 4.5:1
3. **`correct` and `incorrect` cannot be the same color** nor have contrast < 3:1 between them
4. **`accent` debe ser distinguible de `background` con ratio ≥ 3:1**

El Preview Tool reporta el ratio exacto de cada regla fallida con el valor necesario para corregirlo.

---

## 9. Asset Priority for First Playable

✅ Do not produce assets outside M0 until M0 assets are playable and tested in HTML5.

### M0 — First playable passage (absolute minimum)

```
Personaje:
  owl_idle_01..04.png        4 frames — el Profesor existe en pantalla
  owl_thinking_01..04.png    4 frames — durante puzzle activo
  owl_hint_01..04.png        4 frames — al dar pista

Library Scene:
  bg_library_layer_4.png     static background (window/sky) — no parallax yet
  bg_library_layer_3.png     estantes del fondo — sin parallax por ahora
  (layers 1 y 2 pueden ser placeholder de color plano en M0)

PassageView:
  parchment_tile.png         64×64 tileable for text background
  wood_tile.png              64×64 tileable for puzzle panel

UI:
  tile_word_normal.png       word bank tile — estado base
  tile_word_selected.png     word bank tile — seleccionado
  tile_word_found.png        word bank tile — encontrado
  btn_hint.png               hint button (24×24)
  btn_exit.png               exit button (24×24)
  star_empty.png             empty star (8×8)
  star_filled.png            filled star (8×8)
  icon_hint.png              staff crystal (16×16)

Celebration:
  celebration_stub.png       single static frame — placeholder until M1

Total M0: ~20 archivos. Todos deben testear en HTML5/Chromebook antes de M1.
```

### M1 — Statuss completos y parallax

```
Personaje (estados restantes):
  owl_happy_01..06.png       6 frames
  owl_excited_01..08.png     8 frames
  owl_reading_01..04.png     4 frames
  owl_celebrate_01..08.png   8 frames
  owl_sleepy_01..04.png      4 frames
  owl_wave_01..06.png        6 frames

Library Scene:
  bg_library_layer_1.png     objetos primer plano (con alpha)
  bg_library_layer_2.png     central shelves + Professor position (with alpha)
  Parallax activo en los 4 layers

UI:
  tile_word_disabled.png     estado deshabilitado
  tile_word_hover.png        estado hover (desktop)
  btn_*_pressed.png          estado pressed para todos los botones
  btn_*_disabled.png         estado disabled para todos los botones
  star_shimmer_01..04.png    shimmer animation (4 frames)
  icon_star.png, icon_settings.png, icon_home.png (16×16 each)

Celebration scene completa (reemplaza stub)
```

### M2+ — Accesorios, themes, polish

```
M2:  Sistema de accesorios del Profesor (atlas_accessories.png)
     Paletas de daltonismo testeadas e integradas
     Primer theme comunitario de referencia

M3+: Rich Celebration scene with particles
     Libros como objetos con perspectiva en estante
     Assets RTL si el contrato de §7.2 se cierra
```

---

## 10. Acceptance Criteria Visual

Before considering a milestone visually complete, all checks must pass. These are tests anyone can do — no technical knowledge required.

### Checks de silueta y legibilidad

```
✓ The Istari Owl is recognized as "figure with hat and staff"
  when seeing only the silhouette without color, at native 48×48 size.
  Test: screenshot → desaturate → reduce to 12×12 → identifiable.

✓ Los tiles del word bank se leen como "palabras en fichas"
  at 64×32 on screen from 60cm away on a tablet.

✓ Un libro disponible se distingue de uno bloqueado en < 1 segundo
  without prior instruction. Test with a 5-year-old child.

✓ Primary action buttons have a touch area ≥ 96×96 px on screen.
  Test: activar Accessibility → Touch → Show Touches en Android, confirmar zona.
```

### Checks de UI readability

```
✓ Mostrar PassageView 3 segundos a un adulto → tapar → preguntar:
  "What was most important?"
  Respuesta correcta: "el texto" o "las palabras".
  If they say "the owl" or "the background": there is visual noise.

✓ Mostrar Library Scene 3 segundos → tapar → preguntar:
  "Where would you click to read?"
  Correct answer: points to glowing books.
  If they point to Owlorumo or decoration: books do not stand out enough.

✓ Passage text at `small` size (18px) readable from 40cm on a screen
  of a 7-inch tablet. Physical test.

✓ En modo daltonismo deuteranopia: `correct` e `incorrect` son distinguibles
  without sound or animation. Test with Color Oracle enabled.
```

### Checks de consistencia visual

```
✓ Todos los sprites usan colores de la master palette.
  Test: abrir atlas_owl.png en editor → usar cuentagotas en 10 pixels random
  → todos deben estar en la master palette de §2.

✓ El outline del Profesor tiene 1px exacto. Sin zonas de 2px ni 0px.
  Test: zoom 800% en el sprite → inspeccionar borde.

✓ Light direction is upper left on all sprites.
  Test: verify that shadows are in the lower-right of all assets.

✓ El build HTML5 total es < 15MB (incluyendo WASM).
  Test: `du -sh` en el directorio de export. Bloqueador si > 15MB.

✓ El juego corre a 60fps estables en Chromebook de gama media.
  Test: Chrome DevTools → Performance → 30 segundos de gameplay.
  Si hay drops bajo 45fps: investigar antes de continuar.
```

### Checks de storybook warmth

```
✓ Mostrar 3 screenshots del juego a alguien que no lo conoce.
  Question: "Who is this game for?"
  Expected answer: children, school, reading, magic/magical.
  If they say "adults" or "action" or "generic": the style needs work.

✓ The game does NOT look like a productivity app or an education SaaS.
  Check subjetivo pero importante — si tiene look de Google Classroom,
  something is wrong with the palette or the shapes.
```

---

## 11. What Is Still Open

⚠️ Do not produce assets in these areas until they are closed.

| Tema | Status | Milestone | Impacto |
|---|---|---|---|
| **Estilo: pixel art, Estrategia B** | ✅ Cerrado | — | — |
| **Colorblindness palettes** | ✅ Closed in architectural decision | Palettes in M1, integration M2 | Test with Color Oracle before M1 |
| **Validador contraste Preview Tool** | ✅ Cerrado — M1 | M1 | — |
| **Specific fonts** | ✅ Closed — Andika (passage) + Nunito (UI) | M0 | Download and commit to `res://fonts/` before building PassageView |
| **Display typography for titles** | ✅ Closed — Nunito (same as UI font) | M0 | Consistent with UI font decision |
| **Istari Owl accessories** | ⚠️ Open — categories defined | M2 | Does not block M0/M1 |
| **Full Celebration Scene design** | ⚠️ Open — stub in M0 | M1 | Stub sufficient for M0 |
| **Book as perspective object** | ⚠️ Open | M2+ | Can be flat 2D sprite in M0/M1 |
| **RTL visual layout** | 🔴 Blocked — Architecture Contract §7.2 | Post-M3 | Do not produce RTL assets |
| **Visual validation with mock** | ⚠️ Pending | Before end of M0 | 1 Library, 1 PassageView, 1 owl sheet, 1 UI set |

---

*Documento: READCRAFTERY Art Style Guide v1.3*  
*Next revision: visual validation mock (before end of M0), colorblindness palettes tested (M1).*
