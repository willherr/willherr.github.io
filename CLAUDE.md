# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working in this repository.

This file stays intentionally short — it's loaded into every session regardless of what's being worked on. It covers only durable invariants: what a future change must not break, and why. This convention is copied from `willherr/Cassandras10Key`'s own `CLAUDE.md`, the mature reference for this workflow — see that repo for the lived-in version of the same structure.

## Project overview

Will's personal/professional site, served via GitHub Pages at `will-i-am.dev` (`CNAME`). Plain vanilla HTML/CSS, no framework, no build step — `.nojekyll` disables GitHub Pages' default Jekyll processing so files are served as-is. Root files: `index.html` (landing page with the site nav), `about-william-herrmann.html` (framed as an `iframe` inside `index.html`'s content area), `css/`, `content/` (favicons, headshot). `apps/` holds standalone HTML pages for 10-Key (`10-key.html` plus its privacy-policy/terms-of-service pages).

**Currently a hobby/legacy page, not yet the front-company hub it's slated to become** — see the open backlog below. Known real drift as of 2026-09-10, not yet cleaned up:
- `index.html`'s nav links to `/CassandrasCookbook` and `/WillsTools` as if Blazor WASM builds of those apps still get published into this repo — Cassandra's Cookbook has since been rewritten in Flutter, in its own repo, with its own eventual subdomain (`cookbook.will-i-am.dev`, see `willherr/CassandrasCookbook`'s own `CLAUDE.md`), not this domain.
- `apps/10-key.*.html` (the 10-Key marketing/privacy-policy/terms-of-service pages) are superseded — 10-Key's real marketing site moved off this shared root domain to its own `10-key.will-i-am.dev` Cloudflare Worker deploy in `Cassandras10Key`#156. These files are likely safe to remove once confirmed nothing still links to them.
- `README.md`'s site map is stale for the same reasons (references the old Blazor Cassandra's Cookbook and Will's Tools as if still hosted here).

**Backlog** (GitHub Issues, not this file):
- **#13** — redesign this site as a real front-company hub for all of Will's apps (10-Key, Cassandra's Cookbook, future ones), optimized to drive install/purchase revenue rather than just describe Will. Brainstorming-stage — scope beyond an app showcase (blog? resume? distinct company branding?) undecided; flagged as worth a dedicated scoping session before implementation. Will already has ChatGPT-generated branding explorations (a keycap-style logo/favicon concept) at `C:\Users\wch\OneDrive\Pictures\will-i-am-dev\ideas`.
- **#14** — localize the site to whatever language set 10-Key's own marketing-site localization (`Cassandras10Key`#253) settles on. Sequenced after #13.
- **#15** — SEO/Google Search optimization for the hub, mirroring `Cassandras10Key`#256. Sequenced after #13, coordinate with #14 (shared page-head concerns).

This file will need a real pass once #13 actually lands — don't write detailed Architecture for a structure that's about to be replaced.

## Dev workflow

- Default branch is `main` (renamed from `master` 2026-09-10 via GitHub's branch-rename API, matching every other repo of Will's except 10-Key which is already `main`). GitHub Pages' publish source was bound to `master` by name — the rename API repointed it to `main` automatically (verified live, `will-i-am.dev` served correctly immediately after), so this needed no manual Pages reconfiguration, but any *future* branch rename in a repo with GitHub Pages enabled should still verify the live site afterward rather than assuming it carried over.
- Feature/content work branches off `main` (pull latest first), gets a real PR even solo — never committed straight to `main`.
- Branch naming: `issue#<N>/PascalTitle` (literal `#`, issue number, `/`, then a Pascal-case short title). Quote branch names containing `#` in shell commands.
- Backlog/direction lives in GitHub Issues, not an internal markdown doc.
- **Exception: non-application changes — CLAUDE.md updates chief among them — can be committed straight to `main`, no branch/PR needed** (same carve-out every other repo of Will's uses).
- **Issue labels**: `brainstorming`/`needs decision`/`priority: high/medium/low` — the cross-repo convention, see `~/.claude/notes/issue-labels.md` for the full scheme. No release-grouping labels (`release-mvp` etc.) here — those are specific to CassandrasCookbook's pre-launch product, not applicable to this site.
- No PR gets created, and no PR gets merged, without Will's explicit confirmation first — same global rule as every other repo (`~/.claude/CLAUDE.md`).

## Commands

No build step — this is plain static HTML/CSS served directly by GitHub Pages. Nothing to `npm install`, compile, or run locally beyond opening the HTML files in a browser (or a trivial local static server if you need real relative-path/asset behavior). No CI exists yet for the same reason — there's no build/test/lint command to gate on; add a real workflow once #13 gives this site actual structure worth checking (e.g. a link-checker, an HTML validator, or a real build step if it stops being framework-free).

## Notes

- Audit this file for drift whenever a backlog issue closes, same as every other Will repo.
