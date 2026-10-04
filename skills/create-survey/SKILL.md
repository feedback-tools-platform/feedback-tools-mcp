---
name: create-survey
description: Create and set up a feedback.tools survey. Use when the user wants to start collecting feedback, add a CSAT, NPS, CES or open-text survey to their site or app, or change where and when an existing survey shows.
---

# Create a survey

Help the user pick the right survey, then create and configure it with `create_survey` and `update_survey`.

## 1. Choose the type

Ask what the user wants to learn, then suggest one type:

| Goal | Type | Scale |
|---|---|---|
| Was a specific step good (checkout, onboarding, support reply) | `csat_5` | 1-5, stars, emoji or numbers |
| Quick yes/no reaction | `csat_2` | thumbs or emoji |
| How hard was it to get something done | `ces_7` | 1-7 numbers |
| Would they recommend the product overall | `nps_10` | 0-10 numbers |
| Open feedback, no score | `general` | none |

The type cannot be changed after creation.

## 2. Write the question

- One question, about one thing, max 127 characters.
- Name the moment: "How easy was it to complete your order?" works better than "How do you like our site?".
- For NPS keep the standard wording: "How likely are you to recommend <product> to a friend or colleague?"
- Set `min_label` and `max_label` for `csat_5`, `ces_7` and `nps_10` (for example "Not likely" / "Very likely").
- Suggest a follow-up `text_question` such as "What is the main reason for your score?". Comments are what AI themes are built from.

Show the user the type, question, labels and follow-up before creating.

## 3. Create

Call `create_survey` with `survey_type`, `title` (internal name for the dashboard) and `question`, plus the labels and follow-up. Everything else gets dashboard defaults.

The result contains `notice_for_user` with the trial end date and the survey link: pass it on to the user. Do not call `create_survey` twice for the same request; check `list_surveys` first if unsure whether it was created.

## 4. Targeting (optional)

Ask where and when the survey should appear, then call `update_survey` with:

- `show_on_pages` to limit it to certain URLs (for example only the order confirmation page);
- `trigger` to show it immediately, after a delay or after scrolling;
- `allowed_countries` / `disallowed_countries` for country rules;
- `translations` for other languages;
- `responses_limit` to cap the number of responses.

## 5. Install

The widget is installed on the site or in the app with the survey's `api_key` from the result. Point the user to the survey link from `notice_for_user`: the dashboard shows the install snippet.
