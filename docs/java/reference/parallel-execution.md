# Parallel and container execution

Begin sequentially. The sample creates Playwright, Browser, BrowserContext and Page inside the Cucumber Before hook and closes them in After on the same scenario thread. Constructor injection supplies scenario state without statics. The owner-thread check catches accidental cross-thread access.

After confirming data isolation and the lifecycle, opt in with the reference build:

```sh
./gradlew test -Dcucumber.execution.parallel.enabled=true -Dcucumber.execution.parallel.config.strategy=fixed -Dcucumber.execution.parallel.config.fixed.parallelism=2 -Dcucumber.execution.parallel.config.fixed.max-pool-size=2
```

Keep `maxParallelForks=1` initially. Cucumber scenario threads, Gradle test JVM forks and service/container pods are distinct concurrency layers; multiplying all three without a budget can overload the application and workers. Browser reuse must be thread-owned and measured before replacing the simpler lifecycle.

Each scenario needs isolated mutable data or an explicit reservation/cleanup contract. Use scenario/run identifiers for created accounts and artifacts; a fixed demo email is only suitable for the local stateless reference fixture. Do not share authenticated contexts or static Page fields across scenarios.

A container image needs the selected JDK, matching Playwright browser binaries and OS libraries, trusted CA/proxy settings and the actual test entry point. Java dependency and browser revisions must match. Do not assume a Node Playwright image is a complete Java runner.

Assign each scenario to exactly one shard, validate no overlap/omissions, keep shard-specific output directories and aggregate the original statuses. Report queue, image startup and aggregation separately when comparing end-to-end duration. FAST Run Service tag/environment contracts are integration inputs to validate, not APIs invented by the instructions.

Sources: [Java thread ownership](https://playwright.dev/java/docs/multithreading), [Cucumber parallel engine](https://github.com/cucumber/cucumber-jvm/tree/main/cucumber-junit-platform-engine).
