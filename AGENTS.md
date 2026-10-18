# AGENTS.md — 给 AI Agent 的工作指引

本文件面向自动化 AI Agent。人类读者请看 [README.md](README.md)。

## 这个仓库是什么

`human-oversight-gate` 是一个 **Agent Skill 发布包**，核心资产是 `SKILL.md`（EU AI Act Art.14 有效人类监督的落地工具）。把本目录放入 Agent 技能目录，即可在 `ai-governance` 返回 CONDITIONAL 时执行可审计的人审断节点。

## 可用的工作命令

```bash
cat SKILL.md    # 监督模式 / 决策捕获 / KPI / 合规对标
```

前置依赖：无运行时依赖；主管身份核验委托 `identity-verify`，不可变日志委托 `audit-trail-keeper`。

## 约定（Do）

- 修改 `SKILL.md` 时保持 YAML frontmatter 字段兼容（`name` / `version` / `license` / `author` 等）。
- 未具名签核的人审决策**不得放行**受监管动作。
- override 率 KPI 必须计算并公开；≈0% 与 >20% 都要告警。
- 生物识别类动作（Annex III 1(a)）须两名有资质自然人核验。

## 禁止（Don't）

- 不要改动 `LICENSE.md` 的版权主体（© 2026 注册老炮@MedXpert），也不要改 `SKILL.md` 的 `author` 字段或交付元数据块（含指纹）。
- 不要在没有人类决策记录时擅自执行受监管 / 对外动作。
- 不要隐藏 override 率 KPI；这是有效监督与「流程里有个人」的区别。
- 不要在仓库内提交任何签核密钥、令牌或真实主管凭据。

## 边界

本技能专注**人审断节点的可执行化**；不替代主管的实质判断，不覆盖 AI 侧的 `ai-governance` 闸门逻辑。
