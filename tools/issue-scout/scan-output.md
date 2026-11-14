I have all the evidence. Let me compile the final graded report.

---

## Scan Results

**Queries run:**
1. `python-validation` — 100 results
2. `typescript-component` — 100 results

**Combined after dedup:** 200 unique issues
**After ranking filters** (drop assignees, drop > 45 days old, drop ≥ 4 comments): 118 survivors
**Top 5 graded** (sorted by fewest comments, then most recently updated)

---

### Candidate 1 — Sklearn-genetic-opt #396
Surfaced by: `python-validation` | Signals: 0 comments, updated 2026-11-14

- **maintainer-alive** → pass: Rodrigo Arenas committed 2026-11-14, < 60 days
- **repo-active** → pass: last commit 2026-11-14, < 80 days
- **not-claimed** → **fail**: open PR #402 by tridev-tej is cross-linked in the timeline, confirmed `state: open`
- **scope-fit** → pass (moot): docs-only, 2 files explicitly named, no task checklist
- **ai-policy-allowed** → pass (moot): AGENTS.md present, AI-assisted contributions explicitly welcomed
- **beginner-friendly** → pass: labeled "good first issue"

**REJECT** — not-claimed fails (open PR already exists)

---

### Candidate 2 — contextflow #47
Surfaced by: `typescript-component` | Signals: 0 comments, updated 2026-11-13

- **maintainer-alive** → pass: Paul Rayner committed 2026-11-14, < 60 days
- **repo-active** → pass: last commit 2026-11-14, < 80 days
- **not-claimed** → pass: no assignee; cross-ref is backlink to parent issue #45, not a PR; no claim comments
- **scope-fit** → **fail**: issue is an umbrella with four separate dialog items in a task checklist; body explicitly says "One PR per dialog is fine" confirming the items are independent sub-tasks
- **ai-policy-allowed** → pass (moot): CONTRIBUTING.md says "AI-forward project, agent-in-the-loop is also recommended"
- **beginner-friendly** → pass: labeled "good first issue"

**REJECT** — scope-fit fails (umbrella issue, 4 sub-tasks)

---

### Candidate 3 — shot-gobbler #70
Surfaced by: `typescript-component` | Signals: 0 comments, updated 2026-11-13

- **maintainer-alive** → **fail**: last human commit 2026-05-05, > 60 days ago; no maintainer comment in thread or on any open issue
- **repo-active** → **fail**: last commit 2026-05-05, > 80 days before 2026-11-13 (cutoff: 2026-08-25)
- (remaining checks skipped)

**REJECT** — repo-active + maintainer-alive both fail (repo appears dormant since May 2026; issues were bulk-opened 2026-11-13 but code is 6 months stale)

---

### Candidate 4 — Veritag #108
Surfaced by: `typescript-component` | Signals: 0 comments, updated 2026-11-13

- **maintainer-alive** → pass: pendulum-max committed 2026-11-09, < 60 days
- **repo-active** → pass: last commit 2026-11-09, < 80 days
- **not-claimed** → pass: no assignee, no linked PRs, no claim comments
- **scope-fit** → **fail**: issue body explicitly lists 4 files to touch (`TableSkeleton.tsx`, `MetricCardSkeleton.tsx`, `web/app/brand/page.tsx`, `web/app/owner/page.tsx`) — exceeds the 3-file threshold; also carries a 5-item task checklist
- **ai-policy-allowed** → pass (moot): CONTRIBUTING.md silent on AI, silence passes
- **beginner-friendly** → pass: labeled "good first issue"

**REJECT** — scope-fit fails (4 files explicitly stated, exceeds 3-file cap)

---

### Candidate 5 — firstbyte-resource-hub #37 ✓ ACCEPTED
Surfaced by: `typescript-component` | Signals: 0 comments, updated 2026-11-12

- **maintainer-alive** → pass: Hector Batista committed 2026-11-12, < 60 days
- **repo-active** → pass: last commit 2026-11-12, < 80 days
- **not-claimed** → pass: no assignee, no linked PRs, no claim comments in thread
- **scope-fit** → pass: deliverable is 1 new file (`src/components/workshop-card.tsx`); checklist items are acceptance criteria for the single component, not separate sub-tasks; no umbrella structure
- **ai-policy-allowed** → pass: CONTRIBUTING.md says "That goes for code from Claude too: you're the author of every line you commit" — a responsibility/disclosure norm, not a ban
- **beginner-friendly** → pass: labeled "good first issue" and "frontend"

**ACCEPT** — all required checks pass. Fit reasons: React/TypeScript component work, Next.js stack, single-file deliverable, shadcn/Tailwind, well-specified acceptance criteria, fresh repo with active maintainer.

---

```json
[
  {
    "item": "https://github.com/teach-firstbyte/firstbyte-resource-hub/issues/37",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Hector Batista committed 2026-11-12 on default branch, < 60 days before 2026-11-13"},
      {"name": "repo-active", "grade": "pass", "evidence": "Last default-branch commit 2026-11-12, < 80 days"},
      {"name": "not-claimed", "grade": "pass", "evidence": "No assignee, no linked PRs in timeline, no claim comments in thread"},
      {"name": "scope-fit", "grade": "pass", "evidence": "Single deliverable: src/components/workshop-card.tsx; checklist is acceptance criteria for one component, not umbrella sub-tasks"},
      {"name": "ai-policy-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md: 'That goes for code from Claude too: you're the author of every line you commit' — responsibility norm, not a ban"},
      {"name": "beginner-friendly", "grade": "pass", "evidence": "Labeled 'good first issue' and 'frontend'"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/rodrigo-arenas/Sklearn-genetic-opt/issues/396",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Rodrigo Arenas committed 2026-11-14, < 60 days"},
      {"name": "repo-active", "grade": "pass", "evidence": "Last commit 2026-11-14, < 80 days"},
      {"name": "not-claimed", "grade": "fail", "evidence": "Open PR #402 by tridev-tej is cross-linked in the issue timeline with state: open"},
      {"name": "scope-fit", "grade": "pass", "evidence": "Docs-only, 2 files named in body, no task checklist"},
      {"name": "ai-policy-allowed", "grade": "pass", "evidence": "AGENTS.md present; CONTRIBUTING.md explicitly guides AI-assisted contributions"},
      {"name": "beginner-friendly", "grade": "pass", "evidence": "Labeled 'good first issue' and 'help wanted'"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/virtualgenius/contextflow/issues/47",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Paul Rayner committed 2026-11-14, < 60 days"},
      {"name": "repo-active", "grade": "pass", "evidence": "Last commit 2026-11-14, < 80 days"},
      {"name": "not-claimed", "grade": "pass", "evidence": "No assignee; cross-reference is backlink to parent issue #45, not a PR"},
      {"name": "scope-fit", "grade": "fail", "evidence": "4-item task checklist (ProjectCreateDialog, ProjectDeleteDialog, GroupCreateDialog, ImportConflictDialog); body says 'One PR per dialog is fine' confirming umbrella structure"},
      {"name": "ai-policy-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md: 'AI-forward project; agent-in-the-loop is also recommended'"},
      {"name": "beginner-friendly", "grade": "pass", "evidence": "Labeled 'good first issue'"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/jsvirtane/shot-gobbler/issues/70",
    "checks": [
      {"name": "maintainer-alive", "grade": "fail", "evidence": "Last human commit 2026-05-05, > 60 days ago; no maintainer comment in thread or on any open issue"},
      {"name": "repo-active", "grade": "fail", "evidence": "Last commit 2026-05-05, > 80 days before 2026-11-13 (cutoff 2026-08-25)"},
      {"name": "not-claimed", "grade": "pass", "evidence": "No assignee, no linked PRs"},
      {"name": "scope-fit", "grade": "fail", "evidence": "Proposal requires new component + rewriting ShotForm.tsx + ActionForm.tsx + ShotsView.tsx = 4+ files"},
      {"name": "ai-policy-allowed", "grade": "unclear", "evidence": "No CONTRIBUTING.md found; AGENTS.md not found despite a commit mentioning it"},
      {"name": "beginner-friendly", "grade": "pass", "evidence": "Labeled 'good first issue'"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/pendulum-max/Veritag/issues/108",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "pendulum-max committed 2026-11-09, < 60 days"},
      {"name": "repo-active", "grade": "pass", "evidence": "Last commit 2026-11-09, < 80 days"},
      {"name": "not-claimed", "grade": "pass", "evidence": "No assignee, no linked PRs, no claim comments"},
      {"name": "scope-fit", "grade": "fail", "evidence": "Issue explicitly lists 4 files to touch (TableSkeleton.tsx, MetricCardSkeleton.tsx, brand/page.tsx, owner/page.tsx), exceeding the 3-file cap"},
      {"name": "ai-policy-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md silent on AI; silence passes"},
      {"name": "beginner-friendly", "grade": "pass", "evidence": "Labeled 'good first issue' and 'ux'"}
    ],
    "verdict": "reject"
  }
]
```
