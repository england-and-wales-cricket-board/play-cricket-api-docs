# Match Summary

Returns a list of fixtures — both upcoming and played — for a site. Returns fixture details, team names, ground, and officials, but **no result or scorecard data**. Use [Result Summary](./result-summary.md) if you need result information.

This endpoint is primarily used at the start of a season to build a fixture list, then polled at regular intervals using `from_entry_date` to capture any changes.

**Endpoint**
```
GET https://www.play-cricket.com/api/v2/matches.json
```

---

## Parameters

!!! warning "Always specify a season"
    Without `season`, this endpoint returns fixtures across **all seasons** — potentially several thousand records on a league site. Always pass `season` unless you have a specific reason to retrieve the full historical dataset.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |
| `site_id` | integer | Yes | The ID of the club or league site |
| `season` | string | **Recommended** | The season year, e.g. `2024`. Omitting this returns all fixtures across all seasons |
| `division_id` | integer | No | Filter to a specific division |
| `cup_id` | integer | No | Filter to a specific cup |
| `team_id` | integer | No | Filter to a specific team |
| `competition_type` | string | No | Filter by competition type. Accepted values: `League`, `Cup`, `Friendly` |
| `from_entry_date` | string | No | Return only fixtures updated on or after this date. Format: `dd/mm/yyyy` |
| `end_entry_date` | string | No | Return only fixtures updated on or before this date. Format: `dd/mm/yyyy` |
| `include_unpublished` | string | No | Pass `yes` to include unpublished fixtures. Defaults to excluding them |

---

## Example Requests

**All fixtures for a club in a season:**
```
GET https://www.play-cricket.com/api/v2/matches.json?site_id=3540&season=2024&api_token=YOUR_TOKEN
```

**Fixtures updated in a date range (for polling changes):**
```
GET https://www.play-cricket.com/api/v2/matches.json?site_id=3540&season=2024&api_token=YOUR_TOKEN&from_entry_date=27/11/2024&end_entry_date=28/11/2024
```

**League fixtures only for a specific division:**
```
GET https://www.play-cricket.com/api/v2/matches.json?site_id=534&season=2024&division_id=110530&competition_type=League&api_token=YOUR_TOKEN
```

---

## Example Response

```json
{
  "matches": [
    {
      "id": 5681166,
      "status": "New",
      "published": "Yes",
      "last_updated": "11/04/2024",
      "league_name": "Warwickshire County Cricket League",
      "league_id": "534",
      "competition_name": "Premier Division",
      "competition_id": "110530",
      "division_id": "110530",
      "competition_type": "League",
      "match_type": "Limited Overs",
      "game_type": "Standard",
      "season": "2024",
      "match_date": "08/06/2024",
      "match_time": "11:30",
      "ground_name": "Edgbaston Road",
      "ground_id": "6065",
      "ground_latitude": "52.313748",
      "ground_longitude": "-1.4538062",
      "home_club_name": "Chingford CC",
      "home_team_name": "1st XI",
      "home_team_id": "12640",
      "home_club_id": "1835",
      "away_club_name": "Chingford Quackers CC",
      "away_team_name": "1st XI",
      "away_team_id": "208057",
      "away_club_id": "14793",
      "umpire_1_name": "Martin Johnson",
      "umpire_1_id": "67824",
      "umpire_2_name": "",
      "umpire_2_id": "",
      "umpire_3_name": "",
      "umpire_3_id": "",
      "referee_name": "",
      "referee_id": "",
      "scorer_1_name": "Amber Leonard",
      "scorer_1_id": "3778646",
      "scorer_2_name": "",
      "scorer_2_id": ""
    }
  ]
}
```

---

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Unique match identifier. Use as `match_id` in [Match Detail](./match-detail.md) |
| `status` | string | `New` (active) or `Deleted` (removed) |
| `published` | string | `Yes` or `No` — whether the fixture is publicly visible |
| `last_updated` | string | Date this record was last modified. Format: `dd/mm/yyyy` |
| `league_name` | string | Name of the league administering this match |
| `league_id` | string | ID of the league site |
| `competition_name` | string | Name of the division or cup |
| `competition_id` | string | ID of the competition (division or cup) |
| `division_id` | string | ID of the specific division within the league. Empty for cups and friendlies. Note: division IDs are ephemeral — they change each season |
| `competition_type` | string | `League`, `Cup`, or `Friendly` |
| `match_type` | string | e.g. `Limited Overs`, `Declaration` |
| `game_type` | string | e.g. `Standard` |
| `season` | string | Season year, e.g. `2024` |
| `match_date` | string | Date of the fixture. Format: `dd/mm/yyyy` |
| `match_time` | string | Start time of the fixture. Format: `HH:MM` |
| `ground_name` | string | Name of the ground |
| `ground_id` | string | Unique identifier for the ground |
| `ground_latitude` | string | Latitude coordinate of the ground |
| `ground_longitude` | string | Longitude coordinate of the ground |
| `home_club_name` | string | Name of the home club |
| `home_team_name` | string | Name of the home team (e.g. `1st XI`) |
| `home_team_id` | string | Unique identifier for the home team |
| `home_club_id` | string | Unique identifier for the home club |
| `away_club_name` | string | Name of the away club |
| `away_team_name` | string | Name of the away team |
| `away_team_id` | string | Unique identifier for the away team |
| `away_club_id` | string | Unique identifier for the away club |
| `umpire_1_name` | string | Name of the first umpire, if appointed |
| `umpire_1_id` | string | ID of the first umpire |
| `umpire_2_name` | string | Name of the second umpire, if appointed |
| `umpire_2_id` | string | ID of the second umpire |
| `umpire_3_name` | string | Name of the third umpire, if appointed |
| `umpire_3_id` | string | ID of the third umpire |
| `referee_name` | string | Name of the referee, if appointed |
| `referee_id` | string | ID of the referee |
| `scorer_1_name` | string | Name of the first scorer, if recorded |
| `scorer_1_id` | string | ID of the first scorer |
| `scorer_2_name` | string | Name of the second scorer, if recorded |
| `scorer_2_id` | string | ID of the second scorer |

---

## Notes

- For friendly fixtures, `league_name`, `league_id`, `competition_name`, and `competition_id` will be empty strings.
- The `from_entry_date` and `end_entry_date` parameters filter by `last_updated`, not by match date. A fixture's `last_updated` changes when its result or scorecard is added or amended. To retrieve fixtures changed on a specific day, set `from_entry_date` to that day and `end_entry_date` to the following day.
- Unpublished matches are fixtures created in the league system but not yet made visible to clubs or the public. The vast majority of integrations should leave `include_unpublished` unset.
- This endpoint returns **no result data**. For results, use [Result Summary](./result-summary.md).
