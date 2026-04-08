# List Teams in a Division

Returns a list of all teams competing in a specified division or cup.

**Endpoint**
```
GET https://www.play-cricket.com/api/v2/competition_teams.json
```

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |
| `id` | integer | Yes | The ID of the division or cup. Obtain this from [List Divisions & Cups](./competitions.md) |

---

## Example Request

```
GET https://www.play-cricket.com/api/v2/competition_teams.json?id=69548&api_token=YOUR_TOKEN
```

---

## Example Response

```json
{
  "competition_teams": [
    {
      "club_id": "1835",
      "club_name": "Chingford CC",
      "team_id": "10001",
      "team_name": "2nd XI"
    },
    {
      "club_id": "14793",
      "club_name": "Chingford Quackers CC",
      "team_id": "23232",
      "team_name": "2nd XI"
    }
  ]
}
```

---

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `club_id` | string | Unique identifier for the club. Stable across seasons |
| `club_name` | string | Name of the club |
| `team_id` | string | Unique identifier for the team. Stable across seasons |
| `team_name` | string | The team designation (e.g. `1st XI`, `2nd XI`) |

---

## Notes

- The `id` parameter accepts either a `division_id` (from divisions) or a `cup_id` (from cups). Retrieve these via [List Divisions & Cups](./competitions.md).
- Remember that division/cup IDs change each season. Use the current season's ID.
- The `team_id` values returned here can be used as the `team_id` filter on [Match Summary](./match-summary.md) and [Result Summary](./result-summary.md).
