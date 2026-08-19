# Project Memory — Pitfalls & Lessons Learned

Append-only log. Add an entry whenever a mistake repeats or a gotcha is discovered.
Never delete or rewrite existing entries.

## Entries

- 2026-08-19 — Default Expo `.gitignore` only ignores `.env*.local`, NOT plain `.env`. When introducing env vars, add an explicit `.env` entry before creating the file or credentials will show up as untracked and risk being committed.
