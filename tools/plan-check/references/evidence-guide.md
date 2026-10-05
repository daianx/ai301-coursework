# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

- Where it lives: Issue body (for the title/task), Repro evidence section, and Candidate Plan's Diagnosis section.
- What good looks like: The diagnosis clearly specifies the cause of the bug. It is supported by the repro evidence, and is relevant to the issue title.

## Scope

- Where it lives: Candidate Plan's Scope section.
- What good looks like: The plan names each file it will change, says what it won't touch, and provides reasoning for what the changes are for.

## Executability

- Where it lives: Candidate Plan's Changes section.
- What good looks like: It specifies the exact files being modified and why. If it involves adding or deleting files, it provides justification. The changes are minimal (under 500 lines).

## Test plan

- Where it lives: Candidate Plan's Test plan section.
- What good looks like: The plan adds a test that verifies the changes effectively.

## Honesty

- Where it lives: Risks and Unknowns section of the plan.
- What good looks like: The plan acknowledges any risks, uncertainties, or deviations and explains how they will be mitigated.

## Comms

- Where it lives: Candidate Plan comment.
- What good looks like: The comment is professional, aligns with the issue's thread, and accurately summarizes the planned changes without overpromising.
