# Echo Identity

Prompt and profile utilities over EchoMem extension APIs.

## Usage

```bash
echo-identity profile
echo-identity templates [--limit <n>]
echo-identity template-create --title <text> --template <text> [--tags a,b,c]
echo-identity template-delete --ids <id1,id2,...>
echo-identity extract --file <path> [--save true|false]
echo-identity compose --intent <text> [--template-ids id1,id2] [--memory-ids id1,id2]
```

## First-pass behavior

- `profile` returns account profile summary.
- `templates` and `template-*` manage prompt templates.
- `extract` parses raw content into prompt templates.
- `compose` generates prompts from selected templates and memories.