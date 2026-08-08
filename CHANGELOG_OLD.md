# Older changes

Changelog entries for older releases.

### 1.0.3 (17.07.2026)

-   (Stefan Bühler) Corrected several object role/type mismatches found by the ioBroker store submission's object structure check (ACTIONS.HEADLIGHT, ACTIONS.schedule fields, messages.messages, system.id/type/serialNumber). No functional/API changes - purely metadata (common.role/common.type) corrections.

### 1.0.2 and older

Older changelog entries can be found in [CHANGELOG_OLD.md](CHANGELOG_OLD.md).

### 1.0.2 (16.07.2026)

-   (Stefan Bühler) Enabled automated npm releases via GitHub Actions using npm Trusted Publishing (OIDC) - no more manual publishing, and this and all future tagged releases are automatically signed with npm provenance. No functional/API changes.

### 1.0.1 (16.07.2026)

-   (Stefan Bühler) Cleanup release addressing the ioBroker adapter store checker findings, no functional/API changes.
-   (Stefan Bühler) Removed devDependencies already bundled by `@iobroker/testing` (`chai`, `mocha`, `sinon` and their `@types/*`)
-   (Stefan Bühler) Updated `@iobroker/testing`, `admin` and `js-controller` minimum versions; fixed a peer-dependency conflict (`globals`)
-   (Stefan Bühler) Migrated to `@tsconfig/node22` and the current standard Dependabot auto-merge workflow (`automerge-dependabot.yml`)
-   (Stefan Bühler) Fixed copyright line formatting in README.md/LICENSE (Markdown line-break spacing); synced README installation requirements with io-package.json

### 1.0.0 (14.07.2026)

-   (Stefan Bühler) Renamed/continued as `ioBroker.husqvarna-automower-connect`, a complete, actively maintained fork of `ioBroker.husqvarna-automower`. Full credit to ice987987 for the original adapter. BREAKING: adapter instance namespace changes from `husqvarna-automower.x` to `husqvarna-automower-connect.x` - create a new instance and re-enter Application Key/Secret.
-   (Stefan Bühler) fix: `START`, `STARTINWORKAREA`, `PARK`, `CUTTINGHEIGHT`, `DATETIME` and `HEADLIGHT` sent a malformed request body (`attributes` was a sibling of `data` instead of nested inside `data.attributes`) and were rejected by the API
-   (Stefan Bühler) fix: `DATETIME` used `type: 'dateTime'` instead of the required `type: 'settings'`
-   (Stefan Bühler) fix: `HEADLIGHT` used `type: 'HeadLight'` instead of `type: 'settings'`, and sent the mode flat instead of nested in `attributes.headlight.mode`
-   (Stefan Bühler) fix: `HEADLIGHT` validation compared against `'ALWAYS OFF'` (space) instead of `'ALWAYS_OFF'` (underscore)
-   (Stefan Bühler) fix: `.ACTIONS.CUTTINGHEIGHT` was `undefined` until the first WebSocket update after adapter start (REST response returns `cuttingHeight` as a plain number, not `{height: N}`)
-   (Stefan Bühler) fix: memory leak in the internal capabilities cache (grew by one duplicate entry on every statistics poll)
-   (Stefan Bühler) added `.ACTIONS.CONFIRMERROR`, `.ACTIONS.RESETCUTTINGBLADEUSAGETIME`, `.ACTIONS.workAreaSettings` (set cutting height/enabled per work area) and `.ACTIONS.stayOutZoneSettings` (enable/disable a stay-out zone)
-   (Stefan Bühler) added `.messages` channel with the error/event message history (REST on startup/on-demand + live WebSocket updates)
-   (Stefan Bühler) added missing `.workAreas.[workAreaId]` fields: `type`, `useGlobalCuttingHeight`, `orientation`, `orientationShift`, `currentOrientation`, `lastTimeAbandoned`
-   (Stefan Bühler) BREAKING: node.js >= v22 is required (v18 reached end-of-life April 2025, v20 reached end-of-life April 2026)
-   (Stefan Bühler) security: `applicationSecret`, `applicationKey` and the live OAuth access token were logged in plaintext at debug level in several places; added redaction so they can no longer end up in a shared logfile
-   (Stefan Bühler) security: token invalidation on adapter stop used a malformed request (wrong endpoint/headers) and never actually revoked the token with Husqvarna; fixed to use the correct `POST /v1/oauth2/revoke`
-   (Stefan Bühler) security: `axios` updated 1.8.4 -> 1.18.1 (fixes several CVEs, including the critical CVE-2026-40175) and `ws` updated 8.18.3 -> 8.21.1 (fixes two High-severity CVEs); `npm audit --omit=dev` now reports 0 vulnerabilities
-   (Stefan Bühler) fix: `statisticsInterval` validation was permanently unreachable (`&&` instead of `||`), so any configured value was silently accepted
-   (Stefan Bühler) hardening: Application Key/Secret format check is now anchored; `stayOutZoneSettings.zoneId` is URL-encoded before use
-   (Stefan Bühler) optimization: message history is no longer re-polled on every statistics interval tick (only on startup/on-demand), to avoid roughly doubling the request volume against Husqvarna's 10 000 requests/month budget

### 0.6.0-beta.12 and older

Older changelog entries can be found in [CHANGELOG_OLD.md](CHANGELOG_OLD.md).

