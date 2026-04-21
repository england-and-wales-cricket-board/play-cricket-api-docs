# League Table

Returns the current league table for a specified division. This endpoint triggers a live calculation of the table on each request before returning the result.

**Endpoint**
```
GET https://www.play-cricket.com/api/v3/league_table.json
```

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |
| `division_id` | integer | Yes | The ID of the division. Obtain from [List Divisions & Cups](./competitions.md). Note this ID is unique per division per season — no separate `season` parameter is needed |

---

## Example Request

```
GET https://www.play-cricket.com/api/v3/league_table.json?division_id=110530&api_token=YOUR_TOKEN
```

---

## Example Response

```json
{
  "league_table": [
    {
      "id": 110530,
      "name": "Premier Division",
      "headings": {
        "column_1": "Team",
        "column_2": "p",
        "column_3": "w24",
        "column_4": "w20",
        "column_5": "wd",
        "column_6": "ld",
        "column_7": "t",
        "column_8": "l",
        "column_9": "a",
        "column_10": "BatP",
        "column_11": "BowlP",
        "column_12": "Pen",
        "column_13": "Pts"
      },
      "values": [
        {
          "position": "1",
          "team_id": "9073",
          "column_1": "Rugby CC",
          "column_2": "22",
          "column_3": "3",
          "column_4": "13",
          "column_5": "1",
          "column_6": "0",
          "column_7": "0",
          "column_8": "3",
          "column_9": "2",
          "column_10": "19",
          "column_11": "28",
          "column_12": "0",
          "column_13": "385"
        },
        {
          "position": "2",
          "team_id": "11558",
          "column_1": "Bedworth CC",
          "column_2": "22",
          "column_3": "2",
          "column_4": "13",
          "column_5": "3",
          "column_6": "0",
          "column_7": "0",
          "column_8": "1",
          "column_9": "3",
          "column_10": "16",
          "column_11": "15",
          "column_12": "0",
          "column_13": "373"
        }
      ],
      "key": "p - Played, w24 - Win 24pts (24), w20 - Win 20pts (20), wd - Winning draw, ld - Losing Draw, t - Tied (10), l - Loss, a - Abandoned (4), BatP - Batting Bonus Points, BowlP - Bowling Bonus Points, Pen - Penalty Points, Pts - Points"
    }
  ]
}
```

---

## Response Fields

### Table-level fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | The division ID |
| `name` | string | The division name |
| `headings` | object | A set of key-value pairs mapping column keys (`column_1`, `column_2`, etc.) to their display labels |
| `values` | array | One entry per team, in position order |
| `key` | string | A comma-separated string explaining each column code. Suitable for display as a table key or legend |

### Headings object

The `headings` object maps each column to a short label code (e.g. `"p"` for Played, `"Pts"` for Points). The exact columns present depend on how the competition has been configured. `column_1` is always the team name.

### Values array entries

Each entry represents one team's row in the table.

| Field | Type | Description |
|-------|------|-------------|
| `position` | string | The team's current position in the table |
| `team_id` | string | The team's unique identifier |
| `column_1` | string | Team name |
| `column_2` ... `column_n` | string | Values for each column, corresponding to the labels in `headings` |

### Key string

The `key` field provides human-readable descriptions of each column code as a single string. For example:

```
"p - Played, w24 - Win 24pts (24), w20 - Win 20pts (20), ..."
```

Parse this string or display it directly below the table as a legend.

---

## Understanding the Dynamic Column Structure

Play-Cricket competitions can be configured with different scoring systems and result types (e.g. different point values for wins, two types of draw, bonus points). As a result, the number and meaning of columns varies between competitions.

The API only returns columns that have at least one non-null value across all teams. However, **columns where all values are zero are included** — a column containing all zeros is different from one that has no data.

The mapping of `headings` to `values` is always consistent within a single response: `column_1` in `headings` corresponds to `column_1` in every row of `values`. Use the headings to build your table dynamically rather than hardcoding column positions.

---

## Notes

- Because `division_id` is unique per season, you do not need to specify a `season` parameter. The season is implied by the division ID. This also means historical tables for past seasons can be retrieved by using the division ID from that season.
- This endpoint triggers a live table recalculation on every call. Avoid polling it unnecessarily — cache the result for a reasonable period (e.g. one hour) where possible.
- The `division_id` changes each season. Retrieve the current season's IDs from [List Divisions & Cups](./competitions.md).
