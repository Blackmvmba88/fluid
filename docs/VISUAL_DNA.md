# Visual DNA

Visual DNA is the portable description of a fluid organism.

## Required concepts

### Identity
A stable `id`, human-readable `name`, schema version and optional parent references.

### Geometry
Controls such as particle count, field scale, symmetry, pixel size or line density.

### Motion
Speed, damping, turbulence, directionality and phase behavior.

### Palette
A renderer-neutral palette description. Color values belong in the organism; rendering code should not invent a palette silently.

### Audio bindings
Mappings from normalized audio features to bounded visual parameters.

Example:

```json
{
  "source": "low",
  "target": "motion.turbulence",
  "min": 0.1,
  "max": 0.8,
  "smoothing": 0.2
}
```

### Mutation policy
Declares which parameters may change and by how much.

## Crossover rule

Two organisms may cross only when the targeted blocks are schema-compatible. Crossover must record both parents and the chosen operator.

## Reproducibility

Random operations require an explicit seed. A mutation without a recorded seed is considered non-reproducible.
