# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

daianx

**Plan comment**

<https://github.com/codepath/pathreview-ai301-fa26-s3/issues/65#issuecomment-5986933586>

This is my plan to fix issue #65 regarding the `RuntimeWarning: coroutine was never awaited` warnings and `xfail` results in the test suite.

**Diagnosis:** The `mock_result` returned by `mock_db_session.execute` in `tests/unit/test_review_service.py` is currently initialized as an `AsyncMock()`. Because `AsyncMock` returns awaitables for all its method calls, synchronous SQLAlchemy calls like `result.scalars().all()` return unawaited coroutines instead of lists, causing the warnings and test failures.

**Scope:** I will only modify `tests/unit/test_review_service.py`. I will not touch the application's service logic in `core/services/review_service.py`.

**Approach:** I will change `mock_result = AsyncMock()` to `mock_result = Mock()` across the test suite. This ensures that while `await mock_db_session.execute(...)` properly acts as an async call, the returned result object provides synchronous methods like `.scalars().all()` as expected by the service code. Additionally, I will remove the `@pytest.mark.xfail(strict=True)` decorators from the tests, as the fix will cause them to pass and `strict=True` would flag an unexpected pass (`XPASS`) as a failure.

**Test Plan:** I will run `pytest tests/unit/test_review_service.py -v` to confirm that all 19 tests pass cleanly with no `xfail` items and no `RuntimeWarning`.

---

## Your branch

**Branch**

fix/issue-65-change-async-to-mock

**Evidence**

# Test Plan Execution Results

## Before Fix

**Command:**

```powershell
pytest tests/unit/test_review_service.py -v
```

**Output:**

```
===================================== test session starts =====================================
platform win32 -- Python 3.11.9, pytest-9.1.1, pluggy-1.6.0
rootdir: C:\Users\CodePath\AI301\Coursework\pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: anyio-4.13.0, hypothesis-6.168.2, langsmith-0.8.9, platformdirs-4.12.0, asyncio-1.4.0, benchmark-5.3.0, cov-7.1.0, pytest_httpserver-1.1.5
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collecting ... collected 19 items

tests/unit/test_review_service.py::TestReviewService::test_create_review_returns_review_with_pending_status PASSED [  5%]
tests/unit/test_review_service.py::TestReviewService::test_get_review_returns_review_for_correct_owner XFAIL (strict) [ 10%]
tests/unit/test_review_service.py::TestReviewService::test_get_review_returns_none_for_wrong_user XFAIL (strict) [ 15%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_returns_paginated_results XFAIL (strict) [ 21%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_page_2_returns_correct_offset XFAIL (strict) [ 26%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_returns_tuple XFAIL (strict) [ 31%]
tests/unit/test_review_service.py::TestReviewService::test_create_review_calls_db_add PASSED [ 36%]
tests/unit/test_review_service.py::TestReviewService::test_create_review_calls_db_commit PASSED [ 42%]
tests/unit/test_review_service.py::TestReviewService::test_create_review_calls_db_refresh PASSED [ 47%]
tests/unit/test_review_service.py::TestReviewService::test_get_review_uses_select_and_join XFAIL (strict) [ 52%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_default_pagination XFAIL (strict) [ 57%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_custom_page_size XFAIL (strict) [ 63%]
tests/unit/test_review_service.py::TestReviewService::test_create_review_with_uuid_ids PASSED [ 68%]
tests/unit/test_review_service.py::TestReviewService::test_get_review_verifies_ownership XFAIL (strict) [ 73%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_counts_total XFAIL (strict) [ 78%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_returns_reviews_list XFAIL (strict) [ 84%]
tests/unit/test_review_service.py::TestReviewService::test_review_sections_and_score_initially_none PASSED [ 89%]
tests/unit/test_review_service.py::TestReviewService::test_get_review_with_valid_uuid XFAIL (strict) [ 94%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_ordered_by_created_at XFAIL (strict) [100%]

================================== warnings summary ===================================
tests/unit/test_review_service.py::TestReviewService::test_get_review_returns_review_for_correct_owner
  RuntimeWarning: coroutine 'AsyncMockMixin._execute_mock_call' was never awaited

tests/unit/test_review_service.py::TestReviewService::test_get_review_returns_none_for_wrong_user
  RuntimeWarning: coroutine 'AsyncMockMixin._execute_mock_call' was never awaited

================== 6 passed, 13 xfailed, 2 warnings in 1.85s ==================
```

## After Fix

**Command:**

```powershell
pytest tests/unit/test_review_service.py -v
```

**Output:**

```
============================= test session starts =============================
platform win32 -- Python 3.11.9, pytest-9.1.1, pluggy-1.6.0 -- C:\Users\CodePath\AppData\Local\Programs\Python\Python311\python.exe
cachedir: .pytest_cache
hypothesis profile 'default'
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: C:\Users\CodePath\AI301\Coursework\pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: anyio-4.13.0, hypothesis-6.168.2, langsmith-0.8.9, platformdirs-4.12.0, asyncio-1.4.0, benchmark-5.3.0, cov-7.1.0, pytest_httpserver-1.1.5
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collecting ... collected 19 items

tests/unit/test_review_service.py::TestReviewService::test_create_review_returns_review_with_pending_status PASSED [  5%]
tests/unit/test_review_service.py::TestReviewService::test_get_review_returns_review_for_correct_owner PASSED [ 10%]
tests/unit/test_review_service.py::TestReviewService::test_get_review_returns_none_for_wrong_user PASSED [ 15%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_returns_paginated_results PASSED [ 21%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_page_2_returns_correct_offset PASSED [ 26%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_returns_tuple PASSED [ 31%]
tests/unit/test_review_service.py::TestReviewService::test_create_review_calls_db_add PASSED [ 36%]
tests/unit/test_review_service.py::TestReviewService::test_create_review_calls_db_commit PASSED [ 42%]
tests/unit/test_review_service.py::TestReviewService::test_create_review_calls_db_refresh PASSED [ 47%]
tests/unit/test_review_service.py::TestReviewService::test_get_review_uses_select_and_join PASSED [ 52%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_default_pagination PASSED [ 57%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_custom_page_size PASSED [ 63%]
tests/unit/test_review_service.py::TestReviewService::test_create_review_with_uuid_ids PASSED [ 68%]
tests/unit/test_review_service.py::TestReviewService::test_get_review_verifies_ownership PASSED [ 73%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_counts_total PASSED [ 78%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_returns_reviews_list PASSED [ 84%]
tests/unit/test_review_service.py::TestReviewService::test_review_sections_and_score_initially_none PASSED [ 89%]
tests/unit/test_review_service.py::TestReviewService::test_get_review_with_valid_uuid PASSED [ 94%]
tests/unit/test_review_service.py::TestReviewService::test_list_reviews_ordered_by_created_at PASSED [100%]

============================== warnings summary ===============================
core\config.py:7
  C:\Users\CodePath\AI301\Coursework\pathreview-ai301-fa26-s3\core\config.py:7: PydanticDeprecatedSince20: Support for class-based `config` is deprecated, use ConfigDict instead. Deprecated in Pydantic V2.0 to be removed in V3.0. See Pydantic V2 Migration Guide at https://errors.pydantic.dev/2.13/migration/
    class Settings(BaseSettings):

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
======================== 19 passed, 1 warning in 0.95s ========================
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

17/20, 19/20

**Package analysis**

pkg-04
Gold label: reject
Our rubric: reject
Why: Our rubric evaluated `pkg-04` against the `comms` check and found it lacking any issue reference or conversational thread awareness, which violated thread conventions. This correctly aligned our evaluation with the gold label's rejection reason.

**Check rationale**

Check: | comms | Is the comment written as a natural reply linking the issue context? | Must explicitly reference the issue and not sound like a rigid template | 2 |

Rationale: We added this check to specifically test for `thread-convention` requirements. Previously, plans that had strong technical merits were being accepted even if they ignored conversation history and repo norms. This check strictly enforces thread integration and explicit issue referencing.

**Trade-offs**

Adding the `comms` check successfully changes `pkg-04` from `accept` to `reject`. The trade-off is that we may occasionally reject a completely technically accurate plan purely because it lacks a conversational greeting or an explicit issue number link. However, this is acceptable because adhering to repository thread conventions is required.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
