# Changelog

This page tracks changes to the Play-Cricket API. The current API version is `v3`.

---

## How to read this log

Each entry notes the affected endpoint, the nature of the change, and any action required for existing integrations.

---

## Known additions since original documentation

The following fields and behaviours have been added or clarified relative to the original API documentation:

### Result Summary

| Change | Detail |
|--------|--------|
| **New field: `countdown_cricket`** | Added to result summary responses. Values: `"yes"` / `"no"` |
| **New field: `balls_per_innings`** | Added alongside `no_of_overs` to support ball-count formats |
| **New field: `balls`** (innings level) | Added to innings entries alongside `overs` |
| **New field: `forfeited_innings`** | Boolean indicating a forfeited innings |
| **New field: `revised_target_balls`** | Added alongside `revised_target_runs` and `revised_target_overs` |
| **New field: `home_confirmed` / `away_confirmed`** | Indicates whether each club has confirmed the result |
| **New field: `result_locked` / `scorecard_locked`** | Indicates lock status set by league administrators |
| **Timestamp support on `from_entry_date` / `end_entry_date`** | These parameters now accept `dd/mm/yyyyThh:mm:ss` format for precision polling. Previously accepted date only |

### Match Summary

| Change | Detail |
|--------|--------|
| **New field: `ground_latitude` / `ground_longitude`** | Geographic coordinates added to fixture records |
| **New parameter: `include_unpublished`** | Allows retrieval of fixtures not yet published to the public site |
| **New field: `ground_name` / `ground_id`** | These were not present in earlier versions of the match summary response |

---

## Versioning

The API has a `v2` and a `v3`. `v3` adds pagination to supported endpoints and will enforce additional required parameters (such as `season` on matches and `division_id`/`team_id` on results). All new integrations should use `v3`. The `v2` endpoints remain available for legacy integrations during a transition period.

---

*This changelog will be updated as new fields, parameters, or endpoints are introduced. If you notice a discrepancy between this documentation and API behaviour, please contact the Play-Cricket team.*
