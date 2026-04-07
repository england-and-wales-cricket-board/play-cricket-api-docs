# Enum Values Reference

This page collects all known enumerated values across the Play-Cricket API in one place.

---

## `status`

Returned on all list endpoints (clubs, teams, matches, etc.).

| Value | Meaning |
|-------|---------|
| `"New"` | Record is active |
| `"Deleted"` | Record has been removed. Remove from your local data store |

---

## `published`

Returned on match endpoints.

| Value | Meaning |
|-------|---------|
| `"Yes"` | Fixture is publicly visible on Play-Cricket |
| `"No"` | Fixture exists in the system but is not yet public |

---

## `competition_type`

Used as a filter parameter and returned in match responses.

| Value | Meaning |
|-------|---------|
| `"League"` | A divisional league fixture |
| `"Cup"` | A cup competition fixture |
| `"Friendly"` | A friendly match (club sites only) |

---

## `match_type`

Returned on match endpoints. Describes the format of the match.

| Value | Meaning |
|-------|---------|
| `"Limited Overs"` | One-day limited overs match |
| `"Declaration"` | Match where teams may declare their innings |
| `"Twenty20"` | T20 format |
| `"Knock Out"` | Cup knockout match |

> This list may not be exhaustive. Values are determined by competition configuration.

---

## `game_type`

Returned on match endpoints.

| Value | Meaning |
|-------|---------|
| `"Standard"` | Standard match format |

> Additional values may exist. Values are determined by competition configuration.

---

## `result`

Returned on result endpoints. A short code indicating the match outcome.

| Value | Meaning |
|-------|---------|
| `"W"` | Win |
| `"L"` | Loss |
| `"T"` | Tied |
| `"D"` | Draw |
| `"A"` | Abandoned |
| `"C"` | Cancelled |
| `"P"` | Match in progress |
| `"Con"` | Conceded |

> `result_applied_to` indicates which team the result applies to (typically the winning team).

---

## `how_out` (Batting dismissal codes)

Returned in the `bat[]` array within [Match Detail](../reference/match-detail.md).

| Code | Meaning |
|------|---------|
| `"b"` | Bowled |
| `"ct"` | Caught |
| `"ct&b"` | Caught and bowled |
| `"lbw"` | Leg before wicket |
| `"ro"` | Run out |
| `"st"` | Stumped |
| `"hw"` | Hit wicket |
| `"ob"` | Obstructing the field |
| `"hb"` | Hit the ball twice |
| `"tt"` | Timed out |
| `"ret"` | Retired |
| `"no"` | Not out |
| `"dnb"` | Did not bat |
| `"sub"` | Absent / sub |

---

## `captain` / `wicket_keeper`

Returned in the `players[]` array within [Match Detail](../reference/match-detail.md).

| Value | Meaning |
|-------|---------|
| `true` | Player has this role in the match |
| `false` | Player does not have this role |

---

## `declared`

Returned in innings arrays.

| Value | Meaning |
|-------|---------|
| `true` | The innings was declared closed |
| `false` | The innings was not declared (all out, overs completed, or in progress) |

---

## `competition_type` (Competitions endpoint parameter)

Used as the `competition_type` parameter on [List Divisions & Cups](../reference/competitions.md).

| Value | Meaning |
|-------|---------|
| `"divisions"` | Return league divisions |
| `"cups"` | Return cup competitions |

---

## `include_unpublished` (Match Summary parameter)

| Value | Meaning |
|-------|---------|
| `"yes"` | Include unpublished fixtures in results |
| *(omit)* | Exclude unpublished fixtures (default) |

---

## `countdown_cricket`

Returned in [Result Summary](../reference/result-summary.md).

| Value | Meaning |
|-------|---------|
| `"yes"` | Match uses countdown cricket format |
| `"no"` | Match uses standard format |
