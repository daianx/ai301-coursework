# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
| --- | --- | --- | --- |
| `maintainer_alive` | `last push to any branch` date, `last 5 default-branch commits` dates, or `maintainer first-response sample` under Repo facts section | There is active maintainer activity (commits, pushes, or comments) within the last 90 days prior to the capture date. | required |
| `repo_in_use` | `repo:` line (`archived: yes/no`) and `latest release` date or `last push to any branch` date under Repo facts section | The repository `archived` flag is `no`, AND either the latest release or last push to any branch occurred within the last 90 days prior to the capture date. | required |
| `ai_policy_permits` | `contribution policy` line under Repo facts section | The contribution policy does NOT explicitly ban AI-generated code or documentation outright (silent policies and conditional rules pass). | required |
| `issue_unclaimed` | `this issue: assignees:` and `linked PRs:` under Repo facts section, plus open PR mentions or active claim comments in the comment thread | The issue is NOT already assigned (`assignees: none`), has NO open linked PRs (or open PRs submitted in thread), and no active claim indicating someone is currently working on it. | required |
| `bounded_scope_and_spec` | Issue title, body text/checklist, and comment thread | The issue and scope are clearly defined (e.g., with steps to reproduce or a clear description of the desired feature/fix); NOT an umbrella issue, tracking megaissue, open design debate, or feature wish without a settled spec. | required |
| `domain_of_interest` | Repo description and tags under Repo facts section, or issue body text | The repository or issue topic relates to domains of interest such as cybersecurity or data analytics. | preferred |
| `has_clear_reproduction_or_location` | Issue body text | The issue body provides specific code/doc references, file locations, or exact steps to reproduce. | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

An issue is accepted (`accept`) if and only if EVERY `required` check receives a `pass` grade.

If any `required` check receives a `fail` or `unclear` grade, the final verdict is `reject` (`unclear` counts as `fail`).

`preferred` checks (such as `domain_of_interest`) never change or alter the binary verdict (`accept`/`reject`); they are used exclusively to rank and compare accepted candidates.
