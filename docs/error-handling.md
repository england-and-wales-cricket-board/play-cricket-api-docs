# Error Handling & Limits

---

## HTTP Status Codes

The Play-Cricket API uses standard HTTP status codes to indicate success or failure.

| Status code | Meaning |
|-------------|---------|
| `200 OK` | Request succeeded. The response body contains the requested data. |
| `400 Bad Request` | A required parameter is missing or a parameter value is invalid. |
| `401 Unauthorized` | The `api_token` is missing, invalid, or does not have access to the requested resource. |
| `403 Forbidden` | Your token does not have access to this endpoint, or to the organisation you requested. |
| `404 Not Found` | The requested resource (e.g. a specific `match_id`) does not exist. |
| `429 Too Many Requests` | You have exceeded the rate limit for this endpoint. See [Rate Limiting](appendices/rate-limiting.md). |
| `500 Internal Server Error` | An unexpected error occurred on the server. |

---

## Empty Result Sets

If your request is valid but no records match your filters, the API returns an HTTP `200` with an empty array — not an error. For example:

```json
{
  "matches": []
}
```

This is normal behaviour when, for example, no fixtures have been updated within the date range you specified.

---

## Common Mistakes

| Problem | Likely cause |
|---------|-------------|
| Empty response when records are expected | Missing or incorrect `season` parameter; date range too narrow; `site_id` pointing to wrong site |
| Fewer results than expected | `include_unpublished` not set — unpublished matches are excluded by default |
| `division_id` returns no results | Division IDs change each season — ensure you are using the ID for the current season (retrieve via `GET /competitions.json`) |
| A club, CCB, or league site is missing from the response | Your token has not been granted access to it — contact our support team |
| `403` for a site you expect to reach | Your token has not been granted access to that site — contact our support team |
| Very slow response | Large unfiltered result set — add `season`, `division_id`, or date range filters |

---

## Rate Limiting

Requests are rate limited per endpoint. If you exceed a limit, the API returns `429 Too Many Requests`. Stop retrying, wait at least 60 seconds, then try again.

See [Rate Limiting](appendices/rate-limiting.md) for how the limits work and how to design your integration to stay within them.
