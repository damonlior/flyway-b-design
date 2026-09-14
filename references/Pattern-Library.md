# 飞来汇 B 端 Pattern Library

> 来源：Figma 文件「飞来汇设计规划（新） 25 26」  
> 文件 Key：`O7KzP4Nz3A2V3tlySgXNmT`  
> 扫描日期：2026-07-21  
> 组件规则补充来源：Figma 文件「❖ 飞来汇设计规范 B端 V2.0」中的「典型示例及说明」及已发布组件描述  
> 组件规则补充日期：2026-07-23  
> 配套规范：`Design-System.md`、`AI-Design-Skill.md`  
> 说明：本文提炼页面级、任务级与响应式组合模式，不重新定义颜色、字体、间距或基础组件。视觉与组件规则仍以 Design System 为准。

## 0. 扫描范围与结论

文件共有 19 个页面，其中 9 个页面包含内容。

正式 Pattern 主要来自：

- `多分辨率适配`：全局框架、导航、Dropdown、Modal、Drawer、Date Picker 的跨端转换。
- `资金`：资金总览、多币种余额、资金操作入口。
- `飞贸通`：收款订单列表、银行账户卡片/列表。
- `交易管理`：交易列表、拒付/退款分类、交易详情与多状态页面。
- `FlyPay`：多步骤进件、材料上传、审核中、审核不通过、流程中止、站点管理。

`现状截图`和`产品参考`只用于验证问题与方向；`废纸篓`不作为正式 Pattern 来源。

### Pattern 分类

| 层级 | Pattern |
|---|---|
| 全局框架 | Application Shell、Responsive Shell、Global Header、Navigation |
| 页面结构 | Dashboard、List、Card List、Detail、Multi-step Form、Status Result |
| 任务模式 | Filter、Summary Metrics、Batch Action、Risk Action、Draft & Resume |
| 覆盖层 | Dropdown / Action Sheet、Modal / Sheet、Drawer / Sheet、Date Picker |
| 数据表达 | Money、Status、Timeline / Progress、Empty / Error / Permission |

# 1. Application Shell Pattern

## Purpose

为企业后台提供稳定的导航、搜索、身份和内容承载框架，使用户在跨资金、收款、交易、付款和 FlyPay 业务间切换时保持方向感。

## Structure

```text
Application Shell
├── Primary Navigation
│   ├── Brand
│   ├── First-level Navigation
│   ├── Second-level Navigation
│   └── Product Switch / Fly+
└── Main Area
    ├── Global Header
    │   ├── Breadcrumb / Page Title
    │   ├── Global Search
    │   ├── Support
    │   ├── Notification
    │   └── Account Menu
    └── Page Content
```

## Observed Layouts

| 画板 | 导航 | 内容区 | 规则 |
|---:|---:|---:|---|
| 1440 | 180 展开 | 1260 | 标准桌面后台 |
| 1280 | 56 收起 | 1224 | 收缩导航，为内容保留宽度 |
| 800 | 56 收起 | 744 | 紧凑桌面/平板横屏 |
| 390 | 无常驻侧栏 | 390 | 移动端导航通过覆盖层进入 |

这些尺寸是文件中的设计样例，不应直接解释为唯一的前端断点。实现时应以内容可用宽度、导航状态和组件最小宽度共同决定切换点。

## Usage Rules

- Desktop 保留稳定的左侧导航与 Global Header。
- 当前栏目必须同时通过导航选中态和 Breadcrumb / Page Title 表达。
- 侧栏收起后保留可识别图标，并通过 Tooltip 补充名称。
- Mobile 不压缩完整桌面侧栏，应转换为带遮罩的 Navigation Drawer。
- Page Content 使用垂直 Auto Layout；全局 Header 与页面滚动内容分层处理。
- 搜索、客服、消息和账户属于全局能力，不随业务页面重复创建。

## Forbidden

- 不同页面采用不同侧栏宽度或不同 Header 高度。
- 在 390 宽度下继续保留桌面侧栏。
- 仅通过颜色表达当前导航位置。
- 页面自行增加第二套全局搜索或账户菜单。

# 2. Responsive Transformation Pattern

## Purpose

在大屏桌面、紧凑桌面和移动端之间保持任务一致，而不是对桌面页面做等比缩放。

## Transformation Rules

### Desktop → Compact Desktop

- 展开侧栏转换为 56 宽度的图标侧栏。
- 内容列数量按可读宽度减少。
- Filter 优先换行，不缩小控件到不可操作尺寸。
- 表格保留关键列；次要字段可合并为两行 Cell 或进入详情。

### Desktop → Mobile

- 侧栏转换为带遮罩 Drawer。
- 多栏 Card 转为单栏纵向列表。
- 横向 Filter 转为纵向字段或独立筛选 Sheet。
- Table 优先转为 Card List、关键字段列表或横向可控滚动；不能简单压缩全部列。
- Dropdown、复杂 Date Picker 和大体量 Modal 转为 Bottom Sheet。
- 页面级操作可放入底部操作区，但必须避开系统安全区。
- 当视口宽度不大于 375px 时，Button Group 转为垂直排列，组内按钮宽度为 100%。
- 垂直 Button Group 中 Primary 位于上方；水平 Button Group 中 Primary 位于右侧。

## Responsive Priority

缩窄时按以下顺序处理：

1. 保留任务目标和主操作。
2. 保留状态、金额、对象和风险信息。
3. 合并次要字段。
4. 折叠低频操作到 Dropdown。
5. 将辅助说明移入详情或 Tooltip。
6. 最后才允许横向滚动。

# 3. Dashboard / Home Pattern

## Purpose

帮助用户进入系统后快速判断待办、资金、常用操作和业务变化。

## Structure

```text
Page Header
→ Promotion / Important Notice
→ Todo Center
→ Balance Summary
→ News / Information
→ Quick Actions
→ Related Rates / Trends
```

## Modules

### Promotion

- 只承载当前阶段最重要的产品能力或运营信息。
- 提供明确的查看/体验入口。
- 用户已完成目标后应停止持续展示。

### Todo Center

- 按风险与时效排序。
- 每项包含：标题、原因、影响、关键金额/对象、处理动作。
- 身份认证过期、逾期还款等高风险事项优先于普通资讯。

### Balance Summary

- 显示总资产估值、基准币种和更新时间/说明。
- 支持隐藏余额、只看有余额币种、编辑币种。
- 多币种 Card 保持相同结构：旗帜 + 币种名称/代码 + 金额 + 子状态。

### Quick Actions

- 保留 4–8 个最高频动作。
- 每项包含图标、动作名称和必要说明。
- 提款、付款、换汇、结算等金融操作必须使用稳定语义。

## Responsive Rules

- Desktop 可使用主列 + 侧栏信息结构。
- Compact Desktop 将辅助侧栏移动到主内容下方。
- Mobile 所有模块转为单列，并把余额、资讯等长内容折叠。

# 4. Funds Overview Pattern

## Purpose

在同一页面完成资金概览、币种查看和高频资金操作入口。

## Structure

```text
Breadcrumb / Page Title
→ Financial Action Cards
→ Funds Summary Header
→ Currency Controls
→ Currency Balance Grid
→ Related Account / Recipient Entry
```

## Rules

- Action Cards 用于提款、付款、换汇、下发结算等高频任务。
- 总资产必须标注估值币种，例如 `USD 2,320.04`。
- 币种 Card 必须同时显示币种名称与 ISO Code。
- 主余额突出显示；待入账、未结算等子金额降级显示。
- 零余额币种允许隐藏；用户可管理常用币种。
- “切换币种”改变估值口径，不改变底层账户实际币种。
- 金额使用 Number Style，并按币种小数规则格式化。

## States

- Balance Visible / Hidden。
- All Currencies / Non-zero Only。
- Currency Expanded / Collapsed。
- Loading / Partial Loading / Error。
- 无币种账户时使用对应 Empty Illustration，并提供开通或添加入口。

# 5. Data List Pattern

## Purpose

用于收款订单、交易记录、拒付记录、退款记录、站点管理等高密度数据任务。

## Structure

```text
Breadcrumb + Page Title
→ Tabs（可选）
→ Filter Panel
→ Summary Metrics（可选）
→ Page Actions
→ Data Table
→ Pagination
```

## Filter Panel

- Label 顶对齐。
- 日期区间、状态、对象、来源和编号是常见条件。
- 主筛选动作靠右；Reset 使用弱操作。
- 条件过多时保持两行以内，更多条件通过“展开筛选”呈现。
- 筛选后保持条件可见；返回列表时恢复筛选、排序和页码。

## Summary Metrics

适用于收款订单等需要快速判断处理量的页面：

- 已收款
- 已入账
- 待入账
- 其他可执行聚合状态

Metric Card 可附带就近动作，例如“合并入账”，但一个 Card 最多一个主要动作。

## Table Rules

- 文本左对齐；金额右对齐；状态使用 Tag。
- 订单号、流水号等可跳转标识使用 Link。
- 日期时间允许两行展示。
- 操作列固定在右侧。
- 行内保留 1–2 个高频动作，其余放入“更多”。
- 批量操作仅在选择数据后出现，并明确显示选中数量。
- 无数据时保留表头和筛选上下文。
- Pagination 位于 Table 底部，并显示总数、页码、每页数量和前往页。
- Table 与 Pagination 必须构成连续数据区域，不能被无关模块分隔。
- Table Empty 区分“首次无数据”和“筛选无结果”：前者可引导创建，后者优先提供“清空筛选”。
- Table Empty 的插画必须以插画 Main Component 默认宽高的 `0.5×` 等比例显示；具体计算与边界见第 15 章「Empty Illustration Sizing」。
- Mobile 不压缩全部列；按任务优先转换为 Card List、关键字段列表，最后才使用受控横向滚动。

## Typical Variants

### Transaction List

Tabs：全部交易 / 拒付明细 / 退款明细。

关键字段：

- 交易名称
- 交易单号
- 交易来源
- 商户订单号
- 交易对手
- 交易时间
- 交易金额
- 状态
- 操作

### Collection Order List

可在 Table 前增加收款、入账和待入账指标，并提供合并入账等批量动作。

### Site Management List

使用进度与审核状态组合表达申请状态，并提供“查看进度”或“查看接入信息”。

# 6. Card List / Account Management Pattern

## Purpose

用于银行账号等信息较丰富、需要强调账户属性和可操作性的对象集合。

## Structure

```text
Tabs
→ Search + Attribute Filters
→ Create Action
→ Account Cards / Compact List
→ Pagination
```

## Card Variant

适合强调：

- 账户类型
- 清算网络
- 账号
- 收款币种
- 适用场景
- 限制说明
- 查看、复制、导出

## List Variant

适合对象数量较多或需要快速比较时使用。关键信息保持可扫描，银行 Logo、账号、币种和状态不能被次要说明淹没。

## Usage Rules

- 支持通过账号、开户地区、币种和清算网络筛选。
- Copy 操作必须提供成功反馈。
- 导出操作需表达权限和 Loading。
- 账号默认脱敏；只有授权用户可查看完整信息。
- Create Action 使用明确文案，例如“开通新的银行账号”。

# 7. Detail Pattern

## Purpose

展示交易对象的当前状态、核心字段、资金明细和后续操作。

## Structure

```text
Breadcrumb + Page Title
→ Status Header
→ Key Actions
→ Basic Information
→ Payment / Settlement Information
→ Related Records
→ Timeline / Risk Information（按需）
```

## Status Header

包含：

- 业务对象编号
- 对象名称
- 当前状态
- 状态说明
- 必要的流程进度
- 主操作与次要操作

状态变化不能只改变颜色；必须同步调整状态文字、说明和可用操作。

## Information Sections

- 使用稳定的 Label–Value 网格。
- 关键金额加粗，但仍显示币种。
- 未提供的数据统一使用 `-`，不能留空造成误解。
- 支付信息、关联入账、退款等复杂内容使用 Table。
- 长页面按 Section 划分，不将所有字段放入一个 Card。

## Observed Transaction States

### Online Payment

- 未支付
- 已支付 · 待入账
- 已支付 · 已入账
- 交易信息不完整

### TT Transfer

- 支付中
- 部分支付 · 待入账
- 部分支付 · 部分入账
- 已支付 · 已入账

## Action Rules

- 退款、关联入账、补充交易信息等动作由状态决定。
- 不可用动作应隐藏；需要解释时禁用并提供原因。
- 高风险动作必须明确对象、金额、后果和二次确认。

# 8. Multi-step Onboarding Pattern

## Purpose

用于 FlyPay 网站接入、企业资料、材料上传、审核和账户开通等长流程任务。

## Structure

```text
Independent Process Header
→ Horizontal Steps
→ Step Title / Helper
→ Grouped Form Sections
→ Agreement / Confirmation
→ Primary Action + Save Draft
```

## Observed Steps

1. 确认公司信息
2. 上传材料
3. 材料审核
4. 开通账户

## Form Layout

- Desktop 使用居中内容列。
- 同一表单中承载相邻字段及字段组的 `Fields` 纵向 Auto Layout 统一使用 `Gap = 24`；该规则同时适用于 Desktop 与 Mobile。
- `Gap = 24` 仅用于 `Fields` 容器层级，不覆盖单个 Field 内部 Label、Control、Helper / Error 的组件固有间距。
- Form 内容宽度只使用 572 / 720 / 900；不得因大屏而无限拉伸。
- 固定字段宽度只使用 134 / 280 / 426 / 572，其序列关系为 `width = 134n + 12(n−1)`。
- 当固定宽度不适合响应式容器时使用 Fill Container，不创建新的中间字段宽度。
- 同一 Form Section 内保持一种 Label 对齐方式；移动端、长 Label 和单列任务优先顶对齐。
- 简短相关字段可组成两列；长文本、上传和说明使用整行。
- Section 示例：基本信息、法人信息、交易规模、通讯信息、其他信息。
- 已知企业资料可使用只读详情展示，减少重复录入。
- 单位、国家区号和币种通过前置单位组件表达。
- 字段按用户完成任务的顺序排列，关联字段相邻；不得只按后端数据模型排序。
- 提交区与字段区分离，一个提交任务最多一个 Primary Action。

## Progress Rules

- 已完成、进行中、未开始、未通过、已中止必须可区分。
- 用户不能跳过存在依赖关系的步骤。
- 返回上一步时保留已输入内容。
- 长流程必须提供“保存且稍后回来”。
- 离开前如有未保存内容，应提示风险。

## Validation

- 字段错误就地显示。
- 字段必须覆盖初始、激活、录入、录入激活、禁用、为空报错和录入报错等相关状态。
- 上传错误指向具体文件及修复要求。
- 提交失败保留所有输入和文件。
- 首个错误获得焦点，步骤栏同步显示问题所在步骤。
- 禁止使用 Toast 代替字段校验信息。

# 9. Material Upload & Review Pattern

## Purpose

处理资质材料、域名证明、证件照和经营资料的上传、审核与补充。

## Upload Item

每项包含：

- 材料名称
- 用途说明
- 格式/大小/数量要求
- 查看示例
- 上传入口
- 文件列表
- 单文件状态
- 错误原因与重新上传

## Review States

### Reviewing

- 使用居中的状态插画、标题和预计时长。
- 提供返回入口，不要求用户重复提交。

### Rejected / Needs Revision

- 在对应材料附近展示审核意见。
- 明确要求删除、替换或补充哪些文件。
- 保留审核通过的内容，禁止要求全部重新上传。
- 提供再次提交、上一步和保存草稿。

### Terminated

- 使用 Error 语义说明流程已中止。
- 解释原因和可联系渠道。
- 不展示仍可继续提交的主按钮。

# 10. Status Result Pattern

## Purpose

用于审核中、成功、失败、中止以及其他无法继续操作的阶段性结果。

## Structure

```text
Progress Context（可选）
→ Existing Empty/Status Illustration
→ Status Title
→ Explanation
→ Time / Consequence / Contact
→ One Primary or Secondary Action
```

## Rules

- 选择 Design System 中语义匹配的为空插画。
- 标题回答“发生了什么”，说明回答“为什么、多久、接下来做什么”。
- 审核中提供预计时长。
- 失败/中止提供原因、恢复路径或联系渠道。
- 成功结果提供下一任务入口。
- 最多一个 Primary Action；不需要强转化时使用 Secondary。

# 11. Dropdown / Action Sheet Pattern

## Desktop

- Dropdown 锚定触发器。
- 操作菜单与选择菜单分开。
- 危险动作位于菜单底部，并使用 Danger 语义。
- 长列表允许滚动和搜索。
- 菜单默认靠近触发器并优先向下展开；空间不足时允许反向展开。
- Dropdown Item 的辅助说明只能位于主标题右侧或下方。
- 选择、搜索或异步加载失败时，在菜单内保留已选值并提供 Empty / Error / Retry。

## Mobile

- 操作菜单转换为 Action Sheet。
- 选择菜单转换为带标题、关闭按钮和明确选择区的 Bottom Sheet。
- Sheet 使用遮罩，关闭后焦点返回触发器。

## Forbidden

- 在同一菜单混合对象操作和字段选择。
- Mobile 使用超出屏幕宽度的浮动 Dropdown。
- 将复杂表单塞入 Dropdown。
- 将危险动作与普通选择项并排放置，或只依靠红色表达风险。

# 12. Modal / Sheet Pattern

## Small-content Modal

适用于确认、短说明和少量字段。

- Desktop：居中 Modal。
- Mobile：内容仍很短时可使用 Modal，但宽度适配安全边距。

## Large-content Modal

适用于较多字段、较长说明或需要滚动的任务。

- Desktop：Modal。
- Mobile：转换为全宽/近全屏 Bottom Sheet。

## Rules

- Header、Body、Footer 分区稳定。
- Body 独立滚动，Footer 操作保持可见。
- Desktop Footer 通常横排；Mobile 可转为纵向或全宽按钮。
- 禁止嵌套 Modal。
- 提交 Loading 时保持尺寸并阻止重复提交。
- Modal 打开后背景不可操作，焦点进入 Modal；关闭后焦点返回原触发器。
- Error 在内容区就地呈现，并保留用户已输入内容和当前上下文。
- Esc 或点击遮罩关闭只适用于可安全取消的任务。
- Modal / Dialog 内出现 Empty State 时，插画必须放在 Body 区域，并以插画 Main Component 默认宽高的 `0.5×` 等比例显示；移动端对应 Sheet 沿用同一规则。具体计算与边界见第 15 章「Empty Illustration Sizing」。

## Popconfirm Selection

- 简短、低复杂度确认优先使用 Popconfirm；强中断、高风险或需要完整说明时使用 Modal。
- Popconfirm 根据文案长度选择既有宽度：

  | Size | Width | 文案长度与场景 |
  |---|---:|---|
  | `sm` | 160 | 10 字以内；简短提示或验证信息 |
  | `md` | 240 | 11–20 字；功能说明或操作提示 |
  | `lg` | 320 | 21–30 字；重要信息说明或指导 |
  | `xl` | 420 | 30 字以上；完整政策或复杂流程说明 |

- 高风险确认文案必须明确对象、金额或作用范围、操作后果和确认动作。
- `Cell/Header`、`Cell/Bottom` 等内部结构不得脱离 Modal / Sheet 单独使用。

# 13. Drawer / Mobile Sheet Pattern

## Desktop

Drawer 从右侧进入，在保留底层页面上下文时展示详情或编辑任务。

## Mobile

转换为带遮罩的全宽 Sheet；不保留狭窄的右侧抽屉形态。

## Rules

- Header/Footer 固定，Body 滚动。
- 关闭后恢复底层页面位置和焦点。
- 简单确认使用 Popconfirm/Modal，不使用 Drawer。
- 长表单若失去底层上下文价值，应改为独立页面。

# 14. Date Picker Responsive Pattern

## Desktop

- 日期、月份、年份选择使用锚定浮层。
- 日期区间必须同时显示起止关系。
- 支持 Current、Hover、Selected、Disabled。
- 高频日期范围可以提供快捷选择，但必须保留自定义日期入口。
- 日期与时间必须明确格式、时区和不可选范围。
- Current 只表示今天，不得与 Selected 混淆。

## Mobile

- 转换为 Bottom Sheet。
- 日期/月份/年份使用适合单列操作的面板。
- 日期区间可以分步骤选择开始与结束日期。
- 提供明确确认和取消；不能仅点击遮罩完成提交。
- 浏览月份或预览区间时不得提前写入字段；只有完成选择或明确确认后才提交。

# 15. Empty, Error & Permission Pattern

## Empty

- 首次无数据：解释价值并提供创建/开通动作。
- 筛选无结果：保留筛选条件，优先提供“清空筛选”。
- Table Empty：保留表头与页面上下文。
- 使用「08-05 为空插画」中语义匹配的现有插画，禁止自造、拼接或改色。
- Empty State 是 Illustration + Title + Description（可选）+ Action（可选）的组合 Pattern，不得声称存在完整 Empty State master。
- 最多提供一个 Primary Action；次要动作使用 Link 或 Secondary。
- 数据为空、筛选无结果、无权限、系统异常和业务结果必须使用不同语义。
- Placeholder 只表示加载或资源占位，不得替代 Empty State。

### Empty Illustration Sizing

本规则只约束空态插画实例的显示尺寸，不改变 Empty State 的标题、说明、操作、容器尺寸或间距 Token。

- 适用范围：Table 数据区域的空状态、Desktop Modal / Dialog 的空状态，以及其在移动端转换后的 Sheet 空状态。
- 尺寸计算：`显示宽度 = Main Component 默认宽度 × 0.5`；`显示高度 = Main Component 默认高度 × 0.5`。
- 计算基准必须是插画 Main Component 的默认宽高，不得基于已经缩放的 Instance 再次计算，避免重复缩小。
- 必须等比例缩放，保持原始宽高比；禁止拉伸、裁切、改变图形结构或通过近似手工尺寸代替计算值。
- 示例：Main Component 为 `300 × 228` 时，页面显示尺寸为 `150 × 114`。
- 仅缩放 Illustration；Title、Description、Action 及其间距继续使用已有 Typography、Spacing、Button 和布局 Token。
- Table Empty 在数据区域内水平、垂直居中，同时保留 Table Header 与筛选上下文；空态时隐藏 Pagination。
- Modal / Dialog Empty 必须放入 Body 区域并居中，不改变 Modal 既有宽度以及 Header、Footer 结构。
- 使用 Auto Layout 完成居中和内容撑开，禁止通过绝对定位摆放插画。
- 本规则不默认覆盖独立结果页、页面级空状态和 Drawer 空状态；这些场景继续遵循各自 Pattern，除非另有明确尺寸规则。

## Error

- 字段错误：Inline Error。
- 模块加载失败：模块内 Error + Retry。
- 页面级异常：Status Result。
- 提交失败：保留输入、文件和当前步骤。
- 系统级阻断才使用 Modal；短暂、非阻断反馈不得升级为阻断式 Overlay。

## Permission

- 无权限操作优先隐藏。
- 若用户需要理解权限差异，使用 Disabled + 原因说明。
- 不允许点击后才告知无权限。
- 禁用状态必须同时取消交互并保持原因可获取，不能只降低透明度。

# 16. Business Data Rules

## Money

- 格式为 `Currency Code + Amount`，例如 `USD 4,500.00`。
- 汇总金额标注估值币种。
- 同一列小数位和对齐方式一致。
- 不用颜色代替正负、收入/支出或成功/失败。

## Identifier

- 交易号、订单号、流水号保持可复制。
- Table 中可省略显示，但 Tooltip/详情必须提供完整值。

## Date & Time

- 列表可分两行显示日期与时间。
- 详情使用完整时间。
- 跨地区业务需要明确时区。

## Status

- 使用稳定 Tag 语义。
- 状态必须同时具备文字；关键流程可增加图标或 Step。
- 状态名称与可执行操作必须匹配。

# 17. Cross-pattern Component Rules

本章约束会跨越 List、Detail、Form、Dashboard 和 Overlay 的组件组合方式。组件的视觉属性、Variant 和 Token 仍以 `Design-System.md` 为准。

## 17.1 Action Hierarchy & Button Group

- 按钮类型只使用现有 `Primary`、`Default`、`Ghost`、`Danger`、`Icon`。
- 一个页面任务、模块任务或 Overlay Footer 最多一个 Primary Button。
- Default 用于普通次要操作；Ghost 用于低优先级轻操作；Danger 只用于危险或不可逆操作。
- Icon Button 只用于含义稳定的通用功能，并必须同时提供 Tooltip 和可访问名称。
- 图标必须帮助表达操作含义，禁止为了装饰而添加图标。
- 所有按钮检查 Default、Hover、Active、Disabled、Loading；键盘操作还必须具备可见 Focus。
- Loading 保持按钮原有宽度、阻止重复提交，并持续反馈操作正在进行。
- 长按钮文案使用截断；Hover / Focus 时通过 Tooltip 提供完整内容。
- 普通按钮宽度随内容自适应，并遵守既有最小宽度：

  | Size | 最小宽度 | Usage |
  |---|---:|---|
  | Large | 88 | 高强调页面操作 |
  | Regular | 76 | 默认按钮 |
  | Small | 56 | 紧凑操作区 |
  | Text | 44 | 文字弱操作 |

- 强转化或支付确认操作使用既有 240px 固定宽度或 100% 容器宽度，不创建新的 CTA 宽度。
- 同一 Button Group 内尺寸保持一致；水平排列时次操作在左、主操作在右，垂直排列时主操作在上。

## 17.2 General Form Field Composition

- 使用 `01_表单（顶对齐）`、`02_表单（左对齐）` 或 `03_表单（右对齐）`，不得拆复制内部图层制造 Input。
- Label、必填、帮助、单位、字数和错误信息通过 Form Properties 控制。
- `Fields` 容器统一使用纵向 Auto Layout `Gap = 24`；单个 Field 内部间距沿用组件固有设置。
- 固定字段宽度只使用 134 / 280 / 426 / 572；响应式场景使用 Fill Container。
- Field Error 紧邻控件显示；修复后及时清除，但提交失败仍保留输入和页面上下文。
- 长表单按业务主题分 Section，不使用没有分组的连续字段列表。

## 17.3 Selection Control

- 2–6 个互斥短选项可以使用 Radio 或分段选择；大量或复杂选项使用 Select / Dropdown。
- Radio Group 至少包含两个选项；单个确认条件使用 Checkbox。
- Switch 只用于切换后立即生效的二元设置；需要统一“保存/提交”的选项不得使用 Switch。
- 高风险 Switch 在切换前说明后果并按风险等级增加确认。
- Disabled 项保持含义与当前状态可辨，但不响应交互。

## 17.4 Feedback Routing

| 信息范围 | 组件 / Pattern | 规则 |
|---|---|---|
| 字段 | Inline Error | 紧邻字段，说明原因与修复方式 |
| 模块 | Alert / Module Error | 保留模块位置并提供 Retry |
| 短暂非阻断反馈 | Toast | 用于轻量成功或状态确认 |
| 异步重要信息 | Notification | 可稍后到达并保留必要操作 |
| 系统级阻断 / 高风险确认 | Modal / Popconfirm | 明确影响、对象和确认动作 |

- Loading、Empty、Error、Permission 都必须保留用户当前筛选、输入和任务上下文。
- 状态必须同时包含文字、图标或结构提示，禁止只依赖颜色。

## 17.5 Tooltip & Tag

- Tooltip 只用于图标含义、截断全文或非关键辅助说明；必须阅读的信息常驻展示。
- Tooltip 同时支持 Hover 与 Focus，并允许通过 Blur / Esc 关闭。
- 复杂说明使用 Popover、Alert 或独立说明区，不把长流程说明塞入 Tooltip。
- Tag 只表达稳定的状态、分类或筛选条件，不得代替 Button。
- 只有可清除或可跳转的 Tag 才使用 Hover / Active 外观。
- 同一区域 Tag 过多时折叠，避免使用大量颜色制造层级。

## 17.6 Navigation Semantics

- Tabs 只用于同层级内容切换，不表达有依赖关系的步骤。
- Steps 用于有明确先后顺序、完成关系或阻断关系的流程。
- Breadcrumb 表达页面层级，不作为页面内状态切换控件。
- 当前、已完成、未完成和 Disabled 必须有文字、图标或结构差异，不能只改变颜色。

# 18. Pattern Selection Matrix

| 业务目标 | 必选 Pattern | 可选 Pattern |
|---|---|---|
| 查看资金与币种 | Application Shell + Funds Overview | Dashboard、Empty |
| 查询交易/订单 | Application Shell + Data List | Summary Metrics、Batch Action |
| 管理银行账号 | Application Shell + Card List | List Variant、Permission |
| 查看交易详情 | Application Shell + Detail | Timeline、Risk Action |
| 企业/网站接入 | Multi-step Onboarding | Draft & Resume、Material Upload |
| 等待审核 | Status Result | Progress Context |
| 修正被拒材料 | Material Upload & Review | Alert、Draft & Resume |
| 桌面弹层转移动端 | Responsive Transformation | Modal/Sheet、Drawer/Sheet、Action Sheet |

# 19. AI Usage Rules

AI 设计页面前必须：

1. 识别用户任务，不以页面名称代替任务分析。
2. 从本文件选择一个主 Pattern 和必要的辅助 Pattern。
3. 从 `Design-System.md` 映射实际 Component、Variant 和 Token。
4. 检查 Desktop / Compact / Mobile 的结构转换。
5. 覆盖 Loading、Empty、Error、Disabled、Permission 和业务状态。
6. 明确哪些内容来自现有组件，哪些是组合 Pattern。

AI 输出页面方案时必须列出：

- Page Type
- Primary Pattern
- Supporting Patterns
- Information Architecture
- Component Mapping
- Responsive Behavior
- State Coverage
- Risk & Permission Rules
- Missing Component / Extension

# 20. Validation Checklist

## Structure

- [ ] 页面只有一个明确主任务。
- [ ] 使用了正确的 Application Shell。
- [ ] Section 顺序符合用户任务。
- [ ] 页面级、模块级和字段级操作没有混放。

## Components

- [ ] 优先使用现有 Component Instance。
- [ ] Variant 与业务状态匹配。
- [ ] 没有复制组件内部图层制作相似控件。
- [ ] 不存在的能力已标记为组合 Pattern 或需扩展。
- [ ] 一个任务区最多一个 Primary Button，Button Group 顺序与响应式方向正确。
- [ ] Fields 容器 Gap 为 24，字段宽度只使用既有 Width 规则或 Fill Container。

## Responsive

- [ ] Desktop、Compact Desktop、Mobile 均有明确转换。
- [ ] Mobile 没有简单缩小桌面页面。
- [ ] Dropdown、Modal、Drawer、Date Picker 使用正确移动形态。
- [ ] 关键任务和风险信息在窄屏仍可见。
- [ ] 不大于 375px 时，Button Group 已转为垂直且按钮宽度为 100%。

## Data & State

- [ ] 金额含币种且格式一致。
- [ ] 状态不只依赖颜色。
- [ ] Loading、Empty、Error、Disabled、Permission 完整。
- [ ] 失败后保留用户输入和上下文。
- [ ] 高风险操作明确对象、金额、后果和确认方式。
- [ ] 反馈组件按字段、模块、短暂反馈、异步通知和系统阻断的范围正确选择。

## Accessibility

- [ ] 键盘焦点可见。
- [ ] Overlay 关闭后焦点返回触发器。
- [ ] 图标按钮具有可访问名称。
- [ ] 文本与状态在缩放和多语言下保持可读。

---

## Responsive Auto Layout（强制）

本章节基于飞来汇现有 B 端资金、交易、收付款、详情、表单、卡片列表、登录及 FlyLink 页面结构归纳，用于约束页面在宽度变化、内容增减和高度变化时的自适应行为。

### 1. 组件库参数优先规则（最高优先级）

页面使用的字体、字号、字重、行高、颜色、间距、圆角、描边、阴影、图标尺寸、组件高度和其他视觉数值，只要组件库已经提供对应的 Component、Variant、Property、Variable、Style 或 Token，就必须直接调用或绑定组件库定义。

必须：

1. 优先使用组件实例，不得用基础图形重画已有组件。
2. 优先绑定已有 Variable、Style 和 Token，不得重新录入相同数值冒充 Token。
3. 组件已有 Variant 或 Property 时，必须通过属性切换，不得解除实例后手工修改样式。
4. Spacing、Padding、Gap、Radius、Shadow、Typography 和 Color 均遵循组件库语义参数。
5. Pattern 中出现的数值只说明布局关系；组件库存在对应参数时，以组件库实时值为准。
6. 组件库参数更新后，页面应通过绑定关系自动同步，不得保留私有副本。

禁止：

- 创建与现有 Token 数值相同但名称不同的局部变量。
- 为了视觉对齐，手工覆盖组件内部字体、颜色、间距或圆角。
- 将复制出来的颜色值、字号或间距值视为新的规范。
- 未获得组件库维护授权时新增或修改 Component master、Variables、Styles 或 Tokens。

例外：

- 组件库缺少完整容器，但已有组件可以组合时，使用 Composition Pattern。
- 无法通过已有组件或组合完成时，标记 Needs Extension，记录缺失能力、适用场景、建议属性和影响范围；不得直接创建正式组件或新 Token。

### 2. 标准桌面页面骨架

标准设计视口以 1440px 为基准，但 1440px 只用于 Figma 画板展示，不代表运行时固定宽度。

```text
Page Shell：Horizontal
├── Left Navigation：180 Fixed Width / Fill Height
└── Workspace：Vertical / Fill Width / Fill Height
    ├── Top Navigation：Fill Width / 68 Fixed Height
    └── Body Region：Vertical / Fill Width / Fill Remaining Height
        ├── Horizontal Padding：16
        ├── Module Gap：16
        └── Content Canvas：Vertical / Fill Width
            ├── Padding：24
            ├── Section Gap：16 或组件库对应 Token
            └── Modules：Fill Width / Hug Height
```

标准 1440px 页面下，内容净宽度通常为：

```text
1440 - 180 左侧导航 - 32 内容区外边距 - 48 主内容 Padding = 1180px
```

1180px 是标准画板下的计算结果，不得写死为所有运行环境的唯一内容宽度。

### 3. 页面层级设置

| 层级 | Direction | Width | Height | 规则 |
|---|---|---|---|---|
| Page Shell | Horizontal | 设计画板 Fixed；运行时 100% | Min viewport height | Fixed 只表示测试视口 |
| Left Navigation | Vertical | 180 Fixed | Fill | 不随正文压缩 |
| Workspace | Vertical | Fill | Fill | 承接剩余空间 |
| Top Navigation | Horizontal | Fill | 68 Fixed | 不被正文撑高 |
| Body Region | Vertical | Fill | Fill Remaining | 页面主要滚动区域 |
| Content Canvas | Vertical | Fill | Hug 或 Fill | 根据页面类型选择 |
| Section / Module | Vertical | Fill | Hug | 禁止无依据固定高度 |
| Row | Horizontal | Fill | Hug | 子项按业务使用 Fill/Hug |
| Text / Label / Tag | 组件定义 | Hug 或 Fill | Hug | 多行文本自动增高 |

必须先建立父级 Auto Layout，再设置子级尺寸。禁止先用绝对坐标摆放，最后再套 Auto Layout。

### 4. Fill、Hug、Fixed

#### 4.1 Fill Container

用于 Workspace、Body Region、Content Canvas、页面级 Section、列表、表格、卡片列表、筛选、详情、摘要区域、普通输入框、等宽字段、等宽卡片和贯穿父容器的分隔线。

#### 4.2 Hug Contents

用于标题、正文、标签、状态、说明、操作按钮组、内容高度不确定的卡片、详情 Section、表单主体、错误提示、辅助说明、多行文案和长页面模块。

#### 4.3 Fixed

仅用于 Figma 测试画板、导航规格、图标头像、基础控件高度、组件库明确规定的按钮/Modal/Drawer、表头与表格行、固定比例媒体和业务最小卡片宽度。

禁止为了画板整齐而固定页面内容、Section、表单或普通卡片的总高度。

### 5. 页面宽度适配

1. 数据列表、Dashboard、详情页和卡片列表默认 Fill 可用工作区。
2. 聚焦型表单、支付确认、登录表单可使用组件库规定的最大宽度并居中。
3. 页面不得将 Content Canvas 永久固定为 1180px。
4. 更宽视口下，数据密集页面允许扩展；聚焦型内容保持最大可读宽度。
5. 宽度不足时优先换列、换行、折叠次要操作，不得把控件压缩到不可使用。
6. 文本默认自动高度；只有明确要求单行截断的数据列才允许固定宽度和省略号。

### 6. Spacing 语义层级

所有数值必须优先绑定组件库 Spacing Token。下表仅说明语义层级：

| 间距层级 | 使用场景 |
|---:|---|
| 4 | 图标与文字、Tag 内部、紧密信息 |
| 8 | 组件内部、Label 与控件、说明文字 |
| 12 | 卡片子区域、操作按钮组 |
| 16 | 页面模块、筛选换行、普通卡片 Grid |
| 20 | 业务卡片 Grid，仅在对应 Pattern/Token 已定义时 |
| 24 | 页面内容 Padding、Section、表单字段间距 |
| 32 | 大模块内部层级 |
| 40 | 登录、引导等聚焦型页面的大段落间距 |

页面层禁止使用负 Gap。组件内部因描边叠合产生的负间距不得提升为页面规则。

### 7. Wrap 自适应

#### 7.1 筛选区域

```text
Filter Container
- Direction：Horizontal
- Wrap：On
- Width：Fill
- Height：Hug
- Column Gap：16 Token
- Row Gap：16 Token
```

- 字段使用 Fill，并设置组件库允许的最小宽度。
- 标准内容宽度下优先 4 列；紧凑宽度下自动变为 3 列或 2 列。
- 查询、重置占据一个栅格单元，或换行后右对齐。
- 禁止通过持续缩小输入框维持单行。

#### 7.2 卡片列表

```text
Card Grid
- Direction：Horizontal
- Wrap：On
- Width：Fill
- Height：Hug
- Gap：组件库 Grid/Spacing Token
```

- 同一行卡片等宽并使用 Fill。
- 卡片设置业务可用的最小宽度。
- 标准桌面优先 3 列，紧凑桌面 2 列，窄屏 1 列。
- 卡片高度默认 Hug；需要同一行等高时使用 Stretch。
- 禁止逐张写死不同宽度或高度。

#### 7.3 详情信息

- Horizontal + Wrap，标准桌面优先两列，两列字段 Fill。
- 使用组件库 Section Gap。
- 备注、附件、时间线、长文案默认跨整行。
- 奇数个字段的最后一项可跨整行，不使用空白 Frame 占位。

#### 7.4 Tag 与操作区

- Tag Group 使用 Wrap，并调用 Tag 组件内部 Gap。
- 主操作保持可见，次要操作空间不足时进入 More。
- 操作栏左侧区域 Fill，分页器 Hug/Fixed。
- 紧凑宽度下分页器允许换到下一行。
- 不得因操作过多压缩主要数据区域。

### 8. 高度与滚动

#### 8.1 短页面

- Page Shell 使用视口最小高度。
- Body Region 使用 Fill Remaining。
- 空态或结果区域使用 Fill Remaining，并在剩余空间内居中。
- 禁止使用空白 Frame 撑满画板。

#### 8.2 长表单和详情页

- Content Canvas 使用 Vertical + Hug Height。
- Section 使用 Hug Height。
- 页面高度由内容、校验提示和展开状态决定。
- Workspace 或 Body Region 作为唯一主纵向滚动容器。
- Top Navigation 固定高度；左侧导航至少填满视口。
- 禁止把长内容强制塞入固定高度导致裁切或覆盖。

#### 8.3 列表页

- 筛选区、摘要区、列表标题使用 Hug Height。
- 表头和数据行使用组件规定高度。
- 数据容器按场景使用 Hug 或 Fill Remaining。
- 分页跟随列表末尾，不使用画板绝对坐标。
- Empty State 占据数据区域剩余高度，空态时隐藏分页。

#### 8.4 Sticky 与底部操作

- 仅长表单、Drawer、Modal 或强制提交流程允许 Sticky 操作区。
- Sticky 区必须在正文中预留等高底部 Padding。
- 页面不得同时出现两个竞争的纵向主滚动容器。

### 9. 响应宽度分级

断点优先根据 Content Canvas 的实际可用宽度判断：

| 可用内容宽度 | 布局规则 |
|---:|---|
| ≥1180 | 标准桌面：筛选 4 列、卡片 3 列、详情 2 列 |
| 760–1179 | 紧凑桌面：筛选 2–3 列、卡片 2 列、次要操作收起 |
| <760 | 窄屏：单列、卡片 1 列、操作换行 |
| 约 390 | 移动方案：重新组织页面，不缩放桌面画板 |

阈值属于 Pattern 响应规则，不得创建为新的组件库 Token；组件库后续定义正式 Breakpoint 时，以组件库为准。

### 10. 移动端转换

- 移动端不是桌面画板的等比缩小版。
- 左侧导航改为收起导航、抽屉或移动端入口。
- 多列内容改为单列；Banner 可隐藏、裁切或弱化。
- 表单和按钮 Fill 可用宽度。
- 顶部状态区、底部安全区和键盘遮挡必须纳入布局。
- 表单主体 Hug Height；键盘弹起时当前字段和主按钮必须可见。
- 未明确要求移动端的 B 端页面不得擅自生成移动版；至少完成 Desktop 与 Compact Desktop 验证。

### 11. 设计文档与产品页面边界

- 设计文档 Page/Section 可以自由排列画板、说明和流程箭头。
- Screen 层必须建立页面 Auto Layout。
- Module 层必须使用 Fill/Hug、Wrap 和组件库间距。
- Component 层必须遵循自身 Variant、Property 和 Token。
- 不得把设计文档画板的自由坐标结构复制为产品页面实现。

### 12. 禁止规则

1. 禁止把 1440×800 当作唯一运行尺寸。
2. 禁止将 Content Canvas 固定为 1180px 且不允许扩展。
3. 禁止给普通 Section 设置没有业务依据的固定高度。
4. 禁止用绝对坐标排列表单、筛选项、卡片和操作。
5. 禁止通过压缩字段维持单行。
6. 禁止用空白 Frame 撑开页面或补齐 Grid。
7. 禁止页面级负 Gap。
8. 禁止内容增加后手动调整后续模块 Y 坐标。
9. 禁止使用组件库外的字体、颜色、间距、圆角、阴影和尺寸参数。
10. 禁止将移动端设计成桌面页面的缩小版。

### 13. Auto Layout 验收清单

每个页面至少完成：

1. 将画板从 1440 调整到 1280，确认主要模块无溢出。
2. 调整到 1024，确认筛选和卡片自动换列。
3. 将标题、字段和说明增加到原长度两倍，确认高度自动增长。
4. 显示错误、辅助说明和展开内容，确认后续元素自动下移。
5. 删除一个重复项，确认剩余元素自动补位。
6. 增加一个重复项，确认容器自动换行或增高。
7. 切换 Empty State，确认空态填充剩余区域且分页隐藏。
8. 检查页面级容器为 Fill、内容型容器为 Hug。
9. 检查主操作在紧凑宽度下始终可见。
10. 检查长页面只有一个明确主滚动容器。
11. 检查字体、颜色、间距、圆角、阴影和组件尺寸均来自组件库绑定。
12. 检查不存在因展示画板固定高度造成的内容裁切。
