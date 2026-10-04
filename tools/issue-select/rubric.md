# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
| --- | --- | --- | --- |
| `repo_in_use` | `repo:` line (`archived: yes/no`) and `latest release` date or `last push to any branch` date under Repo facts section | The repository `archived` flag is `no`, AND either a release or push to any branch occurred within 365 days prior to the capture date. | required |
| `ai_policy_permits` | `contribution policy` line under Repo facts section | The contribution policy does NOT explicitly ban AI-generated code or documentation. | required |
| `issue_unclaimed` | `this issue: assignees:` and `linked PRs:` under Repo facts section, plus open PR mentions or active claim comments in the comment thread | `assignees:` is `none`, AND there are NO open linked PRs, AND no active claim comment posted within the last 90 days. | required |
| `bounded_scope_and_spec` | Issue title, body text/checklist, and comment thread | The issue describes an actionable bug or feature request that is NOT blocked by missing assets (e.g., "TBD"), missing designs, or unresolved maintainer debates. (A single bug with multiple potential causes or a small list of missing items is acceptable, as long as it is not an open-ended epic/tracking issue). | required |
| `domain_of_interest` | Repo description and tags under Repo facts section, or issue body text | The repository description, tags, or issue topic explicitly relates to developer tooling, infrastructure, data analytics, cybersecurity, or AI/ML. | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

A reproduction package is accepted (`accept`) if and only if EVERY `required` check receives a `pass` grade.

If any `required` check receives a `fail` or `unclear` grade, the final verdict is `reject` (`unclear` counts as `fail`).

`preferred` checks never change or alter the binary verdict (`accept`/`reject`).
