# ID Lifecycle

Different types of IDs in the Play-Cricket API have different lifetimes. Understanding which IDs are stable and which change between seasons is important for building reliable integrations.

---

## Stable IDs (do not change between seasons)

These IDs can be stored permanently and used across seasons.

| ID | Endpoint | Notes |
|----|----------|-------|
| `club_id` / `id` (clubs) | [Clubs](../reference/clubs.md) | A club's ID never changes |
| `site_id` | [Teams](../reference/teams.md), [Players](../reference/players.md), etc. | The numeric site ID for a club or league site |
| `team_id` | [Teams](../reference/teams.md), match endpoints | A team (e.g. "1st XI") retains its ID across seasons |
| `member_id` / `player_id` | [Players](../reference/players.md), [Match Detail](../reference/match-detail.md) | A player's ID is permanent across clubs and seasons |
| `league_id` | [League Sites](../reference/league-sites.md) | A league's site ID is stable |
| `ground_id` | Match endpoints | Ground IDs do not change |

---

## Season-specific IDs (change every season)

These IDs are assigned fresh each season. Do not store them as permanent references — retrieve them at the start of each season.

| ID | Endpoint | Notes |
|----|----------|-------|
| `competition_id` / `division_id` / `cup_id` | [Competitions](../reference/competitions.md), match endpoints | A new ID is assigned to each division and cup at the start of every season. The same division in 2024 and 2025 will have different IDs |

**Why do division IDs change?**

Each season's division is treated as a distinct record, allowing Play-Cricket to maintain a full historical archive of tables and fixtures. The ID effectively encodes a specific division in a specific season.

---

## Match IDs

| ID | Stable? | Notes |
|----|---------|-------|
| `match_id` | Yes, once created | Match IDs are stable once a fixture is created. They do not change if the fixture is rescheduled or its result updated |

---

## Practical Guidance

### At the start of each season

1. Call [List Competitions](../reference/competitions.md) to retrieve the new `division_id` and `cup_id` values for the current season
2. Update any stored references to competition IDs
3. Call [Match Summary](../reference/match-summary.md) with the new season value to build your fixture list

### During the season

- Use `team_id`, `club_id`, and `player_id` freely — these are stable
- Use `division_id` from the current season's competition list
- Store `match_id` values for ongoing reference to specific fixtures

### For historical lookups

- If you stored `division_id` values from past seasons alongside the year, you can retrieve historical league tables and fixtures using those IDs
- League table history is available for any season whose `division_id` you have retained
