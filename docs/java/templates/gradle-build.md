# Gradle Java build

The reference pins an explicitly selected public stack. Review internal framework compatibility before adopting it. Materialize both files and generate the wrapper as described in [migration](../../MIGRATION.md).

Target: `settings.gradle`

```groovy
rootProject.name = 'omc-java-playwright-bdd'
```

Target: `build.gradle`

```groovy
import groovy.json.JsonSlurper

plugins {
    id 'java'
}

repositories {
    mavenCentral()
}

java {
    sourceCompatibility = JavaVersion.VERSION_17
    targetCompatibility = JavaVersion.VERSION_17
}

tasks.withType(JavaCompile).configureEach {
    options.release = 17
    options.encoding = 'UTF-8'
}

dependencies {
    testImplementation platform('io.cucumber:cucumber-bom:8.0.4')
    testImplementation platform('org.junit:junit-bom:6.1.3')
    testImplementation 'io.cucumber:cucumber-java'
    testImplementation 'io.cucumber:cucumber-picocontainer'
    testImplementation 'io.cucumber:cucumber-junit-platform-engine'
    testImplementation 'org.junit.platform:junit-platform-suite'
    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
    testRuntimeOnly 'tools.jackson.core:jackson-databind:3.2.4'
    testImplementation 'com.microsoft.playwright:playwright:1.64.0'
}

tasks.named('test', Test) {
    useJUnitPlatform()
    environment 'PLAYWRIGHT_SKIP_BROWSER_DOWNLOAD', '1'
    include '**/RunCucumberTest.class'
    maxParallelForks = 1
    outputs.upToDateWhen { false }
    def forwarded = [
        'cucumber.filter.tags',
        'cucumber.filter.name',
        'cucumber.execution.parallel.enabled',
        'cucumber.execution.parallel.config.strategy',
        'cucumber.execution.parallel.config.fixed.parallelism',
        'cucumber.execution.parallel.config.fixed.max-pool-size'
    ]
    forwarded.each { key ->
        def value = System.getProperty(key)
        if (value != null) {
            systemProperty key, value
        }
    }
    doFirst {
        delete layout.buildDirectory.dir('reports/cucumber')
    }
    finalizedBy 'verifyCucumberExecution'
}

tasks.register('verifyCucumberExecution') {
    group = 'verification'
    description = 'Rejects missing or empty Cucumber execution evidence.'
    doLast {
        def report = layout.buildDirectory.file('reports/cucumber/cucumber.json').get().asFile
        if (!report.isFile()) {
            throw new GradleException('Cucumber JSON report is missing; execution is unverified.')
        }
        def features
        try {
            features = new JsonSlurper().parse(report)
        } catch (RuntimeException error) {
            throw new GradleException('Cucumber execution evidence is invalid; inspect the original test/reporting failure.', error)
        }
        def scenarios = features.collectMany { feature -> feature.elements ?: [] }
            .findAll { element -> element.type == 'scenario' }
        def executed = scenarios.findAll { scenario ->
            (scenario.steps ?: []).any { step -> step.result?.status in ['passed', 'failed'] }
        }
        if (scenarios.isEmpty() || executed.isEmpty()) {
            throw new GradleException('No Cucumber scenarios executed; inspect empty/skipped selections or failing setup hooks.')
        }
        logger.lifecycle("Cucumber evidence: ${executed.size()} executed scenario(s).")
    }
}

tasks.register('playwrightInstall', JavaExec) {
    group = 'verification'
    description = 'Installs Chromium matching the pinned Playwright Java dependency.'
    classpath = sourceSets.test.runtimeClasspath
    mainClass = 'com.microsoft.playwright.CLI'
    args 'install'
    if (providers.gradleProperty('withDeps').getOrElse('false').toBoolean()) {
        args '--with-deps'
    }
    args 'chromium'
}

tasks.register('showTrace', JavaExec) {
    group = 'verification'
    classpath = sourceSets.test.runtimeClasspath
    mainClass = 'com.microsoft.playwright.CLI'
    doFirst {
        def trace = providers.gradleProperty('traceFile').orNull
        if (!trace) {
            throw new GradleException('Provide -PtraceFile=/absolute/path/to/trace.zip')
        }
        args 'show-trace', trace
    }
}
```

The reference uses Java 17-compatible compilation, JUnit Platform, explicit property forwarding and a zero-execution evidence gate. It does not provide a formatter, Allure adapter, audit scanner or internal-service adapter. Add those capabilities through declared and tested tasks when needed.
