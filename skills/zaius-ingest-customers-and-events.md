---
name: Ingest customers and events into ODP
description: Upsert customer profiles and stream behavioral events into Optimizely Data Platform (formerly Zaius) using the REST APIs.
api: openapi/zaius-customers-openapi.json
operations: [createupdate-customers, upload-events, update-object, update-products]
---

# Ingest customers and events into ODP

Use this skill to send first-party customer and behavioral data into Optimizely Data Platform (ODP).

## Auth
- Send the `x-api-key` header on every request. Use a **private** API key from ODP UI Settings > APIs for server-side ingestion; the **public** (Tracker ID) key is for browser/limited calls.
- Regional base URL: `https://api.us1.odp.optimizely.com/v3` (or `eu1` / `au1`).

## Steps
1. **Upsert customers** — `POST /profiles` (`createupdate-customers`). ODP creates-or-updates by identifier (email, vuid, phone, customer_id), so re-sends are naturally idempotent. Batch up to **500** profiles per request.
2. **Upload events** — `POST /events` (`upload-events`) with the customer identifiers plus event type/action and any custom fields. Events are the core behavioral record.
3. **Update products/objects** as needed — `POST /objects/products` (`update-products`) for catalog items, `POST /objects/{object_name}` (`update-object`) for custom objects.

## Rules
- Stay under **10 requests/second** (default). With 500 objects/request that is 5,000 updates/s; contact support for higher limits.
- Handle `400` (bad request), `403` (bad/insufficient key), `404` (unknown object/identifier). Errors are plain JSON, not RFC 9457.
- Custom objects/fields must exist in the schema first (see the schema-management skill).
