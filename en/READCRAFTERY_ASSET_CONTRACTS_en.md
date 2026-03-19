# READCRAFTERY — Asset Contracts
**Version:** 1.3
**Date:** March 2026
**Status:** Pre-Production
**Companion documents:** Art Guide v1.5 · Build Guide v1.5 · Architecture Contract v1.3

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
> **Global scale:** all game assets are drawn at native pixels and shown
> at 4x in a 1920x1080 viewport. `display_size` = `draw_size x 4`.
> Passage text and UI labels live at native 1080p resolution -- they do not scale.
>
> **Exception -- Owlorumo:** master draw size is 64x64. Display size varies by context:
> 192x192 in PassageView (3x), 256x256 in Library/menu (4x). See Art Guide s5.

---


> **Library identity note:** The visual world is first encountered as **The Sleeping Library**, later understood as **The Reawakened Library**, and finally as **The Library of Beginnings**. Theme variations reinterpret the same living library-world; they do not replace it with a different genre.

## Table of Contents

1. Conventions
2. Shared Assets -- Global UI
3. Library Scene
4. PassageView Scene
5. WordGlow Puzzle
6. Scramble Puzzle
7. WordHunt Puzzle
8. FillPassage Puzzle
9. RhymeFinder Puzzle
10. Celebration Scene
11. Journal Scene
12. Settings Scene
13. Onboarding Flow

---

## 1. Conventions

### Table columns

| Column | Description |
|---|---|
| asset_id | Filename without extension. It is the canonical identifier. |
| node_type | Godot node that renders this asset. Use this node in the placeholder -- it does not change when the art arrives. |
| draw_size | Drawing pixel dimensions (what the artist draws). |
| display_size | On-screen dimensions at 4x. For NinePatch: minimum container size. |
| anchor | Node anchor point. In Godot: PRESET_* from the Control enum or centered for Sprite2D. |
| states | List of required visual states. Each state = a separate PNG file (or frame in AnimatedSprite2D). |
| animates | Whether the asset has a loop or one-shot animation. Format: type (Nframes @ Xfps). |
| layout_role | structural = defines layout (moving it breaks the screen) / interactive = the child touches this / decorative = visual only |
| priority | Milestone by which real art must exist. M1 = blocker for campaign demo. |
| placeholder_color | Palette token for the placeholder ColorRect/modulate. |

### Node types used in this document

```
Sprite2D          -- static image, does not participate in Control layout
AnimatedSprite2D  -- sprite with multiple animations (Owlorumo)
TextureRect       -- image in Control layout system (stretches/adapts)
NinePatchRect     -- image that stretches without distorting corners (tiles, buttons)
TextureButton     -- textured button, handles hover/pressed/disabled automatically
AnimationPlayer   -- does not render -- controls animations of other nodes
ParallaxBackground/ParallaxLayer -- Godot parallax nodes
ColorRect         -- FOR PLACEHOLDERS ONLY. Replace when art arrives.
```

### Placeholder pattern in GDScript

```gdscript
# Correct placeholder -- the node is already the final type
@onready var btn_exit: TextureButton = $BottomBar/BtnExit

func _ready() -> void:
    # Placeholder: solid color until the art arrives
    # When the art arrives: remove these 2 lines and assign texture_normal
    var placeholder := ColorRect.new()
    placeholder.color = Color("#D4A017")  # accent -- palette token color
    placeholder.size = Vector2(96, 96)    # display_size
    btn_exit.add_child(placeholder)
```

### Typography -- closed decision

CLOSED

| Context | Type | Owner |
|---|---|---|
| Passage text (the child reads) | Pedagogical font .ttf/.otf | Not an art asset |
| Interactive puzzle tiles (Scramble, WordHunt, word bank) | Pixel art letters -- sprite | Artist |

**Passage text:** uses a font from the pedagogical typography system
(Andika for passage text; OpenDyslexic optional fallback; Nunito for UI labels as defined in the Art Guide).
Text lives at native 1080p resolution, does not scale with sprites.
No art asset required for this context.

**Puzzle tile letters:** rendered dynamically by Godot using the UI font (Nunito)
drawn on top of a `NinePatchRect` background tile. The artist delivers the tile
backgrounds only — not individual letter sprites.

This decision ensures immediate support for any language, accent, or modded content
without additional art production. A tile for Spanish `ñ`, French `ç`, or German `ß`
requires no extra asset.

> **Style note:** This means puzzle tiles are the one element where pixel art
> and dynamic font rendering coexist. The tile background is pixel art;
> the letter on top is Nunito. This is a conscious tradeoff: localization
> correctness over full pixel art purity.

---

## 2. Shared Assets -- Global UI

Assets that appear in multiple scenes. Defined once, referenced in each scene.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| owl_idle | AnimatedSprite2D | 64x64 | see Art Guide s5 | bottom-center | -- | loop (4fr @ 4fps) | decorative | M2 | #4A2E1A surface |
| owl_thinking | AnimatedSprite2D | 64x64 | see Art Guide s5 | bottom-center | -- | loop (4fr @ 4fps) | decorative | M2 | #4A2E1A surface |
| owl_hint | AnimatedSprite2D | 64x64 | see Art Guide s5 | bottom-center | -- | one-shot (4fr @ 8fps) | decorative | M2 | #4A2E1A surface |
| owl_happy | AnimatedSprite2D | 64x64 | see Art Guide s5 | bottom-center | -- | loop (6fr @ 6fps) | decorative | M2 | #4A2E1A surface |
| owl_excited | AnimatedSprite2D | 64x64 | see Art Guide s5 | bottom-center | -- | one-shot (8fr @ 8fps) | decorative | M2 | #4A2E1A surface |
| owl_reading | AnimatedSprite2D | 64x64 | see Art Guide s5 | bottom-center | -- | loop (4fr @ 4fps) | decorative | M3 | #4A2E1A surface |
| owl_celebrate | AnimatedSprite2D | 64x64 | see Art Guide s5 | bottom-center | -- | one-shot (8fr @ 8fps) | decorative | M2 | #4A2E1A surface |
| owl_sleepy | AnimatedSprite2D | 64x64 | see Art Guide s5 | bottom-center | -- | loop (4fr @ 3fps) | decorative | M3 | #4A2E1A surface |
| owl_wave | AnimatedSprite2D | 64x64 | see Art Guide s5 | bottom-center | -- | one-shot (6fr @ 6fps) | decorative | M2 | #4A2E1A surface |
| fragment_light_small | AnimatedSprite2D | 8x8 | 32x32 | center | -- | one-shot (4fr @ 12fps) | decorative | M2 | #D4A017 accent |
| fragment_light_large | AnimatedSprite2D | 16x16 | 64x64 | center | -- | one-shot (4fr @ 12fps) | decorative | M2 | #D4A017 accent |
| icon_hint | TextureRect | 16x16 | 64x64 | center | -- | no | decorative | M1 | #7B4FBE magic_glow |
| icon_settings | TextureRect | 16x16 | 64x64 | center | -- | no | decorative | M2 | #F5E6C8 parchment |
| icon_home | TextureRect | 16x16 | 64x64 | center | -- | no | decorative | M2 | #F5E6C8 parchment |
| icon_back | TextureRect | 16x16 | 64x64 | center | -- | no | interactive | M2 | #F5E6C8 parchment |
| fragment_light | AnimatedSprite2D | 8x8 | 32x32 | center | -- | one-shot (4fr @ 12fps) — flies to crystal | decorative | M2 | #D4A017 accent |

### Implementation notes -- Owlorumo

Owlorumo uses **a single AnimatedSprite2D node** with multiple named animations. They are not separate nodes.

```gdscript
# In any scene that displays Owlorumo:
@onready var owl: AnimatedSprite2D = $Owl

func set_owl_state(state: String) -> void:
    owl.play(state)  # state = "idle", "thinking", "hint", etc.
```

Display size is set per-scene via scale: Vector2(3, 3) for PassageView (192x192),
Vector2(4, 4) for Library/menu (256x256). Animations are defined in the SpriteFrames
resource assigned to the node -- not in code.

### Owlorumo -- Progression States

Owlorumo has 5 visual states that unlock as the child completes books.
Each state is a separate SpriteFrames resource -- same frame layout,
different texture. The AnimatedSprite2D swaps the resource on state change.

| State | Atlas file | Staff / Crystal | Clothing / Presence | Unlocked after |
|---|---|---|---|---|
| 0 | atlas_owlorumo_state0.png | Staff slightly dry, light cracking; crystal dark | Navy form, diminished presence | Game start |
| 1 | atlas_owlorumo_state1.png | Cracks gone or reduced; faint glow | Same design, slightly steadier material read | First passage |
| 2 | atlas_owlorumo_state2.png | Crystal lit and softly pulsing | Same silhouette; more life in material and light | First book |
| 3 | atlas_owlorumo_state3.png | Crystal bright and warm; staff stronger and more alive | Presence fuller; library increasingly responsive | 3 books |
| 4 | atlas_owlorumo_state4.png | Powerful white-gold crystal; staff fully alive but still organic | White-and-gold restoration with visible continuity; blue mantle remains visible | First complete arc |

`state_4` is a deliberate homage to Tolkien's Gandalf the White, but it should feel fulfilled, not replaced.

**Identity anchors that remain visible through all states:**
- moon brooch
- belt
- boots
- organic staff form

All 5 atlases share identical frame layout. The artist delivers 5 PNG files.
Priority: state_0 and state_1 = M2 blocker. state_2 and state_3 = M2. state_4 = M3.

> **Production cost note:** state_4 requires a full atlas redraw equivalent in effort
> to any other complete state. "Illuminating the existing robe" is a narrative concept,
> not a production shortcut — changing from external ambient lighting to internal
> white-gold luminosity requires reworking the shading on every frame.
> Budget state_4 as a complete atlas, not as a recolor pass.

```gdscript
# Swap SpriteFrames resource on state change
func _apply_owlorumo_state(state: int) -> void:
    var frames: SpriteFrames = load(
        "res://content/atlas_owlorumo_state%d.tres" % state
    )
    if frames == null:
        push_error("Owlorumo SpriteFrames not found for state: %d" % state)
        return
    owl_sprite.sprite_frames = frames
```

---

## 3. Library Scene

**File:** res://scenes/Library/Library.tscn
**Function:** Main menu. The child selects a book to read.
**Layout:** Full screen. 4-layer parallax. Owlorumo in fixed right position.

### Background -- parallax layers

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| bg_library_layer_4 | Sprite2D (in ParallaxLayer) | 480x270 | 1920x1080 | top-left | -- | no (static) | structural | M1 | #2C1A0E background |
| bg_library_layer_3 | Sprite2D (in ParallaxLayer) | 480x270 | 1920x1080 | top-left | -- | no (factor 0.1) | structural | M1 | #4A2E1A surface |
| bg_library_layer_2 | Sprite2D (in ParallaxLayer) | 480x270 | 1920x1080 | top-left | -- | no (factor 0.3) | structural | M2 | #6B4226 surface_light |
| bg_library_layer_1 | Sprite2D (in ParallaxLayer) | 480x270 | 1920x1080 | top-left | -- | no (factor 0.6) | structural | M2 | #4A2E1A surface |

M1: layers 3 and 4 with real art. Layers 1 and 2 as flat ColorRect.
M2: all 4 layers with real art and active parallax.

### Interactive UI

| asset_id | node_type | draw_size | states | animates | priority |
|---|---|---|---|---|---|
| book_spine_{pack_id} | TextureRect | 16×48 | dormant / awakened / in_progress / completed | shimmer on awakened (shader) | M1 |
| book_seal_completed | Sprite2D | 4×4 | static | no | M1 final |

> **Book spine color:** Generated from pack `id` hash when no `cover_image` is provided
> (already specified). The 4 states are achieved via modulate + shader:
> - Dormant: modulate grey (`#9E9E9E` at 60%)
> - Awakened: full color + shimmer shader (golden, 0.8Hz)
> - In-progress: full color + constant glow (no pulse)
> - Completed: full color + constant warm glow + `book_seal_completed` overlay
>
> **Micro-push animation:** Not an art asset — implemented as Tween on `position.x`
> (2px shift, 0.2 sec, spring ease-back).
>
> **Golden seal:** 4×4 native pixel art. Gold (#D4A017) on dark spine. Symbol is
> art direction — rune fragment, crystal mark, or library stamp. Must read at 4× scale.

### Suggested node tree

```
Library (Node2D)
├── ParallaxBackground
│   ├── ParallaxLayer (motion_scale 0.0)  <- layer_4
│   │   └── Sprite2D [bg_library_layer_4]
│   ├── ParallaxLayer (motion_scale 0.1)  <- layer_3
│   │   └── Sprite2D [bg_library_layer_3]
│   ├── ParallaxLayer (motion_scale 0.3)  <- layer_2
│   │   └── Sprite2D [bg_library_layer_2]
│   └── ParallaxLayer (motion_scale 0.6)  <- layer_1
│       └── Sprite2D [bg_library_layer_1]
├── BookShelf (GridContainer)             <- books from active pack
│   └── [BookButton instances]
├── TopBar (HBoxContainer)
│   ├── LabelPlayerName (Label)
│   └── BtnSettings [btn_settings]
└── Owl (AnimatedSprite2D) [owl_idle]
```

---


### Library Resonance Assets

Resonance points are visual elements with dormant/awakened sprite variants.
Each resonance requires two sprites at minimum, identical in size and anchor.

| asset_id pattern | node_type | draw_size | states | animates | priority |
|---|---|---|---|---|---|
| resonance_{id}_dormant | Sprite2D | varies per point | static | no | M1 final |
| resonance_{id}_awakened | Sprite2D | same as dormant | static | no (light overlay allowed) | M1 final |

> **Exact resonance assets are not committed yet.** The architecture supports
> any number of points. Asset IDs will follow the pattern `resonance_{id}_{state}`.
> Each point is defined when the art direction for the Library scene is finalized.

### Hidden Book Shelf Slots

| asset_id | node_type | draw_size | states | animates | priority |
|---|---|---|---|---|---|
| shelf_slot_empty | Sprite2D | 16×12 | static | no | M1 |
| shelf_slot_occupied | Sprite2D | 16×12 | static | soft glow (shader) | M1 |
| shelf_slot_residue | Sprite2D | 16×12 | static | no | M2 |

> `shelf_slot_residue` must be distinguishable from `shelf_slot_empty` only on
> close inspection. The difference is 1–2 pixels of dust pattern or wood tone.
> This is the most subtle asset in the entire game. If a playtester notices it
> immediately without looking for it, it is too obvious.

---

## 4. PassageView Scene

**File:** res://scenes/PassageView/PassageView.tscn
**Function:** Displays the text passage and hosts the active puzzle.
**Layout:** passage-centered reading scene. The passage remains primary. Puzzle support UI sits beside or below it without taking over the reading task.

### Background panels

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| bg_passage_library | TextureRect | 480x270 | fills viewport | full-rect | static | no | structural | M1 final | #2C1A0E background (solid in M0) |
| parchment_tile | TextureRect (tile mode) | 64x64 | centered, ~68% width | center | static | no | structural | M1 | #F5E6C8 parchment |

### Passage Panel (left, 60%)

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| interactive_passage_text | Control (token renderer) | -- | fills panel - padding | top-left | normal / hovered / found / hinted | no | structural | M0 | -- (text, not image) |
| book_illustration | TextureRect | variable | max 30% panel height | top-center | static | no | decorative | M2 | #6B4226 surface_light |
| passage_title | Label | -- | top of panel | top-left | static | no | decorative | M0 | -- (text) |
| page_corner_turn | TextureRect | 16×16 | idle (invisible) / inviting (corner lifted) | fade-in 0.5 sec | M1 | #F5E6C8 parchment shadow |

> **Page corner behavior:** Pixel art parchment corner with subtle shadow.
> Appears bottom-right of ParchmentPanel, 1 sec after Completion Beat completes.
> Fade-in 0.5 sec. Tap target 96×96. On tap: page turn animation (0.5–0.8 sec).
> Not shown on last passage of book.
> M0 placeholder: triangular ColorRect (#D8C6A3).

### Bottom Bar (shared between passage and puzzle)

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| book_tts | TextureButton | 16x16 | 64x64 | passage panel, fixed | normal / playing | pulse while playing | interactive | M2 | #F5E6C8 parchment |
| btn_exit | TextureButton | 24x24 | 96x96 | bottom-left | normal / holding | fill animation 1s | interactive | M1 | #4A2E1A surface |
| support_status | Label | -- | bottom bar / support row | center | static | no | decorative | M0 | -- (text) |
| completion_feedback_host | Control | -- | scene overlay / local anchor | center | -- | -- | decorative | M1 | -- |

> **`btn_exit` behavior:** tap-hold 1 second to activate. Owlorumo looks toward
> the door during the hold. Release before 1 second = no action.
> On activation: saves partial progress before transitioning.
>
> **Crystal as hint access:** there is no Owlorumo sprite in PassageView and no
> separate `btn_hint` asset. The child taps the crystal icon (pixel art, bottom-right).
> The crystal IS Owlorumo's presence in this scene. See §4 Crystal Icon.

### Crystal Icon (Owlorumo's presence)

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| crystal_icon | TextureRect | 12×12 | 48×48 (4×) | bottom-right, 16px margin | idle / hint_available / hint_exhausted | pulse 0.8Hz (engine glow, not sprite) | interactive | M0 | #7B4FBE magic_glow |
| crystal_tap_area | Button (invisible) | — | 64×64 | covers crystal_icon | — | — | interactive | M0 | — (transparent) |

> **Pixel art rules apply.** The crystal is rendered with `image-rendering: pixelated`
> (Nearest filter in Godot). It follows Art Guide §5 shape/shadow rules: 1px outline
> using `magic_glow` shadow variant, flat color blocks, upper-left light direction.
> The glow aura is an engine effect (shader or modulate), not part of the sprite.
>
> **Replaces:** `btn_hint`, `icon_hint`, `owl_thinking` in PassageView, and the entire
> puzzle_container visual panel. PuzzleContainer still exists as an invisible node
> for IPuzzle instantiation and signal routing.

### WordToken (InteractivePassageText child)

WordToken is not a traditional art asset — it is a UI component with programmatic visuals.

| element | implementation | colors | notes |
|---|---|---|---|
| Label | Andika font, text_primary color | #2C1A0E on parchment | Size determined by display profile |
| OverlayRect (normal) | Invisible | — | Default state |
| OverlayRect (target_pending) | Visible, low alpha | #D4A017 at 15% | Subtle gold presence |
| OverlayRect (shimmer) | Tween alpha 40% → 15% over 0.5 sec | #D4A017 | One-shot after TTS |
| OverlayRect (tap_highlight) | Tween alpha 30% → 0% over 0.5 sec | #F5E6C8 | Tap-to-Hear feedback |
| OverlayRect (found) | Visible, constant | #D4A017 at 20% | Permanent gold glow |
| OverlayRect (hinted) | Tween alpha 30% → 0% over 1.0 sec | #7B4FBE | Crystal color pulse |

> No pixel art assets required. All visuals are ColorRect + Tween.
> Minimum tap target: 96×96 per Art Guide. Set via `custom_minimum_size`.

### Suggested node tree

```
PassageView (Control)
├── Background
│   ├── ParchmentPanel (TextureRect tile) [parchment_tile]
│   └── SupportPanel (TextureRect tile) [wood_tile]
├── MainLayout (Container)
│   ├── PassagePanel (MarginContainer)
│   │   ├── PassageTitle (Label)
│   │   ├── BookIllustration (TextureRect) [book_illustration]
│   │   └── InteractivePassageText (Control) [interactive_passage_text]
│   └── PuzzleContainer (MarginContainer) [puzzle_container]
│       └── [puzzle support UI dynamically instantiated here]
├── BottomBar (HBoxContainer)
│   ├── BtnExit (TextureButton) [btn_exit]
│   ├── BookTTS (TextureButton) [book_tts]
│   └── SupportStatus (Label) [support_status]
└── Owl (AnimatedSprite2D) [owl_thinking -- state from save profile]
```

---

## 5. WordGlow Puzzle

**File:** res://scenes/Puzzles/WordGlow/WordGlow.tscn
**Ages:** 4-6
**Mechanic:** The child reads the passage and taps the current target word directly in the passage text. The support UI tracks target order and found state.
**Instantiated in:** PuzzleContainer of PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| current_target_card | NinePatchRect | 32x16 | 128x64 | top-center | normal | no | structural | M1 | #F5E6C8 parchment |
| tile_word_normal | NinePatchRect | 16x8 | min 64x32, grows with text | center | -- | no | decorative | M1 | #F5E6C8 parchment |
| tile_word_selected | NinePatchRect | 16x8 | same as normal | center | -- | pulse loop | decorative | M1 | #D4A017 accent |
| tile_word_found | NinePatchRect | 16x8 | same as normal | center | -- | no | decorative | M1 | #4CAF50 correct |
| tile_word_disabled | NinePatchRect | 16x8 | same as normal | center | -- | no | decorative | M2 | #9E9E9E neutral |
| tile_word_hover | NinePatchRect | 16x8 | same as normal | center | -- | no | decorative | M2 | #E8D4A8 parchment_shadow |
| word_found_fx | AnimatedSprite2D | 16x16 | 64x64 | center of found word | -- | one-shot (6fr @ 12fps) -- soft magical trail | decorative | M2 | #7B4FBE magic_glow |

### NinePatch margins for all tile_word_*

```
patch_margin_left:   4    (in drawing sprite pixels)
patch_margin_right:  4
patch_margin_top:    4
patch_margin_bottom: 4
```

### Word Bank Slots -- anonymous targets

### Word Bank Slots — REMOVED

Word bank slots are no longer part of the standard PassageView layout.
Target progress is visible directly in the passage text (found words retain gold glow).

> **Future M2+ consideration:** The conservative display profile may optionally
> restore anonymous slot indicators for children who need explicit progress cues.
> If reintroduced, the slot spec from the previous version of this document applies.

### Owlorumo proximity glow

Owlorumo's staff crystal glows with intensity proportional to cursor/finger
proximity to target words. This is not an art asset -- it is a shader parameter
on the crystal element of the active Owlorumo state atlas.

```gdscript
# In WordGlowController
func set_glow_radius(radius: float) -> void:
    # radius 0.0 = disabled (advanced profile)
    # radius 0.5 = reduced (standard profile)
    # radius 1.0 = full (conservative profile)
    _glow_radius = radius

func _process(delta: float) -> void:
    if _glow_radius <= 0.0:
        return
    var cursor_pos: Vector2 = get_global_mouse_position()
    var intensity: float = _calculate_glow_intensity(cursor_pos)
    owl_sprite.material.set_shader_parameter("crystal_intensity", intensity)

func _calculate_glow_intensity(cursor: Vector2) -> float:
    var closest_dist: float = INF
    for tile in _target_tiles:
        var dist: float = cursor.distance_to(tile.global_position)
        closest_dist = min(closest_dist, dist)
    # Max activation radius -- does not reveal exact word location
    var max_radius: float = 300.0 * _glow_radius
    return clampf(1.0 - (closest_dist / max_radius), 0.0, 1.0)
```

### Node tree

```
WordGlow (VBoxContainer)  <- instantiated in PuzzleContainer
├── CurrentTargetCard (NinePatchRect)  <- one target word at a time
│   └── Label / optional picture support
├── AnonymousSlots (HBoxContainer)     <- target slots, shown in conservative/standard
│   └── [WordBankSlot x N -- anonymous, no label]
│       └── WordBankSlot.tscn
│           ├── NinePatchRect [slot_word_empty / slot_word_filled]
│           └── Label (hidden until word found)
└── WordBank (HBoxContainer)           <- supportive inventory only
    └── [WordTile x N -- target inventory]
        └── WordTile.tscn
            └── NinePatchRect [tile_word_normal/selected/found/disabled]
                └── Label (word text)
```

---

## 6. Scramble Puzzle

**File:** res://scenes/Puzzles/Scramble/Scramble.tscn
**Ages:** 5-7
**Mechanic:** The child reorders letters in individual tiles to form the target word.
**Instantiated in:** PuzzleContainer of PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| tile_letter_normal | NinePatchRect | 16x16 | 64x64 | center | -- | no | interactive | M1 | #F5E6C8 parchment |
| tile_letter_selected | NinePatchRect | 16x16 | 64x64 | center | -- | lift (2px up) | interactive | M1 | #D4A017 accent |
| tile_letter_placed | NinePatchRect | 16x16 | 64x64 | center | -- | no | interactive | M1 | #E8D4A8 parchment_shadow |
| tile_letter_correct | NinePatchRect | 16x16 | 64x64 | center | -- | pulse one-shot | decorative | M1 | #4CAF50 correct |
| tile_letter_incorrect | NinePatchRect | 16x16 | 64x64 | center | -- | shake one-shot (500ms) | decorative | M1 | #E53935 incorrect |
| slot_letter_empty | NinePatchRect | 16x16 | 64x64 | center | -- | no | interactive | M1 | #2C1A0E background |
| slot_letter_filled | NinePatchRect | 16x16 | 64x64 | center | -- | no | interactive | M1 | #6B4226 surface_light |
| word_target_label | Label | -- | top of puzzle | top-center | static | no | structural | M1 | -- (text) |

### NinePatch margins for tile_letter_* and slot_letter_*

```
patch_margin_*: 4 on all sides (same as tile_word)
```

### Node tree

```
Scramble (VBoxContainer)
├── TargetWordLabel (Label) [word_target_label]
├── AnswerSlots (HBoxContainer)
│   └── [LetterSlot x N dynamic slots]
│       └── NinePatchRect [slot_letter_empty / slot_letter_filled]
│           └── Label (placed letter, if any)
└── LetterBank (HBoxContainer)
    └── [LetterTile x N dynamic tiles]
        └── NinePatchRect [tile_letter_normal/selected/placed/correct/incorrect]
            └── Label (letter)
```

---

## 7. WordHunt Puzzle

**File:** res://scenes/Puzzles/WordHunt/WordHunt.tscn
**Ages:** 6-9
**Mechanic:** Letter grid. The child selects contiguous letters to find words.
**Instantiated in:** PuzzleContainer of PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| grid_cell_normal | NinePatchRect | 16x16 | 64x64 | center | -- | no | interactive | M2 | #4A2E1A surface |
| grid_cell_hover | NinePatchRect | 16x16 | 64x64 | center | -- | no | interactive | M2 | #6B4226 surface_light |
| grid_cell_selected | NinePatchRect | 16x16 | 64x64 | center | -- | no | interactive | M2 | #D4A017 accent |
| grid_cell_found | NinePatchRect | 16x16 | 64x64 | center | -- | glow loop | decorative | M2 | #4CAF50 correct |
| grid_cell_hint | NinePatchRect | 16x16 | 64x64 | center | -- | pulse loop | decorative | M2 | #FF9800 hint |
| found_word_label | Label | -- | side list | top-left | normal / found (strikethrough) | no | structural | M2 | -- (text) |
| grid_selection_line | Line2D | -- | over grid | absolute | -- | animates with drag | decorative | M2 | #D4A017 accent |

Note: grid_selection_line is a Line2D, not a texture -- it is drawn in code
following the selected cells. It has no art asset.

### Node tree

```
WordHunt (HSplitContainer)
├── GridPanel (GridContainer)
│   └── [GridCell x rows x cols dynamic]
│       └── NinePatchRect [grid_cell_*]
│           └── Label (letter)
├── SelectionOverlay (Node2D)
│   └── SelectionLine (Line2D) [grid_selection_line]
└── WordList (VBoxContainer)
    └── [FoundWordLabel x N targets]
        └── Label [found_word_label]
```

---

## 8. FillPassage Puzzle

**File:** res://scenes/Puzzles/FillPassage/FillPassage.tscn
**Ages:** 7-9
**Mechanic:** The passage has blank words. The child drags words from the bank into the blanks.
**Instantiated in:** PuzzleContainer of PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| blank_slot_empty | NinePatchRect | 32x8 | 128x32 | inline in text | -- | pulse loop | interactive | M2 | #2C1A0E background |
| blank_slot_filled | NinePatchRect | 32x8 | 128x32 | inline in text | -- | no | interactive | M2 | #E8D4A8 parchment_shadow |
| blank_slot_correct | NinePatchRect | 32x8 | 128x32 | inline in text | -- | pulse one-shot | decorative | M2 | #4CAF50 correct |
| blank_slot_incorrect | NinePatchRect | 32x8 | 128x32 | inline in text | -- | shake one-shot (500ms) | decorative | M2 | #E53935 incorrect |
| tile_word_draggable | NinePatchRect | 16x8 | min 64x32 | center (in bank) | normal / dragging / placed | lift shadow on drag | interactive | M2 | #F5E6C8 parchment |
| drag_shadow | TextureRect | 16x8 | same as tile | absolute (follows cursor) | -- | no | decorative | M2 | #2C1A0E background (semi-transparent) |

Implementation note: FillPassage does not use RichTextLabel for the passage --
the text is split into Label + blank_slot elements interleaved in an HFlowContainer.
The blanks are NinePatchRect with drop zones.

### Node tree

```
FillPassage (VBoxContainer)
├── PassageFlow (HFlowContainer)
│   └── [dynamic alternation of Labels and BlankSlots]
│       └── NinePatchRect [blank_slot_*]
│           └── Label (placed word, if any)
└── WordBank (HBoxContainer)
    └── [DraggableWord x N targets]
        └── NinePatchRect [tile_word_draggable]
            └── Label (word)
```

---

## 9. RhymeFinder Puzzle

**File:** res://scenes/Puzzles/RhymeFinder/RhymeFinder.tscn
**Ages:** 4-7
**Mechanic:** A word is shown. The child chooses which option rhymes with it.
**Instantiated in:** PuzzleContainer of PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| rhyme_prompt_bg | NinePatchRect | 48x16 | 192x64 | top-center | static | no | structural | M2 | #D4A017 accent |
| rhyme_option_normal | NinePatchRect | 32x16 | 128x64 | center | -- | no | interactive | M2 | #F5E6C8 parchment |
| rhyme_option_hover | NinePatchRect | 32x16 | 128x64 | center | -- | no | interactive | M2 | #E8D4A8 parchment_shadow |
| rhyme_option_correct | NinePatchRect | 32x16 | 128x64 | center | -- | bounce one-shot | decorative | M2 | #4CAF50 correct |
| rhyme_option_incorrect | NinePatchRect | 32x16 | 128x64 | center | -- | shake one-shot (500ms) | decorative | M2 | #E53935 incorrect |
| sound_wave_fx | AnimatedSprite2D | 16x16 | 64x64 | beside prompt word | -- | one-shot (4fr @ 8fps) | decorative | M2 | #7B4FBE magic_glow |

RhymeFinder is the simplest puzzle visually. The 4 option tiles are NinePatchRect
with a Label on top. No drag, no grid. The complexity is in the logic of what
rhymes with what -- the art is minimal.

### Node tree

```
RhymeFinder (VBoxContainer)
├── PromptSection (HBoxContainer)
│   ├── PromptBg (NinePatchRect) [rhyme_prompt_bg]
│   │   └── PromptWord (Label)
│   └── SoundWaveFx (AnimatedSprite2D) [sound_wave_fx]  <- appears when TTS reads
└── OptionsGrid (GridContainer, 2x2)
    └── [RhymeOption x 4]
        └── NinePatchRect [rhyme_option_*]
            └── Label (option word)
```

---

## 10. Celebration Scene

**File:** res://scenes/Celebration/Celebration.tscn
**Function:** Passage completion transformation. Implemented as a state within PassageView's state machine -- not a separate scene load.
**M1:** functional with placeholder art. **M2:** richer animation + discovery moment.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| celebration_bg_stub | TextureRect | 480x270 | 1920x1080 | fill | static | no | structural | M1 | #2C1A0E background |
| celebration_bg | AnimatedSprite2D | 480x270 | 1920x1080 | fill | -- | loop (8-12fr @ 8fps) | structural | M2 | -- (replaces stub) |
| owl_celebrate | (see s2) | -- | 256x256 | center-bottom | -- | -- | decorative | M2 | -- |
| owl_excited | (see s2) | -- | 256x256 | center-bottom | -- | -- | decorative | M2 | -- |
| sticker_earned | TextureRect | 32x32 | 128x128 | center-right | -- | slide-in one-shot | interactive | M2 | #D4A017 accent |
| fragments_row_big | HBoxContainer (1-3 light fragments 16px) | -- | top-center | top-center | -- | animate in sequentially | structural | M1 | -- (see s2 fragments) |
| btn_continue | TextureButton | 32x12 | 128x48 | bottom-center | normal / pressed | no | interactive | M1 | #E8721A accent_warm |
| confetti_fx | AnimatedSprite2D | 480x270 | 1920x1080 | fill (overlay) | -- | one-shot (12fr @ 12fps) | decorative | M2 | #D4A017 accent |
| label_passage_result | Label | -- | top of scene | top-center | static | no | decorative | M1 | -- (text) |
| discovery_book_fx | AnimatedSprite2D | 16x24 | 64x96 | random shelf position | -- | one-shot (6fr @ 8fps) | decorative | M2 | #7B4FBE magic_glow |
| discovery_word_fx | AnimatedSprite2D | 48x16 | 192x64 | over staff crystal | -- | one-shot (8fr @ 6fps) | decorative | M2 | #F5E6C8 parchment |

M1 implementation: celebration_bg_stub is a TextureRect with a ColorRect placeholder.
fragments_row_big uses fragment_light assets from s2. btn_continue is a TextureButton
with ColorRect. Fully functional without art.

Discovery moment (M2):
discovery_book_fx -- a book briefly floats out of the background shelf and glows,
then returns. Plays automatically 1 second after fragments appear. No interaction required.

discovery_word_fx -- Profile advanced only. The first target word of the next passage
appears briefly in Owlorumo's staff crystal, then fades. No label, no explanation.
GameManager provides the word before Celebration loads. The child who sees it and
finds it in the next passage experiences a moment of recognition that belongs
entirely to them.

---

### Journal Assets

| asset_id | node_type | draw_size | display_size | location | states | milestone |
|---|---|---|---|---|---|---|
| journal_book_cover | TextureButton | 24×32 px | 96×128 | Library scene, near Owlorumo | closed / open (hover) | M1 final |
| journal_page_bg | TextureRect | full screen | full screen | Journal scene | — | M2 |
| journal_nav_arrow | TextureButton | 16×16 px | 64×64 | Journal scene | left / right | M2 |
| journal_save_word_icon | TextureButton | 16×16 px | 64×64 | PassageView (post-completion) | normal / pressed | M2 |

### Sticker Assets

| asset_id | node_type | draw_size | display_size | location | milestone |
|---|---|---|---|---|---|
| sticker_template_book | TextureRect | 24×24 px | 96×96 | Journal sticker grid | M2 |
| sticker_template_library | TextureRect | 24×24 px | 96×96 | Journal sticker grid | M2 |

Book souvenir stickers are provided by BookPack authors in their pack's `stickers/` directory. Library milestone stickers (~6) are engine assets.

### Hidden Book Assets

| asset_id | node_type | draw_size | display_size | location | milestone |
|---|---|---|---|---|---|
| hidden_book_sprite | TextureRect | 16×24 px | 64×96 | Library resting shelves | M1 final |
| resting_shelf_texture | TextureRect | varies | varies | Library scene (2–3 shelves) | M1 final |

3–5 variants of hidden book sprite (ancient, mysterious, distinct from regular BookPack books).

### Settings Screen Assets

| asset_id | node_type | draw_size | display_size | milestone |
|---|---|---|---|---|
| flag_en | TextureRect | 32×24 px | 64×48 | M1 |
| flag_es | TextureRect | 32×24 px | 64×48 | M1 |
| icon_music | TextureRect | 16×16 px | 64×64 | M1 |
| icon_sfx | TextureRect | 16×16 px | 64×64 | M1 |
| icon_voice | TextureRect | 16×16 px | 64×64 | M1 |
| icon_speaker | TextureRect | 16×16 px | 64×64 | M1 |
| icon_speaker_muted | TextureRect | 16×16 px | 64×64 | M1 |
| icon_gear | TextureRect | 16×16 px | 64×64 | M1 |
| icon_back_arrow | TextureRect | 16×16 px | 64×64 | M1 |
| font_size_preview (×4) | TextureButton | 24×24 px | 96×96 | M1 |
| colorblind_swatch (×4) | TextureRect | 16×16 px | 64×64 | M2 |

---

## 12. Settings Scene

**File:** res://scenes/Settings/Settings.tscn
**Function:** Session settings -- language, TTS speed, font size, visual theme.
**Audience:** Adult (parent / teacher). More sober, less decorative UI.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| settings_bg | TextureRect | 480x270 | 1920x1080 | fill | static | no | structural | M2 | #2C1A0E background |
| settings_panel | NinePatchRect | 48x48 | fills center | center | static | no | structural | M2 | #4A2E1A surface |
| btn_back | TextureButton | 24x24 | 96x96 | top-left | normal / pressed | no | interactive | M1 | #6B4226 surface_light |
| toggle_normal | TextureRect | 24x12 | 96x48 | center | off | no | interactive | M2 | #9E9E9E neutral |
| toggle_on | TextureRect | 24x12 | 96x48 | center | on | no | interactive | M2 | #4CAF50 correct |
| slider_track | TextureRect | 64x4 | 256x16 | center | static | no | interactive | M2 | #9E9E9E neutral |
| slider_thumb | TextureRect | 8x8 | 32x32 | center over track | normal / dragging | no | interactive | M2 | #D4A017 accent |
| theme_preview_frame | NinePatchRect | 32x20 | 128x80 | center in grid | normal / selected | no | interactive | M3 | #6B4226 surface_light |

M1: Settings only needs a functional btn_back and native Godot controls
(HSlider, CheckButton, OptionButton) without custom art. Custom assets are M2/M3.

---

## 13. Onboarding Flow

**Function:** Child's first time -- meet Owlorumo, learn the core mechanic through narrative.
**Milestone:** M1 (minimal functional), M2 (with full art).

Design: The Onboarding is a standard BookPack with is_onboarding: true.
No special scene or code path. Owlorumo starts in state_0 (cracked crystal, dark).
Owlorumo's name is fixed -- the child does not choose it. See GDD Onboarding section.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| onboarding_bg | TextureRect | 480x270 | 1920x1080 | fill | static | no | structural | M1 | #2C1A0E background |
| btn_confirm | TextureButton | 32x12 | 128x48 | bottom-center | normal / pressed / disabled | no | interactive | M1 | #E8721A accent_warm |
| tutorial_bubble | NinePatchRect | 64x32 | 256x128 | above owl | static | no | decorative | M2 | #F5E6C8 parchment |
| tutorial_arrow | TextureRect | 8x16 | 32x64 | below bubble | static | no | decorative | M2 | #F5E6C8 parchment |
| owl_wave | (see s2) | -- | 256x256 | center | -- | -- | decorative | M2 | -- |
| owl_idle_state0 | (see s2 -- state_0 atlas) | -- | 256x256 | center | -- | -- | decorative | M1 | -- |

M1: Owlorumo is shown in state_0 -- cracked crystal, dark, navy form, diminished presence.
This is the most important visual state to deliver first -- it establishes the narrative
of diminishment before the child begins restoring him.

---

## Appendix A -- M1 Priorities Summary

Assets that must exist (real art or correct placeholder) before M1 is complete
and before the crowdfunding campaign demo is recorded:

```
GLOBAL (art required for campaign):
  atlas_owlorumo_state0.png      -- all animations, draw 64x64, cracked crystal
  atlas_owlorumo_state1.png      -- same layout, faint crystal (shows progression)
  fragment_light_small / large   -- AnimatedSprite2D, 8x8 / 16x16
  icon_hint                      -- TextureRect, 16x16 -- staff crystal motif

LIBRARY:
  bg_library_layer_4             -- Sprite2D, 480x270
  bg_library_layer_3             -- Sprite2D, 480x270
  book_readable, book_dormant    -- TextureButton/TextureRect, 16x24

PASSAGEVIEW:
  parchment_tile, wood_tile      -- TextureRect tile, 64x64
  btn_exit, book_tts             -- TextureButton, 24x24 / 16x16

WORDGLOW:
  tile_word_normal               -- NinePatchRect, 16x8
  tile_word_selected             -- NinePatchRect, 16x8
  tile_word_found                -- NinePatchRect, 16x8
  slot_word_empty                -- NinePatchRect, 16x8
  slot_word_filled               -- NinePatchRect, 16x8

CELEBRATION:
  celebration_bg_stub            -- TextureRect, 480x270 -- ColorRect valid
  btn_continue                   -- TextureButton, 32x12
  fragments_row_big              -- uses fragment_light assets from GLOBAL

SETTINGS:
  btn_back                       -- TextureButton, 24x24

ONBOARDING:
  onboarding_bg                  -- TextureRect -- ColorRect valid
  btn_confirm                    -- TextureButton, 32x12
  owl_idle_state0                -- via AnimatedSprite2D state_0 atlas (see s2)
```

Total M1 art: approximately 20 real art assets + rest as color placeholders.
All nodes must be the final type -- do not use ColorRect directly in the
final tree, only as a temporary child of the correct node.

---

## Appendix B -- Implementation Checklist per Asset

Before considering an asset "correctly implemented" in code, verify:

```
The node is the correct type (no ColorRect in production)
draw_size matches the PNG import (not rescaled in Godot)
display_size = draw_size x scale (Owlorumo: x3 PassageView, x4 Library)
Import settings: Filter=Nearest, Mipmaps=OFF, Compress=Lossless
anchor/alignment configured correctly in the editor
All states have their PNG (or frame in SpriteFrames)
tap target >= 96x96 for any interactive element
The node with layout_role=structural does not have position hardcoded in code
Owlorumo node uses correct state atlas from save profile (not hardcoded state_0)
```

---

Document: READCRAFTERY Asset Contracts v1.1
Update when new scenes are added or when the Art Guide changes dimensions.
This document is the source of truth for dimensions and node types --
the Art Guide is the source of truth for style and palette.
