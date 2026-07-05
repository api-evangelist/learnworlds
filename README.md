# LearnWorlds (learnworlds)

LearnWorlds is an online course and learning management (LMS) platform that lets creators, trainers, and businesses build, sell, and run their own branded online schools. Its REST API (v2) exposes the school's core entities - users, courses, enrollments, subscriptions, payments, course progress, tags, bundles, and certificates - plus webhooks for real-time events.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/learnworlds/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/learnworlds/refs/heads/main/apis.yml)

## Access Model (Read This First)

- **Per-school base URL.** The API is served from each school's own subdomain: `https://{school}.learnworlds.com/admin/api/v2`. There is no single global API host - every request targets your academy's domain.
- **OAuth2 client credentials.** You obtain a `client_id` and `client_secret` from the school admin under **Settings → Developers → API**, then exchange them for a bearer access token at `https://{school}.learnworlds.com/admin/api/oauth2/access_token` (`grant_type=client_credentials`).
- **Two things on every request.** Requests carry both the `Authorization: Bearer ACCESS_TOKEN` header and an `Lw-Client` header whose value is your `client_id`.
- **Plan-gated.** API & Webhooks are **not** included on the entry-level plans. Programmatic access requires the **Learning Center** or **High Volume & Corporate** plan. The Starter and Pro Trainer plans do not include API access as a standard feature.
- **Version 2 only.** API v1 is deprecated and no longer supported.
- **No public WebSocket API.** Real-time event delivery is via outbound webhooks (signed with a `Learnworlds-Webhook-Signature` header and retried on failure), not a client-facing WebSocket or SSE stream. See [review.yml](review.yml).

> Note on grounding: LearnWorlds' full API reference is published as a JavaScript-rendered Stoplight portal at [learnworlds.dev](https://www.learnworlds.dev/docs/api), which is not directly machine-readable. The endpoints modeled in `openapi/learnworlds-openapi.yml` are grounded in the public help center, the official developer documentation, and the official API wrapper, and should be reconciled field-by-field against the live reference before production use.

## Tags

- Online Courses
- LMS
- eLearning
- Education
- Course Platform
- Creator Economy

## Timestamps

- **Created:** 2026-07-05
- **Modified:** 2026-07-05

## APIs

### LearnWorlds Users API

Create, read, update, and list school users (students / members), manage their profile fields, and attach or detach tags. Users are the core identity entity that enrollments, progress, and payments are scoped to.

- **Human URL:** [https://www.learnworlds.dev/docs/api](https://www.learnworlds.dev/docs/api)
- **Base URL:** `https://{school}.learnworlds.com/admin/api/v2`

### LearnWorlds Courses API

List the school's courses, retrieve a single course, and read a course's sections and learning units. Courses are the primary sellable product in a LearnWorlds school.

- **Human URL:** [https://www.learnworlds.dev/docs/api](https://www.learnworlds.dev/docs/api)
- **Base URL:** `https://{school}.learnworlds.com/admin/api/v2`

### LearnWorlds Enrollments API

Enroll and unenroll users on products - courses, bundles, and subscriptions - and list a user's current enrollments. Supports recording a price and justification for manual enrollments.

- **Human URL:** [https://www.learnworlds.dev/docs/api](https://www.learnworlds.dev/docs/api)
- **Base URL:** `https://{school}.learnworlds.com/admin/api/v2`

### LearnWorlds Payments API

Read payment transactions and subscriptions for the school. A payment can include multiple products (cart orders and bundle purchases); subscriptions carry status and billing-period detail.

- **Human URL:** [https://www.learnworlds.dev/docs/api](https://www.learnworlds.dev/docs/api)
- **Base URL:** `https://{school}.learnworlds.com/admin/api/v2`

### LearnWorlds Progress API

Read per-user course progress and completion status across the courses a user is enrolled in, for reporting and downstream analytics.

- **Human URL:** [https://www.learnworlds.dev/docs/api](https://www.learnworlds.dev/docs/api)
- **Base URL:** `https://{school}.learnworlds.com/admin/api/v2`

### LearnWorlds Tags API

Attach and detach tags on users to segment audiences for automations, reporting, and targeted access. Tags are a lightweight labeling primitive across the school.

- **Human URL:** [https://www.learnworlds.dev/docs/api](https://www.learnworlds.dev/docs/api)
- **Base URL:** `https://{school}.learnworlds.com/admin/api/v2`

### LearnWorlds Webhooks API

Create, list, and delete webhook subscriptions that POST event payloads (user registration, enrollment, course completion, certificate awarded, payment created, subscription events, tag changes, and more) to a target URL. Payloads are signed with a `Learnworlds-Webhook-Signature` header and retried on failure.

- **Human URL:** [https://www.learnworlds.dev/docs/api/webhooks](https://www.learnworlds.dev/docs/api/webhooks)
- **Base URL:** `https://{school}.learnworlds.com/admin/api/v2`

## Authentication

```
POST https://{school}.learnworlds.com/admin/api/oauth2/access_token
Content-Type: application/x-www-form-urlencoded
Lw-Client: YOUR_CLIENT_ID

client_id=YOUR_CLIENT_ID&client_secret=YOUR_CLIENT_SECRET&grant_type=client_credentials
```

Use the returned `access_token` on every request:

```
GET https://{school}.learnworlds.com/admin/api/v2/users
Authorization: Bearer ACCESS_TOKEN
Lw-Client: YOUR_CLIENT_ID
```

## Rate Limits

LearnWorlds throttles API requests at approximately **30 requests / 10 seconds**. Throttled requests return HTTP 429; clients should back off and retry. See [rate-limits/learnworlds-rate-limits.yml](rate-limits/learnworlds-rate-limits.yml).

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/learnworlds)
- [Website](https://www.learnworlds.com)
- [Documentation](https://www.learnworlds.dev/docs/api)
- [Plans](plans/learnworlds-plans-pricing.yml)
- [Rate Limits](rate-limits/learnworlds-rate-limits.yml)
- [Fin Ops](finops/learnworlds-finops.yml)
- [Blog](https://www.learnworlds.com/blog/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
