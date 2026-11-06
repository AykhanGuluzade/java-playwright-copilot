# Java assertion helper

Business verification for the reference page.

Target: `src/test/java/com/omc/automation/assertions/LoginAssertions.java`

```java
package com.omc.automation.assertions;

import com.omc.automation.pages.LoginPage;

import static com.microsoft.playwright.assertions.PlaywrightAssertions.assertThat;

public final class LoginAssertions {
    private final LoginPage login;

    public LoginAssertions(LoginPage login) {
        this.login = login;
    }

    public void userIsWelcomed(String email) {
        assertThat(login.welcomeMessage()).hasText("Welcome " + email);
    }
}
```

The retrying locator assertion observes the expected UI result. Do not replace it with a one-time `isVisible()` boolean or a check unrelated to the requirement.
