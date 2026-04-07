# Date Format Reference

The Play-Cricket API uses dates in multiple formats depending on the endpoint and parameter. This page collects all date behaviour in one place.

---

## Summary Table

| Context | Format | Example | Time component |
|---------|--------|---------|----------------|
| Most `from_entry_date` / `end_entry_date` parameters | `dd/mm/yyyy` | `27/11/2024` | Defaults to `00:00:00` |
| Result Summary `from_entry_date` / `end_entry_date` | `dd/mm/yyyyThh:mm:ss` | `27/11/2024T14:30:00` | Full timestamp supported |
| `from_match_date` / `end_match_date` | `dd/mm/yyyy` | `02/09/2024` | Date only, no time |
| Response date fields (e.g. `last_updated`, `match_date`) | `dd/mm/yyyy` | `15/03/2024` | Date only |

---

## Entry Date Parameters (`from_entry_date` / `end_entry_date`)

These parameters filter by the `last_updated` field — the date a record was created or most recently changed.

### On most endpoints

Accepts dates in `dd/mm/yyyy` format. The time component defaults to `00:00:00` (midnight at the start of the day).

**To retrieve records changed on a specific day**, set `from_entry_date` to that day and `end_entry_date` to the *following* day:

```
from_entry_date=27/11/2024&end_entry_date=28/11/2024
```

This works because the range is `27/11/2024 00:00:00` to `28/11/2024 00:00:00`, capturing the full 24-hour period.

### On Result Summary only

Accepts full timestamps in `dd/mm/yyyyThh:mm:ss` format, allowing precision polling down to the second.

**To retrieve records updated in a specific hour:**
```
from_entry_date=27/11/2024T14:00:00&end_entry_date=27/11/2024T14:59:59
```

**To retrieve records updated on a full day** (equivalent to the date-only behaviour):
```
from_entry_date=27/11/2024T00:00:00&end_entry_date=27/11/2024T23:59:59
```

If you pass a date without the `Thh:mm:ss` part on the Result Summary endpoint, it defaults to `00:00:00`, just like other endpoints.

---

## Match Date Parameters (`from_match_date` / `end_match_date`)

Available only on [Result Summary](../reference/result-summary.md). These filter by the **date the match was played**, not the date the record was updated.

Both parameters use `dd/mm/yyyy` format and are **inclusive** — a record on either boundary date will be included.

**To retrieve all results for one match day:**
```
from_match_date=07/09/2024&end_match_date=07/09/2024
```

**To retrieve results for a week's worth of matches:**
```
from_match_date=02/09/2024&end_match_date=08/09/2024
```

---

## Response Date Fields

Dates returned in API responses always use `dd/mm/yyyy` format. They do not include a time component.

| Field | Endpoints | Description |
|-------|-----------|-------------|
| `last_updated` | Most endpoints | Date the record was last modified |
| `match_date` | Match Summary, Result Summary, Match Detail | Date the match was or is scheduled to be played |

---

## Common Mistakes

| Mistake | What happens |
|---------|-------------|
| Setting `from_entry_date` and `end_entry_date` to the same date (e.g. both `27/11/2024`) | No records returned — the range `00:00:00` to `00:00:00` is a zero-length window |
| Omitting the `T` separator on Result Summary timestamps | The time defaults to `00:00:00`, which may cause you to miss records updated later that day |
| Using `mm/dd/yyyy` format | Dates will be misinterpreted or rejected |
