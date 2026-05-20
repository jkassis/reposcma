---
layout: page
title: Example System
author: Jeremy Kassis and the RepoSCMA Working Group
---

# Example System: OrderHub

By Jeremy Kassis and the RepoSCMA Working Group.

OrderHub is a fictional order-management system used by retailers to receive web orders, reserve inventory, collect payment authorization, and coordinate fulfillment.

This example shows how SCMA artifacts can describe a structure graph and how RepoSCMA would place those artifacts in a repository.

## Structure Graph

```text
landscape: Retail Commerce
`- federation: Regional Retail Network
   |- enterprise: Northstar Retail
   |  `- system: OrderHub
   |     |- component: web-app (runtime)
   |     |- component: api (runtime)
   |     |- component: worker (runtime)
   |     |- component: orderhub-helm (deployment)
   |     |- component: prod-terraform (deployment)
   |     |- component: checkout (functional)
   |     |  `- module: pricing
   |     |     `- module: promotions
   |     `- component: fulfillment (functional)
   `- enterprise: ShipQuick Logistics
      `- system: Carrier Gateway
```

The OrderHub repo is concerned mostly with the `system: OrderHub` subtree, but its context artifact still needs to mention the federation and partner enterprise because fulfillment depends on them.

The `web-app`, `api`, and `worker` components are runtime components because they have execution lifecycles. They may run in different execution domains, such as a browser, operating system process, language interpreter, container runtime, or managed platform runner; the model cares that they are operated as running units. The `checkout` and `fulfillment` components are functional components because they own behavior that can be composed into runtime components.

## Example Artifacts

### System Summary

OrderHub accepts customer orders from retail channels and coordinates payment, inventory reservation, and fulfillment handoff.

### System Context

OrderHub operates inside the Regional Retail Network federation. Northstar Retail owns OrderHub. ShipQuick Logistics owns the external Carrier Gateway used for shipping labels, pickup windows, and delivery status.

### System Interfaces

- HTTPS API for checkout submission
- webhook receiver for payment authorization updates
- event stream for inventory reservation results
- outbound REST calls to Carrier Gateway

### System Functions

- validate carts
- price orders
- reserve inventory
- authorize payment
- create fulfillment requests
- publish order state changes

### System States

Orders move through `submitted`, `priced`, `reserved`, `payment_authorized`, `fulfillment_requested`, `fulfilled`, and `cancelled` states. Retryable failures keep the order in its current business state while recording operational retry state.

### System Data

OrderHub owns order records, order state history, fulfillment request records, and idempotency keys. It references inventory, payment, and carrier identifiers owned by external systems.

### System Qualities

- checkout submission should remain available during downstream carrier outages
- order state transitions must be auditable
- payment authorization and inventory reservation must be idempotent
- fulfillment handoff should degrade to retryable queueing when ShipQuick is unavailable

### System Decisions

- Use asynchronous fulfillment handoff so carrier outages do not block checkout.
- Keep payment authorization and inventory reservation as separate idempotent steps.

### System Scenarios

- shopper submits a valid order and receives confirmation
- payment authorization succeeds after inventory reservation
- ShipQuick is unavailable during fulfillment handoff
- duplicate checkout submission is received after a client retry

## Diagram Artifact

Artifacts may include diagrams when they help. A diagram is still an artifact attached to a structural node; it is not the structure itself.

```mermaid
flowchart LR
  Shopper[Shopper] --> Web[web-app runtime component]
  Web --> API[api runtime component]
  API --> Checkout[checkout component]
  Checkout --> Inventory[Inventory System]
  Checkout --> Payment[Payment Processor]
  API --> Worker[worker runtime component]
  Worker --> Fulfillment[fulfillment component]
  Fulfillment --> Carrier[ShipQuick Carrier Gateway]
```

## RepoSCMA Placement

One reasonable RepoSCMA layout for this system:

```text
orderhub/
|- README.md
|- docs/
|  |- CONTEXT.md
|  |- INTERFACES.md
|  |- STATES.md
|  |- DATA.md
|  `- QUALITIES.md
|- tasks/
|  |- TODO.md
|  |- IDEAS.md
|  `- DONE.md
|- comps/
|  |- web-app/
|  |  `- README.md
|  |- api/
|  |  `- README.md
|  |- worker/
|  |  `- README.md
|  |- checkout/
|  |  |- README.md
|  |  `- src/
|  |     `- pricing/
|  |        |- README.md
|  |        `- promotions/
|  |           `- README.md
|  |- fulfillment/
|  |  `- README.md
|  |- orderhub-helm/
|  |  `- README.md
|  `- prod-terraform/
|     `- README.md
```

The root README would carry the system summary and high-level navigation. Root `docs/` would hold system-level spillover. Component READMEs would identify the component kind and carry local responsibilities, interfaces, functions, and quality constraints. Runtime components such as `api` would explain execution lifecycle and operational behavior. Deployment components such as `orderhub-helm` and `prod-terraform` would explain release packaging, environment assembly, infrastructure stacks, and reusable infrastructure modules.

## Task Example

```markdown
# TODO

## ORD-014: Make fulfillment handoff retryable

- [ ] Add idempotency key to Carrier Gateway requests
- [ ] Persist retry state in worker queue
- [ ] Document fulfillment outage behavior in `docs/QUALITIES.md`
- [ ] Add integration test for duplicate fulfillment requests
```

This task is not just project management. It is the synchronization point between code, tests, durable quality documentation, and the eventual commit or merge request.
