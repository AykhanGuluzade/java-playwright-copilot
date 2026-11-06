# Java component object

A reusable navigation fragment with scoped locators.

Target: `src/test/java/com/omc/automation/components/NavigationComponent.java`

```java
package com.omc.automation.components;

import com.microsoft.playwright.Locator;
import com.microsoft.playwright.Page;
import com.microsoft.playwright.options.AriaRole;

public final class NavigationComponent {
    private final Locator navigation;

    public NavigationComponent(Page page) {
        navigation = page.getByRole(AriaRole.NAVIGATION);
    }

    public void openSection(String accessibleName) {
        navigation.getByRole(AriaRole.LINK, new Locator.GetByRoleOptions()
            .setName(accessibleName).setExact(true)).click();
    }
}
```

Add components when shared behavior justifies them. Constructor initialization avoids an unassigned Page. Page/component assertions follow the same dedicated-helper policy.
