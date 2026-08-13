# princessguide

A Claude Code custom skill that co-authors and auto-compiles the multi-chapter
lifestyle book **How to Party Like a Princess** as markdown, straight into this
project directory.

> True princesses don't outsource logistics — they master them.

## Usage

From Claude Code in this repo:

```
/party-princess              # status table, then pick a chapter
/party-princess all          # full build, chapter by chapter
/party-princess 3            # build or rebuild Chapter 3
/party-princess transport    # same, by slug
/party-princess revise 4     # revise an existing chapter in place
/party-princess interview 2  # collect anecdotes only, no prose
/party-princess draft 5      # skip the interview, leave placeholders
/party-princess compile      # regenerate the index and front matter
```

## Sounding like you, not like a robot

Everything in [`voice/`](voice/) is the voice knowledge base. The skill reads it
before writing a single line, and never edits it.

Generic writing happens when a writer knows the *category* but not the
*instance*. "A trendy nightclub" is category. The room you actually go to, on
the night you actually go, is instance — and instance can't be guessed. So:

| File | What it holds |
|---|---|
| [`voice/samples.md`](voice/samples.md) | Raw things you've written — texts, captions, voice notes. **The highest-value file here.** |
| [`voice/world.md`](voice/world.md) | Your venues, cities, brands, drink order, songs, crew, tipping numbers |
| [`voice/verdicts.md`](voice/verdicts.md) | Your opinions, ethics, hills to die on |
| [`voice/lexicon.md`](voice/lexicon.md) | Your phrases, your sentence habits, words you'd never say |
| [`voice/quotes.md`](voice/quotes.md) | Lines you write yourself, for epigraphs and pull quotes |

There's a 20-minute fast path in [`voice/README.md`](voice/README.md). You don't
have to fill any of it in before starting — the skill asks for what it's missing
as it goes.

The skill also triggers on plain requests — "write chapter 4," "let's keep
working on the Princess book."

## How it works

Each chapter runs a three-step loop:

1. **Interview gate.** The skill asks you 2–3 questions about your actual
   nights out and saves your answers verbatim to `book/.memoir/`. This is the
   part that makes it a memoir instead of a listicle. Decline or skip and it
   drops a `MEMOIR PROMPT` block into the prose for you to fill later — it
   never invents your life.
2. **Draft.** Cold open, numbered operational sections with real checklists and
   thresholds, your anecdotes woven in, and a closing **Princess Protocol**
   checklist. 1,400–2,200 words, ending on that chapter's locked sign-off line.
3. **Compile.** Writes the file to `book/` and updates the manuscript index
   with status, word count, and remaining open slots.

### The two kinds of blank

**`> [!MEMOIR PROMPT]`** — a story slot, 150–250 words. Answer it in the
interview and it gets written up for you; skip and the block waits.

**`> [!YOUR QUOTE]`** — an epigraph or pull quote. **Yours to write, always.**
The skill won't draft one even as a placeholder to replace, because a plausible
fake in your own voice is precisely the thing that slips into print unnoticed.
Every chapter opens with one under the title and carries one or two more at its
strongest turns. Bank lines in `voice/quotes.md` whenever they arrive.

## Chapters

| # | File | Sign-off |
|---|------|----------|
| 1 | `book/chapter-1-glowup.md` — The 24-Hour Glow-Up & The Universal City Codes | *Stay shiny, stay shady.* |
| 2 | `book/chapter-2-homebase.md` — The Home Base Sanctuary & The Micro-Purse Arsenal | *Your bag is your vault, darling.* |
| 3 | `book/chapter-3-transport.md` — The Transport Protocol & The Communication Trio | *Never let them see you sit in the front seat.* |
| 4 | `book/chapter-4-clubplaybook.md` — The VIP Playbook & The Romance Variable | *Boyfriends are temporary, VIP tables are forever.* |
| 5 | `book/chapter-5-royaltyrules.md` — Royalty Rules: You Can Be a Princess, But Don't Be Rude | *Manners cost nothing; exclusivity costs everything.* |
| 6 | `book/chapter-6-donts.md` — Emergencies, Curveballs & The Definitive Don'ts | *Tragedies happen, but hot messes are entirely optional.* |
| 7 | `book/chapter-7-afterparty.md` — The After-Party Protocol & The Morning Reign | *XOXO, keep your crown adjusted.* |
| 8 | `book/chapter-8-travel.md` — Quick Travel Tips: Going Out Somewhere That Isn't Home | *Pack light, tip heavy.* |

Chapters 1–7 run chronologically through one night, from twenty-four hours out
to the morning after. Chapter 8 is the other axis — the night that needs a
flight — and runs shorter and denser, 900–1,400 words, built to be read on a
plane.

Chapter 1 carries the universal city behavioral codes (Los Angeles door
culture, Las Vegas security, Miami sparkle dress codes); Chapter 7 carries the
Sonos pre-flight test.

## Layout

```
.claude/skills/party-princess/
├── SKILL.md                       # orchestrator: modes, workflow, hard rules
├── references/
│   ├── voice.md                   # default tone contract — your voice/ overrides it
│   ├── chapters.md                # locked spec: titles, beats, sign-offs
│   └── memoir-interview.md        # per-chapter question banks
└── assets/
    ├── chapter-template.md        # structural skeleton
    └── exemplar-prose.md          # placeholder calibration until samples.md fills up

voice/                             # YOUR knowledge base — read every time, never edited
├── README.md                      # how it works + the 20-minute fast path
├── samples.md                     # raw writing (highest value)
├── world.md                       # venues, brands, drinks, songs, crew, money
├── verdicts.md                    # opinions, ethics, hills to die on
├── lexicon.md                     # phrases, sentence habits, banned words
└── quotes.md                      # your epigraphs and pull quotes

book/
├── 00-front-matter.md             # title page, thesis, how to read
├── README.md                      # manuscript index + build status
├── chapter-*.md                   # generated chapters
└── .memoir/                       # your verbatim interview notes
```

## Editing the book's DNA

`voice/` is yours and outranks everything — anything you put there wins over the
skill's defaults.

Beyond that: change the fallback tone in `references/voice.md`. Change what a
chapter must cover in `references/chapters.md` — filenames, titles, and
sign-offs are locked there and the skill copies them character-for-character.
Change what you get asked in `references/memoir-interview.md`.
