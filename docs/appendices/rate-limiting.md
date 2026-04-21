# Rate Limiting

The Play-Cricket API applies rate limits to protect service reliability and ensure fair access for all consumers. This page explains how limits work, what to expect when you exceed them, and how to design your integration to stay well within them.

---

## The API is not real-time

The Play-Cricket API is a data access layer over a managed cricket administration platform — it is **not a real-time feed**. Match data, scorecards, and results are entered and published by club and league administrators. Responses may also be served from cache at our end to protect API latency under load.

This has two practical consequences:

- **Polling at high frequency returns the same data.** If you call an endpoint every few seconds expecting live score updates, you will receive identical responses almost every time. The data simply does not change at that rate.
- **There is no valid reason to exceed our rate limits.** If your integration is being limited, it is retrieving the same cached data it already has. The correct response is to poll less frequently, not to retry faster.

---

## Consider the right data access pattern for your product

There is no single correct way to use this API. The best approach depends on your product — and a thoughtful mix of local caching and dynamic retrieval will often serve both your users and our infrastructure better than either extreme alone.

### Caching and local data stores

Much of the data served by this API changes infrequently. For these data types, the most efficient pattern is to **fetch once, store locally, and refresh on a schedule** — serving your users from your own data store rather than making a live API call on every request:

| Data type | How often it changes | Suggested refresh |
|-----------|----------------------|-------------------|
| Clubs, CCBs, league sites | Rarely — once per season at most | At season start, or weekly at most |
| Teams, players | Occasionally — new registrations, transfers | Daily or on-demand |
| Competitions, divisions | Once per season | At season start |
| Fixtures | Weekly — as new fixtures are scheduled or changed | Daily during the season |

Consumers who cache this structural data locally and refresh it at appropriate intervals will never come close to the rate limits — and will also benefit from faster response times for their users.

### Dynamic retrieval

For data that changes more often — such as results, scorecards, or league tables — many consumers choose to retrieve it dynamically on page load rather than maintaining a local store. This is a perfectly reasonable pattern, and our limits accommodate it well for the kind of traffic a cricket club website would typically see.

It is also worth considering that dynamic retrieval can actually reduce total API traffic compared to scheduled polling: if nobody visits your results page overnight, no requests are made. A polling approach would have made them regardless.

!!! info "Operating at larger scale? Use the Play-Cricket web application."
    If your site regularly serves thousands of concurrent users, this API is not the right tool for dynamic data retrieval. The [Play-Cricket web application](https://play-cricket.com) is purpose-built to serve cricket data at volume — we would encourage you to direct your users there rather than building a high-traffic custom integration on top of this API.

---

## Per-endpoint limits

Rate limits are applied **per endpoint**. Each endpoint has its own independent limit, set according to the typical volume and frequency of legitimate use for that data type. Endpoints covering more frequently updated data (such as results) have more generous limits than those covering near-static data (such as clubs or CCBs).

The specific numeric limits are not published, but they are set at levels that no well-designed integration should reach.

---

## Burst allowance

Each endpoint includes a **burst allowance** — a short-term tolerance for higher request rates above the sustained limit. This is intended to accommodate developers who are actively building and exploring a new integration, where running the same request repeatedly to inspect responses is a normal part of the process.

If you are in active development and hit a limit, wait a short period and your access will be restored automatically. You do not need to contact us.

---

## 429 Too Many Requests

When a rate limit is exceeded, the API returns:

```
HTTP 429 Too Many Requests
```

If you receive a 429 response:

1. **Stop retrying immediately.** Retrying in a tight loop will not help and will extend the time before your access is restored.
2. **Back off and wait.** Pause for at least 60 seconds before retrying.
3. **Review your integration.** A 429 is a signal that your polling frequency is higher than necessary. Consider whether you need a local cache, a longer polling interval, or narrower query parameters.

See [Error Handling](../error-handling.md) for a full list of HTTP status codes and general error handling guidance.

---

## Designing within the limits

The following patterns keep integrations well within rate limits:

- **Cache locally.** Store retrieved data in your own database and serve it from there. Refresh on a schedule rather than on demand.
- **Use filters.** Narrow requests with `season`, `division_id`, `team_id`, or date ranges rather than retrieving full datasets and filtering client-side.
- **Use `from_entry_date` for incremental updates.** Rather than re-fetching a full season of results, poll for only records updated since your last check.
- **Use v3 paginated endpoints.** Paginated responses are smaller and faster, reducing both your latency and load on our infrastructure.
- **Poll on match days, not every day.** Results only change when matches are played and entered. There is no need to poll the Result Summary endpoint on days when no matches are scheduled.
