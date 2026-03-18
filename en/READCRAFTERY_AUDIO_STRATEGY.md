# READCRAFTERY — Audio Strategy v3.1

**Version:** 3.1
**Date:** March 2026
**Status:** Working document — ready for integration into GDD §10 update
**Aligned with:** Canon Core v0.3 · GDD v1.4 · Art Guide v1.5 · Architecture Contract v1.3 · Build Guide v1.5

**Replaces:** All previous audio strategy versions (v1, v2, v3).

---

## 1. Sound Identity

### The Emotional Arc

Readcraftery's audio is not static ambiance. It reflects the state of a living place
that begins dormant and progressively reawakens through the act of reading.

The child arrives to a library that is sleeping — not dead, not empty, but veiled.
Owlorumo is present but diminished. His crystal is dark. The books are quiet.
As reading restores fragments of light, the place begins to answer.

The audio must carry this arc. What the child hears at game start should feel
meaningfully different from what they hear after completing their first book —
not because the soundtrack changed, but because the same musical identity
became more complete.

**Reference:** Canon Core §2 (The Library), §4 (Crystal, eyes, and library response),
§5 (Restoration philosophy — "reopens a living continuity").

### Four Words

**Warm.** Acoustic instruments. Piano, soft strings, woodwinds, harp, cello.
Low-end warmth from cello or double bass, never from bass synth.
No synthetic aggression.

**Present.** Audio should feel like it's in the room — close-mic'd, intimate.
The library is a physical place with walls, wood, candles, rain outside a window.
Sound reinforces that physicality.

**Breathing.** Natural pauses and dynamic variation. Not a wall of constant sound.
Silence is an active design tool — especially during reading and during
the most important emotional moments (see §2 Layer 4).

**Nostalgic.** Owlorumo starts diminished and veiled, sensing that something
important has dimmed and must not be lost. The music carries a thread of
gentle melancholy — not sadness, but the weight of things almost forgotten.
This melancholy has direction: it leans toward hope, toward rediscovery,
toward light returning. It is the sound of "not yet lost."

**Reference:** Canon Core §3 (Owlorumo — "he senses that something important
has dimmed and must not be lost"), §6 (Narrative layering).

### References

| Reference | What to take | What NOT to take |
|---|---|---|
| **Studio Ghibli (Hisaishi)** | The quieter moments — Chihiro's train ride, the opening of Howl before anything happens. Nostalgia without sentimentality. | Adventure themes, bombastic orchestration. |
| **Ori and the Blind Forest** | Early sections where the forest is dying. Warmth layered with loss. A world that remembers what it was. | Action sequences, intensity ramps. |
| **Journey (Austin Wintory)** | Cello as a voice of solitary hope. The sense of something vast and lost being slowly recovered through presence. Closest reference to Owlorumo's emotional arc. | The multiplayer interaction layer. |
| **Hollow Knight (Christopher Larkin)** | How music reflects a kingdom that was magnificent and is now diminished but not gone. City of Tears = the Sleeping Library as sound. | Boss fight intensity, darkness. |
| **A Short Hike** | Intimate acoustic scale, playfulness. | Too light/cheerful for Sleeping state. Better reference for Reawakened. |

### What the Sound Is NOT

- ❌ Chiptune / 8-bit — contradicts the "real book" warmth (same logic as text at 1080p vs pixel art sprites — Art Guide §1)
- ❌ Generic "cozy game" — Readcraftery is not a farm sim or a café. The warmth comes from a deeper place.
- ❌ Competitive/tense — no timers, no urgency beats, no rising intensity
- ❌ Triumphant fantasy — restoration is quiet, personal, internal. Never epic.
- ❌ Plastic/synthetic UI — no generic mobile game clicks
- ❌ Harsh error sounds of any kind — contradicts Owl protocol ("No red X. No error sound." — GDD §8)
- ❌ Vocal samples in music — distracts from TTS and reading
- ❌ Heavy percussion — creates pressure
- ❌ Music that fills every moment — the most powerful moments are defined by designed silence

---

## 2. Audio Layers

### Layer 1: Music — Evolves with Restoration

The music is not a collection of unrelated loops. It is a **single musical identity
with variants by restoration state and scene context.**

In practice this means multiple coherent pieces that share melodic material,
harmonic language, and instrumentation palette — not literally one track with layers,
but a family of pieces where the Beginnings version is recognizably the complete
form of what was only hinted at in the Sleeping version.

**Reference:** Canon Core §5 — "Restoration does not return the world to a pristine
original state. It reopens a living continuity." The music itself must undergo
restoration, not replacement.

**Production approach:** Compose the full theme (Library of Beginnings version) first.
Then strip layers to create the Sleeping and Reawakened versions.
This ensures organic continuity across states.

> **Scope protection:** M1 minimum acceptable state is the Sleeping state well
> resolved — one Library loop, one Reading ambient, one Puzzle texture.
> Reawakened and Beginnings can start as reduced arrangements or light
> variations (additional stem, warmer pad, slightly fuller mix), not as
> entirely new compositions. Full production of all three states is M1 final
> or later. Do not let music production block M1 technical.

#### The Sleeping Library (state_0, state_1)

The child arrives to a place that is waiting.

| Context | Character | Notes |
|---|---|---|
| Library Scene | Dormant, veiled, ancient. A place that breathes but doesn't answer yet. | Solo piano or solo cello. Very sparse. Long silences between phrases. Fragments of melody that don't quite resolve — the music itself is "remembering" something it can't reach. Subtle low-register warmth. Optional ambient: distant rain, soft clock. 2–4 min loop. |
| PassageView | Focused, subordinate. Protected reading space. | Near-silence. A single sustained pad at the edge of hearing. Fades further during TTS. The parchment is the center. 2–3 min loop. |
| Puzzle Active | Gently engaged, inviting. | Slightly more present than reading but still sparse. Soft pizzicato or music box — something small and delicate. Not urgent. 1–2 min loop. See Reading Protection Rule below. |

#### The Reawakened Library (state_2, state_3)

The place begins to answer.

| Context | Character | Notes |
|---|---|---|
| Library Scene | Warmer, more present, inhabited. The library responds. | Solo instrument gains a companion — piano + soft strings. The melody fragments from Sleeping state start connecting. Warmer ambient: fire crackle joins rain. The hum of the library is now gentle presence, not distant echo. |
| PassageView | Still subordinate but safer. The quiet feels more held. | Same near-silence, but the pad has more harmonic richness. |
| Puzzle Active | Curious, gently encouraged. | Woodwind joins the pizzicato. Still subject to Reading Protection Rule. |

#### The Library of Beginnings (state_4)

The deeper truth of the place. Not a pristine return — renewed continuity.

| Context | Character | Notes |
|---|---|---|
| Library Scene | Full, alive, continuous. Hope realized. | The complete theme — all fragments connected into a real melody. Piano + strings + woodwinds + harp. Still breathing, still warm, but with a sense of arrival. Not triumphant — *fulfilled*. The music doesn't become a different piece. It becomes the complete version of what was always there. |

**Estimated music files for M1 minimum:** 3 (library_sleeping, reading_sleeping, puzzle_sleeping).
**For M1 final / M2:** additional 3–6 variants for Reawakened and Beginnings states.

### Reading Protection Rule

This is a non-negotiable pedagogical constraint on all audio during reading
and puzzle interaction.

1. **No melodic hooks during active reading.** Music must not plant a melody
   in the child's working memory while they are decoding text.
2. **No strong transients during target search.** No percussive hits, no sudden
   dynamic changes that break concentration.
3. **No sound may imply failure or urgency.** Not during puzzle, not during
   reading, not ever.
4. **Puzzle music must never introduce pulse, rhythm, or melodic motion
   strong enough to compete with word recognition.**
5. **Silence is preferred over decorative audio when in doubt.**

### Owlorumo's Audio Presence Rule

**Owlorumo's audio presence supports reading; it never competes with
the child's reading task.**

His TTS lines are short (max one sentence at any level). His non-verbal
sounds are soft and brief. His crystal pulse is ambient, not foreground.
When the child is actively reading or searching, Owlorumo is sonically
subordinate to the text.

### Layer 2: Sound Effects — Mapped to Architecture Contract Events

Every SFX is tied to a specific signal or event already defined in the docs.
No orphan sounds. No sounds without a contract.

Two categories of feedback are distinguished:

- **Book awakening** — a local event. One specific book responds. The sound
  is intimate and contained: a breath, a soft resonance, the book "exhaling"
  after a long sleep.
- **Library response** — a systemic/ambient event. The environment shifts.
  Warmer light in the ambient texture, a subtle change in the music mix,
  the sense that the room itself noticed. This is not a discrete SFX but
  a gradual shift in the ambient layer.

These are different assets with different purposes. Do not conflate them.

#### Core SFX (M0 — 5 sounds minimum)

| Event / Signal | Sound Character | Duration | Source doc |
|---|---|---|---|
| `word_found` | Soft chime with faintly crystalline quality — a fragment of light returning. Connected to crystal resonance, not generic UI. | 0.5–1 sec | GDD §10, Contract #2 |
| `puzzle_completed` | Warm bloom that opens and folds gently. Think candle lighting, not firework. Followed by fragment-flight sound. | 1–2 sec | GDD §8, Contract #3 |
| Fragment arrival pulse | Soft crystalline whisper that moves (panning or pitch shift) and arrives at the crystal. Absorbed. 3 intensity variants matching completion tier. | 1–1.5 sec | GDD §8 "fragments of white-gold light flying to staff crystal" |
| Button tap | Soft wooden thump — book spine tap or leather-on-wood. Physical, not digital. | 0.1–0.2 sec | GDD §10 |
| TTS play button | Subtle "book open" — paper and air. | 0.3 sec | GDD §10 |

#### Extended SFX (M1 — additional ~8 sounds)

| Event / Signal | Sound Character | Duration | Source doc |
|---|---|---|---|
| Scaffolding cue | Soft ambient tone — signals Owl is preparing to help. NOT error. NOT alarm. A gentle "I'm here." | 0.5 sec | GDD §10, Contract #4b |
| Book awakening | Not a page turn. Something local shifted — a soft resonance, a breath. The book "exhales" after a long sleep. Intimate and contained. | 1–2 sec | GDD §10 |
| Crystal pulse (idle) | Soft, rhythmic. 0.8Hz. Barely perceptible. Like a heartbeat at the edge of hearing. | 0.3 sec (loopable) | Art Guide §3 "pulses at 0.8Hz in idle" |
| **Crystal ignition** | **See Layer 4 below — designed from scratch.** | 3–4 sec | Build Guide §8 |
| Letter placed (Scramble) | Gentle pop. | 0.2 sec | GDD §10 |
| Navigation back | Gentle page turn. | 0.3 sec | — |
| Hover/pre-select | Very subtle paper rustle. | 0.1 sec | — |
| `owl_excited` vocalization | Very brief warm exhale with avian quality. Not a full hoot — a gesture. | 0.3 sec | Contract #7c |

#### Deferred SFX (M2+)

| Event | Sound Character | Reason for deferral |
|---|---|---|
| Sticker earned | Satisfying sticky-paper sound. | Journal = M2 |
| Hidden Book appears | Barely audible displacement of air — book placed by unseen hand. | Hidden Books = M1+ |
| Hidden Book withdrawal | Silence. Owlorumo notices visually. No sound. | Canon Core §10 |
| Owlorumo early_emergent "magic sound" | **Deferred — nature TBD pending crowdfunding.** | GDD §Owl Adaptive Language |

### Layer 3: Owlorumo's Voice (TTS)

Owlorumo's primary sound identity is his **spoken voice**, not a hoot or SFX.
He speaks. The complexity adapts to `reading_stage`.

**Reference:** Canon Core §7, GDD §Owl Adaptive Language (✅ CLOSED).

| `reading_stage` | What the child hears | Audio implementation |
|---|---|---|
| `early_emergent` | Single words or exclamations: "That one!" / "Yes!" | TTS with short strings from locale file. |
| `developing` | Short complete sentence: "You found 'seed'!" | TTS with template strings. |
| `fluent` | Word origin or usage: "'Seed' comes from 'to sow'. Well done!" | TTS with richer strings. |

**TTS ducking rule:** Music ducks aggressively during TTS playback until spoken
words remain effortlessly intelligible. Initial default: music volume reduces to
~20% of current level. This value is a starting point to be validated on
real hardware (tablet speakers, Chromebook speakers, cheap earbuds) and adjusted
per platform if necessary.

Implementation: call `AudioServer.set_bus_volume_db("Music", -14.0)` before
`DisplayServer.tts_speak()`, restore after TTS finishes.

**Critical technical note:** `DisplayServer.tts_speak()` does **not** route audio
through Godot's AudioServer. It is an OS-level API. This means:

- The Voice/TTS bus in the AudioBus layout is conceptual for pre-recorded
  passage audio only. Runtime TTS bypasses it entirely.
- TTS volume is controlled only via the `volume` parameter (0–100) passed
  to `tts_speak()`, not via bus volume.
- Ducking cannot be reactive (listening to TTS bus activity). It must be
  done by timing: duck music BEFORE calling `tts_speak()`, restore AFTER
  `DisplayServer.tts_is_speaking()` returns false (poll or timer).
- TTS behavior, latency, and volume vary across platforms (Web, Android, iOS,
  desktop). Test on each target. Do not assume uniform behavior.

**Non-verbal Owlorumo sounds (secondary):**

The hoot is a gesture, not the identity. It plays in situations where Owlorumo
reacts without speaking:

- Slow blink during idle (trust signal) — **no sound. Silence IS the design.**
- Accompaniment gesture (inactivity, crystal soft pulse) — crystal pulse SFX only.
- `owl_excited` animation — very brief warm vocalization (0.3 sec).

### Layer 4: Designed Silence

These moments are defined in the docs as silent or near-silent.
Silence here is not the absence of design — it IS the design.

#### The Crystal Ignition (state_0 → state_2)

> "No text. No UI. No sound except the crystal pulse." — Build Guide §8
>
> "He looks at them. Two seconds of silence.
> The child understands — without anyone explaining — that they did this." — GDD §8

Audio design for this moment:

1. All music stops. Complete silence. (0.5 sec)
2. The crystal pulse sound begins — a new, unique sound not heard before.
   **Designed from scratch.** Low, singular tone (glass harmonica or bowed metal)
   that slowly gains harmonics over 3–4 seconds. It must feel like light
   becoming sound. Not dramatic — *intimate*. As if something that was
   always there finally found its voice.
3. Owlorumo looks at the child. The pulse sustains softly. (2 sec)
4. The library ambient resumes at Reawakened level — imperceptibly warmer
   than what was playing before.

This sound plays **exactly once per save file**. It is non-repeating.
It is the most important audio asset in the game.

#### Other Designed Silences

| Moment | Why silence | Source |
|---|---|---|
| Owl slow blink (idle) | Trust signal — sound would break it | Art Guide §3 |
| Hidden Book withdrawal | "a glance toward that shelf, a moment of stillness" | Canon Core §10 |
| Owlorumo Memory fragments | The rarest Hidden Book type. TTS only, no music. | Canon Core §9 |
| Dormant book — child touches it | It simply does not respond. No sound confirms this. | GDD §4 "A dormant book simply does not respond." |
| Incorrect word selected | No error sound. Owl reads both words via TTS. | GDD §Owl Protocol (✅ CLOSED) |

### Layer 5: Ambient Texture (M2+)

Subtle environmental sound layered under music:
- Library: distant rain, soft fire crackle, clock tick, wood settling
- Not music — texture. 5–10 sec loops, very low volume.
- Relevant once Library scene has real art. Skip for M0/M1.
- Rain is already suggested in Art Guide §4: "Large window at the back —
  soft rain or starry night, depending on the time."

---

## 3. Free Sources — Evaluated

### Tier 1: CC0 (no attribution required)

**Kenney Audio Packs** — kenney.nl/assets (CC0)
- **UI Audio** (50 sounds) — clicks, switches. Good M0 placeholder for button_tap.
- **Interface Sounds** (100 sounds) — more variety. Same style.
- **RPG Audio** (50 sounds) — chimes, magic effects. Candidates for word_found and fragment SFX.
- Already packaged for Godot on the Asset Library.
- **Verdict:** M0 placeholder source. Cherry-pick 5–10. Replace for M1 final.

**Pixabay Sound Effects** — pixabay.com/sound-effects
- Large library. Good for specific organic sounds (page turn, bell, chime).
- License is permissive (royalty-free, no attribution for most).
- Check individual asset terms for commercial use.

**Blacis Fantasy Music Mega Pack** — itch.io (CC0)
- 100+ free songs. Variable quality. Some ambient/calm tracks could work
  as basis for Library Sleeping state if carefully selected.

### Tier 2: CC-BY (attribution required — fine for NOTICE file)

**Soundimage.org** by Eric Matyas (CC-BY)
- Enormous library in OGG format. Fantasy "wonder" and "calm" subcategories
  fit Readcraftery's tone.
- Consistently good quality. Some tracks too epic — filter for sparse/intimate.
- **Verdict:** Best free source for Library and Puzzle music.

**YannZ Contemplative Fantasy Pack** (CC-BY, OpenGameArt)
- Designed for "story-driven or cozy games." Inspired by Zelda, Ori, Ghibli.
- Includes main menu theme, modular 1-minute in-game loops, credits theme.
- OGG included. All at 120 BPM.
- **Verdict:** Audition first. May cover reading/puzzle contexts.

**OpenGameArt CC0 Fantasy Music & Sounds collection**
- Curated collection of high-quality fantasy tracks (no chiptune).
- Mixed licenses within collection — verify per track.

### Tier 3: Paid but affordable

**itch.io cozy/fantasy music packs** — $5–$15 range
- Multiple packs tagged "cozy" or "fantasy ambient."
- One-time purchase, royalty-free.
- **Budget:** $20–$30 total if free options don't fit.

### Recommendation by Milestone

| Need | Source | Cost | Milestone |
|---|---|---|---|
| M0 placeholder SFX (5 sounds) | Kenney UI Audio + RPG Audio | Free (CC0) | Now |
| word_found chime | Kenney RPG Audio or Pixabay | Free | Now |
| Library Sleeping music | Soundimage.org calm/wonder or YannZ | Free (CC-BY) | M1 |
| Reading ambient pad | Soundimage.org or custom drone | Free (CC-BY) | M1 |
| Puzzle texture | YannZ modular loops | Free (CC-BY) | M1 |
| Crystal ignition sound | Custom — designed from scratch | $0 (self) or $20–$50 (commission) | M1 |
| Reawakened/Beginnings layers | Composed or commissioned | $0–$100 | M1 final+ |
| early_emergent "magic sound" | TBD — deferred pending crowdfunding | — | Post-M1 |

**Total audio budget M0→M1: $0–$50.** Full custom music: $100–$300 if commissioned.

---

## 4. Technical Specs

### Build Size Budget

- Godot WASM: ~10MB (fixed)
- Total content budget: ~5MB
- **Audio budget: ~1MB maximum** for HTML5 build

Breakdown:
- Music: 3–4 loops at OGG 96kbps ≈ 600–800KB
- SFX: 12–15 short sounds at OGG 96kbps ≈ 100–200KB
- TTS: runtime (OS-native), no file cost

### Format

- **Music:** OGG Vorbis, 96kbps, mono or stereo, loopable
- **SFX:** OGG Vorbis, 96kbps, mono, short (< 2 sec each)
- **Never WAV** in production builds. WAV only for source/editing.
- All audio in `res://audio/music/` and `res://audio/sfx/`

### Godot AudioBus Layout

```
Master
├── Music        (default: -6dB, ducks during TTS — see §2 Layer 3)
├── SFX          (default: 0dB)
├── PassageAudio (default: 0dB — for pre-recorded .ogg narration only)
└── Ambient      (default: -12dB, M2+)
```

**Note:** Runtime TTS (`DisplayServer.tts_speak()`) does NOT route through
any Godot AudioBus. It is OS-level audio. Volume controlled only via the
`volume` parameter in the API call. See §2 Layer 3 technical note.

Each bus independently controllable from Settings.

### Loop Points

OGG files in Godot support seamless looping via import settings:
- Import → Audio → Loop: ON
- Set loop begin/end if the track has a non-repeating intro

---

## 5. Theme Audio Override (M2+ — architecture note only)

Themes may optionally override music tracks. To enable this without M2 work:

**Do now:** Load music by path string, not by hardcoded `preload()`.
Store default paths as constants in AudioManager.

**Do in M2:** `theme.json` includes optional `"audio"` block:
```json
{
  "audio": {
    "music_library": "audio/my_library_theme.ogg",
    "music_reading": "audio/my_reading_ambient.ogg"
  }
}
```
If absent, default theme audio plays. No extra work from theme authors.

**Do not build this now.** Just don't hardcode paths.

---

## 6. Audio Asset Naming Convention

Consistent with project naming (Art Guide §5, Asset Contracts, snake_case).

### Music

```
music_library_sleeping.ogg
music_library_reawakened.ogg
music_library_beginnings.ogg
music_reading_sleeping.ogg
music_reading_reawakened.ogg
music_puzzle_sleeping.ogg
music_puzzle_reawakened.ogg
```

### SFX

```
sfx_word_found.ogg
sfx_puzzle_complete.ogg
sfx_fragment_arrival.ogg          (3 variants: _soft, _moderate, _intense)
sfx_button_tap.ogg
sfx_tts_play.ogg
sfx_scaffolding_cue.ogg
sfx_book_awakening.ogg
sfx_crystal_pulse.ogg
sfx_crystal_ignition.ogg
sfx_letter_placed.ogg
sfx_navigation_back.ogg
sfx_hover.ogg
sfx_owl_excited.ogg
```

No use of `star`, `reward`, `score`, `error`, or `wrong` in any audio asset name.

---

## 7. Documentation Plan

### Update GDD §10

Replace current §10 with content from this document:
- Sound Identity (4 words + references + avoids)
- Reading Protection Rule
- Audio Event Table (mapped to Architecture Contract signals)
- Music restoration arc (Sleeping → Reawakened → Beginnings)
- Crystal ignition audio design
- Designed silences
- TTS ducking rule + technical note
- Technical specs (format, size budget, bus layout)

### Add to Architecture Contract §4

Audio feedback column in Event Contract Table:

| Signal | Audio response |
|---|---|
| `word_found` | `sfx_word_found` (SFX bus) |
| `puzzle_completed` | `sfx_puzzle_complete` + `sfx_fragment_arrival` (SFX bus) + music crossfade |
| `owlorumo_state_upgrade_ready` | `sfx_owl_excited` + celebration TTS line |
| `scaffolding_requested` | `sfx_scaffolding_cue` (SFX bus) |
| `passage_started` | Music crossfade to reading level; TTS begins; Music bus ducks |
| Incorrect word | No SFX. Owl reads both words (TTS only) |
| Inactivity auto-trigger | Owl reads + syllabifies (TTS only) |

### Add to Asset Contracts

| asset_id | format | max_size | duration | bus | milestone |
|---|---|---|---|---|---|
| `music_library_sleeping` | OGG 96k | 300KB | 2–4 min loop | Music | M1 |
| `music_reading_sleeping` | OGG 96k | 200KB | 2–3 min loop | Music | M1 |
| `music_puzzle_sleeping` | OGG 96k | 200KB | 1–2 min loop | Music | M1 |
| `music_library_reawakened` | OGG 96k | 300KB | 2–4 min loop | Music | M1 final |
| `sfx_word_found` | OGG 96k | 30KB | 0.5–1 sec | SFX | M0 |
| `sfx_puzzle_complete` | OGG 96k | 50KB | 1–2 sec | SFX | M0 |
| `sfx_fragment_arrival` | OGG 96k | 40KB | 1–1.5 sec (×3 variants) | SFX | M0 |
| `sfx_button_tap` | OGG 96k | 10KB | 0.1–0.2 sec | SFX | M0 |
| `sfx_tts_play` | OGG 96k | 15KB | 0.3 sec | SFX | M0 |
| `sfx_crystal_ignition` | OGG 96k | 100KB | 3–4 sec | SFX | M1 |
| `sfx_crystal_pulse` | OGG 96k | 15KB | 0.3 sec (loop) | SFX | M1 |
| `sfx_scaffolding_cue` | OGG 96k | 20KB | 0.5 sec | SFX | M1 |
| `sfx_book_awakening` | OGG 96k | 50KB | 1–2 sec | SFX | M1 |
| `sfx_owl_excited` | OGG 96k | 15KB | 0.3 sec | SFX | M1 |

---

## 8. Implementation Order

### M0 (current)

1. Create `res://audio/sfx/` and `res://audio/music/` directories
2. Download Kenney UI Audio + RPG Audio packs (CC0)
3. Pick 5 placeholder sounds: `sfx_button_tap`, `sfx_word_found`, `sfx_puzzle_complete`, `sfx_fragment_arrival`, `sfx_tts_play`
4. Place as OGG in `res://audio/sfx/`
5. Wire `AudioManager.play_sfx()` to real files
6. **No music yet.** Silence is better than wrong music.
7. Ensure music paths are loaded by string constant, not `preload()` (M2 theme prep)

### M1 Technical

1. Audition YannZ and Soundimage.org for Library + Reading music
2. Select or trim loops for Sleeping state only. Convert to OGG 96kbps.
3. Implement AudioBus layout (Master → Music / SFX / PassageAudio / Ambient)
4. Implement music ducking during TTS (timing-based, not bus-reactive — see §2 Layer 3)
5. Replace placeholder SFX with curated or better sounds
6. Design `sfx_crystal_ignition` (custom — most important audio asset)
7. Design `sfx_crystal_pulse` (0.8Hz idle, 0.3 sec loop)
8. Test on HTML5: verify audio plays, verify build size under 1MB
9. Test TTS ducking on tablet speakers, Chromebook, earbuds — adjust default if needed

### M1 Final

1. Produce Reawakened music variants (reduced arrangements from Sleeping, not new compositions)
2. Final audio mix — balance buses for classroom and headphone
3. Settings screen: independent volume sliders for Music, SFX, Voice
4. Classroom mode defaults (see §9)
5. Verify Reduced Motion mode doesn't break audio
6. Verify "No error sound" rule holds across all puzzle types

### M2+

- Beginnings music variants (full ensemble version)
- Ambient texture layer (rain, fire, clock)
- Theme audio override system
- Sticker/Journal SFX
- Hidden Book SFX
- Library response ambient shifts
- early_emergent "magic sound" (pending crowdfunding decision)

---

## 9. Classroom Mode

Teachers will use Readcraftery on projectors and shared devices.

**Defaults for classroom profile:**
- Music: OFF
- SFX: low-to-medium (validate on real hardware before fixing a number)
- Voice/TTS: 100%
- Single toggle to mute all audio (accessible from any screen)

**Reference:** GDD §12 (Classroom & Caregiver Use), GDD §10 (Audio Accessibility).

---

## 10. The 8-bit Question

The pixel art visual style might suggest chiptune music. **No.**

The Art Guide §1 establishes that text renders at 1080p native resolution
while sprites are pixel art at 48×48 scaled 4×. The contrast is intentional:
"the pixel grid is the medium, not the message."

The same logic applies to audio: warm, acoustic music reinforces that
the reading experience is real. The pixel art world is the magical layer
around it. Chiptune would collapse both into "retro game."

The sound must feel like it comes from the library, not from a console.
