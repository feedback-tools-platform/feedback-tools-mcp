---
name: feedback-digest
description: Summarize customer feedback from a feedback.tools survey for a period. Use when the user asks for a feedback digest, a weekly or monthly review, "what are customers saying", how the score changed, or the top bugs, feature requests and emotions.
---

# Feedback digest

Build a short digest of one feedback.tools survey for one period, using the feedback.tools MCP tools.

## Steps

1. **Pick the survey.** Call `list_surveys`. If the user named a survey, match it by title. If there is more than one candidate, ask which one. Note the survey type (`csat_2`, `csat_5`, `ces_7`, `nps_10`, `general`).
2. **Pick the period.** Use the period the user gave. If none, use the last 7 days and say so. Also take the previous period of the same length for comparison. Pass dates in `filters` as `since` / `until` (ISO dates).
3. **Score and volume** (skip the score for `general` surveys, they have no scale):
   - `get_csat_score` for the current and the previous period.
   - `get_stats` for response counts, responses with a comment and response ratio.
   - `get_score_distribution` only if the score moved noticeably.
4. **Themes.** Call `list_bugs`, `list_feature_requests` and `list_emotions` for the current period. Take the top 3-5 of each by `finding_count`. For the 1-2 biggest bugs, call `get_theme` to see the weekly trend and a few responses behind it.
5. **Quotes.** Take 2-4 short, representative comments from `get_theme` or `get_responses` (`text_only: true`). Quote them as written, do not edit them.

## Output

Write the digest in the user's language, in this order:

- **Headline:** one sentence with the main change of the period.
- **Score:** current value, previous value, direction. For NPS give the number, for CSAT and CES the percentage.
- **Volume:** responses and responses with a comment.
- **Top bugs:** name, number of responses, trend (growing, stable, new).
- **Top feature requests:** name and number of responses.
- **Mood:** the leading emotions with counts.
- **Quotes:** 2-4 comments.
- **Worth a look:** 1-3 items that grew the most or appeared for the first time.

Keep it under one screen. Use only numbers returned by the tools; do not estimate or invent them. Responses marked `is_ignored: true` are already excluded from scores and themes; do not add them back.

If a call fails because the survey has no active subscription or trial, tell the user and give the survey link from the error.
