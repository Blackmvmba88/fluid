# fluid

**fluid** is a living pixel-fluid audiovisual engine for the BlackMamba ecosystem.

It is not just a visualizer. It treats a visual state as a reproducible organism that can be saved, replayed, mutated, crossed with another preset and driven by live audio.

> A pixelated fluid where the sine wave comes alive like a cobra.

## Core model

```text
Visual Organism
  = Visual DNA
  + Runtime State
  + Audio Features
  + Mutation Rules
  + Rendering Backend
```

The engine should remain useful whether the source is:
- microphone input;
- a song from MEngine;
- oscillator / sine-wave data;
- offline rendered features;
- manually authored control signals.

## Why this exists

Most visualizers are disposable render states. `fluid` makes them addressable and reproducible.

A preset can become:
- a known visual identity for a track;
- a live-performance scene;
- a mutation parent;
- a cross between two visual organisms;
- an exportable piece of visual metadata.

## Initial architecture

```text
audio/features
      ↓
normalization
      ↓
visual DNA ─── mutation / crossover
      ↓
runtime state
      ↓
renderer
      ↓
frames / live output
```

See:
- [Architecture](docs/ARCHITECTURE.md)
- [Visual DNA](docs/VISUAL_DNA.md)
- [Roadmap](docs/ROADMAP.md)
- [Visual DNA schema](specs/visual-dna.schema.json)

## BlackMamba integration

`fluid` is intended to interoperate with:
- **MEngine** for music intelligence and track-level context;
- **Onda Sinusoidal Reactiva** for signal-driven visual primitives;
- **Rainbow Mic Scope** for microphone/spectrum features;
- **BlackMamba Paint** for image/texture generation and visual composition;
- future live-performance and video pipelines.

The integration contract should be data-first: other projects provide normalized features; `fluid` renders and evolves visuals without owning the whole audio pipeline.

## Foundation status

Current repository stage: **architecture / specification seed**.

The next implementation target is a minimal deterministic renderer that can:
1. load one Visual DNA document;
2. accept normalized audio features;
3. render a repeatable state transition;
4. mutate one parameter under a seeded random source;
5. serialize the resulting organism.
