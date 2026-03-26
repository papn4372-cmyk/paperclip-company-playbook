# Paperclip Company Playbook

A production-tested framework for running AI agent companies in Paperclip with two-layer verification, quality gates, and anti-drift mechanisms.

## Metadata

- **name:** paperclip-company-playbook
- **version:** 1.0.0
- **license:** MIT
- **author:** [@aronprins](https://x.com/aronprins)
- **repository:** https://github.com/aronprins/paperclip-company-playbook

## Goals

1. **Two-layer verification** — Every deliverable is checked by the agent (self-check) and the CEO (quality gate) before reaching the Founder.
2. **No busywork** — Idle agents with finished deliverables are a success state, not a problem to solve.
3. **Institutional memory** — Anti-patterns tables and feedback loops ensure the same mistake never happens twice.
4. **Quality over speed** — A bad "done" report creates more work than a day of delay.

## Description

This package provides a complete agent company structure with:

- A **CEO agent** configured as a quality gatekeeper with a 12-step heartbeat state machine, identity/soul definition, and full tooling reference.
- A **Worker agent** template with mandatory self-check procedures, role-specific checklists, and anti-pattern tracking.
- **Reusable skills** for quality control, self-checking, and feedback loops that can be attached to any agent.
- **Company-level files** for project inventory tracking and contribution conventions.

Every mechanism exists because its absence caused real failures in production: rework, wasted tokens, frustrated founders, and broken trust.

## Tags

- quality-control
- verification
- agent-management
- paperclip
- playbook
