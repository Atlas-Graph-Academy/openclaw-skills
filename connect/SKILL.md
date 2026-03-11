# Connect

Memory-driven discovery and retrieval using the MemoryFeed API.

## Usage

```bash
connect find --user-id <uuid> --query <text>
connect friends-prior --user-id <uuid> --query <text>
connect similar --memory-id <uuid>
```

## First-pass behavior

- `find` runs social memory search for a user query.
- `friends-prior` prioritizes friends-related resonance for the same query.
- `similar` returns memories similar to one memory id.
- Outputs are sanitized DTOs suitable for OSS runtime.