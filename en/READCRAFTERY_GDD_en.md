# READCRAFTERY — Game Design Document
**Version:** 1.2  
**Date:** March 2026  
**Status:** Pre-Production Spec  
**Author:** Andrés Reyes. El Programador Pobre  
**Companion documents:** Architecture Contract v1.1 · Build Guide v1.3  

---

> **Note for technical readers:** This document describes the game's vision and design.
> It is intentionally aspirational: it includes features such as Teacher Dashboard,
> karaoke-style highlighting, and RTL support that do not yet have a closed technical contract.
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
12. [Teacher & Parent Tools](#12-teacher--parent-tools)
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
| **Tagline** | *"Every word is an adventure."* |
| **Genre** | Educational Word Puzzle / Literary Adventure |
| **Primary Platform** | PC (Windows/Mac/Linux), Web (HTML5), Android & iOS |
| **Target Age** | 4–9 years old (core); 6–12 with teacher/classroom use |
| **Languages at Launch** | English, Spanish (+ modding API supports any language) |
| **Monetization** | One-time purchase (itch.io / Steam) — pay once, own forever |

### Elevator Pitch
READCRAFTERY is a word discovery game that wraps age-appropriate literary content inside fun, colorful puzzle mechanics. Players explore a magical library, choose books, and then dive into the text — hunting for hidden words, unscrambling letters, and connecting meaning to story. Each found word animates, sparkles, and rewards the player with story progress, unlockable characters, and visual celebrations. The entire game — from books to UI themes — is community-moddable.

---

## 2. Vision & Pillars

### Design Pillars

| Pillar | Description |
|---|---|
| 🔤 **Reading First** | Every mechanic must reinforce reading skills, never replace them. The text is always present and central. |
| 🎉 **Joyful Reward** | Children must feel celebrated frequently. Visual and audio feedback must be immediate, warm, and exciting. |
| 📚 **Literary Respect** | Books are not mere word banks — the story matters. Players should come away having absorbed content. |
| 🔧 **Open by Design** | Modding is not an afterthought; the content system IS the game. Books are mods. Themes are mods. |
| 👩‍🏫 **Teacher Empowered** | The game doubles as a classroom tool. Teachers need control without needing to be developers. |

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

### Secondary: Educators & Parents
- Primary school teachers looking for literacy tools
- Parents seeking screen time with learning value
- Homeschool families

### Tertiary: Modding Community
- Indie developers who want to add book content
- Teachers creating custom book packs
- Word puzzle enthusiasts (ages 10+) drawn by community content

### Persona Examples

**"Sofia, age 6"** — learning to read in Spanish and English at home. Loves bright colors and animals. Gets frustrated quickly if puzzles are too hard. Needs audio support and positive reinforcement constantly.

**"Ms. Rivera, 2nd Grade Teacher"** — wants to assign the same book to her class and use it as a shared reading activity. Can direct students to a specific book pack and use the game as a classroom tool without any setup. Creates her own book packs using the Preview Tool.

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
│  [UNLOCK: next passage / sticker / theme / character]       │
│       ↓                                                     │
│  [RETURN TO LIBRARY or CONTINUE BOOK]                       │
└─────────────────────────────────────────────────────────────┘
```

### Step-by-Step Flow

1. **The Great Library** — The main menu is a cozy, magical library. Bookshelves line the walls. Books glow softly to invite interaction. The player's "Reading Owl" companion sits nearby.

2. **Book Selection** — The player picks a book. Each book has a cover, a title, a difficulty star rating (1–3), and a word count badge. New books are locked until sufficient stars are collected.

3. **Story Time (Passage View)** — A passage from the book is displayed. Large, friendly font. Illustration alongside (if the book pack includes art). The Reading Owl reads the passage aloud (text-to-speech or recorded audio). Player can replay the reading at any time.

4. **Puzzle Challenge** — Below or alongside the passage, a puzzle appears. The type of puzzle depends on the difficulty tier and the player's age profile. (See Section 5.)

5. **Word Discovery** — Player interacts with letters/words. Successful finds trigger immediate visual celebration.

6. **Passage Complete** — A "Chapter Complete" screen shows stars earned, new words learned, and a short summary/question to reinforce comprehension.

7. **Unlock & Progress** — New passage unlocks, or bonus content is revealed (sticker, theme element, mini-story). Player returns to library or continues.


**UI State Separation (Anti Pattern-Matching Design)**

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

---

## 5. Puzzle Mechanics

### Puzzle Type 1: Word Glow (Ages 5–7, Difficulty ★☆☆)
**Core Mechanic:** The full passage is displayed. A target word appears in the word bank at the bottom. The player must tap/click the same word when they spot it in the passage.

- Words in the passage highlight faintly when hovered.
- The target word is shown with a picture icon alongside it.
- Audio reads the target word aloud.
- No time limit. No fail state — only encouragement.
- On success: the word physically "flies" from the passage into the word bank slot with sparkles.

**Skill Reinforced:** Word recognition, sight words, left-to-right scanning.

---

### Puzzle Type 2: Letter Scramble (Ages 5–7, Difficulty ★★☆)
**Core Mechanic:** A word from the passage is shown scrambled below the text. The player rearranges letter tiles to spell it correctly.

- The scrambled word tiles sit on a small "craft table" visual.
- A picture hint is available (tap the owl for a hint — limited uses per session).
- The corresponding word in the passage is blurred or hidden until solved.
- On success: the passage word "unblurs" with a satisfying pop effect.

**Skill Reinforced:** Letter ordering, spelling patterns, phonics.

---

### Puzzle Type 3: Word Hunt Grid (Ages 6–9, Difficulty ★★☆ to ★★★)
**Core Mechanic:** A word-search grid is generated from letters in the passage. Players find 5–10 hidden words in the grid.

- Words run left-to-right and top-to-bottom only for younger players (diagonal unlocks at difficulty 3).
- As each word is found in the grid, it highlights in the passage too — connecting the puzzle to the literary context.
- Word list is shown with small icons.

**Skill Reinforced:** Spelling, vocabulary, pattern recognition.

---

### Puzzle Type 4: Fill the Passage (Ages 7–9, Difficulty ★★★)
**Core Mechanic:** A sentence from the passage is shown with 1–3 blanks. A small set of word tiles is offered. Player drags the correct word(s) into the blanks.

- Wrong placements shake and bounce back — no harsh failure sound.
- Correct placement causes the full sentence to "light up."
- Distractors (wrong word choices) are always plausible but wrong.

**Skill Reinforced:** Reading comprehension, vocabulary in context, grammar awareness.

---

### Puzzle Type 5: Rhyme Finder (Ages 4–7, Difficulty ★★☆)
**Core Mechanic:** A word from the passage is highlighted. The player must find another word in the passage (or in a provided set) that rhymes with it.

- Rhyming pairs are chosen during book pack authoring.
- Audio support reads both words aloud for comparison.

**Skill Reinforced:** Phonemic awareness, rhyme recognition.

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

> **Auto-generation rule:** When `targets` is the string `"auto"`, `PuzzleGenerator` runs at pack-load time and populates the targets array before any `IPuzzle` scene receives the `PuzzleDefinition`. The puzzle scene never distinguishes between hand-authored and auto-generated targets. Stars awarded are identical in both cases.
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

### Star System
Each puzzle earns 1–3 stars:
- ⭐ — Completed with 2+ hints used
- ⭐⭐ — Completed with 1 hint
- ⭐⭐⭐ — Completed with no hints

Stars unlock new books on the library shelf.

### The Reading Owl Companion
The player's owl companion (named by the player at start) grows and changes as progress is made:
- Earns accessories: hats, scarves, glasses, wings
- Reacts emotionally to player performance — celebrates, looks curious, cheers
- Can be renamed and reskinned via unlockable themes

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
- **Manual** (child presses hint button): deducts from `hint_count`
- `hint_count` minimum: 3 per puzzle, regardless of difficulty

### Sticker Collection
Each book completed adds stickers to the player's "Reading Journal" — an in-game scrapbook. Stickers are themed around the book's content (animals, objects, characters).

### Reading Journal
A persistent, visual record of:
- Books read and % completion
- Favorite words collected (player can "keep" any word they like)
- Star totals per book
- Badges earned (e.g., "Found 100 words!", "Night Owl Reader!")

### Achievement Badges
| Badge | Trigger |
|---|---|
| First Word! | Find first word ever |
| Bookworm | Complete first book |
| No Hints Needed | Complete a puzzle without hints |
| Speed Reader | Complete a puzzle under time limit |
| Library Card | Unlock 5 books |
| Word Collector | Save 50 words to journal |
| Language Star | Complete a puzzle in a second language |

---

## 8. Visual Effects & Feedback

### Design Philosophy
For ages 4–9, feedback must be **immediate (< 200ms)**, **visually clear**, and **emotionally warm**. Avoid red X marks or harsh failure indicators. Use redirection and encouragement instead.

### Success Effects (Word Found)
- **Sparkle Burst:** The found word emits a burst of colored sparkles matching the book's color palette.
- **Word Flight:** The word physically lifts from the passage and floats into its word bank slot.
- **Letter Pop:** Each correct letter tile bounces in sequence with a soft pop sound.
- **Star Rain:** On puzzle complete, 1–3 stars fall from the top of the screen with a gentle chime.
- **Owl Dance:** The Reading Owl bounces and flaps wings on word found; performs a full celebratory dance on passage complete.

### Encouragement Effects (Wrong Attempt)
- **Gentle Wobble:** Wrong answer tiles wobble and return to position. No harsh sound.
- **Owl Hint Nudge:** The owl tilts its head and blinks as if curious — subtly guiding without criticizing.
- **Soft Glow Fade:** Attempted letters briefly glow amber then fade, suggesting "almost."

### Passage Complete Screen
Full-screen celebration:
- Confetti in book-themed colors
- Stars animate in one by one
- Owl performs a unique animation tied to the book theme (e.g., dances with the book's main character)
- New sticker slides in from the side and "sticks" to the journal with a satisfying thwap

### Effect Variety System
To prevent repetition fatigue, celebrate effects are drawn from a randomized pool per session:
- 5 sparkle color palettes per book theme
- 3 owl celebration animations
- 4 confetti patterns
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
- Bookshelves with glowing available books, faded locked books
- Owl companion seated or animated in corner
- Top bar: stars collected, player name, settings icon
- Large, friendly "PLAY" or "READ" button for youngest players

#### Passage View Screen
- Left panel (60%): Book passage in large, readable font. Active words subtly shimmer.
- Right panel (40%): Puzzle area (grid / tiles / blanks)
- Bottom: Word bank targets, Owl hint button, audio replay button
- Top: Book title, passage number, exit to library

#### Responsive Breakpoints
| Device | Layout |
|---|---|
| Mobile portrait (phones) | Stacked: passage on top, puzzle on bottom; swipe to switch |
| Tablet / iPad | Side-by-side (passage left, puzzle right) |
| PC / Web 1080p | Full side-by-side with decorative book frame |
| Web 720p | Condensed side-by-side |

### Theme System (Modding-Friendly)
The UI is skinned via **Theme Packs** — JSON + asset bundles that override:
- Color palette tokens (background, text, primary, accent, shadow)
- Font family (must be included in pack; default: Nunito / Comic Neue)
- Owl character sprite sheet
- Background scene illustration
- Button / tile sprite frames
- Particle effect color overrides

**Built-in themes at launch:**
| Theme | Description |
|---|---|
| Cozy Library (default) | Warm browns, amber, cream. Classic bookshelf aesthetic. |
| Enchanted Forest | Deep greens, purples, firefly particles. |
| Ocean Voyage | Blues, teals, wave animations. |
| Space Station | Dark blue, neon, star particles. |
| Classroom Chalk | Simple, high-contrast, teacher-friendly. |


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
| Book unlock | Page turn + brief fanfare |
| Sticker earned | Satisfying sticky-paper sound |
| Button tap | Soft click / thump |

### Text-to-Speech (TTS) System
- All passage text must be readable by TTS engine or pre-recorded audio.
- **Fallback order:** Pre-recorded audio → Platform TTS (OS-native) → in-engine TTS library.
- TTS speed should be adjustable (0.75x, 1x, 1.25x) — important for early readers.
- Word highlight synced to TTS playback (karaoke-style word highlighting during read-aloud).

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
- **Launch Languages:** English (en), Spanish (es).
- **Modding:** Any community member can submit a locale file; framework handles it automatically.

### RTL Language Support
The UI layout engine must support `direction: RTL` flag for Arabic, Hebrew, and Urdu book packs added by modders.

---

## 12. Teacher & Parent Tools

### Parent Dashboard (in-app)
Accessible via PIN or password set at first launch. Shows:
- Time spent reading today / this week
- Books completed
- Words found total
- Puzzle accuracy over time (simple chart)
- Difficulty profile settings

### Teacher Book Upload Flow (No JSON Required)
Teachers can create a playable book pack in under 5 minutes without editing any JSON:

```
Step 1 — Paste or type passage text (plain text area)
Step 2 — Set age range: 4–6 / 6–9 (dropdown)
Step 3 — Pick puzzle types (checkboxes: Word Glow, Scramble, Word Hunt, etc.)
Step 4 — System auto-generates targets via PuzzleGenerator
Step 5 — Preview renders exactly as it will appear in-game
Step 6 — Optional: tap any word in the preview to remove it from the target list
Step 7 — "Save Pack" → downloads pack.zip → teacher drops into /mods folder
```

This flow is powered entirely by `targets: "auto"` under the hood. The resulting `pack.zip` is a valid modding pack identical in format to hand-authored packs. Teachers with JSON knowledge can open and extend it manually.


> ** Design Note: Future Distribution System — Classroom Codes **
> 
> To simplify classroom deployment,
> future versions may support loading Book Packs via short codes.
> 
> Example workflow:
> 
> Teacher publishes a pack online and receives a short code.
> Students enter the code in the game.
> The pack is downloaded automatically.
> 
> This removes the need to manually copy files to each device.
> 
> Planned milestone: M4.

---

## 13. Modding System

### Overview
READCRAFTERY is built on the principle that **content = mods**. Even the built-in books use the same modding format. This means the modding system is fully validated by shipping with it.

### Two Modding Layers

#### Layer 1: Content Mods (Books & Puzzles)
Anyone can create a Book Pack by authoring a folder of JSON + assets.

**Book Pack Validator Tool**
A standalone desktop/web tool (ships with the game, also available at readcraftery.io) that:
- Lets modders preview their book pack exactly as it will appear in-game
- Validates JSON schema and reports errors with clear messages
- Generates a `pack.zip` ready to upload to itch.io or the community hub

**Distribution**
- Packs uploaded to itch.io as "READCRAFTERY Book Pack" tag
- In-game mod browser (Phase 2) lets players browse and install packs with one click
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
│   └── ProgressManager.gd      ← Singleton: stars, journal, achievements
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
│   ├── Celebration/            ← Passage complete screen
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
- Supports multiple profiles (up to 4) — useful for siblings sharing a device
- Save includes: current book progress, stars, journal, settings, active theme

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
    "active_theme": "cozy_library"
  },
  "progress": {
    "total_stars": 42,
    "books": {
      "little_seed": { "passages_completed": 3, "stars": [3, 2, 3] }
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
class_name IPuzzle extends Control
signal word_found(word: String)
signal puzzle_completed(stars: int)

func initialize(puzzle_def: PuzzleDefinition, passage_text: String) -> void:
    pass  # Abstract — implemented by each puzzle type

func get_hint() -> void:
    pass  # Decrements hint count, reveals partial solution
```

This interface makes it trivial to add new puzzle types without modifying core systems — critical for modding extensibility.

---

## 18. Concept Art Descriptions

*(These descriptions serve as briefs for an artist. An AI image generation tool such as Midjourney or Stable Diffusion, or a commissioned artist, should produce these assets.)*

### Scene 1: The Great Library (Main Menu)
**Style:** Warm 2D illustrated, slightly isometric perspective. Think "cozy illustrated children's book." Color palette: ambers, creams, warm reds, soft gold lighting from a fireplace off-screen. Art style reference: Studio Ghibli library scenes meets Duolingo playfulness.

**Contents:** Floor-to-ceiling bookshelves with softly glowing books. A round reading table center-frame. A large owl (the companion) perched on a stack of books, blinking slowly. Books that are unlocked have a golden shimmer. Locked books are dust-covered with a small padlock. Stars float gently around the room.

---

### Scene 2: Puzzle View — Word Glow Mode
**Style:** Clean split-screen. Left side: a parchment-textured text panel with a large, friendly passage. One word glows with a golden pulse. Right side: the target word card with an illustration of the word (e.g., a drawing of a tree for the word "tree"). Bottom: a wide word bank strip.

**Visual accent:** When the player taps the correct word in the passage, it lifts off the page in a sparkle burst and flies to the word bank.

---

### Scene 3: Celebration Screen
**Style:** Full-screen explosion of color. The owl center-screen doing a victory dance. Stars raining down. Confetti in 5 colors spiraling from corners. The earned sticker slides in from the right and "sticks" to a scrapbook visible in the lower corner. Three gold stars animate in one at a time.

---

### Scene 4: Theme Examples
**Enchanted Forest Theme:** Background is a twilight forest. Fireflies replace sparkle particles. Bookshelves wrapped in vines. Owl has green and purple feathers.

**Space Station Theme:** Dark space background with Earth visible through a porthole. Books float in zero gravity. Neon blue UI elements. Owl is an astronaut owl with a tiny helmet.

**Classroom Chalk Theme:** Black/dark green chalkboard background. All UI text looks hand-written in chalk. Simple, high-contrast. Designed for projector display in classrooms.

---

### Scene 5: Mobile Portrait Layout
**Style:** Top 50% of screen: passage text on a parchment panel. Bottom 50%: puzzle tiles in a bright, colorful tray. Swipe up/down gesture indicator subtly visible. Owl is miniaturized to a small avatar icon in the bottom-right corner.

---

## 19. Release Roadmap

### Milestone 0 — Foundation (Month 1–2)
- [ ] Godot 4 project setup, folder structure, scene architecture
- [ ] **Save file schema implemented with `save_version` field** ← Day 0, no exceptions
- [ ] ModLoader core — book pack format finalized and loading
- [ ] Passage view scene — text display + basic TTS
- [ ] Word Glow puzzle — fully functional
- [ ] 1 built-in book (bilingual EN/ES)
- [ ] Basic progression (stars stored locally)
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
| Same stars for auto-generated vs hand-authored puzzles? | **Yes** — player never knows the difference; parity is correct |
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
| Reading Owl | The player's animated companion character |
| Reading Journal | The persistent in-game scrapbook of progress and stickers |
| IPuzzle | The programming interface (abstract class) all puzzle types implement |
| TTS | Text-to-Speech — automated voice reading of game text |
| PuzzleGenerator | Rule-based engine that extracts target words from passage text when `targets: "auto"` |
| Auto-generated puzzle | A puzzle whose targets were produced by PuzzleGenerator, not hand-authored; awards identical stars |

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

*Document End — READCRAFTERY GDD v1.0*  
*Next document: Technical Specification (modding API detail) and Art Style Guide*
