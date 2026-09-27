# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

- **Where it lives:** In an eval bundle, look under the Candidate Repro Report section (or environment block) and compare it against the Issue Context and Repo facts section. In live mode, look in the student's draft repro report or comment, comparing it against the issue body's target platform/version and the repo's `CONTRIBUTING.md` / `README.md`.
- **What good looks like:** The environment record explicitly names operating system, language runtime/compiler version, dependency versions, and execution context. The recorded versions match what the issue targets, or any version deviation is explicitly called out with a rationale.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

- **Where it lives:** In an eval bundle, look under the reproduction steps / commands section of the Candidate Repro Report. In live mode, look under the "Steps to Reproduce" heading in the draft repro comment.
- **What good looks like:** The reproduction steps are complete, deterministic, and followable by a stranger without guessing missing context. They specify the starting state (e.g., repository commit hash or branch), any required environment variables, configuration files, and exact shell commands or code snippets executed to trigger the behavior.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

- **Where it lives:** In an eval bundle, look in the artifacts section of the Candidate Repro Report (logs, terminal output excerpts, tracebacks, or test runner output). In live mode, look at the code blocks, attached logs, or terminal output in the draft comment, compared directly against the bug description in the issue body.
- **What good looks like:** The artifact directly exhibits the exact error message, stack trace, or unexpected output described in the issue. If the issue is a "cannot reproduce" report, the artifact demonstrates clean execution passing under the exact reported conditions. The output is a raw unedited snippet or relevant log excerpt, not a summarized paraphrase.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

- **Where it lives:** Compare the Candidate Repro Report's stated conclusion ("reproduced" vs "cannot reproduce" vs "partially reproduced") directly against the attached log artifacts and execution results.
- **What good looks like:** The report's claim accurately matches what the evidence demonstrates. An evidenced "cannot reproduce" (showing clean test runs under the target environment) is rated a valid pass. A report claiming full reproduction when the log shows a different error, an unrelated dependency failure, or missing evidence is rated a fail.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

- **Where it lives:** Compare the Candidate Claim Comment and Candidate Repro Report against the repo's `contribution policy` line under Repo facts (including AI usage policies, issue templates, and claim conventions), plus the issue's existing comment thread.
- **What good looks like:** The words respect all repo rules and guidelines: any required AI-assistance disclosure is explicitly stated alongside human testing confirmation, no empty claims or "+1" comments are posted, and all comments remain professional, specific to the issue, and free of generic boilerplate or unverified LLM text.
