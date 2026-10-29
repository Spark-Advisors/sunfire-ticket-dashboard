# SunFire Ticket Status — Themed Dashboard

A single-page, static dashboard that reads a SunFire support export (CSV), groups
tickets into themes, and shows status, severity, team, created date, and a link to
each JIRA ticket. No server or build step — it's one `index.html`.

## Files
- `index.html` — the dashboard (HTML + CSS + JS, no external dependencies)
- `tickets.csv` — **sample data only (fully fictional)**. Replace with the real
  export when hosting privately, or load the real file in-browser (see below).

## How it works
- **Choose CSV…** reads a CSV **in your browser**. The data is parsed and rendered
  client-side and is **never uploaded or stored** anywhere.
- **Load tickets.csv** fetches the `tickets.csv` file committed next to the page.
- **Refresh** re-reads whatever is currently loaded and updates the "loaded" time.
- **Redact PII** (on by default) scrubs detectable identifiers on render — NPNs,
  agent IDs, personal/enrollment codes, and enrollment-ID tokens, plus a few common
  name patterns.

## Daily workflow
Either:
1. Open the page and use **Choose CSV…** to load that day's export (recommended —
   the sensitive data stays in your browser), **or**
2. Commit/replace `tickets.csv` next to `index.html` and click **Load tickets.csv**.

## ⚠️ PII / HIPAA note
The SunFire export contains agent names, NPNs, and enrollment/personal codes.

- The **redaction toggle is best-effort** for detectable identifiers. It does **not**
  guarantee removal of arbitrary free-text names.
- Do **not** commit a real `tickets.csv` to any public location. For a public host,
  either keep the file-upload workflow (data stays local) or pre-de-identify the
  `Summary` column before upload.
- The committed sample data here is fictional.

## Expected CSV columns
`Summary`, `Key`, `Status`, `Client Sev Level`, `SunFire Sev Level`, `Team`, `Created`
(header matching is case-insensitive; extra columns are ignored).
