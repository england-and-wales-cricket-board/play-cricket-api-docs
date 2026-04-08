# Authentication

## API Token

Every request to the Play-Cricket API must include an `api_token` parameter. Requests without a valid token will be rejected.

```
GET https://www.play-cricket.com/api/v2/clubs.json?api_token=YOUR_TOKEN
```

---

## Obtaining a Token

API tokens are generated from within the Play-Cricket administration area of your club or league site.

1. Read the details [here](https://play-cricket.ecb.co.uk/hc/en-us/articles/115004270145-Do-You-Have-an-API-to-Access-Play-Cricket-Data)
2. Request your token from our help desk team
3. Sign and return the API access agreement
4. Receive your token

Treat your API token like a password — do not expose it in client-side JavaScript or commit it to public source code repositories.

---

## Token Scope

Your token is tied to your Play-Cricket site. The type of site determines what data is accessible:

| Site type | Access |
|-----------|--------|
| **Club site** | Data for teams and players associated with your club; fixtures and results for matches your club participates in |
| **League (Competition) site** | Data across all clubs, teams, and matches in the leagues you administer |

Some endpoints require a `site_id` parameter. This is the numeric identifier for your Play-Cricket site, visible in the URL of your site's admin area.

---

## Passing the Token

The token is always passed as a query string parameter:

```
?api_token=YOUR_TOKEN
```

It can be combined with other parameters in any order:

```
GET https://www.play-cricket.com/api/v2/matches.json?site_id=3540&season=2024&api_token=YOUR_TOKEN
```
