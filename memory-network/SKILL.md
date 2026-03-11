# Memory Network

Social memory network access over MemoryFeed and Mercury endpoints.

## Usage

```bash
memory-network feed --user-id <uuid>
memory-network search --user-id <uuid> --query <text>
memory-network friends --user-id <uuid>
```

## First-pass behavior

- `feed` returns grouped social memory feed data.
- `search` runs query search scoped to a user.
- `friends` returns friend relationships via Mercury service.
- Persistence and recommendation tuning remain backend-owned.