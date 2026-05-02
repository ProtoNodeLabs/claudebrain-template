# Gotchas

Things that burned you. Claude reads this to avoid repeating mistakes.

---

## [Category]

- **[Gotcha title]:** [What happened and how to avoid it next time]

---

## Example entries

- **Vercel doesn't auto-promote main to Production** — many projects are configured to build `main` as Preview only. After merging, check whether the Production deployment updated.
- **GitHub App "Configure >" doesn't trigger OAuth** — if the app is already installed on an org, clicking Configure goes to settings, not a new OAuth callback. Uninstall and reinstall to get a fresh callback.
- **CSS Grid items overflow despite row constraints** — `min-height: auto` is the default. Any grid item that should scroll or shrink needs `min-height: 0` explicitly set.

---
_Add at the top. Never remove — even fixed bugs are useful history._
