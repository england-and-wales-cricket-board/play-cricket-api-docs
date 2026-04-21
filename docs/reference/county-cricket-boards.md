# List County Cricket Boards

Returns a list of all County Cricket Boards (CCBs) registered on Play-Cricket.

**Endpoint**
```
GET https://www.play-cricket.com/api/v3/CCBs.json
```

---

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `api_token` | string | Yes | Your API authentication token |

---

## Example Request

```
GET https://www.play-cricket.com/api/v3/CCBs.json?api_token=YOUR_TOKEN
```

---

## Example Response

```json
{
  "CCBs": [
    {
      "id": 1,
      "name": "Warwickshire Cricket Board",
      "county_id": 37,
      "status": "New"
    },
    {
      "id": 2,
      "name": "Derbyshire Cricket Board",
      "county_id": 10,
      "status": "New"
    }
  ]
}
```

---

## Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Unique identifier for the CCB |
| `name` | string | Name of the County Cricket Board |
| `county_id` | integer | Identifier for the associated county |
| `status` | string | `New` (active) or `Deleted` (removed) — see [Common Patterns](../common-patterns.md) |

---

## Notes

- This endpoint returns all CCBs nationally. There is no filter parameter.
- Use the `id` returned here as the `county_id` filter on the [List Clubs](./clubs.md) endpoint to retrieve clubs for a specific board.
