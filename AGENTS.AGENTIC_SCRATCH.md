# Agentic Scratch — Fork of scratch-blocks

> Fork of [scratchfoundation/scratch-blocks](https://github.com/scratchfoundation/scratch-blocks) (2.7K⭐)
> Adds: timeline/MIDI sequencing, genre system, AI block generation, git-native deployment

## The Core Idea

Scratch blocks are arranged on a **horizontal timeline** like MIDI notes, not stacked vertically like code.
Each track is a game element (Player, Enemies, Collectibles, Music). Each beat is a block.
The composition *is* the game — and you can hear it.

## Architecture

```
scratch-blocks (upstream) → Agentic Scratch (our fork)
└── src/
    ├── blocks/          ← Upstream (all 10 categories)
    ├── timeline/        ← NEW: MIDI sequencer mode
    │   ├── Sequencer.ts      ← Beat grid, BPM, time signature
    │   ├── Track.ts          ← One track = one game element
    │   ├── Genre.ts          ← Classical, Jazz, HipHop, Rock, Dance, Acoustic
    │   ├── BeatBlock.ts      ← A block placed on the timeline
    │   └── Player.ts         ← Plays the composition like MIDI
    ├── genres/          ← NEW: Genre templates
    │   ├── classical.ts      ← Puzzle (perfection, minimal moves)
    │   ├── jazz.ts           ← Sandbox (creativity, expression)
    │   ├── hiphop.ts         ← Flow (rhythm, beat accuracy)
    │   ├── rock.ts           ← Action (energy, combos)
    │   ├── dance.ts          ← Party (movement, crowd energy)
    │   └── acoustic.ts       ← Story (emotion, atmosphere)
    ├── ai/              ← NEW: Nebula AI integration
    │   ├── Generator.ts      ← "Generate a level" using reflex engine
    │   └── Completer.ts      ← Auto-complete partial compositions
    └── index.ts          ← Entry point; registers all
```

## Genre → Game Mapping

| Genre | Game Type | Victory Condition | What You Score On |
|-------|-----------|-----------------|-------------------|
| 🎻 Classical | Puzzle | Perfect sequence | Accuracy, minimal moves |
| 🎷 Jazz | Sandbox | Hit target your way | Creativity, unique combos |
| 🎤 Hip Hop | Flow runner | Reach end, keep combo | Beat accuracy, flow |
| 🎸 Rock | Action | Max energy at finale | Combos, big moments |
| 💃 Dance | Party | Keep crowd energy | Move variety, energy |
| 🎵 Acoustic | Story | Complete journey | Atmosphere, emotion |

## How Blocks Become MIDI Notes

In vanilla Scratch, blocks are nested vertically:
```
when [flag] clicked
  move [10] steps
  say [Hello!]
```

In Agentic Scratch, blocks are arranged on a timeline:
```
Beat: | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
Player: [move→] [move→] [jump↑] [move→] [move→] [jump↑]
Music:  [♪beat]                  [♪melody]
Coins:            [💰]                     [💰]
Enemies:                    [⚠️spike]      [⚠️spike]
```

Each block makes a musical note when the composition plays.
You *hear* your game before you play it.

## Agent Guidelines

1. **Timeline mode is additive** — it does not break existing Scratch functionality. Users can switch between "Freeform" (classic Scratch) and "Timeline" (MIDI) modes.
2. **All vanilla Scratch blocks work in Timeline mode.** They just get beat-position metadata.
3. **Genre templates are compositional** — each adds/removes blocks from the palette, changes the play area theme, and modifies victory conditions.
4. **The play button runs both** — the composition audio AND the game simulation. Blocks make sound AND execute logic.
5. **Keep the upstream AGENTS.md rules** — minimal changes, no Blockly edits, fix root causes.
6. **Write tests first** for any new timeline/genre functionality.

## Build

```bash
npm ci
npm run build        # Compiles to dist/main.mjs
npm run test         # Unit + browser tests
```

## Genres vs Scratch Themes

Scratch already has "themes" (classic, cat blocks, high contrast). Our "genres" extend this — they change:
- Block availability (which blocks appear in the palette)
- Play area appearance (background, colors, vibe)
- Win conditions (collect all, reach end, survive, score target)
- Scoring criteria (accuracy, creativity, flow, energy, movement, emotion)
- Sound palette (genre-appropriate musical notes)

## Integration with VoxelWorks Fleet

- **Nebula**: Receives "make me a [genre] game" intents → generates blocks on timeline
- **Cloudflare Workers**: Serves the compiled editor + hosts deployed games
- **GitHub**: Every save is a commit. Every publish is a deploy.
- **I2I**: Agents collaborate on game generation via bottle protocol

## Status

- ✅ Forked scratch-blocks → SuperInstance/scratch-blocks
- ✅ Forked scratch-vm → SuperInstance/scratch-vm
- ✅ Forked scratch-www → SuperInstance/scratch-www
- ⬜ Agentic Scratch prototype built (standalone HTML at voxelworks/agentic-scratch/)
- ⬜ Timeline/MIDI mode in scratch-blocks
- ⬜ Genre templates as scratch-blocks themes
- ⬜ AI block generation via nebula reflex
- ⬜ Git-native deployment in scratch-www
