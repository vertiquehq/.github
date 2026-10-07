<!--
SPDX-FileCopyrightText: 2026 Koivisto Capital Oy
SPDX-License-Identifier: EUPL-1.2
-->

# Vertique

**Focus on business logic, not the plumbing under it.**

Vertique is a Vert.x-native Java 21+ framework for building APIs, durable workflows, and
background jobs. Contracts are typed, wiring is checked when you compile, and messages leave in
the same transaction as your data.

[**vertique.dev**](https://vertique.dev) · [hello@vertique.dev](mailto:hello@vertique.dev)

## What you get

- **Explicit and non-blocking.** Built on Vert.x, with no hidden thread-pool magic.
- **Compile-time assembly.** Dagger-based wiring and diagnostics fail the build, not production.
- **Typed service contracts.** Call plain Java interfaces; Vertique handles event-bus dispatch and context propagation.
- **Durable by design.** PostgreSQL-backed workflows, jobs, and transactional inbox/outbox messaging.
- **REST, security, config, observability, Kafka.** Modules that compose around the same core.

## Repositories

| Repository | What it is |
|---|---|
| [**vertique**](https://github.com/vertiquehq/vertique) | The open-core framework. Start here. |
| [**vertique-skills**](https://github.com/vertiquehq/vertique-skills) | Agent skills (Claude Code, Codex, Copilot, Cursor) that answer Vertique questions from the exact module versions your project uses. |

## Get started

Read the docs and quick start at [vertique.dev](https://vertique.dev), or open an issue or discussion in
[vertiquehq/vertique](https://github.com/vertiquehq/vertique).

---

<sub>Open core under the [EUPL-1.2](https://github.com/vertiquehq/vertique/blob/main/LICENSE). Maintained by [Mika Koivisto](https://github.com/mikakoivisto).</sub>
