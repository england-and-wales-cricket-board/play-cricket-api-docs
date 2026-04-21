# List Divisions & Cups

Returns a list of divisions or cups for a specified league and season.

**Endpoint**
```
GET https://www.play-cricket.com/api/v3/competitions.json
```

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |
| `league_id` | integer | Yes | The ID of the league site. Obtain this from [List League Sites](./league-sites.md) |
| `season` | string | Yes | The season year, e.g. `2024` |
| `competition_type` | string | Yes | The type of competition to return. Accepted values: `divisions`, `cups` |

---

## Example Requests

**Divisions in a league for a season:**
```
GET https://www.play-cricket.com/api/v3/competitions.json?league_id=296&season=2024&competition_type=divisions&api_token=YOUR_TOKEN
```

**Cups in a league for a season:**
```
GET https://www.play-cricket.com/api/v3/competitions.json?league_id=296&season=2024&competition_type=cups&api_token=YOUR_TOKEN
```

---

## Example Response

```json
{
  "competitions": [
    {
      "id": 69548,
      "name": "Division 1"
    },
    {
      "id": 69563,
      "name": "Division 10 North"
    }
  ]
}
```

---

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Unique identifier for this competition. Use as `division_id` or `cup_id` in other endpoints. **Changes every season.** |
| `name` | string | Name of the division or cup |

---

## Notes

- The `id` returned here maps to `division_id` (for divisions) or `cup_id` (for cups) on the Match Summary, Result Summary, League Table, and Teams in Division endpoints.
- **The `id` is unique per season.** The same division in a different year will have a different ID. Always retrieve fresh competition IDs at the start of each season rather than storing them permanently.
- Make two separate calls — one with `competition_type=divisions` and one with `competition_type=cups` — if you need both.
