---
name: Multitenancy
category: basic/shards
also-known-as: [Shared Infrastructure, Logical Isolation, SaaS Multitenancy]
tags: [isolation, cost-efficiency, saas, logical-separation, shared-resources]
parent: shards
related: [cells, partitions, row-level-security, rbac]
source: https://github.com/denyspoltorak/metapatterns/wiki/Shards
---

## Summary
A single shared instance of the application and its infrastructure serves multiple tenants simultaneously. Isolation between tenants is enforced in the application layer — typically via a tenant ID column in every table and row-level security policies — rather than by physical separation. Tenants share compute, storage, and network resources, maximizing utilization and minimizing per-tenant cost.

## When To Use
- Serving many small-to-medium tenants where dedicated infrastructure per tenant would be prohibitively expensive
- Operational simplicity is valued: deploying one system is cheaper and faster than managing per-tenant stacks
- Tenants have similar usage profiles and workloads, so resource contention is manageable
- Fast tenant onboarding is required — adding a new tenant is a data operation, not an infrastructure provisioning step

## When To Avoid
- Tenants have strong contractual or regulatory requirements for physical data isolation (GDPR, HIPAA, financial data residency)
- A single noisy tenant can exhaust shared resources and degrade all other tenants (noisy-neighbor problem)
- Tenants require customized schema evolution, independent upgrade schedules, or divergent feature sets
- A security breach in the application isolation layer would have unacceptably high blast radius across all tenants

## Pros and Cons

* Good, because infrastructure costs are amortized across all tenants — utilization is much higher than per-tenant stacks
* Good, because operational overhead is minimal — one deployment pipeline, one monitoring configuration, one system to patch
* Good, because onboarding a new tenant is instant and requires no infrastructure provisioning
* Bad, because a misconfigured query or authorization bug can leak one tenant's data to another — logical isolation is weaker than physical
* Bad, because one high-traffic tenant can degrade performance for all others unless explicit throttling and quotas are implemented
* Bad, because schema changes and migrations must be backward-compatible for all tenants simultaneously, slowing evolution

## Evolutions
- **From:** Shards (Multitenancy is the logical extreme — all tenants share one shard, isolated only by application logic)
- **To:** Cells (promote high-value or regulated tenants to dedicated cell stacks), Partitions (add physical data partitioning per tenant to reduce noisy-neighbor impact), or Hybrid Multitenancy (shared pool for small tenants, dedicated cells for enterprise tenants)
