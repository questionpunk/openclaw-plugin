# QuestionPunk for OpenClaw

Production connection: `https://app.questionpunk.com/api/v1` (QuestionPunk OAuth protected resource).

Install with `openclaw plugins install git:github.com/questionpunk/openclaw-plugin@v1.1.1 --force --accept-capabilities`, or use the extracted release package path. These flags acknowledge the reviewed direct GitHub source and declared capabilities; normal install-policy checks still apply. Then inspect `openclaw plugins inspect questionpunk --runtime`. This is a native OpenClaw skills plugin with `openclaw.plugin.json`, a dependency-free registration entry, and four shared skills. Private MCP tools are configured through the explicit OAuth setup below; the plugin does not embed credentials or register a second copy of the tools.

Before invoking private tools on a shared Gateway, merge the sibling `config-merge.json` into the existing OpenClaw configuration using its normal config controls. It defines `mcp.servers.questionpunk` with Streamable HTTP, OAuth, and `oauth.identity: per-requester`. Configure the Gateway's actual public HTTPS `gateway.publicOrigin` for its callback. Preserve unrelated config. Do not replace this with an operator's shared bearer token. If the installed release cannot enforce per-requester identity, keep the connector disabled on shared channels.

Authenticate through the configured host OAuth flow (`openclaw mcp login questionpunk` is the documented operator command; verify requester-specific login in the actual channel). Start a new session. OpenClaw tool names are prefixed, such as `questionpunk__survey_list`; the skills refer to their base names. Test two different authenticated senders before enabling shared access. Package inspection alone does not prove token ownership or a working connection.

For a private, single-user operator setup, configure the server with `openclaw mcp set questionpunk '{"url":"https://app.questionpunk.com/api/v1","transport":"streamable-http","auth":"oauth","oauth":{"scope":"read write responses:read"}}'`, then use the login command above. This uses that operator's credentials and must not be offered to shared-channel senders. For shared Gateways use the supplied per-requester configuration and verify two independent senders before enabling it.

Sources checked October 3, 2026: [bundles](https://docs.openclaw.ai/plugins/bundles), [MCP/OAuth configuration](https://docs.openclaw.ai/gateway/config-extensions). The native package targets the tested OpenClaw 2026.9.8 plugin API. ClawHub 0.23.3 rejects portable Agent Plugins publish attempts with `openclaw.plugin.json required`, so this package uses a complete native format with compiled JavaScript and declared compatibility. Direct GitHub/archive distribution is separate from registry publication. Requester OAuth tests remain release QA requirements.

## Connection for this build

MCP endpoint: https://app.questionpunk.com/api/v1

QuestionPunk: https://app.questionpunk.com
