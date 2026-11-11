# Audit Logs

The common audit-log vocabulary -- the audit events that record who did what to which resource, and the log streams that export them to a SIEM -- distilled from the APIs that already exist. Cross-cutting: almost every enterprise API keeps an audit log. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Compliance, Security, Identity, Authentication, Governance, Audit, Audit Logging, SIEM, Enterprise Software in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| audit_event | 61 | 53 | action 76%, id 68%, created_at 62%, actor_id 53% | audit-logs 11, auditlogs 10, audit-log 9, audit_logs 7 |

Cohort: 844 providers with harvested OpenAPI, 61 crosswalks. Of the providers exposing a audit_event: 16% create, 90% list, 23% fetch, 5% update, 3% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- An audit event agrees on the action, the actor, an id and when it happened -- who did what, and when -- across 62 providers. The target, the IP address and the outcome sit below core: every audit log records the actor and the act, fewer record what was acted on.
- Log streams to a SIEM are almost never a resource of their own (2 providers); exporting audit logs is configured, not modelled.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The cohort is the security, identity, compliance and governance tags: audit logs are part of the enterprise surface of almost any API, and these tags find the ones that publish them.
- Only audit-specific paths count -- audit logs, audit events, audit trails, activity logs, and events or logs beneath an audit path; a bare `/events` or `/logs` is another context's.
- Audit events are `/audit-events`.
- Duplicates merged: eight listings, including ConductorOne, Oracle Health, Cvent and LSEG.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
