# EchoMemory Troubleshooting

Use this reference for the common breakpoints in the plugin flow.

## Plugin installed but not behaving

Check these in order:

1. the plugin is actually installed or linked
2. `tools.profile` is `"full"` in `~/.openclaw/openclaw.json`
3. the plugin config entry key is exactly `echo-memory-cloud-openclaw-plugin`
4. `openclaw gateway restart` was run after the last change

## `plugin not found: echo-memory-cloud-openclaw-plugin`

Likely causes:

- the plugin was never installed
- the install path was not quoted on Windows
- the gateway was not restarted after install

Preferred fix:

```powershell
openclaw plugins install --link "C:\Users\Your Name\Documents\GitHub\EchoMemory-Cloud-OpenClaw-Plugin"
openclaw gateway restart
```

If discovery is still blocked, start the local UI manually with [`../scripts/start-local-ui.mjs`](../scripts/start-local-ui.mjs).

## Local UI does not open on gateway restart

Expected behavior:

- the service starts the local UI during gateway startup
- browser auto-open only happens on local desktop sessions

Checks:

1. find `[echo-memory] Local workspace viewer:` in gateway logs
2. verify port `17823` is listening
3. confirm `localUiAutoInstall` is not disabled before the first run

Manual fallback:

```powershell
node .\echo-memory\scripts\start-local-ui.mjs
```

## Local UI shows local-only mode unexpectedly

Likely causes:

1. `localOnlyMode` is still `true`
2. the API key is blank
3. `ECHOMEM_LOCAL_ONLY_MODE=true` was saved in `~/.openclaw/.env`

Fix:

1. set `localOnlyMode` back to `false`
2. restore a valid `ec_...` API key
3. restart the gateway

## `/echo-memory` commands fail with authorization errors

If Slack returns `This command requires authorization`, the plugin may be loaded and OpenClaw is blocking the request.

Check:

- `channels.slack.allowFrom`
- channel-specific user allowlists
- then restart the gateway

## `/echo-memory sync` or search returns nothing

Check:

1. the API key includes `ingest:write` and `memory:read`
2. `memoryDir` points to the markdown directory you expect
3. the local markdown files actually exist
4. the user is testing with a known imported topic rather than a narrow literal phrase
