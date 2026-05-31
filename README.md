# PACT — Persistent Agentic Context Trust

> *MCP defines how agents communicate. PACT verifies whether those communications can be trusted — across time, across handoffs, across systems.*

[![MIT License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![PyPI](https://img.shields.io/pypi/v/pact-protocol?label=pact-protocol)](https://pypi.org/project/pact-protocol/)
[![PyPI](https://img.shields.io/pypi/v/pact-ax-client?label=pact-ax-client)](https://pypi.org/project/pact-ax-client/)

---

## Install

```bash
pip install pact-protocol      # core intent protocol
pip install pact-langchain     # LangChain integration
pip install pact-ax-client     # multi-agent collaboration SDK
```

---

## 30-second quickstart

```python
from pact_ax_client import Agent

agent = Agent("my-agent", base_url="http://localhost:8000")
agent.register_capability("contract_review", description="Reviews NDAs")

decision = agent.route("contract_review")
if decision.routed:
    result = agent.handoff(decision.best_agent, state_data={"doc": "..."})
    agent.remember("contract_review",
                   partner_id=decision.best_agent,
                   outcome="positive")
```

→ Full SDK docs: [neurobloomai/pact-ax-client](https://github.com/neurobloomai/pact-ax-client)  
→ Server + primitives: [neurobloomai/pact-ax](https://github.com/neurobloomai/pact-ax)

---

## The Problem

BigTech built the compute layer. The model layer. The protocol layer.

Nobody built the **trust layer** — not because they forgot, because they assumed it existed.

When an AI agent acts on your behalf — across sessions, across systems, across handoffs — who verifies it's still behaving as authorized? Who catches the drift between what was approved and what is actually happening?

Policy engines catch rule violations. They don't catch **behavioral drift over time.**

That gap is what PACT addresses.

---

## What PACT Is

PACT is **trust infrastructure for AI agent deployments.**

Not a platform. Not an agent framework. Not a competitor to MCP or A2A.

PACT is the layer that sits between agents and the systems they operate on — measuring, recording, and verifying relational continuity over time.

Think TCP/IP moved packets. HTTPS verified the connection could be trusted. MCP moves agent context. **PACT verifies the agent carrying that context is still who it claimed to be — and behaving as authorized.**

---

## Core Concepts

### Relational Intelligence (RI)
The capacity of an agent — or a system of agents — to maintain consistent, authorized behavior across time and context. RI is the engine.

### Relational Quality (RQ)
The measurable output of that capacity. RQ is the currency. It answers: *how trustworthy has this agent demonstrated itself to be, over what conditions, over what duration?*

### PACT as Infrastructure
PACT converts RI into RQ. It is the accounting system that makes trust measurable — not as a moment, but as a track record.

> *Safety is a moment. Trust is duration.*

---

## The Trust Gap PACT Fills

| Layer | What It Does | Who Built It |
|---|---|---|
| Compute | Run models at scale | Cloud providers |
| Model | Reason, generate, act | AI labs |
| Protocol (MCP) | Agent-to-system communication | Anthropic |
| Orchestration (A2A) | Agent-to-agent coordination | Google |
| **Trust (PACT)** | **Verify agent behavior over time** | **NeuroBloom** |

---

## What's Built

PACT-AX is the live entry point — agent collaboration primitives with a REST API and Python SDK:

| Primitive | What it does |
|-----------|-------------|
| **Capabilities** | Register and discover agent skills |
| **Trust** | Persistent, weighted trust scores that evolve from real outcomes |
| **Router** | Route tasks to the best trusted + capable agent |
| **Episodic Memory** | Record and recall past interactions |
| **Handoff / Transfer** | Prepare → send → receive state packets |
| **Dead Letter Queue** | Park failed deliveries for retry with exponential backoff |
| **Consensus** | Weighted-vote decisions across agents |

```bash
pip install pact-ax-client
```

---

## How PACT Trust Works

PACT uses a three-layer trust measurement architecture:

```
StoryKeeper        — Long behavioral baseline. What has this agent consistently been?
Rupture Detection  — Recency-sensitive drift detection. What just changed?
Trust Score        — Weighted synthesis. What does the full pattern say?
```

**StoryKeeper** maintains the long behavioral baseline — the agent's relational history.

**Rupture Detection** flags when recent behavior deviates from that baseline. Recency-sensitive by design — drift that just started is more dangerous than drift that resolved.

**Trust Score** synthesizes both into a queryable, portable signal: this agent's demonstrated trustworthiness, weighted by recency and severity.

---

## Stable Packets

The portable primitive that makes trust transferable.

When an agent moves between systems — session to session, handoff to handoff — its trust state travels with it as a **Stable Packet**: a verified, signed record of behavioral history that any receiving system can verify.

> *Stablecoins made value portable across financial systems. Stable Packets make trust portable across agent systems.*

A Stable Packet is not a credential. It's a track record.

---

## RLP-0: Relational Ledger Protocol

The state primitive underlying PACT. Three-layer design:
- **Semantic layer** — what was intended
- **Protocol layer** — what was communicated
- **Storage layer** — what was recorded and persisted

RLP-0's design philosophy: **serve, not resolve.** It maintains relational tensions rather than collapsing them into false certainty.

→ [neurobloomai/rlp-0](https://github.com/neurobloomai/rlp-0)

---

## What PACT Is Not

- Not an agent framework — PACT doesn't build agents
- Not a policy engine — PACT doesn't write rules
- Not a competitor to MCP — PACT sits on top of MCP
- Not a monitoring dashboard — PACT is infrastructure, not tooling
- Not a product that pivots — PACT is substrate

> *Substrate doesn't pivot.*

---

## The Ecosystem

| Repo | What it is |
|---|---|
| [`pact`](https://github.com/neurobloomai/pact) | This repo — protocol spec and core concepts |
| [`pact-ax`](https://github.com/neurobloomai/pact-ax) | Agent collaboration server (84 REST routes, 743 tests) |
| [`pact-ax-client`](https://github.com/neurobloomai/pact-ax-client) | Python SDK — `pip install pact-ax-client` |
| [`pact-hx`](https://github.com/neurobloomai/pact-hx) | Human experience layer |
| [`pact-demos`](https://github.com/neurobloomai/pact-demos) | Runnable reference implementations |
| [`rlp-0`](https://github.com/neurobloomai/rlp-0) | Relational Ledger Protocol state primitive |

---

## Who This Is For

**Security teams** deploying AI agents: *how do we know if an agent starts behaving outside its authorized boundary?*

**Platform builders** deploying MCP-native architectures: *what does post-deployment accountability look like?*

**Enterprise and GovCon**: *how do we demonstrate our AI systems are behaving as approved — not just at deployment, but over time?*

---

## The Canonical Framing

PACT is to AI agent trust what:
- **TCP/IP** is to packet routing
- **GAAP** is to financial reporting
- **SWIFT** is to value transfer

Invisible substrate. Completing infrastructure. The layer that makes everything built on top of it trustworthy — not by controlling it, but by accounting for it.

---

## Contributing

PACT is open source. The trust layer for AI infrastructure should be community-owned — not vendor-controlled.

If you're working on MCP deployments, multi-agent coordination, or AI governance — we want to hear from you.

**GitHub:** [github.com/neurobloomai](https://github.com/neurobloomai)  
**Email:** [support@neurobloom.ai](mailto:support@neurobloom.ai)

---

## License

MIT — open protocols, community ownership, infrastructure that endures.

*Built by [NeuroBloom AI](https://neurobloom.ai) — the trust layer BigTech assumed existed.*
