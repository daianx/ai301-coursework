# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis | Issue title, Repro evidence, Candidate plan diagnosis | passes if the plan says what causes the bug and also provides the evidence to support the diagnosis in agreement with the issue title (diagnosis is relevant to the issue). | required |
| scope | Candidate plan scope | passes if it names each file it will change and says what it won't touch. Provide reasoning for what the changes are for. | required |
| changes | Candidate plan changes | passes if it specifies the files being modified and why. If adding/deleting, it must justify why. Changes should be minimal (under 500 lines). | required |
| test | Candidate plan test | passes if the plan adds a test. | required |
| comms | Candidate plan comment, Repo facts | passes if the comment is free of generic boilerplate, respects repo conventions, and matches the thread requests. | required |

## Verdict rule

ready if every required check passes. Preferred checks do not change the verdict. Unclear (?) counts as fail.
