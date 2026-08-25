---
title: "Move a Self-Hosted Instance to Dawarich Cloud"
description: "Move years of location history off your own server and into Dawarich Cloud: export your points, import them, verify the result, then retire the server."
---

# Move a self-hosted instance to Dawarich Cloud

You already run Dawarich on your own hardware and your history goes back years. This page walks that history from your server into Dawarich Cloud without losing points and without a day where neither instance is trustworthy.

Nothing here asks you to give anything up first. Your self-hosted instance keeps running until you have checked the copy in the cloud, and [your data stays exportable from either side, on any plan](https://dawarich.app/pricing/).

<!-- widget:stepper -->

### Take a full backup of the server you are leaving

Before touching anything, take a database dump the way you would before an upgrade. The commands are the same ones you already use: see [Backup and Restore](../self-hosting/maintenance/backup-and-restore.md).

This dump is not what you upload to the cloud. It is the copy you keep in case you want the old instance back.

### Export your points from the self-hosted instance

On your own instance, open the **Points** page, choose a time range, click **Search**, then click **Export**. The export runs in the background and the download link appears on the **Exports** page.

The file is JSON, structured the same way as the OwnTracks JSON format, and Dawarich can read it back in. That is the property that makes this move possible at all — see [Exporting your data](../getting-started/export-your-data.md).

> **Export in slices if your history is long**
>
> The Points page exports the range you searched for. For a history measured in years, export year by year rather than in one request: smaller files upload more reliably and a failed slice costs you one year, not the whole archive.

### Create your cloud account and start the trial

Sign up for [Dawarich Cloud](https://my.dawarich.app/users/sign_up). Every plan starts with a 7-day free trial, and there is a 14-day money-back guarantee, so the migration can be finished and checked before any of it is final.

Which plan you need depends mostly on how far back your history goes: Lite keeps 12 months of searchable history, Pro and Family keep it unlimited. The full comparison is on the [pricing page](https://dawarich.app/pricing/).

### Import the export into your cloud account

In your cloud account open **Imports** and create a new import with the JSON file you exported. Source type is detected from the file content, and processing happens in the background — you get a notification when it finishes.

Repeat for each slice you exported. Order does not matter.

> **Re-importing a file is safe**
>
> Points are unique per user by coordinates and timestamp, so importing the same file twice does not create duplicates, and neither does a tracking app that sends the same point twice. If you are unsure whether a slice went through, import it again. See [Imports](../features/imports.md).

### Point your phone at the cloud instead of your server

In the Dawarich app on [iOS](../getting-started/dawarich-for-ios.md) or [Android](../getting-started/dawarich-for-android.md), open Settings, replace your instance URL with your cloud URL and paste the API key from your cloud account, then tap **Test connection**.

From this moment new points land in the cloud. Old points are already there from the previous step.

### Verify before you retire anything

Compare the two instances before you switch the server off:

- **Stats** — total distance, points tracked, countries and cities visited should line up between the two. `GET /api/v1/stats` returns the same numbers through the API if you would rather diff them than read them.
- **The map** — pick a few trips you remember from the earliest years and check they are on the cloud map with the same shape.
- **Visits and places** — confirmed visits carry over with the points they were built from; see [Visits and Places](../features/visits-and-places.md).

### Retire the server

Once the cloud copy checks out, stop the containers and keep the dump from step one. There is no rush to delete it, and nothing in the cloud account depends on the old server still existing.

<!-- /widget -->

## If your history is too large to export by hand

Two options, both using things that already exist.

**Let them do it.** Every plan includes the White-Glove Import Service — you send the archive and it gets imported for you, usually within 24 hours. It is listed on the [pricing page](https://dawarich.app/pricing/) at €99 value, included free.

**Do it over the API.** Your self-hosted instance and your cloud account expose the same API. Read points out of the old instance page by page and post them in batches to the new one:

| Step | Endpoint | Notes |
|---|---|---|
| Read from the old instance | `GET /api/v1/points` | Accepts `start_at`, `end_at`, `page`, `per_page`, `order` |
| Write to the cloud account | `POST /api/v1/points` | Accepts a batch of points |
| Check as you go | `GET /api/v1/stats` | Aggregated totals for the authenticated user |

Both instances validate uniqueness on coordinates and timestamp, so a batch that gets sent twice after a network error does not double anything. See the project's [OpenAPI specification](https://github.com/Freika/dawarich/blob/master/swagger/v1/swagger.yaml).

## What you are actually buying

Self-hosting Dawarich is free and stays free, and their own pricing page says so plainly: every Pro feature, your server, zero cost. So this move is not about unlocking features. It is about who gets paged when the database needs upgrading, when the reverse proxy certificate expires, or when a Postgres major version changes under you.

If that trade is not obvious to you yet, it probably is not time. Keep [self-hosting](../self-hosting/introduction.md) — the guides are all here.

<!-- widget:cta -->

**Your history, someone else's pager**

## Try it for a week before you commit

Start the trial, import a year, and see whether the copy looks right. Nothing is final for 14 days.

[Start free trial](https://my.dawarich.app/users/sign_up) · [Compare plans](https://dawarich.app/pricing/)

<!-- /widget -->

## Related

- [Self-hosted or cloud](./self-hosted-vs-cloud.md)
- [Exporting your data](../getting-started/export-your-data.md)
- [Imports](../features/imports.md)
- [Backup and Restore](../self-hosting/maintenance/backup-and-restore.md)
