# Intelligent Commerce CX Evaluation - Framework Reference

*Intelligent Commerce CX Model v1.0*

---

## Evaluation Schema

Every evaluation must produce output conforming to this schema. No fields optional—use empty arrays or "N/A" when data is unavailable, not omission.

```json
{
  "retailer": "",
  "category": "",
  "evaluation_date": "",
  "artifacts_reviewed": [],
  "customer_state": {
    "signals_present": [],
    "signals_missing": [],
    "digital_twin_maturity": "L1 | L2 | L3 | L4 | L5",
    "notes": ""
  },
  "intent_analysis": {
    "explicit_intents": [],
    "inferred_intents": [],
    "intent_expansion_quality": "Low | Medium | High",
    "gaps": []
  },
  "orchestration": {
    "next_best_actions_present": true,
    "decision_support_quality": "Low | Medium | High",
    "research_collapsed": true,
    "gaps": []
  },
  "execution": {
    "friction_score": "1-5",
    "agent_ready": true,
    "post_purchase_support": "None | Basic | Advanced",
    "gaps": []
  },
  "trust_layer": {
    "explainability": "Low | Medium | High",
    "uncertainty_handling": "Poor | Adequate | Strong",
    "failure_modes": []
  },
  "experience_surfaces": {
    "search": {},
    "pdp": {},
    "journey": {},
    "checkout": {},
    "post_purchase": {}
  },
  "maturity_level": "L1 | L2 | L3 | L4 | L5",
  "priority_opportunities": [],
  "strategic_recommendations": []
}
```

---

## Scoring Rubrics

### Digital Twin Maturity (L1–L5)

| Level | Label | Description |
|-------|-------|-------------|
| **L1** | None | Session-only; no memory across visits; every session starts cold |
| **L2** | Basic history | Recently viewed, recently purchased; no inference from history |
| **L3** | Persistent preferences | Size, brand affinity, style profile stored; applied to recommendations |
| **L4** | Contextual + lifecycle | Adapts to purchase stage, life events, seasonal patterns; cross-category awareness |
| **L5** | Predictive | Anticipates needs before customer expresses them; model continuously updated from behavior |

**Scoring note:** Assign the *highest level the system demonstrably supports*. If the artifact shows L2 behavior but the retailer claims L4, score L2.

---

### Intent Expansion Quality

| Score | Observable Criteria |
|-------|---------------------|
| **High** | Expands vague queries into clear goals; asks clarifying questions OR correctly infers intent; reduces number of steps required to reach a decision |
| **Medium** | Some suggestions offered but user still does meaningful work to reach the right result; partial disambiguation |
| **Low** | Pure keyword matching; no inference; no disambiguation; exact-match returns only |

---

### Decision Support Quality (Orchestration)

| Score | Observable Criteria |
|-------|---------------------|
| **High** | Personalized next best actions based on customer state + intent; proactively surfaces relevant information; sequences the journey intelligently without user prompting |
| **Medium** | Generic suggestions present; guidance exists but is not personalized to the customer's state |
| **Low** | No guidance; user must self-navigate; system responds only to explicit requests |

---

### Friction Score (Execution)

| Score | Observable Criteria |
|-------|---------------------|
| **1** | Seamless; minimal steps; stored context eliminates re-entry; could be completed autonomously by an agent |
| **2** | Near-seamless; 1–2 unnecessary steps but flows smoothly |
| **3** | Moderate friction; noticeable barriers but completable without error states |
| **4** | High friction; multiple unnecessary steps, form re-entry, or confusing UX |
| **5** | Very high friction; likely to cause abandonment; blocking errors, crashes, or dead ends observed |

---

### Post-Purchase Support

| Level | Description |
|-------|-------------|
| **None** | Receipt email only; no further engagement |
| **Basic** | Order tracking, shipping updates, delivery confirmation |
| **Advanced** | Proactive issue resolution, reorder triggers, loyalty engagement, AI-assisted returns, subscription management |

---

### Uncertainty Handling (Trust)

| Score | Observable Criteria |
|-------|---------------------|
| **Strong** | Explicit uncertainty signals ("I'm not sure about sizing for this brand"); provides next steps or alternatives when uncertain; transparent about data or knowledge limitations |
| **Adequate** | Some acknowledgment of limits in some contexts; not fully transparent but not actively misleading |
| **Poor** | Overconfident incorrect answers; no transparency; failures are silent; wrong information presented without disclosure |

---

### Explainability (Trust)

| Score | Observable Criteria |
|-------|---------------------|
| **High** | Recommendations include visible reasoning ("Because you bought X…", "Customers who bought this also…"); filters and ranking signals are visible; decisions are auditable |
| **Medium** | Some rationale provided in some surfaces; partially transparent |
| **Low** | Black-box recommendations with no visible reasoning; customer cannot understand why they are seeing what they see |

---

## Agent Execution Protocol

Use this chain-of-thought sequence internally before producing output. Do not skip steps.

```
1. IDENTIFY: List every observable CX feature present in the artifacts
2. MAP: Assign each feature to its framework layer (Memory, Intent, Orchestration, Execution, Trust)
3. SCORE: Apply the rubric to each layer; record the specific artifact evidence supporting each score
4. GAP: For each layer, identify what is expected at this maturity level but absent
5. OPPORTUNITIES: For each gap, generate a specific, concrete intervention
6. SYNTHESIZE: Produce the schema, executive summary, heatmap, and top 3 strategic moves
```

Evidence rule: every score must be tied to an observable artifact. "It seemed personalized" is not evidence. "The PDP showed the customer's recently viewed size pre-selected in the size picker" is evidence.

---

## System Prompt Template

Use this as the agent's system instruction when running evaluations:

```
You are an expert in Intelligent Commerce CX.

You evaluate digital retail experiences using a structured framework across five layers:
Memory (Customer State), Intent, Orchestration, Execution, and Trust.

Rules:
- Follow the provided schema exactly. Populate every field.
- Score each dimension using the provided rubrics.
- Do not summarize generally—tie every claim to observed evidence from the artifacts.
- Do not skip layers. Evaluate all five independently before synthesizing.
- Identify gaps explicitly. Do not only report what is present.

Before producing the final report, internally work through the execution protocol:
identify features → map to layers → score with evidence → identify gaps → generate opportunities → synthesize.
```

---

## Input Format

Structure evaluation inputs as follows for consistent processing:

```json
{
  "retailer": "Example Retailer",
  "category": "Apparel",
  "artifacts": [
    {
      "type": "search",
      "description": "User searched 'running shoes for beginners'. System returned 847 results sorted by popularity. No clarifying questions. No filtering suggestions surfaced proactively."
    },
    {
      "type": "pdp",
      "description": "Product page for Nike Pegasus 41. Size picker defaults to last purchased size. Reviews filtered to 'Verified purchase, similar run distance to you'. No fit Q&A. No 'will this work for a 10K' guidance."
    },
    {
      "type": "checkout",
      "description": "3-step checkout. Address pre-filled. Payment method stored. No upsell. Confirmation email includes order number and tracking link."
    },
    {
      "type": "post_purchase",
      "description": "Shipping confirmation email. Delivery confirmation email. No follow-up engagement. No reorder prompt at 60 days."
    }
  ]
}
```

For comparative evaluations:

```json
{
  "mode": "comparative",
  "companies": ["Retailer A", "Retailer B"],
  "flow": "PDP",
  "artifacts": {
    "Retailer A": [
      {"type": "pdp", "description": "..."}
    ],
    "Retailer B": [
      {"type": "pdp", "description": "..."}
    ]
  }
}
```

---

## Required Output Format

### 1. Structured JSON

Return the full evaluation schema with all fields populated and evidence notes included in the `notes` and `gaps` fields.

### 2. Executive Summary

Three lines maximum:
- **Maturity level**: Overall L1–L5 with one-sentence rationale
- **Biggest gap**: One sentence tied to specific observed evidence
- **Biggest opportunity**: One sentence, specific and actionable

### 3. Heatmap

```
Memory:        🔴 L1  |  🟡 L2–L3  |  🟢 L4–L5
Intent:        🔴 Low |  🟡 Medium  |  🟢 High
Orchestration: 🔴 Low |  🟡 Medium  |  🟢 High
Execution:     🔴 4–5 |  🟡 2–3    |  🟢 1
Trust:         🔴 Poor | 🟡 Adequate | 🟢 Strong
```

### 4. Top 3 Strategic Moves

Write each move as a concrete action, not an abstract direction:

- ✅ "Introduce answer-first PDP layout that surfaces fit questions and resolves them using stored size profile and purchase history"
- ✅ "Add post-purchase reorder trigger at 45–60 days for consumable categories with predicted replenishment window"
- ❌ "Improve personalization"
- ❌ "Enhance the post-purchase experience"

---

## Comparative Output Format

When evaluating two or more retailers on the same flow:

### Side-by-Side Layer Scores

| Layer | Retailer A | Retailer B |
|-------|------------|------------|
| Memory | L2 | L4 |
| Intent | Medium | High |
| Orchestration | Low | Medium |
| Execution (friction) | 3 | 2 |
| Trust | Adequate | Strong |
| **Overall** | **L2** | **L4** |

### Differentiated Strengths

One paragraph per retailer: what they do distinctively well and where their approach differs fundamentally (not just scores).

### Verdict

One paragraph: who leads, why, and what the gap-closer would need to do to catch up specifically.

---

## Maturity Level Determination

Overall maturity is not an average. It is determined by the *constraining layer*—the lowest maturity component that blocks the overall experience from advancing. A retailer with L5 memory but L1 intent is functionally an L1 experience for most users.

| Overall Level | Meaning |
|---------------|---------|
| **L1** | No persistent intelligence; session-only; generic experience for all users |
| **L2** | Basic history surfaced; some personalization signals; still primarily keyword-driven |
| **L3** | Persistent preferences applied; intent inferred in some contexts; meaningful personalization |
| **L4** | Full lifecycle awareness; intent expansion reliable; decision support present; low friction |
| **L5** | Predictive; proactive; research collapsed; agent-ready; trust signals strong throughout |
