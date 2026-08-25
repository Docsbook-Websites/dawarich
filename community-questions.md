---
title: "Community Questions, Answered From These Docs"
description: "Seven recent unanswered Dawarich discussions, matched against the documentation: four are already answered here, two partly, one is a genuine gap."
---

# Community questions, answered from these docs

Every question below is a real thread in [GitHub Discussions](https://github.com/Freika/dawarich/discussions) that had no reply when this page was built. Each one was checked against the documentation on this site.

Four of the seven are answered outright by pages that already exist. Two are half answered. One is not covered anywhere, and it is marked as such rather than padded out.

That split is the point. When people wait weeks for an answer that was already written down, the problem is not what the documentation says — it is that nobody found it in time.

<!-- widget:accordion -->

### Can I mix location data sources — dashcam GPS plus my phone?

**Answered here.** [Discussion #3382](https://github.com/Freika/dawarich/discussions/3382), asked 18 August, still open. The asker has a self-hosted instance tracking from the iOS app and found a file of higher-resolution coordinates on their dashcam SD card. They say outright: "I've browsed thru the FAQ and the docs but couldn't get a clear answer."

Yes, sources can be mixed, and two documented behaviours are why:

1. [Imports](./features/imports.md) accepts GPX for recorded routes, GeoJSON, OwnTracks `.rec`, and Dawarich's own export format. If the dashcam file can be converted to GPX or GeoJSON, it imports like anything else.
2. Points are unique per user by **coordinates and timestamp**. Importing a second source alongside phone tracking does not create duplicates, and re-importing the same file does not either. Denser dashcam points land as additional points on the same routes.

The one thing the docs do not cover: converting a vendor-specific `.txt` from a dashcam into GPX. That step is on you, and the format varies by device.

### Will Dawarich import Apple Health workouts automatically?

**Half answered.** [Discussion #3372](https://github.com/Freika/dawarich/discussions/3372), asked 17 August, no replies. A Pro self-hoster can select workouts and import them by hand, and asks two things: does it run automatically, and will workouts collide with normal tracking?

The second half is answered: points are validated for uniqueness on coordinates and timestamp, so a workout that overlaps a period of ordinary tracking will not double up your history. See [Imports](./features/imports.md).

The first half is not documented anywhere on this site. Whether automatic Apple Health import exists, is planned, or is deliberately manual is a question only the maintainer can answer.

### I created a trip and it has been spinning for days

**Not covered.** [Discussion #3275](https://github.com/Freika/dawarich/discussions/3275), asked 31 July, no replies, with a screenshot of the stuck state.

[Trips](./features/trips.md) explains how to create, edit and delete a trip and what the detail page shows. It does not describe what happens in the background when a trip is built, how long it should take, or what to check when it never finishes.

Nearby pages hold pieces of the answer — [Prometheus monitoring](./self-hosting/monitoring/prometheus.md) and the [Sidekiq queues described under Imports](./features/imports.md) are where background jobs surface — but nothing joins them up for this symptom. This is a real gap, not a findability problem.

### The iOS app only saves a few points a day now

**Half answered.** [Discussion #3160](https://github.com/Freika/dawarich/discussions/3160), asked 19 July. Routes show as straight lines between distant points, and standing still all day records nothing.

The straight lines are explainable from the docs: **Minutes Between Routes** and **Meters Between Routes** in [Settings](./self-hosting/environment-variables.md) decide when a gap starts a new route rather than joining two points with a line. Tuning those changes how sparse data is drawn.

What is not documented is the app side — how often the iOS app records, what accuracy mode it uses, and whether it is expected to log anything while stationary. [Dawarich for iOS](./getting-started/dawarich-for-ios.md) covers installing, connecting and offline buffering, but not tracking frequency.

### Docker images fail on my Orange Pi 5 with "no matching manifest for linux/arm64/v8"

**Answered here, and it takes two pages.** [Discussion #3158](https://github.com/Freika/dawarich/discussions/3158), asked 18 July, still open. The asker concluded ARM64 builds might not exist and offered to help test them.

ARM64 is supported. [Hardware requirements](./self-hosting/hardware-requirements.md) states Dawarich runs on AMD64 or ARM64, and the [self-hosting introduction](./self-hosting/introduction.md) carries the note that matters: on an ARM64 server, check the Moving to PostGIS guide for suitable database images.

The error is not about the Dawarich image. It is the database image. [Moving to PostGIS](./self-hosting/maintenance/moving-to-postgis.md) gives the replacement by architecture:

| Architecture | Old image | New image |
| --- | --- | --- |
| arm64 | `postgres:17-alpine` | `imresamu/postgis:17-3.5-alpine` |
| linux/arm/v8 | `postgres:17-alpine` | `imresamu/postgis:17-3.5-alpine` |

Swap the database image in `docker-compose.yml` and the pull succeeds.

### Is there an admin API endpoint for all users and their point counts?

**Answered, and the answer is no.** [Discussion #2968](https://github.com/Freika/dawarich/discussions/2968), asked 19 June. The asker wants the numbers from the admin Users screen for a homepage dashboard.

The published API has no admin or all-users endpoint. What exists is scoped to the authenticated user: `GET /api/v1/stats` returns that user's aggregated totals, and `GET /api/v1/users/me` returns that user's own record. `GET /api/v1/users/exist` only checks whether given user IDs exist. See the [API reference](./rest-api.md).

For an instance-wide dashboard today, the numbers have to come from the database rather than the API.

### Which settings improve visit detection on a short commute?

**Answered in part, and the missing part is a recommendation.** [Discussion #2960](https://github.com/Freika/dawarich/discussions/2960), asked 16 June, no replies. Visits are being created several hundred metres after leaving home and before arriving at work, on a 5 km commute.

The knobs are documented. Under Visit Settings in [Settings](./self-hosting/environment-variables.md):

| Setting | Description |
| --- | --- |
| Time Threshold Minutes | Minimum time at a location for visit detection |
| Merge Threshold Minutes | Gap to merge nearby visits |
| Visits Suggestions Enabled | Enable automatic visit detection |

[Visits and Places](./features/visits-and-places.md) explains the nightly job, suggested versus confirmed visits, and how to decline a suggestion so it stops coming back.

Two things are genuinely absent: any recommended value for a short-commute case, and **Smart density fill**, the setting the asker names, which does not appear anywhere in this documentation.

<!-- /widget -->

## What this adds up to

| Question | Status |
| --- | --- |
| Mixing data sources (#3382) | Answered by existing pages |
| Apple Health auto-import (#3372) | Dedup answered, automation undocumented |
| Stuck trip (#3275) | Not covered |
| iOS point frequency (#3160) | Drawing answered, app behaviour undocumented |
| ARM64 / Orange Pi 5 (#3158) | Answered by existing pages |
| Admin API (#2968) | Answered by the API reference |
| Visit detection tuning (#2960) | Settings answered, guidance missing |

Four answered, two partly, one not at all. The four were answerable the day they were asked.

<!-- widget:cta -->

## Ask the docs directly

Every answer above came out of pages already on this site. Search them, or point a question at them and see which page it lands on.

[Browse the docs](./README.md) · [Open a discussion](https://github.com/Freika/dawarich/discussions)

<!-- /widget -->
