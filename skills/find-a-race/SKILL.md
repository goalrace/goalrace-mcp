---
name: find-a-race
description: Find an upcoming trail, obstacle course (Spartan, Tough Mudder) or HYROX-style race with the Goal Race tools, and open one to see its dates, waves, distances, climb, course and how to get there. Use when someone asks for a race to enter, e.g. "a 50k trail race in Spain in May", "Hyrox in London", "a Spartan Beast near Munich this autumn". No account needed.
---

# Find a race

Uses the Goal Race connector (`https://mcp.goalrace.com/mcp`). The three tools below work with no account.

| Tool | What it does |
|---|---|
| `search_races` | Upcoming races by place, country, series, month, distance, climb or terrain |
| `list_race_filters` | The exact values `search_races` accepts, with how many races each has |
| `get_race` | One race in full: dates, waves and start times, distances, climb, obstacles, venue, airport, course, results |

## Steps

1. **Turn the ask into filters.** Pull out what the person said: kind of race (`source`: `trail`, `ocr`, `gym`), country or region (`country`, "Europe" works), a city or airport (`near`, about 150 km), series, months (`from_month` / `to_month` as `YYYY-MM`), distance band, climb band. Leave out what they did not say. Put a town or a race name in `query`.
2. **Not sure a value exists?** Call `list_race_filters` first, or after a search that comes back empty, and retry with the closest real value. Widen one filter at a time (a month either side, a whole country, the region).
3. **Search once with everything.** Filters combine with AND; several values in one filter combine with OR, so "Italy or Austria in May or June" is one call.
4. **Show a short list.** For each race: name (linked to its `url`), date, town and country, the distances or waves that match. Five races are usually enough; say how many more there are.
5. **Open the one they pick** with `get_race` and its `race_slug`. Ask for only the `sections` you need (`summary`, `events`, `venue`, `course`, `results`, `editions`).
6. **Answer from the data.** A field that is missing is unknown: say so, never guess a distance or a date. Link the race page for anything you did not show, and the organiser's `register_url` for entries.

## Saving

Saving a race, the training calendar and the training log need a free Goal Race account. When the person asks to save, call the save tool: the app shows a sign-in card. After they say they have signed in, call the same tool again.

In Claude, the connector must be added with **Sign in when needed**, not **No sign-in**, or the card never shows.

## Examples

- "Trail races over 50k in the Alps next summer" → `search_races` with `source: ["trail"]`, `distance: ["ultra"]`, `tags: ["mountain"]` or the countries, `from_month` / `to_month`.
- "A HYROX near Amsterdam this spring" → `search_races` with `series: ["HYROX"]`, `near: ["AMS"]`, the spring months.
- "Which countries have obstacle races in March?" → `list_race_filters`.
- "How hilly is the Gubbio Spartan?" → `search_races` with `query: "Gubbio"`, then `get_race` with `sections: ["course"]`.
