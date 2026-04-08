# List Clubs

Returns a list of clubs registered on Play-Cricket, with optional filtering by county or last-updated date.

**Endpoint**
```
GET https://www.play-cricket.com/api/v2/clubs.json
```

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |
| `county_id` | integer | No | Filter clubs by county. Use the `id` from the [CCBs endpoint](./county-cricket-boards.md) |
| `from_entry_date` | string | No | Return only clubs updated on or after this date. Format: `dd/mm/yyyy` |
| `end_entry_date` | string | No | Return only clubs updated on or before this date. Format: `dd/mm/yyyy` |

---

## Example Requests

**All clubs nationally:**
```
GET https://www.play-cricket.com/api/v2/clubs.json?api_token=YOUR_TOKEN
```

**Clubs in a specific county:**
```
GET https://www.play-cricket.com/api/v2/clubs.json?api_token=YOUR_TOKEN&county_id=37
```

**Clubs updated in a date range (for polling changes):**
```
GET https://www.play-cricket.com/api/v2/clubs.json?api_token=YOUR_TOKEN&from_entry_date=01/01/2024&end_entry_date=01/02/2024
```

---

## Example Response

```json
{
  "clubs": [
    {
      "id": 1835,
      "name": "Chingford CC",
      "county_id": 26,
      "status": "New",
      "last_updated": "15/03/2024"
    },
    {
      "id": 14793,
      "name": "Chingford Quackers CC",
      "county_id": 26,
      "status": "New",
      "last_updated": "22/01/2024"
    }
  ]
}
```

---

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Unique identifier for the club. Stable across seasons. Use as `club_id` in other endpoints |
| `name` | string | Club name |
| `county_id` | integer | The county this club belongs to |
| `status` | string | `New` (active) or `Deleted` (removed) |
| `last_updated` | string | Date this record was last modified. Format: `dd/mm/yyyy` |

---

## Notes

- Club `id` values are stable and do not change between seasons.
- To retrieve teams for a club, use the [Teams endpoint](./teams.md) with the club's `id` as the `site_id`.
- Use `from_entry_date` and `end_entry_date` together to poll for clubs added or changed since your last sync. See [Common Patterns](../common-patterns.md) for guidance on date filtering.
