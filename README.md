<div align="center">

# LIQAA OpenAPI Specification

**The official OpenAPI 3.1 spec for the LIQAA Public API.**

[![spec version](https://img.shields.io/badge/OpenAPI-3.1.0-1d4ed8?style=flat-square)](https://spec.openapis.org/oas/v3.1.0)
[![api version](https://img.shields.io/badge/API-v1.0.0-10b981?style=flat-square)](https://liqaa.io/docs)
[![license](https://img.shields.io/badge/license-MIT-475569?style=flat-square)](./LICENSE)

[Spec file](./openapi.yaml) · [Live docs](https://liqaa.io/docs) · [Console](https://liqaa.io/console)

</div>

---

This repository contains the **machine-readable OpenAPI specification** for [LIQAA](https://liqaa.io) — the drop-in video and messaging API.

Use it to:

- Generate clients in [50+ languages](https://openapi-generator.tech/docs/generators) via `openapi-generator`
- Import into [Postman](https://www.postman.com), [Insomnia](https://insomnia.rest), [Bruno](https://www.usebruno.com), [HTTPie](https://httpie.io)
- Render interactive docs with [Redoc](https://redocly.com), [Swagger UI](https://swagger.io/tools/swagger-ui/), [Stoplight](https://stoplight.io)
- Validate requests/responses with [Spectral](https://stoplight.io/open-source/spectral) or [Prism](https://stoplight.io/open-source/prism)

## Quick start

```bash
# Render the docs in Redoc (one command, no install)
npx @redocly/cli preview-docs openapi.yaml

# Or generate a TypeScript client
npx openapi-typescript openapi.yaml -o liqaa-client.ts
```

## Importing into Postman

1. Open Postman → **File** → **Import**
2. Drag `openapi.yaml` (or paste the URL)
3. Postman generates a full collection with example requests for every endpoint

## Endpoint summary

| Endpoint                                  | Method | Description                                          |
| ----------------------------------------- | ------ | ---------------------------------------------------- |
| `/conversations`                          | POST   | Create or reuse a persistent room                    |
| `/conversations/{id}`                     | GET    | Fetch room state                                     |
| `/conversations/{id}`                     | DELETE | End an active call                                   |
| `/sdk-token`                              | POST   | Exchange identity → 1-hour browser-safe JWT          |
| `/webhooks`                               | GET    | List your subscriptions                              |
| `/webhooks`                               | POST   | Subscribe (returns one-time signing secret)          |
| `/webhooks/{id}`                          | DELETE | Cancel a subscription                                |
| `/webhooks/{id}/deliveries`               | GET    | Recent delivery audit                                |

## Authentication

All endpoints require `Authorization: Bearer sk_live_…`. **Never expose `sk_live_…` to the browser** — exchange identities via `/sdk-token` and pass the resulting JWT to the SDK.

```bash
curl https://liqaa.io/api/public/v1/conversations \
  -H "Authorization: Bearer sk_live_…" \
  -H "Content-Type: application/json" \
  -d '{"caller_email":"a@b.com","callee_email":"c@d.com"}'
```

## Versioning

The spec follows [SemVer](https://semver.org). Breaking changes increment the major version (a new path prefix `/v2`). Within `v1`, additive changes are guaranteed.

## License

MIT — feel free to redistribute and adapt.
