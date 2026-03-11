# Memory Map

Render and query conceptual memory maps using Mercury APIs.

## Usage

```bash
memory-map render [--map-type category|description]
memory-map search --query <text> [--map-type category|description] [--limit <n>]
memory-map convergence [--map-type category|description] [--run-index <n>] [--max-tier <n>]
memory-map compute-convergence [--map-type category|description]
```

## First-pass behavior

- `render` fetches the current map node set.
- `search` returns map nodes related to a query.
- `convergence` returns convergence runs and candidate paths.
- `compute-convergence` triggers recomputation on backend.