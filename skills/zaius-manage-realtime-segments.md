---
name: Manage ODP real-time segments
description: Create, list, install, validate and remove real-time audience segments in Optimizely Data Platform (formerly Zaius).
api: openapi/zaius-realtimesegments-openapi.json
operations: [RealtimeSegments_ListSegments, RealtimeSegments_GetSegment, RealtimeSegments_CreateSegment, RealtimeSegments_ValidateSegment, RealtimeSegments_InstallSegment, RealtimeSegments_UninstallSegment]
---

# Manage ODP real-time segments

Use this skill to manage real-time audience segments through the ODP RealtimeSegments API.

## Auth
- Send the `x-api-key` header (private key). Base URL: `https://api.us1.odp.optimizely.com/v3`.

## Steps
1. **List existing segments** — `GET /segments` (`RealtimeSegments_ListSegments`).
2. **Inspect one** — `GET /segments/{segment_id}` (`RealtimeSegments_GetSegment`).
3. **Validate a definition** — `POST /segments/{segment_id}:validate` (`RealtimeSegments_ValidateSegment`) before creating, to catch definition errors.
4. **Create** — `POST /segments/{segment_id}` (`RealtimeSegments_CreateSegment`).
5. **Install / uninstall** — `PUT /segments/{segment_id}` (`RealtimeSegments_InstallSegment`) to activate, `DELETE /segments/{segment_id}` (`RealtimeSegments_UninstallSegment`) to remove.

## Rules
- Query segment results/membership via the GraphQL API at `/v3/graphql`.
- Handle `400` (invalid definition) and `404` (unknown segment id). Validate before create to avoid `400`s.
