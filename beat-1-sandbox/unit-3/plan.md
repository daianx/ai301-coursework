# Plan for Issue #65

## Diagnosis

The issue states that tests are failing with `RuntimeWarning: coroutine 'AsyncMockMixin._execute_mock_call' was never awaited`. In the repro evidence, running the `review_service` unit test suite results in:

```
RuntimeWarning: coroutine 'AsyncMockMixin._execute_mock_call' was never awaited
================== 6 passed, 13 xfailed, 2 warnings in 1.85s ==================
```

This indicates that the returned result objects from `mock_db_session.execute` are incorrectly initialized as `AsyncMock` objects in `tests/unit/test_review_service.py`. When the service correctly awaits the `execute()` call, it gets back an `AsyncMock` object instead of a synchronous Mock. Consequently, subsequent synchronous SQLAlchemy method calls like `.scalars().all()` or `.scalars().first()` return unawaited coroutines instead of concrete values, producing the warnings and `xfail` items.

## Scope

- Files I will change: `tests/unit/test_review_service.py`
- What I won't touch: I will not modify any service logic in `core/services/review_service.py` or the actual database models.

## Approach

I will modify `tests/unit/test_review_service.py` in three ways:

1. **Fix the AsyncMock issue**: Change `mock_result = AsyncMock()` to `mock_result = Mock()` across all the test functions. This will ensure that `mock_db_session.execute(...)` behaves as an awaitable but resolves to a synchronous result Mock, properly imitating SQLAlchemy 2.0 `Result` objects.
2. **Remove xfail decorators**: Remove the `@pytest.mark.xfail(strict=True...)` decorators from all the updated tests. Because the `Mock()` fix resolves the original issue, the tests will now pass successfully. Leaving `strict=True` causes pytest to fail them as an unexpected pass (`XPASS(strict)`).

## Test Plan

I will run the exact same reproduction steps as the original issue:

1. Activate the environment:

   ```powershell
   python -m venv .venv
   .venv\Scripts\Activate.ps1
   pip install -e .[dev]
   ```

2. Run the `review_service` unit test suite:

   ```powershell
   pytest tests/unit/test_review_service.py -v
   ```

**Expected Result:** All 19 unit tests should pass successfully without any `xfail` results and without `RuntimeWarning: coroutine was never awaited`.

## Risks and Unknowns

- There may be multiple areas where `AsyncMock` needs to be updated. If the tests use different mock return values dynamically, I might need to adjust the `side_effect` instead of `return_value`.

## Deviations

One minor deviation during implementation: In `test_list_reviews_ordered_by_created_at`, removing the `xfail` decorator exposed a faulty test assertion (`mock_db_session.execute.assert_called_once()`). Because `list_reviews` correctly executes two queries (one to count the total, one to fetch the reviews), the `execute` mock is actually called twice. The fix required changing the assertion to `assert mock_db_session.execute.call_count == 2` to properly reflect the service logic.
