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
   with status, word count, and remaining memoir slots.

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

Chapter 1 carries the universal city behavioral codes (Los Angeles door
culture, Las Vegas security, Miami sparkle dress codes); Chapter 7 carries the
Sonos pre-flight test.

## Layout

```
.claude/skills/party-princess/
├── SKILL.md                       # orchestrator: modes, workflow, hard rules
├── references/
│   ├── voice.md                   # tone contract, banned phrases, devices
│   ├── chapters.md                # locked spec: titles, beats, sign-offs
│   └── memoir-interview.md        # per-chapter question banks
└── assets/
    ├── chapter-template.md        # structural skeleton
    └── exemplar-prose.md          # gold-standard voice calibration

book/
├── 00-front-matter.md             # title page, thesis, how to read
├── README.md                      # manuscript index + build status
├── chapter-*.md                   # generated chapters
└── .memoir/                       # your verbatim interview notes
```

## Editing the book's DNA

Change the tone in `references/voice.md`. Change what a chapter must cover in
`references/chapters.md` — filenames, titles, and sign-offs are locked there
and the skill copies them character-for-character. Change what you get asked in
`references/memoir-interview.md`.
