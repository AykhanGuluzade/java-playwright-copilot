# Cucumber Java steps

Thin glue with scenario-scoped PicoContainer injection.

Target: `src/test/java/com/omc/automation/steps/LoginSteps.java`

```java
package com.omc.automation.steps;

import com.omc.automation.assertions.LoginAssertions;
import com.omc.automation.data.UserData;
import com.omc.automation.pages.LoginPage;
import com.omc.automation.support.BrowserSession;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;

public final class LoginSteps {
    private final BrowserSession session;
    private LoginPage login;
    private UserData user;

    public LoginSteps(BrowserSession session) {
        this.session = session;
    }

    @Given("the login page is ready")
    public void loginPageIsReady() {
        login = new LoginPage(session.page());
        login.open();
    }

    @When("I submit the synthetic user")
    public void submitSyntheticUser() {
        user = UserData.synthetic();
        login.submit(user);
    }

    @Then("the submitted user is welcomed")
    public void submittedUserIsWelcomed() {
        new LoginAssertions(login).userIsWelcomed(user.email());
    }
}
```

The Given step creates the Page Object after Before has started BrowserSession. No static Page, undefined `page` variable, direct locators or test assertions appear in the glue.
