# fluid Architecture

## 1. Design principles

### Deterministic when requested
Given the same Visual DNA, normalized features, seed and time step, the engine should be able to reproduce the same state evolution.

### Audio is input, not ownership
`fluid` should not duplicate MEngine, microphone capture stacks or catalog systems. It accepts normalized feature frames through adapters.

### Renderer independence
Visual DNA describes intent and parameters rather than tying the model to one frontend. A WebGL, Canvas, native or offline renderer may consume the same organism.

### Mutation is explicit
A visual may mutate only through declared mutation rules. Every mutation can record:
- parent id;
- seed;
- parameters changed;
- mutation operator;
- resulting id.

## 2. Layers

```text
Source Adapter
   ↓
Feature Frame
   ↓
Normalizer
   ↓
Visual DNA + Runtime State
   ↓
Evolution Engine
   ├── modulation
   ├── mutation
   └── crossover
   ↓
Renderer Adapter
   ↓
Live / Offline Output
```

## 3. Feature frame

Initial normalized feature contract:

```json
{
  "t": 0.0,
  "rms": 0.0,
  "low": 0.0,
  "mid": 0.0,
  "high": 0.0,
  "spectral_centroid": 0.0,
  "beat": 0.0
}
```

All normalized scalar values should normally live in `[0, 1]`; adapters are responsible for conversion and clamping.

## 4. Evolution engine

The first engine should support:
- parameter modulation from one feature;
- bounded smoothing;
- seeded mutation;
- crossover between compatible DNA blocks;
- snapshot/restore.

No AI model is required for the first implementation. Generative intelligence can be layered later after deterministic behavior is trustworthy.

## 5. Evidence

Each exportable organism should be able to retain provenance:
- schema version;
- parent identifiers;
- creation seed;
- source track or session reference when applicable;
- mutation history;
- renderer compatibility version.
