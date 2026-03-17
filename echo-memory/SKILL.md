---
name: echo-memory
description: "Guide users through installing, configuring, and troubleshooting the EchoMemory Cloud OpenClaw Plugin. Use for plugin setup, API key onboarding, local mode vs cloud mode switching, local UI startup, gateway restart checks, localhost viewer issues, and /echo-memory command guidance."
---

# EchoMemory Plugin

Use this skill when the user is setting up or debugging the EchoMemory OpenClaw plugin.

Prefer the plugin's current runtime behavior over old repo habits:

- the plugin starts the local UI during `openclaw gateway` startup
- `localUiAutoOpenOnGatewayStart` defaults to `true`
- browser auto-open is skipped automatically on headless, SSH, or CI sessions
- removing the API key from the local UI forces local-only mode for future loads

## First checks

1. Confirm the plugin is installed or linked.

```powershell
openclaw plugins install "C:\path\to\EchoMemory-Cloud-OpenClaw-Plugin"
```

or

```powershell
openclaw plugins install --link "C:\path\to\EchoMemory-Cloud-OpenClaw-Plugin"
```

2. Confirm `tools.profile` is `"full"` in `~/.openclaw/openclaw.json`.
3. Confirm the plugin config entry exists at `plugins.entries.echo-memory-cloud-openclaw-plugin`.
4. Restart the gateway after install or config changes.

```powershell
openclaw gateway restart
```

## Mode switching

Use cloud mode when the user wants sync and retrieval from EchoMemory cloud:

- `localOnlyMode: false`
- `apiKey: "ec_..."`
- key scopes should include `ingest:write` and `memory:read`

Use local mode when the user only wants localhost browsing of markdown files:

- `localOnlyMode: true`
- API key can be blank
- the local UI should still be available

If the user wants to switch modes, read [`references/mode-switching.md`](./references/mode-switching.md).

## Local UI behavior

If the user asks to "view memories" and does not explicitly mention graph, public memories, or iditor.com, treat that as the local UI, not the cloud graph.

Successful gateway startup usually includes:

```text
[echo-memory] Local workspace viewer: http://127.0.0.1:17823
```

If the plugin is loaded but the user still cannot open the viewer:

1. confirm the gateway was restarted
2. confirm localhost port `17823` is listening
3. confirm `localUiAutoInstall` was not disabled before the first run
4. use the fallback script at [`scripts/start-local-ui.mjs`](./scripts/start-local-ui.mjs)

## Working flow

1. Install or link the plugin.
2. Set `tools.profile` to `"full"`.
3. Set plugin config or `~/.openclaw/.env`.
4. Restart `openclaw gateway`.
5. Verify the localhost viewer URL appears in gateway logs.
6. For cloud mode, run:

```text
/echo-memory whoami
/echo-memory status
/echo-memory sync
/echo-memory search <known topic>
```

## Configuration examples

Cloud mode:

```json5
{
  "plugins": {
    "entries": {
      "echo-memory-cloud-openclaw-plugin": {
        "enabled": true,
        "config": {
          "apiKey": "ec_your_key_here",
          "localOnlyMode": false,
          "memoryDir": "C:\\Users\\your-user\\.openclaw\\workspace\\memory",
          "localUiAutoOpenOnGatewayStart": true,
          "localUiAutoInstall": true
        }
      }
    }
  }
}
```

Local mode:

```json5
{
  "plugins": {
    "entries": {
      "echo-memory-cloud-openclaw-plugin": {
        "enabled": true,
        "config": {
          "localOnlyMode": true,
          "memoryDir": "C:\\Users\\your-user\\.openclaw\\workspace\\memory",
          "localUiAutoOpenOnGatewayStart": true,
          "localUiAutoInstall": true
        }
      }
    }
  }
}
```

## References

- [`references/mode-switching.md`](./references/mode-switching.md): exact local/cloud toggles, config precedence, and restart rules
- [`references/troubleshooting.md`](./references/troubleshooting.md): failure patterns for plugin discovery, local UI startup, auth, and sync
- [`scripts/start-local-ui.mjs`](./scripts/start-local-ui.mjs): manual fallback to launch the local UI when the gateway cannot start it
