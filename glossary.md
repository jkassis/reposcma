---
layout: page
title: Glossary
author: Jeremy Kassis and the RepoSCMA Working Group
---

# Glossary

By Jeremy Kassis and the RepoSCMA Working Group.

## SCMA

The artifact model for explaining systems through structural nodes and documentation artifacts.

SCMA names:

- landscapes
- federations
- enterprises
- systems
- components
- modules
- artifacts

## RepoSCMA

The repo documentation model that applies SCMA artifacts to concrete repository layout, README/docs packaging, and task files.

SCMA says what kinds of things can be described. RepoSCMA says where those descriptions should live in a repo.

## Structure Graph

The graph of structural nodes and relationships that matter for understanding a system.

A structure graph can include nodes above the repo boundary, such as landscapes, federations, and enterprises.

## Structural Node

A thing that can own or contain other structural nodes and can be described by artifacts.

Common structural nodes:

- landscape
- federation
- enterprise
- system
- component
- module

## Landscape

The broadest environment under consideration. A landscape may contain federations, independent enterprises, shared infrastructure, markets, regulatory environments, and external systems.

## Federation

A cooperating group of enterprises. A federation may share governance, standards, interfaces, data exchange, identity, operating procedures, or commercial relationships.

## Enterprise

An organization or organizational unit that owns capabilities, systems, people, policies, and operational responsibility.

## System

A coherent product, service, platform, application, or operational capability. In RepoSCMA, a single repository usually maps to a system.

## Component

A meaningful owned system unit. `Unit` is a useful plain-language synonym, but `component` is the canonical SCMA term.

Components usually carry responsibilities, interfaces, and internal behavior worth documenting. Common component kinds include:

- functional component: owns behavior or responsibility and may not be distinctly runnable
- runtime component: has an execution lifecycle in an execution domain
- deployment component: assembles, configures, provisions, or releases other components and supporting resources into an environment
- infrastructure component: owns or defines operational resources or platform capability

Runtime components run in execution domains such as operating system processes, language interpreters, web browsers, mobile operating systems, serverless function runners, WASM hosts, embedded processors, container runtimes, hypervisors, workflow orchestrators, database engines, or plugin hosts. The execution domain matters more than the application category or packaging format. The deciding factor is whether the thing is operated, invoked, scheduled, scaled, monitored, restarted, or failure-isolated as a running unit.

## Module

A code-aligned sub-unit inside a component. Modules may contain child modules when the implementation is naturally nested.

## Artifact

A durable explanation attached to a structural node.

Artifacts can include prose, copy, diagrams, tables, schemas, interface snippets, command examples, runbook excerpts, or mixed-format documents.

Core artifact roles:

- summary
- context
- components
- interfaces
- functions
- states
- data
- qualities
- decisions
- scenarios

## Summary

An artifact that briefly states what a structural node is, who or what it serves, and what success looks like.

## Components

An artifact that explains meaningful internal parts of a structural node. The parts may be structural nodes themselves, such as components or modules.

## Interfaces

An artifact that explains contracts at a boundary: APIs, events, schemas, files, commands, protocols, human procedures, or integration points.

## Functions

An artifact that explains behavior, responsibilities, workflows, transformations, or operational activities.

## States

An artifact that explains lifecycle, modes, state machines, transitions, invariants, and valid or invalid state changes.

State artifacts borrow naturally from UML state machines, workflow modeling, protocol modeling, and operational mode analysis.

## Data

An artifact that explains domain concepts, entities, schemas, ownership, retention, lineage, consistency, or storage responsibilities.

Data artifacts may borrow from ER modeling, OOAD class modeling, DDD aggregates, schema design, and data architecture.

## Qualities

An artifact that explains non-functional concerns such as correctness, latency, reliability, security, operability, cost, maintainability, usability, and compliance.

## Decisions

An artifact that records rationale, tradeoffs, accepted decisions, rejected alternatives, and consequences.

Decision artifacts often map to ADRs, design notes, architecture reviews, or recorded operating decisions.

## Scenarios

An artifact that explains concrete cases used to reason about the structural node.

Scenarios may include use cases, user stories, sequence examples, threat scenarios, failure scenarios, incident drills, or acceptance examples.

## Context

An artifact that explains why a structural node exists in its environment and what surrounds it.

Context is not the top of the structure graph. A landscape, federation, enterprise, system, component, or module can each have context.

## Task

A repo-local record of intended, active, or completed work. RepoSCMA treats task state as part of documentation because it synchronizes planning, code changes, artifacts, commits, and merge requests.

## Modeling Notation

A representation format used inside an artifact, such as UML, BPMN, ER diagrams, C4 views, sequence diagrams, state machines, tables, prose, or runbooks.

In SCMA, notations are rendering choices. Artifact roles define documentation responsibilities.
