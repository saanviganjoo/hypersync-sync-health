# HyperSync Sync Health prototype

A clickable prototype of a single **Sync Health** page for HyperSync. It shows whether each active HRMS and SFTP connection is syncing, based on its latest run.

Open `index.html` in a browser. There's no build step and nothing to install. Fonts and icons load from Google Fonts.

## What's on the page

- **Summary cards:** HRMS health %, connections that need attention, SFTP connections on schedule, and passthrough status. Clicking a card jumps to the matching tab or filter.
- **HRMS and SFTP tabs:**
  - Both tables share the same columns: Name · Health · Connections or Schedule · Last Sync · Issues · Sync Logs.
  - Lists are paginated.
- **HRMS rows:** each HRMS shows its health %, with its alert threshold marked on the bar. Expanding a row lists its connections, most urgent first.
- **SFTP rows:** each connection shows its last result, schedule and due time, and whether it's late.
- **Alert settings drawer:** recipients, a default threshold, per-HRMS thresholds, and when emails go out (breach, reminder every 24h, recovered).
- **Passthrough connections:** Tartan doesn't store these syncs, so today they show as "Not tracked", with a network-wide success rate as a reference. The *Proposed* scenario shows what the page looks like once per-request metadata is logged: live success %, request volume, latency, failure reasons and a request detail drawer.

## Preview scenarios

The panel in the bottom-left corner is only for the prototype. It switches between:

- **Client setup:** a client with scheduled and passthrough connections, or a passthrough-only client.
- **Passthrough tracking:** what's available today, or the proposed version.

All data is made up. "Kredify" and every corporate name are fictional.

## Health rules used

- Latest sync `success` or `partial_success` → healthy. `fail` → failed. `stuck` → stuck. `running` and not-yet-synced are left out.
- HRMS health % = healthy ÷ (healthy + failed + stuck).
- An HRMS is below threshold when its health % is lower than its threshold. The default threshold is 80%.
- An SFTP sync is on time if the latest one started within one schedule interval plus a 6-hour grace period.
