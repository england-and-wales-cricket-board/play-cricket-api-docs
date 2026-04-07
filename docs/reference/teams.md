# List Teams for a Site

Returns a list of teams associated with a specific club or CCB site.

**Endpoint**
```
GET https://play-cricket.com/api/v2/sites/{site_id}/teams.json
```

Replace `{site_id}` with the numeric ID of the Play-Cricket site you want to query.

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |
| `site_type` | string | No | Filter by site type. Accepted values: `club`, `CCB` |
| `from_entry_date` | string | No | Return only teams updated on or after this date. Format: `dd/mm/yyyy` |
| `end_entry_date` | string | No | Return only teams updated on or before this date. Format: `dd/mm/yyyy` |

---

## Example Requests

**All teams for a club site:**
```
GET https://play-cricket.com/api/v2/sites/3540/teams.json?api_token=YOUR_TOKEN
```

**Teams updated within a date range:**
```
GET https://play-cricket.com/api/v2/sites/3540/teams.json?api_token=YOUR_TOKEN&from_entry_date=01/01/2024&end_entry_date=01/04/2024
```

---

## Example Response

```json
{
  "teams": [
    {
      "id": 175868,
      "status": "New",
      "last_updated": "12/03/2024",
      "site_id": 3540,
      "team_name": "1st XI",
      "other_team_name": "",
      "nickname": "The Quackers",
      "team_captain": "Joe Bloggs"
    },
    {
      "id": 175869,
      "status": "New",
      "last_updated": "12/03/2024",
      "site_id": 3540,
      "team_name": "2nd XI",
      "other_team_name": "",
      "nickname": "",
      "team_captain": ""
    }
  ]
}
```

---

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Unique identifier for the team. Stable across seasons. Use as `team_id` in other endpoints |
| `status` | string | `New` (active) or `Deleted` (removed) |
| `last_updated` | string | Date this record was last modified. Format: `dd/mm/yyyy` |
| `site_id` | integer | The site this team belongs to |
| `team_name` | string | The team's official name (e.g. `1st XI`, `2nd XI`) |
| `other_team_name` | string | An alternative or historical name for the team, if set |
| `nickname` | string | An informal name for the team, if set |
| `team_captain` | string | Name of the team captain, if set |

---

## Notes

- Team `id` values are stable and do not change between seasons.
- To retrieve players associated with a club, use the [Players endpoint](./players.md).
- To retrieve which teams are in a specific division, use [Teams in Division](./teams-in-division.md).
