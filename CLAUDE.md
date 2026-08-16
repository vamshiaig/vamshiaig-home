# vamshiaig.com

One-page corporate site + product tabs for VAMSHIAIG LLP. Pure static HTML, no build step —
`index.html` is the whole site. Full context: [README.md](README.md).

Deployed on Vercel at `vamshiaig.com` / `www.vamshiaig.com`. Sibling deployed product:
`shopfront` (Storefront, at `store.vamshiaig.com`), linked from the Products tabs here.

## Working practices (repeated here because they keep slipping)

- **Fix the class, not the instance.** A reported bug is one case of a pattern — grep for
  sibling occurrences before patching, fix all confirmed ones in one pass.
- **Verify before claiming done.** A green build/deploy proves no regression, not that a
  never-observed behavior is correct — load the actual changed page/state before saying it
  works, and say plainly which states were checked vs not.
- **State known gotchas up front**, especially silent failure modes (Vercel domain ownership,
  gh account context — see below).
- **No overengineering, no under-scoping.** Minimal = smallest change that fixes the whole
  confirmed problem, not the narrowest patch that silences one report.
- **Epistemic honesty.** Say what was observed vs inferred; don't assert from absence of
  evidence.

## Git / GitHub

Remote is `github.com/vamshiaig/vamshiaig-home` (migrated from `vamshi-vadala/vamshiaig-site`
2026-08-16 — old repo is orphaned, no longer deployed). The `gh` CLI on this machine has two
logged-in accounts, `vamshiaig` and `vamshi-vadala` — only one is "active" at a time, and it's
global to `gh`, not per-repo. Any `gh` command scoped to `vamshi-vadala` silently flips the
active account; the next push/fetch against this (`vamshiaig`-owned) repo then fails or 404s
in a way that looks like data loss — it isn't, it's an auth-context mixup.

**Before pushing or fetching:** `gh api user --jq '.login'` must print `vamshiaig`; if not,
`gh auth switch --user vamshiaig` first.

`git push`/`fetch` from a plain POSIX/bash shell fails outright here (no tty for the
credential prompt). Use a native PowerShell/cmd shell instead — `gh auth git-credential` is
wired as the credential helper for `github.com` there.

## Editing

Everything is in `index.html` — copy, styles, and metadata. Light/dark both styled via
`prefers-color-scheme`; keep text on `--panel`/`--bg` (not on tinted accent surfaces) so
contrast stays AA. Adding a product: new `<button role="tab">` + matching `<div role="tabpanel">`
— the tab-switcher JS at the bottom activates itself once there are 2+ tabs.

## Deploy gotcha (incident, 2026-08-16)

Vercel only lets one project own a given domain. While repointing this project's domain during
the repo migration, the apex `vamshiaig.com` briefly attached to the **shopfront** Vercel
project instead, so this homepage vanished and vamshiaig.com served Shopfront directly — no
error, no warning. If a domain move is ever needed again: verify with
`curl -sI https://vamshiaig.com | grep -i x-sf-build` — presence of that header means Shopfront
has the domain, not this site.
