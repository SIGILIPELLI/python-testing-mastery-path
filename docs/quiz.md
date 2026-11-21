---
title: "Final Quiz"
description: "Test what you have learned across all four levels of Python Testing Mastery Path with a 20-question final quiz."
---

# Final Quiz

20 questions drawn from all four levels of this course. You need **70% (14 out of 20)** to pass —
you can retake it as many times as you like. Your best result is saved in this browser.

<div id="mp-quiz-root"></div>

<script type="application/json" id="mp-quiz-data">
[
  {
    "question": "What does pytest report?\n```python\n# test_a.py\nimport pytest\n@pytest.mark.parametrize(\"x,y\", [(1, 1), (2, 3), (3, 3)])\ndef test_eq(x, y):\n    assert x == y\n```\n",
    "options": [
      "...\n3 passed",
      "1 passed",
      ".F.\n1 failed, 2 passed",
      "F..\n1 failed"
    ],
    "correctIndex": 2,
    "explanation": "One test per parameter set. Verified by running pytest (shown output normalized)."
  },
  {
    "question": "What does pytest report?\n```python\n# test_b.py\nimport pytest\n@pytest.fixture(scope=\"module\")\ndef shared(): return []\ndef test_one(shared): shared.append(1); assert shared == [1]\ndef test_two(shared): assert shared == [1]\n```\n",
    "options": [
      "FF",
      "..\n1 passed",
      "..\n2 passed",
      ".F\n1 failed"
    ],
    "correctIndex": 2,
    "explanation": "Module-scoped fixtures are shared within a file. Verified by running pytest (shown output normalized)."
  },
  {
    "question": "What does pytest report?\n```python\n# test_c.py\nimport pytest\ndef test_raises_message():\n    with pytest.raises(ValueError, match=\"positive\"):\n        raise ValueError(\"qty must be positive\")\ndef test_wrong_exception():\n    with pytest.raises(ValueError):\n        raise KeyError(\"x\")\n```\n",
    "options": [
      ".F\n1 error",
      ".F\n1 failed, 1 passed",
      "..\n2 passed",
      "FF\n2 failed"
    ],
    "correctIndex": 1,
    "explanation": "A different exception type propagates and fails the test. Verified by running pytest (shown output normalized)."
  },
  {
    "question": "What does pytest report?\n```python\n# test_d.py\nfrom unittest.mock import patch\nimport datetime\ndef greeting(now=None):\n    hour = (now or datetime.datetime.now()).hour\n    return \"morning\" if hour < 12 else \"evening\"\ndef test_fixed_time():\n    assert greeting(datetime.datetime(2026, 1, 1, 9)) == \"morning\"\n    assert greeting(datetime.datetime(2026, 1, 1, 18)) == \"evening\"\n```\n",
    "options": [
      ".\n1 passed",
      ".\n1 error",
      "Error",
      "F\n1 failed"
    ],
    "correctIndex": 0,
    "explanation": "Injecting the clock makes tests deterministic. Verified by running pytest (shown output normalized)."
  },
  {
    "question": "What does pytest report?\n```python\n# test_e.py\nimport pytest\ndef test_a(): assert True\n@pytest.mark.skip(reason=\"later\")\ndef test_b(): assert False\n@pytest.mark.skipif(True, reason=\"never runs here\")\ndef test_c(): assert False\n```\n",
    "options": [
      ".FF\n2 failed",
      ".ss\n1 passed, 2 skipped",
      "ss.\n1 passed",
      "...\n3 passed"
    ],
    "correctIndex": 1,
    "explanation": "skip and skipif. Verified by running pytest (shown output normalized)."
  },
  {
    "question": "A test passes alone but fails after another test. Cause?",
    "options": [
      "pytest bug",
      "Shared state or order dependence",
      "Python",
      "Speed"
    ],
    "correctIndex": 1,
    "explanation": "Make tests independent."
  },
  {
    "question": "What does a fixture with yield guarantee?",
    "options": [
      "The code after yield runs as teardown even if the test fails",
      "Mock",
      "Retry",
      "Skip"
    ],
    "correctIndex": 0,
    "explanation": "Cleanup."
  },
  {
    "question": "What should you mock?",
    "options": [
      "Nothing",
      "Own code",
      "Everything",
      "External boundaries like network, clock and filesystem"
    ],
    "correctIndex": 3,
    "explanation": "Not your logic."
  },
  {
    "question": "What's wrong with asserting a mock was called without checking arguments?",
    "options": [
      "Nothing",
      "Style",
      "It can pass while the call used the wrong values",
      "Speed"
    ],
    "correctIndex": 2,
    "explanation": "assert_called_once_with."
  },
  {
    "question": "What is the test pyramid?",
    "options": [
      "Many fast unit tests, fewer integration tests, few end-to-end tests",
      "Reverse",
      "UI only",
      "Equal"
    ],
    "correctIndex": 0,
    "explanation": "Speed and reliability."
  },
  {
    "question": "Which Selenium wait is preferred?",
    "options": [
      "None",
      "Implicit only",
      "Explicit waits on conditions",
      "time.sleep"
    ],
    "correctIndex": 2,
    "explanation": "Reduce flakiness."
  },
  {
    "question": "What does the Page Object Model improve?",
    "options": [
      "Coverage",
      "Cost",
      "Maintainability: UI changes are fixed in one place",
      "Speed"
    ],
    "correctIndex": 2,
    "explanation": "Encapsulation."
  },
  {
    "question": "A UI test fails only in CI. What do you collect first?",
    "options": [
      "Screenshots, logs and traces from the failing run",
      "Nothing",
      "Retry",
      "Disable"
    ],
    "correctIndex": 0,
    "explanation": "Evidence."
  },
  {
    "question": "When is a retry acceptable?",
    "options": [
      "Forever",
      "Always",
      "Never",
      "Temporarily, while tracking and fixing the root cause of flakiness"
    ],
    "correctIndex": 3,
    "explanation": "Don't hide it."
  },
  {
    "question": "What does Hypothesis add?",
    "options": [
      "Generated inputs and shrinking to minimal failing examples",
      "Mocks",
      "Reports",
      "Browsers"
    ],
    "correctIndex": 0,
    "explanation": "Properties."
  },
  {
    "question": "What does contract testing protect?",
    "options": [
      "DB",
      "Load",
      "Integrations between consumers and providers without full end-to-end environments",
      "UI"
    ],
    "correctIndex": 2,
    "explanation": "Pact."
  },
  {
    "question": "Why not chase 100% coverage?",
    "options": [
      "Speed",
      "Coverage doesn't prove assertions are meaningful",
      "Law",
      "Cost"
    ],
    "correctIndex": 1,
    "explanation": "Focus on risk."
  },
  {
    "question": "What belongs in a quality gate?",
    "options": [
      "Docs",
      "Tests passing, coverage trend and security scan results",
      "Meetings",
      "Opinion"
    ],
    "correctIndex": 1,
    "explanation": "Automated."
  },
  {
    "question": "How run tests in parallel safely?",
    "options": [
      "Make them independent and isolate shared resources",
      "Global DB",
      "Share files",
      "More sleep"
    ],
    "correctIndex": 0,
    "explanation": "pytest-xdist."
  },
  {
    "question": "What does shift-left mean?",
    "options": [
      "Finding defects earlier through reviews, unit tests and CI",
      "Manual",
      "Later",
      "UI"
    ],
    "correctIndex": 0,
    "explanation": "Cheaper."
  }
]
</script>

## Coding challenges

Try these on your own computer, then compare your output. Nothing you write is sent anywhere.

### A parametrized test suite for a shopping cart

Write the pytest suite for the Cart class: a fixture, merging quantities, parametrized rejection of bad input, parametrized discount boundaries, KeyError on removing a missing SKU, a total and one strict xfail that documents an unspecified rounding case. The file runs itself with pytest.main so it can be executed with plain python.

**Starter code**

```python
import pytest

# ---- code under test ----
class Cart:
    def __init__(self): self.lines = {}
    def add(self, sku, qty, price_cents):
        if qty <= 0: raise ValueError("qty must be positive")
        if price_cents < 0: raise ValueError("price must not be negative")
        if sku in self.lines: self.lines[sku][0] += qty
        else: self.lines[sku] = [qty, price_cents]
    def remove(self, sku):
        del self.lines[sku]
    def subtotal(self): return sum(q * p for q, p in self.lines.values())
    def discount(self): return self.subtotal() // 10 if self.subtotal() >= 10_000 else 0
    def total(self): return self.subtotal() - self.discount()

# ---- tests ----
# TODO: write tests (pytest) so that the final run reports:  10 passed, 1 xfailed
#  - a `cart` fixture with 2 pens at 250 cents
#  - subtotal, merging quantities on a repeated add
#  - parametrized rejection of bad input (qty 0, qty -1, negative price)  -> 3 tests
#  - parametrized discount boundary (9_999 -> 0, 10_000 -> 1_000, 25_000 -> 2_500)  -> 3 tests
#  - removing a missing SKU raises KeyError
#  - total after discount (4 x 3_000 -> 10_800)
#  - one strict xfail documenting that fractional-cent discounts are unspecified

if __name__ == "__main__":
    raise SystemExit(pytest.main([__file__, "-q", "--tb=no", "-rN", "-p", "no:cacheprovider", "-W", "ignore"]))
```

**Expected output**

```text
..........x                                                              [100%]
10 passed, 1 xfailed
```

<details><summary>Show solution and explanation</summary>

<pre><code>import pytest

# ---- code under test ----
class Cart:
    def __init__(self): self.lines = {}
    def add(self, sku, qty, price_cents):
        if qty &lt;= 0: raise ValueError(&quot;qty must be positive&quot;)
        if price_cents &lt; 0: raise ValueError(&quot;price must not be negative&quot;)
        if sku in self.lines: self.lines[sku][0] += qty
        else: self.lines[sku] = [qty, price_cents]
    def remove(self, sku):
        del self.lines[sku]
    def subtotal(self): return sum(q * p for q, p in self.lines.values())
    def discount(self): return self.subtotal() // 10 if self.subtotal() &gt;= 10_000 else 0
    def total(self): return self.subtotal() - self.discount()

# ---- tests ----
@pytest.fixture
def cart():
    c = Cart(); c.add(&quot;pen&quot;, 2, 250); return c

def test_subtotal(cart):
    assert cart.subtotal() == 500

def test_add_merges_quantities(cart):
    cart.add(&quot;pen&quot;, 3, 250)
    assert cart.lines[&quot;pen&quot;][0] == 5 and cart.subtotal() == 1250

@pytest.mark.parametrize(&quot;qty,price&quot;, [(0, 100), (-1, 100), (1, -5)])
def test_add_rejects_bad_input(qty, price):
    with pytest.raises(ValueError):
        Cart().add(&quot;x&quot;, qty, price)

@pytest.mark.parametrize(&quot;subtotal_cents,expected_discount&quot;, [(9_999, 0), (10_000, 1_000), (25_000, 2_500)])
def test_discount_boundary(subtotal_cents, expected_discount):
    c = Cart(); c.add(&quot;big&quot;, 1, subtotal_cents)
    assert c.discount() == expected_discount

def test_remove_missing_sku_raises(cart):
    with pytest.raises(KeyError):
        cart.remove(&quot;nope&quot;)

def test_total_after_discount():
    c = Cart(); c.add(&quot;a&quot;, 4, 3_000)
    assert c.total() == 10_800

@pytest.mark.xfail(reason=&quot;rounding of fractional cents is not specified yet&quot;, strict=True)
def test_known_gap():
    c = Cart(); c.add(&quot;a&quot;, 1, 10_001)
    assert c.discount() == 1_000.1

if __name__ == &quot;__main__&quot;:
    raise SystemExit(pytest.main([__file__, &quot;-q&quot;, &quot;--tb=no&quot;, &quot;-rN&quot;, &quot;-p&quot;, &quot;no:cacheprovider&quot;, &quot;-W&quot;, &quot;ignore&quot;]))
</code></pre>

<p>Fixtures give every test fresh state, parametrization turns boundary tables into separate test cases, pytest.raises checks the error path and a strict xfail documents a known gap (it would fail the run if the behavior unexpectedly started working). Verified by running the file with pytest.</p>
</details>

### Testing a rate limiter with a fake clock, parametrization and Hypothesis

Write tests for a token-bucket RateLimiter using an injected FakeClock (no real sleeping), a parametrized partial-refill table and two Hypothesis properties (tokens stay in bounds; allowed calls never exceed the budget). Include a test proving the limiter uses the injected clock and not wall time.

**Starter code**

```python
import time
import pytest
from hypothesis import given, strategies as st

# ---- code under test: a token-bucket rate limiter with an injectable clock ----
class RateLimiter:
    def __init__(self, capacity, per_second, clock=time.monotonic):
        self.capacity, self.rate, self.clock = capacity, per_second, clock
        self.tokens, self.last = float(capacity), clock()
    def allow(self, cost=1):
        now = self.clock()
        self.tokens = min(self.capacity, self.tokens + (now - self.last) * self.rate)
        self.last = now
        if self.tokens >= cost:
            self.tokens -= cost
            return True
        return False

class FakeClock:
    def __init__(self): self.t = 0.0
    def __call__(self): return self.t
    def advance(self, s): self.t += s

# ---- tests ----
# TODO: write the tests so the run reports:  9 passed
#  - a FakeClock-based `clock` fixture (already defined above)
#  - burst of 3 then blocked; refill after advancing the clock
#  - parametrized partial refill: capacity 1, rate 2/s: waits 0.4 -> False, 0.5 -> True, 10 -> True   (3 tests)
#  - never exceeds capacity after a very long wait
#  - hypothesis: tokens always within [0, capacity] for random waits
#  - hypothesis: number of allowed calls == min(capacity, calls) when the rate is 1/s and no time passes
#  - the limiter uses the injected clock, not wall time (sleep 10 ms, still blocked)

if __name__ == "__main__":
    raise SystemExit(pytest.main([__file__, "-q", "--tb=no", "-rN", "-p", "no:cacheprovider", "-W", "ignore"]))
```

**Expected output**

```text
.........                                                                [100%]
9 passed
```

<details><summary>Show solution and explanation</summary>

<pre><code>import time
import pytest
from hypothesis import given, strategies as st

# ---- code under test: a token-bucket rate limiter with an injectable clock ----
class RateLimiter:
    def __init__(self, capacity, per_second, clock=time.monotonic):
        self.capacity, self.rate, self.clock = capacity, per_second, clock
        self.tokens, self.last = float(capacity), clock()
    def allow(self, cost=1):
        now = self.clock()
        self.tokens = min(self.capacity, self.tokens + (now - self.last) * self.rate)
        self.last = now
        if self.tokens &gt;= cost:
            self.tokens -= cost
            return True
        return False

class FakeClock:
    def __init__(self): self.t = 0.0
    def __call__(self): return self.t
    def advance(self, s): self.t += s

# ---- tests ----
@pytest.fixture
def clock(): return FakeClock()

def test_burst_then_blocked(clock):
    rl = RateLimiter(3, 1, clock)
    assert [rl.allow() for _ in range(4)] == [True, True, True, False]

def test_refills_over_time(clock):
    rl = RateLimiter(2, 1, clock)
    rl.allow(); rl.allow()
    assert not rl.allow()
    clock.advance(1)
    assert rl.allow() and not rl.allow()

@pytest.mark.parametrize(&quot;wait,expected&quot;, [(0.4, False), (0.5, True), (10, True)])
def test_partial_refill(clock, wait, expected):
    rl = RateLimiter(1, 2, clock)
    assert rl.allow()
    clock.advance(wait)
    assert rl.allow() == expected

def test_never_exceeds_capacity(clock):
    rl = RateLimiter(2, 5, clock)
    clock.advance(1000)
    assert [rl.allow() for _ in range(3)] == [True, True, False]

@given(st.lists(st.floats(min_value=0, max_value=5, allow_nan=False), max_size=50))
def test_tokens_stay_within_bounds(waits):
    clock = FakeClock(); rl = RateLimiter(4, 2, clock)
    for w in waits:
        clock.advance(w)
        rl.allow()
        assert 0 &lt;= rl.tokens &lt;= rl.capacity

@given(st.integers(min_value=1, max_value=20), st.integers(min_value=1, max_value=20))
def test_allowed_never_exceeds_budget(capacity, calls):
    clock = FakeClock(); rl = RateLimiter(capacity, 1, clock)
    assert sum(rl.allow() for _ in range(calls)) == min(capacity, calls)

def test_uses_injected_clock_not_wall_time(clock):
    rl = RateLimiter(1, 1, clock)
    assert rl.allow()
    time.sleep(0.01)                      # real time passing must not refill the bucket
    assert not rl.allow()

if __name__ == &quot;__main__&quot;:
    raise SystemExit(pytest.main([__file__, &quot;-q&quot;, &quot;--tb=no&quot;, &quot;-rN&quot;, &quot;-p&quot;, &quot;no:cacheprovider&quot;, &quot;-W&quot;, &quot;ignore&quot;]))
</code></pre>

<p>Injecting the clock makes time-based code deterministic; properties check invariants for many generated inputs; example-based tests pin down boundaries. Verified by running the file with pytest and Hypothesis.</p>
</details>
