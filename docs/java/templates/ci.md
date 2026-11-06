# Java CI workflow template

Target: `.github/workflows/java-bdd.yml` after Java runtime migration. The workflow expects the wrapper, reference Gradle tasks and an authorized reachable non-production BASE_URL. Configure the repository variable and network access before enabling it. It does not provision OMC or bypass a private network boundary.

```yaml
name: Java BDD
on:
  pull_request:
  workflow_dispatch:
permissions:
  contents: read
jobs:
  test:
    runs-on: ubuntu-latest
    env:
      BASE_URL: ${{ vars.BASE_URL }}
      HEADLESS: 'true'
      BROWSER: chromium
    steps:
      - uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1 # v7.0.1
      - uses: actions/setup-java@b843ebf9b913146b38da2eaa7aeddf76074ae1ad # v6.1.0
        with:
          distribution: temurin
          java-version: '17'
      - name: Compile Java test code
        run: ./gradlew --no-daemon testClasses
      - name: Install matching Chromium and OS dependencies
        run: ./gradlew --no-daemon playwrightInstall -PwithDeps=true
      - name: Execute Cucumber smoke scenarios
        run: ./gradlew --no-daemon test -Dcucumber.filter.tags=@smoke
      - name: Retain execution evidence
        if: always()
        uses: actions/upload-artifact@cf430e030ddbb5b0abf93d22962f4752f3646cd9 # v7.0.2
        with:
          name: java-bdd-evidence
          path: |
            build/reports/
            build/test-results/
            build/artifacts/
          if-no-files-found: warn
          retention-days: 7
```

Actions use full commit SHAs resolved from the official release tags in SOURCES.md. Review organization approval and update ownership. This is a GitHub.com hosted-runner example; verify action/runtime support before adapting it to GitHub Enterprise Server or self-hosted runners. Review artifact access/retention. The failing test step stays failed; artifact upload does not publish a public site or make the run successful. No dummy web service or invented application startup is included.

The pinned checkout/setup-java actions use Node 24 and require compatible runners (their documented minimum is 2.327.1). The pinned upload-artifact release targets GitHub.com; its v4-and-newer family is not supported on GitHub Enterprise Server. Use your GHES-supported, organization-approved upload action when adapting this example. See the linked official action releases in SOURCES.md.
