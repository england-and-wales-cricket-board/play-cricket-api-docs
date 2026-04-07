# Data Model & Core Concepts

Understanding how Play-Cricket structures its data will help you navigate the API effectively and choose the right endpoints for your use case.

---

## Entity Hierarchy

```
County Cricket Board (CCB)
  └── Club
        ├── Team (1st XI, 2nd XI, etc.)
        │     └── Player
        └── [participates in] League / Competition

League Site
  └── Season (e.g. "2024")
        └── Competition (Division or Cup)
              ├── [has] Teams (from Clubs)
              ├── [has] Matches
              │     ├── Result & Points
              │     ├── Innings
              │     │     ├── Batting
              │     │     ├── Bowling
              │     │     └── Fall of Wickets
              │     └── League Table
```

---

## Key Concepts

### Sites and site_id

A **site** in Play-Cricket corresponds to either a **club** or a **league (competition) administrator**. Each site has a unique numeric `site_id`.

- Club sites manage their own teams, players, and friendly fixtures
- League sites manage competitions, divisions, cups, fixtures, and results across all participating clubs

The `site_id` appears in the URL of your Play-Cricket site's public-facing pages.

### Clubs and club_id

A **club** is a cricket club registered on Play-Cricket. Clubs have a stable `id` (also returned as `club_id` in some endpoints) that does not change between seasons.

### Teams and team_id

A **team** belongs to a club (e.g. "Chingford CC — 2nd XI"). A club may have multiple teams. The `team_id` is stable across seasons.

### Leagues and league_id

A **league** is the administrative body running one or more competitions (e.g. "Warwickshire County Cricket League"). The `league_id` is stable across seasons and corresponds to a league site's `site_id`.

### Competitions, Divisions, and Cups

Within a league and season, there are one or more **competitions**. A competition is either a **division** (league table format) or a **cup** (knockout format). Each competition has a unique `competition_id` (also referred to as `division_id` in some endpoints).

> **Important:** The `division_id` / `competition_id` is unique per season. The same division in a different year will have a different ID. When building season archives, store the ID alongside the season year.

### Matches and match_id

A **match** (also called a fixture) has a unique `match_id` that is stable once created. Matches go through states: unpublished → published → result entered → result locked.

### Players and member_id

Players are identified by a `member_id` (also returned as `player_id` in match scorecards). This ID is stable across seasons and clubs.

---

## Choosing the Right Match Endpoint

There are three match-related endpoints with different levels of detail:

| Endpoint | What it returns | Best used for |
|----------|-----------------|---------------|
| `GET /matches.json` | Fixture list — dates, teams, ground, officials. No result data. | Building a fixture list at the start of a season; polling for fixture changes |
| `GET /result_summary.json` | Everything in match summary, plus result, points, and innings totals (runs, wickets, overs, extras). No ball-by-ball data. | Results widgets, league result feeds, polling for new results |
| `GET /match_detail.json` | Full scorecard — team sheets, batting, bowling, fall of wickets. | Full scorecard display pages |

The recommended workflow is:
1. Use **Match Summary** to build and maintain your fixture list
2. Use **Result Summary** to pick up results as they come in (poll using `from_entry_date`)
3. Use **Match Detail** on demand when a user requests a full scorecard view
