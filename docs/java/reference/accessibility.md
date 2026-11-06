# Accessibility and locator evidence

Role/name and label locators improve test intent and can expose some accessibility problems. Finding an element with one of those locators does not prove accessibility conformance. A browser snapshot also does not prove business correctness or comprehensive coverage.

If automated accessibility scans are in scope, select and declare a Java-compatible scanner, pin its version, define the rule set/standard, establish a reviewed baseline and assert the returned violations. Do not copy the old JavaScript aXe imports into Java or claim a scanner exists because a Markdown skill names it.

Test keyboard navigation, focus and meaningful labels against explicit requirements where relevant. Keep approved exceptions documented with evidence and an owner. Manual assessment remains necessary for aspects the scanner cannot establish.

Source: [Playwright Java accessibility testing](https://playwright.dev/java/docs/accessibility-testing).
