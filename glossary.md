---
layout: page
title: Glossary
---

# Glossary

## SCMA

The artifact model for explaining systems through structural nodes and documentation artifacts.

SCMA names:

- landscapes
- federations
- enterprises
- systems
- containers
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
- container
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

## Container

A deployable or runtime unit in a system, such as a service, worker, database, web app, mobile app, CLI, or scheduled job.

## Component

A meaningful owned subsystem or implementation unit. Components usually carry responsibilities, interfaces, and internal behavior worth documenting.

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
- qualities

## Context

An artifact that explains why a structural node exists in its environment and what surrounds it.

Context is not the top of the structure graph. A landscape, federation, enterprise, system, container, component, or module can each have context.

## Task

A repo-local record of intended, active, or completed work. RepoSCMA treats task state as part of documentation because it synchronizes planning, code changes, artifacts, commits, and merge requests.
