# Business-focused feature

A concrete, synthetic example that binds to the supplied Java steps.

Target: `src/test/resources/features/login.feature`

```gherkin
@smoke @REQ-LOGIN-001
Feature: Welcome a submitted user
  Scenario: Display the submitted user's identity
    Given the login page is ready
    When I submit the synthetic user
    Then the submitted user is welcomed
```

The requirement tag is a sample ID. Replace it with a real traceable requirement for application scenarios. This example verifies display of a submitted identity, not a real OMC authentication guarantee.
