# Flyway B Design

飞来汇（Flyway）B 端产品设计规范与 AI Design Skills。

本仓库用于统一跨境支付、收付款、换汇、账户、银行卡、风控及企业资金管理等 B 端产品的设计语言、页面结构和 AI 设计执行流程。

## 仓库内容

主要规范包括：

- `AGENTS.md`：AI Agent 的总执行协议与任务边界
- `Design-System.md`：颜色、字体、间距、组件和设计 Token 规范
- `AI-Design-Skill.md`：AI 进行页面设计、评审和交付的方法
- `Pattern-Library.md`：列表、详情、表单、Dashboard 等页面结构模式

> 实际文件位置请以仓库中的目录结构为准。

## 使用方式

开始页面设计、页面改版、设计评审或 Figma 落图前，应依次阅读：

1. `AGENTS.md`
2. `Design-System.md`
3. `AI-Design-Skill.md`
4. `Pattern-Library.md`

完整设计依据为：

```text
Design-System.md
+ AI-Design-Skill.md
+ Pattern-Library.md
+ AGENTS.md
= 合规的飞来汇 B 端页面设计
```

## 基本原则

- 优先复用现有 Component、Variant、Variable 和 Style
- 使用语义化 Token，不直接使用任意颜色或尺寸
- 页面结构必须匹配 Pattern Library
- 使用 Auto Layout 构建可变内容
- 覆盖加载、错误、空状态、权限和风险状态
- 分别定义 Desktop、Compact Desktop 和 Mobile 行为
- 未经授权，不修改正式组件库和设计 Token
- 缺失能力应标记为 `Composition Pattern` 或 `Needs Extension`

## 适用范围

本规范适用于：

- 跨境收款与付款
- 企业账户与资金管理
- 换汇及汇率相关功能
- 银行卡及支付工具管理
- 交易记录与业务详情
- KYC、KYB、合规和风险控制
- 企业运营及管理后台

## 目录结构

```text
flyway-b-design/
├── README.md
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── AGENTS.md
    ├── AI-Design-Skill.md
    ├── Design-Document-Output-Rules.md
    ├── Design-System.md
    └── Pattern-Library.md
```

`SKILL.md` 为 skill 入口；`references/` 下为四份治理文档与 Figma 交付规则。
