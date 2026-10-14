# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/84

**Branch**

fix/72-handle-unknown-hash-error

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. 19/20 scored items  (bar: 18/20: PASS)

**Package analysis**

`pkg-13`:
- Gold label: `accept`
- Rubric decision: `reject`
- Explanation: The rubric failed `pkg-13` on `standards-compliance` because the PR description omitted one of the standard checklist sections required by the target repository's template, even though the core code fix was fully correct and contained no drift. While gold allowed the omission under a permissive template threshold, our rubric strictly required all template sections to be filled.

**Check rationale**

Check from `rubric.md`:
`| standards-compliance | The PR title and description read against the repo's PR template and contributing instructions | All required sections of the PR template are filled with substantive content (no blank fields or leftover placeholders), and required disclosures (including AI-use disclosure) are present | required |`

Why it reads that way:
The check was formulated to reject pull requests that bypass repository instructions by leaving template sections empty or omitting the required AI-use disclosure. The category floor specifically requires matching both packages in `standards-wall`, so the check was made strict to guarantee that PRs skipping mandatory repository standards (like `pkg-01` and `pkg-20`) are reliably caught.

**Trade-offs**

By enforcing strict adherence to every template section under `standards-compliance`, the rubric produced a false rejection on `pkg-13` (where the gold label accepted despite a minor template omission). This trade-off was accepted to guarantee a 100% detection rate on the critical `standards-wall` category (`pkg-01` and `pkg-20`), satisfying the category floor bar without introducing false passes on substandard PRs.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
