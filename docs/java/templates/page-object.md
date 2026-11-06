# Java page object

A concrete example for an authorized fixture with an Email field, Continue button and status region. Adapt that contract to the actual application.

Target: `src/test/java/com/omc/automation/pages/LoginPage.java`

```java
package com.omc.automation.pages;

import com.microsoft.playwright.Locator;
import com.microsoft.playwright.Page;
import com.microsoft.playwright.options.AriaRole;
import com.omc.automation.data.UserData;

public final class LoginPage {
    private final Page page;
    private final Locator email;
    private final Locator submit;
    private final Locator welcome;

    public LoginPage(Page page) {
        this.page = page;
        email = page.getByLabel("Email", new Page.GetByLabelOptions().setExact(true));
        submit = page.getByRole(AriaRole.BUTTON, new Page.GetByRoleOptions()
            .setName("Continue").setExact(true));
        welcome = page.getByRole(AriaRole.STATUS);
    }

    public void open() {
        page.navigate("/login");
    }

    public void submit(UserData user) {
        email.fill(user.email());
        submit.click();
    }

    public Locator welcomeMessage() {
        return welcome;
    }
}
```

Locators initialize in the constructor. Actions do not assert. Use [assertion helpers](assertions.md) for outcomes and [steps](step-definitions.md) for glue.
