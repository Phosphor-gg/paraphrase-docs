# Paraphrase documentation

Markdown sources for paraphrase.bot/docs. The website clones this repo at build
time, traverses `docs/`, renders every page, and generates the sidebar.

## Writing rules

**No em dashes or en dashes. Ever.** Not `—`, not `–`. Use a comma, a colon,
parentheses, or two sentences. Check before committing:

```bash
grep -rn '—\|–' docs/
```

- British spelling, sentence case for headings.
- Second person, imperative for instructions ("Click a word", not "You can
  click a word").
- Short sentences. Docs are scanned, not read.

## Accuracy

Docs describe what the editor does, so a wrong line here becomes a support
email.

- **Every behaviour, limit and price is checked against the source before
  writing**: `paraphrase-website` (the editor), `paraphrase-backend` (limits,
  credits), `paraphrase-types/src/pricing.rs` (plan limits) and the live Stripe
  products. Read it, do not recall it.
- The plan limits are also enforced by a website test that reads these pages:
  the credits page must say "3 AI cleanups a day", "30 AI cleanups a day",
  "projects of up to 5 minutes" and "projects of up to 4 hours" in those exact
  words while those are the limits in `paraphrase-types`.
- If a value could not be verified, leave it out rather than guess.
- When behaviour changes in code, the docs change in the same session.

## Format

- `docs/NN-category/NN-page.md`; the numeric prefixes order the sidebar.
- `_category.json` in each directory gives the sidebar heading:
  `{"title": "Using Paraphrase"}`.
- Frontmatter: `title` (required), `description` (required, used for meta
  tags and the index card), `nav` (sidebar label), `slug` (the URL under
  `/docs/`; keep existing slugs stable, they are linked from the site and the
  blog).
- Body starts with `# Title`, then one sentence saying what the page covers.
