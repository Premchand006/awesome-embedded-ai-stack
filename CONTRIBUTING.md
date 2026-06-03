# Contributing to awesome-embedded-ai-stack

Thanks for helping build a genuinely useful, vendor-neutral hub for Physical AI / Edge AI. This guide explains **what we accept**, **the quality bar**, and **how to submit**.

## What this repo is (and isn't)

- ✅ A curated **awesome list** + **learning roadmap** + **ecosystem map** + **reproducible starter projects**.
- ✅ Opinionated, current, and beginner-friendly.
- ❌ Not a benchmark suite, not a heavy engineering monorepo, not a dumping ground for every link.

## Great first contributions

- 🔗 **Fix a broken or outdated link** (CI flags these automatically — see open `broken-link` issues).
- 🧰 **Add a beginner quick-win project** using the [project template](#quick-win-template).
- 🔌 **Add or correct a hardware page** (specs, price, official docs/GitHub).
- 🆕 **Flag a rename/deprecation** (e.g., a SDK that changed names).
- ✍️ **Improve an explanation** so a newcomer understands it faster.

## Quality bar for resources

A link earns a place only if it clears **all** of these:

1. **Authoritative or high-signal** — official docs/repos, maintainers, recognized practitioners, or peer-reviewed work. No SEO spam, no content farms.
2. **Currently maintained** — for repos, a commit within ~12 months (or clearly "stable/complete"). Stale links get pruned.
3. **Specific** — links to the exact page/repo, not a homepage you have to dig through.
4. **Adds something** — don't add a 4th tutorial that says the same thing as three we already list.
5. **Described** — one short clause on *why* it's worth a click.

Format (Awesome style, enforced by `awesome-lint`):

```markdown
- [Name](https://example.com) — Short description of why it's useful.
```

Use `-` for list markers, sentence-case descriptions, a hyphen (`-`) before the description, and **no trailing slash** on URLs.

## <a name="quick-win-template"></a>Quick-win project template

Every file in `beginner-projects/` should include:

- **What you'll build** (one sentence) and a screenshot/GIF if possible.
- **Required hardware** — exact board, camera, accelerator, cables (with rough cost).
- **Difficulty** — Easy / Medium / Hard, and **estimated time**.
- **Setup complexity** — what has to be installed/flashed.
- **Steps** — numbered, linking to *official* tutorials rather than re-hosting code where possible.
- **Learning outcome** — what the reader understands afterward.
- **Troubleshooting** — the 2–3 things that actually go wrong.

Add a row to the table in `beginner-projects/README.md` when you add a project.

## How to submit

1. **Fork** and create a branch: `git checkout -b add/<short-name>`.
2. Make your change. Keep PRs focused (one project or one topic).
3. Run the checks locally (optional but appreciated):
   ```bash
   npx awesome-lint
   # link check (Rust binary "lychee" — see https://github.com/lycheeverse/lychee)
   lychee --offline . || lychee .
   ```
4. Use a [Conventional Commits](https://www.conventionalcommits.org/) message, e.g.
   `docs: add Pi 5 + AI HAT+ 2 GenAI quick-win`.
5. Open a PR. CI runs `awesome-lint` and the link checker; fix anything red.

## Style

- Prefer **prose + tables** over walls of bullets.
- Keep claims **sourced** (link the vendor/spec page).
- TOPS, prices, and versions change — add the **date** you verified a figure when it matters.
- Be vendor-neutral. Note trade-offs, not just strengths.

## Code of Conduct

By participating you agree to the [Code of Conduct](CODE_OF_CONDUCT.md).

## License of contributions

Contributions are accepted under the repo's dual license: **MIT** for code/snippets and **CC BY 4.0** for prose/tables. By submitting a PR you agree to license your contribution under these terms.
