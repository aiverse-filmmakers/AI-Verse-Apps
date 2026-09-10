# AI-Verse Apps

**The AI-native application layer for AI-Verse OS.**

Status: **Founding architecture / research seed**  
Implementation status: **Not started**  
Created: **September 2026**

AI-Verse Apps is intended to let humans and AI agents create, install, operate, evolve, and safely remove permanent applications inside an AI-Verse environment.

The long-term goal is simple:

> **If a user can describe a useful piece of software, AI-Verse should be able to build it into a durable app that becomes part of their operating system.**

This repository exists so that capability does not get buried inside AI-Verse Dashboard, AI-Verse OS, or AI-Verse Skills.

---

## Why this repository exists

During research into modern AI workspaces and agent platforms, Kylon highlighted an important capability that was not yet explicitly represented in the AI-Verse architecture: agents can build applications that remain inside the workspace and become tools the humans and agents continue using.

This is materially different from asking an agent to generate a one-off webpage or a folder of source code.

The target experience is closer to combining ideas from:

- Kylon's built-in Apps and agent-operated workspace model
- Lovable-style natural-language application creation
- Replit-style full application generation and iteration
- Retool-style internal tools and operational interfaces
- AI-Verse's own local-first, modular, source-of-truth architecture

The useful lesson is not to clone any one product. It is to make **applications a first-class extension type of the AI operating system**.

An AI-Verse user should eventually be able to say things such as:

```text
Build me a production-management app.

Build me a CRM for my clients.

Build me a website builder that works the way I like to work.

Build me a content planner that my Content Bot can maintain.

Build me a dashboard for our sales data.
```

The result should not disappear when the conversation ends. It should become an installed, versioned, permissioned AI-Verse App.

---

# North star

> **Turn useful software created by an agent into a durable, safe, installable part of the user's AI operating system.**

AI-Verse Apps should make AI-generated software feel native to AI-Verse rather than like an unrelated website opened in another browser tab.

---

# Role in the wider AI-Verse architecture

AI-Verse Apps is one layer in a modular system. It must not absorb responsibilities that already belong elsewhere.

```text
AI-Verse OS
    -> canonical operating-system structure, workspace boundaries, policy, app registration

AI-Verse Brain
    -> intent, goals, planning, evaluation, deciding what should exist or improve

AI-Verse Memory
    -> durable historical recall

AI-Verse Skills
    -> reusable capabilities agents use to design, code, test, deploy and maintain apps

AI-Verse Multiple Bots
    -> persistent teammates and temporary workers that can build or operate apps

AI-Verse Data
    -> canonical structured records, schemas, relations and events used by apps

AI-Verse Connections
    -> safe access to external APIs, accounts and services

AI-Verse Apps
    -> app definition, lifecycle, SDK, sandbox, versions, permissions and runtime contract

AI-Verse Dashboard
    -> visual host and navigation surface where installed apps can appear
```

The important boundary is:

> **Dashboard displays apps. Apps defines what an app is. OS governs the environment. Skills and Bots build and operate apps. Data owns structured application records. Connections reaches external services.**

---

# What an AI-Verse App should be

An AI-Verse App should be more than a frontend bundle.

A first-class app will likely have a manifest describing its identity and requirements, for example:

```yaml
id: production-manager
name: Production Manager
version: 1.0.0
entrypoint: ui/index.html
scope: workspace
permissions:
  data:
    - productions:read
    - productions:write
  connections:
    - google-drive:read
  capabilities:
    - document.generate
surfaces:
  - dashboard-tab
```

Exact schemas are intentionally not fixed yet. This repository is currently an architectural seed, not an implementation specification.

A mature app contract should be able to describe at least:

- stable app identity
- version
- author/origin
- compatible AI-Verse versions
- UI entrypoints
- workspace or system scope
- required AI-Verse Data schemas
- requested capabilities
- requested Connections
- runtime requirements
- permissions
- background behavior
- app-specific commands
- migration requirements
- health checks
- provenance
- install/update/rollback metadata

---

# The target user experience

## Create from natural language

A user should eventually be able to request an app from Chat, a Bot, or a dedicated Apps builder:

```text
"Build me a client CRM with company, contact, deal value,
status, next action and a dashboard showing pipeline value."
```

AI-Verse can then coordinate something like:

```text
User intent
   |
   v
Brain / planning
   |
   v
Builder Bot or Team Run
   |
   +-- define app requirements
   +-- define structured data schema
   +-- build UI
   +-- bind permitted Skills and Connections
   +-- test
   +-- security / permission review
   |
   v
Draft App
   |
   v
Preview
   |
   v
User approval
   |
   v
Install
```

## Preview before installation

Agent-generated software should never silently become trusted software.

The expected lifecycle is:

```text
idea
 -> generated draft
 -> preview
 -> automated checks
 -> permission review
 -> user approval where required
 -> install
 -> operate
 -> update
 -> rollback if necessary
```

## Permanent Dashboard surface

Installed apps may appear inside AI-Verse Dashboard as first-class tabs or pages:

```text
AI-Verse Dashboard
├── Now
├── Chat
├── Work
├── Bots
├── Brain
├── Apps
│   ├── Production Manager
│   ├── CRM
│   ├── Website Builder
│   └── Content Planner
└── Settings
```

The Dashboard should host or embed the app through a controlled extension contract. It should not copy the app's business logic into Dashboard itself.

---

# A "Lovable of my own" inside AI-Verse

One motivating use case is a permanent AI-native website/app builder.

Instead of repeatedly opening an external builder, a user could install or create an AI-Verse App such as:

```text
Website Studio
```

It could provide:

- prompt-to-site generation
- visual preview
- code view where useful
- page and component management
- image generation through Skills
- copy generation
- deployment adapters
- Git integration through Connections
- reusable brand context from the selected workspace
- persistent project history
- agent collaboration
- versioning and rollback

This would itself be an AI-Verse App built on the same platform available to other applications.

The system should avoid hard-coding "website builder" into Dashboard. The stronger architecture is to build a professional app platform capable of hosting a website builder, CRM, production tracker, analytics tool, or something not yet imagined.

---

# Relationship to AI-Verse Data

AI-Verse Apps should not invent a new database model for every application.

For apps that need operational records, the preferred future relationship is:

```text
AI-Verse App
     |
     v
AI-Verse Data API
     |
     v
canonical structured records
```

Examples:

```text
CRM App
 -> Customers
 -> Companies
 -> Deals
 -> Activities

Production App
 -> Productions
 -> Crew
 -> Locations
 -> Shoot Days
 -> Deliverables
```

AI-Verse Data owns the structured truth. The App owns how that truth is presented and interacted with.

This is deliberately separate from AI-Verse Memory. Memory exists for historical recall and context. Operational application data is a different class of truth.

---

# Relationship to AI-Verse Skills

Skills provide the abilities used to build and operate apps.

Examples might eventually include:

```text
app.scaffold
app.design
app.test
app.audit
app.package
app.migrate
app.publish
ui.generate
data.schema.design
```

Those are capabilities. AI-Verse Apps owns the app lifecycle and contract.

This distinction allows other agents and runtimes to build an AI-Verse App without requiring one specific coding agent.

---

# Relationship to AI-Verse Multiple Bots

Building non-trivial software is an ideal use case for the Multiple Bots coordination layer.

For example:

```text
App Builder Bot
   |
   +-- UI Worker
   +-- Data-model Worker
   +-- Test Worker
   +-- Security Reviewer
   +-- Accessibility Reviewer
   |
   v
verified app version
```

The app platform should not implement its own multi-agent framework. It requests work through the coordination layer.

Persistent Bots may also become app operators. A Content Bot could maintain a Content Planner. A Sales Bot could update a CRM. A Finance Bot could produce reports from a finance app.

---

# Relationship to AI-Verse Connections

Apps may need external systems, but should receive scoped connection handles rather than raw credentials.

Example:

```text
Website Studio
  -> GitHub connection
  -> deployment provider connection
  -> image-generation service

CRM
  -> Gmail
  -> HubSpot
  -> Calendar
```

An app should request declared permissions and only receive the capabilities the current system/workspace/user grants.

---

# Security model

Agent-generated apps must be treated as untrusted until verified.

Future implementation should strongly consider:

- sandboxed app execution
- explicit capability manifests
- least-privilege permissions
- no arbitrary access to the host filesystem
- no direct secret exposure
- scoped AI-Verse Data access
- scoped AI-Verse Connections access
- content-security policy for hosted UI
- outbound-network controls where practical
- dependency and package scanning
- generated-code review gates
- auditability of app-originated mutations
- version pinning
- signed/trusted packages for shared apps
- explicit approval for privilege expansion

An app update must not silently gain new permissions.

---

# Local-first principle

AI-Verse is local-first. Apps should preserve that philosophy whenever practical.

A local app should be able to run against the user's local AI-Verse system without requiring AI-Verse itself to become a hosted SaaS.

Cloud hosting, remote deployment, shared-team deployment and public websites may be supported through adapters, but they should be choices rather than architectural requirements.

---

# Multi-system isolation

If one Dashboard is connected to several separate AI-Verse OS installations, installed apps and app state must remain scoped to their owning system.

```text
System A / App X
```

must not inherit data, provider sessions, permissions, app configuration or Connections from:

```text
System B / App X
```

A similarly named app in two systems represents two isolated installations unless an explicit export/import mechanism is used.

---

# Multi-user future

AI-Verse is currently primarily designed around a local single-user/operator experience, but the app contract should not prevent a future hosted/team version.

A future application may need to understand:

- human identities
- roles
- workspace membership
- app-level permissions
- shared views
- private views
- audit history
- concurrent editing

Those concerns should integrate with the future AI-Verse identity/access layer rather than Apps inventing a separate account system.

---

# Research findings that motivated this layer

The September 2026 research highlighted several useful lessons:

### Kylon

Kylon demonstrates that an AI-native workspace becomes much more powerful when agents can create and operate real applications where the work already happens. Their product combines human/agent collaboration, structured data, apps, workflows and external integrations in the same environment.

Reference: https://kylon.io/

### Lovable / Replit / Retool pattern

Modern builders demonstrate that natural language can move from "help me code" toward "build the working application." The AI-Verse opportunity is to take the next step and make the generated result a governed, permanent extension of the operating system rather than merely an external project.

### AI-Verse-specific opportunity

AI-Verse already separates Brain, Memory, Skills, Bots, Dashboard and canonical OS state. That makes it possible for generated apps to call stable platform contracts instead of becoming mini operating systems themselves.

---

# What this repository should eventually own

AI-Verse Apps should own:

- App manifest specification
- App package format
- lifecycle state machine
- create/install/update/disable/uninstall contracts
- app SDK
- app-to-Dashboard extension protocol
- sandbox/runtime contract
- permission request model
- app health contract
- compatibility model
- migration contract
- versioning and rollback
- app registry format
- import/export packaging
- development/preview mode
- trusted publishing/signing model if an ecosystem is created

---

# What this repository must NOT own

It should not become:

- the AI-Verse operating system
- the canonical Memory store
- the structured-data engine
- a second Bot framework
- a second Skills registry
- an OAuth/token vault
- the Dashboard itself
- a mandatory cloud hosting service
- an unrestricted code-execution backdoor

---

# Possible future repository shape

Illustrative only:

```text
AI-Verse-Apps/
├── packages/
│   ├── manifest/
│   ├── sdk/
│   ├── runtime/
│   ├── sandbox/
│   ├── installer/
│   └── verifier/
├── templates/
├── examples/
├── docs/
└── tests/
```

No implementation is committed by this founding document.

---

# Initial capability milestones

A sensible future progression could be:

1. Define the stable App manifest and lifecycle.
2. Prove one manually authored app can install into AI-Verse and appear in Dashboard.
3. Add scoped AI-Verse Data access.
4. Add scoped Skills and Connections access.
5. Add preview, validation, update and rollback.
6. Add a builder Skill/Bot capable of producing valid apps from natural language.
7. Add professional visual app-building/iteration UX.
8. Add export/import and potentially a trusted app ecosystem.
9. Add multi-user app permissions when the wider AI-Verse platform gains multi-user identity.

The exact implementation phases should be researched before construction begins.

---

# Non-negotiable invariants

1. An App never becomes a second AI-Verse OS.
2. App permissions are explicit and least-privilege.
3. Agent-generated code is not automatically trusted.
4. Apps never receive raw secrets when a scoped connection handle can be used.
5. An App cannot bypass workspace or system isolation.
6. Structured operational data belongs to AI-Verse Data or another explicitly declared canonical source, not hidden app state.
7. Dashboard is the host/presentation surface, not the app's source of truth.
8. Apps can be disabled or removed without corrupting the OS.
9. Updates are versioned and rollbackable.
10. A permission-expanding update requires explicit review.

---

# Final vision

AI-Verse Apps should eventually turn the operating system from a fixed collection of screens into a **self-extensible AI environment**.

The user should not have to wait for the AI-Verse developers to build every tool they need.

If a need is repeatable and software can solve it, the system should eventually be capable of turning that need into a professional, persistent application while preserving AI-Verse's security, modularity, local-first design and source-of-truth rules.

That is the purpose of this repository.
