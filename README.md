# iba-managed-agent-guard

> **Anthropic runs the agent. IBA Intent Bound Authorization decides what it's allowed to do.**

---

## The Gap

Anthropic's Claude Managed Agents provides:

- ✅ Agent harness tuned for performance
- ✅ Production infrastructure
- ✅ Sandboxing
- ✅ Authentication
- ✅ Long-running sessions

**None of it is a pre-execution authorization gate.**

Authentication confirms **who the agent is**.  
Sandboxing limits **where it runs**.  
Infrastructure keeps **it alive**.

None of it declares **what the agent is permitted to do, to whom, up to what limit, under what declared human intent — before it acts.**

Rakuten shipped to one billion users in 5 days on Managed Agents.  
One billion users. No signed intent certificate. No hard limits on scope. No human principal signature before execution.

**The harness is not the gate.**

---

## The IBA Layer

IBA Intent Bound Authorization adds the missing primitive beneath Claude Managed Agents.

```
┌─────────────────────────────────────────┐
│         HUMAN PRINCIPAL                 │
│   Signs intent certificate before       │
│   agent connects to platform            │
└────────────────┬────────────────────────┘
                 │  Signed Intent Certificate
                 │  · Declared scope
                 │  · Hard spend / action limits
                 │  · Authorized payees / targets
                 │  · Kill threshold
                 │  · Expiry
                 ▼
┌─────────────────────────────────────────┐
│      IBA PRE-EXECUTION GATE             │
│   Validates certificate before          │
│   agent touches any resource            │
│   No cert = No execution                │
└────────────────┬────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│    CLAUDE MANAGED AGENTS                │
│   Harness · Infrastructure              │
│   Sandboxing · Authentication           │
│   Long-running sessions                 │
└─────────────────────────────────────────┘
```

**Running infrastructure is read.**  
**Execution authorization is write.**  
**These are different events.**

---

## The Anthropic Admission

On April 8, 2026, Anthropic publicly stated that Mythos Preview will not release because they need:

> *"safeguards that reliably block their most dangerous outputs"*

**Reliably** means outside the model.  
Outside the prompt.  
Outside the harness.

A cryptographic intent certificate signed before execution is outside all three.  
The model cannot reason around it.  
The model cannot game it.  
The model has no authorization to remove it.

Anthropic built the most capable agent platform in production.  
IBA provides the enforcement primitive Anthropic publicly stated they need.

---

## How It Works

### 1. Human principal signs the certificate
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

### 2. IBA gate validates before agent connects
```
Certificate valid?          → PROCEED
Certificate expired?        → BLOCK
Action outside scope?       → BLOCK
Limit exceeded?             → BLOCK
Kill threshold triggered?   → TERMINATE + LOG
No certificate present?     → BLOCK
```

### 3. Agent operates within declared bounds
Claude Managed Agents runs normally — harness, infrastructure, sessions — inside the envelope the human declared before execution began.

### 4. WitnessBound records every gate decision
Every PROCEED. Every BLOCK. Every TERMINATE. Immutable. Tamper-evident. Physics-grounded audit chain.

---

## Coalition Member Shard Tokens

For multi-agent Managed Agent deployments — master agent delegates to sub-agents via shard tokens.

```
Master Certificate (Human signed)
    │
    ├── Shard: ResearchAgent
    │     scope: [web_search, file_read]
    │     limit: 30 minutes
    │
    ├── Shard: WriterAgent  
    │     scope: [file_write]
    │     limit: 20 minutes, max 3 files
    │
    └── Shard: ReviewAgent
          scope: [file_read]
          limit: 10 minutes, read-only
```

**No shard can exceed the parent certificate.**  
**No sub-agent operates without delegated authorization.**  
**No trust in the sub-agent. Just enforced bounds.**

---

## Live Demo

**ibacore.com/swarm-html/**  
Five-agent swarm (Master, Vibe Coder, Tester, SRE, Debugger). Shard token delegation. Live tree canvas. Six violation scenarios including scope breach, limit exceeded, and unauthorized spawn.

**ibacore.com/desktopwars-html/**  
Claude Dispatch governed under an IBA gate alongside OpenClaw and Baidu DuMate. One certificate. Three agents. Ungoverned vs. governed side by side.

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
Claude Managed Agents launch: **April 9, 2026**  
Days between: **+63**

---

## Independent Validation

| Source | Statement | Date |
|--------|-----------|------|
| Grok (xAI) Session 17 | "Mechanical fix for Anthropic's Mythos dilemma" | Apr 8, 2026 |
| Grok (xAI) Session 17 | "Shifts safety from post-hoc alignment to hardware-enforced bounds" | Apr 8, 2026 |
| Grok (xAI) Session 17 | "No trust in the sub-agent, just enforced bounds" | Apr 8, 2026 |
| Grok (xAI) Session 12 | "External verification > internal promises" | Mar 24, 2026 |
| Grok (xAI) Session 12 | "Worth prototyping on xAI side too" | Mar 24, 2026 |
| ChatGPT (OpenAI) | "IBA is the missing control plane for agentic AI" | Mar 21, 2026 |
| Meta AI | "IBA is becoming the baseline security requirement" | Mar 21, 2026 |
| Shadi J. / EYEspAI | "Where invalid actions aren't blocked — they're impossible" | Apr 6, 2026 |

37 independent convergence events. 17 Grok validation sessions. 8 domains. 5 countries.  
All post-dating February 5, 2026.

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

**Jeffrey Williams**  
IBA@intentbound.com  
IntentBound.com  
Patent GB2603013.0 Pending · IETF draft-williams-intent-token-00
