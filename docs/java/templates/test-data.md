# Immutable Java test data

A small synthetic data record for the stateless reference fixture.

Target: `src/test/java/com/omc/automation/data/UserData.java`

```java
package com.omc.automation.data;

import java.util.Objects;

public record UserData(String email) {
    public UserData {
        Objects.requireNonNull(email, "email");
        if (email.isBlank()) {
            throw new IllegalArgumentException("email must not be blank");
        }
    }

    public static UserData synthetic() {
        return new UserData("qa-sample@example.invalid");
    }
}
```

The example email does not represent real credentials. Add a run/scenario namespace and provisioning/cleanup for mutable application data; do not reuse a single shared client under parallel execution.
