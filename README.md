# ActOS

**The runtime layer for agents that do digital work.**

ActOS turns the web from a human-clicked interface into an agent-executable surface.

It gives AI the missing layer between:

```text
I know what to do.
```

and

```text
It is done.
```

---

## What is ActOS?

ActOS is a supervised Web Agent Runtime for operating real websites, SaaS dashboards, portals and internal tools.

It is not a search engine.  
It is not a browser macro recorder.  
It is not raw screen control.

It is an execution substrate for digital workers:

```text
Natural Language Goal
        ↓
Mission Runtime
        ↓
Browser / API / File / Human Handoff
        ↓
Verified Digital Work
```

---

## Core Ideas

- **Intent over clicks** — agents express what they want to do; the runtime grounds it safely.
- **Structured first** — DOM, accessibility, network and state before pixels.
- **Vision as fallback** — screenshots help when the web stops being semantic.
- **Human in command** — risky actions pause for approval.
- **Every action is evidence** — replayable traces for every mission.
- **Failure is a state** — recover, retry, rollback or hand off.

---

## Architecture

```text
Agent / Planner
      ↓
ActOS Control Plane
  - Mission Orchestrator
  - Policy Engine
  - Human Approval
  - Identity & Profile Manager
      ↓
ActOS Data Plane
  - Browser Session Runtime
  - Observe Layer
  - Action Router
  - Web World Model
  - State Ledger
  - Recovery Engine
  - Trace Store
      ↓
Execution Adapters
  - Playwright / CDP
  - MCP
  - Browser Extension
  - Computer Use
  - APIs
      ↓
The Web
```

---

## Example

```ts
import { ActOS } from "@actos/runtime";

const actos = new ActOS({ apiKey: process.env.ACTOS_API_KEY });

const mission = await actos.missions.create({
  goal: "Export yesterday's failed refund orders and prepare a review table",
  policy: "supervised",
});

const session = await mission.sessions.create({
  profile: "ops-user-a",
  startUrl: "https://admin.example.com/orders",
  isolation: "strict",
});

await session.act({
  intent: "fill",
  target: { role: "textbox", name: "Status" },
  value: "Refund failed",
});

await session.act({
  intent: "click",
  target: { role: "button", name: "Search" },
});

await session.verify({
  expect: { textVisible: "Refund failed" },
});

const trace = await mission.trace.export();
```

---

## Why ActOS?

The future of software is not only apps that humans use.

It is software that agents can operate, under human control, with memory, policy and proof.

ActOS is the operating layer for that future.

```text
Less browsing.
More doing.
```

---

## Status

Concept design / early architecture.

