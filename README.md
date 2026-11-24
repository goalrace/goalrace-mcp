<p align="center"><img src="icon.png" width="96" height="96" alt="Goal Race"></p>

# Goal Race MCP

**Search races with no account. Sign in to save.**

Goal Race connects your AI assistant to a calendar of upcoming trail and ultra races, obstacle course races (Spartan, Tough Mudder, Runmageddon and more) and HYROX-style hybrid fitness races. Ask in plain words, "a 50k trail race in Spain in May" or "a HYROX near Amsterdam this spring", and get dates, waves, distances, climb, the course and how to get there. With a free Goal Race account you can also save races to your list, put a training plan on your calendar and log each session, by typing or by voice.

```
https://mcp.goalrace.com/mcp
```

A hosted remote MCP server (Streamable HTTP). Nothing to install, no token to copy. This repo holds the plugin files, one skill and the registry entry. The server itself is not open source.

## Add it

### Claude (web, desktop, mobile)

1. Settings → Connectors → **Add custom connector**.
2. Name `Goal Race`, URL `https://mcp.goalrace.com/mcp`.
3. For sign-in, choose **Sign in when needed**. Claude may pick *No sign-in* for you: change it, or Claude cannot ask you to sign in when you save a race.
4. Ask for races right away. When you save one, Claude shows a sign-in card. Sign in, click Allow, then tell Claude you have signed in.

Walkthrough with screenshots: https://www.goalrace.com/mcp

### Claude Code

```
/plugin marketplace add goalrace/goalrace-mcp
/plugin install goal-race@goalrace
```

This adds the server and the `find-a-race` skill. Run `/mcp` and pick `goal-race` to sign in when you want to save.

### ChatGPT

Settings → Apps → Advanced settings → turn on Developer mode → **Create app**. Name `Goal Race`, URL `https://mcp.goalrace.com/mcp`, authentication OAuth. ChatGPT asks you to sign in when you connect.

### Cursor

[Add to Cursor](https://cursor.com/install-mcp?name=goal-race&config=eyJ1cmwiOiJodHRwczovL21jcC5nb2FscmFjZS5jb20vbWNwIn0=), or put this in `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "goal-race": { "url": "https://mcp.goalrace.com/mcp" } } }
```

### VS Code

```
code --add-mcp '{"name":"goal-race","type":"http","url":"https://mcp.goalrace.com/mcp"}'
```

### Gemini CLI

```
gemini extensions install https://github.com/goalrace/goalrace-mcp
```

## Tools

**No account needed**

| Tool | What it does |
|---|---|
| `search_races` | Upcoming races by place, country, series, month, distance, climb or terrain |
| `list_race_filters` | The countries, series, distance and climb bands, tags and months search accepts, with counts |
| `get_race` | One race in full: dates, waves and start times, distances, climb, obstacles, venue, nearest airport, course, past results |

**Free account** (asked only when one of these is used)

| Area | Tools |
|---|---|
| Your race list | `save_race`, `add_custom_race`, `remove_race`, `get_trip`, `save_trip_plan` |
| Calendar and training | `get_calendar`, `get_training_log`, `get_session`, `add_sessions`, `update_session`, `log_session`, `remove_sessions`, `add_training_plan` |
| Training blocks | `get_blocks`, `add_block`, `update_block`, `remove_block` |
| Diary | `add_note`, `update_note`, `delete_note`, `get_notes` |
| Profile | `get_profile`, `update_profile` |

## Skill

[`skills/find-a-race`](skills/find-a-race/SKILL.md) turns a request like "trail races over 50k in the Alps next summer" into the right search, and opens the race you pick.

## Links

- Setup guide: https://www.goalrace.com/mcp
- Docs: https://www.goalrace.com/docs
- Privacy: https://www.goalrace.com/privacy
- Official MCP registry: `com.goalrace/goal-race`
- Support: support@goalrace.com

## Licence

MIT, for the files in this repo. See [LICENSE](LICENSE).
