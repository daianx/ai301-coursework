# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

<https://github.com/LegalQuants/lq-ai/issues/490>

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

Evaluation summary for candidate issue: issue-14 (LegalQuants/lq-ai#490)

- Check `maintainer_alive`: PASS (Maintainer default-branch commits on 2026-08-05)
- Check `repo_in_use`: PASS (Repository active, archived: no, last push on 2026-08-05)
- Check `ai_policy_permits`: PASS (CONTRIBUTING.md is silent on AI tools; policy permits)
- Check `issue_unclaimed`: PASS (assignees: none; linked PRs: none; 0 comments)
- Check `bounded_scope_and_spec`: PASS (Bounded documentation cleanup task listing exact file locations)

Final Verdict: accept

```json
{
  "item": "issue-14",
  "checks": [
    {"name": "maintainer_alive", "grade": "pass", "evidence": "Recent default-branch commit by SaifAlYounan on 2026-08-05"},
    {"name": "repo_in_use", "grade": "pass", "evidence": "Repository active (archived: no) with push on 2026-08-05"},
    {"name": "ai_policy_permits", "grade": "pass", "evidence": "CONTRIBUTING.md is silent on AI usage; terms permitted"},
    {"name": "issue_unclaimed", "grade": "pass", "evidence": "assignees: none; linked PRs: none; 0 comments in thread"},
    {"name": "bounded_scope_and_spec", "grade": "pass", "evidence": "Bounded documentation task with exact list of files and changes specified"}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

Run 1: 15/20 scored items

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

Issue ID: issue-05 (source: sympy/sympy#28806)
Rubric decision: reject
Gold label: reject

Reasoning:
`issue-05` ("Adding more type annotations to the codebase") is a codebase-wide type-annotation umbrella issue wearing a `good-first-issue` label. It asks contributors to incrementally add type annotations across various modules over time. The rubric check `bounded_scope_and_spec` correctly graded this issue as `fail` because it is an open-ended, multi-task tracking issue rather than a single self-contained work item suitable for a newcomer's initial contribution.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

Quoted check:
`| bounded_scope_and_spec | Issue title, body text/checklist, and comment thread | The issue describes a single, self-contained task or fix (bug fix, documentation, or feature request) with a clear target; NOT a multi-task umbrella issue, tracking megaissue, epic, or unresolved design debate. | required |`

Reasoning:
Newcomers easily fall into traps where an issue looks friendly because of a `good-first-issue` label, but is actually an umbrella tracking task (`issue-05`, `issue-10`) or has years of unresolved design debate without a settled spec (`issue-15`, `issue-20`). Requiring the issue to be a bounded single-task item ensures that a newcomer spends time implementing a settled fix rather than navigating open-ended architectural decisions.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

What the check gives up:
The strict wording of `bounded_scope_and_spec` initially caused the grader to reject well-bounded documentation tasks (`issue-01`) or maintainer-filed bugs (`issue-04`) if explicit "steps to reproduce" were not formally listed. It trades off occasional false rejects on terse but valid bug/doc tasks in order to strictly protect newcomers from getting trapped in open-ended tracking issues or design debates.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

4. Fit to interests and time: `issue-14` (`LegalQuants/lq-ai#490`) is a well-defined documentation cleanup task removing stale Discord links across 5 community doc files and routing questions to GitHub Discussions. It requires no complex code dependencies and fits cleanly within a 1-hour window for Unit 2. It is not a perfect fit to my interests but it is a good starting point and fits the time available.
5. What the verdict identified correctly vs human weighing: The rubric correctly verified that the repository is active (`last push 2026-08-05`), maintainers are active, the issue is completely unassigned with 0 comments/PRs, and the AI policy is non-restrictive. As a human, I further weighed that the issue author explicitly outlined exact lines and files to modify, ensuring a frictionless contribution.
6. Anticipated difficulty in claiming: Very low difficulty. The issue has no assigned maintainers, 0 comments in the thread, and no open linked PRs.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
