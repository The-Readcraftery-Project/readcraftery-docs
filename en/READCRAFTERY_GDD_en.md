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


**UI State Separation (Anti Pattern-Matching Design)****UI State Separation (Anti Pattern-Matching Design)**

To prevent children from solving puzzles through visual pattern recognition
instead of reading, the interface separates the reading phase from the search phase.

**READING_STATE**
The story sentence is visible.
The Owl may narrate the sentence using TTS.
Puzzle grid is hidden.

The player presses a button to start the puzzle.

**SEARCH_STATE**
The story text disappears or collapses.
The puzzle grid becomes visible.

The player must recall the words from working memory.

Optional Hint Button
A hint temporarily reveals the sentence again,
but interrupts puzzle solving for a moment.

This design encourages phonological decoding rather than geometric scanning.

> **WordGlow and Scramble exception:** Both puzzles operate during READING_STATE,
> not SEARCH_STATE. WordGlow requires the passage visible because the child taps
> words directly in the text. Scramble requires the passage visible because the
> child reconstructs a word in the context of the sentence it belongs to —
> removing that context turns spelling reconstruction into abstract memory work.
> All other puzzle types (WordHunt, FillPassage, RhymeFinder) operate in
> SEARCH_STATE as defined above.


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
**Core Mechanic:** The full passage is displayed. A target word appears in the word bank at the bottom. The player must tap/click the same word when they spot it in the passage.

- Words in the passage highlight faintly when hovered.
- The target word is shown with a picture icon alongside it.
- Audio reads the target word aloud.
- No time limit. No fail state — only encouragement.
- On success: the word physically "flies" from the passage into the word bank slot with sparkles.

**Skill Reinforced:** Word recognition, sight words, left-to-right scanning.

---

### Puzzle Type 2: Letter Scramble (Ages 5–7, Difficulty 2/3)
**Core Mechanic:** A word from the passage is shown scrambled below the text. The player rearranges letter tiles to spell it correctly.

- The scrambled word tiles sit on a small "craft table" visual.
- A picture hint is available through Owlorumo support — limited uses per puzzle according to profile and difficulty.
- The corresponding word in the passage is blurred or hidden until solved.
- On success: the passage word "unblurs" with a satisfying pop effect.

**Skill Reinforced:** Letter ordering, spelling patterns, phonics.

---

### Puzzle Type 3: Word Hunt Grid (Ages 6–9, Difficulty 2/3 to 3/3)
**Core Mechanic:** A word-search grid is generated from letters in the passage. Players find 5–10 hidden words in the grid.

- Words run left-to-right and top-to-bottom only for younger players (diagonal unlocks at difficulty 3).
- As each word is found in the grid, it highlights in the passage too — connecting the puzzle to the literary context.
- Word list is shown with small icons.

**Skill Reinforced:** Spelling, vocabulary, pattern recognition.

---

### Puzzle Type 4: Fill the Passage (Ages 7–9, Difficulty 3/3)
**Core Mechanic:** A sentence from the passage is shown with 1–3 blanks. A small set of word tiles is offered. Player drags the correct word(s) into the blanks.

- Wrong placements shake and bounce back — no harsh failure sound.
- Correct placement causes the full sentence to "light up."
- Distractors (wrong word choices) are always plausible but wrong.

**Skill Reinforced:** Reading comprehension, vocabulary in context, grammar awareness.

---

### Puzzle Type 5: Rhyme Finder (Ages 4–7, Difficulty 2/3)
**Core Mechanic:** A word from the passage is highlighted. The player must find another word in the passage (or in a provided set) that rhymes with it.

- Rhyming pairs are chosen during book pack authoring.
- Audio support reads both words aloud for comparison.

**Skill Reinforced:** Phonemic awareness, rhyme recognition.


#### WordGlow — UI behavior details

**Tile found behavior:**
When a target word is found, the tile remains visible in the word bank
in `found` state — grey, no glow, not interactive. Simultaneously, a copy
of the tile flies to the anonymous slot and arrives with a gold pulse.
The child retains the full word inventory visible at all times while
receiving the motion feedback of the word reaching its destination.

**Anonymous slots:**
Slots communicate "something belongs here" before any word arrives.
Visual: grey `#9E9E9E` at 60% opacity. No label, no animation in rest state.
The count of slots equals the count of target words — the child knows
how many words to find without being told which ones.

**Hint behavior — Owlorumo as hint button:**
There is no separate hint button. The child taps Owlorumo directly.

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

| Display profile | Passage shown | Owlorumo glow | Slots |
|---|---|---|---|
| `conservative` | Relevant sentence only | Active, full radius | Anonymous |
| `standard` | Full paragraph | Active, reduced radius | Anonymous |
| `advanced` | Full passage | Disabled | No slots |

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

#### Sequence (6–8 seconds if child does not interact)

1. **Puzzle complete**
   — Found tiles pulse gold simultaneously
   — Passage above glows softly

2. **Owlorumo reacts** (`owl_excited` → `owl_celebrate`)
   — Staff crystal explodes in particles
   — Duration: 2–3 seconds

3. **Fragments of light emerge from the staff crystal**
   — One by one, each with a small sound
   — Duration: 1.5 seconds

4. **The Discovery moment**
   — Something small and unexpected happens in the background
   — A book floats briefly out of the shelf
   — Profile C: a word from the next passage glows in the crystal
   — Duration: 1–2 seconds

5. **Continue button appears**
   — Not urgent — child can stay and watch
   — Owlorumo returns to `owl_idle` after 3 seconds

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


### Sticker Collection
Each book completed adds stickers to the player's "Reading Journal" — an in-game scrapbook. Stickers are themed around the book's content (animals, objects, characters).

### Reading Journal
A persistent, visual record of:
- Books read and % completion
- Favorite words collected (the player can "keep" any word they love)
- Restoration milestones discovered across books and the library-world
- Meaningful reading memories and collection-style badges (e.g., "Found 100 words!", "Night Owl Reader!", "First Book Completed")

### Achievement Badges
| Badge | Trigger |
|---|---|
| First Word! | Find first word ever |
| Bookworm | Complete first book |
| Library Awakener | Help reawaken 5 books |
| Word Collector | Save 50 words to the journal |
| Night Owl Reader | Complete 10 reading sessions |
| Second Language Reader | Complete a puzzle in a second language |


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

### Music
- **Library Theme:** Soft, looping ambient music. Piano + soft strings. Calm but inviting.
- **Puzzle Theme:** Upbeat, light, non-distracting. Tempo slightly faster to encourage engagement. Loops seamlessly.
- **Celebration Sting:** Short (3–5 sec) triumphant melody on puzzle complete.
- All music should have a child-friendly, warm tone — avoid anything tense or competitive.

### Sound Effects
| Event | Sound |
|---|---|
| Word found | Soft chime + sparkle whoosh |
| Letter placed correctly | Gentle pop |
| Scaffolding cue | Soft ambient tone — signals Owl is about to help. Not associated with error. |
| Owl hint | Soft hoot |
| Book awakening | Page turn + brief warm reveal |
| Sticker earned | Satisfying sticky-paper sound |
| Button tap | Soft click / thump |

### Text-to-Speech (TTS) System
- All passage text must be readable by TTS engine or pre-recorded audio.
- **Fallback order for passages:** Pre-recorded audio → Platform TTS (OS-native) → in-engine TTS library.
- **Owlorumo's adaptive lines:** runtime TTS only.
- TTS speed should be adjustable (0.75x, 1x, 1.25x) — important for early readers.
- Word highlight synced to TTS playback (karaoke-style word highlighting during read-aloud).
  **Scope:** karaoke highlighting is available only when using runtime TTS (OS-native).
  Pre-recorded `.ogg` audio does not carry word-level timing data — when a pack uses
  pre-recorded audio, the full passage illuminates as a block during playback,
  not word by word. Timestamp-based sync files are not required from modders.

### Audio Accessibility
- All audio is independently volume-controllable: Music, SFX, Voice/TTS.
- Option to mute music only (for classroom use).
- Subtitles/captions for all spoken dialogue.

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

> **Scope note:** teacher dashboards, student management, classroom codes, and upload flows are future-facing ideas and are not part of the closed technical contract for the current milestone set.

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
    "achievements": ["first_word", "bookworm"]
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
