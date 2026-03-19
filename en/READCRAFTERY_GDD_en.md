# READCRAFTERY — Game Design Document
**Version:** 1.4  
**Date:** March 2026  
**Status:** Pre-Production Spec  
**Author:** Andrés Reyes. El Programador Pobre  
**Companion documents:** Architecture Contract v1.2 · Build Guide v1.4  

---

> **Note for technical readers:** This document describes the game's product vision and design intent.
> It includes future-facing ideas such as public mod tooling, advanced localization paths, and classroom-oriented usage patterns that may not yet have a closed technical contract.
> To see what is specified and buildable today, see the **Architecture Contract**.
> For build order and implementation guidance, see the **Build Guide**.

---


## Table of Contents

1. [Game Overview](#1-game-overview)
2. [Vision & Pillars](#2-vision--pillars)
3. [Target Audience](#3-target-audience)
4. [Core Gameplay Loop](#4-core-gameplay-loop)
5. [Puzzle Mechanics](#5-puzzle-mechanics)
6. [Literary Integration System](#6-literary-integration-system)
7. [Progression & Reward Systems](#7-progression--reward-systems)
8. [Visual Effects & Feedback](#8-visual-effects--feedback)
9. [UI/UX Design](#9-uiux-design)
10. [Audio Design](#10-audio-design)
11. [Accessibility & Localization](#11-accessibility--localization)
12. [Classroom & Caregiver Use](#12-classroom--caregiver-use)
13. [Modding System](#13-modding-system)
14. [Monetization Strategy](#14-monetization-strategy)
15. [Platform Strategy](#15-platform-strategy)
16. [Technology Stack Recommendation](#16-technology-stack-recommendation)
17. [Technical Architecture](#17-technical-architecture)
18. [Concept Art Descriptions](#18-concept-art-descriptions)
19. [Release Roadmap](#19-release-roadmap)
20. [Open Questions & Risks](#20-open-questions--risks)

---

## 1. Game Overview

| Field | Details |
|---|---|
| **Title** | READCRAFTERY |
| **Tagline** | *"Reading is a power that changes the world."* |
| **Genre** | Educational Word Puzzle / Literary Adventure |
| **Primary Platform** | PC (Windows/Mac/Linux), Web (HTML5), Android & iOS |
| **Target Age** | 4–9 years old (core); usable in classroom and home contexts |
| **Language Scope** | English and Spanish are the core product languages; the closed localization system lands in M2 |
| **Monetization** | One-time purchase (itch.io / Steam) — pay once, own forever |

### Elevator Pitch
READCRAFTERY is a reading-first word discovery game set in a magical sleeping library. Players explore books, read passages, and then recognize words and patterns inside the text through warm, age-appropriate puzzle play. Each successful interaction returns light to Owlorumo's crystal and helps reawaken the library. The content system is designed so books — and later themes — can be extended through the same mod-friendly structure.

### Design Thesis — ✅ CLOSED
**Reading is a power that discovers and restores human knowledge.**

The child does not begin by hunting disconnected targets. The child reads the passage first, then recognizes and names words and patterns inside it. Immediate puzzle feedback may react to individual correct interactions, but major restoration happens through meaningful reading milestones across passages, books, and arcs.

---

## 2. Vision & Pillars

### The Core Mechanic — One Sentence

**Reading restores the world in a visible and thematic way.**

This is not a metaphor. It is the mechanic:
- Every word the child finds returns a fragment of light to Owlorumo's crystal
- Every book completed restores a layer of his presence and memory
- Every arc completed brings the library into a more awake, more responsive state — opening new continuity rather than returning to a pristine past

The child is doing something that matters
in a world that responds to reading as a real force.

This is what makes Readcraftery different from every other literacy game:
the reward is not external to the reading act — it is the reading act itself,
made visible.

### Design Pillars

| Pillar | Description |
|---|---|
| 🔤 **Reading First** | Every mechanic must reinforce reading skills, never replace them. The text is always present and central. |
| 🎉 **Joyful Reward** | Children must feel celebrated frequently. Visual and audio feedback must be immediate, warm, and exciting. |
| 📚 **Literary Respect** | Books are not mere word banks — the story matters. Players should come away having absorbed content. |
| 🔧 **Open by Design** | Modding is not an afterthought; the content system IS the game. Books are mods. Themes are mods. |
| 🧭 **Classroom-Aware** | The core loop must work in short school sessions and in free play at home. Optional discovery layers must never block the reading task. |

---

## 3. Target Audience

### Primary: Children Ages 4–9

**Sub-segments:**
- **Ages 4–6 (Pre-Readers / Early Phonics):** Focus on letter recognition, simple 2–3 letter words, picture-aided vocabulary. Needs heavy visual support, large fonts, audio read-aloud of all text.
- **Ages 6–9 (Early Readers):** Can handle 4–6 letter words, basic sentences, short passages. Benefit from context clues and comprehension questions.

### Reader profiles — internal segmentation

The 4–9 age range covers very different stages of reading development.
The game recognizes three internal profiles:

**Profile A — Pre-reader (ages 4–5)**
Not yet decoding. Recognizes letters and their own name.
The game offers exposure to written language and phonological awareness.
Book packs marked `early_emergent` are designed for this profile.
WordGlow in simplified mode (TTS reads each word on touch,
no expectation of independent reading).

**Profile B — Emergent reader (ages 6–7)**
Learning to decode. Reads syllable by syllable.
Needs phonetically regular words, repetition, and feedback without frustration.
This is Readcraftery's primary design profile.

**Profile C — Developing reader with difficulties (ages 7–9)**
Can read with effort. May have dyslexia, ADHD, or less prior exposure.
Needs controlled vocabulary texts, appropriate fonts, and a pace
that does not expose them negatively in front of peers.
The `dyslexia_font` and `reduce_motion` modes are designed
primarily for this profile.

> **Design note:** Profile B is the center of gravity of the game.
> Design decisions that conflict between profiles
> are resolved in favor of Profile B.


#### Golden Path — Profile B (Emerging Reader, age ~6)

M0/M1 validation criterion: if WordGlow does not work well for a 6-year-old who is still sounding out syllables, the engine is not validated.
The core gameplay loop is designed and tested first for Profile B — a child who recognizes letters, is learning to decode words, and benefits from visual + auditory scaffolding. This is the product's center of gravity.
ProfileDescriptionMilestone priorityA — Pre-reader (age 4–5)Cannot decode yet. Needs heavy visual/audio support.Adjacent, exploratory. Not M0 validation criteria.B — Emerging reader (age 5–7)Decoding syllables. Golden Path. Core product fit.M0/M1 — primary target.C — Reader with difficulties (age 6–9)Dyslexia, ADHD, visual stress. Needs accessibility adaptations.M2 — accessibility presets, theme support, TTS pacing.
Profile A and C are real audiences, but the game is validated against Profile B first. Features specific to A or C that don't serve B are deferred to their respective milestones.

### Secondary: Educators & Caregivers
- Primary school teachers looking for literacy tools
- Parents seeking screen time with learning value
- Homeschool families

### Tertiary: Modding Community
- Indie developers who want to add book content
- Educators and facilitators selecting or curating suitable book packs
- Word puzzle enthusiasts (ages 10+) drawn by community content

### Persona Examples

**"Sofia, age 6"** — learning to read in Spanish and English at home. Loves bright colors and animals. Gets frustrated quickly if puzzles are too hard. Needs audio support and positive reinforcement constantly.

**"Ms. Rivera, 2nd Grade Teacher"** — wants to use the game as a shared or station-based reading activity. She values short, readable sessions, the ability to skip optional rewards when time is tight, and the option to revisit discovered content later without breaking the lesson flow.

**"Carlos, indie game dev"** — wants to upload a public domain book and create a puzzle pack to share on itch.io. Needs clean JSON documentation and a mod preview tool.

---

## 4. Core Gameplay Loop

```
┌─────────────────────────────────────────────────────────────┐
│                    THE READCRAFTERY LOOP                    │
│                                                             │
│  [LIBRARY]  →  [CHOOSE BOOK]  →  [READ PASSAGE]             │
│                                          ↓                  │
│  [CELEBRATE] ←  [FIND WORDS]  ←  [PUZZLE CHALLENGE]         │
│       ↓                                                     │
│  [RESTORATION: next passage / journal / library response]   │
│       ↓                                                     │
│  [RETURN TO LIBRARY or CONTINUE BOOK]                       │
└─────────────────────────────────────────────────────────────┘
```

### Step-by-Step Flow

1. **The Sleeping Library** — The main menu is a living, magical library discovered in a dormant state. Bookshelves line the walls. Some books glow softly to invite interaction. Others remain quiet and unresponsive. Owlorumo is present nearby, not as decoration, but as part of the place itself.

2. **Book Selection** — The player picks a book. Each book has a cover, a title, and a readable age/reading-stage presentation. Dormant books do not use numeric progress gates; they awaken through restoration milestones and library response.

3. **Story Time (Passage View)** — A passage from the book is displayed. Large, friendly font. Illustration alongside (if the book pack includes art). Owlorumo or the passage audio reads the passage aloud (runtime TTS or recorded narration). The player can replay the reading at any time.

4. **Puzzle Challenge** — Below or alongside the passage, a puzzle appears. The type of puzzle depends on the difficulty tier and the player's age profile. (See Section 5.)

5. **Word Discovery** — The player interacts with words and patterns. Successful finds trigger immediate warm feedback.

6. **Passage Complete** — The current scene transforms briefly in response to completion. Fragments of white-gold light return to Owlorumo's crystal, new words learned may be surfaced, and an optional short comprehension beat may follow.

7. **Restoration & Continuity** — New passage access, book awakening, or quiet library changes may occur through restoration milestones. The player returns to the library or continues reading.

### Library Book Interaction — ✅ CLOSED

Books in the library have four visual states on the shelf:

| State | Light | Physical mark | Touch response |
|---|---|---|---|
| Dormant | None — grey, muted | None | Micro-push (book shifts slightly and returns). Does not open. |
| Awakened (unread) | Golden shimmer, breathes softly | None | One tap → opens directly to first passage. |
| In-progress | Soft constant glow, no pulse, does not compete with awakened | None | One tap → opens, resumes where the child left off. |
| Completed | Warm constant glow, serene, no pulse | Small golden seal on spine (like a library stamp) | One tap → opens for re-reading. |

**Selection model:**
- One tap to open. No preview screen, no confirmation.
- No TTS in book selection — visual only. The child picks books by color, glow, and position.
- The golden seal on completed books is an object of the world — it could be a rune fragment,
  a crystal mark, or a library stamp. The exact symbol is art direction, not architecture.
  It must be recognizable at shelf scale (book spine is ~16×48 draw size).

**Dormant book feedback:** The micro-push is a 0.2 sec animation — the book shifts 2px toward
the child and springs back. No sound, no Owlorumo reaction. The child learns quickly:
books that glow respond, books that don't glow don't. The absence of response is the feedback.

> **Portadas / covers as collectibles:** BookPack `cover_image` is displayed when the book
> opens. Covers as Journal collectibles are a possible M2+ feature — not committed.

### Re-reading and End of Content

**Completed passages are available for re-reading.** A child who returns to a completed
book can re-read any passage. The passage displays with all target words in permanent
`found` state (gold glow). The crystal is visible but non-functional — passive pulse only,
no hint on tap. Tap-to-Hear remains active on all words. The page corner (pass page) is
available from the start — no Completion Beat replays.
 
The re-reading experience is a calm, already-illuminated passage. The child sees what
they accomplished and can listen to any word. No puzzle, no challenge, no feedback loop.
 
> **M2 review:** Testing may reveal that children benefit from re-playing puzzles on
> completed passages (spaced repetition). If so, a "replay puzzle" option can be added
> without changing the default re-reading behavior. The default remains read-only.


### PassageView — Unified Reading Surface — ✅ CLOSED

PassageView is a single continuous reading surface. There is no visible transition
between reading and puzzle. The child discovers the puzzle through touch.

**Background:** The library is visible but dimmed — shelves, window, warm light points —
all subdued. The parchment floats within this space. The child feels they are reading
inside the library, not in a separate screen.

**During reading (TTS active):**
The passage appears and TTS reads it automatically. No start button. All words are
tappable for Tap-to-Hear (unchanged). The crystal pulses softly in the bottom-right
corner — Owlorumo's presence, not a functional button.

**Puzzle activation (after TTS finishes first read):**
Target words shimmer briefly in gold (0.5 sec) — contextual instruction, not explicit
command. A subtle gold underline persists on targets. The child is never told "find
the words" — they discover that some words respond differently to touch.

> **TTS fallback:** When TTS is unavailable (device without voices, unsupported browser),
> the shimmer triggers after a configurable delay instead of waiting for TTS completion.
> Default: 3 seconds after passage text appears. The delay gives the child time to read
> silently before targets are revealed. The value is configurable in Settings (adult-facing)
> and stored in `settings.tts_fallback_delay_sec` in the save profile.
>
> The same fallback applies to Camino B if adopted: `_targets_active` becomes true
> after the delay instead of after TTS completion.

**During puzzle:**
- Tap a target word → gold glow fills the word, crystal micro-pulse. Word found.
- Tap a non-target word → Tap-to-Hear (TTS says the word, brief highlight).
- Tap the crystal → hint action on the text (same scaffolding as before).
- Tap the crystal during reading → subtle pulse, no function.

**No word bank. No counter. No separate puzzle panel.**
The only elements on screen are the passage text and the crystal.

**State machine:** `INTRO → ACTIVE → COMPLETE`.
INTRO: passage loading/appearing. ACTIVE: reading + puzzle coexist on one surface.
COMPLETE: Completion Beat in-place (already defined).

> **Targets active by default (Camino A).** All words respond to touch from the
> moment the text appears, including during TTS. If testing with real children shows
> "hunting without reading," switch to Camino B: targets respond only after TTS
> completes the first read. This is a single boolean change with zero architectural
> impact. Both paths share identical scene structure and layout.

> **Puzzle type exceptions remain.** WordGlow and Scramble operate on the visible
> passage (reading-visible). WordHunt, FillPassage, and RhymeFinder may use a
> separate search/support flow where appropriate — but even those types now use
> the same dimmed-library background rather than a separate screen.

> **WordGlow and Scramble exception:** Both puzzles operate during READING_STATE,
> not SEARCH_STATE. WordGlow requires the passage visible because the child taps
> words directly in the text. Scramble requires the passage visible because the
> child reconstructs a word in the context of the sentence it belongs to —
> removing that context turns spelling reconstruction into abstract memory work.
> All other puzzle types (WordHunt, FillPassage, RhymeFinder) operate in
> SEARCH_STATE as defined above.

### Tap-to-Hear — ✅ CLOSED

During READING_STATE, the child can tap any word in the passage and Owlorumo says it aloud via TTS.

**Rules:**
- Any word is tappable, not only target words. Target words are not visually distinguished during READING_STATE.
- TTS speaks the single word in the passage's language. No additional phrase, no sentence context.
- While Owlorumo is speaking a word, additional taps are ignored. No queue, no interruption, no cacophony. The tapped word may show a brief visual highlight (subtle underline, 0.5 sec) as acknowledgement even if TTS is busy.
- Not counted as a hint. Does not affect completion tier.
- Also available during re-reading of completed passages.
- Crystal micro-pulse (barely perceptible) when a word is spoken — reinforces the connection between reading and the crystal's life.

**Implementation:** `RichTextLabel` with `meta_clicked` signal. Each word wrapped in a meta tag. Guard: `if DisplayServer.tts_is_speaking(): return`.

**Milestone:** M1.


### Passage Transitions

**Between passages (Next →):** Page turn animation (0.5–0.8 sec). The parchment animates as if turning a physical page. Reinforces that the child is reading a book, not using an app.

**Return to Library:** Soft fade or book-closing animation. Different from page turn — this is leaving the book, not turning a page.

**M0 placeholder:** Direct cut (instantaneous). Page turn animation is M1 final polish.

### First-Run Flow — ✅ CLOSED

**Language selector → Library with single awakened BookPack → Owlorumo gesture on inactivity.**

On first launch (no profiles exist), the flow is:

1. **Language selector** — Two large buttons (EN / ES) with flag icons. No other UI. The selection sets `settings.language` in the new profile and is used for all TTS and locale resolution.

2. **Library appears** — The Sleeping Library in its initial state. One BookPack is pre-awakened (the onboarding pack, marked `is_onboarding: true` in its metadata). All other books are dormant and do not respond.

3. **Owlorumo invitation** — If the child does not interact within 10 seconds, Owlorumo looks toward the glowing book (gesture, no speech). If inactivity continues beyond 20 seconds, Owlorumo speaks a short TTS prompt adapted to `reading_stage` of the onboarding pack.

There is no tutorial overlay, no text instructions, no blocking modal. The invitation IS the book.

**Introductory scene (optional):** An optional narrative opening beat (crystal awakening, Owlorumo's first words) is accessible from the title screen as a standalone scene. It is not part of the main game flow — the child can always skip directly to the Library. This scene is M1 final scope and requires art + audio polish.

> **Reference:** Architecture Contract §3.1 (`is_onboarding` field), §5 (boot sequence).

### Profile Selection

The game supports multiple profiles with no hard limit — designed for classroom
lab deployment where each student needs their own profile on a shared device.

- Profile identification uses a written name — no avatar or color code.
  A first-grade child knows how to write their name; a teacher can assign
  conventions like `g1_1` (grade 1, class 1, student 1).
- Profile selection appears at launch **only when more than one profile exists**.
  A single-profile device loads directly — no selection screen friction.
- Adding a new profile is always visible and immediate from the selection screen.
  The "new profile" button is at the top of the list, never buried after a scroll.
- Partial progress is saved when exiting mid-passage. The child resumes exactly
  where they left off in the next session.

---

## 5. Puzzle Mechanics

### Puzzle Type 1: Word Glow (Ages 5–7, Difficulty 1/3)
**Core Mechanic:** The full passage is displayed on parchment within the dimmed library.
After TTS reads the passage, target words shimmer briefly in gold and retain a subtle
gold underline. The child taps a target word directly in the text to find it.

- All words are tappable. Non-targets trigger Tap-to-Hear. Targets glow gold when found.
- No word bank. No separate puzzle panel. The passage IS the puzzle surface.
- No time limit. No fail state — only encouragement.
- On success: the word illuminates with gold glow in place. Crystal micro-pulse.
- Hint: child taps the crystal (bottom-right corner). Crystal responds with resonance
  + hint action in the text (highlight area, read phoneme, etc.).

**Skill Reinforced:** Word recognition, sight words, left-to-right scanning.

---

### Puzzle Type 2: Letter Scramble (Ages 5–7, Difficulty 2/3)
**Core Mechanic:** A word from the passage is shown scrambled below the text. The player rearranges letter tiles to spell it correctly.

- The scrambled word tiles sit on a small "craft table" visual.
- A picture hint is available through Owlorumo support — limited uses per puzzle according to profile and difficulty.
- The corresponding word in the passage is blurred or hidden until solved.
- On success: the passage word "unblurs" with a satisfying pop effect.

**Skill Reinforced:** Letter ordering, spelling patterns, phonics.

> **PassageView layout:** TextZone shows the passage with the target word blurred.
> SupportZone (below text) holds the draggable letter tiles. Parchment adapts.

---

### Puzzle Type 3: Word Hunt Grid (Ages 6–9, Difficulty 2/3 to 3/3)
**Core Mechanic:** A word-search grid is generated from letters in the passage. Players find 5–10 hidden words in the grid.

- Words run left-to-right and top-to-bottom only for younger players (diagonal unlocks at difficulty 3).
- As each word is found in the grid, it highlights in the passage too — connecting the puzzle to the literary context.
- Word list is shown with small icons.

**Skill Reinforced:** Spelling, vocabulary, pattern recognition.

> **PassageView layout:** WordHunt takes over the full parchment. TextZone displays
> the letter grid instead of the passage text. SupportZone holds the word list.
> The passage is not visible during WordHunt — this is the only puzzle type where
> the pedagogical invariant (text hidden during search) applies.

---

### Puzzle Type 4: Fill the Passage (Ages 7–9, Difficulty 3/3)
**Core Mechanic:** A sentence from the passage is shown with 1–3 blanks. A small set of word tiles is offered. Player drags the correct word(s) into the blanks.

- Wrong placements shake and bounce back — no harsh failure sound.
- Correct placement causes the full sentence to "light up."
- Distractors (wrong word choices) are always plausible but wrong.

**Skill Reinforced:** Reading comprehension, vocabulary in context, grammar awareness.

> **PassageView layout:** TextZone shows the passage with blanks replacing target words.
> SupportZone holds the candidate word tiles for drag-and-drop into blanks.

---

### Puzzle Type 5: Rhyme Finder (Ages 4–7, Difficulty 2/3)
**Core Mechanic:** A word from the passage is highlighted. The player must find another word in the passage (or in a provided set) that rhymes with it.

- Rhyming pairs are chosen during book pack authoring.
- Audio support reads both words aloud for comparison.

**Skill Reinforced:** Phonemic awareness, rhyme recognition.

> **PassageView layout:** TextZone shows the passage with the source word highlighted.
> SupportZone holds rhyme candidates if they are not in the text itself.
> If candidates are in the text, SupportZone is collapsed — the child taps
> the rhyming word directly in the passage (similar to WordGlow interaction).

### Future: Composable puzzle parameters (M3)

Each puzzle type will declare an `allowed_config` schema:

```gdscript
# Future addition to PuzzleTypeConfig
"word_glow": {
    "scene": "res://scenes/Puzzles/WordGlow/WordGlow.tscn",
    "passage_visible": true,
    "passage_interactive": true,
    "uses_support_zone": false,
    "replaces_text_zone": false,
    "allowed_config": {
        "selection_order": {"type": "String", "values": ["any", "sequential"], "default": "any"},
        "distractor_words": {"type": "int", "min": 0, "max": 10, "default": 0},
        "hint_type": {"type": "String", "values": ["highlight_area", "read_phoneme", "show_first_letter"], "default": "highlight_area"},
        "reveal_mode": {"type": "String", "values": ["all_at_once", "one_by_one"], "default": "all_at_once"},
    }
}
```

BookPack modders write `auto_config` in their passage JSON. ModLoader validates
against the schema at pack-load time. IPuzzle reads validated parameters from
`definition.auto_config` in `initialize()`.

This is not implemented in M0–M2. The architecture supports it without changes
because `auto_config` already exists as a Dictionary field in PuzzleDefinition
and is already passed to IPuzzle. The only addition is the validation schema.

### Puzzle Type Extensibility — ✅ CLOSED (architecture)

Puzzle types are not hardcoded in PassageView. They are registered in a centralized
config that declares how each type interacts with the reading surface.

**Current (M0–M2):** Five built-in types. Adding a new type requires creating a scene
and adding one config entry. PassageView never changes — it reads behavior flags
from the config.

**M3 — Composable variants:** BookPack modders can configure existing puzzle types
through `auto_config` parameters in their passage JSON. A WordGlow with
`"selection_order": "sequential"` and `"hint_type": "read_phoneme"` feels like a
different puzzle without requiring new code. The engine validates parameters against
a schema per puzzle type. No executable code in mods — only JSON.

**Future — Curated puzzle authoring:** If community demand warrants, approved authors
can submit new puzzle types as signed bundles. These pass through review before
distribution. This is curated modding, not open modding. ModLoader only loads
signed puzzle types.

**Design principle:** At every level of extensibility, the same rules apply:
- The puzzle implements IPuzzle.
- PassageView mediates between text and puzzle via signals.
- The Owl never evaluates — it models.
- No puzzle type can introduce timers, fail states, or punitive feedback.
  These constraints are architectural, not advisory.

### Multiple Puzzles per Passage — ✅ CLOSED
 
A passage can contain more than one puzzle in its `puzzles` array. The puzzles execute
sequentially — the child completes the first, then the second, and so on.
 
**Flow:**
 
```
Passage appears → TTS reads → Shimmer (first puzzle targets) → Child solves puzzle 1
  → Intermediate Completion Beat (shorter: 1 sec resolve + Owlorumo response)
  → Parchment reconfigures for puzzle 2 (SupportZone changes, new shimmer)
  → Child solves puzzle 2
  → ... repeat for each puzzle ...
  → Final Completion Beat (full: resolve + Owlorumo + settling + page corner)
```
 
**Intermediate Completion Beat:** Same structure as the final beat but shorter. Resolve
(0.5 sec) + Owlorumo response (1 sec). No settling phase. No page corner. The parchment
transitions smoothly to the next puzzle — found words from puzzle 1 remain in `found`
state while puzzle 2 targets shimmer.
 
**Use case — classroom:** A teacher can author a passage with WordGlow first (word
recognition) followed by RhymeFinder (phonemic awareness) on the same text. The child
engages with the same passage from two different angles without leaving the reading
surface.
 
**Pergamino behavior between puzzles:** If puzzle 1 is WordGlow (no SupportZone) and
puzzle 2 is Scramble (uses SupportZone), the parchment adapts between puzzles. TextZone
may resize. The transition is a simple reconfiguration, not a scene change.
 
**State machine expansion:**
 
```
INTRO → ACTIVE_PUZZLE_1 → INTERMEDIATE_BEAT → ACTIVE_PUZZLE_2 → ... → COMPLETE
```
 
PassageView tracks `_current_puzzle_index` and advances through the array.
 
**Single puzzle remains the common case.** Most passages have one puzzle. The multi-puzzle
flow is opt-in per passage, not a new default. A passage with `"puzzles": [single_puzzle]`
behaves exactly as designed — no intermediate beat, no reconfiguration.

#### WordGlow — UI behavior details

**Tile found behavior:**

**Target progress is visible in the text itself.** Found words retain their gold glow
permanently in the passage. The child sees their progress directly in the reading —
the passage gradually illuminates as they find more words. No external counter, no
word bank, no slot system.

> **Display profile exception (future M2+):** The conservative display profile may
> optionally show anonymous slot indicators below the passage for children who need
> explicit progress cues. This is not part of the standard or advanced profiles.

**Anonymous slots:**
Slots communicate "something belongs here" before any word arrives.
Visual: grey `#9E9E9E` at 60% opacity. No label, no animation in rest state.
The count of slots equals the count of target words — the child knows
how many words to find without being told which ones.

**Hint behavior — Crystal as hint access:**
There is no separate hint button. The child taps the crystal (Owlorumo's presence
in PassageView) directly. The crystal is pixel art (12×12 native, 48×48 display at 4×),
positioned in the bottom-right corner with a 64×64 tap target.

| Situation | Behavior |
|---|---|
| Hints available | `owl_hint` — staff points toward puzzle, crystal bright |
| Hints exhausted | Repeats previous hints in cyclic order — never silence |
| No hints given yet, inactivity | Accompaniment gesture — looks at child, crystal soft pulse |
| Inactivity auto-trigger | Same accompaniment, initiated by system |

Owlorumo never expresses frustration or abandonment.
When hints are exhausted, he repeats what he already shared — he does not refuse.

**Fragments of light — immediate completion feedback:**
Puzzle completion sends fragments of white-gold light flying to Owlorumo's
staff crystal.

| Result | Fragments |
|---|---|
| Completed without hints | 3 fragments — crystal intense pulse |
| Completed with 1 hint | 2 fragments — crystal moderate pulse |
| Completed with 2+ hints | 1 fragment — crystal soft pulse |

Fragments are immediate feedback — fugitive flashes absorbed by the crystal.
They are visually distinct from the crystal's permanent state base level.
Permanent progression belongs to book and arc milestones, not individual puzzles.

### Completion Beat — In-Place Transformation — ✅ CLOSED

Puzzle completion transforms PassageView in place. There is no detached reward screen.

**Timeline:**

1. **Resolve (0–1 sec):** Last word found. Fragments of light fly from found words to Owlorumo's crystal. `sfx_puzzle_complete` + `sfx_fragment_arrival`.
2. **Owlorumo responds (1–3 sec):** Eyes closed, slight smile. TTS phrase adapted to `reading_stage`. Crystal pulses per completion tier.
3. **Settling (3–5 sec):** Owlorumo returns to idle. Found words remain highlighted in the passage with a soft permanent glow.
4. **Child's moment (5+ sec):** The bottom-right corner of the parchment lifts subtly,
   inviting a page turn. Appears after 1 second delay + 0.5 second fade-in.
   The child taps the lifted corner to advance. Page turn animation (0.5–0.8 sec).
   
   The corner is diegetic — the child is turning a page in a book, not pressing a button.
   Tap target: 96×96 minimum. Asset: pixel art page corner, 16×16 native.
   
   **Last passage of a book:** The page corner does not appear. The transition back to
   the Library triggers after the Completion Beat via the standard reverse transition
   (parchment fade-out → overlay clears → library returns).
**Last passage of a book — slightly more intense:**

- Crystal flash breve. Owlorumo's eyes gain soft glow.
- TTS phrase about the book, not the word: adapted to `reading_stage`.
- "Next →" returns to the Library, not to another passage.
- A subtle pulse of warm light crosses the screen — something elsewhere responded.
- No confetti. No score. No "Book Complete!" banner.

**What the completion beat never does:**

- Show score, points, visible stars, or percentages
- Compare with previous attempts
- Say "Perfect!" or "You can do better!"
- Block the child with a mandatory animation
- Auto-advance on a timer

### Owlorumo Reaction States — Revised — ✅ CLOSED

| Moment | Owlorumo response | What changes |
|---|---|---|
| Puzzle completed (normal) | Eyes closed, slight smile. Quiet satisfaction. | Facial expression only. Crystal does its normal fragment pulse. |
| Last passage of a book | Eyes open with soft glow. Crystal flash. Looks at the child. | Eyes illuminate. It is something that *happens to him*, not an action he takes. |
| `celebrate` (2–3 times in the entire game) | Eyes glow sustained. Crystal stays lit, not pulsing. Looks at the child without looking away. Silence. | No physical gesture. The celebration is total presence. The most powerful moment has the least movement. |

`celebrate` is reserved for: crystal ignition (state_0 → state_2), completing a full arc, state_4 transition. It occurs 2–3 times per save file.

### Owlorumo Behavior Controller — ✅ CLOSED (architecture)

Owlorumo can receive multiple triggers simultaneously (puzzle completion + resonance +
Hidden Book). His gestures are managed by a priority queue.

**Queue rules:**
- One gesture at a time. Next begins when previous completes.
- 0.5 sec pause between consecutive gestures.
- The queue pauses when the child interacts (opens a book, taps a word).
  Interrupted gestures are NOT discarded — they remain in the queue and
  resume when Owlorumo returns to idle.
- `owl_signaled` is marked `true` only when a gesture **completes**, not when it enters the queue.

**Priority order:**

| Priority | Gesture | Category |
|---|---|---|
| 1 (highest) | Completion Beat / celebrate | Uninterruptible |
| 2 | Crystal ignition (state change) | Uninterruptible |
| 3 | Hidden Book appears | Interruptible — pause and retry |
| 4 | Resonance new | Interruptible — pause and retry |
| 5 (lowest) | Idle / ambient activity | Interruptible — always yields |

**Uninterruptible gestures — input is absorbed, not processed:**

| Gesture | Max duration | Occurrence |
|---|---|---|
| Crystal ignition | 3 sec | Once per save file |
| `celebrate` | 4 sec | 2–3 times per save file |
| Completion Beat (resolve + response) | 2 sec | Every puzzle completed |

During uninterruptible gestures, the child can touch anything — nothing responds
until the gesture completes. This is not a UI freeze; the touch simply has no effect.
Maximum absolute duration in the system: 4 seconds (`celebrate`).

**Interruptible gestures:** If the child interacts mid-gesture, the gesture stops cleanly,
is NOT marked as signaled, and returns to the front of the queue for the next idle opportunity.

> **Artist note:** "Draw Owlorumo as if he just remembered who he is."

### Library Resonances — ✅ CLOSED (architecture)

The library contains resonance points — visual elements that change state as the
child accumulates reading. Resonances are never announced. The child discovers them
by returning to the library and noticing that something is different.

**Trigger types:**
- **Accumulation:** activated when ProgressManager crosses internal milestones
  (passages completed, books completed, `owlorumo_state`, hidden books read).
- **Content-specific:** activated when a specific book is completed. The trigger
  is defined by the engine/theme, not by the BookPack — the BookPack does not know
  it activates anything.

**Owlorumo's role:** The first time a resonance awakens and the child returns to
the library, Owlorumo reacts once — a glance toward the change, a different crystal
pulse, a moment of stillness. This is his only signal. He does not name or explain
the change. After the first signal, the resonance simply exists.

**Resonance points are defined by the theme, not by content.** A BookPack never
declares, references, or activates a resonance. The engine evaluates milestones
and the theme defines what visual changes correspond to each threshold. This
preserves P1: content is data, not code.

**Examples** (illustrative, not committed — exact points defined later):

| Point | Dormant | Awakened | Possible trigger |
|---|---|---|---|
| Window | Rain, fogged glass | Starry sky, moonlight enters | books_completed ≥ 3 |
| Wall clock | Stopped | Pendulum swings, hands move | passages_completed ≥ 15 |
| Candelabra | One candle lit | All candles lit, warm light | owlorumo_state ≥ 2 |
| Distant shelf | Grey, dusty | Spines show color, one glows | hidden_books_read ≥ 1 |
| Ink well on table | Dry | Fresh ink, quill resting | books_completed ≥ 5 |

**Milestone:** Architecture defined now. Schema in save at M1 technical. 1–2 visible
resonances at M1 final. Full system at M2+.

### Silent Consequences — Design Directive — ✅ CLOSED

**Rule:** No change in the library produced by the child's reading is announced with
UI, pop-up, notification, achievement sound, or explanatory text. The change exists.
If the child notices, it is theirs. If not, it waits.

**Owlorumo first-time signal:** The single exception. The first time the child returns
to the library after a new change, Owlorumo reacts once with a corporeal gesture —
glance, crystal pulse, stillness. Never speech. Never text. After that one signal,
the change is simply part of the world.

**This rule applies to:** resonance awakenings, Hidden Book appearances, Hidden Book
withdrawals, library state name transitions (Sleeping → Reawakened → Beginnings),
and any future ambient change.

**This rule does NOT apply to:** Completion Beat in PassageView (which is immediate
puzzle feedback, not a library change).


#### Hidden Books — Archaeology Principles — ✅ CLOSED

**Fixed positions.** Each Hidden Book appears at a specific, memorable location in
the library (shelf, row, slot). The position is not random. A Hidden Book that
withdraws and later reappears may return to the same position or a different one,
but always to a defined slot — never scattered arbitrarily. The child can remember
where they found something.

**Residue.** When a Hidden Book withdraws, its position retains a subtle visual
trace — a space slightly cleaner than the surrounding dust, a faint mark in the
wood, a texture difference only visible to someone who looks. The residue is
permanent: once a Hidden Book occupied a place, that place remembers. This
transforms the library into a space with visible memory.

**Seed fragments.** `owlorumo_memory` is the canonical fragment kind for content
that opens narrative questions beyond Readcraftery. These fragments may contain
names Owlorumo does not recognize, references to places that are not this library,
or images that suggest a larger world. The child of 6 reads a beautiful story.
The child of 9 senses there is more. A future project answers.

Seed fragments are authored content, not a technical feature. No special engine
support is needed — only a design directive that `owlorumo_memory` content is
written with deliberate unanswered questions.

---

### Puzzle Difficulty Scaling

| Player Age Profile | Default Puzzle Types | Word Length | Time Limit | Hint Uses |
|---|---|---|---|---|
| 4–5 years | Rhyme Finder | 2–4 letters | None | Unlimited |
| 5–6 years | Word Glow, Letter Scramble | 3–5 letters | None | 3 per puzzle |
| 6–7 years | Scramble, Word Hunt | 3–6 letters | Optional | 2 per puzzle |
| 7–9 years | Word Hunt, Fill Passage | 4–8 letters | Optional | 1 per puzzle |

The difficulty profile is set during onboarding and can be changed by a parent/teacher at any time.

---

## 6. Literary Integration System

### Book Structure
Each book in READCRAFTERY is composed of:

```
Book Pack
├── metadata.json        ← Title, author, age range, language, cover art ref
├── cover.png            ← Cover art (512x512 recommended)
├── passages/
│   ├── passage_01.json  ← Text, illustration ref, puzzle definitions
│   ├── passage_02.json
│   └── ...
├── audio/               ← Optional: pre-recorded read-aloud .ogg files
│   ├── passage_01_en.ogg
│   └── passage_01_es.ogg
└── illustrations/       ← Optional: passage art
    └── passage_01.png
```

### Passage JSON Format (example)
```json
{
  "id": "passage_01",
  "title": "The Brave Little Seed",
  "text": "Once upon a time, a tiny seed fell from a great oak tree. The wind carried it far across the green meadow.",
  "language": "en",
  "difficulty": 1,
  "illustration": "passage_01.png",
  "audio": "passage_01_en.ogg",
  "puzzles": [
    {
      "type": "word_glow",
      "targets": ["seed", "wind", "tree", "green"]
    },
    {
      "type": "word_hunt",
      "targets": "auto",
      "auto_config": {
        "word_count": 6,
        "min_length": 3,
        "max_length": 7,
        "pos_filter": ["noun", "verb"]
      }
    },
    {
      "type": "scramble",
      "targets": ["meadow", "carried"]
    }
  ],
  "comprehension_question": {
    "text": "Where did the wind carry the seed?",
    "options": ["A forest", "A green meadow", "A big city"],
    "correct": 1
  }
}
```

> **Auto-generation rule:** When `targets` is the string `"auto"`, `PuzzleGenerator` runs at pack-load time and populates the targets array before any `IPuzzle` scene receives the `PuzzleDefinition`. The puzzle scene never distinguishes between hand-authored and auto-generated targets. Completion feedback and restoration behavior are identical in both cases.
>
> **Auto-generation algorithm (v1 — rule-based, no NLP dependency):**
> 1. Tokenize passage text → word list
> 2. Lowercase + strip punctuation
> 3. Remove stopwords (see Stopwords Bundle below)
> 4. Filter by `min_length` / `max_length`
> 5. Deduplicate
> 6. Sort by ascending frequency (rarer words = higher educational value)
> 7. Take top `word_count` words
> 8. *(M1)* Filter out tokens containing uppercase letters → removes proper nouns without NLP
> 9. *(M1)* Filter out tokens containing apostrophes or hyphens → reduces complexity for early readers
> 10. *(M2)* Optional: enforce `sight_words_ratio` (0.0–1.0, default 0.0) — if set, ensures at least that fraction of targets come from the bundled sight words list. Disabled by default; teacher-configurable via `auto_config`. Not hardcoded to avoid imposing a specific pedagogical methodology (Dolch vs Fry vs SNSWL, etc.)
>
> **Stopwords Bundle (categorized format):**
> ```json
> {
>   "always_exclude": ["a", "an", "the", "of", "in", "on", "at"],
>   "exclude_age_4_6": ["because", "although", "nevertheless", "through"],
>   "exclude_age_6_9": [],
>   "pedagogical_override": ["the", "and", "is"]
> }
> ```
> `pedagogical_override` words are excluded by default but can be re-included by a teacher setting `"include_pedagogical_overrides": true` in `auto_config`. Rationale: "the" and "and" are critical sight words for ESL learners even though they are stopwords in standard NLP contexts.
> Stopword lists (`stopwords_en.json`, `stopwords_es.json`) are bundled with the engine and versioned in the repo. Community PRs accepted. Book packs may add per-pack overrides via `metadata.json → stopword_overrides[]` without modifying the base lists.
>
> **Internal flag:** Auto-generated puzzles set `"auto_generated": true` in the save record for that puzzle instance. This is never surfaced to the player but allows debugging of generator quality from teacher/parent reports.

### Built-in Book Library (Launch Content)
| Book | Age Range | Language | Source |
|---|---|---|---|
| *The Little Seed* (original) | 4–6 | EN, ES | Original content |
| *Adventures of Pip the Puppy* (original) | 5–7 | EN, ES | Original content |
| *Aesop's Fables — Selections* | 6–9 | EN, ES | Public domain (Project Gutenberg 1909 ed.) |
| *Simple Science Stories* (original) | 6–8 | EN, ES | Original content |
| *Fairy Tales for Early Readers* | 5–8 | EN, ES | PD source text rewritten by author |

> **Content Licensing Policy:** "Public domain adaptations" is a risk category and must not appear in shipped content. The only safe options are: (a) original text authored by the dev, (b) PD text used verbatim from a verified pre-1928 edition (Project Gutenberg preferred), or (c) PD source text fully rewritten by the dev (new copyright). Specific-edition translations post-1928 and 3rd-party illustrations are presumed copyrighted. A `CONTENT_LICENSING.md` table (text source, illustration source, license status per asset) must be committed to the repo before M3 beta launch. This is not required for internal development milestones but is a hard prerequisite for any public distribution.

---

## 7. Progression & Reward Systems

### Fragments of Light — Immediate Completion Feedback

Puzzle completion sends fragments of white-gold light to Owlorumo's staff crystal.
Every completion signal is narratively connected to the restoration of Owlorumo's presence.

| Result | Fragments | Crystal response |
|---|---|---|
| Completed without hints | 3 | Intense pulse |
| Completed with 1 hint | 2 | Moderate pulse |
| Completed with 2+ hints | 1 | Soft pulse |

Fragments are immediate visual feedback — they fly, arrive, and are absorbed.
They do not accumulate visibly and they do not operate as a visible currency.
The crystal's permanent brightness is determined by `owlorumo_state`,
book milestones, and arc milestones.

### Book Awakening — Restoration Milestones

Dormant books awaken through restoration milestones, not through visible numeric accumulation.

- The child never sees a number or a progress bar toward awakening
- Owlorumo does not announce when a book awakens
- The child notices a new book on the shelf — or does not
- Some dormant books are visible from game start
- Others appear silently when the child returns to the library
  after completing a passage — as if someone placed them there

There is no lock icon. A dormant book simply does not respond.
An awakened book breathes softly and invites.

### The Library — Revealed Names by Restoration State

The library is the same place throughout the game, but its deeper name is revealed
through restoration.

**State names (canonical):**
- **The Sleeping Library** — the child first discovers the place as dormant, veiled, and waiting
- **The Reawakened Library** — after meaningful restoration milestones, the place begins to answer again
- **The Library of Beginnings** — the deeper truth of the place; restoration does not return it to a pristine past, but opens new continuity and new doors

These are not UI “levels” or numeric labels.
They are narrative names for the same living library-world as it becomes more present.

Words such as **forgotten** or **lost** may be used in prose or narration to evoke the child's discovery,
but they are not the canonical state names.

### The Reading Owl Companion
The player's owl companion is named **Owlorumo**. The name is fixed — it is part of the character's identity, not assigned by the player.

Owlorumo changes through restoration, not through gamified reward layers.
His main progression is expressed through the staff crystal, eyes, presence, and the library's response.
Later milestones may unlock carefully chosen accessories or theme-specific visual accents,
but themes do not rename him and do not replace his core identity.

### Owl feedback protocol — ✅ CLOSED

The Owl is the most important pedagogical element of the game.
Its behavior in response to errors determines whether the child
keeps trying or develops a negative identity as a reader.

**Core rule: the Owl never evaluates — it models.**

#### When the child does not interact for more than 8 seconds:
- The Owl enters `thinking` state
- After 5 additional seconds: the Owl reads the target word aloud
  and syllabifies it slowly (TTS with pause between syllables)
- The hint is offered without the child having to ask for it
- Not recorded as "hint used" if triggered automatically by inactivity

#### When the child selects an incorrect word:
- No red X. No error sound.
- The Owl reads the selected word aloud (TTS)
- 1 second pause
- The Owl reads the target word aloud
- The incorrect tile returns to its position with no failure animation
- The attempt counter is not visible to the child

#### When the child finds a correct word:
- Immediate positive feedback — the Owl enters `happy`
- The word is highlighted in the passage
- TTS reads the word and uses it in a short sentence (M1)

#### What the Owl never does:
- Show an error counter
- Express impatience or frustration
- Interrupt the child while they are attempting
- Celebrate in a way that exposes the child in front of others

#### Automatic vs manual hints:
- **Automatic** (inactivity > 13 seconds): does not deduct from `hint_count`
- **Manual** (child presses Owlorumo for help): deducts from `hint_count`
- Default `hint_count` is set by profile and puzzle difficulty; it is not globally fixed

### Owlorumo — adaptive language — ✅ CLOSED

Owlorumo speaks. The complexity of his speech adapts to the `reading_stage` of the active book pack.

| `reading_stage` | Example phrase | Speech style |
|---|---|---|
| `early_emergent` (ages 5–6) | *"That one!"* / *"Yes!"* / magic sound | Single words or exclamations. TTS-driven. |
| `developing` (ages 7–9) | *"You found 'seed'!"* | Short, complete sentence. Positive. |
| `fluent` (ages 9+) | *"'Seed' comes from 'to sow'. Well done!"* | Word origin or usage. One extra fact. |

**Implementation:** Owlorumo's lines are strings defined per `reading_stage` in the book pack's locale file or in the base `en.json` / `es.json`. The engine selects the appropriate string set at pack load time via `LocaleManager`.

**Rules:**
- Owlorumo never comments on errors — only on correct actions and on hints (see feedback protocol above)
- Speech lines are never longer than one sentence at any level
- The `early_emergent` level may replace speech with a short TTS sound effect and an animation — no words required
- All Owlorumo speech goes through TTS — never pre-recorded (ensures voice consistency across languages)

### The Story of Owlorumo — ✅ CLOSED

Owlorumo is both companion and ancient guardian. He was the owl companion of Athena, and he remains in the library — the last place where wisdom, books, and remembered knowledge survived. But his identity, power, and purpose are veiled by a soft mist. He does not fully remember what he was meant to protect or restore. He only senses that something important has grown dim and must not be lost.

The child does not know this. Owlorumo does not explain it.

The staff crystal is not generic magic. It is collective human wisdom made light. As reading returns, that light returns. Owlorumo's eyes are part of the same logic: they are his connection to vision, insight, and what Athena once entrusted to him. The library is not decorative background; it is the final refuge where wisdom endured long enough to be reawakened.

The child restores this without knowing it directly. Each recognized word or pattern creates a local response, but the deeper restoration is tied to reading progress — passages completed, books finished, arcs fulfilled, and restoration milestones reached. Reading helps reconnect fragments of living human knowledge.

That is the thesis inside the title:
**Reading is a power that discovers and restores human knowledge.**

> This story is never told explicitly in the game.
> It lives in visual details, in Owlorumo's phrases,
> in the progression of his staff crystal, eyes, and presence,
> and in the awakening of the library itself.
> A 5-year-old sees a wizard owl getting brighter.
> A 9-year-old feels they are helping someone who needs them.
> An attentive adult understands that reading matters because it restores what a culture might otherwise lose.

---

### Owlorumo — Companion Progression — ✅ CLOSED

Owlorumo does not start complete. He starts diminished.
Restoration is progressive, warm, and never announced as a system reward.

#### Visual progression states

| State | Staff / Crystal | Clothing / Presence | Eyes | Unlocked after |
|---|---|---|---|---|
| `state_0` | Staff slightly dry, light cracking; crystal dark | Navy form, diminished presence | Normal | Game start |
| `state_1` | Cracks gone or reduced; faint crystal glow | Same design, slightly steadier material read | Normal | First passage milestone |
| `state_2` | Crystal lit and softly pulsing | Same silhouette; more life in material and light | Occasional soft glint | First book |
| `state_3` | Crystal bright and warm; staff reads stronger and more alive | Presence fuller, library increasingly responsive | Occasional soft glow | 3 books |
| `state_4` | Powerful white-gold crystal; staff fully alive but still organic | White-and-gold restoration with visible continuity: blue mantle remains, no full redesign | Constant soft living glow | First complete arc / late-game goal |

**Identity anchors that do not change:**
- moon brooch
- belt
- boots
- organic staff form

`state_4` is not a replacement design. It is a fulfilled form with the journey still visible in it. The white-and-gold restoration is carried by light, material, and presence — not by a radical costume swap.

#### Rules

- Progression is primarily expressed through **staff + crystal**, then eyes, then library response
- Major restoration happens at reading milestones — not on every isolated word
- Local correct interactions can trigger micro-feedback without causing a full restoration beat
- Changes are discovered, not announced
- Restoration does not return everything to a pristine original state; it opens a living continuity

#### The first crystal ignition moment

When the crystal lights fully for the first time, Owlorumo does not celebrate the child. He looks at them.
Two seconds of silence.
The child understands — without anyone explaining — that they did this.

This is the most important moment in the game.

### Display Profile System — ✅ CLOSED

The display profile controls how content is presented to a specific child.
It is separate from the book pack's `reading_stage` — it adapts to
the individual child's demonstrated ability, not their age.

#### Three levels — forward only
```
conservative → standard → advanced
```

| Display profile | Text visible | Visual focus | Glow radius | Slots |
|---|---|---|---|---|
| `conservative` | Full passage | Relevant sentence highlighted (warm bg or rest at 70% opacity) | Full | Optional anonymous (M2+) |
| `standard` | Full passage | None — uniform presentation | Reduced | Optional anonymous (M2+) |
| `advanced` | Full passage | None | Disabled | None |

> **M2 testing note:** The conservative highlight behavior (Option B) is provisional.
> Real testing with early emergent readers (5–6 years) may reveal that full-passage
> display with highlight is insufficient for reducing cognitive load. Alternative
> approaches (sentence isolation, enlarged font, progressive reveal) are reserved
> for M2 evaluation. The architecture supports changing conservative's visual
> behavior without affecting the profile system, save schema, or advancement rules.
>
> For early_emergent passages (1–2 sentences), conservative and standard produce
> nearly identical results — the distinction matters primarily for developing-stage
> passages with 3+ sentences.

#### Conditions to advance — all three must be met

- **Autonomy:** N consecutive puzzles without hints, max glow, or prolonged inactivity
- **Consistency:** both signals sustained across a full book, not a single passage

> **Design note:** Speed is intentionally excluded as a metric.
> A child decoding phonologically reads more slowly than one pattern-matching —
> rewarding speed would penalize the children who are actually reading.
> Autonomy and consistency are the only pedagogically valid signals of mastery.

#### Application rules

- Change occurs only at the start of the next book — never between passages
- Owlorumo celebrates the new book with `owl_excited` + phrase adapted to `reading_stage`
- The phrase never mentions "level" — it only celebrates the new book
- **The profile never goes down**
- When a child struggles, support increases silently:
  more automatic hints, more frequent glow — display profile unchanged

#### Owlorumo's phrase on profile advance

| `reading_stage` | Phrase |
|---|---|
| `early_emergent` | *"Look! More words!"* |
| `developing` | *"This book has more story!"* |
| `fluent` | *"This one looks interesting..."* |

---

### Celebration — ✅ CLOSED

The Celebration is not a separate screen. It is a **transformation
of the current screen** — the world reacts to the child's achievement
without removing them from the world.


#### The Discovery word (Profile C / advanced)

GameManager already knows the next passage before Celebration loads.
The first target word of the next passage appears briefly in the
staff crystal — glowing, then fading. No label, no explanation.
Just a word. The child who sees it and finds it in the next passage
experiences a moment of recognition that belongs entirely to them.

---

### Onboarding — ✅ CLOSED

#### Design principle

Gandalf does not talk to Bilbo about dragons or rings on their first meeting.
They talk about the meaning of "good morning."

The Onboarding does not start with "Welcome to ReadCraftery, here you
will learn to read." It starts with something small, apparently
unimportant — and in that unimportant moment, everything is contained.

#### The opening scene

The child arrives at the library. It is dim. Owlorumo is at his lectern,
crystal almost dark, reading — or trying to. He does not look at the
child immediately.

After a moment, he looks up. And says:

> *"This word... do you see it?"*

He points — not with urgency, with curiosity.
The passage is open. One word glows faintly.

Pause.

> *"Ah. Yes. That one."*

#### What happens next

Owlorumo does not ask the child for help. He shows them a page.
One sentence. And says:

> *"This word... do you see it?"*

The child touches the word. The crystal pulses — faintly, like a weak heartbeat.

Owlorumo looks at it. He does not say "well done!" He says:

> *"Ah. Yes. That one."*

As if he just remembered something he had forgotten long ago.

#### Why this works

The child learned to tap a word. But they do not know it —
they only helped Owlorumo remember something.
The tutorial happened inside the narrative, not on top of it.

#### Technical note

The Onboarding is a special `BookPack` with `id: "onboarding"`.
It uses the same PassageView + WordGlow pipeline.
The only difference is that `GameManager` loads it before any
other book on first run, and Owlorumo starts in `state_0`.
No special scene, no special code path.

### The Reading Journal — ✅ CLOSED

The Journal is the child's personal space inside the library. If the Library is Owlorumo's place, the Journal is the child's. It is where the child keeps things they want to remember — not things the system decides to show them.

**Physical presence:** A small book in the Library scene near Owlorumo. The child's `display_name` is on the cover. Always visible. Tap to open.

**Visual tone:** Parchment (#F5E6C8) pages. The Journal is an object of the world, not a UI screen. Pages are turned with swipe or buttons.

#### Page 1: My Words

Words the child chose to save. Not all words found — only those the child decided matter.

Each saved word shows:
- The word itself
- Which book it comes from
- A TTS button to hear it again

No definitions, no translations, no phonetic classification. This is a personal album, not a dictionary.

**How words are saved:** After puzzle completion, found words glow in the passage. The child can tap any found word. A small "save" icon appears (open book). If tapped, the word is saved to the Journal with subtle feedback. If not tapped, nothing happens. Not obligatory. Not blocking.

#### Page 2+: My Books

A personal bookshelf — smaller and more intimate than the Library. Only completed books appear. Each can be opened for re-reading. No progress bars, no percentages, no counters.

#### Page 3+: Stickers

A grid of earned stickers. Two sources:
- **Book souvenirs** (`source: "book"`) — declared by BookPack authors in `metadata.json`. Earned on book completion.
- **Library milestones** (`source: "library"`) — earned through restoration milestones (see Library Milestone Stickers table above).

Both follow the sticker contract: objects that could exist inside an ancient library.

#### What the Journal does NOT contain

- Achievement badges with numeric triggers
- Percentages of anything
- Counters of anything
- Rankings of anything
- Anything that tells the child "you need X more to get Y"

**Milestone:** M2. Save schema reserved now. BookPack sticker field reserved now.

> **Save schema:** See Architecture Contract §3.4 — `journal.saved_words` (Array[Dictionary]) and `journal.stickers` (Array[Dictionary]).

### Library Milestone Stickers — ✅ CLOSED

Milestones are not badges, trophies, or score indicators. They are objects that could exist inside an ancient library — discovered, not awarded. They appear in the Journal without announcement.

| Sticker | Trigger | Visual identity |
|---|---|---|
| First Light | First word found in the entire game | A tiny crystal fragment |
| The First Book | First book completed | A dry leaf between the pages |
| Crystal Awakening | Crystal ignition (state_0 → state_2) | An illuminated rune |
| The Library Answers | Transition to Reawakened state | An ancient ink mark that wasn't there before |
| A Memory Returns | First Hidden Book discovered | An owl feather |
| New Continuity | First book read in a second language | A wax seal with two moons |

**Extensibility:** Future engine versions may add milestones. BookPack authors may declare book-specific souvenir stickers in `metadata.json`. All stickers must follow the sticker contract (see below).

**Sticker contract:** A sticker is an object that could exist inside an ancient library. It is never a badge, a trophy, a medal, or a score indicator. It does not display numbers, percentages, or rankings. It is discovered, not awarded. Modders who declare stickers in their BookPack must follow this rule.

> **Save schema:** Stickers are stored in `journal.stickers` as `Array[Dictionary]`. See Architecture Contract §3.4.


###  — BookPack Theme Family

🔴 INTENT — do not implement until closed.

Each BookPack may declare a `theme_family` that drives coherent
visual and symbolic feedback during gameplay.

Example values: `ocean`, `forest`, `sky`, `ancient`, `urban`

When declared, the engine uses `theme_family` to select:
- fragment light color palette (currently always white-gold)
- particle variant for celebration and restoration moments
- rune variant family for Owlorumo's mantle progression

The modder declares the family. The engine resolves the assets.
No semantic analysis required — this is a creative declaration, not computation.

Status: 🔴 INTENT — schema, asset pipeline, and fallback behavior not specified.
Earliest milestone: M2.

### Engagement Strategy

Readcraftery's retention mechanism is narrative restoration, not mechanical variety. The child returns because the library responds to reading as a real force — not because of points, leaderboards, or unlockable cosmetics.

To support this:

1. **BookPacks should vary puzzle types across passages.** A book with 5 passages should not use WordGlow for all 5. Mixing WordGlow, Scramble, and RhymeFinder across passages prevents mechanical fatigue and keeps the child uncertain about what comes next.

2. **Owlorumo's response phrases must have variety.** Minimum 5 variants per event per `reading_stage`. A child who hears "You found 'seed'!" three times in a row stops hearing it. Variants are content in locale files, not code.

3. **Completed books remain visible as living objects.** The book on the shelf — glowing, breathing, with its own spine color — is the reward. The child collects read books. Not badges. Books.

4. **The Journal (M2) provides a space of ownership.** Stickers, saved words, a personal space the child fills. This is Readcraftery's answer to avatar customization without betraying the literary tone.



---

## 8. Visual Effects & Feedback

### Design Philosophy
For ages 4–9, feedback must be **immediate (< 200ms)**, **visually clear**, and **emotionally warm**. Avoid red X marks or harsh failure indicators. Use redirection and encouragement instead.

### Success Effects (Word Found)
- **Sparkle Burst:** The found word emits a burst of colored sparkles matching the book's color palette.
- **Word Flight:** The word physically lifts from the passage and floats into its word bank slot.
- **Letter Pop:** Each correct letter tile bounces in sequence with a soft pop sound.
- **Fragment Flight:** On puzzle complete, 1–3 white-gold fragments of light arc toward Owlorumo's crystal with a gentle chime.
- **Owlorumo Reaction:** Owlorumo answers with a brief warm reaction tied to the moment — never a comic dance, never a game-show mascot beat.

### Encouragement Effects (Wrong Attempt)
- **Gentle Wobble:** Wrong answer tiles wobble and return to position. No harsh sound.
- **Owl Hint Nudge:** The owl tilts its head and blinks as if curious — subtly guiding without criticizing.
- **Soft Glow Fade:** Attempted letters briefly glow amber then fade, suggesting "almost."

### Passage Completion Transformation
The current scene reacts without cutting away to a detached reward screen.

- Confetti is optional and theme-safe only if it does not compete with reading clarity
- Fragments of light animate toward Owlorumo's crystal
- Owlorumo performs a warm, brief reaction tied to the book tone
- A new sticker or journal update may appear if that book milestone grants one

### Effect Variety System
To prevent repetition fatigue, celebrate effects are drawn from a randomized pool per session:

- 5 sparkle color palettes per book theme
- 3 owl celebration animations
- 4 ambient celebratory particle patterns
- Effects escalate in intensity for streaks (3 in a row correct = bigger burst)


> ** Design note: Pedagogical Failure Handling **
> 
> Pedagogical Failure Handling
> 
> Comprehension errors should never be treated as punishment.
> 
> If the player selects an incorrect answer:
> 
> The Owl responds with encouragement, for example:
> "Let's read it again to find the answer."
> 
> The story is replayed or briefly shown again,
> allowing the learner to re-engage with the text.
> 
> This approach reinforces comprehension through repetition
> instead of negative feedback.

---

## 9. UI/UX Design

### Core Design Principles for Ages 4–9
- **Large tap targets** — minimum 48x48dp on mobile, 60x60px on PC
- **High contrast** — WCAG AA minimum for all text
- **No reading required to navigate** — all menu buttons have icons + audio labels
- **Single-finger operation** on mobile — no complex gestures
- **Always-visible back/home** — no dead ends

### Screen Layouts

#### Main Library Screen
- Warm illustrated library room (isometric or flat 2D)
- Bookshelves with inviting readable books and quiet dormant books
- Owl companion seated or animated in corner
- Top bar: player name, settings icon, and optional teacher-facing progress summary when relevant
- Large, friendly "PLAY" or "READ" button for youngest players

#### Passage View Screen
- Primary reading area: Book passage in large, readable font. The passage remains visually central.
- Secondary support area: Puzzle support UI (target card / tiles / blanks depending on puzzle type)
- WordGlow rule: the child resolves WordGlow in the passage itself; support UI remains informative
- Bottom / support area: target inventory, Owlorumo hint access, audio replay button
- Top: Book title, passage number, exit to library

#### Responsive Breakpoints
| Device | Layout |
|---|---|
| Mobile portrait (phones) | Stacked: passage on top, support/puzzle area below; no swipe-only navigation required |
| Tablet / iPad | Side-by-side (passage left, puzzle right) |
| PC / Web 1080p | Full side-by-side with decorative book frame |
| Web 720p | Condensed side-by-side |

### Diegetic UI — The World as Interface

READCRAFTERY uses diegetic UI wherever possible: interface elements exist
inside the world, not drawn on top of it. Every interactive element is
an object the child recognizes as part of the library.

#### Settings Book
A closed book with a navy spine (`#1E2A4A`) and a crescent moon symbol.
Fixed position: top-right of the Library Scene. Always visible.
Tap-hold 1 second to activate — prevents accidental activation.

The color and moon symbol are brand invariants. A theme may restyle
the texture but must preserve both. This is the child's and teacher's
navigation anchor across all sessions and themes.

> **Classroom use case:** before the first session, the teacher shows
> the class the blue book with the moon. "When I say so, hold that book
> and save." One second. Done. No menu navigation required.

#### TTS Button — Open Book
A small open book in the passage panel. Tap to read the passage aloud.
Tap again to stop. Pulses softly while audio plays.
Karaoke word highlighting available when using runtime TTS or
pre-generated audio with sync data. Pre-recorded `.ogg` without sync
illuminates the full passage as a block.

#### Exit Button — Door
A small door, bottom-left of PassageView. Always visible.
Tap-hold 1 second to activate — Owlorumo looks toward the door
during the hold as visual feedback of progress.
On activation: partial progress is saved before transitioning.
The child resumes exactly where they left off.

#### Library Books — Three States
Books communicate their state through visual presence, not labels or icons.

| State | Visual | Behavior |
|---|---|---|
| Available | Saturated colors, gold shimmer, breathes softly | Brightens on hover |
| Dormant | Desaturated, no shimmer | No reaction to hover or tap |
| Completed | Warm permanent glow | Owlorumo occasionally looks toward it |

Dormant books have no lock icon. They simply do not respond.
Some are visible from the first session. Others appear silently
after a passage is completed — never announced, never explained.

#### Owlorumo in the Library
Owlorumo inhabits the library — he is not static in a corner.

**Ambient activities:**
- Sorting books with magic — a book floats, he examines it, returns it
- Walking to the window — looks outside, returns
- Reading at his lectern — base state between activities
- Writing on parchment — state_2 and above only

**Energy by state:** same activities, different quality.
In state_0 movements are heavy and occasionally clumsy.
In state_3/4 they are fluid and present.

**On child entry:** Owlorumo always notices. He finishes his current
gesture naturally, then looks at the child. Never startled. Never ignoring.
He was here. He was waiting. There is a difference.

**On book selection:** a small gesture of recognition.
Not celebration, not instruction.

**On tap in library (no active event):** crystal soft pulse,
a glance toward the child. Presence, not function.

#### Progress Indicator
Two layers for two audiences:

**For the child:** Owlorumo himself communicates accumulated progress.
His `owlorumo_state` visual — crystal brightness, runes, mantle — is the
only progress indicator the child needs. No numbers, no bars.

**For the teacher:** a discrete indicator in the top bar showing
the active profile name and "X of Y books completed."
Visible only when more than one profile is configured.
Readable from a distance in one glance.

#### Audio Strategy

| Content | Strategy |
|---|---|
| Owlorumo's lines | Runtime TTS (canonical) |
| Built-in books | Pre-recorded narration when available; runtime TTS fallback |
| Modder books | Runtime TTS |
| Universal fallback | System TTS |

Owlorumo's lines are text-first and spoken through runtime TTS for consistency across languages and milestones.
Built-in passage audio may use bundled narration when available, but the system always falls back to runtime TTS when needed.

### Theme System (Future-Compatible, Modding-Friendly)
The UI is skinned via **Theme Packs** — JSON + asset bundles that override:
- Color palette tokens (background, text, primary, accent, shadow)
- Font family (must be included in pack; default: Nunito / Comic Neue)
- Owl character sprite sheet
- Background scene illustration
- Button / tile sprite frames
- Particle effect color overrides

**Future-compatible theme examples (M2+):**
| Theme | Description |
|---|---|
| The Sleeping Library (default/base) | Warm browns, amber, parchment, wood, and dormant living shelves. |
| Enchanted Castle | Ancient stone halls, torchlight, tower shelves, and sleeping corridors of knowledge. |
| Alchemical Observatory | Brass instruments, star charts, moonlit study, and a tower-of-reading atmosphere. |
| Sky City | Elevated terraces, bridges, cloudlight, and airy architecture of living knowledge. |


Motor Precision Tolerance

Children aged 6–7 often have limited fine motor precision,
especially on touch screens.

To avoid penalizing reading ability due to imprecise tapping:

• Interactive areas should extend beyond the exact text bounds.
• Word hitboxes may expand ~30% around the word.
• Overlapping hitboxes should prioritize the intended puzzle word.
• Selection should require a deliberate release action.

The system evaluates reading, not pointing accuracy.

---

## 10. Audio Design

The full audio specification is in **READCRAFTERY_AUDIO_STRATEGY v3.1** (companion document). This section summarizes key decisions.

### Sound Identity

Four words: **Warm, Present, Breathing, Nostalgic.**

Acoustic instruments only — piano, soft strings, woodwinds, harp, cello. No chiptune, no synthetic UI, no competitive audio, no harsh error sounds. The sound comes from the library, not from a console.

References: Studio Ghibli (quieter moments), Ori and the Blind Forest (early sections), Journey (cello as solitary hope), Hollow Knight (diminished kingdom).

### Music — Evolves with Restoration

A single musical identity with variants by restoration state and scene context. Sleeping Library: solo fragments, long silences. Reawakened: melody connects, duo/trio. Library of Beginnings: complete theme, fulfilled.

M1 minimum: Sleeping state only. Reawakened/Beginnings as reduced arrangements, not new compositions.

### Reading Protection Rule

1. No melodic hooks during active reading.
2. No strong transients during target search.
3. No sound may imply failure or urgency.
4. Puzzle music must never compete with word recognition.
5. Silence is preferred over decorative audio when in doubt.

### Sound Effects

| Event | Sound | Bus |
|---|---|---|
| `word_found` | Soft crystalline chime — fragment of light returning | SFX |
| `puzzle_completed` | Warm bloom + fragment flight to crystal | SFX |
| Scaffolding cue | Soft ambient tone — "I'm here." Not error. | SFX |
| Book awakening | Soft resonance — the book exhales | SFX |
| Crystal ignition (state_0→2) | Unique sound, plays once per save. Designed from scratch. | SFX |
| Button tap | Soft wooden thump | SFX |
| Incorrect word | **No sound.** Owl reads both words via TTS. | — |

### Text-to-Speech

- Fallback order: Pre-recorded audio → Platform TTS (OS-native).
- Owlorumo's lines: runtime TTS only — never pre-recorded.
- TTS speed adjustable (0.75x, 1x, 1.25x).
- Karaoke word highlighting when using runtime TTS. Pre-recorded `.ogg` illuminates full passage.
- Music ducks aggressively during TTS. Initial default: ~20% volume. Validate on hardware.
- Technical: `DisplayServer.tts_speak()` does not route through Godot AudioServer. Ducking is timing-based.

### Designed Silence

| Moment | Why |
|---|---|
| Crystal ignition (2 sec) | "The child understands — without anyone explaining — that they did this." |
| Owl slow blink | Trust signal. Sound would break it. |
| Dormant book touched | It does not respond. No sound confirms this. |
| Incorrect word | No error sound. Owl reads via TTS only. |
| `celebrate` moment | Total presence. Silence IS the celebration. |

### Audio Accessibility

- Independent volume: Music, SFX, Voice/TTS.
- Single-tap mute all.
- Classroom defaults: Music OFF, SFX low, TTS 100%.
- Subtitles/captions for all spoken dialogue.

> **Full specification:** see `READCRAFTERY_AUDIO_STRATEGY.md` v3.1.

---

## 11. Accessibility & Localization

### Accessibility Features
| Feature | Detail |
|---|---|
| Font size adjustment | Small / Medium / Large / Extra Large |
| High contrast mode | Inverts and boosts UI contrast |
| Dyslexia-friendly font option | OpenDyslexic font available |
| Colorblind modes | Deuteranopia, Protanopia, Tritanopia palette swaps |
| Full TTS for all UI text | Not just passage text |
| Reduced motion mode | Disables particle/confetti effects |
| Left/right hand layout | Mirror puzzle layout for left-handed players |

### Localization Architecture
- All strings stored in external `.po` / `.json` locale files — never hardcoded.
- Date/number formatting respects locale.
- Font system supports extended Latin, Cyrillic, Arabic (RTL layout flag available).
- Language selector always accessible from main menu and settings.
- **Core product languages:** English (en), Spanish (es). Full closed localization system lands in M2.
- **Modding:** Any community member can submit a locale file; framework handles it automatically.

### RTL Language Support
The UI layout engine must support `direction: RTL` flag for Arabic, Hebrew, and Urdu book packs added by modders.

---

## 12. Classroom & Caregiver Use

READCRAFTERY should work in homes, classrooms, and school computer labs without requiring teacher-facing tooling in the core product.

### Core rule

The reading loop must remain usable in short sessions.
Optional discovery layers must never block the passage, the puzzle, or core progress.

### Classroom compatibility goals

- A teacher can use the main reading loop without needing dashboards or analytics
- Optional discoveries (such as Hidden Books or re-readable rewards) can be left for later
- Sessions can end cleanly after a passage or book milestone
- The game should tolerate mixed contexts: station work, shared reading, home follow-up

### Caregiver-friendly expectations

- The game should be legible and reassuring without requiring constant adult intervention
- Optional content may be revisited later from the library once discovered
- The experience should reward curiosity without punishing short sessions

### Direct Access — Classroom Entry Point

A teacher may need all students to open the same book at the same passage. The standard Library → Book Selection flow adds friction in a timed classroom session.

**Design:** The game accepts an optional direct-access parameter that bypasses the Library and loads a specific book and passage directly.

- **HTML5 (school Chromebooks):** URL parameter. The teacher shares a link: `?book=little_seed_01&passage=2`. The game loads directly into that passage. On completion, the child can continue the book or return to the Library.
- **App (Android/iOS):** A simple text field in the Settings Book (adult-facing) where a book_id can be entered. Alternatively, a QR code scan.

This is not a teacher dashboard. It is a single entry point — one parameter, one destination. No student management, no analytics, no class codes.

**Milestone:** Design closed. Implementation M1 (URL parameter) and M2 (in-app field).


### Error Presentation — ✅ CLOSED

**The child never sees an error.** Owlorumo never breaks. The library never fails visibly.

| Error | What the child sees | What the adult sees |
|---|---|---|
| BookPack corrupted/rejected | The book simply does not exist in the Library. | `push_error()` in console. |
| TTS unavailable for language | TTS speaks in fallback language. | Deferred notice in Settings. |
| Save fails | Nothing. Game continues. Retry on next opportunity. | `push_error()` in console. |
| Passage file missing | Book has fewer pages. Child doesn't know how many "should" exist. | `push_error()` with context. |

**Rule:** If the world cannot respond, the world stays asleep. Errors are dormant books.

**Report a Problem (M3):** A button in the Settings Book (adult screen) generates a local text file with recent session errors. The adult can email it manually. No automatic transmission. Compatible with zero-data-collection policy.

> **Scope note:** Teacher dashboards, student management, classroom codes, upload flows, and student data collection are out of scope. See Architecture Contract §1 (Teacher Edition — removed).


---

## 13. Modding System

### Overview
READCRAFTERY is built on the principle that **content = mods**. Even the built-in books use the same modding format. This means the modding system is fully validated by shipping with it.

### Two Modding Layers

#### Layer 1: Content Mods (Books & Puzzles)
Anyone can create a Book Pack by authoring a folder of JSON + assets.

**Book Pack Validator Tool**
A future-facing validation/preview tool path that may eventually ship as a desktop/web utility. When present, it would:
- Lets modders preview their book pack exactly as it will appear in-game
- Validates JSON schema and reports errors with clear messages
- Generates a `pack.zip` ready to upload to itch.io or the community hub

**Distribution**
- Packs uploaded to itch.io as "READCRAFTERY Book Pack" tag
- In-game mod browser remains a later-phase ambition, not a current launch contract
- Local file drop: players can drop a `pack.zip` into a `/mods` folder and it auto-loads

#### Layer 2: Theme Mods (UI)
A Theme Pack consists of:
```
my_theme/
├── theme.json         ← Color tokens, font refs, flags (RTL, dark mode)
├── fonts/
│   └── MyFont.ttf
├── sprites/
│   ├── owl_idle.png
│   ├── owl_celebrate.png
│   ├── bg_library.png
│   ├── btn_normal.png
│   └── btn_hover.png
└── preview.png        ← 800x500 screenshot for the theme selector
```

### Modding API Reference (Outline)

#### Book Pack JSON Schema
```
metadata.json
  required: title, author, language, age_min, age_max, difficulty (1-3), version
  optional: description, cover_image, tags[], license

passage_XX.json
  required: id, text, language, difficulty, puzzles[]
  optional: title, illustration, audio, comprehension_question

puzzles[]
  required: type (word_glow|scramble|word_hunt|fill_passage|rhyme_finder)
  required: targets (array of target words OR the string "auto")
  optional: auto_config.word_count, auto_config.min_length, auto_config.max_length, auto_config.pos_filter[]
  optional: time_limit_seconds, hint_count, grid_size (for word_hunt)

  Note: "targets": "auto" triggers PuzzleGenerator at load time using the passage
  text as source. Hand-authored targets always take precedence over auto_config.
```

#### Theme JSON Schema
```
theme.json
  required: name, version, author
  color_tokens: background, surface, text_primary, text_secondary,
                accent, highlight, correct, incorrect, shadow
  fonts: body_font (filename), display_font (filename)
  flags: rtl (bool), dark_mode (bool)
  sprites: (all optional, falls back to defaults if missing)
    owl_idle, owl_celebrate, owl_hint,
    bg_library, bg_puzzle,
    btn_normal, btn_hover, btn_pressed,
    tile_blank, tile_filled, tile_correct
```

### Modding Documentation
A full **Modding Guide** (separate document, ~20 pages) will be published as:
- In-game help section
- PDF on itch.io and readcraftery.io
- GitHub wiki (if open source tools are hosted publicly)

---

## 14. Monetization Strategy

### Model: One-Time Purchase
✅ **CLOSED** — READCRAFTERY is a **pay-once, own-forever** game. No free-to-play, no DLC tiers, no in-game currency. The player pays once and gets the complete game including all built-in book packs and themes.

**Rationale:** Honest alignment with a solo dev's reality. Maximizes trust with parents. Avoids the infrastructure complexity of subscription or DLC systems. The Stardew Valley model — pay once, own forever, community mods are free — is simple, sustainable, and friction-free.

READCRAFTERY follows a strict **no dark patterns, no ads, no in-game currency** policy — targeting a young audience demands this both ethically and for COPPA/GDPR-K compliance.

### Revenue Streams

| Stream | Description | Price Tier |
|---|---|---|
| **Base Game** | All built-in book packs, all themes, full gameplay — one payment | $4.99–$7.99 (TBD) |
| **Community Book Packs** | Third-party content on itch.io — priced by creator (READCRAFTERY takes 0% cut) | Varies |
| **Steam Release (Phase 2)** | Same one-time purchase model on Steam with Workshop integration | TBD |

### Notes
- No advertising ever shown to players.
- No gameplay content behind a paywall — the game is complete at purchase.
- Community modders are encouraged to distribute and monetize their own packs freely.
- Exact pricing TBD based on content volume at launch and market research.

---

## 15. Platform Strategy

### Phase 1: itch.io + Web (Months 1–12)
- Web (HTML5) version deployed to itch.io page — free to play in browser
- Windows + Mac downloadable builds on itch.io
- Devlog updates and community engagement on itch.io
- Modding community established via itch.io tags + Discord

### Phase 2: Mobile (Months 9–18)
- Android via Google Play
- iOS via App Store
- Mobile-specific UX adaptations (see Section 9)

### Phase 3: Steam (Months 18–30)
- Steam release with Steam Workshop for mod distribution
- Achievements, trading cards (cosmetic stickers → trading cards)
- Steam Deck compatibility (PC layout, controller support)

### Platform-Specific Notes
| Platform | Key Consideration |
|---|---|
| Web (HTML5) | Must load in < 5 seconds on average school connection. Keep base assets < 20MB. |
| Android | Support Android 8.0+ (API 26+). Large-screen (Chromebook) layout. |
| iOS | App Store age rating: 4+. No third-party analytics SDKs (COPPA). |
| Steam | Controller input mapped for all interactions. Steam Deck resolution (1280x800). |

---

## 16. Technology Stack Recommendation

### Primary Recommendation: Godot 4

**Verdict: Best choice for a solo developer targeting all three platforms.**

| Criterion | Assessment |
|---|---|
| Platform export | PC + Web (HTML5) + Android + iOS — all from one codebase ✅ |
| 2D performance | Excellent. This game is pure 2D — Godot 4 is ideal ✅ |
| Scripting | GDScript (Python-like, easy to learn) + C# option ✅ |
| Cost | 100% free and open source. No royalties ever ✅ |
| Modding support | JSON loading, file system access, runtime resource loading ✅ |
| Community | Large, active, extensive documentation ✅ |
| itch.io export | One-click HTML5 export directly to itch.io ✅ |
| Solo dev suitability | Excellent — fast iteration, built-in scene editor ✅ |
| TTS / Audio | GodotTTS plugin (Android/iOS/PC native TTS access) ✅ |
| Learning curve | Moderate — 2–4 weeks to productive for a developer with any experience |

**Godot 4 Specific Modules to Use:**
- `FileAccess` + `JSON` — mod loading at runtime
- `AudioStreamPlayer` + `AudioBus` — layered audio control
- `RichTextLabel` with BBCode — styled, interactive passage text
- `AnimationPlayer` / `Tween` — visual effects and celebrations
- `HTTPClient` — future mod browser API calls
- `DisplayServer` — screen size and orientation handling

---

### Alternative 1: Web-First (TypeScript + Phaser.js)

**Best if:** You want the fastest path to itch.io and web, and are already a JavaScript/TypeScript developer.

| Criterion | Assessment |
|---|---|
| Web (HTML5) | Native — zero export friction ✅ |
| Mobile | Via Capacitor/Cordova wrapper — functional but not native ⚠️ |
| PC standalone | Electron wrapper — works but adds 100MB+ overhead ⚠️ |
| Modding | JSON files + dynamic asset loading — excellent ✅ |
| 2D performance | Good for this game's complexity ✅ |
| TTS | Web Speech API (excellent in browser; limited offline) ✅ |
| Cost | Free (Phaser.js MIT license) ✅ |
| Solo dev speed | Fast if you know JS/TS ✅ |

**Verdict:** Excellent for Phase 1 (itch.io/web), more painful for mobile and standalone. Suitable if you want to launch quickly and port later.

---

### Alternative 2: Unity (C#)

| Criterion | Assessment |
|---|---|
| Platform export | Excellent — all platforms ✅ |
| 2D performance | Good, but heavier than Godot for pure 2D ⚠️ |
| Cost | Free tier has revenue cap; recent licensing controversy ⚠️ |
| Modding | Requires custom implementation or third-party tool ⚠️ |
| HTML5 export | Works but builds are large (5–30MB WASM) ⚠️ |
| Solo dev suitability | Steeper than Godot for 2D focused games ⚠️ |

**Verdict:** Not recommended. Godot 4 is strictly better for this use case, especially for a solo dev. Unity's recent pricing changes add risk for an indie project.

---

### Alternative 3: C++ with Raylib

| Criterion | Assessment |
|---|---|
| Performance | Maximum — overkill for this game ⚠️ |
| Dev speed | Slow — everything built from scratch ❌ |
| Platform export | Possible but requires platform-specific toolchains ⚠️ |
| Modding support | Must be fully custom implemented ❌ |
| TTS integration | Very manual — platform APIs directly ❌ |
| Solo dev suitability | Not recommended unless you're a systems programmer ❌ |

**Verdict:** Not recommended for this project. The gameplay complexity does not justify the low-level effort. Reserve for performance-critical games or if you have a strong C++ background and enjoy that style of development.

---

### Alternative 4: Flutter + Flame Engine (Dart)

**Emerging option — worth mentioning.**

| Criterion | Assessment |
|---|---|
| Mobile (Android/iOS) | Excellent — Flutter is first-class mobile ✅ |
| Web | Good HTML canvas output ✅ |
| Desktop PC | Works via Flutter Desktop ✅ |
| 2D game (Flame) | Adequate for this complexity ✅ |
| TTS | flutter_tts plugin — very good ✅ |
| Modding | JSON-based, feasible ✅ |
| Community | Smaller game dev community than Godot ⚠️ |

**Verdict:** A legitimate alternative, especially if you have Flutter/Dart experience. Falls slightly behind Godot due to smaller game dev ecosystem.

---

### Final Recommendation Summary

```
Solo dev + PC + Web + Mobile + Children's game + Modding system
                         ↓
              ✅ GODOT 4 (Primary Recommendation)
              ✅ Phaser.js/TypeScript (If web-first priority)
              ⚠️  Flutter/Flame (If strong mobile priority)
              ❌  Unity / C++/Raylib (Not recommended)
```

---

## 17. Technical Architecture

### High-Level Architecture (Godot 4)

```
READCRAFTERY
├── /core
│   ├── GameManager.gd          ← Singleton: global state, save/load
│   ├── AudioManager.gd         ← Singleton: music, SFX, TTS
│   ├── LocaleManager.gd        ← Singleton: current language, string lookup
│   └── ProgressManager.gd      ← Singleton: restoration milestones, journal, achievements
│
├── /content
│   ├── ModLoader.gd            ← Scans /mods/, validates, registers packs
│   ├── BookPack.gd             ← Resource class: book metadata + passages
│   ├── Passage.gd              ← Resource class: text, puzzles, audio refs
│   ├── PuzzleDefinition.gd     ← Resource class: type, targets, config
│   └── PuzzleGenerator.gd      ← Auto-generates targets[] from passage text
│                                  Called by ModLoader when targets == "auto"
│                                  Outputs a populated PuzzleDefinition
│                                  Bundles: stopwords_en.json, stopwords_es.json
│
├── /scenes
│   ├── Library/                ← Main menu / book selection
│   ├── PassageView/            ← Text display + read-aloud
│   ├── Puzzles/
│   │   ├── WordGlow/
│   │   ├── Scramble/
│   │   ├── WordHunt/
│   │   ├── FillPassage/
│   │   └── RhymeFinder/
│   ├── Completion/             ← Passage completion transformation controller / overlay
│   ├── Journal/                ← Reading journal / stickers
│   └── Settings/               ← Audio, language, accessibility, profiles
│
├── /themes
│   ├── ThemeLoader.gd          ← Loads theme.json + assets at runtime
│   └── ThemeTokens.gd          ← Applies palette/font to all UI nodes
│
└── /mods                       ← User/community mod folder (runtime)
    ├── builtin_books/          ← Shipped packs (same format as user mods)
    └── [community packs]/
```

### Save System
- Save data stored in `user://saves/profile_01.json` (Godot user data path)
- Supports multiple profiles — no hard limit. Useful for siblings sharing a device
or classroom lab deployments where each student needs their own profile.
Profile selection appears at launch only when more than one profile exists.
Adding a new profile is always visible and immediate from the selection screen.
- Save includes: current book progress, restoration milestones, journal, settings, active theme

**Save File Schema (must be implemented from Day 0 / M0):**
```json
{
  "save_version": "1.0.0",
  "profile_id": "profile_01",
  "display_name": "Sofia",
  "avatar_id": "owl_default",
  "settings": {
    "language": "es",
    "tts_speed": 1.0,
    "font_size": "large",
    "active_theme": "sleeping_library"
  },
  "progress": {
    "owlorumo_state": 2,
    "books": {
      "little_seed": {
        "awakened": true,
        "passages_completed": 3,
        "passage_completion_tiers": [3, 2, 3],
        "book_milestones": ["first_passage", "book_completed"],
        "last_played": "2026-03-09T15:30:00Z"
      }
    },
    "achievements": []
  },
  "journal": {
    "stickers": ["seed_sticker", "owl_hat"],
    "saved_words": ["meadow", "carried"]
  }
}
```

> **Why `save_version` matters:** Every time a new feature adds fields to the save schema (M2+), migration logic in `GameManager._migrate_save(data)` must handle older versions gracefully. Without the version field, there is no way to detect which migration to run. Adding it at M0 costs one line; retrofitting it at M3 risks corrupting existing saves. Migration rule: if `save_version` is absent, treat as `"0.9.0"` (pre-release) and run full migration.

### Mod Loading Flow
```
App Start
  → ModLoader scans /mods/ directory
  → For each folder: validate metadata.json schema (fail fast, log errors)
  → Valid packs → registered in BookPackRegistry
  → Invalid packs → logged to error panel (visible in dev mode)
  → Library scene queries BookPackRegistry for available books
  → Player selects book → Passage resources loaded lazily on demand
    → For each puzzle in passage:
        if targets == "auto" → PuzzleGenerator.generate(passage_text, auto_config)
        else → use hand-authored targets as-is
    → Resolved PuzzleDefinition passed to IPuzzle scene (never sees "auto")
```

### Localization Flow
```
LocaleManager.set_language("es")
  → loads /locales/es.json
  → all UI nodes with "translatable" flag auto-update
  → TTS language code updated → AudioManager.tts_language = "es-ES"
  → active book pack checked for matching language passage
  → if no matching language passage → fallback to "en"
```

### Puzzle Engine
Each puzzle type is a self-contained scene implementing `IPuzzle` interface:
```gdscript
class_name IPuzzle
extends Control

signal word_found(word: String)
signal puzzle_completed(completion_tier: int)
signal hint_requested()

func initialize(puzzle_def: PuzzleDefinition, passage_text: String) -> void:
    pass  # Abstract — implemented by each puzzle type

func show_hint() -> void:
    pass  # Reveals support according to puzzle rules
```

This interface makes it trivial to add new puzzle types without modifying core systems — critical for modding extensibility.

---

## 18. Concept Art Descriptions

*(These descriptions serve as briefs for an artist. An AI image generation tool such as Midjourney or Stable Diffusion, or a commissioned artist, should produce these assets.)*

### Scene 1: The Sleeping Library (Main Menu)

**Style:** Storybook Arcane in warm organic pixel art. The scene should feel like a real illustrated page made tangible: hand-touched, slightly irregular, textured, and alive. The library is welcoming and magical, never sterile, modern-flat, or app-like. Warm browns, parchment creams, amber lamplight, and deep night-blue magical counterpoints. Magic is ambient, not explosive.

**Camera / Composition:** A readable front-facing or gently angled library composition that prioritizes clarity over spectacle. The player should immediately understand: this is a living library, not a generic fantasy room. Keep the space visually calm enough to support menu readability.

**Contents:** Floor-to-ceiling bookshelves, curved wooden furniture, tactile paper and wood textures, a central reading area, and visible shelf zones that can gradually feel more inhabited over time. Some books glow softly. Some shelves look slightly neglected or dormant. No padlocks, no numeric progress symbols, no overt progression iconography.

**Owlorumo:** Owlorumo is present in the library as companion and guardian, not as a mascot sticker. He should feel alive even at rest: a soft blink, subtle breath, staff crystal dim but not dead, posture attentive and kind. His staff, moon brooch, belt, boots, and blue mantle remain clearly readable. He is young, trustworthy, and curious — never severe, never ornamental.

**Progress expression:** Restoration is shown through light, presence, and response — not through numeric gates, lock icons, or overt UI trophies. The earliest visible changes should be subtle: a warmer crystal, a faint eye glow, a shelf that feels more awake, a once-dormant book now breathing softly with invitation.

**Emotional goal:** The child should feel: “This place was waiting for reading to wake it.”

---

### Scene 2: Puzzle View — WordGlow Mode

**Style:** Storybook Arcane reading scene in warm organic pixel art. The passage remains the visual center at all times. The puzzle UI supports the act of reading; it must never overpower or visually replace the text. The overall feeling is calm, focused, magical, and tactile.

**Layout / Composition:** The readable passage occupies the primary area of the screen on a parchment-like reading surface. A compact target card and puzzle support UI sit below or beside the passage without creating a hard competitive split. The child should immediately understand that the task is happening in the text itself.

**Passage behavior:** The full passage is visible and readable. Words may respond softly on hover or touch-ready focus, but the correct answer is never pre-revealed by a strong glow. The text must feel inviting and searchable, not annotated like a worksheet.

**Target presentation:** One target word appears at a time. It is shown clearly with optional picture support and can be read aloud. The target presentation should feel like a gentle reading prompt, not a command badge.

**Word bank / progress UI:** A persistent word inventory remains visible as supportive puzzle UI. Found words stay visible in a quiet `found` state. Anonymous slots communicate how many targets belong to the puzzle, but they do not turn the screen into a progress dashboard.

**Success accent:** When the child taps the correct word in the passage, that occurrence responds warmly. A copy of the found word travels toward its destination with a soft magical trail, while the original location in the passage remains resolved and calm. The feedback should feel satisfying, never explosive.

**Owlorumo presence:** Owlorumo may appear nearby as a reading companion or support anchor, watching, thinking, or gently reacting. He is not the center of the layout. The passage is.

**Emotional goal:** The child should feel: “I found it because I read it.”

---

### Scene 3: Passage Completion Transformation

**Style:** In-scene transformation, not a separate reward screen. The existing reading scene responds warmly and briefly to completion. The feeling is magical, restorative, and intimate — never noisy, arcade-like, or disconnected from the act of reading.

**Visual behavior:** Small white-gold fragments of light emerge and travel toward Owlorumo's staff crystal. The crystal answers with a soft pulse whose intensity reflects the completion result. Light may briefly echo into Owlorumo's eyes and then into the surrounding scene, hinting that the library itself is waking with him.

**Owlorumo:** Owlorumo gives a brief, warm reaction appropriate to the tone of the book and the child's moment of success. He may shift posture, brighten softly, or show a quiet spark of recognition. He does not perform a comic victory dance and he is never framed like a game-show mascot.

**Scene response:** The current environment may answer subtly — a shelf feels more awake, dust lifts in the lamplight, a dormant book breathes, a sticker or journal memory appears if a real milestone was reached. The transformation should feel like the world noticed the reading.

**Intensity rule:** The effect should remain modest and readable. No star rain, no reward numerals, no explosive confetti storm as the default language. If celebratory particles exist, they must remain theme-safe, brief, and secondary to the crystal response.

**Emotional goal:** The child should feel: “Something came back because I finished reading.”

---

### Scene 4: Theme Variations — Future-Compatible Examples

**Purpose:** These are future-compatible theme examples, not alternate core identities for READCRAFTERY. Every theme must preserve reading clarity, functional UI roles, emotional warmth, and Owlorumo's recognizability. A theme may change mood, palette, materials, and decorative language, but it must never make the game feel like a different genre or a different character system.

**Global rule:** Theme variation changes surface expression — not the reading-first structure of the game. Passage readability, target visibility, support cues, and child-safe warmth remain constant across all themes.

**Owlorumo across themes:** Owlorumo remains recognizably the same character in every theme. His hat, staff, moon brooch, belt, boots, and overall silhouette remain intact. Theme variation may appear through one small belt accessory and minor material accents only. These additions are secondary and must never compete with the staff, brooch, or silhouette.

**Enchanted Castle Theme:** Ancient stone halls, warm torchlight, candlelit reading alcoves, tower shelves, carved arches, old banners, and sleeping corridors of knowledge. The mood is magical and noble, never dark-horror or harsh gothic. Reading surfaces remain warm and clear.  
**Owlorumo accent:** a small adventurer-mage belt pouch — practical, worn, and scholarly, as if it carried small tools, folded notes, or restoration dust.

**Alchemical Observatory Theme:** A high tower of study beneath the night sky. Brass instruments, star charts, parchment diagrams, moonlit windows, and slow dust motes create the feeling of wisdom being interpreted through sky and symbol. This is not sci-fi. It is literary, mystical, and handcrafted — like an old scholar climbing a tower to read the heavens.  
**Owlorumo accent:** a small astrolabe hanging from the belt. It is a secondary detail only, readable but never dominant.

**Sky City Theme:** Elevated reading terraces, bridges between towers, drifting banners, cloudlight, airy domes, and a sense of wonder carried by height and wind. The theme should feel luminous and spacious without becoming noisy or over-bright. It is a city of living knowledge above the clouds, not a whimsical toy skyline.  
**Owlorumo accent:** a small celestial star charm hanging from the belt. The charm should read as a sky talisman, not as a game reward icon.

**Constraint:** No theme may break the functional role mapping of the UI, the readability doctrine, or the identity of Owlorumo and the library-world as a refuge of living human knowledge.

---

### Scene 5: Mobile Portrait Layout

**Style:** A calm stacked reading layout for phones and narrow portrait screens. The passage remains primary and readable in the upper portion of the screen. The lower portion contains puzzle support UI sized for child touch, without reducing the experience to a tray of disconnected tiles.

**Layout / Composition:** Top area: passage text on a parchment-like panel with generous margins and native-resolution text. Bottom area: puzzle support UI, targets, and interaction controls arranged for single-finger use. WordGlow still resolves in the passage itself; the lower area supports the task rather than replacing it.

**Owlorumo presence:** Owlorumo remains part of the scene as a companion anchor, not a tiny detached avatar sticker. He may appear as a reduced but still integrated support presence near the reading space or support area.

**Interaction rule:** No swipe-only navigation is required for core play. The layout must work through simple taps and visible controls.

**Emotional goal:** The child should feel: “Even on a small screen, the story still comes first.”

## 19. Release Roadmap## 19. Release Roadmap

### Milestone 0 — Foundation (Month 1–2)
- [ ] Godot 4 project setup, folder structure, scene architecture
- [ ] **Save file schema implemented with `save_version` field** ← Day 0, no exceptions
- [ ] ModLoader core — book pack format finalized and loading
- [ ] Passage view scene — text display + basic TTS
- [ ] Word Glow puzzle — fully functional
- [ ] 1 built-in book (bilingual EN/ES)
- [ ] Basic progression (restoration state stored locally)
- [ ] **Godot HTML5 export validated on itch.io** — confirm `Cross-Origin-Opener-Policy: same-origin` and `Cross-Origin-Embedder-Policy: require-corp` headers are active; confirm audio works in Chrome, Firefox, Safari. Failure mode: silent audio breakage. Fix: itch.io HTML5 "SharedArrayBuffer" setting must be enabled in the game dashboard.
- [ ] **Base build size audit** — HTML5 export must be under 15MB uncompressed. Establish asset compression pipeline (audio as `.ogg` streams, textures with mipmaps) before content accumulates. Retrofitting is expensive.
- [ ] **TTS platform smoke test** — build a single-screen prototype with one paragraph and a TTS play button. Export to Web (Chrome + Firefox), Android (test device), and iOS (simulator). Confirm Spanish and English voices resolve correctly. Document any fallback behavior per platform. Known risk: Android devices with non-Spanish system locale may not have `es-*` TTS voice installed — define fallback strategy (prompt user to install, or fall back to EN voice with warning).

### Milestone 1 — Vertical Slice (Month 3–4)
- [ ] All 5 puzzle types implemented
- [ ] Owl companion animations (idle, celebrate, hint)
- [ ] Visual effects system (sparkles, star rain, confetti)
- [ ] 3 built-in book packs
- [ ] Settings screen (audio, language, accessibility basics)
- [ ] Export to Web (HTML5) and test on itch.io
- [ ] **Internal Preview Tool (dev-only)** — `[Text Area] → [Generate] → [Preview Panel]` — used to validate built-in book content and catch PuzzleGenerator bugs before they reach playtesters. Not distributed publicly yet; public release moves to M3.
- [ ] **M1 content gate:** At least 1 BookPack with 5+ passages, `reading_stage: early_emergent`, original text, 2+ puzzle types represented. Language: `es`. This pack is the integration test for the full pipeline. If it doesn't feel like a complete reading session for a 6-year-old, M1 is not done.
- [ ] **1 functional Hidden Book** (`world_tale`) appears after completing onboarding book.
- [ ] Comprehension questions deferred — schema exists, UI design deferred to M2 when `developing`-stage content arrives.

### Milestone 2 — Alpha (Month 5–6)
- [ ] Full built-in book library (5 books)
- [ ] Reading Journal + Sticker system
- [ ] Achievement badges
- [ ] Theme system — 3 built-in themes
- [ ] Parent Dashboard (in-app PIN)
- [ ] Localization system (EN + ES)
- [ ] Android build tested

### Milestone 3 — Beta / itch.io Launch (Month 7–8)
- [ ] Modding documentation published
- [ ] **Book Pack Validator Tool — public release** (internal version shipped in M1; this is the polished, distributable version for teachers and community modders)
- [ ] **`CONTENT_LICENSING.md` committed to repo** ← hard gate before any public distribution
- [ ] **Privacy policy published** (template-based, covers zero-data-collection base game; no lawyer required at this stage)
- [ ] iOS build tested
- [ ] User testing with 5–9 year olds (recruit via local school or community)
- [ ] Bug fix sprint based on feedback
- [ ] Soft launch on itch.io (free, web)
- [ ] 5 featured community themes highlighted (curated from early modding community)
- [ ] Base support / feedback system in place

### Milestone 4 — Post-Launch (Month 9–12)
- [ ] First official community-curated Book Pack collection
- [ ] Community mod browser (in-game, Phase 2)
- [ ] First community mod showcase

### Milestone 5 — Steam (Month 18–30)
- [ ] Steam Greenlight / Direct submission
- [ ] Steam Workshop integration
- [ ] Controller support + Steam Deck certification
- [ ] Steam achievements + trading cards

---

## 20. Open Questions & Risks

### Hard Blockers — Must Resolve Before Indicated Milestone

| Issue | Why It Blocks | When |
|---|---|---|
| **Save versioning** (`save_version` field) | Without it, M2+ feature additions break existing saves with no migration path | M0 Day 0 |
| **Godot HTML5 COOP/COEP headers** | Missing headers cause silent audio failure on itch.io; SharedArrayBuffer required for Godot 4 WASM threading | M0 — validate on first export |
| **TTS platform smoke test** | TTS behaves differently on Web/Android/iOS; Spanish voice may be absent on non-ES Android devices; must define fallback before content depends on it | M0 |
| **HTML5 build size baseline** | Godot 4 WASM export starts at ~6MB empty; uncontrolled asset growth reaches 50MB+, unusable on school connections | M0 — establish compression pipeline |
| **Content licensing (`CONTENT_LICENSING.md`)** | Cannot publicly distribute books without clear rights documentation; "public domain adaptations" is a risk category | Pre-M3 (before any public release) |
| **Privacy policy (template)** | Required for any public-facing product; template-based is sufficient for zero-data-collection base game | Pre-M3 |

### Quality Improvements — Implement Based on Feedback

| Improvement | Impact Without It | Target Milestone |
|---|---|---|
| Algorithm steps 8–9 (proper noun + apostrophe filter) | PuzzleGenerator produces ~80% quality targets vs ~95%; some odd words slip through | M1 |
| Stopwords categorized by age tier | All ages get the same exclusion list; teachers cannot override for ESL context | M2 (post-feedback) |
| Algorithm step 10 (`sight_words_ratio`) | Teachers cannot enforce sight word quotas; pedagogical flexibility reduced | M2 (opt-in, off by default) |
| PuzzleGenerator test suite (100+ passages) | Generator bugs found by playtesters instead of automated tests | M1–M2 |
| Accessibility validation with real children (ages 4–9) | UX assumptions may not match actual behavior | Pre-M3 (Beta testing) |

### Resolved Questions (Archived)

| Question | Decision |
|---|---|
| Same completion feedback for auto-generated vs hand-authored puzzles? | **Yes** — player never knows the difference; parity is correct |
| Preview Tool milestone? | **M1 internal, M3 public** — needed to validate own content before distributing to modders |
| Analytics for base game? | **None** — no analytics. Zero data collection, full stop. |
| COPPA for base game (no data collection)? | **Trivial** — zero data collection means COPPA compliance is automatic. No personal data is ever collected from players. |
| Should TTS be pre-recorded or runtime? | **Hybrid** — pre-recorded audio for official built-in books (quality); runtime TTS (OS-native) for modded books |
| Font licensing? | **Andika** (SIL OFL) for passage text · **Nunito** (OFL) for UI. Both OFL-licensed. Download from Google Fonts. Commit to `res://fonts/` before building PassageView. |
| Monetization model? | **One-time purchase** — pay once, own forever. No free-to-play, no DLC tiers, no in-game currency, no subscription. Stardew Valley model: complete game at purchase, community mods are free. See §14. |
| Repository structure? | **Four repos under the [The-Readcraftery-Project](https://github.com/The-Readcraftery-Project) GitHub organization.** See table below. Engine is commercial closed-source; modding format is open. |

### Repository Structure

| Repo | Visibility | Purpose | URL |
|---|---|---|---|
| `readcraftery` | 🔒 Private | Engine + official content. Complete Godot project, built-in book packs, official art assets, saves, locales, production content. | https://github.com/The-Readcraftery-Project/readcraftery |
| `readcraftery-docs` | 🌐 Public | Public documentation site (GitHub Pages). GDD, Art Guide, Asset Contracts, Modding Guide. Audience: modders, teachers, press, collaborators. | https://github.com/The-Readcraftery-Project/readcraftery-docs |
| `readcraftery-dev-docs` | 🔒 Private | Internal technical documentation. Build Guide, Architecture Contract, design notes and internal decisions. | https://github.com/The-Readcraftery-Project/readcraftery-dev-docs |
| `readcraftery-SDK` | 🌐 Public | Modding SDK. Book pack JSON schema, theme JSON schema, Preview Tool (M3), example book packs. Audience: modders and content creators. | https://github.com/The-Readcraftery-Project/readcraftery-SDK |

---

## Appendix A: Glossary

| Term | Definition |
|---|---|
| Book Pack | A mod-format bundle containing passages, puzzles, and assets for one book |
| Theme Pack | A mod-format bundle that reskins the game's visual UI |
| Passage | A single text excerpt from a book, with associated puzzles |
| Word Bank | The list of target words a player must find in the current puzzle |
| Owlorumo | The player's animated owl companion character |
| Reading Journal | The persistent in-game scrapbook of progress and stickers |
| IPuzzle | The programming interface (abstract class) all puzzle types implement |
| TTS | Text-to-Speech — automated voice reading of game text |
| PuzzleGenerator | Rule-based engine that extracts target words from passage text when `targets: "auto"` |
| Auto-generated puzzle | A puzzle whose targets were produced by PuzzleGenerator, not hand-authored; yields identical completion feedback |

---

## Appendix B: Competitive Landscape

| Game | Similarity | Key Difference |
|---|---|---|
| Endless Reader (Originator) | Children's word game | No modding, closed content |
| Duolingo ABC | Literacy app | App only, no community content |
| Wordle / NYT Games | Word puzzles | Not for children, no literary context |
| Epic! (reading app) | Digital books for kids | No puzzle mechanics |
| Khan Academy Kids | Educational app | Broader focus, no modding |

**READCRAFTERY's Differentiator:** The only literacy-focused word puzzle game with a full modding system enabling teachers and community creators to add their own books and themes.

## Appendix C: Optional Phonetic Metadata (Future Feature)

Future versions of READCRAFTERY may support phonetic metadata
for each puzzle word.

Example:

```json
{
  "word": "conejo",
  "phonetic_difficulty": "medium",
  "pattern": "CV-CV-CV",
  "tags": ["regular", "animal"]
}
```

This metadata would allow:

• phonics-aware puzzle generation
• difficulty scaling
• targeted reading exercises

This feature is planned for milestone M2
and is not required for the initial implementation.


---

*Document End — READCRAFTERY GDD v1.4*  
*Next document: Technical Specification (modding API detail) and Art Style Guide*
