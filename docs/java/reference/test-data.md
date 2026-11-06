# Scenario data and configuration

Use immutable Java records or small value objects with explicit validation. Keep real credentials in the approved secret mechanism and inject them when needed; never copy credentials from the original demo README into prompts, features or fixtures. Environment variables do not load `.env` by themselves.

[UserData](../templates/test-data.md) is a synthetic example with a reserved `.invalid` email. It does not claim to authenticate a real user. For mutable OMC flows, create deterministic cases with a unique run/scenario namespace, record a non-sensitive replay key and define ownership plus cleanup. Do not invent missing outcomes just to fill a Scenario Outline.

Read shared state through scenario-scoped injection. Do not use static mutable maps for data, sessions or pages. A factory can be pure while a separate provisioning service creates and cleans external resources. Those responsibilities should be named and tested rather than hidden inside a fixture getter.

Validate base URLs, browser selections and required configuration. Require an authorized environment; do not default to a production endpoint. Preserve enterprise TLS validation and proxy/CA configuration. No `ignoreHTTPSErrors` workaround is part of the reference.

Log enough for replay while excluding secrets, client documents and regulated data. Treat environment names, screenshots and network traces according to actual organization requirements rather than claiming generic compliance.
