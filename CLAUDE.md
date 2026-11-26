# Paddleout — Surf the Change (paddleout.life)

Static website hosted on Netlify. Every merge to `main` deploys automatically.
The main editor is Masa (Masayuki Ohno), who writes in Japanese or English and is
not a developer. Reply in the language he writes in, keep explanations short and
non-technical, and show him what changed in plain words.

## Where things live

- `content.json` — **all site content** (articles, videos, Q&A, drill, seminar,
  meetup, profile, books, global/impact, Connect promo, settings). Most requests
  are edits to this file only.
- `index.html` — layout, styles and code. Change only when the request is about
  design, layout or behavior.
- `img/` photos, `files/` PDFs, `books/*.json` booklet text (read in the on-page reader).

## content.json conventions

- `publish`: `"YES"` = shown, `"NO"` = hidden (draft). Never delete content just to hide it.
- English versions use the same field name plus `_en` (e.g. `title_en`, `body_en`).
  They show when a visitor presses the English button. **When you add or change
  Japanese text, also write or update the matching `_en` field** (natural, warm,
  clear English; translate Bible book names, e.g. マタイの福音書 7章 → Matthew 7),
  unless Masa says not to. Some sections use `_ja` for the Japanese version instead.
- `articles`: `kind` is `daily` or `weekly`. **Newest goes at the end of the list.**
  The latest two of each kind show on the page; older ones go to the archive.
  If every article has a `date` (e.g. `2026-11-16`) they sort by date instead.
  `label` can stay empty (it becomes DAY 3 / VOL. 2 automatically).
  Paragraphs in `body` are separated by a blank line (`\n\n`); the first paragraph
  is the lead shown on the page. `question` is an optional question to readers.
- `videos`: paste a YouTube URL in `youtube_url`. Newest at the end.
- `qa`: **newest at the top.** In `answer`, a paragraph starting with `> ` is a Bible
  quote (next line `— Book chapter`), a paragraph starting with `## ` is a subheading.
- `drill_info`: the first published entry is "this month's drill".
- `seminar_events`: the first published entry shows on the seminar ticket.
  A non-empty `button` shows a registration button.
- Multi-line list fields use one item per line, with `|` between parts:
  `milestones` = `heading|text`, `timeline` = `year|heading|text`,
  `program` = `number|title|text`, `points` = `EN heading|heading|text`.
- `**text**` in some titles/quotes marks highlighted words.
- Keep the JSON valid. After editing, check it parses:
  `python3 -m json.tool content.json > /dev/null`

## Images and files

- New photos go in `img/`, PDFs in `files/`. Keep photos under ~400 KB and no wider
  than 1600 px; resize/compress before committing if needed.
- Reference them by relative path, e.g. `"photo": "img/new-photo.jpg"`.

## Forms (Netlify Forms)

Forms send to Netlify, which emails each submission to the address set in the
Netlify dashboard. `storeRow()` in `index.html` posts them. The hidden `<form>`
elements right after `<body>` list every form name and field so Netlify can detect
them: **if you add or rename a field, update both places**.

| storeRow collection | Netlify form name | Used by |
|---|---|---|
| `questions` | `anonymous-question` | "Ask us" anonymous question form |
| `talks` | `speaking-request` | "Request a talk" and seminar registration (`kind: join`) |
| `contacts` | `contact` | contact form (currently not linked; "Contact us" shows the email address) |

## Rules

- Work on a branch and open a pull request; Netlify posts a preview link on the PR.
  Masa checks the preview and merges. Don't push straight to `main`.
- This site no longer runs inside Claude: don't add `window.claude` / `claude.use`
  code or Claude artifact links. Site links: https://paddleout.life,
  Connect: https://joinconnect.jp.
- Content is faith-based (Biblical wisdom for business people) and welcoming to
  everyone, whatever they believe. Keep that tone in anything you draft.
