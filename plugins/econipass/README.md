# EcoNiPass DEV

EcoNiPass connects emissions, energy management, product CFP input, reduction work and statutory-report preparation to the user's existing EcoNiPass account. This bundle provides seven workflow skills and a remote MCP definition. It targets the DEV service, so it is not a production connection or a guarantee that every operation is available to the signed-in user.

## Installation

Install a published version from the EcoNiPass marketplace in a Claude Code session:

```text
/plugin install econipass --marketplace emmatch-dev/econipass-mcp-plugins
```

Confirm the installed version and DEV endpoint, then use `econipass:setup`. Existing connections should be checked before adding another one.

## What this plugin runs and sends

The plugin contains instructions and a remote HTTPS MCP configuration. It does not install a local server, execute hooks, launch package managers, or include credentials. The configured destination is `https://api.dev.app.econipass.com/mcp`. Authentication and consent use the client's supported EcoNiPass connection flow; the caller's organization permissions, contracts, scopes and server feature flags still apply.

When the user requests an operation, the MCP request can contain organization identifiers, periods, filters, record values, comments, report proposals, or workbook bytes needed for that specific operation. The server returns the requested business records or file resources to the AI client. Those results are available to that client's model according to the client's own data-handling settings. Do not include secrets in record text or workbook cells.

Some explicitly requested EcoNiPass operations can use the service's configured external providers, such as generating measure ideas, synchronizing an intake provider, or sending a configured notification. Inspect the operation's current schema, preview and delivery scope before execution. A skill does not authorize an unsolicited message, notification test or external submission.

## Writes and files

Read current state before a change. Use the server preview and its single-use confirmation token for the exact change authorized by the user. Re-read after a conflict or unknown result instead of automatically repeating a write. CFP uploads can replace existing records; retain data outside the requested change and verify the full replacement scope. A download, preview or generated report is not evidence of a completed upload or official filing. CFP downloads return metadata by default; no workbook is attached or saved in that mode. Use the returned steps to download separately in your signed-in EcoNiPass screen, or explicitly request embedded delivery through a client that supports XLSX resources and verify the received file before editing.

The eleven EMS file downloads and exports also return metadata by default. Only a compatible host or SDK should explicitly request `delivery_mode="embedded"`, receive the actual file, and verify its size and SHA-256. The server does not confirm client receipt or saving, and an opaque resource URI is not a public download link. Do not assume an EMS browser download procedure that has not been verified.

Start with the `setup` skill and choose only the workflow needed for the request. The bundle does not grant additional access. Shared statutory output remains a human-authenticated browser step when the returned tool capability requires that handoff.

## Help and privacy

[EcoNiPass website and support](https://econipass.com/), [installation and current acceptance status](https://github.com/emmatch-dev/econipass-mcp-plugins#readme), and [EmMatch privacy policy covering EcoNiPass](https://emmatch.com/privacy-policy).
