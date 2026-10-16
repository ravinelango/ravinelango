# Validate the validator: QA habits that carry over to LLM evals

*Eval notes · Ravin Elango · October 2026*

After 10+ years in QA, UAT and performance testing, the idea I trust most for LLM work is an old one: **before you trust a measurement, validate the instrument.** A gauge that has never been checked is not a measurement system. An LLM judge that has never been compared to human labels is the same thing.

These notes come from building three small open-source tools: [judge-calibration-kit](https://github.com/ravinelango/judge-calibration-kit), [part11-eval-evidence](https://github.com/ravinelango/part11-eval-evidence) and [agent-uat-playbook](https://github.com/ravinelango/agent-uat-playbook). All three are early. Every dataset in them is synthetic, and none publishes real-model results. What follows is design lessons, not benchmark claims. The only numbers quoted are from the synthetic demos, and they are labeled that way.

## 1. A judge is a test instrument; measure its agreement, not its accuracy

If 90% of outputs pass, a judge that always says "pass" is 90% "accurate". In QA we would never accept that gauge. Two habits help:

- **Report Cohen's kappa next to raw agreement.** Kappa discounts the agreement you would get by chance. judge-calibration-kit prints both, plus a confusion matrix that separates *too lenient* (human fail, judge pass) from *too strict* (human pass, judge fail). Those two errors need different fixes: tighten the rubric for one, loosen it for the other.
- **Put an interval on it.** The bundled 10-item synthetic demo gives a kappa of 0.583, and its bootstrap 95% interval runs from 0.000 to 1.000. That is the honest picture: ten labels cannot tell you whether a judge is good. A report that shows only the point estimate would hide that.

## 2. Measure the humans too

A judge cannot reasonably agree with humans more than humans agree with each other. `jck agree` computes human-to-human agreement from two label columns, so you know the ceiling before you blame the judge. If two careful people only reach moderate agreement, the rubric is the problem, and no judge prompt will fix it.

## 3. Compare changes on the same labels, and say when you can't tell

When you change a judge prompt or model, run both versions against the *same* human labels (`jck ab`). The report lists every item where they disagree, which is where the learning is, and it warns when the kappa intervals overlap. In the synthetic demo, judge B has the higher kappa, and the report still says the sample does not show a reliable difference. Saying "can't tell yet" is part of the job.

## 4. An eval run is a record; make it tamper-evident, then say what that means

In regulated work (I focus on FDA 21 CFR Part 11), an auditor asks which requirement each test verifies, which model and config ran, and whether anyone changed the results afterwards. part11-eval-evidence turns a run into a SHA-256 hash-chained log, a requirements-to-test traceability matrix, and a validation summary.

Two lessons stuck:

- **A hash chain alone has a known gap.** Someone who can rewrite the whole file can rebuild a consistent chain, and can drop entries from the end. So the tool has `p11e head` and `p11e verify --expect-head`: record the final hash somewhere you don't control (a QMS record, a ticket, a signed tag) and check against it later. The README says "tamper-evident, not tamper-proof" for this reason.
- **The demo should fail loudly.** In the synthetic example, editing one result in the log makes `p11e verify` exit 1 with `content hash mismatch (entry edited)`. A control you have never seen fail is not a control.

## 5. Failures need dispositions, and the tool needs its own validation

A traceability matrix with red rows is not an evidence package until each failure has a root cause, a disposition (accepted, corrected or deferred), a rationale, and an approver. The tool now takes a dispositions file for exactly that.

And the tool is itself a computerized system. The repo includes an IQ/OQ-style validation-plan *template* for qualifying it, clearly labeled as a template, not a completed validation. It is not Part 11 compliant on its own (no access control or electronic signatures), and the README and mapping say so.

## 6. UAT for agents: acceptance is about actions, and about non-determinism

Offline evals tell engineers how a model scores. UAT asks whether the agent will do the job without doing anything it must never do. Two changes to classic UAT mattered most in agent-uat-playbook:

- **Actions are acceptance criteria.** A scenario lists the tools the agent must call, the tools it must never call, and now the order and arguments. "Called the refund tool" is not a pass if it ran before the order lookup or on the wrong order.
- **Run it more than once.** The same scenario can pass twice and fail once. The sign-off report shows per-scenario pass/fail counts and flags unstable scenarios, and any occurrence of an S1 defect stays S1. In the synthetic demo, an agent that acted on a prompt injection in 1 of 3 runs produces a **NO-GO**, even though most runs passed.

## What is not done

- No real judge has been calibrated against a real hand-labeled set in these repos yet. That is the next step for judge-calibration-kit, and the raw data will be published with it.
- part11-eval-evidence does not make anything compliant. It produces supporting evidence for people who own the validation.
- agent-uat-playbook has no real agent results; its examples exist to show the format.

If you work on QA for AI systems and see something wrong in these ideas or the tools, issues are welcome.
