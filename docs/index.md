---
hide:
  - navigation
  - toc
---

# Play-Cricket API Documentation

The Play-Cricket API provides read-only access to cricket data held within the Play-Cricket platform — fixtures, results, scorecards, league tables, clubs, teams, and players.

!!! warning "Who this API is for"
    Play-Cricket's API is intended for clubs and competitions to retrieve their own data from the platform for processing elsewhere. It is not available as a service for those looking to build products or applications using cricket data. For more info, [read here](https://play-cricket.ecb.co.uk/hc/en-us/articles/24640412683037-Play-Cricket-API-Access-for-commercial-non-profit-projects).

All endpoints use **HTTP GET** requests and return **JSON**. The API is at version `v2`.

**Base URL**
```
https://www.play-cricket.com/api/v2/
```

!!! info "Access required"
    All requests require an API token. See [Authentication](authentication.md) for details on obtaining one.

---

## Getting Started

<div class="grid cards" markdown>

-   :material-key-outline: **Authentication**

    ---

    How to obtain and use your API token.

    [:octicons-arrow-right-24: Authentication](authentication.md)

-   :material-sitemap: **Data Model**

    ---

    How clubs, teams, competitions, and matches relate to each other.

    [:octicons-arrow-right-24: Data Model](data-model.md)

-   :material-calendar-clock: **Common Patterns**

    ---

    Date filtering, polling for changes, and avoiding large result sets.

    [:octicons-arrow-right-24: Common Patterns](common-patterns.md)

-   :material-alert-circle-outline: **Error Handling**

    ---

    HTTP status codes, common mistakes, and rate limiting.

    [:octicons-arrow-right-24: Error Handling](error-handling.md)

</div>

---

## API Reference

### Organisation

| Endpoint | Description |
|----------|-------------|
| [`GET /CCBs.json`](reference/county-cricket-boards.md) | List all County Cricket Boards |
| [`GET /clubs.json`](reference/clubs.md) | List clubs, filtered by county or date |
| [`GET /league_sites.json`](reference/league-sites.md) | List all league sites and their URLs |

### Teams & Players

| Endpoint | Description |
|----------|-------------|
| [`GET /sites/{site_id}/teams.json`](reference/teams.md) | List teams for a club or CCB site |
| [`GET /sites/{site_id}/players`](reference/players.md) | List players for a club |
| [`GET /competition_teams.json`](reference/teams-in-division.md) | List teams in a specific division or cup |

### Competitions

| Endpoint | Description |
|----------|-------------|
| [`GET /competitions.json`](reference/competitions.md) | List divisions and cups for a league season |

### Matches

| Endpoint | Description |
|----------|-------------|
| [`GET /matches.json`](reference/match-summary.md) | Fixture list — dates, teams, ground, officials. No result data |
| [`GET /result_summary.json`](reference/result-summary.md) | Completed matches with result, points, and innings totals |
| [`GET /match_detail.json`](reference/match-detail.md) | Full scorecard — batting, bowling, fall of wickets |

### Standings

| Endpoint | Description |
|----------|-------------|
| [`GET /league_table.json`](reference/league-table.md) | Current league table for a division |

---

## Appendices

| | |
|--|--|
| [Enum Values](appendices/enum-values.md) | All known values for status, result, dismissal codes, and more |
| [Date Formats](appendices/date-formats.md) | Date and timestamp formats across all endpoints |
| [ID Lifecycle](appendices/id-lifecycle.md) | Which IDs are stable vs season-specific |
| [Changelog](appendices/changelog.md) | History of API changes |
