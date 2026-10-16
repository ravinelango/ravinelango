# Ravin Elango

**AI Evaluation & Quality Engineer** · I make LLM and agent systems measurable, reliable, and safe to ship.

10+ years leading QA, test automation, performance/load testing, and UAT in healthcare, automotive, and fintech. Now applying that discipline to LLM and GenAI quality: evals, golden datasets, graders you can trust, and release gates that stop regressions before users see them.

## What I do

- **Eval strategy & harnesses:** turning "does it work?" into golden datasets, rubrics, and automated eval suites wired into CI
- **LLM-as-a-judge, validated:** measuring judge agreement against human-in-the-loop labels before trusting any score
- **RAG & agent evaluation:** retrieval quality, faithfulness, tool use, and failure taxonomies from error analysis
- **Safety & red teaming:** prompt injection and jailbreak testing mapped to the OWASP Top 10 for LLM Applications, plus guardrail checks
- **Release gates & regression:** go/no-go rules for model and prompt upgrades, with quality, latency, and cost tracked together
- **Regulated-domain rigor:** healthcare EDI/HIPAA testing and FDA 21 CFR Part 11 validation

## Selected impact

- Built an AI-driven Python/Playwright test automation solution that avoided about **$200K** in licensing costs
- Used ChatGPT and Claude to cut manual test design and root-cause analysis effort by about **70%**
- Cut mobile app crashes from **2% to 0.7%** and lifted the app rating from **2.9 to 4.5**
- Led UAT for a health record portal serving about **50 million** consumers
- Designed a UAT strategy that raised defect detection efficiency **39%** with **98%** coverage
- Built a Tosca framework from scratch: test coverage/accuracy up **88%**, time to release down **45%**
- Led onshore/offshore QA teams; built Azure/KQL monitoring dashboards

## Featured projects

### [part11-eval-evidence](https://github.com/ravinelango/part11-eval-evidence)

Turns an LLM eval run into an audit-ready validation record: a SHA-256 hash-chained run log with a `verify` command that catches edits, a requirements traceability matrix, and a one-page validation summary, each mapped to FDA 21 CFR Part 11 clauses. Early stage with synthetic example data only; it supports evidence and is not itself a compliant system.

### [judge-calibration-kit](https://github.com/ravinelango/judge-calibration-kit)

Measures whether an LLM-as-a-judge can be trusted before its scores are used: agreement with human labels (Cohen's kappa with a bootstrap CI, Wilson CIs on pass rates), a per-rubric-criterion breakdown, a human-to-human baseline, and a disagreement report. Early stage; synthetic demo data only, no real results yet.

### [agent-uat-playbook](https://github.com/ravinelango/agent-uat-playbook)

User acceptance testing for AI agents: Given/When/Then acceptance scenarios with expected and forbidden tool calls and guardrails, a business-user test script, an agent defect triage guide, and a go/no-go sign-off report usable as a release gate. Synthetic example only.

### [ai-qa-eval](https://github.com/ravinelango/ai-qa-eval)

An LLM quality-engineering portfolio that tests an LLM application the way a QA team would, on a public FDA 21 CFR Part 11 guidance corpus.

| Phase | What | Status |
|---|---|---|
| 0 | Scaffold: provider contract, budget guard, tracing (local JSONL / Langfuse), CI | ✅ Done |
| 1 | RAG eval harness: golden dataset, Ragas/DeepEval metrics, validated LLM-as-a-judge, CI release gate | 🛠️ Next |
| 2 | Agent red-team suite: promptfoo + garak, OWASP LLM Top 10 | 🗺️ Roadmap |
| 3 | Model-upgrade regression dashboard: paired stats, latency/cost, Streamlit | 🗺️ Roadmap |

Ground rule: no made-up evidence. Every number in that repo will come from a saved run, and nothing is reported until it has run.

## Eval notes

- [Validate the validator: QA habits that carry over to LLM evals](notes/validate-the-validator.md): judge agreement vs accuracy, tamper-evident eval records, and UAT for agents, from building three small open-source tools.

## Toolkit

**Testing & automation:** Python · pytest · Playwright · Selenium · Tosca · LoadRunner · JMeter · GitHub Actions
**LLM eval (current focus):** DeepEval · Ragas · promptfoo · garak · Langfuse · Arize Phoenix · LangSmith · Anthropic & OpenAI APIs
**Data & cloud:** Azure · KQL · AWS

**Education:** MS, Information Technology and Management, Illinois Institute of Technology

## Open to

AI Evaluation / LLM Evaluation Engineer, AI Quality Engineer, AI Quality & Reliability, and AI eval leadership roles. Chicago or remote.

📫 [Connect on LinkedIn](https://www.linkedin.com/in/ravinelango/)
