---
title: "Self-Hosted or Cloud: Which Dawarich Is for You"
description: "Self-hosting Dawarich is free and includes every Pro feature. Here is what the paid cloud actually changes, and when it is worth it."
---

# Self-hosted or cloud

Most projects put their good features behind the paid tier. Dawarich does not, and it says so on its own pricing page: **self-host for free — every Pro feature, your server, zero cost.**

That makes the choice unusually clean. You are not comparing feature lists. You are deciding who runs the server.

## What is identical either way

- The same application, from [the same open-source repository](https://github.com/Freika/dawarich).
- The same tracking apps for [iOS](../getting-started/dawarich-for-ios.md) and [Android](../getting-started/dawarich-for-android.md).
- The same map, heatmap, Fog of War, trips, visits, statistics and insights.
- The same imports and exports. Your data is yours and stays exportable on any plan.
- The same API.

## What actually differs

<!-- widget:accordion -->

### Who maintains the database

Self-hosted, that is you. Dawarich moved to PostGIS in 0.23.6, which meant [replacing the database image](../self-hosting/maintenance/moving-to-postgis.md), and PostgreSQL major upgrades come with [their own procedure](../self-hosting/maintenance/update-postgresql.md). None of it is hard. It is just yours to do, on a day you did not choose.

On cloud, that work is theirs.

### Who keeps it reachable

Self-hosted means a [reverse proxy](../self-hosting/configuration/reverse-proxy.md) or a [Cloudflare tunnel](../self-hosting/configuration/cloudflare-tunnel.md), certificates that expire, and a home connection that has opinions about uptime. Your phone is uploading points the whole time, so an instance that is unreachable for a week is a week of history you have to hope the app buffered.

### How long history is kept

Self-hosted, as long as your disk lasts. On cloud, the Lite plan keeps 12 months of searchable history while Pro and Family keep it unlimited. Check the [pricing page](https://dawarich.app/pricing/) for the current comparison.

### API rate limits

Self-hosted, whatever your server tolerates. On cloud, the published limits are 200 requests per hour on Lite and 1,000 on Pro and Family, with full write access on Pro and above.

### Cost

Self-hosted: zero to Dawarich, plus your hardware and your electricity, plus your time. Cloud: from €59.99 a year, with a 7-day free trial and a 14-day money-back guarantee.

### Where the data sits

Self-hosted, wherever you put it. Cloud is hosted in Germany, and the [privacy policy](https://dawarich.app/privacy-policy/) lists the processors involved.

<!-- /widget -->

## A reasonable way to decide

Keep self-hosting if maintaining a small Postgres and a reverse proxy is something you already do for other services, and one more container costs you nothing extra. The [self-hosting guides](../self-hosting/introduction.md) are complete and the community is on [Discord](https://discord.gg/pHsBjpt5J8) and [GitHub Discussions](https://github.com/Freika/dawarich/discussions).

Move to cloud when the maintenance has started to feel like a second job, or when the history you are protecting has become too valuable to sit on a single disk you keep meaning to back up.

You can change your mind in either direction. Exports work on every plan, and [moving an existing self-hosted history into the cloud](./migrate-from-self-hosted.md) is a documented path.

<!-- widget:cta -->

## Already decided?

Bring your existing history with you — the migration is seven steps and nothing is final for 14 days.

[Move my instance to cloud](./migrate-from-self-hosted.md) · [Compare plans](https://dawarich.app/pricing/)

<!-- /widget -->
