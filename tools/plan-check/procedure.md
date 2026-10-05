# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the Issue and Repro evidence first.
2. Read the candidate plan, including Diagnosis, Scope, Changes that are planned, and then Test plan.
3. Finally, read the Candidate plan comment.

## Evidence gathering

1. Issue: Grab the issue title and the task in hand from the issue body.
2. Repro evidence: Identify the reproduced behavior. If repro evidence results all show the same output, note if any new test cases are needed to narrow down the source of the bug.
3. Candidate Plan: Gather the Diagnosis, Scope, Changes, and Test plan sections.
4. Compare the Candidate plan with the issue in hand and the repro evidence to ensure consistency and alignment.

## Check execution

1. **diagnosis (required)**: Grade by checking if the Diagnosis specifies what causes the bug and provides the evidence to support it. Pass if the cause is specified, repro evidence is used, and it agrees with the issue title. Fail if any are missing.
2. **scope (required)**: Grade by checking where the plan says what it will change. Pass if it names each file it will change, provides reasoning for the changes, and (optionally) says what it won't touch. Fail if missing.
3. **changes (required)**: Grade by checking the modified files and justification. Pass if it specifies the files being modified, justifies why it is adding/deleting, and the changes are minimal (under 500 lines). Fail if no justification is given for additions/deletions or if changes are too large.
4. **test (required)**: Grade by checking if the plan adds a test. Pass if the Candidate plan has a test provided. Fail if missing.
5. **comms (required)**: Grade by checking the Candidate plan comment against the Repo facts and issue thread. Pass if the comment respects repo conventions and matches the thread requests without generic boilerplate. Fail if it ignores stated conventions.

## Verdict assembly

1. Apply the verdict rule: Pass (ready) if all required checks pass.
2. Preferred checks do not change the verdict.
3. Unclear (?) grades count as a fail.
