> For Mintlify product knowledge (components, configuration, writing standards),
> install the Mintlify skill: `npx skills add https://mintlify.com/docs`

# Documentation project instructions

## About this project

- This is the documentation site for the cNGN third-party API, built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP
- Use the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, to query information about using Mintlify via MCP

## Terminology

- **business** (or **merchant**): the API consumer. Every endpoint operates on the
  authenticated business; there is no per-request account ID.
- **environments**: test (`cngn_test` key prefix) and live (`cngn_live`). Same base URL
  (`https://api.cngn.co/v1/api`); the key prefix selects the environment. Each environment
  has its own API key, encryption key, and Ed25519 SSH key slot.
- **redemption**: converting cNGN back to Naira, settled to a bank account. Use "redeem",
  never "withdraw to bank".
- **withdrawal**: an on-chain transfer of cNGN to an external wallet. Always on-chain.
- **bridge**: moving cNGN between blockchain networks. The backend calls this "swap"
  internally; the docs always say "bridge".
- **virtual account**: a NUBAN bank account for Naira deposits. "Dedicated" (permanent,
  per business) or "temporary" (one-time, per customer payment).
- **networkId**: environment-specific database ID from `GET /networks`. Never hard-code
  network IDs in examples; always show them being fetched.
- **wire format**: request bodies are AES-256-CBC encrypted as `{content, iv}`; response
  `data` is encrypted to the merchant's Ed25519 public key. All reference examples show
  the plain (decrypted) payloads with a callout explaining the wire format.

## Source of truth

- Endpoint behaviour comes from the cNGN v2 backend (`../cNGN_v2`), specifically the
  third-party router `src/Core/api/v1/routes.ts`, its controllers
  (`src/Core/api/v1/controllers.v1.ts`), and Zod validations (`src/Core/api/v1/validations.ts`).
- Webhook events come from `src/Modules/Events` and
  `src/Core/Config/transaction.event.constants.ts`; delivery payload fields from
  `src/Core/Realtime/transaction.events.ts`.
- When endpoints change in the backend, update the matching page under `api-reference/`
  and the changelog.

## Style preferences

- Use active voice and second person ("you")
- Keep sentences concise: one idea per sentence
- Use sentence case for headings
- Do not use em-dashes; use commas, colons, semicolons, or parentheses instead
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

- Document only the third-party API surface (`/v1/api/*`) and merchant-facing webhooks
- Do not document admin routes, dashboard-only endpoints, or internal modules of cNGN_v2
- Contract addresses must match the official published list exactly; never infer or
  abbreviate an address
