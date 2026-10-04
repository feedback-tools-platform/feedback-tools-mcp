<p align="center">
  <img src="assets/logo.png" alt="feedback.tools" width="96" height="96">
</p>

<h1 align="center">feedback.tools MCP server</h1>

<p align="center">
  Customer feedback for your AI assistant: CSAT, NPS and CES scores, response search,
  AI themes with bugs and feature requests. Create surveys and import feedback.
</p>

<p align="center">
  <a href="https://feedback.tools/docs/mcp">Documentation</a> ·
  <a href="https://feedback.tools">feedback.tools</a> ·
  <a href="https://registry.modelcontextprotocol.io/v0.1/servers/tools.feedback%2Fmcp/versions/latest">MCP Registry</a>
</p>

---

[feedback.tools](https://feedback.tools) collects customer feedback with CSAT, NPS, CES and
open-text surveys that run as a widget on your website or app. AI reads every response and
groups it into themes: bugs, feature requests and emotions.

The MCP server lets an AI assistant work with that data from a chat. Ask "What are the top
bugs this month?" or "How did our NPS change since August?", and the assistant picks the
tools it needs.

This repository holds the connection config and the Claude Code plugin with skills. The server itself is
hosted by feedback.tools.

| | |
|---|---|
| Server URL | `https://feedback.tools/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth 2.0. You sign in to feedback.tools in the browser and click Allow |
| Registry name | `tools.feedback/mcp` |

## Requirements

A feedback.tools account with at least one survey. Responses, themes and scores are
available for surveys on a free trial or with a subscription.

## Connect

### Claude

1. Open **Customize → Connectors** and click **Add custom connector**.
2. Name: `feedback.tools`. URL: `https://feedback.tools/mcp`. Leave OAuth Client ID and
   Client Secret empty.
3. Click **Connect**, sign in to feedback.tools and click **Allow**.

### Claude Code

Install the plugin from this repository:

```
/plugin marketplace add feedback-tools-platform/feedback-tools-mcp
/plugin install feedback-tools@feedback-tools
```

Or add the server directly:

```
claude mcp add --transport http feedback-tools https://feedback.tools/mcp
```

Then run `/mcp`, pick `feedback-tools` and sign in.

### ChatGPT, Codex and other clients

Any client that supports remote MCP servers with OAuth can connect to
`https://feedback.tools/mcp`. Step-by-step guides:
[feedback.tools/docs/mcp](https://feedback.tools/docs/mcp).

## Tools

### Read

| Tool | What it does |
|---|---|
| `ping` | Checks the connection and shows the name of the connected app |
| `list_surveys` | Lists your surveys with their subscription status |
| `get_survey` | Shows one survey: settings, status and response counts |
| `get_responses` | Lists responses, newest first, with filters by score, date, country and comment |
| `get_response` | Shows one response with the bugs, feature requests and emotions found in it |
| `search_responses` | Full-text search over response text |
| `list_themes` | Lists AI themes with the number of responses behind each one |
| `list_bugs` | Lists bug themes |
| `list_feature_requests` | Lists feature-request themes |
| `list_emotions` | Lists emotion themes |
| `get_theme` | Shows one theme with its weekly trend and the responses behind it |
| `get_csat_score` | Returns the CSAT, NPS or CES score for a period |
| `get_score_distribution` | Breaks responses down by score |
| `get_stats` | Returns response count, average score and response ratio |

### Write

| Tool | What it does |
|---|---|
| `create_survey` | Creates a survey from a type, a title and a question |
| `update_survey` | Changes survey settings: texts, languages, pages, trigger, country rules, response limit |
| `create_response` | Imports feedback from email, chats or support tickets as a response |
| `set_response_ignored` | Keeps a response but leaves it out of scores and themes, or brings it back |
| `delete_response` | Deletes one response permanently. The assistant asks you to confirm |

The assistant cannot delete a survey or your account.

## Skills (Claude Code plugin)

The plugin adds three skills on top of the tools. Claude picks them up when your request matches.

| Skill | What it does |
|---|---|
| `feedback-digest` | Summary of a survey for a period: score and its change, top bugs, feature requests, emotions and quotes |
| `bug-reports` | Turns bug themes into bug report drafts to paste into your issue tracker, with counts, trend and quotes |
| `create-survey` | Helps choose the survey type and question, then creates and sets up the survey |

## Revoke access

In feedback.tools open **Settings → MCP connection → Connected apps** and click
**Disconnect** next to the app.

## Support

[support@feedback.tools](mailto:support@feedback.tools) ·
[Privacy policy](https://feedback.tools/privacy-policy)

## License

The configuration files in this repository are released under the [MIT License](LICENSE).
The feedback.tools service is subject to its own terms.
