# READCRAFTERY — Asset Contracts
**Version:** 1.0  
**Date:** March 2026  
**Status:** Pre-Production  
**Companion documents:** Art Guide v1.2 · Build Guide v1.3 · Architecture Contract v1.1

---

> **Language patch note:** This English version was normalized from the current working draft to keep terminology, identifiers, and document roles consistent across the bilingual set. Technical names, class names, routes, JSON keys, and code identifiers were preserved as-is.

---


> **Purpose of this document**
>
> Each row in each table is a contract between code and art.
> Code is written against these tables — never against the final art.
> Art is produced against these tables — never against the code.
> When the real art arrives, the change is texture replacement, not refactoring.
>
> **How to use placeholders:**
> For each asset, instantiate the correct `node_type` with `modulate = Color("hex")`
> using the `placeholder_color` from the table. When the art arrives: assign the
> texture, remove the modulate. Nothing else changes.
>
> **Global scale:** all game assets are drawn at native pixels
> y are shown at 4× en viewport 1920×1080. `display_size` = `draw_size × 4`.
> Passage text and UI labels live at native 1080p resolution — they do not scale.

---

## Table of Contents

1. [Conventions](#1-convenciones)
2. [Shared Assets — Global UI](#2-assets-compartidos--global-ui)
3. [Library Scene](#3-library-scene)
4. [PassageView Scene](#4-passageview-scene)
5. [WordGlow Puzzle](#5-wordglow-puzzle)
6. [Scramble Puzzle](#6-scramble-puzzle)
7. [WordHunt Puzzle](#7-wordhunt-puzzle)
8. [FillPassage Puzzle](#8-fillpassage-puzzle)
9. [RhymeFinder Puzzle](#9-rhymefinder-puzzle)
10. [Celebration Scene](#10-celebration-scene)
11. [Journal Scene](#11-journal-scene)
12. [Settings Scene](#12-settings-scene)
13. [Onboarding Flow](#13-onboarding-flow)

---

## 1. Conventions

### Columns de la tabla

| Column | Description |
|---|---|
| `asset_id` | Filename without extension. It is the canonical identifier. |
| `node_type` | Godot node that renders this asset. Use this node in the placeholder — it does not change when the arte. |
| `draw_size` | Drawing pixel dimensions (what the artist draws). |
| `display_size` | On-screen dimensions at 4×. For NinePatch: minimum container size. |
| `anchor` | Node anchor point. In Godot: `PRESET_*` from the `Control` enum or `centered` for `Sprite2D`. |
| `states` | List of required visual states. Each state = a separate PNG file (or frame in AnimatedSprite2D). |
| `animates` | Whether the asset has a loop or one-shot animation. Format: `type (Nframes @ Xfps)`. |
| `layout_role` | `structural` = defines layout (moving it breaks the screen) · `interactive` = the child touches this · `decorative` = visual only |
| `priority` | Milestone by which real art must exist. M0 = blocker for first playable passage. |
| `placeholder_color` | Palette token for the placeholder ColorRect/modulate. |

### Node types used in this document

```
Sprite2D          — static image, does not participate in Control layout
AnimatedSprite2D  — sprite with multiple animations (the Istari Owl)
TextureRect       — imagen en el sistema de layout de Control (se estira/adapta)
NinePatchRect     — imagen que se estira sin distorsionar esquinas (tiles, botones)
TextureButton     — textured button, handles hover/pressed/disabled automatically
AnimationPlayer   — no renderiza — controla animaciones de otros nodos
ParallaxBackground/ParallaxLayer — nodos de parallax de Godot
ColorRect         — SOLO para placeholders. Reemplazar cuando llega el arte.
```

### Placeholder pattern in GDScript

```gdscript
# Correct placeholder — the node is already the final type
@onready var btn_hint: TextureButton = $BottomBar/BtnHint

func _ready() -> void:
    # Placeholder: solid color until the art arrives
    # When the art arrives: remove these 2 lines and assign texture_normal
    var placeholder := ColorRect.new()
    placeholder.color = Color("#D4A017")  # accent — color del token
    placeholder.size = Vector2(96, 96)    # display_size
    btn_hint.add_child(placeholder)
```

### Typography — closed decision

✅ **CLOSED**

| Context | Type | Owner |
|---|---|---|
| Passage text (the child reads) | Pedagogical font `.ttf`/`.otf` | Not an art asset |
| Interactive puzzle tiles (Scramble, WordHunt, word bank) | Pixel art letters — sprite | Artist |

**Passage text:** uses a font from the pedagogical typography system
(Andika / Lexie Readable / OpenDyslexic — decision pending in Art Guide §7).
Text lives at native 1080p resolution, does not scale with sprites.
No art asset required for this context.

**Pixel art letters:** drawn as `16×16 px` sprites → `64×64 px` on screen.
Included in the UI atlas. Artist delivers A–Z uppercase and lowercase + 0–9 minimum.
Same pipeline as any other sprite: transparent background, master palette, 1px outline.

---

## 2. Shared Assets — Global UI

Assets that appear in multiple scenes. Defined once, referenced in each scene.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `owl_idle` | AnimatedSprite2D | 48×48 | 192×192 | bottom-center | — | loop (4fr @ 4fps) | decorative | M0 | `#4A2E1A` surface |
| `owl_thinking` | AnimatedSprite2D | 48×48 | 192×192 | bottom-center | — | loop (4fr @ 4fps) | decorative | M0 | `#4A2E1A` surface |
| `owl_hint` | AnimatedSprite2D | 48×48 | 192×192 | bottom-center | — | one-shot (4fr @ 8fps) | decorative | M0 | `#4A2E1A` surface |
| `owl_happy` | AnimatedSprite2D | 48×48 | 192×192 | bottom-center | — | loop (6fr @ 6fps) | decorative | M1 | `#4A2E1A` surface |
| `owl_excited` | AnimatedSprite2D | 48×48 | 192×192 | bottom-center | — | one-shot (8fr @ 8fps) | decorative | M1 | `#4A2E1A` surface |
| `owl_reading` | AnimatedSprite2D | 48×48 | 192×192 | bottom-center | — | loop (4fr @ 4fps) | decorative | M1 | `#4A2E1A` surface |
| `owl_celebrate` | AnimatedSprite2D | 48×48 | 192×192 | bottom-center | — | one-shot (8fr @ 8fps) | decorative | M1 | `#4A2E1A` surface |
| `owl_sleepy` | AnimatedSprite2D | 48×48 | 192×192 | bottom-center | — | loop (4fr @ 3fps) | decorative | M1 | `#4A2E1A` surface |
| `owl_wave` | AnimatedSprite2D | 48×48 | 192×192 | bottom-center | — | one-shot (6fr @ 6fps) | decorative | M1 | `#4A2E1A` surface |
| `star_empty` | TextureRect | 8×8 | 32×32 | center | — | no | interactive | M0 | `#9E9E9E` neutral |
| `star_filled` | TextureRect | 8×8 | 32×32 | center | — | no | interactive | M0 | `#D4A017` accent |
| `star_shimmer` | AnimatedSprite2D | 8×8 | 32×32 | center | — | one-shot (4fr @ 8fps) | decorative | M1 | `#D4A017` accent |
| `icon_hint` | TextureRect | 16×16 | 64×64 | center | — | no | decorative | M0 | `#7B4FBE` magic_glow |
| `icon_star` | TextureRect | 16×16 | 64×64 | center | — | no | decorative | M1 | `#D4A017` accent |
| `icon_settings` | TextureRect | 16×16 | 64×64 | center | — | no | decorative | M1 | `#F5E6C8` parchment |
| `icon_home` | TextureRect | 16×16 | 64×64 | center | — | no | decorative | M1 | `#F5E6C8` parchment |
| `icon_back` | TextureRect | 16×16 | 64×64 | center | — | no | interactive | M1 | `#F5E6C8` parchment |

### Implementation notes — Owl

The Istari Owl uses **a single `AnimatedSprite2D` node** with multiple named animations. They are not separate nodes.

```gdscript
# En cualquier scene que muestre el Owl:
@onready var owl: AnimatedSprite2D = $Owl

func set_owl_state(state: String) -> void:
    owl.play(state)  # state = "idle", "thinking", "hint", etc.
```

The atlas is at `res://content/atlas_owl.png`. Animations are defined in the `SpriteFrames` resource assigned to the node — not in code.

---

## 3. Library Scene

**Archivo:** `res://scenes/Library/Library.tscn`  
**Function:** Main menu. The child selects a book to read.  
**Layout:** Full screen. 4-layer parallax. Owl in fixed right position.

### Background — parallax layers

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `bg_library_layer_4` | Sprite2D (in ParallaxLayer) | 480×270 | 1920×1080 | top-left | — | no (estático) | structural | M0 | `#2C1A0E` background |
| `bg_library_layer_3` | Sprite2D (en ParallaxLayer) | 480×270 | 1920×1080 | top-left | — | no (factor 0.1) | structural | M0 | `#4A2E1A` surface |
| `bg_library_layer_2` | Sprite2D (en ParallaxLayer) | 480×270 | 1920×1080 | top-left | — | no (factor 0.3) | structural | M1 | `#6B4226` surface_light |
| `bg_library_layer_1` | Sprite2D (en ParallaxLayer) | 480×270 | 1920×1080 | top-left | — | no (factor 0.6) | structural | M1 | `#4A2E1A` surface |

> **M0:** layers 3 and 4 with real art. Layers 1 and 2 as flat ColorRect.  
> **M1:** all 4 layers with real art and active parallax.

### Interactive UI

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `book_available` | TextureButton | 16×24 | 64×96 | center | normal / hover / focused | shimmer loop (4fr @ 4fps) — M1 | interactive | M0 | `#D4A017` accent |
| `book_locked` | TextureRect | 16×24 | 64×96 | center | static | no | decorative | M0 | `#9E9E9E` neutral |
| `book_completed` | TextureRect | 16×24 | 64×96 | center | static | glow loop (4fr @ 3fps) — M1 | decorative | M1 | `#D4A017` accent |
| `book_lock_icon` | TextureRect | 8×8 | 32×32 | center-bottom over book | static | no | decorative | M0 | `#9E9E9E` neutral |
| `btn_settings` | TextureButton | 24×24 | 96×96 | top-right | normal / pressed / disabled | no | interactive | M1 | `#6B4226` surface_light |
| `owl_idle` | (ver §2) | — | — | bottom-right | — | — | decorative | M0 | — |

### Suggested node tree

```
Library (Node2D)
├── ParallaxBackground
│   ├── ParallaxLayer (motion_scale 0.0)  ← layer_4
│   │   └── Sprite2D [bg_library_layer_4]
│   ├── ParallaxLayer (motion_scale 0.1)  ← layer_3
│   │   └── Sprite2D [bg_library_layer_3]
│   ├── ParallaxLayer (motion_scale 0.3)  ← layer_2
│   │   └── Sprite2D [bg_library_layer_2]
│   └── ParallaxLayer (motion_scale 0.6)  ← layer_1
│       └── Sprite2D [bg_library_layer_1]
├── BookShelf (GridContainer)             ← libros del pack activo
│   └── [instancias de BookButton]
├── TopBar (HBoxContainer)
│   ├── LabelPlayerName (Label)
│   ├── StarCounter (HBoxContainer)
│   └── BtnSettings [btn_settings]
└── Owl (AnimatedSprite2D) [owl_idle]
```

---

## 4. PassageView Scene

**Archivo:** `res://scenes/PassageView/PassageView.tscn`  
**Function:** Displays the text passage and hosts the active puzzle.  
**Layout:** HSplitContainer — 60% passage panel left, 40% puzzle panel right.

### Background panels

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `parchment_tile` | TextureRect (tile mode) | 64×64 | fills 60% width | top-left | static | no | structural | M0 | `#F5E6C8` parchment |
| `wood_tile` | TextureRect (tile mode) | 64×64 | fills 40% width | top-right | static | no | structural | M0 | `#4A2E1A` surface |

### Passage Panel (left, 60%)

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `passage_text` | RichTextLabel | — | fills panel - padding | top-left | normal / word_highlighted | no (BBCode handles highlight) | structural | M0 | — (es texto, no imagen) |
| `book_illustration` | TextureRect | variable | max 30% panel height | top-center | static | no | decorative | M1 | `#6B4226` surface_light |
| `passage_title` | Label | — | top of panel | top-left | static | no | decorative | M0 | — (text) |

### Bottom Bar (shared between passage and puzzle)

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `btn_hint` | TextureButton | 24×24 | 96×96 | bottom-right | normal / pressed / disabled | no | interactive | M0 | `#7B4FBE` magic_glow |
| `btn_exit` | TextureButton | 24×24 | 96×96 | bottom-left | normal / pressed | no | interactive | M0 | `#E53935` incorrect |
| `hint_counter` | Label | — | over btn_hint | center | static | no | decorative | M0 | — (text) |
| `star_row` | HBoxContainer (3× star) | — | top of bottom bar | top-center | — | — | decorative | M0 | — (ver §2 stars) |

### Puzzle Panel (right, 40%)

The puzzle panel is an empty container. The active puzzle is dynamically instantiated inside it. See §5–§9 for the assets of each puzzle type.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `puzzle_container` | MarginContainer | — | fills 40% | top-right | — | — | structural | M0 | — (empty container) |
| `owl_thinking` | (ver §2) | — | 192×192 | top-right corner | — | — | decorative | M0 | — |

### Suggested node tree

```
PassageView (Control)
├── Background
│   ├── ParchmentPanel (TextureRect tile) [parchment_tile]
│   └── WoodPanel (TextureRect tile) [wood_tile]
├── HSplitContainer
│   ├── PassagePanel (MarginContainer)
│   │   ├── PassageTitle (Label)
│   │   ├── BookIllustration (TextureRect) [book_illustration]
│   │   └── PassageText (RichTextLabel) [passage_text]
│   └── PuzzleContainer (MarginContainer) [puzzle_container]
│       └── [puzzle dynamically instantiated here]
├── BottomBar (HBoxContainer)
│   ├── BtnExit (TextureButton) [btn_exit]
│   ├── StarRow (HBoxContainer)
│   │   ├── Star1 (TextureRect) [star_empty/star_filled]
│   │   ├── Star2 (TextureRect) [star_empty/star_filled]
│   │   └── Star3 (TextureRect) [star_empty/star_filled]
│   └── HintSection (HBoxContainer)
│       ├── BtnHint (TextureButton) [btn_hint]
│       └── HintCounter (Label)
└── Owl (AnimatedSprite2D) [owl_thinking]
```

---

## 5. WordGlow Puzzle

**Archivo:** `res://scenes/Puzzles/WordGlow/WordGlow.tscn`  
**Ages:** 4–6  
**Mechanic:** The child taps words in the passage that match the word bank.  
**Instanciado en:** PuzzleContainer de PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `tile_word_normal` | NinePatchRect | 16×8 | min 64×32, crece con texto | center | — | no | interactive | M0 | `#F5E6C8` parchment |
| `tile_word_selected` | NinePatchRect | 16×8 | igual que normal | center | — | pulse loop | interactive | M0 | `#D4A017` accent |
| `tile_word_found` | NinePatchRect | 16×8 | igual que normal | center | — | no | interactive | M0 | `#4CAF50` correct |
| `tile_word_disabled` | NinePatchRect | 16×8 | igual que normal | center | — | no | decorative | M1 | `#9E9E9E` neutral |
| `tile_word_hover` | NinePatchRect | 16×8 | igual que normal | center | — | no | interactive | M1 | `#E8D4A8` parchment_shadow |
| `word_found_fx` | AnimatedSprite2D | 16×16 | 64×64 | center of found word | — | one-shot (6fr @ 12fps) — sparkle | decorative | M1 | `#7B4FBE` magic_glow |

### NinePatch margins para todos los `tile_word_*`

```
patch_margin_left:   4    (en pixels del sprite de dibujo)
patch_margin_right:  4
patch_margin_top:    4
patch_margin_bottom: 4
```

### Node tree

```
WordGlow (VBoxContainer)  ← instanciado en PuzzleContainer
├── PassageContainer (RichTextLabel)   ← texto con BBCode clickeable
└── WordBank (HBoxContainer)
    └── [WordBankSlot × N instancias dinámicas]
        └── WordBankSlot.tscn
            └── NinePatchRect [tile_word_*]
                └── Label (texto de la palabra)
```

---

## 6. Scramble Puzzle

**Archivo:** `res://scenes/Puzzles/Scramble/Scramble.tscn`  
**Ages:** 5–7  
**Mechanic:** The child reorders letters in individual tiles to form the target word.  
**Instanciado en:** PuzzleContainer de PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `tile_letter_normal` | NinePatchRect | 16×16 | 64×64 | center | — | no | interactive | M0 | `#F5E6C8` parchment |
| `tile_letter_selected` | NinePatchRect | 16×16 | 64×64 | center | — | lift (2px up) | interactive | M0 | `#D4A017` accent |
| `tile_letter_placed` | NinePatchRect | 16×16 | 64×64 | center | — | no | interactive | M0 | `#E8D4A8` parchment_shadow |
| `tile_letter_correct` | NinePatchRect | 16×16 | 64×64 | center | — | pulse one-shot | decorative | M0 | `#4CAF50` correct |
| `tile_letter_incorrect` | NinePatchRect | 16×16 | 64×64 | center | — | shake one-shot (500ms) | decorative | M0 | `#E53935` incorrect |
| `slot_letter_empty` | NinePatchRect | 16×16 | 64×64 | center | — | no | interactive | M0 | `#2C1A0E` background |
| `slot_letter_filled` | NinePatchRect | 16×16 | 64×64 | center | — | no | interactive | M0 | `#6B4226` surface_light |
| `word_target_label` | Label | — | top of puzzle | top-center | static | no | structural | M0 | — (text) |

### NinePatch margins para `tile_letter_*` y `slot_letter_*`

```
patch_margin_*: 4 en todos los lados (igual que tile_word)
```

### Node tree

```
Scramble (VBoxContainer)
├── TargetWordLabel (Label) [word_target_label]
├── AnswerSlots (HBoxContainer)
│   └── [LetterSlot × N slots dinámicos]
│       └── NinePatchRect [slot_letter_empty / slot_letter_filled]
│           └── Label (letra colocada, si existe)
└── LetterBank (HBoxContainer)
    └── [LetterTile × N tiles dinámicos]
        └── NinePatchRect [tile_letter_normal/selected/placed/correct/incorrect]
            └── Label (letra)
```

---

## 7. WordHunt Puzzle

**Archivo:** `res://scenes/Puzzles/WordHunt/WordHunt.tscn`  
**Ages:** 6–9  
**Mechanic:** Letter grid. The child selects contiguous letters to find words.  
**Instanciado en:** PuzzleContainer de PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `grid_cell_normal` | NinePatchRect | 16×16 | 64×64 | center | — | no | interactive | M0 | `#4A2E1A` surface |
| `grid_cell_hover` | NinePatchRect | 16×16 | 64×64 | center | — | no | interactive | M0 | `#6B4226` surface_light |
| `grid_cell_selected` | NinePatchRect | 16×16 | 64×64 | center | — | no | interactive | M0 | `#D4A017` accent |
| `grid_cell_found` | NinePatchRect | 16×16 | 64×64 | center | — | glow loop | decorative | M0 | `#4CAF50` correct |
| `grid_cell_hint` | NinePatchRect | 16×16 | 64×64 | center | — | pulse loop | decorative | M0 | `#FF9800` hint |
| `found_word_label` | Label | — | side list | top-left | normal / found (strikethrough) | no | structural | M0 | — (texto) |
| `grid_selection_line` | Line2D | — | overlay sobre grid | absolute | — | animates con drag | decorative | M1 | `#D4A017` accent |

> **Note:** `grid_selection_line` is a `Line2D`, not a texture — it is drawn in code following the selected cells. It has no art asset.

### Node tree

```
WordHunt (HSplitContainer)
├── GridPanel (GridContainer)
│   └── [GridCell × rows×cols dinámicos]
│       └── NinePatchRect [grid_cell_*]
│           └── Label (letra)
├── SelectionOverlay (Node2D)
│   └── SelectionLine (Line2D) [grid_selection_line]
└── WordList (VBoxContainer)
    └── [FoundWordLabel × N targets]
        └── Label [found_word_label]
```

---

## 8. FillPassage Puzzle

**Archivo:** `res://scenes/Puzzles/FillPassage/FillPassage.tscn`  
**Ages:** 7–9  
**Mechanic:** The passage has blank words. The child drags words from the bank into the blanks.  
**Instanciado en:** PuzzleContainer de PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `blank_slot_empty` | NinePatchRect | 32×8 | 128×32 | inline en texto | — | pulse loop | interactive | M0 | `#2C1A0E` background |
| `blank_slot_filled` | NinePatchRect | 32×8 | 128×32 | inline en texto | — | no | interactive | M0 | `#E8D4A8` parchment_shadow |
| `blank_slot_correct` | NinePatchRect | 32×8 | 128×32 | inline en texto | — | pulse one-shot | decorative | M0 | `#4CAF50` correct |
| `blank_slot_incorrect` | NinePatchRect | 32×8 | 128×32 | inline en texto | — | shake one-shot (500ms) | decorative | M0 | `#E53935` incorrect |
| `tile_word_draggable` | NinePatchRect | 16×8 | min 64×32 | center (en bank) | normal / dragging / placed | lift shadow on drag | interactive | M0 | `#F5E6C8` parchment |
| `drag_shadow` | TextureRect | 16×8 | igual que tile | absolute (sigue cursor) | — | no | decorative | M1 | `#2C1A0E` background (semitransparente) |

> **Implementation note:** `FillPassage` does not use `RichTextLabel` for the passage — the text is split into `Label` + `blank_slot` elements interleaved in an `HFlowContainer`. The blanks are `NinePatchRect` with drop zones.

### Node tree

```
FillPassage (VBoxContainer)
├── PassageFlow (HFlowContainer)
│   └── [dynamic alternation of Labels and BlankSlots]
│       └── NinePatchRect [blank_slot_*]
│           └── Label (palabra colocada, si existe)
└── WordBank (HBoxContainer)
    └── [DraggableWord × N targets]
        └── NinePatchRect [tile_word_draggable]
            └── Label (palabra)
```

---

## 9. RhymeFinder Puzzle

**Archivo:** `res://scenes/Puzzles/RhymeFinder/RhymeFinder.tscn`  
**Ages:** 4–7  
**Mechanic:** A word is shown. The child chooses which option rhymes with it.  
**Instanciado en:** PuzzleContainer de PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `rhyme_prompt_bg` | NinePatchRect | 48×16 | 192×64 | top-center | static | no | structural | M0 | `#D4A017` accent |
| `rhyme_option_normal` | NinePatchRect | 32×16 | 128×64 | center | — | no | interactive | M0 | `#F5E6C8` parchment |
| `rhyme_option_hover` | NinePatchRect | 32×16 | 128×64 | center | — | no | interactive | M0 | `#E8D4A8` parchment_shadow |
| `rhyme_option_correct` | NinePatchRect | 32×16 | 128×64 | center | — | bounce one-shot | decorative | M0 | `#4CAF50` correct |
| `rhyme_option_incorrect` | NinePatchRect | 32×16 | 128×64 | center | — | shake one-shot (500ms) | decorative | M0 | `#E53935` incorrect |
| `sound_wave_fx` | AnimatedSprite2D | 16×16 | 64×64 | beside prompt word | — | one-shot (4fr @ 8fps) | decorative | M1 | `#7B4FBE` magic_glow |

> **RhymeFinder is the simplest puzzle visually.** The 4 option tiles are NinePatchRect with a Label on top. No drag, no grid. The complexity is in the logic of what rhymes with what — the art is minimal.

### Node tree

```
RhymeFinder (VBoxContainer)
├── PromptSection (HBoxContainer)
│   ├── PromptBg (NinePatchRect) [rhyme_prompt_bg]
│   │   └── PromptWord (Label)
│   └── SoundWaveFx (AnimatedSprite2D) [sound_wave_fx]  ← aparece al leer con TTS
└── OptionsGrid (GridContainer, 2×2)
    └── [RhymeOption × 4]
        └── NinePatchRect [rhyme_option_*]
            └── Label (option word)
```

---

## 10. Celebration Scene

**Archivo:** `res://scenes/Celebration/Celebration.tscn`  
**Function:** Victory screen on completing a book or a passage with all stars.  
**M0:** static placeholder frame. M1: full animation.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `celebration_bg_stub` | TextureRect | 480×270 | 1920×1080 | fill | static | no | structural | M0 | `#2C1A0E` background |
| `celebration_bg` | AnimatedSprite2D | 480×270 | 1920×1080 | fill | — | loop (8–12fr @ 8fps) | structural | M1 | — (reemplaza stub) |
| `owl_celebrate` | (ver §2) | — | 192×192 | center-bottom | — | — | decorative | M1 | — |
| `sticker_earned` | TextureRect | 32×32 | 128×128 | center-right | — | slide-in one-shot | interactive | M1 | `#D4A017` accent |
| `stars_row_big` | HBoxContainer (3× star 16px) | — | top-center | top-center | — | animate in sequentially | structural | M0 | — (ver §2 stars) |
| `btn_continue` | TextureButton | 32×12 | 128×48 | bottom-center | normal / pressed | no | interactive | M0 | `#E8721A` accent_warm |
| `confetti_fx` | AnimatedSprite2D | 480×270 | 1920×1080 | fill (overlay) | — | one-shot (12fr @ 12fps) | decorative | M1 | `#D4A017` accent |
| `label_book_title` | Label | — | top of scene | top-center | static | no | decorative | M0 | — (texto) |

> **M0 implementation:** `celebration_bg_stub` is a `TextureRect` with a `ColorRect` placeholder. `stars_row_big` uses the assets de `star_empty/star_filled` de §2. `btn_continue` es `TextureButton` con `ColorRect`. Todo funcional sin arte.

---

## 11. Journal Scene

**Archivo:** `res://scenes/Journal/Journal.tscn`  
**Function:** The child's journal — earned stickers, saved words, progress.  
**Milestone:** M1 (no bloquea M0).

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `journal_bg` | TextureRect | 480×270 | 1920×1080 | fill | static | no | structural | M1 | `#F5E6C8` parchment |
| `journal_cover` | TextureRect | 64×80 | 256×320 | center | static | no | decorative | M1 | `#4A2E1A` surface |
| `sticker_slot_empty` | TextureRect | 24×24 | 96×96 | center (en grid) | static | no | decorative | M1 | `#E8D4A8` parchment_shadow |
| `sticker_slot_filled` | TextureRect | 24×24 | 96×96 | center (en grid) | static | no | decorative | M1 | `#D4A017` accent |
| `saved_word_card` | NinePatchRect | 32×8 | 128×32 | left-align en list | static | no | interactive | M1 | `#F5E6C8` parchment |
| `btn_back` | TextureButton | 24×24 | 96×96 | top-left | normal / pressed | no | interactive | M1 | `#6B4226` surface_light |
| `owl_reading` | (ver §2) | — | 192×192 | bottom-right | — | — | decorative | M1 | — |

---

## 12. Settings Scene

**Archivo:** `res://scenes/Settings/Settings.tscn`  
**Function:** Session settings — language, TTS speed, font size, visual theme.  
**Audience:** Adult (parent / teacher). More sober, less decorative UI.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `settings_bg` | TextureRect | 480×270 | 1920×1080 | fill | static | no | structural | M1 | `#2C1A0E` background |
| `settings_panel` | NinePatchRect | 48×48 | fills center | center | static | no | structural | M1 | `#4A2E1A` surface |
| `btn_back` | TextureButton | 24×24 | 96×96 | top-left | normal / pressed | no | interactive | M0 | `#6B4226` surface_light |
| `toggle_normal` | TextureRect | 24×12 | 96×48 | center | off | no | interactive | M1 | `#9E9E9E` neutral |
| `toggle_on` | TextureRect | 24×12 | 96×48 | center | on | no | interactive | M1 | `#4CAF50` correct |
| `slider_track` | TextureRect | 64×4 | 256×16 | center | static | no | interactive | M1 | `#9E9E9E` neutral |
| `slider_thumb` | TextureRect | 8×8 | 32×32 | center (sobre track) | normal / dragging | no | interactive | M1 | `#D4A017` accent |
| `theme_preview_frame` | NinePatchRect | 32×20 | 128×80 | center (en grid) | normal / selected | no | interactive | M2 | `#6B4226` surface_light |

> **M0:** Settings only needs a functional `btn_back` and native Godot controls (`HSlider`, `CheckButton`, `OptionButton`) sin arte custom. Los assets custom son M1/M2.

---

## 13. Onboarding Flow

**Function:** Child's first time — choose Owl name, basic tutorial.  
**Milestone:** M0 (minimal functional), M1 (with full art).

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `onboarding_bg` | TextureRect | 480×270 | 1920×1080 | fill | static | no | structural | M0 | `#2C1A0E` background |
| `name_input_bg` | NinePatchRect | 48×16 | 192×64 | center | normal / focused | no | interactive | M0 | `#F5E6C8` parchment |
| `btn_confirm` | TextureButton | 32×12 | 128×48 | bottom-center | normal / pressed / disabled | no | interactive | M0 | `#E8721A` accent_warm |
| `tutorial_bubble` | NinePatchRect | 64×32 | 256×128 | above owl | static | no | decorative | M1 | `#F5E6C8` parchment |
| `tutorial_arrow` | TextureRect | 8×16 | 32×64 | below bubble | static | no | decorative | M1 | `#F5E6C8` parchment |
| `owl_wave` | (ver §2) | — | 192×192 | center | — | — | decorative | M0 | — |

---

## Appendix A — M0 Priorities Summary

Assets that must exist (real art or correct placeholder) before the first playable passage:

```
GLOBAL:
  owl_idle, owl_thinking, owl_hint    (AnimatedSprite2D, 48×48, 4fr cada uno)
  star_empty, star_filled              (TextureRect, 8×8)
  icon_hint                            (TextureRect, 16×16)

LIBRARY:
  bg_library_layer_4, bg_library_layer_3  (Sprite2D, 480×270)
  book_available, book_locked              (TextureButton/TextureRect, 16×24)
  book_lock_icon                           (TextureRect, 8×8)

PASSAGEVIEW:
  parchment_tile, wood_tile    (TextureRect tile, 64×64)
  btn_hint, btn_exit            (TextureButton, 24×24)

WORDGLOW (primer puzzle):
  tile_word_normal, tile_word_selected, tile_word_found  (NinePatchRect, 16×8)

CELEBRATION:
  celebration_bg_stub  (TextureRect, 480×270 — ColorRect válido)
  btn_continue          (TextureButton, 32×12)

SETTINGS:
  btn_back  (TextureButton, 24×24)

ONBOARDING:
  onboarding_bg  (TextureRect — ColorRect valid)
  name_input_bg  (NinePatchRect, 48×16)
  btn_confirm     (TextureButton, 32×12)
  owl_wave        (via AnimatedSprite2D de §2)
```

Total M0: **~20 real art assets** + rest as color placeholders. All nodes must be the final type — do not use `ColorRect` directly in the final tree, only as a temporary child of the correct node.

---

## Appendix B — Implementation Checklist per Asset

Before considering an asset "correctly implemented" in code, verify:

```
□ The node is the correct type (no ColorRect in production)
□ draw_size matches the PNG import (not rescaled in Godot)
□ display_size es draw_size × 4 (scale del nodo = Vector2(4, 4))
□ Import settings: Filter=Nearest, Mipmaps=OFF, Compress=Lossless
□ anchor/alignment configured correctly in the editor
□ All states have their PNG (or frame in SpriteFrames)
□ tap target ≥ 96×96 para cualquier elemento interactive
□ The node with layout_role=structural does not have position hardcoded in code
```

---

*Documento: READCRAFTERY Asset Contracts v1.0*  
*Update when new scenes are added or when the Art Guide changes dimensions.*  
*This document is the source of truth for dimensions and node types — the Art Guide is the source of truth for style and palea.*
