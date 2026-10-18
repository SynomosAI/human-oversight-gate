# human-oversight-gate · 人类监督闸门（人审断 · Art.14）

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.md)
[![Agent Skill](https://img.shields.io/badge/Agent%20Skill-SKILL.md-blue.svg)](SKILL.md)
[![EU AI Act Art.14](https://img.shields.io/badge/EU%20AI%20Act-Art.14-brightgreen.svg)](SKILL.md)
[![HITL / HOTL](https://img.shields.io/badge/oversight-HITL%20%7C%20HOTL%20%7C%20HIC-2ea44f.svg)](SKILL.md)
[![ISO/IEC 42001](https://img.shields.io/badge/ISO%2FIEC%2042001-A.6.2.6-informational.svg)](SKILL.md)
[![Version](https://img.shields.io/badge/version-1.0.0-informational.svg)](SKILL.md)

SynomosAI 四支柱体系：**身份（Identity）· 溯源（Traceability）· 治理（Governance）· 共生（Symbiosis）**——当 AI 进入商业，可信是唯一的硬通货。

> 本仓库属于 [SynomosAI](https://github.com/SynomosAI) 生态技能包的一员。生态全景见 [`synomosai-skills`](https://github.com/SynomosAI/synomosai-skills)，理论站位见 [`traceability-audit`](https://github.com/SynomosAI/traceability-audit)。

**关键词 / Keywords**：人类监督 · 人审断 · EU AI Act Art.14 · HITL/HOTL/HIC · override 率 KPI · 具名主管签核 · 审计证据链 · human oversight · effective human oversight · regulated AI

把人机协同治理闭环里的**人审断节点**做成可执行的工具，落地 **EU AI Act 第 14 条有效人类监督**。它不是「流程里随便有个人」，而是可被审计接受的、有证据、可 override 的监督：`ai-governance` 闸门给出 CONDITIONAL 时，由本技能选择监督模式、捕获 Accept/Override/Block、具名签核、跟踪 override 率、把证据写入不可变审计轨迹。**人类保留最终问责权，AI 只提供可治理性。**

---

## ✨ 特性 / Features

- **监督模式选择器**：按动作类别与风险分级选 HITL / HOTL / HIC。
  - **HITL**（人在环）：Agent 提议，人在每个重大动作执行前批准（诊断、信贷、法律）。
  - **HOTL**（人在上）：Agent 执行，人监控并可干预 / 叫停（欺诈、监控）。
  - **HIC**（人在控）：人设定、审计并可撤销限额；战略治理。
- **决策捕获**：Accept（执行）/ Override（人给替代方案 + 原因码）/ Block（叫停）；记录时间戳、主管 ID（经 `identity-verify`）、原因码、AI 原建议与置信度以便对照。
- **具名主管签核**：主管的能力 / 职权委托 `identity-verify` 核验；未签核则拒绝执行。生物识别（Annex III 1(a)）须**两名**有资质自然人核验（Art.14(5)）。
- **Override 率 KPI**：跟踪人类推翻 AI 决策的比例。≈0% → 橡皮图章告警；>20% → 模型失效告警。指标必须公开，不得隐藏。
- **证据发射**：决策记录写入 `audit-trail-keeper`（不可变）。证据是轨迹，不是意图。

---

## 🚀 快速开始 / Quick Start

> 前置：把本目录放入 Agent 技能目录；主管身份核验委托 `identity-verify`，不可变日志委托 `audit-trail-keeper`。

```bash
# 1. 克隆本仓
git clone https://github.com/SynomosAI/human-oversight-gate.git
cd human-oversight-gate

# 2. 查看技能主文件（监督模式 / 决策捕获 / KPI / 合规对标）
cat SKILL.md
```

当 `ai-governance` 闸门返回 CONDITIONAL，或任何受监管 / 对外 AI 动作需要 HITL 时调用：先选监督模式，再呈证据包，再捕获人审决策并签核。

```text
触发词示例：
  人审断 / 人类监督 / HITL / HOTL / override
  CONDITIONAL 闸门 / 高风险动作 / 受监管 AI / 电子签核
```

---

## 📖 使用方式 / Usage

1. 接收 `ai-governance` 的闸门决策与上下文；
2. 按动作类别选择监督模式（HITL / HOTL / HIC）；
3. 呈证据包（`ai-grader` 评分、轨迹摘录、合规对标图）；
4. 捕获人类决策（Accept / Override / Block）并完成具名签核；
5. 计算 / 更新 override 率 KPI；
6. 证据写入 `audit-trail-keeper`，相应放行或扣住动作。

### 决策捕获记录示例（节选）

```text
动作：自动给某高风险客户发放信贷提额
  AI 原建议：批准（置信度 0.82）
  监督模式：HITL（信贷动作类）
  主管签核：张主管（identity-verify 已核验，competence=信贷审批）
  人类决策：Override
  原因码：R-07 风险偏好超限
  人类替代方案：降额 30% 后人工复核
  override 率（近 30 天）：12.4%（正常区间）
  证据已写入 audit-trail-keeper（记录 ID：...）
```

---

## 🧩 仓库结构 / Repository layout

```text
human-oversight-gate/
├── README.md                # 本文件
├── README.en.md             # 英文版说明
├── SKILL.md                 # 技能主文件（监督模式 / 决策捕获 / KPI / 合规对标）
├── LICENSE.md               # MIT License
├── llms.txt / llms-full.txt # 给 AI 的索引与完整文本
├── AGENTS.md                # 给 AI Agent 的工作指引
├── SECURITY.md              # 安全策略
└── CODEOWNERS               # 代码所有者
```

---

## 🔎 合规对标 / Compliance mapping

- **EU AI Act Art.14(1)–(5)**：有效监督；理解局限；避免自动化偏见；解读输出；可 override / 叫停；生物识别两人核验。
- **ISO/IEC 42001:2023 A.6.2.6**：人类监督作为设计内控制。
- **NIST AI RMF MANAGE-2.4**：取代 / 脱离 / 停用不一致系统的机制。
- **FDA 21 CFR Part 11**：受监管决策的电子签名。

---

## ❓ 常见问题 / FAQ

- **流程里有人就算有效监督吗？** 不算。需要可 override、有证据、具名签核，且 override 率被持续跟踪（防橡皮图章）。
- **Override 率多少算正常？** ≈0% 提示橡皮图章，>20% 提示模型失效；指标必须公开。
- **生物识别类动作有何特殊？** Annex III 1(a) 须两名有资质自然人核验（Art.14(5)）。

---

## License / 许可

本项目以 **MIT** 许可发布，详见仓库根目录 [LICENSE.md](LICENSE.md)。版权：© 2026 注册老炮@MedXpert。

---

## 🔒 安全 / Security

如发现安全问题，请按 [`SECURITY.md`](SECURITY.md) 的方式私下报告，不要在公开 issue 中披露。

## 🤝 贡献 / Contributing

欢迎补充监督模式矩阵、原因码字典与 KPI 阈值；修改 `SKILL.md` 时保持 YAML frontmatter 字段兼容。代码所有者见 [CODEOWNERS](CODEOWNERS)。

---

## 免责声明

本仓库内容为 SynomosAI 的**理论站位与工具化探索**，不代表任何已获认证、已商业化交付或已服务特定客户的声明；文中涉及的 EU AI Act Art.14、ISO/IEC 42001、NIST AI RMF、FDA 21 CFR Part 11 等外部标准与条款信息为公开资料转述，正式引用前请**独立核实**。签名密钥管理与 override 率存储路径为运行环境依赖（待真实部署时配置）。API、授权码与形象大使等为路线图（roadmap）事项，尚未上线。
