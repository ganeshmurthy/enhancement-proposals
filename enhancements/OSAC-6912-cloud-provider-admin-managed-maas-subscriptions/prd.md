# Cloud Provider Admin MaaS Subscription Management

| Field     | Value                                                    |
|-----------|----------------------------------------------------------|
| Author(s) | ganeshmurthy                                             |
| Jira      | https://redhat.atlassian.net/browse/OSAC-6912            |
| Date      | 2026-10-27                                               |
| Milestone | Backlog                                                  |

## Problem Statement

OSAC currently has no provider-managed workflow for Cloud Provider Admins to
define MaaS subscriptions for tenant organizations. As a result, they cannot
use OSAC to connect eligible groups and, when needed, individual users in a
Tenant to existing MaaS models with per-model token rate limits, measured in
tokens per hour and reset hourly. This leaves providers without a consistent
way to grant model access and revoke it through OSAC within five minutes.
[Jira: OSAC-6912] [User]

## In Scope

- Cloud Provider Admins can create, list, view, update, and delete Subscriptions
  through the OSAC UI, API, and CLI. Only Cloud Provider Admins can view or
  manage Subscription objects. [Clarify: R1.Q1] [Clarify: R1.Q4]
- Each Subscription is associated with one OSAC Tenant. A Cloud Provider Admin
  can select already-registered MaaS models and groups and/or individual users
  belonging to that Tenant. Members of selected groups and directly assigned
  users can access the selected models. Groups are the standard assignment path;
  direct user assignment is available for exceptions. [Clarify: R5.Q1]
  [Clarify: R5.Q2] [Clarify: R7.Q1] [Clarify: R8.Q1] [Clarify: R9.Q1]
- Cloud Provider Admins can set a token rate limit for each model, measured in
  tokens per hour and reset hourly. They can also set Subscription priority.
  The associated Tenant is the only required attribution; separate cost-center
  and label attribution are not required. [Clarify: R3.Q1] [User]
  [Clarify: R2.Q3] [Clarify: R7.Q2]
- Cloud Provider Admins can see overall and per-model Pending, Applied, and
  Failed status. Applied means the entitlement is active; failures identify the
  affected model and provide an actionable reason. [Clarify: R1.Q5]
  [Clarify: R2.Q4] [Clarify: R3.Q4]
- Changes that remove a group or model, and Subscription deletion, revoke the
  affected access within five minutes. [User]

## Out of Scope

- Tenant Admin or Tenant User access to view or manage Subscription objects.
- Unlimited model access, inference priority, guardrails, separate cost-center
  or label attribution, and a separate change-history view.
- Creating or deploying MaaS models, or managing their cluster placement.

## User Stories

### Cloud Infrastructure Admin

Not affected by this feature.

### Cloud Provider Admin

- As a Cloud Provider Admin, I want to create a Subscription for an OSAC Tenant
  by selecting existing MaaS models, eligible groups, and, when needed,
  individual Tenant users, and setting a token rate limit in tokens per hour
  for each model, so I can provide controlled access within that Tenant.
  [Jira: OSAC-6912] [Clarify: R5.Q1]
  [Clarify: R5.Q2] [Clarify: R3.Q1] [User] [Clarify: R2.Q3]
  [Clarify: R7.Q1] [Clarify: R8.Q1]
- As a Cloud Provider Admin, I want to see overall and per-model status with
  actionable failure reasons, so I can tell whether a Subscription is active
  and what needs attention. [Clarify: R1.Q5] [Clarify: R2.Q4]
  [Clarify: R3.Q4]
- As a Cloud Provider Admin, I want changes and deletions to revoke affected
  access within five minutes, so removed groups or models do not retain stale
  access. [User]

### Tenant Admin

Not affected by Subscription management. Tenant Admins cannot view or manage
Subscription objects.

### Tenant User

- As a Tenant User who belongs to a group selected for a Subscription or is
  directly assigned to one, I want to access the MaaS models granted to me within
  their hourly token rate limits, so I can use the provider's MaaS offering
  without managing the Subscription. [Clarify: R1.Q1] [Clarify: R5.Q2]
  [Clarify: R6.Q3] [Clarify: R7.Q1] [Clarify: R3.Q1] [Clarify: R9.Q1] [User]

## Dependencies

- **MaaS model catalog:** Selected models must already be registered and
  available before a Cloud Provider Admin can include them in a Subscription.
  [Clarify: R8.Q1]
- **Tenant identity resolution:** OSAC must be able to resolve group membership
  and individually selected user identities within the associated Tenant so
  only intended subjects receive the entitlement. [Clarify: R5.Q2, R6.Q3,
  R7.Q1, R9.Q1]
- **MaaS access enforcement:** The MaaS access path must enforce per-model token
  rate limits that reset hourly and group or direct-user entitlements, report
  status, and revoke access within five minutes. [Jira: OSAC-6912]
  [Clarify: R8.Q1] [Clarify: R9.Q1] [User]

---

## Provenance

Authored: respond @ prd 0.11.5 - 7b2b8de, workspace main @ 2753cc412
Phases: draft, respond, respond, respond

<!-- ai-workflow-provenance:{"schema_version":1,"provenance_kind":"session","workflow":"prd","workflow_version":"0.11.5","ai_workflows":"7b2b8de","source_repo":"2753cc412","source_repo_branch":"main","commits_behind_main":0,"commits_ahead_main":579,"main_ref":"main","phases":["draft","respond","respond","respond"],"authoring_modes":["skill"],"context_changed":false,"origin_untracked":false} -->
