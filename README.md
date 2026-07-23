# cNGN API Documentation

Mintlify documentation for the cNGN third-party API (`https://api.cngn.co/v1/api`).

## Structure

- `docs.json`: Mintlify site configuration (navigation, theme, branding)
- `index.mdx`, `quickstart.mdx`: getting-started pages
- `guides/`: integration guides (authentication, encryption, response format, permissions, rate limits, networks, errors)
- `api-reference/`: one page per endpoint, grouped by Wallet, Deposits, Redemptions, On-Chain Transfers, and Address Whitelisting

## Local development

Install the Mintlify CLI and run the dev server from this directory:

```bash
npm i -g mint
mint dev
```

The site is served at `http://localhost:3000`.

## Checks

```bash
mint broken-links
```

## Source of truth

Endpoint behaviour is documented from the cNGN v2 backend (`cNGN_v2`), specifically the third-party router at `src/Core/api/v1/routes.ts` and its controllers, validations, and middleware. When endpoints change there, update the matching page under `api-reference/`.
