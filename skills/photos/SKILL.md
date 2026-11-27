---
name: photos
description: Apple Photos through the `photos` CLI (osxphotos). Find photos, albums and metadata; import saved media; export originals or edits; change library metadata.
---

# Photos

`photos` is the `osxphotos` CLI itself, with no wrapper. `photos COMMAND --help` is the reference; this file holds what the help leaves out. Source-checked against osxphotos 0.77.2.

- **Keep reads read-only.** A request to find a photo does not authorize importing, editing metadata, changing the active library or deleting assets. Follow the owner's exact effect for mutations; native support is not permission to act.
- **Shared albums are unreadable on macOS 26.x** (vendor README). A missing shared album or missing items in one is a coverage gap, not an empty album.
- **Import goes into the library Photos.app has open.** `--library` only points osxphotos' duplicate lookup at a library; it does not select the destination. `photos list --json` gives `system_library` and `last_library`. Settle the destination before importing, and query that same library afterward.
- **Unattended import:** `--skip-dups --no-progress --report FRESH.json`, with a new report path per job (`--report` overwrites).
  - `--dry-run` writes no report.
  - `--resume` skips already-imported paths before they reach the report, so a first import leaves it off.
  - `--stop-on-error` makes osxphotos kill and restart Photos at its threshold, so leave it off.
- **Duplicate prevention is not guaranteed:** `--skip-dups` matches photos by fingerprint and videos only by filename and size.
- **Per-file import errors leave the exit code at zero.** Read the JSON report: a top-level array with one record per file group (a Live Photo or RAW pair is one record). For every input, check `imported`, `error`, `skipped`, `duplicate_of` and a non-empty `uuid`. `skipped` means a match already existed.
- **Placement is proven by UUID**, never by exit status: `photos query --library LIBRARY --uuid UUID --json --field uuid '{uuid}' --mute` must return that UUID. Several UUIDs: repeat `--uuid`, or use `--uuid-from-file`.
- After a timeout or crash, read the report and query the library before importing again.
