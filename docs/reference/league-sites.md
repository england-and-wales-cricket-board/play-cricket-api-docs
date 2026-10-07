# List League Sites

Returns the league (competition) sites you've been granted access to, including their public-facing URLs.

**Endpoint**
```
GET https://www.play-cricket.com/api/v3/league_sites.json
```

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |

---

## Example Request

```
GET https://www.play-cricket.com/api/v3/league_sites.json?api_token=YOUR_TOKEN
```

---

## Example Response

```json
{
  "leagues": [
    {
      "league_id": 296,
      "name": "Derbyshire County Cricket League",
      "subsite_url": "https://derbycl.play-cricket.com"
    },
    {
      "league_id": 534,
      "name": "Warwickshire County Cricket League",
      "subsite_url": "https://warcl.play-cricket.com"
    }
  ]
}
```

---

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `league_id` | integer | Unique identifier for the league site. Use as `league_id` in the [Competitions endpoint](./competitions.md) |
| `name` | string | Name of the league |
| `subsite_url` | string | The public-facing URL of the league's Play-Cricket site |

---

## Notes

- Only league sites you've been granted access to are returned. There is no filter parameter.
- The `league_id` returned here is used as the `league_id` parameter when calling [List Divisions & Cups](./competitions.md).
- Use this endpoint to look up the `league_id` of a league you have access to.
- If you have any queries about your access, or wish to request wider access, contact our support team.
