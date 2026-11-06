# Scenario design

Target example: `src/test/resources/features/onboarding.feature` after agreeing real OMC behavior.

```gherkin
@ui @REQ-ONBOARDING-EXAMPLE
Feature: Validate an onboarding request
  Scenario: Reject a request without required client information
    Given an onboarding request is missing required client information
    When the operator submits the request
    Then the request remains unsubmitted
    And the operator is told which client information is required
```

This is a proposed business scenario, not a confirmed OMC rule or an executable part of the reference fixture. Confirm its source requirement, labels and outcomes before implementing corresponding Java glue. Do not invent a UI action for every element merely to increase a coverage count.
