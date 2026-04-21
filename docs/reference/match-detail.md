# Match Detail

Returns the full scorecard for a single match, including team sheets, batting figures, bowling figures, and fall of wickets. Also includes all fixture and result information from [Result Summary](./result-summary.md).

**Endpoint**
```
GET https://www.play-cricket.com/api/v3/match_detail.json
```

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |
| `match_id` | integer | Yes | The unique match identifier. Obtain from [Match Summary](./match-summary.md) or [Result Summary](./result-summary.md) |

---

## Example Request

```
GET https://www.play-cricket.com/api/v3/match_detail.json?match_id=5694618&api_token=YOUR_TOKEN
```

---

## Example Response

The response structure is nested. A condensed representation is shown below with all fields present.

```json
{
  "match_details": [
    {
      "id": 5694618,
      "match_id": "5694618",
      "status": "New",
      "published": "Yes",
      "last_updated": "07/09/2024",
      "league_name": "Warwickshire County Cricket League",
      "league_id": "534",
      "competition_name": "Premier Division",
      "competition_id": "110530",
      "competition_type": "League",
      "match_type": "Declaration",
      "game_type": "Standard",
      "match_date": "07/09/2024",
      "match_time": "10:45",
      "ground_name": "Peter May Sports Centre",
      "ground_id": "13909",
      "home_team_name": "3rd XI",
      "home_team_id": "12640",
      "home_club_name": "Chingford CC",
      "home_club_id": "1835",
      "away_team_name": "2nd XI",
      "away_team_id": "208057",
      "away_club_name": "Chingford Quackers CC",
      "away_club_id": "14793",
      "umpire_1_name": "Martin Johnson",
      "umpire_1_id": "67824",
      "umpire_2_name": "Georgie Best",
      "umpire_2_id": "65280",
      "umpire_3_id": "",
      "referee_id": "",
      "scorer_1_name": "Amber Leonard",
      "scorer_1_id": "3778646",
      "scorer_2_name": "Chew Leonard",
      "scorer_2_id": "3778631",
      "toss_won_by_team_id": "12640",
      "toss": "Chingford CC - 3rd XI won the toss and elected to bat",
      "batted_first": "12640",
      "no_of_overs": "50",
      "no_of_innings": "1",
      "no_of_days": "",
      "no_of_players": "11",
      "no_of_reserves": "0",
      "result": "W",
      "result_description": "Chingford Quackers CC - 2nd XI - Won",
      "result_applied_to": "208057",
      "match_notes": "What a match!",
      "points": [
        {
          "team_id": "12640",
          "game_points": "0",
          "penalty_points": "1",
          "bonus_points_together": "",
          "bonus_points_batting": "3",
          "bonus_points_bowling": "0",
          "bonus_points_2nd_innings_together": "",
          "bonus_points_2nd_innings_batting": "",
          "bonus_points_2nd_innings_bowling": ""
        },
        {
          "team_id": "208057",
          "game_points": "20",
          "penalty_points": "",
          "bonus_points_together": "",
          "bonus_points_batting": "4",
          "bonus_points_bowling": "1",
          "bonus_points_2nd_innings_together": "",
          "bonus_points_2nd_innings_batting": "",
          "bonus_points_2nd_innings_bowling": ""
        }
      ],
      "match_result_types": [
        ["Chingford CC - 3rd XI - Won", "582111#12640"],
        ["Chingford Quackers CC - 2nd XI - Won", "582111#208057"],
        ["Tied", 582117],
        ["Cancelled", 582113],
        ["Abandoned", 582114],
        ["Chingford CC - 3rd XI - Conceded", "582115#208057"],
        ["Chingford Quackers CC - 2nd XI - Conceded", "582116#12640"],
        ["Match In Progress", 14]
      ],
      "players": [
        {
          "home_team": [
            {
              "position": 1,
              "player_name": "Chew Leonard",
              "player_id": 3778631,
              "captain": false,
              "wicket_keeper": false
            },
            {
              "position": 2,
              "player_name": "Mars Leonard",
              "player_id": 3778630,
              "captain": true,
              "wicket_keeper": true
            }
          ]
        },
        {
          "away_team": [
            {
              "position": 1,
              "player_name": "Amber Duck",
              "player_id": 3778926,
              "captain": true,
              "wicket_keeper": false
            },
            {
              "position": 2,
              "player_name": "Smoke Duck",
              "player_id": 3778927,
              "captain": false,
              "wicket_keeper": false
            }
          ]
        }
      ],
      "innings": [
        {
          "team_batting_name": "Chingford CC - 3rd XI",
          "team_batting_id": "12640",
          "innings_number": 1,
          "extra_byes": "4",
          "extra_leg_byes": "6",
          "extra_wides": "3",
          "extra_no_balls": "2",
          "extra_penalty_runs": "0",
          "penalties_runs_awarded_in_other_innings": "0",
          "total_extras": "15",
          "runs": "185",
          "wickets": "10",
          "overs": "48.3",
          "declared": false,
          "revised_target_runs": "",
          "revised_target_overs": "",
          "bat": [
            {
              "position": "1",
              "batsman_name": "Chew Leonard",
              "batsman_id": "3778631",
              "how_out": "b",
              "fielder_name": "",
              "fielder_id": "",
              "bowler_name": "Amber Duck",
              "bowler_id": "3778926",
              "runs": "30",
              "fours": "2",
              "sixes": "1",
              "balls": "21"
            },
            {
              "position": "2",
              "batsman_name": "Mars Leonard",
              "batsman_id": "3778630",
              "how_out": "ct",
              "fielder_name": "Smoke Duck",
              "fielder_id": "3778927",
              "bowler_name": "Whistle Duck",
              "bowler_id": "3778928",
              "runs": "50",
              "fours": "6",
              "sixes": "0",
              "balls": "68"
            }
          ],
          "fow": [
            {
              "runs": "40",
              "wickets": 1,
              "batsman_out_name": "Chew Leonard",
              "batsman_out_id": "3778631",
              "batsman_in_name": "Mars Leonard",
              "batsman_in_id": "3778630",
              "batsman_in_runs": "10"
            }
          ],
          "bowl": [
            {
              "bowler_name": "Amber Duck",
              "bowler_id": "3778926",
              "overs": "12",
              "maidens": "2",
              "runs": "45",
              "wides": "2",
              "wickets": "3",
              "no_balls": "1"
            }
          ]
        }
      ]
    }
  ]
}
```

---

## Response Fields

### Match-level fields

The match-level fields are the same as those returned by [Result Summary](./result-summary.md), with the following additions:

| Field | Type | Description |
|-------|------|-------------|
| `no_of_days` | string | Number of days (for multi-day matches) |
| `no_of_players` | string | Number of players per side |
| `no_of_reserves` | string | Number of reserve players listed |

### Points array fields (`points[]`)

Same as Result Summary, with these additional fields per team:

| Field | Type | Description |
|-------|------|-------------|
| `bonus_points_2nd_innings_together` | string | Combined bonus points for the second innings |
| `bonus_points_2nd_innings_batting` | string | Batting bonus points for the second innings |
| `bonus_points_2nd_innings_bowling` | string | Bowling bonus points for the second innings |

### Match result types (`match_result_types[]`)

A list of all possible result outcomes for this specific match. Each entry is a two-element array of `[description, code]`. This can be used to build a result-entry UI. The code format is either a plain integer or `"typeId#teamId"` for team-specific results (e.g. wins, concessions).

### Players array (`players[]`)

Contains two objects: `home_team` and `away_team`. Each is an array of player entries.

| Field | Type | Description |
|-------|------|-------------|
| `position` | integer | Batting position in the team sheet |
| `player_name` | string | Player's full name |
| `player_id` | integer | Unique player identifier. Same as `member_id` from the [Players endpoint](./players.md) |
| `captain` | boolean | Whether this player is the captain |
| `wicket_keeper` | boolean | Whether this player is the wicket-keeper |

### Innings array (`innings[]`)

One entry per innings. Each innings contains three sub-arrays.

#### Innings-level fields

| Field | Type | Description |
|-------|------|-------------|
| `team_batting_name` | string | Full name of the batting team |
| `team_batting_id` | string | ID of the batting team |
| `innings_number` | integer | Innings number (1 or 2) |
| `extra_byes` | string | Byes conceded |
| `extra_leg_byes` | string | Leg byes conceded |
| `extra_wides` | string | Wides bowled |
| `extra_no_balls` | string | No balls bowled |
| `extra_penalty_runs` | string | Penalty runs |
| `penalties_runs_awarded_in_other_innings` | string | Penalty runs that count in the opposing innings |
| `total_extras` | string | Total extras |
| `runs` | string | Total runs scored |
| `wickets` | string | Wickets fallen |
| `overs` | string | Overs faced |
| `declared` | boolean | Whether the innings was declared |
| `revised_target_runs` | string | Revised target (e.g. Duckworth-Lewis) |
| `revised_target_overs` | string | Revised overs target |
| `revised_target_balls` | string | Revised balls target |

#### Batting entries (`bat[]`)

One entry per batsman.

| Field | Type | Description |
|-------|------|-------------|
| `position` | string | Batting position |
| `batsman_name` | string | Batsman's name |
| `batsman_id` | string | Batsman's player ID |
| `how_out` | string | Dismissal code. See [Enum Values](../appendices/enum-values.md) |
| `fielder_name` | string | Name of the fielder involved in the dismissal (for catches, run outs, stumpings) |
| `fielder_id` | string | Fielder's player ID |
| `bowler_name` | string | Name of the bowler who took the wicket |
| `bowler_id` | string | Bowler's player ID |
| `runs` | string | Runs scored |
| `fours` | string | Number of fours hit |
| `sixes` | string | Number of sixes hit |
| `balls` | string | Balls faced |

#### Fall of wickets entries (`fow[]`)

| Field | Type | Description |
|-------|------|-------------|
| `runs` | string | Team score at which the wicket fell |
| `wickets` | integer | Wicket number (1st, 2nd, etc.) |
| `batsman_out_name` | string | Name of the batsman dismissed |
| `batsman_out_id` | string | ID of the batsman dismissed |
| `batsman_in_name` | string | Name of the incoming batsman |
| `batsman_in_id` | string | ID of the incoming batsman |
| `batsman_in_runs` | string | Runs scored by the incoming batsman at the time the wicket fell |

#### Bowling entries (`bowl[]`)

One entry per bowler.

| Field | Type | Description |
|-------|------|-------------|
| `bowler_name` | string | Bowler's name |
| `bowler_id` | string | Bowler's player ID |
| `overs` | string | Overs bowled |
| `maidens` | string | Maiden overs |
| `runs` | string | Runs conceded |
| `wides` | string | Wides bowled |
| `wickets` | string | Wickets taken |
| `no_balls` | string | No balls bowled |

---

## Notes

- This endpoint accepts a single `match_id`. To retrieve scorecards in bulk, you will need to make one call per match.
- Empty strings (`""`) indicate data that has not been recorded. For example, `fours` and `balls` may be blank if the scorer did not record them.
- The `how_out` field uses short codes (e.g. `"b"` for bowled, `"ct"` for caught, `"no"` for not out). See [Enum Values](../appendices/enum-values.md) for a full list.
- `player_id` in the scorecard corresponds to `member_id` in the [Players endpoint](./players.md), enabling cross-referencing.
- The response wraps everything in a `match_details` array, but this will always contain a single object for a given `match_id`.
