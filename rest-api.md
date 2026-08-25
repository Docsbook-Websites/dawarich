---
title: "Dawarich API Reference"
description: "Try the Dawarich REST API from the browser: read points and stats, create points and areas, and queue imports on your own instance or Dawarich Cloud."
---

# Dawarich API reference

Dawarich exposes a REST API on every instance, self-hosted or cloud. The endpoints below are generated from the project's own OpenAPI specification (`swagger/v1/swagger.yaml`) and can be called straight from this page.

Your API key is found in your Dawarich account settings. It never leaves your browser — requests go directly from you to the instance you name.

> **Point this at your own instance**
>
> The forms below default to Dawarich Cloud. Self-hosting? Replace the host with your own instance URL. Older endpoints take the key as an `api_key` query parameter, newer ones as an `Authorization: Bearer` header, which is why both appear below.

<!-- widget:api -->

## GET /api/v1/health

Returns the health status of the application. No authentication required, which makes it the right endpoint for uptime checks and for confirming a fresh install is reachable through your reverse proxy.

### Example

```bash
curl https://my.dawarich.app/api/v1/health
```

## GET /api/v1/stats

Returns aggregated statistics for the authenticated user: total distance, points tracked, countries and cities visited, with yearly breakdowns.

| Field | Type | Required | Description |
|---|---|---|---|
| `api_key` | string | yes | Your API key |

### Example

```bash
curl "https://my.dawarich.app/api/v1/stats?api_key=YOUR_API_KEY"
```

### Errors

| Status | Meaning |
|---|---|
| `401` | Missing or invalid API key |

## GET /api/v1/points

Returns paginated location points for the authenticated user, optionally filtered by date range. This is the endpoint to read a self-hosted history out of an instance you are migrating away from.

| Field | Type | Required | Description |
|---|---|---|---|
| `api_key` | string | yes | Your API key |
| `start_at` | string | no | Start date, e.g. `2024-02-03T13:00:03Z` or `2024-02-03` |
| `end_at` | string | no | End date, e.g. `2024-02-03T13:00:03Z` or `2024-02-03` |
| `page` | integer | no | Page number |
| `per_page` | integer | no | Number of points per page |
| `order` | string | no | Order of points: `asc` or `desc` |

### Example

```bash
curl "https://my.dawarich.app/api/v1/points?api_key=YOUR_API_KEY&start_at=2024-01-01&end_at=2024-12-31&per_page=1000"
```

## POST /api/v1/points

Creates a batch of points. Points are validated for uniqueness by coordinates and timestamp, so a batch resent after a network error does not duplicate anything.

| Field | Type | Required | Description |
|---|---|---|---|
| `api_key` | string | yes | Your API key |

## GET /api/v1/users/me

Returns the current user. Uses the bearer header rather than the query parameter.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | `Bearer {api_key}` |

## GET /api/v1/visits

Lists visits for the authenticated user. Supports a date range, or an area search when `selection` is set to `true` and a bounding box is supplied.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | `Bearer {api_key}` |
| `start_at` | string | no | Start date (ISO 8601) |
| `end_at` | string | no | End date (ISO 8601) |
| `selection` | string | no | Set to `true` for area-based search |
| `sw_lat` | number | no | Southwest latitude for area search |
| `sw_lng` | number | no | Southwest longitude for area search |
| `ne_lat` | number | no | Northeast latitude for area search |
| `ne_lng` | number | no | Northeast longitude for area search |

## GET /api/v1/areas

Returns all areas belonging to the authenticated user.

| Field | Type | Required | Description |
|---|---|---|---|
| `api_key` | string | yes | Your API key |

## POST /api/v1/imports

Uploads a file (GPX, GeoJSON, KML, OwnTracks and others) and queues it for import processing. The source type is detected from the file content, and processing happens asynchronously in the background.

| Field | Type | Required | Description |
|---|---|---|---|
| `api_key` | string | yes | Your API key |

## GET /api/v1/imports

Returns all imports for the authenticated user, ordered newest first.

| Field | Type | Required | Description |
|---|---|---|---|
| `api_key` | string | yes | Your API key |
| `page` | integer | no | Page number |
| `per_page` | integer | no | Items per page (default: 25) |

<!-- /widget -->

## Scope of the API

Every endpoint above is scoped to the authenticated user. There is no admin endpoint that returns all users on an instance or their point counts — a question that [comes up in discussions](./community-questions.md) and is answered by the specification rather than by a page.

The full specification, including endpoints not listed here (families, digests, tracks, places, notes, photos, two-factor authentication and the OwnTracks, Overland and Traccar ingestion paths), lives at [`swagger/v1/swagger.yaml`](https://github.com/Freika/dawarich/blob/master/swagger/v1/swagger.yaml) in the main repository.

## Related

- [Community questions](./community-questions.md)
- [Move a self-hosted instance to Dawarich Cloud](./cloud/migrate-from-self-hosted.md)
- [Imports](./features/imports.md)
