# Medux plugin for Cursor

Connects Cursor to the [Medux](https://medux.io) remote MCP server for AI media generation and editing: video, image, speech, voice cloning, avatars, and PDF/audio/video tools.

- Endpoint: `https://medux.io/mcp` (Streamable HTTP)
- Authentication: Medux API key as a Bearer token
- The old endpoint `https://medux.io/api/mcp/v1` still works but is no longer used by this plugin.

## Setup

1. Create an API key (`sk-medux-...`) in your Medux account.
2. Export it before launching Cursor (apps opened from the Dock or Start menu may not see your shell profile, so start Cursor from a terminal):
   ```bash
   export MEDUX_API_KEY=sk-medux-...
   ```
3. Install the plugin from the Cursor Marketplace, then restart Cursor.
4. Open **Customize** in the sidebar and check that `medux` is on.

## Manual configuration

Without the plugin, add this to `.cursor/mcp.json` (project) or `~/.cursor/mcp.json` (all projects):

```json
{
  "mcpServers": {
    "medux": {
      "url": "https://medux.io/mcp",
      "headers": { "Authorization": "Bearer ${env:MEDUX_API_KEY}" }
    }
  }
}
```

## Troubleshooting

- Server missing or off: check the JSON is valid, then restart Cursor.
- `401 Unauthorized` in **Output → MCP Logs**: the key is empty or wrong, or `MEDUX_API_KEY` is not set in the environment Cursor was launched from.

More: [Connect Medux MCP](https://github.com/MeduxIO/medux-mcp-examples/blob/main/docs/connection.md).

## License

MIT
