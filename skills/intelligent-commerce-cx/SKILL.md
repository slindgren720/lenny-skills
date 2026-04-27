---
name: intelligent-commerce-cx
description: Help users evaluate and improve AI-native retail experiences. Use when someone is auditing a commerce site, scoring a digital shopping journey, assessing AI personalization maturity, benchmarking against the Intelligent Commerce CX Model, or building a roadmap for AI-native retail.
---

# Intelligent Commerce CX Evaluation

Help the user assess digital retail experiences against the Intelligent Commerce CX Model—a structured 5-layer framework covering Memory, Intent, Orchestration, Execution, and Trust.

## How to Help

When the user asks for a commerce CX evaluation:

1. **Gather artifacts** - Ask for screen recordings, PDP screenshots, search interaction descriptions, checkout flows, or post-purchase emails
2. **Evaluate each layer independently** - Score Memory, Intent, Orchestration, Execution, and Trust against the rubric before synthesizing
3. **Identify gaps explicitly** - For each layer, surface what is present, what is missing, and the maturity level
4. **Produce structured output** - Return the full evaluation schema, an executive summary, and top 3 strategic opportunities

## Core Principles

### Layer 1: Customer State (Memory / Digital Twin)

**No profile = no intelligence**
The starting point is whether the system knows the customer. Without persistent state—browsing history, purchase patterns, preferences, lifecycle stage—every session starts cold. Score L1 (session-only) through L5 (predictive, continuously updated model). The maturity ladder drives what experiences are even possible downstream.

**Each level unlocks qualitatively different capability**
L2 shows recently viewed items. L4 surfaces the right product at the right life stage. L5 anticipates before the customer asks. A retailer cannot skip levels without building the data infrastructure underneath—maturity here constrains everything else in the framework.

### Layer 2: Intent

**Intent expansion beats keyword matching**
The difference between Low and High intent quality: a Low system returns results matching exact words; a High system asks clarifying questions or correctly infers the goal behind the words. Score: Low (keyword only) → Medium (some suggestions, user still does work) → High (expands vague queries, reduces steps to decision).

**Explicit vs. inferred intents both matter**
Strong intent analysis captures both stated needs ("I need running shoes") and unstated goals ("for my first 10K in 4 weeks"). The gap between these two is where most retailers leave decision support on the table. Unexpanded intents are lost conversions.

### Layer 3: Orchestration

**Decision support quality determines the journey**
Orchestration is the system's ability to sequence the right actions at the right moment. Score: Low (no guidance) → Medium (generic suggestions) → High (next best actions personalized to customer state + intent). The signal is whether the system drives the journey or the customer has to self-navigate.

**Research should be collapsed, not delegated**
A High-maturity orchestration layer answers questions before they're asked—"Will this fit in a studio apartment?"—rather than sending the user to a knowledge base. Score whether research is collapsed (yes/no). Delegating research is a gap; absorbing it is the target state.

### Layer 4: Execution

**Friction is the enemy of conversion**
Score friction 1 (seamless) through 5 (high friction). Look for: steps to purchase, form re-entry, error states, payment options, and whether the flow is agent-ready—meaning it can complete autonomously using the customer's stored context. Agent-readiness is the leading indicator of future-proof execution.

**Post-purchase is the forgotten layer**
Most CX audits stop at checkout. Post-purchase ranges from None (receipt email only) → Basic (order tracking, shipping updates) → Advanced (proactive issue resolution, reorder triggers, loyalty engagement, AI-assisted returns). Retention and repeat purchase live here.

### Layer 5: Trust

**Uncertainty should be explicit, not hidden**
A Strong trust layer surfaces what the system doesn't know: "I'm not sure about sizing for this brand—here are similar items with confident fit data." Poor trust means overconfident wrong answers delivered without disclosure. Score both explainability (Low/Medium/High) and uncertainty handling (Poor/Adequate/Strong) independently.

**Failure modes must be catalogued from evidence**
Every system breaks. The question is whether failures are graceful (offer alternative, acknowledge limit) or silent (wrong answer delivered confidently). Catalogue failure modes observed in the artifacts—not abstract risks. Observed failures are the most actionable input to trust improvements.

## Questions to Help Users

- "What artifacts do you have—screen recordings, screenshots, flow descriptions, or emails?"
- "Which experience surfaces are you evaluating: search, PDP, checkout, post-purchase, or all?"
- "Is this a single-retailer audit or a comparative benchmark across multiple companies?"
- "What decision does this evaluation need to support—roadmap prioritization, executive alignment, or vendor selection?"
- "Do you have access to the post-purchase flow, or only the pre-purchase journey?"
- "Are there specific layers where you already have a hypothesis or concern?"

## Common Mistakes to Flag

- **Stopping at checkout** - Post-purchase is where retention and repeat purchase live; evaluations that end at order confirmation are incomplete
- **Conflating personalization with memory** - A retailer can display personalized-looking content without a real digital twin; surface-level recommendations are not L3+ maturity
- **Scoring vibes instead of evidence** - Every score needs an observable artifact; "it felt helpful" is not evidence; tie every claim to what was seen
- **Missing the intent gap** - Most teams evaluate what the system does, not what it fails to surface; explicitly look for queries that went unexpanded or unanswered
- **Treating maturity as binary** - The L1–L5 ladder matters because each level has specific, different interventions; "they have personalization" is not a maturity assessment

## Deep Dive

For the full evaluation schema, scoring rubrics, agent prompt template, and example output format, see `references/evaluation-framework.md`

## Related Skills

- AI Product Strategy
- Building with LLMs
- AI Evals
- Behavioral Product Design
