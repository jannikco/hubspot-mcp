# HubSpot MCP server

Find CRM contacts and inspect their properties before creating a new contact in the same HubSpot account.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `HUBSPOT_ACCESS_TOKEN`



Credential help: https://developers.hubspot.com/docs/apps/legacy-apps/private-apps/overview

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call hubspot_list_objects '{"objectType":"contacts","limit":5}'
```

## Use with an MCP client

Launch `node /absolute/path/hubspot-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| hubspot_list_objects | Read | hubspot list objects |
| hubspot_get_object | Read | hubspot get object |
| hubspot_create_object | Explicit approval required | hubspot create object |

## Concrete workflow

Find CRM contacts and inspect their properties before creating a new contact in the same HubSpot account.

1. hubspot_list_objects
2. hubspot_get_object
3. hubspot_create_object

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=hubspot&integration=hubspot-mcp&utm_source=github&utm_campaign=github-hubspot-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/hubspot/).

## Provenance and maintenance

- https://api.hubspot.com/public/api/spec/v2/specs/release/75278/version/2026-03

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
