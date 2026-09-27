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
| `environment_recorded` | Candidate Repro Report environment record compared against target issue context | The candidate repro report explicitly records the environment (naming OS, language/runtime version, or primary package version), AND either matches the issue's target setup or explicitly states and acknowledges the version or OS deviation. | required |
| `steps_followable` | Candidate Repro Report reproduction steps | The candidate repro report provides exact, complete commands or input steps that a stranger can execute starting from the repo, without relying on unshared private monorepos or missing local configuration files. | required |
| `behavior_matches_issue` | Candidate Repro Report artifacts (terminal outputs, logs, tracebacks) compared against issue description | The attached log or terminal output directly exhibits the exact bug, error message, stack trace, or behavior described in the issue (or for an evidenced cannot-reproduce report, shows clean passing execution under reported conditions), without altering command arguments or syntax to produce a different error. | required |
| `repo_in_use` | `repo:` line (`archived: yes/no`) and `latest release` date or `last push to any branch` date under Repo facts section | The repository `archived` flag is `no`, OR either a release or push to any branch occurred within 365 days prior to the capture date. | required |
| `ai_policy_permits` | `contribution policy` line under Repo facts section | The contribution policy does NOT explicitly ban AI-generated code or documentation outright (silent policies and conditional rules pass). | required |
| `issue_unclaimed` | `this issue: assignees:` and `linked PRs:` under Repo facts section, plus open PR mentions or active claim comments in the comment thread | `assignees:` is `none`, OR there are NO open linked PRs (or open PRs submitted in thread), OR no active claim comment posted within 90 days prior to capture date (stale claims over 90 days old with no PR do not block). | required |
| `bounded_scope_and_spec` | Issue title, body text/checklist, and comment thread | The issue body describes a single discrete task (not an umbrella issue, tracking metaissue, epic, or multi-task cleanup with 3+ distinct sub-tasks), AND the comment thread contains no unresolved design debate or conflicting architectural proposal from maintainers/members. | required |
| `maintainer_alive` | `last push to any branch` date, `last 5 default-branch commits` dates, or `maintainer first-response sample` under Repo facts section | There is active maintainer activity (commits, pushes, or maintainer comments) within 365 days prior to the capture date. | preferred |
| `domain_of_interest` | Repo description and tags under Repo facts section, or issue body text | The repository description, tags, or issue topic explicitly relates to developer tooling, infrastructure, data analytics, cybersecurity, or AI/ML. | preferred |
| `has_clear_reproduction_or_location` | Issue body text | The issue body or maintainer comments provide specific file paths, line numbers, code snippets, or step-by-step reproduction instructions. | required |
| `comms_quality` | Candidate Claim Comment text | The claim comment is specific, modest, and free of generic boilerplate, over-promising timeframe guarantees ("fixed in 2 days"), or empty "+1" claims. | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

A reproduction package is accepted (`accept`) if and only if EVERY `required` check receives a `pass` grade.

If any `required` check receives a `fail` or `unclear` grade, the final verdict is `reject` (`unclear` counts as `fail`).

`preferred` checks (such as `maintainer_alive`, `repo_in_use`, `issue_unclaimed`, `bounded_scope_and_spec`, `domain_of_interest`, `has_clear_reproduction_or_location`, `comms_quality`) never change or alter the binary verdict (`accept`/`reject`).
