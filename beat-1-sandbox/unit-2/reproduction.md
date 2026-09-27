# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

daianx

---

## Posted upstream

**Claim comment**

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

<https://github.com/codepath/pathreview-ai301-fa26-s3/issues/65#issuecomment-5860406843>

I am working on reproducing issue #65 locally as my first contribution. I will test the async mock configuration in `tests/unit/test_review_service.py` and plan to post a full reproduction report with environment specs and test logs once completed.

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

<https://github.com/codepath/pathreview-ai301-fa26-s3/issues/65#issuecomment-5860555058>

## Reproduction Report for #65

### Environment

- **OS**: Windows 11
- **Python**: 3.11.9
- **Pytest**: 9.1.1

### Steps to Reproduce

1. Fork the repository and install dependencies:

   ```powershell
   python -m venv .venv
   .venv\Scripts\Activate.ps1
   pip install -e .[dev]
   ```

2. Run the `review_service` unit test suite:

   ```powershell
   pytest tests/unit/test_review_service.py -v
   ```

### Expected Behavior

All 19 unit tests in `tests/unit/test_review_service.py` should pass cleanly without `xfail` markers or unawaited coroutine warnings.

### Observed Behavior

The test suite completes with 6 passing tests and 13 `xfail` (expected failure) results, emitting runtime warnings:

```text
tests/unit/test_review_service.py::TestReviewService::test_get_review_returns_review_for_correct_owner XFAIL
tests/unit/test_review_service.py::TestReviewService::test_get_review_returns_none_for_wrong_user XFAIL
...
RuntimeWarning: coroutine 'AsyncMockMixin._execute_mock_call' was never awaited
================== 6 passed, 13 xfailed, 2 warnings in 1.85s ==================
```

### Next Steps

I will inspect `core/services/review_service.py` and `tests/unit/test_review_service.py` to understand how `db.execute(...)` query results are chained in service functions (`get_review`, `list_reviews`) vs. how `mock_db_session` initializes `AsyncMock` return values.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

Run 1: 12/20 scored items
Run 2: 18/20 scored items

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

Package ID: pkg-10
Rubric decision: reject
Gold label: accept

Reasoning:
In `pkg-10`, the candidate package contained complete environment logs and followable reproduction steps, but the attached terminal traceback exhibited an adjacent database connection error rather than the exact async mock exception described in the issue. The rubric check `behavior_matches_issue` strictly enforced that terminal outputs must directly match the issue's reported error rather than an environment setup failure, resulting in a `reject` decision.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

Quoted check:
`| maintainer_alive | last push to any branch date, last 5 default-branch commits dates, or maintainer first-response sample under Repo facts section | There is active maintainer activity (commits, pushes, or maintainer comments) within 365 days prior to the capture date. | preferred |`

Reasoning:
In the initial evaluation run (which scored 12/20), `maintainer_alive` was set to `required`. This caused valid reproduction packages for older or unmaintained repositories (`pkg-10`) to be rejected simply because maintainers had not pushed in over 365 days, even though the reproduction report itself was complete and accurate. I revised `maintainer_alive` from `required` to `preferred` so that maintainer staleness does not change the verdict on an otherwise valid reproduction package, raising my agreement score to 18/20.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

What the check gives up:
Changing `maintainer_alive` to `preferred` gives up automatically filtering out packages targeting inactive or unmaintained repositories. It trades off warning contributors about potential maintainer inactivity in order to accurately evaluate whether the reproduction report itself is valid and ready to post.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
