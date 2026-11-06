# Reports, tracing, screenshots and video

The baseline uses Cucumber's declared JSON, HTML, JUnit XML and message plugins. Fresh reports live under `build/reports/cucumber/`; scenario diagnostics live under `build/artifacts/<unique-id>/`. Keep generated artifacts, authentication state, local environment files and transient agent state out of version control.

The supplied session records a BrowserContext trace during the scenario and writes it on failure. This is failure retention, not an impossible promise to begin recording after the failure and recover prior actions. It takes a screenshot before closing a failed scenario's Page and attaches the bytes through Cucumber. Partial setup still receives cleanup. A diagnostics failure does not replace the original test failure; cleanup failure on an otherwise passing scenario fails the run.

```sh
./gradlew showTrace -PtraceFile=/absolute/path/to/trace.zip
```

The task launches the Java Playwright CLI locally. Treat traces, DOM snapshots, screenshots, URLs, request bodies and saved auth state as potentially sensitive. Use approved storage, limited access, retention and redaction. Do not upload artifacts to a public trace viewer or Pages site without authorization.

Optional video requires `Browser.NewContextOptions().setRecordVideoDir(...)` at context creation. Close the context before reading/publishing the saved video, and retain/delete it according to the agreed policy. There is no Java `retainAll` or Node Playwright Test video-mode setting in this sample.

Allure is optional. Choose an actual adapter compatible with the selected Cucumber major and declare it, test its plugin registration and inspect a known-failure attachment. The public sample does not claim an Allure adapter is already installed or invent `allure:generate` scripts. FAST/TURBO mapping is separate from Allure and must preserve original scenario identifiers and statuses.

Build summaries use actual discovered/executed/passed/failed/skipped/pending counts and artifact locations. A report's existence is not evidence that it is fresh, complete, sanitized or successfully published.

Sources: [Java trace viewer](https://playwright.dev/java/docs/trace-viewer), [Java video lifecycle](https://playwright.dev/java/docs/videos), [Cucumber reporting](https://cucumber.io/docs/cucumber/reporting/).

For CLI-assisted work, keep snapshots/command evidence and original failure copies under an ignored `build/agent-evidence/<run-id>/` location. Review [CLI lifecycle](cli-browser.md) and [gate evidence](review-gates.md); a separate reproduction cannot be labelled an attachment to a Java browser already closed by the After hook.
