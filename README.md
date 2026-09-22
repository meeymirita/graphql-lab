# GraphQL Lab — Helpdesk API без REST

![GraphQL](GraphQL.png)

**Статус: ⚪ методичка готова, прохождение впереди.**
**Сложность: высокая.** Нужна пройденная NestJS Lab целиком — декораторы и `reflect-metadata`, provider scopes, Guards и JWT переиспользуются здесь без повторного объяснения, только в новом контексте.

## О чём

Тот же Helpdesk-backend, что в NestJS Lab (тот же Prisma, тот же JWT) — но HTTP-слой контроллеров заменяется на GraphQL-резолверы: over/under-fetching и зачем единый `/graphql`-эндпоинт, code-first типы и резолверы, N+1 на новом уровне и `DataLoader`, Guards через `GqlExecutionContext`, Subscriptions вместо WebSocket Gateway. Домен не меняется специально — чтобы видеть именно то, что меняется при переходе на GraphQL, а не тонуть в новом коде.

## Стек

`@nestjs/graphql` + Apollo Server, code-first (`@ObjectType`/`@Field`/`@Resolver`), `dataloader` для батчинга, тот же Prisma + PostgreSQL и Passport-JWT, что в NestJS Lab. Всё в Docker.

## Формат

Методичка [`GraphQL_Lab_Plan.html`](GraphQL_Lab_Plan.html) — открывается в браузере, прогресс по чекбоксам сохраняется локально.

## Что внутри (5 сессий)

- **Сессия 1** — замер REST (round trips); первый `ObjectType` и `Query`; первая `Mutation`
- **Сессия 2** — `ResolveField` для комментариев; input types и валидация; порядок вызова резолверов
- **Сессия 3** — замер N+1 в резолвере; `DataLoader`: батчинг; `DataLoader` per-request (`Scope.REQUEST`)
- **Сессия 4** — `GqlExecutionContext` и перенос Guards; `CurrentUser`-декоратор; `Subscription ticketUpdated`; auth для subscription
- **Сессия 5** — unit-тест резолвера; e2e через `/graphql`; "Production Hell" — финальный сценарий без подсказок

Разделы 1–7 методички — теория (over/under-fetching в REST, типы/Query/Mutation, резолверы и порядок вызова, N+1 и DataLoader, Guards и контекст в GraphQL, Subscriptions, тестирование резолверов), раздел 8 — пять сессий заданий, разделы 9–12 — чек-лист, глоссарий, вопросы для собеседования, что дальше.

---

Часть сборного репозитория лабораторных работ — [submodule-group-lab](https://github.com/meeymirita/submodule-group-lab).
