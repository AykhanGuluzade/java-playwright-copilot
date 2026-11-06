# Cucumber JUnit Platform suite

An executable Java suite selecting the feature resources and glue.

Target: `src/test/java/com/omc/automation/runner/RunCucumberTest.java`

```java
package com.omc.automation.runner;

import org.junit.platform.suite.api.ConfigurationParameter;
import org.junit.platform.suite.api.IncludeEngines;
import org.junit.platform.suite.api.SelectPackages;
import org.junit.platform.suite.api.Suite;

import static io.cucumber.junit.platform.engine.Constants.GLUE_PROPERTY_NAME;

@Suite
@IncludeEngines("cucumber")
@SelectPackages("features")
@ConfigurationParameter(key = GLUE_PROPERTY_NAME, value = "com.omc.automation")
public class RunCucumberTest {
}
```

Keep the class/package aligned with Gradle filtering and [runner properties](junit-platform-properties.md). The suite does not launch a Node Playwright Test runner.
