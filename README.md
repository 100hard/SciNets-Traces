# SciNets-Traces
# SciNets Reasoning Trace Dataset

This repository contains the behavioral reasoning traces used in the SciNets paper.
Rather than evaluating only outputs, SciNets is evaluated as a *scientific reasoning engine*.
We publish full traces to enable transparent inspection of how the system explores,
constructs hypotheses, fails, and stabilizes reasoning.

---

## What is Included
- Full JSON reasoning traces for Q1–Q6
- Structural exploration logs
- Symbolic vs grounded causal reasoning paths
- Collapse detection and grounding stability metrics
- Prompts used to produce the traces
- Metadata detailing execution configuration

---

## System Metadata (Summary)
- Base Model: `gpt-5-mini`, accessed via ChatOpenAI
- Hardcoded Model Identity: `gpt-4o`
- Temperature: `0.0` (deterministic intent)
- No seeds used
- OpenAI does not guarantee literal bit-level determinism

---

## Retrieval & Knowledge Environment
- Primary: OpenAlex (scientific papers)
- Secondary: DuckDuckGo Search (validation)
- Max 10 papers per query
- Typical graph: ~120–210 nodes, ~150–260 edges
- Corpus is dynamic and non-deterministic
- Query refinement is LLM driven → introduces variance

---

## Graph Construction Pipeline
1. Retrieve top-10 papers (OpenAlex)
2. Extract `(Subject, Predicate, Object)` knowledge triplets
3. Normalize entity variants
4. Optional densification step
5. Extract symbolic paths using `networkx`
6. Select diverse chains using Jaccard filtering

High repeatability, but small variations in node naming may occur.

---

## Execution Policy
- Single run per query
- No cherry picking
- Q5 rerun only due to Unicode runtime error
- Collapses are preserved deliberately
- Q3/Q4/Q5 demonstrate explicit grounding failure, recorded as evidence

See `execution_policy.md` for full statement.

---

## Intended Use
These traces enable:
- behavioral auditing
- epistemic reliability analysis
- failure characterization
- methodological transparency

They do **not** enable reconstruction of the proprietary SaaS.

---

## License
Academic Transparency License:
- Free for research analysis and citation
- Not allowed for commercial system replication

---

## Citation
If using these traces, please cite:
"SciNets: Structural Trace-Based Behavioral Evaluation for Scientific Discovery Systems"
