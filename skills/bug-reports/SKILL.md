---
name: bug-reports
description: Turn bug themes from feedback.tools into ready-to-paste bug report drafts. Use when the user asks to triage bugs from customer feedback, prepare issues or tickets from feedback, or find out which reported bugs to fix first.
---

# Bug reports from feedback

Turn the bug themes of a feedback.tools survey into bug report drafts the user can paste into their issue tracker. This skill only writes text; it does not create issues anywhere.

## Steps

1. **Pick the survey** with `list_surveys`. Ask if it is unclear which one.
2. **Pick the period.** Use the user's period, or the last 30 days by default, and say which one you used. Pass it in `filters` as `since` / `until`.
3. **List bugs** with `list_bugs` for the period. Rank by `finding_count`.
4. **For each bug the user wants** (by default the top 5), call `get_theme` with its `id`:
   - read the weekly `trend` to see if it is new, growing or fading;
   - read the responses behind it; open 1-2 of them with `get_response` if you need details such as the page URL, metadata or attachments.
5. **Check for duplicates.** If two themes describe the same problem, merge them into one report and say so.

## Report format

One block per bug, in the user's language unless they ask otherwise:

```
Title: <what goes wrong, from the user's side, one line>

Reported by: <N> responses in <period> (<trend>)
Where: <page, feature or flow, if the responses say it>
What users report:
- "<quote>"
- "<quote>"
Steps to reproduce: <only if responses describe them; otherwise "not described in feedback">
Expected: <what users expected, if stated>
Source: feedback.tools theme <id>
```

After the blocks, add a short priority list: order the bugs by number of affected responses and by trend, and explain the order in one line each.

Use only what the responses say. Do not invent steps, environments or causes. If the feedback does not contain enough detail to reproduce a bug, say that and suggest asking affected users (responses that left contact details have `user_email`).
