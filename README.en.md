# human-oversight-gate · Human Oversight Gate (Art.14)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.md)
[![Agent Skill](https://img.shields.io/badge/Agent%20Skill-SKILL.md-blue.svg)](SKILL.md)
[![EU AI Act Art.14](https://img.shields.io/badge/EU%20AI%20Act-Art.14-brightgreen.svg)](SKILL.md)

SynomosAI four-pillar system: **Identity · Traceability · Governance · Symbiosis**.

> This repo is part of the [SynomosAI](https://github.com/SynomosAI) skill ecosystem.

**Keywords**: human oversight · HITL/HOTL/HIC · EU AI Act Article 14 · override-rate KPI · named supervisor sign-off · audit trail · regulated AI

Operationalizes the human-decision node of the human-AI co-governance loop, implementing EU AI Act Article 14 effective human oversight. When the `ai-governance` gate returns CONDITIONAL, it selects an oversight mode, captures Accept/Override/Block with named sign-off, tracks the override-rate KPI, and writes evidence to an immutable audit trail. Humans retain final accountability.

## Quick Start

Prerequisite: place this directory in your agent skills folder. Supervisor identity is delegated to `identity-verify`; the immutable log to `audit-trail-keeper`.

```bash
git clone https://github.com/SynomosAI/human-oversight-gate.git
cd human-oversight-gate
cat SKILL.md
```

```text
Triggers: human oversight · HITL · HOTL · override · CONDITIONAL gate
high-risk action · regulated AI · electronic sign-off
```

## What it covers

- **Oversight-mode selector**: HITL (human approves each consequential action) / HOTL (human monitors and can stop) / HIC (human sets, audits, revokes limits).
- **Decision capture**: Accept / Override (human alternative + reason code) / Block, with timestamp, supervisor ID, AI recommendation and confidence.
- **Named sign-off**: supervisor competence verified via `identity-verify`; unsigned = refuse. Biometrics require two competent persons (Art.14(5)).
- **Override-rate KPI**: ~0% = rubber-stamping alert; >20% = model-broken alert. Always surfaced, never hidden.
- **Evidence emission**: decision record written to `audit-trail-keeper`.

## Decision record example (excerpt)

```text
Action: auto credit-limit increase for a high-risk customer
  AI recommendation: approve (0.82)
  mode: HITL (credit action class)
  supervisor: Zhang (identity-verify, competence=credit approval)
  human decision: Override, reason R-07 risk-appetite exceeded
  override rate (30d): 12.4% (normal band)
  evidence written to audit-trail-keeper
```

## Compliance mapping

EU AI Act Art.14(1)-(5) · ISO/IEC 42001:2023 A.6.2.6 · NIST AI RMF MANAGE-2.4 · FDA 21 CFR Part 11.

## License

MIT License. © 2026 注册老炮@MedXpert. See [LICENSE.md](LICENSE.md).

## Disclaimer

Theoretical-positioning and tooling exploration. External standards (EU AI Act Art.14, ISO/IEC 42001, NIST AI RMF, FDA 21 CFR Part 11) are paraphrased from public sources; verify independently before formal citation.
