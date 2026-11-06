# Java API helpers

Use Playwright Java's APIRequestContext for setup, teardown or API checks when it fits the project. Keep requests outside page-object UI actions, close the request context, inject base URLs/auth through approved configuration and preserve response status plus meaningful payload assertions.

Add a real JSON parser/schema validator dependency before relying on one. A Java record declaration does not validate an arbitrary JSON body. State the endpoint contract, expected status, relevant fields and error behavior; do not generate a test merely because an endpoint was discovered.

Readiness and response waits should observe actual conditions. Register a response wait around the triggering action when using `page.waitForResponse(predicate, action)`. Do not sleep and hope a response arrived.

Use idempotent setup where possible and explicit cleanup for created records. Synthetic clients/identities must be unique under concurrency. Avoid request/response attachments that expose authorization headers, cookies or regulated payloads. Redacting a few exact field names is not a complete secret-filtering strategy.

Source: [Playwright Java API testing](https://playwright.dev/java/docs/api-testing).
