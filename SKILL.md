---
name: human-oversight-gate
description: >-
  This skill operationalizes the human-decision node (人审断) of the human-AI
  co-governance loop, implementing EU AI Act Article 14 effective human oversight.
  Use it before any regulated or external AI action, or when ai-governance returns
  CONDITIONAL. It selects the oversight mode per action class (HITL / HOTL / HIC),
  captures Accept / Override / Block with a named supervisor sign-off (via
  identity-verify), tracks override-rate to defeat rubber-stamping, and emits
  evidence to audit-trail-keeper. Humans retain final accountability; AI only
  provides governability. Trigger for high-risk, medical-device, or international
  business contexts requiring human-oversight compliance.

version: 1.0.0
author: 注册老炮@MedXpert
license: MIT
category: AI治理
platforms: [windows, macos, linux]
displayName: 人类监督门禁
title: 人类监督门禁
tags: [人类监督, AI治理, 监督门禁, 闭环治理, 合规]
---

# Human Oversight Gate（人审断闸门 · Art.14）

## Overview

The control tower `ai-governance` decides PASS / CONDITIONAL / BLOCK. This skill makes the **CONDITIONAL human-decision step runnable** — it is the concrete instrument of EU AI Act Art.14. Not "a human somewhere in the workflow", but effective, evidenced, override-capable oversight that an auditor will accept.

## When to use

- `ai-governance` gate returns CONDITIONAL (human sign-off required).
- Any high-risk / regulated / external AI action where HITL applies.
- Periodic HOTL monitoring of an autonomous agent's operation.

## Core capabilities

### 1. Oversight-mode selector
Pick HITL / HOTL / HIC per action class, risk-tiered:
- **HITL**: agent proposes, human approves each consequential action before execution (diagnostics, credit, legal).
- **HOTL**: agent acts, human monitors and can intervene / stop (fraud, monitoring).
- **HIC**: human sets, audits, and can revoke limits; strategic governance.

### 2. Decision capture
Three actions: **Accept** (executes) / **Override** (human alternative + reason code) / **Block** (halt). Capture: timestamp, supervisor ID (via `identity-verify`), reason code, and the AI's original recommendation + confidence for comparison.

### 3. Named-supervisor sign-off
Delegate to `identity-verify` for the supervisor's competence / authority; refuse if unsigned. For Annex III point 1(a) biometrics, require verification by **two** competent natural persons (Art.14(5)).

### 4. Override-rate KPI
Track the percentage of AI decisions reversed by a human over time. ~0% → rubber-stamping alert; >20% → model-broken alert. Surface the metric; never hide it. This is what separates effective oversight from a warm body in the loop.

### 5. Evidence emission
Write the decision record to `audit-trail-keeper` (immutable). Evidence is the trail, not the intention.

## Workflow

1. Receive gate decision + context from `ai-governance`.
2. Select oversight mode for the action class.
3. Present the evidence bundle (`ai-grader` score, trail excerpt, compliance map).
4. Capture the human decision (Accept / Override / Block) with sign-off.
5. Compute / update the override-rate KPI.
6. Emit evidence to `audit-trail-keeper`; release or hold the action accordingly.

## Bridging existing skills

| Need | Delegate to |
|---|---|
| Supervisor identity / authority | `identity-verify` |
| Immutable log store | `audit-trail-keeper` |
| Gate pre-condition | `ai-governance` |
| Behavior baseline | `ai-grader` |

## Compliance mapping

- **EU AI Act Art.14(1)–(5)**: effective oversight; understand limitations; avoid automation bias; interpret output; override / stop; two-person verify for biometrics.
- **ISO/IEC 42001:2023 A.6.2.6**: human oversight as a designed control.
- **NIST AI RMF MANAGE-2.4**: mechanisms to supersede, disengage, or deactivate inconsistent systems.
- **FDA 21 CFR Part 11**: electronic signature on regulated decisions.

## Status（占位已落）

上述 5 项能力已落到本 SKILL.md；签名密钥管理与 override-rate 存储路径为运行环境依赖（非阻塞，待真实部署时配置）。

---

## 交付元数据（Deliverable Metadata）

- **版权（Copyright）**：© 2026 注册老炮@MedXpert。保留所有权利。引用需附出处。
- **时间戳（Timestamp）**：2026-08-28 10:41 GMT+8（生成）
- **指纹（Fingerprint / SHA-256）**：ef1c286f8e767beaa90d5e61360784791fc902133dbcc591fb6abe0d7d48550a（正文 SHA-256，不含本元数据块，可复验）
- **配套治理框架**：`人与AI治理理论及闭环落地_v1.0.md`（外部共享治理框架，未随包，需从治理理论知识库另行获取）
