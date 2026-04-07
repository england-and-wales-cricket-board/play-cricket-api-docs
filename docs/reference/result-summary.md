# Result Summary

Returns completed matches (and matches in progress) with result, points, and innings totals. Returns everything in [Match Summary](./match-summary.md) plus result information and innings-level scoring — but **not** individual batting or bowling figures. Use [Match Detail](./match-detail.md) for full scorecards.

**Endpoint**
```
GET https://play-cricket.com/api/v2/result_summary.json
```

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |
| `site_id` | integer | Yes | The ID of the club or league site |
| `season` | string | Yes | The season year, e.g. `2024` |
| `division_id` | integer | No | Filter to a specific division |
| `cup_id` | integer | No | Filter to a specific cup |
| `team_id` | integer | No | Filter to a specific team |
| `competition_type` | string | No | Filter by competition type. Accepted values: `League`, `Cup`, `Friendly` |
| `from_match_date` | string | No | Return only matches played on or after this date. Format: `dd/mm/yyyy`. Inclusive |
| `end_match_date` | string | No | Return only matches played on or before this date. Format: `dd/mm/yyyy`. Inclusive |
| `from_entry_date` | string | No | Return only records updated on or after this date/time. Format: `dd/mm/yyyyThh:mm:ss` |
| `end_entry_date` | string | No | Return only records updated on or before this date/time. Format: `dd/mm/yyyyThh:mm:ss` |

---

## Example Requests

**All results for a division on a specific match day:**
```
GET https://play-cricket.com/api/v2/result_summary.json?site_id=534&season=2024&division_id=110530&from_match_date=07/09/2024&end_match_date=07/09/2024&api_token=YOUR_TOKEN
```

**All results updated in the last hour (polling for new results):**
```
GET https://play-cricket.com/api/v2/result_summary.json?site_id=534&season=2024&from_entry_date=07/09/2024T14:00:00&end_entry_date=07/09/2024T15:00:00&api_token=YOUR_TOKEN
```

**All results for a specific team in a season:**
```
GET https://play-cricket.com/api/v2/result_summary.json?site_id=3540&season=2024&team_id=175868&api_token=YOUR_TOKEN
```

---

## Example Response

```json
{
  "result_summary": [
    {
      "id": 5694618,
      "status": "New",
      "published": "Yes",
      "last_updated": "07/09/2024",
      "league_name": "Warwickshire County Cricket League",
      "league_id": "534",
      "competition_name": "Premier Division",
      "competition_id": "110530",
      "competition_type": "League",
      "match_type": "Limited Overs",
      "game_type": "Standard",
      "countdown_cricket": "no",
      "match_date": "07/09/2024",
      "match_time": "11:30",
      "ground_name": "Handsworth Park",
      "ground_id": "4932",
      "home_team_name": "1st XI",
      "home_team_id": "65134",
      "home_club_name": "Handsworth CC",
      "home_club_id": "3144",
      "away_team_name": "1st XI",
      "away_team_id": "33573",
      "away_club_name": "Solihull Blossomfield CC",
      "away_club_id": "1225",
      "umpire_1_name": "Peter Gibson",
      "umpire_1_id": "3218559",
      "umpire_2_name": "Adam Hitchcock",
      "umpire_2_id": "12683",
      "umpire_3_name": "",
      "umpire_3_id": "",
      "referee_name": "",
      "referee_id": "",
      "scorer_1_name": "Sushil Yadav",
      "scorer_1_id": "5788489",
      "scorer_2_name": "",
      "scorer_2_id": "",
      "toss_won_by_team_id": "65134",
      "toss": "Handsworth CC - 1st XI won the toss and elected to field",
      "batted_first": "33573",
      "no_of_overs": "50",
      "balls_per_innings": "",
      "no_of_innings": "1",
      "result": "W",
      "result_description": "Handsworth CC - 1st XI - Win 20pts",
      "result_applied_to": "65134",
      "home_confirmed": "false",
      "away_confirmed": "false",
      "result_locked": "true",
      "scorecard_locked": "true",
      "match_notes": "",
      "points": [
        {
          "team_id": 65134,
          "game_points": "20",
          "penalty_points": "0.0",
          "bonus_points_together": "0.0",
          "bonus_points_batting": "0.0",
          "bonus_points_bowling": "0.0",
          "bonus_points_2nd_innings_together": ""
        },
        {
          "team_id": 33573,
          "game_points": "0",
          "penalty_points": "0.0",
          "bonus_points_together": "2.0",
          "bonus_points_batting": "0.0",
          "bonus_points_bowling": "2.0",
          "bonus_points_2nd_innings_together": ""
        }
      ],
      "innings": [
        {
          "team_batting_id": "33573",
          "innings_number": 1,
          "extra_byes": "5",
          "extra_leg_byes": "3",
          "extra_wides": "5",
          "extra_no_balls": "2",
          "extra_penalty_runs": "0",
          "penalties_runs_awarded_in_other_innings": "0",
          "total_extras": "15",
          "runs": "131",
          "wickets": "10",
          "overs": "38.5",
          "balls": "",
          "declared": false,
          "forfeited_innings": false,
          "revised_target_runs": "",
          "revised_target_overs": "50.0",
          "revised_target_balls": ""
        },
        {
          "team_batting_id": "65134",
          "innings_number": 1,
          "extra_byes": "0",
          "extra_leg_byes": "7",
          "extra_wides": "10",
          "extra_no_balls": "0",
          "extra_penalty_runs": "0",
          "penalties_runs_awarded_in_other_innings": "0",
          "total_extras": "17",
          "runs": "132",
          "wickets": "5",
          "overs": "33.0",
          "balls": "",
          "declared": false,
          "forfeited_innings": false,
          "revised_target_runs": "",
          "revised_target_overs": "50.0",
          "revised_target_balls": ""
        }
      ]
    }
  ]
}
```

---

## Response Fields

### Match-level fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Unique match identifier. Use as `match_id` in [Match Detail](./match-detail.md) |
| `status` | string | `New` (active) or `Deleted` (removed) |
| `published` | string | `Yes` or `No` |
| `last_updated` | string | Date this record was last modified. Format: `dd/mm/yyyy` |
| `league_name` | string | Name of the administering league |
| `league_id` | string | ID of the league site |
| `competition_name` | string | Name of the division or cup |
| `competition_id` | string | ID of the competition |
| `competition_type` | string | `League`, `Cup`, or `Friendly` |
| `match_type` | string | e.g. `Limited Overs`, `Declaration` |
| `game_type` | string | e.g. `Standard` |
| `countdown_cricket` | string | `yes` or `no` — indicates if the match uses countdown cricket format |
| `match_date` | string | Date the match was played. Format: `dd/mm/yyyy` |
| `match_time` | string | Start time. Format: `HH:MM` |
| `ground_name` | string | Name of the ground |
| `ground_id` | string | Unique identifier for the ground |
| `home_team_name` | string | Home team designation |
| `home_team_id` | string | Home team identifier |
| `home_club_name` | string | Home club name |
| `home_club_id` | string | Home club identifier |
| `away_team_name` | string | Away team designation |
| `away_team_id` | string | Away team identifier |
| `away_club_name` | string | Away club name |
| `away_club_id` | string | Away club identifier |
| `umpire_1_name` | string | First umpire name |
| `umpire_1_id` | string | First umpire identifier |
| `umpire_2_name` | string | Second umpire name |
| `umpire_2_id` | string | Second umpire identifier |
| `umpire_3_name` | string | Third umpire name |
| `umpire_3_id` | string | Third umpire identifier |
| `referee_name` | string | Referee name |
| `referee_id` | string | Referee identifier |
| `scorer_1_name` | string | First scorer name |
| `scorer_1_id` | string | First scorer identifier |
| `scorer_2_name` | string | Second scorer name |
| `scorer_2_id` | string | Second scorer identifier |
| `toss_won_by_team_id` | string | Team ID of the side that won the toss |
| `toss` | string | Human-readable toss description |
| `batted_first` | string | Team ID of the side that batted first |
| `no_of_overs` | string | Maximum overs per innings |
| `balls_per_innings` | string | Maximum balls per innings (alternative to overs in some formats) |
| `no_of_innings` | string | Number of innings per side |
| `result` | string | Result code. See [Enum Values](../appendices/enum-values.md) |
| `result_description` | string | Human-readable result description |
| `result_applied_to` | string | Team ID of the side the result is applied to (usually the winning team) |
| `home_confirmed` | string | Whether the home club has confirmed the result (`true`/`false`) |
| `away_confirmed` | string | Whether the away club has confirmed the result (`true`/`false`) |
| `result_locked` | string | Whether the result has been locked by a league administrator (`true`/`false`) |
| `scorecard_locked` | string | Whether the scorecard has been locked (`true`/`false`) |
| `match_notes` | string | Commentary and match highlights, may contain HTML |

### Points array fields (`points[]`)

One entry per team.

| Field | Type | Description |
|-------|------|-------------|
| `team_id` | integer | Team identifier |
| `game_points` | string | Points awarded for the match result |
| `penalty_points` | string | Penalty points deducted |
| `bonus_points_together` | string | Combined bonus points (used when batting and bowling bonuses are not tracked separately) |
| `bonus_points_batting` | string | Batting bonus points |
| `bonus_points_bowling` | string | Bowling bonus points |
| `bonus_points_2nd_innings_together` | string | Combined bonus points for a second innings |

### Innings array fields (`innings[]`)

One entry per innings. For a standard one-innings-per-side match there will be two entries.

| Field | Type | Description |
|-------|------|-------------|
| `team_batting_id` | string | ID of the team batting in this innings |
| `innings_number` | integer | Innings number (1 or 2) |
| `extra_byes` | string | Byes conceded |
| `extra_leg_byes` | string | Leg byes conceded |
| `extra_wides` | string | Wides conceded |
| `extra_no_balls` | string | No balls conceded |
| `extra_penalty_runs` | string | Penalty runs |
| `penalties_runs_awarded_in_other_innings` | string | Penalty runs that will count in the other team's innings |
| `total_extras` | string | Total extras |
| `runs` | string | Total runs scored |
| `wickets` | string | Wickets fallen |
| `overs` | string | Overs faced |
| `balls` | string | Balls faced (used in some formats instead of overs) |
| `declared` | boolean | Whether the innings was declared |
| `forfeited_innings` | boolean | Whether the innings was forfeited |
| `revised_target_runs` | string | Revised target (e.g. Duckworth-Lewis) |
| `revised_target_overs` | string | Revised overs target |
| `revised_target_balls` | string | Revised balls target |

---

## Notes

- **Watch your result set size.** Calling this endpoint for a full season on a league site without additional filters can return 1,000+ records. Always apply at least one of `division_id`, `cup_id`, `team_id`, or a date range.
- The `from_entry_date` / `end_entry_date` parameters on this endpoint accept a **datetime** format (`dd/mm/yyyyThh:mm:ss`), unlike most other endpoints which accept date only. This allows hour-precision polling for new results. If you pass a date without a time, it defaults to `00:00:00`.
- The `last_updated` field changes whenever the result is updated, the scorecard is modified, or the result/scorecard is locked or unlocked. Polling on `from_entry_date` will catch all of these changes.
- `match_notes` may contain HTML markup. Strip or sanitise as appropriate for your display context.
- For individual batting and bowling figures, use [Match Detail](./match-detail.md).
