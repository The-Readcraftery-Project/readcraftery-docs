# READCRAFTERY — Contratos de Assets
**Versión:** 1.0  
**Fecha:** marzo de 2026  
**Estado:** Preproducción  
**Documentos complementarios:** Guía de Arte v1.2 · Guía de Construcción v1.3 · Contrato de Arquitectura v1.1

---

> **Propósito de este documento**
>
> Cada fila de cada tabla es un contrato entre el código y el arte.
> El código se escribe contra estas tablas — nunca contra el arte real.
> El arte se produce contra estas tablas — nunca contra el código.
> Cuando llega el arte real, el cambio es sustitución de textura, no refactor.
>
> **Cómo usar placeholders:**
> Para cada asset, instanciar el `node_type` correcto con `modulate = Color("hex")`
> usando el `placeholder_color` de la tabla. Cuando llega el arte: asignar la
> textura, borrar el modulate. Nada más cambia.
>
> **Escala global:** todos los assets de juego se dibujan en píxeles nativos
> y se muestran a 4× en viewport 1920×1080. `display_size` = `draw_size × 4`.
> El texto de pasajes y UI labels vive en resolución nativa 1080p — no escala.

---

## Tabla de Contenidos

1. [Convenciones](#1-convenciones)
2. [Assets Compartidos — Global UI](#2-assets-compartidos--global-ui)
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

## 1. Convenciones

### Columnas de la tabla

| Columna | Descripción |
|---|---|
| `asset_id` | Nombre de archivo sin extensión. Es el identificador canónico. |
| `node_type` | Nodo de Godot que renderiza este asset. Usar este nodo en el placeholder — no cambia cuando llega el arte. |
| `draw_size` | Dimensiones en píxeles de dibujo (lo que dibuja el artista). |
| `display_size` | Dimensiones en pantalla a 4×. Para NinePatch: tamaño mínimo del contenedor. |
| `anchor` | Punto de anclaje del nodo. En Godot: `PRESET_*` del enum `Control` o `centered` para `Sprite2D`. |
| `states` | Lista de estados visuales requeridos. Cada estado = un archivo PNG separado (o frame en AnimatedSprite2D). |
| `animates` | Si el asset tiene animación en loop o one-shot. Formato: `tipo (Nframes @ Xfps)`. |
| `layout_role` | `structural` = define layout (mover rompe la pantalla) · `interactive` = el niño toca esto · `decorative` = solo visual |
| `priority` | Milestone en que debe existir el arte real. M0 = bloqueador de primer pasaje jugable. |
| `placeholder_color` | Token de paleta para el ColorRect/modulate del placeholder. |

### Node types usados en este documento

```
Sprite2D          — imagen estática, no participa en layout de Control
AnimatedSprite2D  — sprite con múltiples animaciones (el Istari Owl)
TextureRect       — imagen en el sistema de layout de Control (se estira/adapta)
NinePatchRect     — imagen que se estira sin distorsionar esquinas (tiles, botones)
TextureButton     — botón con textura, maneja hover/pressed/disabled automáticamente
AnimationPlayer   — no renderiza — controla animaciones de otros nodos
ParallaxBackground/ParallaxLayer — nodos de parallax de Godot
ColorRect         — SOLO para placeholders. Reemplazar cuando llega el arte.
```

### Placeholder pattern en GDScript

```gdscript
# Placeholder correcto — el nodo ya es el tipo final
@onready var btn_hint: TextureButton = $BottomBar/BtnHint

func _ready() -> void:
    # Placeholder: color sólido hasta que llegue el arte
    # Cuando llegue el arte: borrar estas 2 líneas y asignar texture_normal
    var placeholder := ColorRect.new()
    placeholder.color = Color("#D4A017")  # accent — color del token
    placeholder.size = Vector2(96, 96)    # display_size
    btn_hint.add_child(placeholder)
```

---

## 2. Assets compartidos — UI global

Assets que aparecen en múltiples escenas. Se definen una vez, se referencian en cada escena.

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

### Notas de implementación — Owl

El Istari Owl usa **un solo nodo `AnimatedSprite2D`** con múltiples animaciones nombradas. No son nodos separados.

```gdscript
# En cualquier escena que muestre el Owl:
@onready var owl: AnimatedSprite2D = $Owl

func set_owl_state(state: String) -> void:
    owl.play(state)  # state = "idle", "thinking", "hint", etc.
```

El atlas está en `res://content/atlas_owl.png`. Las animaciones se definen en el `SpriteFrames` resource asignado al nodo — no en código.

---

## 3. Escena Library

**Archivo:** `res://scenes/Library/Library.tscn`  
**Función:** Menú principal. El niño selecciona un libro para leer.  
**Layout:** Pantalla completa. Parallax de 4 layers. El Owl en posición fija derecha.

### Background — parallax layers

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `bg_library_layer_4` | Sprite2D (en ParallaxLayer) | 480×270 | 1920×1080 | top-left | — | no (estático) | structural | M0 | `#2C1A0E` background |
| `bg_library_layer_3` | Sprite2D (en ParallaxLayer) | 480×270 | 1920×1080 | top-left | — | no (factor 0.1) | structural | M0 | `#4A2E1A` surface |
| `bg_library_layer_2` | Sprite2D (en ParallaxLayer) | 480×270 | 1920×1080 | top-left | — | no (factor 0.3) | structural | M1 | `#6B4226` surface_light |
| `bg_library_layer_1` | Sprite2D (en ParallaxLayer) | 480×270 | 1920×1080 | top-left | — | no (factor 0.6) | structural | M1 | `#4A2E1A` surface |

> **M0:** layers 3 y 4 con arte real. Layers 1 y 2 como ColorRect plano.  
> **M1:** los 4 layers con arte real y parallax activo.

### UI interactiva

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `book_available` | TextureButton | 16×24 | 64×96 | center | normal / hover / focused | shimmer loop (4fr @ 4fps) — M1 | interactive | M0 | `#D4A017` accent |
| `book_locked` | TextureRect | 16×24 | 64×96 | center | static | no | decorative | M0 | `#9E9E9E` neutral |
| `book_completed` | TextureRect | 16×24 | 64×96 | center | static | glow loop (4fr @ 3fps) — M1 | decorative | M1 | `#D4A017` accent |
| `book_lock_icon` | TextureRect | 8×8 | 32×32 | center-bottom over book | static | no | decorative | M0 | `#9E9E9E` neutral |
| `btn_settings` | TextureButton | 24×24 | 96×96 | top-right | normal / pressed / disabled | no | interactive | M1 | `#6B4226` surface_light |
| `owl_idle` | (ver §2) | — | — | bottom-right | — | — | decorative | M0 | — |

### Árbol de nodos sugerido

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

## 4. Escena PassageView

**Archivo:** `res://scenes/PassageView/PassageView.tscn`  
**Función:** Muestra el pasaje de texto y aloja el puzzle activo.  
**Layout:** HSplitContainer — 60% passage panel izquierda, 40% puzzle panel derecha.

### Panels de fondo

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `parchment_tile` | TextureRect (tile mode) | 64×64 | fills 60% width | top-left | static | no | structural | M0 | `#F5E6C8` parchment |
| `wood_tile` | TextureRect (tile mode) | 64×64 | fills 40% width | top-right | static | no | structural | M0 | `#4A2E1A` surface |

### Passage Panel (izquierda, 60%)

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `passage_text` | RichTextLabel | — | fills panel - padding | top-left | normal / word_highlighted | no (BBCode handles highlight) | structural | M0 | — (es texto, no imagen) |
| `book_illustration` | TextureRect | variable | max 30% panel height | top-center | static | no | decorative | M1 | `#6B4226` surface_light |
| `passage_title` | Label | — | top of panel | top-left | static | no | decorative | M0 | — (es texto) |

### Bottom Bar (compartida entre passage y puzzle)

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `btn_hint` | TextureButton | 24×24 | 96×96 | bottom-right | normal / pressed / disabled | no | interactive | M0 | `#7B4FBE` magic_glow |
| `btn_exit` | TextureButton | 24×24 | 96×96 | bottom-left | normal / pressed | no | interactive | M0 | `#E53935` incorrect |
| `hint_counter` | Label | — | over btn_hint | center | static | no | decorative | M0 | — (es texto) |
| `star_row` | HBoxContainer (3× star) | — | top of bottom bar | top-center | — | — | decorative | M0 | — (ver §2 stars) |

### Puzzle Panel (derecha, 40%)

El puzzle panel es un contenedor vacío. El puzzle activo se instancia dinámicamente dentro. Ver §5–§9 para los assets de cada tipo de puzzle.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `puzzle_container` | MarginContainer | — | fills 40% | top-right | — | — | structural | M0 | — (contenedor vacío) |
| `owl_thinking` | (ver §2) | — | 192×192 | top-right corner | — | — | decorative | M0 | — |

### Árbol de nodos sugerido

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
│       └── [puzzle instanciado dinámicamente aquí]
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

## 5. Puzzle WordGlow

**Archivo:** `res://scenes/Puzzles/WordGlow/WordGlow.tscn`  
**Ages:** 4–6  
**Mecánica:** El niño toca palabras en el pasaje que coinciden con el word bank.  
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

### Árbol de nodos

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

## 6. Puzzle Scramble

**Archivo:** `res://scenes/Puzzles/Scramble/Scramble.tscn`  
**Ages:** 5–7  
**Mecánica:** El niño reordena letras en tiles individuales para formar la palabra target.  
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
| `word_target_label` | Label | — | top of puzzle | top-center | static | no | structural | M0 | — (es texto) |

### NinePatch margins para `tile_letter_*` y `slot_letter_*`

```
patch_margin_*: 4 en todos los lados (igual que tile_word)
```

### Árbol de nodos

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

## 7. Puzzle WordHunt

**Archivo:** `res://scenes/Puzzles/WordHunt/WordHunt.tscn`  
**Ages:** 6–9  
**Mecánica:** Grid de letras. El niño selecciona letras contiguas para encontrar palabras.  
**Instanciado en:** PuzzleContainer de PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `grid_cell_normal` | NinePatchRect | 16×16 | 64×64 | center | — | no | interactive | M0 | `#4A2E1A` surface |
| `grid_cell_hover` | NinePatchRect | 16×16 | 64×64 | center | — | no | interactive | M0 | `#6B4226` surface_light |
| `grid_cell_selected` | NinePatchRect | 16×16 | 64×64 | center | — | no | interactive | M0 | `#D4A017` accent |
| `grid_cell_found` | NinePatchRect | 16×16 | 64×64 | center | — | glow loop | decorative | M0 | `#4CAF50` correct |
| `grid_cell_hint` | NinePatchRect | 16×16 | 64×64 | center | — | pulse loop | decorative | M0 | `#FF9800` hint |
| `found_word_label` | Label | — | lista lateral | top-left | normal / found (strikethrough) | no | structural | M0 | — (texto) |
| `grid_selection_line` | Line2D | — | overlay sobre grid | absolute | — | animates con drag | decorative | M1 | `#D4A017` accent |

> **Nota:** `grid_selection_line` es un `Line2D`, no una textura — se dibuja en código siguiendo las celdas seleccionadas. No tiene asset de arte.

### Árbol de nodos

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

## 8. Puzzle FillPassage

**Archivo:** `res://scenes/Puzzles/FillPassage/FillPassage.tscn`  
**Ages:** 7–9  
**Mecánica:** El pasaje tiene palabras en blanco. El niño arrastra palabras del bank a los huecos.  
**Instanciado en:** PuzzleContainer de PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `blank_slot_empty` | NinePatchRect | 32×8 | 128×32 | inline en texto | — | pulse loop | interactive | M0 | `#2C1A0E` background |
| `blank_slot_filled` | NinePatchRect | 32×8 | 128×32 | inline en texto | — | no | interactive | M0 | `#E8D4A8` parchment_shadow |
| `blank_slot_correct` | NinePatchRect | 32×8 | 128×32 | inline en texto | — | pulse one-shot | decorative | M0 | `#4CAF50` correct |
| `blank_slot_incorrect` | NinePatchRect | 32×8 | 128×32 | inline en texto | — | shake one-shot (500ms) | decorative | M0 | `#E53935` incorrect |
| `tile_word_draggable` | NinePatchRect | 16×8 | min 64×32 | center (en bank) | normal / dragging / placed | lift shadow on drag | interactive | M0 | `#F5E6C8` parchment |
| `drag_shadow` | TextureRect | 16×8 | igual que tile | absolute (sigue cursor) | — | no | decorative | M1 | `#2C1A0E` background (semitransparente) |

> **Nota de implementación:** `FillPassage` no usa `RichTextLabel` para el pasaje — el texto se divide en `Label` + `blank_slot` intercalados en un `HFlowContainer`. Los blanks son `NinePatchRect` con drop zones.

### Árbol de nodos

```
FillPassage (VBoxContainer)
├── PassageFlow (HFlowContainer)
│   └── [alternancia dinámica de Labels y BlankSlots]
│       └── NinePatchRect [blank_slot_*]
│           └── Label (palabra colocada, si existe)
└── WordBank (HBoxContainer)
    └── [DraggableWord × N targets]
        └── NinePatchRect [tile_word_draggable]
            └── Label (palabra)
```

---

## 9. Puzzle RhymeFinder

**Archivo:** `res://scenes/Puzzles/RhymeFinder/RhymeFinder.tscn`  
**Ages:** 4–7  
**Mecánica:** Se muestra una palabra. El niño elige cuál de las opciones rima con ella.  
**Instanciado en:** PuzzleContainer de PassageView.

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `rhyme_prompt_bg` | NinePatchRect | 48×16 | 192×64 | top-center | static | no | structural | M0 | `#D4A017` accent |
| `rhyme_option_normal` | NinePatchRect | 32×16 | 128×64 | center | — | no | interactive | M0 | `#F5E6C8` parchment |
| `rhyme_option_hover` | NinePatchRect | 32×16 | 128×64 | center | — | no | interactive | M0 | `#E8D4A8` parchment_shadow |
| `rhyme_option_correct` | NinePatchRect | 32×16 | 128×64 | center | — | bounce one-shot | decorative | M0 | `#4CAF50` correct |
| `rhyme_option_incorrect` | NinePatchRect | 32×16 | 128×64 | center | — | shake one-shot (500ms) | decorative | M0 | `#E53935` incorrect |
| `sound_wave_fx` | AnimatedSprite2D | 16×16 | 64×64 | beside prompt word | — | one-shot (4fr @ 8fps) | decorative | M1 | `#7B4FBE` magic_glow |

> **RhymeFinder es el puzzle más simple visualmente.** Los 4 tiles de opción son NinePatchRect con Label encima. No hay drag, no hay grid. La complejidad está en la lógica de qué rima con qué — el arte es mínimo.

### Árbol de nodos

```
RhymeFinder (VBoxContainer)
├── PromptSection (HBoxContainer)
│   ├── PromptBg (NinePatchRect) [rhyme_prompt_bg]
│   │   └── PromptWord (Label)
│   └── SoundWaveFx (AnimatedSprite2D) [sound_wave_fx]  ← aparece al leer con TTS
└── OptionsGrid (GridContainer, 2×2)
    └── [RhymeOption × 4]
        └── NinePatchRect [rhyme_option_*]
            └── Label (palabra opción)
```

---

## 10. Escena Celebration

**Archivo:** `res://scenes/Celebration/Celebration.tscn`  
**Función:** Pantalla de victoria al completar un libro o un pasaje con todas las estrellas.  
**M0:** frame estático placeholder. M1: animación completa.

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

> **M0 implementation:** `celebration_bg_stub` es un `TextureRect` con `ColorRect` placeholder. `stars_row_big` usa los assets de `star_empty/star_filled` de §2. `btn_continue` es `TextureButton` con `ColorRect`. Todo funcional sin arte.

---

## 11. Escena Journal

**Archivo:** `res://scenes/Journal/Journal.tscn`  
**Función:** El diario del niño — stickers ganados, palabras guardadas, progreso.  
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

## 12. Escena Settings

**Archivo:** `res://scenes/Settings/Settings.tscn`  
**Función:** Ajustes de la sesión — idioma, velocidad TTS, tamaño de fuente, tema visual.  
**Audience:** Adulto (parent / teacher). UI más sobria, menos decorativa.

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

> **M0:** Settings solo necesita `btn_back` funcional y los controles de Godot nativos (`HSlider`, `CheckButton`, `OptionButton`) sin arte custom. Los assets custom son M1/M2.

---

## 13. Flujo de onboarding

**Función:** Primera vez del niño — elegir nombre del Owl, tutorial básico.  
**Milestone:** M0 (mínimo funcional), M1 (con arte completo).

| asset_id | node_type | draw_size | display_size | anchor | states | animates | layout_role | priority | placeholder_color |
|---|---|---|---|---|---|---|---|---|---|
| `onboarding_bg` | TextureRect | 480×270 | 1920×1080 | fill | static | no | structural | M0 | `#2C1A0E` background |
| `name_input_bg` | NinePatchRect | 48×16 | 192×64 | center | normal / focused | no | interactive | M0 | `#F5E6C8` parchment |
| `btn_confirm` | TextureButton | 32×12 | 128×48 | bottom-center | normal / pressed / disabled | no | interactive | M0 | `#E8721A` accent_warm |
| `tutorial_bubble` | NinePatchRect | 64×32 | 256×128 | above owl | static | no | decorative | M1 | `#F5E6C8` parchment |
| `tutorial_arrow` | TextureRect | 8×16 | 32×64 | below bubble | static | no | decorative | M1 | `#F5E6C8` parchment |
| `owl_wave` | (ver §2) | — | 192×192 | center | — | — | decorative | M0 | — |

---

## Apéndice A — Resumen de prioridades M0

Assets que deben existir (arte real o placeholder correcto) antes del primer pasaje jugable:

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
  onboarding_bg  (TextureRect — ColorRect válido)
  name_input_bg  (NinePatchRect, 48×16)
  btn_confirm     (TextureButton, 32×12)
  owl_wave        (via AnimatedSprite2D de §2)
```

Total M0: **~20 assets** de arte real + resto como placeholders de color. Todos los nodos deben ser el tipo final — no usar `ColorRect` directamente en el árbol final, sino como child temporal del nodo correcto.

---

## Apéndice B — Checklist de implementación por asset

Antes de considerar un asset "implementado correctamente" en código, verificar:

```
□ El nodo es el tipo correcto (no ColorRect en producción)
□ draw_size coincide con el import del PNG (no se reescala en Godot)
□ display_size es draw_size × 4 (scale del nodo = Vector2(4, 4))
□ Import settings: Filter=Nearest, Mipmaps=OFF, Compress=Lossless
□ anchor/alignment configurado correctamente en el editor
□ Todos los estados tienen su PNG (o frame en SpriteFrames)
□ tap target ≥ 96×96 para cualquier elemento interactive
□ El nodo con layout_role=structural no tiene position hardcodeada en código
```

---

*Documento: READCRAFTERY Asset Contracts v1.0*  
*Actualizar cuando se añaden nuevas escenas o cuando el Guía de Arte cambia dimensiones.*  
*Este documento es fuente de verdad para dimensiones y node types — el Guía de Arte es fuente de verdad para estilo y paleta.*
