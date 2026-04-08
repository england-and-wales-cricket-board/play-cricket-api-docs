# Common Patterns

---

## Filtering by Date

Several endpoints support date-based filtering via pairs of parameters. There are two distinct types of date filter — read carefully as they behave differently.

---

### Entry Date Filtering (`from_entry_date` / `end_entry_date`)

These parameters filter by the **last_updated** field — the date a record was created or last modified. Use this to poll for changes since your last call.

#### On most endpoints (Clubs, Teams, Match Summary)

Accepts dates in `dd/mm/yyyy` format. Times default to `00:00:00`.

To retrieve records changed on a specific day, set `from_entry_date` to that day and `end_entry_date` to the following day:

```
from_entry_date=27/11/2024&end_entry_date=28/11/2024
```

#### On Result Summary only

Accepts full timestamps in `dd/mm/yyyyThh:mm:ss` format, allowing hour-precision polling. If you omit the time component, it defaults to `00:00:00`.

To retrieve all results updated on a specific day:
```
from_entry_date=27/11/2024T00:00:00&end_entry_date=27/11/2024T23:59:59
```

---

### Match Date Filtering (`from_match_date` / `end_match_date`)

Available on **Result Summary** only. These parameters filter by the **date the match was played**, not the date the record was last updated.

Both dates are **inclusive**. To retrieve matches played on a single day:
```
from_match_date=02/09/2024&end_match_date=02/09/2024
```

---

## Polling for Changes

The intended pattern for keeping data in sync:

1. At the **start of the season**, call the relevant endpoint without date filters to retrieve the full dataset
2. **On each subsequent poll**, pass `from_entry_date` and `end_entry_date` to retrieve only records that changed since your last call
3. Check the `status` field — records with `"status": "Deleted"` should be removed from your local store

---

## The `status` Field

Most endpoints return a `status` field on each record. This indicates whether the record is active or has been removed.

| Value | Meaning |
|-------|---------|
| `"New"` | Record is active and current |
| `"Deleted"` | Record has been removed — delete it from your local data |

---

## The `published` Field

On match endpoints, `published` indicates whether a fixture is visible on the public-facing Play-Cricket site.

| Value | Meaning |
|-------|---------|
| `"Yes"` | Fixture is published and visible |
| `"No"` | Fixture exists in the system but is not yet publicly visible |

By default, unpublished matches are **not returned** by the API. Pass `include_unpublished=yes` to include them. Most applications will not need this.

---

## Always Specify a Season

!!! warning
    On Match Summary, `season` is optional but omitting it returns fixtures across **all seasons** — potentially several thousand records. On Result Summary, `season` is required, but a season-only request against a league site can still return 1,000+ records.

    Always pair `season` with at least one additional filter (`division_id`, `team_id`, or a date range) on any site with significant data volume.

```
# Good — season + division filter
GET /api/v2/matches.json?site_id=3540&season=2024&division_id=110530&api_token=xxx

# Acceptable for a small club site
GET /api/v2/matches.json?site_id=3540&season=2024&api_token=xxx

# Avoid — returns all fixtures for all seasons
GET /api/v2/matches.json?site_id=3540&api_token=xxx
```

---

## Large Result Sets

| Scenario | Potential record count |
|----------|----------------------|
| Match Summary — no `season` on a league site | Several thousand |
| Result Summary — `season` only on a league site | 1,000+ |
| Result Summary — `season` only on a club site | 100+ |

Always apply the most specific filters available before making requests in production.
