# Memory Signal

Signal summaries derived from memory metadata for trend analysis.

## Usage

```bash
memory-signal analyze [--limit <n>]
memory-signal trends --start <iso> --end <iso> [--limit <n>]
```

## First-pass behavior

- `analyze` summarizes top emotion/category/object signals from recent memories.
- `trends` summarizes the same signals within a time range.
- This pass is metadata-aggregation only; no private model internals are exposed.