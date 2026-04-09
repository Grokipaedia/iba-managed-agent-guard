# iba-platform-guard

> **Every managed agent platform provides the harness. None of them provide the gate.**

---

## The Universal Gap

The world's largest technology companies have built managed agent platforms.

| Platform | Provider | Harness | Infrastructure | Sandboxing | Authentication | Pre-execution Authorization Gate |
|----------|----------|---------|---------------|------------|----------------|----------------------------------|
| Bedrock Agents | AWS | ✅ | ✅ | ✅ | ✅ | ❌ |
| Vertex AI Agents | Google | ✅ | ✅ | ✅ | ✅ | ❌ |
| Azure AI Agents | Microsoft | ✅ | ✅ | ✅ | ✅ | ❌ |
| Agentforce | Salesforce | ✅ | ✅ | ✅ | ✅ | ❌ |
| Claude Managed Agents | Anthropic | ✅ | ✅ | ✅ | ✅ | ❌ |

Every platform confirms who the agent is.  
Every platform limits where it runs.  
Every platform keeps it alive.

**None of them declare what the agent is permitted to do, to whom, up to what limit, under what declared human intent — before it acts.**

Authentication is identity.  
Sandboxing is containment.  
Infrastructure is availability.

**None of these is authorization.**

The pre-execution authorization gate is missing from every managed agent platform on the market.

---

## The Scale of the Gap

- Rakuten shipped to **one billion users** in 5 days on Claude Managed Agents — no signed intent certificate
- AWS Bedrock serves **hundreds of thousands** of enterprise deployments — no pre-execution authorization primitive
- Salesforce Agentforce is **live in production** across Fortune 500 companies — no declared human intent before execution
- Google Vertex AI Agents powers **60+ AP2 protocol partners** including Mastercard, Coinbase, Stripe — no authorization gate beneath the payment rail

Every agent on every platform operates without a cryptographic boundary declared before execution begins.

---

## The Public Admission

On April 8, 2026, Anthropic publicly stated that Mythos Preview will not release because they need:

> *"safeguards that reliably block their most dangerous outputs"*

**Reliably** means outside the model.  
Outside the prompt.  
Outside the harness.  
Outside the platform.

The same gap exists on every platform. Anthropic is the first to say it publicly.

On March 21, 2026, four independent AI systems reached the same conclusion unprompted:

> *"IBA is the missing control plane for agentic AI."*  
> — ChatGPT (OpenAI)

> *"IBA is becoming the baseline security requirement for autonomous AI systems."*  
> — Meta AI

> *"Safe scaling demands IBA first."*  
> — Grok (xAI)

---

## The IBA Layer

IBA Intent Bound Authorization adds the missing primitive beneath every managed agent platform.

```
┌─────────────────────────────────────────────────┐
│                HUMAN PRINCIPAL                  │
│   Signs intent certificate before               │
│   agent connects to any platform                │
└───────────────────────┬─────────────────────────┘
                        │  Signed Intent Certificate
                        │  · Declared scope
                        │  · Hard action / spend limits
                        │  · Authorized targets
                        │  · Kill threshold
                        │  · Expiry
                        ▼
┌─────────────────────────────────────────────────┐
│           IBA PRE-EXECUTION GATE                │
│   Validates certificate before agent            │
│   touches any resource on any platform          │
│                                                 │
│   No cert = No execution                        │
└───────────────────────┬─────────────────────────┘
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
   ┌────────────┐ ┌──────────┐ ┌──────────────┐
   │  Bedrock   │ │  Vertex  │ │    Azure     │
   │  Agents    │ │  Agents  │ │  AI Agents   │
   └────────────┘ └──────────┘ └──────────────┘
          ▼             ▼             ▼
   ┌────────────┐ ┌──────────────────────────┐
   │Agentforce  │ │  Claude Managed Agents   │
   └────────────┘ └──────────────────────────┘
```

**The platform runs the agent.**  
**IBA Intent Bound Authorization governs the platform.**

---

## How It Works

### 1. Human principal signs the certificate — before connecting to any platform
```json
{
  "intent": "Research competitor pricing and compile report",
  "scope": ["web_search", "file_write"],
  "forbidden": ["email_send", "payment", "code_execute"],
  "limits": {
    "duration_minutes": 60,
    "max_files_written": 5,
    "kill_threshold": "any_payment_attempt"
  },
  "principal": "jeffrey@example.com",
  "issued": "2026-04-09T06:00:00Z",
  "expires": "2026-04-09T07:00:00Z",
  "signature": "ed25519:..."
}
```

### 2. IBA gate validates before the agent touches any platform resource
```
Certificate valid?          → PROCEED
Certificate expired?        → BLOCK
Action outside scope?       → BLOCK
Limit exceeded?             → BLOCK
Kill threshold triggered?   → TERMINATE + LOG
No certificate present?     → BLOCK
```

### 3. Agent operates within declared bounds on any platform
Bedrock, Vertex, Azure, Agentforce, Claude Managed Agents — the platform runs normally inside the envelope the human declared before execution began.

### 4. WitnessBound records every gate decision
Every PROCEED. Every BLOCK. Every TERMINATE.  
Immutable. Tamper-evident. Physics-grounded audit chain.  
Platform-agnostic. One record across all platforms.

---

## Multi-Agent: Shard Token Delegation

For swarm deployments across any managed agent platform — master agent delegates to sub-agents via shard tokens.

```
Master Certificate (Human signed)
    │
    ├── Shard: ResearchAgent  →  Bedrock
    │     scope: [web_search, file_read]
    │     limit: 30 minutes
    │
    ├── Shard: WriterAgent    →  Vertex AI
    │     scope: [file_write]
    │     limit: 20 minutes, max 3 files
    │
    └── Shard: ReviewAgent   →  Claude Managed Agents
          scope: [file_read]
          limit: 10 minutes, read-only
```

**No shard can exceed the parent certificate.**  
**No sub-agent operates without delegated authorization.**  
**No trust in the sub-agent. Just enforced bounds.**  
**Platform choice is irrelevant. The gate is upstream of all of them.**

---

## The Payment Rail Problem

Every major agentic payment rail launched in 2026 with the same gap:

| Rail | Provider | Launch | Authorization Gate |
|------|----------|--------|-------------------|
| x402 Foundation | Linux Foundation + 22 members | Apr 2, 2026 | ❌ |
| Agent Payments Protocol (AP2) | Google + 60+ partners | 2026 | ❌ |
| CDP CLI + MCP Server | Coinbase | Apr 9, 2026 | ❌ |
| Intelligent Commerce Connect | Visa | Apr 9, 2026 | ❌ |
| Verifiable Intent | Mastercard | Mar 2026 | ❌ |

Every rail governs payment mechanics.  
None governs what the agent is permitted to pay, to whom, up to what limit, under what declared human intent.

IBA is the missing enforcement primitive beneath all of them.

---

## Live Demos

**ibacore.com/swarm-html/**  
Five-agent swarm across multiple platforms. Shard token delegation. Live tree canvas. Six violation scenarios.

**ibacore.com/desktopwars-html/**  
Three desktop agents — governed simultaneously under one IBA gate. Ungoverned vs. governed side by side.

**aipayhq.com/triple-html/**  
MCP + x402 + IBA — the complete agentic payment stack with the authorization gate added.

**aipayhq.com/402-html/**  
Same payment rail. Same attack. Ungoverned pays. IBA-governed blocks.

---

## Independent Validation — 37 Convergence Events

37 independent parties arrived at the same architectural requirement without knowledge of IBA — across 8 domains, 5 countries, 62 days — all post-dating the patent priority date of February 5, 2026.

| Source | Statement | Date |
|--------|-----------|------|
| Grok (xAI) Session 17 | "Mechanical fix for Anthropic's Mythos dilemma" | Apr 8, 2026 |
| Grok (xAI) Session 17 | "Shifts safety from post-hoc alignment to hardware-enforced bounds" | Apr 8, 2026 |
| Grok (xAI) Session 17 | "No trust in the sub-agent, just enforced bounds" | Apr 8, 2026 |
| Grok (xAI) Session 17 | "Sub-1ms shard validation is exactly the scaling win we need for swarms" | Apr 8, 2026 |
| Shadi J. / EYEspAI | "Where invalid actions aren't blocked — they're impossible" | Apr 6, 2026 |
| Gerald G. Johnson | "Enforcement is a design decision" | Apr 4, 2026 |
| Grok (xAI) Session 12 | "External verification > internal promises" | Mar 24, 2026 |
| Grok (xAI) Session 12 | "Worth prototyping on xAI side too" | Mar 24, 2026 |
| ChatGPT (OpenAI) | "IBA is the missing control plane for agentic AI" | Mar 21, 2026 |
| Meta AI | "IBA is becoming the baseline security requirement" | Mar 21, 2026 |
| Better Identity Coalition | "Cryptographically bind the agent to the human who granted authority" | Mar 9, 2026 |
| Google DeepMind | arXiv:2602.11865 — independent architectural convergence | Feb 12, 2026 |

---

## Patent & Standards Record

```
Patent:   GB2603013.0 (Pending) · UK IPO · Filed February 5, 2026
PCT:      150+ countries · Protected until August 2028
IETF:     draft-williams-intent-token-00 · CONFIRMED LIVE
          datatracker.ietf.org/doc/draft-williams-intent-token/
NIST:     13 filings
NCCoE:    10 filings · AI Agent Identity & Authorization
          Most complete single-framework submission in 319 entries
```

IBA priority date: **February 5, 2026**  
Every platform, rail, and framework in this document: **post-February 5, 2026**

---

## Related Repos

| Repo | Gap closed |
|------|-----------|
| [glasswing-iba-guard](https://github.com/Grokipaedia/glasswing-iba-guard) | Govern the patch. Not just find the bug. |
| [iba-code-guard](https://github.com/Grokipaedia/iba-code-guard) | They got the commit. They didn't get the cert. |
| [iba-swarm-demo](https://github.com/Grokipaedia/iba-swarm-demo) | Five-agent swarm. Shard token delegation. |
| [iba-skill-guard](https://github.com/Grokipaedia/iba-skill-guard) | Govern the skill before it executes. |
| [iba-seo-guard](https://github.com/Grokipaedia/iba-seo-guard) | Zero hallucinations. Not zero humans. |

---

## Acquisition Enquiries

IBA Intent Bound Authorization is available for acquisition.

Every managed agent platform on this page needs this layer.  
One patent. One IETF draft. One priority date.  
February 5, 2026.

**Jeffrey Williams**  
IBA@intentbound.com  
IntentBound.com  
Patent GB2603013.0 Pending · IETF draft-williams-intent-token-00
