<!--
SPDX-FileCopyrightText: 2026 Koivisto Capital Oy
SPDX-License-Identifier: EUPL-1.2
-->

# Vertique

Vertique is a Java 21+ framework for building services on Vert.x: REST APIs, typed service
calls, durable workflows, scheduled jobs, and transactional messaging on one runtime. Dagger
resolves the object graph at compile time, so a missing binding or a malformed contract fails
the build instead of the deployment.

Documentation and a quickstart are at [vertique.dev](https://vertique.dev).

## A service contract

```java
@ServiceContract(namespace = "shop", value = "pricing")
public interface PricingService {

    @Resilient(policy = "pricing")
    @Timeout(2_000)
    @Retry(maxRetries = 2, delayMs = 50)
    @CircuitBreaker(maxFailures = 5)
    Future<Quote> quote(QuoteRequest request);
}
```

The interface is the whole contract. Vertique generates the client and the event-bus wiring,
carries the request context across the call, and enforces the timeout, retries, and breaker.
You write the pricing.

## What it includes

Workflows keep their state in PostgreSQL. A workflow can wait days for an approval, a signal,
or a timer, and it resumes where it stopped after a restart. There is no separate
orchestration cluster to run.

Outgoing messages are written in the same transaction as the business change. A relay retries
delivery, and the inbox drops a message that arrives twice.

Cron and delayed jobs are coordinated across the cluster. A failed job is retried, and one that
keeps failing goes to a dead-letter queue.

The same correlation context follows a request through the API, over the event bus, and into
a workflow that resumes later. Logs, metrics, and traces carry it.

Around that core: JAX-RS APIs, a REST client, request validation, input sanitization,
resilience, caching, JWT security, typed configuration, secret providers, Kafka, WebSocket,
localization, compile-time AOP, and an MCP server. Each is a separate module, so you use the
parts you need and leave the rest out.

## Try it

Vertique 0.2.0 is on Maven Central. With JDK 21 and Maven installed:

```bash
VERTIQUE_VERSION=0.2.0
mvn -B -ntp archetype:generate \
  -DarchetypeGroupId=dev.vertique \
  -DarchetypeArtifactId=vertique-archetype-rest \
  -DarchetypeVersion=$VERTIQUE_VERSION \
  -DgroupId=com.example \
  -DartifactId=rest-app \
  -Dversion=0.1.0-SNAPSHOT \
  -Dpackage=com.example.restapp \
  -DvertiqueVersion=$VERTIQUE_VERSION \
  -DinteractiveMode=false
cd rest-app && mvn -ntp verify
```

That generates a REST application, runs its integration tests against a real instance, and
leaves you with a working `/hello` endpoint. The [quickstart](https://vertique.dev/docs/quickstart/)
walks through it step by step. There are also archetypes for service contracts and for REST
with PostgreSQL.

## Repositories

| | |
|---|---|
| [vertique](https://github.com/vertiquehq/vertique) | The framework: source, examples, issues, and releases. |
| [vertique-skills](https://github.com/vertiquehq/vertique-skills) | Skills for Claude Code, Codex CLI, GitHub Copilot, and Cursor. The skill reads the reference docs shipped inside the jars your build resolves, so its answers match your version, not the newest one. |

## Docs, license, contact

- [Documentation](https://vertique.dev/docs/) and the [module reference](https://vertique.dev/docs/modules/).
  Every published module also carries its own reference inside the jar at
  `META-INF/vertique/module.md`.
- Open source under [EUPL-1.2](https://github.com/vertiquehq/vertique/blob/main/LICENSE).
  [Commercial extensions](https://vertique.dev/docs/extensions/) are available; write to
  [hello@vertique.dev](mailto:hello@vertique.dev).
- Made in Finland by [Mika Koivisto](https://github.com/mikakoivisto).
