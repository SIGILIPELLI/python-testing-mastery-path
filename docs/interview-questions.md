---
title: "Python Testing Interview Questions and Answers (180 Questions)"
description: "180 Python Testing interview questions with answers and explanations, from beginner to advanced, organised by level. Free, from the Python Testing Mastery Path."
---

# Python Testing Interview Questions and Answers

**180 questions** with the correct answer and a short explanation, organised from beginner (Level 1) to advanced (Level 4). Every question comes from a lesson in the free Python Testing Mastery Path, so you can open the lesson to go deeper.

!!! tip "Practise, don't just read"
    Each lesson also ends with an interactive quiz, and the [final quiz](quiz.md) tests all four levels. Try to answer each question below before reading the answer.

## Level 1 · Entry

### [01 · What Is Software Testing?](level-1/01-what-is-software-testing.md)

**Q1.** What is the main goal of software testing?

**Answer:** Find defects and give information about quality and risk

Testing can't prove absence of bugs.

**Q2.** Which principle says exhaustive testing is impossible?

**Answer:** Test with risk-based selection because inputs and paths are practically infinite

Prioritize.

**Q3.** What is the difference between verification and validation?

**Answer:** Verification checks we built it right; validation checks we built the right thing

Spec vs need.

**Q4.** Why test early?

**Answer:** Defects are cheaper to find and fix the earlier they're caught

Shift left.

### [02 · Test Case Design &amp; Documentation](level-1/02-test-case-design.md)

**Q5.** What does equivalence partitioning do?

**Answer:** Groups inputs that should behave the same and tests one per group

Reduces cases.

**Q6.** An age field accepts 18–65. Which boundary values do you test?

**Answer:** 17, 18, 65, 66

Boundary value analysis.

**Q7.** What is a decision table for?

**Answer:** Testing combinations of conditions and their outcomes

Business rules.

**Q8.** What makes a good test case?

**Answer:** Clear steps, data, expected result and independence

Reproducible.

### [03 · Test Types &amp; Levels](level-1/03-test-types-levels.md)

**Q9.** What is the test pyramid?

**Answer:** Many unit tests, fewer integration tests and fewest end-to-end tests

Speed and cost.

**Q10.** Which test type checks components work together?

**Answer:** Integration test

Interfaces.

**Q11.** What is a smoke test?

**Answer:** A quick check that the build's critical functions work

Gatekeeper.

**Q12.** What does regression testing guard against?

**Answer:** Previously working behavior breaking after changes

Automate.

### [04 · Defect Lifecycle &amp; Bug Reporting](level-1/04-defect-lifecycle.md)

**Q13.** What is the usual defect lifecycle?

**Answer:** New → assigned → fixed → retested → closed (or reopened)

Tracking.

**Q14.** What should a bug report include?

**Answer:** Steps to reproduce, expected vs actual, environment and evidence

Reproducible.

**Q15.** Severity vs priority?

**Answer:** Severity is impact; priority is how soon to fix

Different axes.

**Q16.** What is a 'cannot reproduce' bug?

**Answer:** One the developer can't recreate; add details or logs

Collaborate.

### [05 · Manual Testing in Practice](level-1/05-manual-testing-practice.md)

**Q17.** What is exploratory testing?

**Answer:** Simultaneous learning, test design and execution guided by charters

Finds unexpected bugs.

**Q18.** When is manual testing best?

**Answer:** Usability, exploration and one-off checks

Human judgement.

**Q19.** What is a test charter?

**Answer:** A mission and time-box for an exploratory session

Focus.

**Q20.** What do you record in sessions?

**Answer:** Notes, bugs found and areas covered

Evidence.

### [06 · Python Setup for Testers](level-1/06-python-setup.md)

**Q21.** What does this print?

```python
import sys
print(sys.version_info >= (3, 9))
import pytest
print(pytest.__name__)
```

**Answer:** True
pytest

Environment sanity check. Verified by running it.

**Q22.** Why use a virtual environment?

**Answer:** Isolate dependencies per project

Reproducible.

**Q23.** How pin test dependencies?

**Answer:** requirements.txt/lock file with exact versions

Reproducible CI.

**Q24.** What does pip install -e . do?

**Answer:** Installs the project in editable mode for development

Import your package.

### [07 · pytest Fundamentals](level-1/07-pytest-fundamentals.md)

**Q25.** What does pytest report?

```python
# test_a.py
def test_pass(): assert 2 + 2 == 4
def test_fail(): assert "a".upper() == "b"
def test_error_in_code(): int("x")
```

**Answer:** .FF
2 failed, 1 passed

Assertion introspection shows values. Verified by running pytest (shown output normalized).

**Q26.** What does pytest report?

```python
# test_b.py
import pytest
def test_raises():
    with pytest.raises(ZeroDivisionError):
        1 / 0
def test_approx():
    assert 0.1 + 0.2 == pytest.approx(0.3)
def test_skip():
    pytest.skip("not today")
@pytest.mark.xfail
def test_known_bug():
    assert False
```

**Answer:** ..sx
2 passed, 1 skipped, 1 xfailed

raises, approx, skip, xfail. Verified by running pytest (shown output normalized).

**Q27.** How does pytest discover tests?

**Answer:** Files named test_*.py or *_test.py with functions named test_*

Conventions.

**Q28.** What's the advantage of plain assert?

**Answer:** pytest rewrites it to show helpful values on failure

No self.assertEqual.

### [08 · pytest Fixtures &amp; Parametrize](level-1/08-fixtures-parametrize.md)

**Q29.** What does pytest report?

```python
# test_f.py
import pytest
@pytest.fixture
def items():
    return []
def test_a(items):
    items.append(1)
    assert items == [1]
def test_b(items):
    assert items == []
@pytest.mark.parametrize("a,b,total", [(1, 2, 3), (2, 2, 4), (5, 5, 11)])
def test_add(a, b, total):
    assert a + b == total
```

**Answer:** ....F
1 failed, 4 passed

Function-scoped fixtures give each test a fresh object; parametrize creates one test per row. Verified by running pytest (shown output normalized).

**Q30.** What does `yield` do in a pytest fixture?

**Answer:** Splits setup (before) from teardown (after the test)

Cleanup.

**Q31.** What does scope='session' do?

**Answer:** Creates the fixture once for the whole run

Expensive resources.

**Q32.** Where do shared fixtures go?

**Answer:** conftest.py

Auto-discovered.

### [09 · Selenium WebDriver Basics with Python](level-1/09-selenium-basics.md)

**Q33.** What does Selenium automate?

**Answer:** A real browser through WebDriver

UI tests.

**Q34.** What are explicit waits for?

**Answer:** Waiting for a condition (visible, clickable) instead of sleeping

WebDriverWait.

**Q35.** Which locator is usually most stable?

**Answer:** IDs or dedicated test attributes (data-testid)

Resilient.

**Q36.** Why avoid time.sleep?

**Answer:** It is slow and still flaky; wait for conditions

Sync properly.

### [10 · Project — Test Plan + Automated Suite](level-1/10-project-test-suite.md)

**Q37.** What does the test suite project combine?

**Answer:** Manual design, pytest tests, fixtures, parametrization and Selenium checks

Level 1 project.

**Q38.** How organize tests?

**Answer:** By feature with clear names and shared fixtures

Maintainable.

**Q39.** What should failures show?

**Answer:** Clear assertion messages and screenshots for UI tests

Diagnosable.

**Q40.** How run a subset?

**Answer:** -k expression or markers (-m smoke)

Selective runs.

## Level 2 · Intermediate

### [01 · Page Object Model in Python](level-2/01-page-object-model.md)

**Q41.** What does pytest report for this page-object test?

```python
# test_pom.py
class Page:
    def __init__(self, store): self.store = store
class LoginPage(Page):
    def login(self, user, pw):
        self.store["user"] = user if pw == "ok" else None
        return self
    @property
    def logged_in(self): return self.store.get("user") is not None
def test_login():
    assert LoginPage({}).login("ann", "ok").logged_in
def test_bad():
    assert not LoginPage({}).login("ann", "no").logged_in
```

**Answer:** ..
2 passed

Page objects hold actions and state; tests assert intent. Verified by running pytest (shown output normalized).

**Q42.** What belongs in a page object?

**Answer:** Locators and user actions, not test assertions about goals

Encapsulation.

**Q43.** What's the main benefit of POM?

**Answer:** One place to fix when the UI changes

Maintainability.

**Q44.** Should page methods return something?

**Answer:** Often another page object or self for fluent flows

Chaining.

### [02 · Selenium Advanced](level-2/02-selenium-advanced.md)

**Q45.** When use ActionChains?

**Answer:** Hover, drag-and-drop and complex mouse/keyboard sequences

Advanced input.

**Q46.** How handle iframes?

**Answer:** Switch to the frame first, then back to default content

switch_to.frame.

**Q47.** How handle alerts?

**Answer:** switch_to.alert to accept or dismiss

Browser dialogs.

**Q48.** How run JavaScript?

**Answer:** execute_script (sparingly)

Escape hatch.

### [03 · API Testing with requests + pytest](level-2/03-api-testing.md)

**Q49.** What does pytest report?

```python
# test_api.py
import json
from http.server import BaseHTTPRequestHandler, HTTPServer
from threading import Thread
from urllib.request import urlopen
class H(BaseHTTPRequestHandler):
    def do_GET(self):
        body = json.dumps({"id": 7, "name": "ann"}).encode()
        self.send_response(200); self.send_header("Content-Type", "application/json"); self.end_headers(); self.wfile.write(body)
    def log_message(self, *a): pass
def test_get_user():
    srv = HTTPServer(("127.0.0.1", 0), H); Thread(target=srv.serve_forever, daemon=True).start()
    r = urlopen(f"http://127.0.0.1:{srv.server_port}/users/7")
    assert r.status == 200 and r.headers["Content-Type"] == "application/json"
    assert json.load(r) == {"id": 7, "name": "ann"}
    srv.shutdown()
```

**Answer:** .
1 passed

A tiny local server makes API tests deterministic. Verified by running pytest (shown output normalized).

**Q50.** What should API tests assert?

**Answer:** Status code, headers and the response body schema

Contract.

**Q51.** Why test negative cases?

**Answer:** Invalid input and auth failures must be handled correctly

Robustness.

**Q52.** Which library is common for HTTP tests?

**Answer:** requests (or httpx) with pytest

Simple.

### [04 · Mocking with unittest.mock](level-2/04-mocking.md)

**Q53.** What does pytest report?

```python
# test_m.py
from unittest.mock import Mock, patch
def fetch(client, uid): return client.get(f"/u/{uid}")["name"].upper()
def test_fetch():
    c = Mock(); c.get.return_value = {"name": "ann"}
    assert fetch(c, 3) == "ANN"
    c.get.assert_called_once_with("/u/3")
def test_patch():
    with patch("os.getenv", return_value="x") as g:
        import os
        assert os.getenv("A") == "x"
        g.assert_called_once_with("A")
def test_side_effect():
    m = Mock(side_effect=[1, ValueError("boom")])
    assert m() == 1
    try: m()
    except ValueError as e: assert str(e) == "boom"
```

**Answer:** ...
3 passed

Mock return values, patch and side effects. Verified by running pytest (shown output normalized).

**Q54.** What should you mock?

**Answer:** Slow or external boundaries (network, clock, DB), not your own logic

Boundary mocking.

**Q55.** What is the patch rule?

**Answer:** Patch where the name is looked up, not where it's defined

Common trap.

**Q56.** What does assert_called_once_with verify?

**Answer:** That the mock was called exactly once with those arguments

Interaction check.

### [05 · Test Data Management &amp; Factories](level-2/05-test-data-management.md)

**Q57.** What's a good test data approach?

**Answer:** Create data per test with factories and clean it up

Isolation.

**Q58.** What is a factory?

**Answer:** A helper creating valid objects with overridable defaults

Readable tests.

**Q59.** Why avoid shared mutable data?

**Answer:** Tests become order-dependent and flaky

Independence.

**Q60.** How handle secrets in tests?

**Answer:** Environment variables or a secret store

Security.

### [06 · pytest Plugins &amp; Configuration](level-2/06-pytest-config.md)

**Q61.** What does pytest report with this config?

```python
# pytest.ini
[pytest]
addopts = -q --tb=no -m "not slow"
markers =
    slow: slow tests

# test_c.py
import pytest
def test_fast(): pass
@pytest.mark.slow
def test_slow(): pass
```

**Answer:** .
1 passed, 1 deselected

addopts and markers in pytest.ini. Verified by running pytest (shown output normalized).

**Q62.** What do markers allow?

**Answer:** Selecting or skipping groups of tests (-m smoke)

Register them.

**Q63.** Where else can config live?

**Answer:** pyproject.toml or tox.ini

Common files.

**Q64.** What does --strict-markers do?

**Answer:** Fails on unregistered markers (catching typos)

Safety.

### [07 · Reporting (pytest-html, Allure)](level-2/07-reporting.md)

**Q65.** Which plugin makes HTML reports?

**Answer:** pytest-html

Readable results.

**Q66.** What does Allure add?

**Answer:** Rich reports with steps, attachments and history

Team reporting.

**Q67.** What does --junitxml do?

**Answer:** Writes results CI tools understand

Integration.

**Q68.** What belongs in a failure report?

**Answer:** Error, steps, screenshots/logs and environment

Debuggable.

### [08 · Parallel Execution (pytest-xdist)](level-2/08-parallel-execution.md)

**Q69.** What does pytest -n auto do?

**Answer:** Runs tests in parallel across CPU cores (pytest-xdist)

Faster suites.

**Q70.** What must parallel tests avoid?

**Answer:** Shared state like the same file, DB rows or ports

Independence.

**Q71.** How share expensive setup safely?

**Answer:** Per-worker fixtures using worker_id

xdist.

**Q72.** What is sharding?

**Answer:** Splitting tests across multiple machines/jobs

CI matrix.

### [09 · Cross-Browser Testing](level-2/09-cross-browser-testing.md)

**Q73.** What does cross-browser testing check?

**Answer:** Behavior on different browsers/versions

Compatibility.

**Q74.** Which services run browsers in the cloud?

**Answer:** BrowserStack, Sauce Labs or Selenium Grid

Grids.

**Q75.** How choose browsers?

**Answer:** From user analytics and risk

Cost-benefit.

**Q76.** What often differs across browsers?

**Answer:** Rendering, timing and unsupported features

Test the risky parts.

### [10 · Project — POM Framework with API Tests](level-2/10-project-pom-framework.md)

**Q77.** What does the POM framework project combine?

**Answer:** Page objects, fixtures, config, reports and parallel runs

Level 2 project.

**Q78.** How keep tests readable?

**Answer:** Intent-revealing methods and no locators in tests

Abstraction.

**Q79.** How handle environments?

**Answer:** Config files/env vars selecting base URLs and credentials

Portability.

**Q80.** What makes it maintainable?

**Answer:** Small page objects, naming conventions and review

Standards.

## Level 3 · Advanced

### [01 · Playwright for Python](level-3/01-playwright.md)

**Q81.** What's an advantage of Playwright?

**Answer:** Auto-waiting, fast, built-in tracing and multiple browsers

Modern tool.

**Q82.** What does the trace viewer show?

**Answer:** Actions, DOM snapshots, network and console for failed tests

Post-mortem.

**Q83.** How isolate tests in Playwright?

**Answer:** A fresh browser context per test

Fast isolation.

**Q84.** What replaces explicit waits?

**Answer:** Auto-wait plus web-first assertions

expect(...).

### [02 · BDD with pytest-bdd / Behave](level-3/02-bdd.md)

**Q85.** What is BDD?

**Answer:** Describing behavior in a shared language (Given/When/Then) that all roles understand

Collaboration.

**Q86.** Which Python library runs Gherkin?

**Answer:** pytest-bdd (or behave)

Step definitions.

**Q87.** What is a bad BDD smell?

**Answer:** Scenarios full of UI details instead of business behavior

Declarative style.

**Q88.** Who writes scenarios?

**Answer:** Business, QA and developers together (three amigos)

Shared understanding.

### [03 · Robot Framework Basics](level-3/03-robot-framework.md)

**Q89.** What is Robot Framework?

**Answer:** A keyword-driven automation framework with readable tables

Extensible.

**Q90.** What are keywords?

**Answer:** Reusable actions made of other keywords or libraries

Abstraction.

**Q91.** When choose Robot?

**Answer:** For teams wanting keyword/readable tests and acceptance testing

Fit.

**Q92.** How extend it?

**Answer:** Custom libraries in Python

Flexible.

### [04 · CI/CD Integration](level-3/04-cicd-integration.md)

**Q93.** What should CI run?

**Answer:** Fast tests on every push and slower suites on a schedule or before release

Feedback speed.

**Q94.** What artifacts to keep?

**Answer:** Reports, logs, screenshots and traces

Debuggability.

**Q95.** How speed CI?

**Answer:** Cache dependencies and parallelize

Efficiency.

**Q96.** What gates a merge?

**Answer:** Green required checks

Quality.

### [05 · Property-Based Testing with Hypothesis](level-3/05-property-based-testing.md)

**Q97.** What does pytest report?

```python
# test_h.py
from hypothesis import given, strategies as st
def reverse(xs): return xs[::-1]
@given(st.lists(st.integers()))
def test_reverse_twice(xs):
    assert reverse(reverse(xs)) == xs
@given(st.lists(st.integers()))
def test_length(xs):
    assert len(reverse(xs)) == len(xs)
@given(st.integers(), st.integers())
def test_add_commutes(a, b):
    assert a + b == b + a
```

**Answer:** ...
3 passed

Properties hold for generated inputs. Verified by running pytest (shown output normalized).

**Q98.** What does Hypothesis do when a property fails?

**Answer:** Shrinks the input to a minimal failing example and reports it

Counterexamples.

**Q99.** What is a property?

**Answer:** A statement that should hold for all valid inputs (e.g. reverse twice is identity)

Beyond examples.

**Q100.** When use property-based tests?

**Answer:** For parsers, serializers and invariants

Good fit.

### [06 · Performance Testing with Locust](level-3/06-performance-testing.md)

**Q101.** What does a load test measure?

**Answer:** Behavior under expected concurrent usage (throughput, latency, errors)

Performance.

**Q102.** Which tool is Python-based for load tests?

**Answer:** Locust

Python scripts.

**Q103.** Which metrics matter?

**Answer:** Percentile latency (p95/p99), error rate and throughput

Tail latency.

**Q104.** What is a common mistake?

**Answer:** Testing a different environment from production

Realism.

### [07 · Mobile Testing with Appium](level-3/07-mobile-testing-appium.md)

**Q105.** What does Appium automate?

**Answer:** Native and hybrid mobile apps on iOS/Android via WebDriver

Mobile.

**Q106.** What do capabilities define?

**Answer:** The device, platform and app under test

Session setup.

**Q107.** What's a mobile-specific challenge?

**Answer:** Device fragmentation and flaky gestures

Use cloud devices.

**Q108.** Which locators are best?

**Answer:** Accessibility IDs

Stable and accessible.

### [08 · Database Testing from Python](level-3/08-database-testing.md)

**Q109.** What does pytest report?

```python
# test_db.py
import sqlite3, pytest
@pytest.fixture
def db():
    c = sqlite3.connect(":memory:")
    c.execute("CREATE TABLE u(id INTEGER PRIMARY KEY, email TEXT UNIQUE NOT NULL)")
    yield c
    c.close()
def test_insert(db):
    db.execute("INSERT INTO u(email) VALUES ('a@x.com')")
    assert db.execute("SELECT count(*) FROM u").fetchone()[0] == 1
def test_unique(db):
    db.execute("INSERT INTO u(email) VALUES ('a@x.com')")
    with pytest.raises(sqlite3.IntegrityError):
        db.execute("INSERT INTO u(email) VALUES ('a@x.com')")
def test_not_null(db):
    with pytest.raises(sqlite3.IntegrityError):
        db.execute("INSERT INTO u(email) VALUES (NULL)")
```

**Answer:** ...
3 passed

In-memory databases give isolated, fast tests. Verified by running pytest (shown output normalized).

**Q110.** What do database tests verify?

**Answer:** Constraints, migrations and queries behave as designed

Data layer.

**Q111.** How isolate DB tests?

**Answer:** Use transactions rolled back after each test or a fresh DB

Clean state.

**Q112.** What should migrations be tested for?

**Answer:** Applying forwards (and rollback) on realistic data

Safety.

### [09 · Flaky Test Diagnosis &amp; Stabilization](level-3/09-flaky-tests.md)

**Q113.** What does pytest report for this order-dependent suite?

```python
# test_flaky.py
state = []
def test_a():
    state.append(1)
    assert state == [1]
def test_b():
    assert state == []
```

**Answer:** .F
1 failed, 1 passed

Shared state makes test_b depend on test_a. Verified by running pytest (shown output normalized).

**Q114.** What causes flaky tests?

**Answer:** Timing, shared state, order dependence and unstable environments

Fix root causes.

**Q115.** What do retries do?

**Answer:** Hide flakiness; use them only with tracking

Short-term.

**Q116.** How find order dependence?

**Answer:** Run with random order (pytest-randomly) and in isolation

Detect.

### [10 · Project — Playwright + BDD in CI](level-3/10-project-playwright-bdd.md)

**Q117.** What does the Playwright BDD project combine?

**Answer:** Gherkin scenarios, Playwright steps, fixtures, reports and CI

Level 3 project.

**Q118.** How structure steps?

**Answer:** Reusable step definitions calling page objects

DRY.

**Q119.** What report helps stakeholders?

**Answer:** Scenario-level pass/fail in readable form

Living documentation.

**Q120.** How keep scenarios maintainable?

**Answer:** Business-language steps and few UI details

Declarative.

## Level 4 · Master

### [01 · Test Architecture at Scale](level-4/01-test-architecture.md)

**Q121.** What does a good test architecture have?

**Answer:** Layers, clear responsibilities, reusable components and fast feedback

Scalable.

**Q122.** How decide what to automate?

**Answer:** Risk, repetition and stability

Value.

**Q123.** What is the cost of bad architecture?

**Answer:** Brittle suites that nobody trusts

Maintenance.

**Q124.** What is a test strategy?

**Answer:** Goals, scope, levels and approaches for testing the product

Direction.

### [02 · Shift-Left &amp; Continuous Testing](level-4/02-shift-left-continuous-testing.md)

**Q125.** What is shift-left?

**Answer:** Testing earlier (requirements, unit, CI) to find defects sooner

Cheaper bugs.

**Q126.** What does continuous testing mean?

**Answer:** Automated tests as part of every pipeline stage

Fast feedback.

**Q127.** Who owns quality?

**Answer:** The whole team

Shared.

**Q128.** What supports shift-left?

**Answer:** Testable design, fast unit tests and early reviews

Culture.

### [03 · Contract Testing (Pact)](level-4/03-contract-testing.md)

**Q129.** What is contract testing?

**Answer:** Verifying that consumers and providers agree on an API contract independently

Pact.

**Q130.** What problem does it solve?

**Answer:** Breaking integrations without slow end-to-end environments

Microservices.

**Q131.** Who defines the contract in consumer-driven contracts?

**Answer:** Consumers state what they need; providers verify they satisfy it

Direction.

**Q132.** Where run contract verification?

**Answer:** In the provider's CI

Gate.

### [04 · Security Testing Basics for QA](level-4/04-security-testing.md)

**Q133.** Which issues does basic security testing look for?

**Answer:** Injection, broken auth, XSS and misconfiguration

OWASP Top 10.

**Q134.** What is SAST vs DAST?

**Answer:** SAST analyzes source code; DAST tests the running app

Complementary.

**Q135.** What tool scans dependencies?

**Answer:** pip-audit/Dependabot

Supply chain.

**Q136.** Who does security testing?

**Answer:** Everyone, with specialists for deep reviews

Shared.

### [05 · Test Metrics &amp; Quality Gates](level-4/05-test-metrics-quality-gates.md)

**Q137.** What is a quality gate?

**Answer:** Criteria that must pass before code proceeds (tests, coverage, security)

Automated.

**Q138.** Why not chase 100% coverage?

**Answer:** Coverage doesn't measure assertion quality; focus on risk

Meaningful tests.

**Q139.** Which metrics help?

**Answer:** Defect escape rate, flakiness and lead time

Outcome-focused.

**Q140.** How avoid metric gaming?

**Answer:** Use them for learning, not individual performance

Healthy.

### [06 · Containerized Test Environments](level-4/06-containerized-environments.md)

**Q141.** Why use containers for test environments?

**Answer:** Reproducible, isolated and disposable environments

Parity.

**Q142.** What does docker compose give tests?

**Answer:** A multi-service environment (app, DB) started on demand

Integration.

**Q143.** What are Testcontainers?

**Answer:** Libraries that start throwaway containers from test code

Real dependencies.

**Q144.** What should containers avoid?

**Answer:** Persisting state between tests

Clean.

### [07 · AI-Assisted Testing](level-4/07-ai-assisted-testing.md)

**Q145.** A good use of AI in testing?

**Answer:** Generating test ideas and boilerplate that humans review

Assist.

**Q146.** A risk?

**Answer:** Plausible but wrong tests that assert nothing meaningful

Review.

**Q147.** What must stay human?

**Answer:** Judgement about risk and what 'correct' means

Responsibility.

**Q148.** How evaluate AI-generated tests?

**Answer:** Run mutation testing or seed bugs to see if they fail

Test the tests.

### [08 · Building an In-House Test Framework](level-4/08-inhouse-framework.md)

**Q149.** When build an in-house framework?

**Answer:** When off-the-shelf tools can't meet needs, built as thin layers over proven libraries

Avoid reinventing.

**Q150.** What should the framework provide?

**Answer:** Conventions, reusable helpers, reporting and docs

Productivity.

**Q151.** What is a risk?

**Answer:** Becoming a bottleneck nobody else understands

Document and share.

**Q152.** How measure success?

**Answer:** Adoption, stability and time to write tests

Outcome.

### [09 · QA Leadership &amp; Strategy](level-4/09-qa-leadership-strategy.md)

**Q153.** What does QA leadership focus on?

**Answer:** Strategy, risk, coaching and enabling quality across teams

Scale.

**Q154.** How build a quality culture?

**Answer:** Shared ownership, fast feedback and learning from escapes

Mindset.

**Q155.** What is a test strategy review for?

**Answer:** Aligning approach with product risk and goals

Governance.

**Q156.** How grow testers?

**Answer:** Coaching, varied challenges and technical depth

Development.

### [10 · Capstone — Production-Grade Framework](level-4/10-capstone-project.md)

**Q157.** What does the capstone combine?

**Answer:** Framework design, CI, reports, quality gates and documentation

Level 4 project.

**Q158.** How prove it works?

**Answer:** Stable CI runs, trend metrics and fewer escaped defects

Evidence.

**Q159.** What documentation helps?

**Answer:** Architecture, conventions and how to debug failures

Onboarding.

**Q160.** What sustains it?

**Answer:** Ownership, flake triage and regular updates

Maintenance.

## Mixed questions across all levels

**Q161.** What does pytest report?

```python
# test_a.py
import pytest
@pytest.mark.parametrize("x,y", [(1, 1), (2, 3), (3, 3)])
def test_eq(x, y):
    assert x == y
```

**Answer:** .F.
1 failed, 2 passed

One test per parameter set. Verified by running pytest (shown output normalized).

**Q162.** What does pytest report?

```python
# test_b.py
import pytest
@pytest.fixture(scope="module")
def shared(): return []
def test_one(shared): shared.append(1); assert shared == [1]
def test_two(shared): assert shared == [1]
```

**Answer:** ..
2 passed

Module-scoped fixtures are shared within a file. Verified by running pytest (shown output normalized).

**Q163.** What does pytest report?

```python
# test_c.py
import pytest
def test_raises_message():
    with pytest.raises(ValueError, match="positive"):
        raise ValueError("qty must be positive")
def test_wrong_exception():
    with pytest.raises(ValueError):
        raise KeyError("x")
```

**Answer:** .F
1 failed, 1 passed

A different exception type propagates and fails the test. Verified by running pytest (shown output normalized).

**Q164.** What does pytest report?

```python
# test_d.py
from unittest.mock import patch
import datetime
def greeting(now=None):
    hour = (now or datetime.datetime.now()).hour
    return "morning" if hour < 12 else "evening"
def test_fixed_time():
    assert greeting(datetime.datetime(2026, 1, 1, 9)) == "morning"
    assert greeting(datetime.datetime(2026, 1, 1, 18)) == "evening"
```

**Answer:** .
1 passed

Injecting the clock makes tests deterministic. Verified by running pytest (shown output normalized).

**Q165.** What does pytest report?

```python
# test_e.py
import pytest
def test_a(): assert True
@pytest.mark.skip(reason="later")
def test_b(): assert False
@pytest.mark.skipif(True, reason="never runs here")
def test_c(): assert False
```

**Answer:** .ss
1 passed, 2 skipped

skip and skipif. Verified by running pytest (shown output normalized).

**Q166.** A test passes alone but fails after another test. Cause?

**Answer:** Shared state or order dependence

Make tests independent.

**Q167.** What does a fixture with yield guarantee?

**Answer:** The code after yield runs as teardown even if the test fails

Cleanup.

**Q168.** What should you mock?

**Answer:** External boundaries like network, clock and filesystem

Not your logic.

**Q169.** What's wrong with asserting a mock was called without checking arguments?

**Answer:** It can pass while the call used the wrong values

assert_called_once_with.

**Q170.** What is the test pyramid?

**Answer:** Many fast unit tests, fewer integration tests, few end-to-end tests

Speed and reliability.

**Q171.** Which Selenium wait is preferred?

**Answer:** Explicit waits on conditions

Reduce flakiness.

**Q172.** What does the Page Object Model improve?

**Answer:** Maintainability: UI changes are fixed in one place

Encapsulation.

**Q173.** A UI test fails only in CI. What do you collect first?

**Answer:** Screenshots, logs and traces from the failing run

Evidence.

**Q174.** When is a retry acceptable?

**Answer:** Temporarily, while tracking and fixing the root cause of flakiness

Don't hide it.

**Q175.** What does Hypothesis add?

**Answer:** Generated inputs and shrinking to minimal failing examples

Properties.

**Q176.** What does contract testing protect?

**Answer:** Integrations between consumers and providers without full end-to-end environments

Pact.

**Q177.** Why not chase 100% coverage?

**Answer:** Coverage doesn't prove assertions are meaningful

Focus on risk.

**Q178.** What belongs in a quality gate?

**Answer:** Tests passing, coverage trend and security scan results

Automated.

**Q179.** How run tests in parallel safely?

**Answer:** Make them independent and isolate shared resources

pytest-xdist.

**Q180.** What does shift-left mean?

**Answer:** Finding defects earlier through reviews, unit tests and CI

Cheaper.

## Practical coding questions

### A parametrized test suite for a shopping cart

Write the pytest suite for the Cart class: a fixture, merging quantities, parametrized rejection of bad input, parametrized discount boundaries, KeyError on removing a missing SKU, a total and one strict xfail that documents an unspecified rounding case. The file runs itself with pytest.main so it can be executed with plain python.

Starter code:

```
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

Expected output:

```text
..........x                                                              [100%]
10 passed, 1 xfailed
```

??? success "Show a solution"

    ```
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
    @pytest.fixture
    def cart():
        c = Cart(); c.add("pen", 2, 250); return c

    def test_subtotal(cart):
        assert cart.subtotal() == 500

    def test_add_merges_quantities(cart):
        cart.add("pen", 3, 250)
        assert cart.lines["pen"][0] == 5 and cart.subtotal() == 1250

    @pytest.mark.parametrize("qty,price", [(0, 100), (-1, 100), (1, -5)])
    def test_add_rejects_bad_input(qty, price):
        with pytest.raises(ValueError):
            Cart().add("x", qty, price)

    @pytest.mark.parametrize("subtotal_cents,expected_discount", [(9_999, 0), (10_000, 1_000), (25_000, 2_500)])
    def test_discount_boundary(subtotal_cents, expected_discount):
        c = Cart(); c.add("big", 1, subtotal_cents)
        assert c.discount() == expected_discount

    def test_remove_missing_sku_raises(cart):
        with pytest.raises(KeyError):
            cart.remove("nope")

    def test_total_after_discount():
        c = Cart(); c.add("a", 4, 3_000)
        assert c.total() == 10_800

    @pytest.mark.xfail(reason="rounding of fractional cents is not specified yet", strict=True)
    def test_known_gap():
        c = Cart(); c.add("a", 1, 10_001)
        assert c.discount() == 1_000.1

    if __name__ == "__main__":
        raise SystemExit(pytest.main([__file__, "-q", "--tb=no", "-rN", "-p", "no:cacheprovider", "-W", "ignore"]))
    ```

    Fixtures give every test fresh state, parametrization turns boundary tables into separate test cases, pytest.raises checks the error path and a strict xfail documents a known gap (it would fail the run if the behavior unexpectedly started working). Verified by running the file with pytest.

### Testing a rate limiter with a fake clock, parametrization and Hypothesis

Write tests for a token-bucket RateLimiter using an injected FakeClock (no real sleeping), a parametrized partial-refill table and two Hypothesis properties (tokens stay in bounds; allowed calls never exceed the budget). Include a test proving the limiter uses the injected clock and not wall time.

Starter code:

```
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

Expected output:

```text
.........                                                                [100%]
9 passed
```

??? success "Show a solution"

    ```
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

    @pytest.mark.parametrize("wait,expected", [(0.4, False), (0.5, True), (10, True)])
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
            assert 0 <= rl.tokens <= rl.capacity

    @given(st.integers(min_value=1, max_value=20), st.integers(min_value=1, max_value=20))
    def test_allowed_never_exceeds_budget(capacity, calls):
        clock = FakeClock(); rl = RateLimiter(capacity, 1, clock)
        assert sum(rl.allow() for _ in range(calls)) == min(capacity, calls)

    def test_uses_injected_clock_not_wall_time(clock):
        rl = RateLimiter(1, 1, clock)
        assert rl.allow()
        time.sleep(0.01)                      # real time passing must not refill the bucket
        assert not rl.allow()

    if __name__ == "__main__":
        raise SystemExit(pytest.main([__file__, "-q", "--tb=no", "-rN", "-p", "no:cacheprovider", "-W", "ignore"]))
    ```

    Injecting the clock makes time-based code deterministic; properties check invariants for many generated inputs; example-based tests pin down boundaries. Verified by running the file with pytest and Hypothesis.

---

More free practice: the [Python Testing Mastery Path](index.md) curriculum, the [Interview Prep Pack](https://learnmasterypath.com/interview-pack/) and the [free resume ATS check](https://learnmasterypath.com/resume/).
