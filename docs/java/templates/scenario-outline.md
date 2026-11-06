# Scenario Outline design

```gherkin
@REQ-CLIENT-VALIDATION-EXAMPLE
Feature: Validate a client contact
  Scenario Outline: Explain invalid contact information
    Given a proposed client contact email is "<email>"
    When the operator validates the contact
    Then the contact validation result is "<result>"

    Examples:
      | email               | result                  |
      | invalid-address     | Email format is invalid |
      | client@example.test | Contact is valid        |
```

The values are a proposed illustration, not verified application behavior. Confirm the actual domain contract and error wording, then supply matching Java steps. Use data variation only when each row has a meaningful expected result; do not include credentials or empty placeholders that falsely imply a runnable feature.
