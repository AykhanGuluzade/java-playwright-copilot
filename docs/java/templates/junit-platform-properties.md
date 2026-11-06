# Runner properties

Select report plugins, sequential baseline execution and one discovery path.

Target: `src/test/resources/junit-platform.properties`

```properties
cucumber.junit-platform.discovery.as-root-engine=false
cucumber.execution.parallel.enabled=false
cucumber.plugin=pretty,json:build/reports/cucumber/cucumber.json,html:build/reports/cucumber/cucumber.html,junit:build/reports/cucumber/cucumber.xml,message:build/reports/cucumber/cucumber.ndjson
```

Cucumber properties must agree with the pinned engine. [The build](gradle-build.md) forwards supported command-line overrides into the test JVM.
