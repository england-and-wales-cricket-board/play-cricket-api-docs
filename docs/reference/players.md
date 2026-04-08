# List Players for a Club

Returns a list of players (members) associated with a specific club site.

**Endpoint**
```
GET https://www.play-cricket.com/api/v2/sites/{site_id}/players
```

Replace `{site_id}` with the numeric ID of the club's Play-Cricket site.

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |
| `include_everyone` | string | No | Pass `yes` to include all members with any active role at the club, not just those with an active squad role |
| `include_historic` | string | No | Pass `yes` to also include members who have a historic (past) squad role at the club |

---

## Example Requests

**Active squad members only (default):**
```
GET https://www.play-cricket.com/api/v2/sites/3540/players?api_token=YOUR_TOKEN
```

**All members with any active role:**
```
GET https://www.play-cricket.com/api/v2/sites/3540/players?api_token=YOUR_TOKEN&include_everyone=yes
```

**Include members with historic squad roles:**
```
GET https://www.play-cricket.com/api/v2/sites/3540/players?api_token=YOUR_TOKEN&include_historic=yes
```

---

## Example Response

```json
{
  "players": [
    {
      "member_id": 3778631,
      "name": "Chew Leonard"
    },
    {
      "member_id": 3778630,
      "name": "Mars Leonard"
    }
  ]
}
```

---

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `member_id` | integer | Unique identifier for this player across the Play-Cricket platform. Also returned as `player_id` and `batsman_id` / `bowler_id` in scorecard endpoints |
| `name` | string | Player's full name |

---

## Behaviour by Parameter Combination

| Parameters | Records returned |
|------------|-----------------|
| Neither optional param | Members with an **active squad role** at the club |
| `include_everyone=yes` | Members with **any active role** at the club (includes non-playing roles such as officials) |
| `include_historic=yes` | Members with an active squad role **plus** those with a historic (past) squad role |
| Both optional params | Members with any active role **plus** those with any historic squad role |

---

## Notes

- `member_id` is the same as `player_id` returned within match scorecard responses ([Match Detail](./match-detail.md)), allowing you to cross-reference players between endpoints.
- Player records do not contain squad or team assignment information. To see which players are in a team for a specific match, use [Match Detail](./match-detail.md).
