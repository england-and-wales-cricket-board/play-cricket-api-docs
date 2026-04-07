# List League Sites

Returns a list of all league (competition) sites registered on Play-Cricket, including their public-facing URLs.

**Endpoint**
```
GET https://play-cricket.com/api/v2/league_sites.json
```

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |

---

## Example Request

```
GET https://play-cricket.com/api/v2/league_sites.json?api_token=YOUR_TOKEN
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

- This endpoint returns all league sites nationally. There is no filter parameter.
- The `league_id` returned here is used as the `league_id` parameter when calling [List Divisions & Cups](./competitions.md).
- This is a useful starting point if you do not know the ID of a league you want to query.
