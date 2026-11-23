---
title: "Python Testing Cheat Sheet: Quick Reference, Beginner to Advanced"
description: "A free Python Testing cheat sheet: 27 quick-reference tables from every level of the Python Testing Mastery Path, each linked to its full lesson."
---

# Python Testing Cheat Sheet

Quick-reference tables from **27 lessons** of the free Python Testing Mastery Path, in course order from beginner to advanced. Each section links to the full lesson with explanations and runnable examples.

## Level 2 · Intermediate

### [01 · Page Object Model in Python](level-2/01-page-object-model.md)

| Principle | Rule |
|---|---|
| Locators | Live only inside the page object, never in a test |
| Assertions | Live only inside the test, never in the page object |
| Method naming | Name for user intent (`login`, `add_to_cart`), not implementation (`click_button_3`) |
| Return values | `self` for same-page actions, next page object for navigation |
| Shared mechanics | Factor into a `BasePage` |
| Large pages | Split into composable component objects, not one giant class |
| Waits | Belong in the page object (or base page) — a test should never call `time.sleep` or raw `find_element` |

### [02 · Selenium Advanced](level-2/02-selenium-advanced.md)

| Need | API |
|---|---|
| Element in DOM, may be hidden | `EC.presence_of_element_located` |
| Element rendered, about to read it | `EC.visibility_of_element_located` |
| About to click it | `EC.element_to_be_clickable` |
| Anything else | Custom predicate passed to `wait.until` |
| Timeout that names the failure | `wait.until(cond, message="...")` |
| Enter an iframe / leave it | `switch_to.frame(el)` / `switch_to.default_content()` |
| New tab | `switch_to.new_window("tab")`, then `switch_to.window(handle)` |
| Native dialog | `EC.alert_is_present()`, then `.accept()` / `.dismiss()` |
| Hover, drag, modifier keys | `ActionChains(driver)...perform()` |
| Read state JS knows and Selenium doesn't | `driver.execute_script("return ...")` |
| Stale element | Re-find it; never cache across a re-render |

### [03 · API Testing with requests + pytest](level-2/03-api-testing.md)

| Task | Code |
|---|---|
| GET with params | `session.get(url, params={"q": "shoes"}, timeout=10)` |
| POST JSON | `session.post(url, json=payload, timeout=10)` |
| Auth for all requests | `session.headers.update({"Authorization": ...})` |
| Parse body | `response.json()` — after checking the status code |
| Raw body for error messages | `response.text` |
| Fail on 4xx/5xx immediately | `response.raise_for_status()` |
| Response duration | `response.elapsed.total_seconds()` |
| Redirect history | `response.history` |
| Never omit | `timeout=` |

| Status | Means | Typical test |
|---|---|---|
| 200 | OK | Read succeeded, body matches |
| 201 | Created | POST returned the new resource + id |
| 204 | No content | DELETE succeeded, body is empty |
| 400 | Bad request | Malformed payload rejected |
| 401 / 403 | Unauthenticated / forbidden | Token missing vs. token lacks the role |
| 404 | Not found | Unknown id |
| 422 | Validation failed | Well-formed but semantically invalid input |
| 429 | Rate limited | Client backs off rather than hammering |

### [04 · Mocking with unittest.mock](level-2/04-mocking.md)

| Need | Code |
|---|---|
| Replace a name | `patch("module_that_uses_it.name")` |
| Fake a return | `mock.return_value = x` |
| Fake a chained call | `mock.return_value.json.return_value = {...}` |
| Raise an exception | `side_effect=Timeout()` |
| Different result per call | `side_effect=[a, b, c]` |
| Result depends on args | `side_effect=some_function` |
| Signature-safe mock | `patch(..., autospec=True)` |
| Restrict attributes | `Mock(spec=RealClass)` |
| Patch a dict entry | `patch.dict(os.environ, {"ENV": "test"})` |
| Patch an attribute | `patch.object(Client, "send")` |
| Async collaborator | `AsyncMock` |

### [05 · Test Data Management &amp; Factories](level-2/05-test-data-management.md)

| Need | Pattern |
|---|---|
| Two of a thing in one test | Factory fixture yielding a callable |
| Guaranteed-unique field | `factory.Sequence` or a `uuid4()` prefix |
| Realistic values | `factory.Faker("name")`, seeded |
| Related object | `factory.SubFactory(UserFactory)` |
| Derived value | `factory.LazyAttribute(lambda o: f"{o.name}@x.test")` |
| Many at once | `Factory.create_batch(10)` |
| Cleanup | `yield`, then delete in reverse creation order |
| Expensive shared resource | `scope="session"` — connections only, never data |
| Temp files | pytest's built-in `tmp_path` fixture |

### [06 · pytest Plugins &amp; Configuration](level-2/06-pytest-config.md)

| Task | Command / setting |
|---|---|
| Run a marker | `pytest -m smoke` |
| Exclude a marker | `pytest -m "not slow"` |
| Match by name | `pytest -k "login and not admin"` |
| Stop at first failure | `pytest -x` |
| Stop after N failures | `pytest --maxfail=3` |
| Re-run only last failures | `pytest --lf` |
| Failures first, then the rest | `pytest --ff` |
| List tests without running | `pytest --collect-only -q` |
| Show available fixtures | `pytest --fixtures` |
| Show why a fixture ran | `pytest --setup-show` |
| Full traceback / one line | `--tb=long` / `--tb=line` |
| Show print output | `pytest -s` |
| Which config was used | Read the `configfile:` line in the header |

### [07 · Reporting (pytest-html, Allure)](level-2/07-reporting.md)

| Need | Command |
|---|---|
| CI-readable results | `--junitxml=reports/junit.xml` |
| Shareable single file | `--html=r.html --self-contained-html` |
| Allure results | `--alluredir=reports/allure-results` |
| Render Allure | `allure serve reports/allure-results` |
| Coverage report | `--cov=src --cov-report=html` |
| Summary of skips/xfails | `-ra` |
| Compact tracebacks | `--tb=short` |
| Slowest 10 tests | `--durations=10` |
| Attach an image | `pytest_html.extras.image(path)` |
| Allure step | `with allure.step("..."):` |
| Detect failure in teardown | `pytest_runtest_makereport` hook + `report_call` |

### [08 · Parallel Execution (pytest-xdist)](level-2/08-parallel-execution.md)

| Need | Flag |
|---|---|
| N workers | `-n 4` |
| One per CPU | `-n auto` |
| Include hyperthreads | `-n logical` |
| Keep a module together | `--dist loadfile` |
| Keep a class together | `--dist loadscope` |
| Rebalance dynamically | `--dist worksteal` |
| Stop the whole run early | `--maxfail=1` (xdist honours it) |
| Which worker am I? | `worker_id` fixture |
| Re-run failures serially | `pytest --lf` (no `-n`) |
| Find slow tests | `--durations=10` |
| Expose hidden coupling | `pytest -p randomly` |

### [09 · Cross-Browser Testing](level-2/09-cross-browser-testing.md)

| Need | Code |
|---|---|
| Run every browser | `@pytest.fixture(params=["chrome", "firefox"])` |
| Browser from CLI | `pytest_generate_tests` + `--browsers` |
| Run one browser | `pytest -k chrome` |
| Headless Chrome | `options.add_argument("--headless=new")` |
| Headless Firefox | `options.add_argument("--headless")` |
| Fixed viewport | `options.add_argument("--window-size=1440,900")` |
| Remote/Grid | `webdriver.Remote(command_executor=url, options=options)` |
| Grid in Docker | `--shm-size=2g` — not optional |
| Driver binaries | Selenium Manager handles it (Selenium ≥ 4.6) |
| Watch a Grid session | Port 7900, noVNC, password `secret` |
| Speed it up | Combine with `-n` from module 08 |

## Level 3 · Advanced

### [01 · Playwright for Python](level-3/01-playwright.md)

| Selenium | Playwright | Notes |
|---|---|---|
| `webdriver.Chrome()` | `p.chromium.launch()` | Playwright manages the binary itself |
| `driver.find_element(By.ID, "x")` | `page.locator("#x")` | Playwright locator is lazy, re-queries each action |
| `WebDriverWait(...).until(EC.visibility_of_element_located(...))` | `locator.wait_for(state="visible")` | Auto-waiting removes most explicit waits |
| `driver.get_cookie(...)` | `context.cookies()` | Scoped to a context, not global |
| One `driver` per suite (careful cleanup) | One `context` per test (cheap, isolated) | Contexts replace incognito-window tricks |
| `ElementClickInterceptedException` | Timeout naming the blocking element | Better diagnostics out of the box |
| N/A | `page.screenshot(path=...)` | Built-in, no extra library |
| N/A | Trace viewer (`context.tracing`) | Records a full timeline + screenshots per test |

### [02 · BDD with pytest-bdd / Behave](level-3/02-bdd.md)

| Concept | Gherkin | pytest-bdd wiring |
|---|---|---|
| Setup | `Given ...` | `@given("...")` |
| Action | `When ...` | `@when("...")` |
| Assertion | `Then ...` | `@then("...")` |
| Parametrization | `Scenario Outline` + `Examples` | one pytest test per row, auto-IDed |
| Shared state | (implicit) | ordinary pytest fixture, e.g. `context` |
| Placeholder capture | `"{username}"` in step text | `parsers.parse` / `parsers.re` |
| Regrouping steps | `Background:` | steps run before each `Scenario` in the file |
| Run it | — | plain `pytest`, no separate runner |

### [03 · Robot Framework Basics](level-3/03-robot-framework.md)

| pytest | Robot Framework |
|---|---|
| `def test_add(): assert add(2,3)==5` | `Add Two Numbers` test case + `Should Be Equal As Integers` |
| `@pytest.mark.parametrize` | `[Template]` + data rows |
| Python function | Keyword (from a library or `*** Keywords ***`) |
| `pytest.ini` / `conftest.py` | `*** Settings ***`, `__init__.robot` for suite setup |
| Terminal pass/fail + optional HTML plugin | `report.html` + `log.html` generated by default |
| `pytest.raises(ZeroDivisionError)` | `Run Keyword And Expect Error    ZeroDivisionError*    ...` |
| Fixtures (`setup`/`teardown`) | `Suite Setup` / `Test Setup` / `Test Teardown` in `*** Settings ***` |

### [04 · CI/CD Integration](level-3/04-cicd-integration.md)

| Need | Command / config |
|---|---|
| Machine-readable results | `pytest --junitxml=report.xml` |
| Install Playwright in CI | `playwright install --with-deps chromium` |
| Don't swallow the exit code | avoid bare `\| tee`; use `pipefail` or separate steps |
| Cache slow downloads | `actions/cache@v4` on `~/.cache/ms-playwright` |
| Fast subset every push | `pytest -m smoke` |
| Full suite before merge | `pytest -m "not smoke"` on `main` |
| Show results even on failure | `if: always()` on the reporting step |
| Kill hanging tests | `pytest-timeout`, `@pytest.mark.timeout(30)` |

### [05 · Property-Based Testing with Hypothesis](level-3/05-property-based-testing.md)

| Concept | API |
|---|---|
| Generate integers | `st.integers()`, with `min_value`/`max_value` |
| Generate lists | `st.lists(st.integers(), min_size=1)` |
| Generate strings | `st.text()` |
| Pick from a fixed set | `st.sampled_from([...])` |
| Combine strategies | `st.tuples(...)`, `st.dictionaries(...)`, `st.one_of(...)` |
| Pin a known regression | `@example(value)` |
| Control effort | `@settings(max_examples=N, deadline=None)` |
| What Hypothesis does on failure | shrinks to the minimal failing case automatically |
| Good property shapes | round-trip, invariant, comparison to a reference impl |

### [06 · Performance Testing with Locust](level-3/06-performance-testing.md)

| Concept | Locust API |
|---|---|
| A simulated user | `class MyUser(HttpUser):` |
| Time between actions | `wait_time = between(min, max)` |
| An action, weighted | `@task(weight)` |
| Per-user setup (e.g. login) | `def on_start(self):` |
| Make a request | `self.client.get/post(...)` |
| Validate beyond status code | `catch_response=True` + `response.failure(...)` |
| Run without the web UI | `--headless -u N -r RATE --run-time Ns` |
| Machine-readable output | `--csv=prefix` produces `prefix_stats.csv` etc. |
| Distribute load | `--master` / `--worker` |

### [07 · Mobile Testing with Appium](level-3/07-mobile-testing-appium.md)

| Selenium (Level 1) | Appium |
|---|---|
| `webdriver.Chrome()` | `webdriver.Remote("http://localhost:4723", options=...)` |
| `By.ID` | `AppiumBy.ID` (platform resource-id) |
| N/A | `AppiumBy.ACCESSIBILITY_ID` (cross-platform) |
| N/A | `AppiumBy.ANDROID_UIAUTOMATOR` (Android-only DSL) |
| `WebDriverWait` + `EC` | identical API, same import |
| Browser tabs/windows | `driver.contexts` — `NATIVE_APP` vs `WEBVIEW_*` |
| Fresh browser per test | `options.full_reset = True` or `driver.reset()` |
| N/A | disable device animations to reduce transition flakiness |

### [08 · Database Testing from Python](level-3/08-database-testing.md)

| Need | Pattern |
|---|---|
| Fast, disk-free test DB | `sqlite3.connect(":memory:")` |
| Fresh DB per test | function-scoped `conn` fixture, no shared state |
| Verify a constraint fires | `pytest.raises(sqlite3.IntegrityError)` |
| Verify transaction atomicity | assert unrelated fields are unchanged after a failed operation |
| Match production engine exactly | `testcontainers` spinning up real Postgres/MySQL in Docker |
| Avoid false passes from same-connection reads | commit, then read back with a separate connection |
| Avoid cross-test pollution | function-scoped fixtures unless deliberately testing rollback behavior |

### [09 · Flaky Test Diagnosis &amp; Stabilization](level-3/09-flaky-tests.md)

| Symptom | Likely cause | Real fix |
|---|---|---|
| Fails ~sometimes, no code change | timing/threshold assertion | assert an invariant, not a magic number |
| Passes alone, fails in full suite | test order / shared state | function-scoped fixtures; `pytest-randomly` to surface it |
| Fails only in CI, not locally | unmocked network / real external dependency | mock it (Level 2 Module 4) unless it's an intentional integration test |
| Fails only under `-n auto` | shared mutable state across workers | isolate per-test fixtures, unique ports/files/table rows |
| Async assertion right after `.start()` | race condition | join the thread / await properly, never `sleep()`-and-hope |
| "It's flaky, just rerun it" as policy | root cause never investigated | `--reruns` only as a last resort, with a tracked ticket |

## Level 4 · Master

### [01 · Test Architecture at Scale](level-4/01-test-architecture.md)

| Layer | Tests | Speed | Failure tells you |
|---|---|---|---|
| Unit | pure functions, no I/O | ms | exactly which function broke |
| Integration | components wired together, in-process | ~seconds | wiring/contract mismatch between components |
| E2E | full stack, real browser/network | seconds–minutes | something in the whole user flow broke (needs more digging) |
| Enforce the split | `pytest.ini` markers + `testpaths` | — | `-m unit` / `-m e2e` selects a layer |
| Keep suites decoupled | directory-scoped `conftest.py` | — | a layer's fixture change can't break another layer |
| Catch marker typos | `--strict-markers` | — | unregistered markers become collection errors, not warnings |

### [02 · Shift-Left &amp; Continuous Testing](level-4/02-shift-left-continuous-testing.md)

| Goal | Tool / command |
|---|---|
| Fail the build on undertested code | `pytest --cov=app --cov-fail-under=N` |
| Catch issues before commit | `pre-commit install` + `.pre-commit-config.yaml` |
| Fast local iteration | `pytest --lf`, `pytest --ff` |
| Different depth per pipeline stage | fast subset on PR, full suite + gate on `main` |
| Avoid slow hooks getting bypassed | keep pre-commit to unit tests + lint only |
| Avoid coverage-as-vanity-metric | pair with meaningful assertions, not just line execution |
| Complement, don't replace, prod signal | shift-left + production monitoring together |

### [03 · Contract Testing (Pact)](level-4/03-contract-testing.md)

| Concept | Pact-Python API |
|---|---|
| Define consumer/provider names | `Pact("WebConsumer", "UserService")` |
| Describe one interaction | `.upon_receiving(...).given(...).with_request(...).will_respond_with(...)` |
| Run consumer test against a mock | `with pact.serve() as srv: ...` |
| Save the contract | `pact.write_file("./pacts")` |
| Provider replays and checks | `Verifier(...).verify_pacts(...)` |
| Share contracts across teams | Pact Broker (versioned, queryable) |
| What breaks the contract | consumer expectations changing, or provider dropping a used field |
| What contract testing is NOT | a substitute for all E2E/business-logic tests |

### [04 · Security Testing Basics for QA](level-4/04-security-testing.md)

| Technique | Tool | Catches |
|---|---|---|
| Static pattern scan | `bandit` | shell injection, weak crypto, hardcoded secrets, etc. |
| Prove an exploit works | payload + assertion against a live endpoint | confirms the vulnerability is real, not theoretical |
| Prove a fix blocks it | same payload against the fixed endpoint | regression guard, same "red/green" discipline as any bug fix |
| Regression suite for known attack classes | `@pytest.mark.parametrize` over payload lists | catches the well-known variants automatically |
| Document a known gap | an assertion recording current (missing) behavior | tracks debt without silently ignoring it |
| What these don't catch | business-logic authorization bugs, novel payloads | needs dedicated logic-level tests, not just pattern matching |

### [05 · Test Metrics &amp; Quality Gates](level-4/05-test-metrics-quality-gates.md)

| Metric | What it actually tells you | What it misses |
|---|---|---|
| Line/branch coverage | which lines executed | whether the outcome was actually verified |
| Mutation score | whether tests would catch a real logic change | equivalent mutants inflate "gaps"; slow to run |
| Flaky-test rate | trust erosion risk in the suite | doesn't localize *which* test's root cause |
| Defect escape rate | whether testing investment prevents real bugs | lagging indicator, needs incident-to-test tracing |
| Suite runtime (Module 1) | pyramid shape / architecture health | not a correctness signal at all |

### [06 · Containerized Test Environments](level-4/06-containerized-environments.md)

| Need | Tool |
|---|---|
| One real service from inside a test | `testcontainers-python` |
| Multiple services, integration suite | `docker-compose.test.yml` |
| Reproducible test runner itself | `Dockerfile.test` + `docker build`/`run` |
| CI-native lightweight service | GitHub Actions `services:` block |
| Avoid port collisions | let testcontainers pick a random port |
| Avoid container-per-test slowness | session-scoped container, reset data per test |
| Avoid startup races | wait for a real health check / connection, not just "container started" |

### [07 · AI-Assisted Testing](level-4/07-ai-assisted-testing.md)

| Tool/technique | What it's good at | What still needs a human |
|---|---|---|
| Pynguin (search-based) | mechanically finding code-path edge cases | curating which generated cases are meaningful |
| LLM-drafted tests | fast first drafts, boilerplate parametrize tables | verifying expected values against spec, not implementation |
| LLM-explained failures | fast hypothesis generation for a stack trace | confirming the explanation against the actual code |
| Either, for property suggestions (Level 3 Module 5) | surfacing candidate invariants | verifying the invariant is actually true |
| Neither | encoding domain/business rules as edge cases | requires understanding the requirements, not just the code |

### [08 · Building an In-House Test Framework](level-4/08-inhouse-framework.md)

| Building block | Purpose |
|---|---|
| A tagging decorator over `@pytest.mark` | team-specific metadata + registry, without replacing markers |
| A shared client class | one place to add auth/logging/retries for every test |
| `pytest_configure` | register custom markers so `--strict-markers` doesn't reject them |
| `pytest_runtest_makereport` (hookwrapper) | hook into pass/fail reporting for custom notifications |
| `pyproject.toml` + `pytest11` entry point | make the framework a real, versioned, installable pytest plugin |
| When to build one at all | after the same setup pattern repeats across 3+ test files, not before |

### [09 · QA Leadership &amp; Strategy](level-4/09-qa-leadership-strategy.md)

| Decision | Tool from this module |
|---|---|
| Should we automate this test? | `automation_roi` — breakeven point, not gut feeling |
| Which of many candidates first? | `prioritize_automation_candidates` — frequency × savings, discounted by flakiness risk |
| Are we ready for a new testing demand? | `coverage_gaps` — required skills minus current skills |
| Is quality actually healthy? | `quality_status` — explicit thresholds, not a subjective read |
| What to avoid reporting | raw counts with no outcome link (Trap 1) |

---

Go deeper with the full [Python Testing Mastery Path](index.md) curriculum or test yourself with the [interview questions](interview-questions.md).
