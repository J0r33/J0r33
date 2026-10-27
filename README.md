# Joree Weatherly

**Technical Product & Solutions** | Architecting and shipping a live booking & payments platform with AI agents | Claude Code · TypeScript · Supabase · Payments

I take a business that runs on spreadsheets and a no-code app, work out what it actually needs, and ship
and run the system that does it. Most of my work is in private client repos, so the contribution graph
shows the volume and this page explains it.

[joreeweatherly.com](https://joreeweatherly.com) · [LinkedIn](https://www.linkedin.com/in/joreeweatherly)

---

## Case study: O2Oasis booking, membership and payments platform

**Problem.** O2Oasis, a gym, ran member booking, memberships and payments on an app built in a
no-code tool. The business had outgrown it: there was no staging environment, no review step before
changes went live, and no way to test against real data safely. Members were already booking and
paying through the app, so it couldn't go down while we replaced it.

**My role.** Sole technical owner, covering requirements with the owner, architecture, build,
migration, release management and day-to-day support. I write the tickets, run the AI agents that do much
of the implementation, review their work, and decide what ships.

**Stack.** React + TypeScript (Vite), Supabase (Postgres with row-level security, edge functions),
Square for payments, Resend for email, Vercel for hosting, GitHub Actions for CI, Linear for tickets.

**Key decisions**

- **Moved the app into a codebase we own.** It now runs on its own Supabase project and Vercel
  deployment, every schema change ships as a reviewed migration, and the code runs locally against a
  local database.
- **Migrated members without a forced password reset.** Existing accounts moved over with their
  credentials intact, so no one had to reset a password.
- **Releases go out in waves.** Each wave moves from feature branches to dev, then to staging for
  QA, then to production. Nothing reaches production without a human merging it by hand.
- **CI checks fail closed.** I found several checks that reported success while checking nothing,
  and fixed them. Every gate now has to be shown failing on a deliberately broken change before I trust
  it. The gates cover type checks, secret scanning (gitleaks), dependency audits and a PR quality gate.
- **Kept member data out of logs and analytics.** Personal and payment data never goes to error
  trackers, logs or ad platforms. Ad conversions are reported without customer details.
- **Split the platform when the business split.** When the company separated into two legal
  entities, I divided one shared app and database into separate systems for each business.

**Results**

- 500+ pull requests across the platform repos, each tied to its own ticket
- Members moved to the new platform with no service interruption
- Platform separated cleanly across two legal entities

**Read more:** [booking-platform-case-study](https://github.com/J0r33/booking-platform-case-study) has the
architecture and ten excerpts from the production code: webhook verification, idempotent payments,
row-level security, and checks that fail closed.

---

## How I work with AI agents

I use Claude Code as a team of specialist agents, not as autocomplete. Every ticket goes through five
steps:

1. **Check the claims.** Before planning, an agent verifies what the ticket says against the
   actual code and database.
2. **Design, challenge, build.** It drafts one to three approaches, an adversarial review attacks the
   chosen one, then it builds in small commits.
3. **Prove it in the running app.** Tests aren't enough. The change has to work in a real browser
   against a local copy of the stack.
4. **Ask what it might break.** It traces every code path the change touches and produces a
   checklist, and each item gets tested.
5. **Review, open the PR, stop.** Reviewer agents check the work, including one whose job is to
   disagree. Then the PR opens and the work stops: I review and merge it myself.

The workflow files (agents, commands, checklists and CI gate templates) are in
[agentic-workflow](https://github.com/J0r33/agentic-workflow), with credit for the workflow I adapted.

---

## Other work

- [bellabeat_case_study](https://github.com/J0r33/bellabeat_case_study): fitness tracker data analysis
  in R and SQL, with marketing recommendations.
