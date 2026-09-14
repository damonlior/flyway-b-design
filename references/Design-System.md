# 飞来汇 B 端 Design System V2.0

> 来源：Figma 文件「❖ 飞来汇设计规范 B端 V2.0」  
> 扫描日期：2026-07-21  
> 文件 Key：`mT4aiPr8CZ5l5S0na8qb4p`  
> 说明：本文以 Figma 本地 Variables、Styles、Component / Component Set、示例页和规则页为事实来源。标注为“推导”的内容是对现有资产的系统化归纳，不代表 Figma 中已有同名组件。

## 0. 扫描摘要

| 项目 | 数量 | 备注 |
|---|---:|---|
| Pages | 93 | 67 个非空页面；其余主要为分组标题或待建设页面 |
| Variable Collections | 14 | Color、Spacing、Radius、Font、WidthSize、业务数据等 |
| Variables | 507 | 包括 85 个语义颜色、152 个 Primitive，以及业务枚举变量 |
| Local Styles | 34 | Text 18、Effect 3、Grid 13、Paint 0 |
| Component Sets | 112 | 含基础、表单、反馈、导航、业务封装和图标集合 |
| Component masters | 1,384 | 1,149 个 Variant Component + 235 个独立 Component |
| 可复用主资产总数 | 1,496 | Component Set + Component master；不含实例 |

扫描覆盖：93 个页面均完成结构读取；67 个非空页面已逐页统计，未出现读取失败。数量仅统计当前文件的本地资产，不把跨文件实例重复计为本地 Component master。

### 组件分类

1. Token：颜色、间距、圆角、字体、阴影、宽度、栅格、层级。
2. 图标与品牌：基础图标、业务图标、国家旗帜、银行、支付方式、联系人、Logo。
3. 基础通用：Button、Button Group、Link。
4. 信息录入：Form、Radio、Checkbox、Switch、Select、Date Picker、Rating、Upload、Dropdown、单位输入、步进器。
5. 信息容器：Modal、Sheet、Table、Drawer、Collapse。
6. 信息反馈：Dialog、Popconfirm、Notification、Toast、Alert、Progress。
7. 信息展示：Tag、Badge、Tooltip、Placeholder、Preview。
8. 导航布局：Tab、Breadcrumb、Pagination、Anchor、Steps、Timeline、Scrollbar。
9. 业务封装：国家地区、币种金额、收款人、汇率提醒/日历、安全验证、验证码、银行卡、引导、授权、汇率趋势、运营弹窗。
10. 页面模板：邮件、操作结果和示例页。

### 成熟度与缺口

- Card 与 Slider 页面标记为“建设中”且无本地组件。
- Input 页面只有规则示例，输入控件实际封装在 Form 组件中；AI 不应臆造独立 Input master。
- 已新增「08-05 为空插画」资产页，包含 34 个通用/业务插画实例与 4 个资金类状态实例；但当前文件仍没有本地 Empty State 容器 Component Set，也未发现这些插画对应的本地主组件。
- 未发现正式 KPI Card、Chart 或 Dashboard Component Set；Dashboard Pattern 只能作为受控推导模式。
- Paint Style 为 0；颜色必须从 Color Variables 使用，不能用不存在的 Paint Style 名称。
- 组件属性中存在少量 Figma `SLOT` 属性；实现侧需映射为内容插槽，不能误当成 Variant。

# 1. Design System Overview

## 1.1 产品定位

该系统面向跨境支付、收付款、换汇、账户、银行卡及企业资金操作等 B 端金融业务。依据来自币种金额、收款人、银行账户、汇率、安全验证、银行卡和交易表格等业务组件。

## 1.2 设计风格

- 高信息密度、低装饰、任务导向。
- 以紫色 `#5548FF` 为品牌和主操作色，灰蓝中性色承载结构与数据。
- 卡片和容器以白色/浅灰表面、轻边框和轻阴影建立层级。
- 风险、成功、预警、提示各自使用独立语义色，避免仅靠文案表达状态。
- 支持 Light / Dark 语义模式，颜色通过 Semantic → Primitive 别名链解析。

## 1.3 适用业务场景

- 交易与订单列表、入账、付款、收款人管理。
- 企业账户、银行卡、银行信息与支付方式管理。
- 换汇、汇率趋势、价格日历和汇率变化提醒。
- 风控、安全校验、验证码、授权和高风险操作确认。
- 多国家地区、多币种、多语言的企业后台。

## 1.4 用户角色

- 企业财务、出纳、资金运营人员。
- 审批人、管理员和权限配置人员。
- 风控、合规、客服和运营人员。
- 需要批量处理和审阅高密度数据的专业用户。

## 1.5 设计原则

1. **效率优先**：高频操作就近呈现，批量操作与分页固定在数据上下文中。
2. **语义一致**：颜色、文字、间距、状态和组件只使用已有 Token 与 Variant。
3. **风险可感知**：危险操作使用 Danger 语义、二次确认和明确后果说明。
4. **渐进披露**：次要说明、更多操作和复杂选项按需展开。
5. **可扫描**：表格、表单和详情均保持稳定对齐与可预测层级。
6. **跨端一致**：Desktop 与 Mobile 使用同一语义体系，但采用不同 Grid、容器和 Overlay 形态。

## 1.6 核心体验目标

- 用户能快速定位数据、理解状态、完成批量任务。
- 高风险金融操作有足够确认与反馈，不产生不可逆误操作。
- 长流程表单可预期、可恢复、错误可定位。
- 多语言、多币种和长文本下仍保持稳定布局。

# 2. Foundations（基础设计规范）

## 2.1 Color System

### 颜色架构

颜色分为 Primitive 与 Semantic 两层。页面和组件必须引用 `Color` 集合中的 Semantic Token；`_Primitives` 仅供语义别名使用。Light / Dark 切换时不得在页面层手工替换色值。

| 语义 | Token | Light | Dark | 使用场景 | 限制 |
|---|---|---|---|---|---|
| Brand / Primary | `Basic/color-basic-primary` | `#5548FF` | `#5548FF` | 主按钮、焦点、关键选中 | 单个任务区只保留一个主操作 |
| Secondary | 无独立品牌 Token | — | — | 使用 Secondary-Outline 组件或 Neutral Surface | 禁止新建“Secondary Color” |
| Info | `Info/color-info` | `#3369FF` | `#3369FF` | 信息提示、处理中状态 | 不用于主 CTA |
| Success | `Success/color-success` | `#21A470` | `#21A470` | 成功、完成、已入账 | 不用于普通装饰 |
| Warning | `Warning/color-warning` | `#F98C1F` | `#F98C1F` | 预警、需关注状态 | 不等同于 Error |
| Error / Danger | `Danger/color-danger` | `#EA423B` | `#EA423B` | 错误、失败、危险操作 | 危险操作需配合确认文案 |
| Text Primary | `Text icon/color-text-icon-primary` | `#171717` | `#F5F5F5` | 正文、标题、默认图标 | 禁止用纯黑替代 |
| Text Secondary | `Text icon/color-text-icon-secondary` | `#38373D` | `#D2D1D8` | 次级正文 | 文件标注为“不常用” |
| Text Tertiary | `Text icon/color-text-icon-tertiary` | `#817F86` | `#817F86` | 辅助信息 | 不用于关键数值 |
| Text Quaternary | `Text icon/color-text-icon-quaternary` | `#A5A4AA` | `#5C5B61` | Placeholder、弱提示 | 需检查可读性 |
| Surface Primary | `Surface/color-surface-primary` | `#FFFFFF` | `#222126` | 卡片、基础容器 | 默认内容承载面 |
| Surface Secondary | `Surface/color-surface-secondary` | `#F1F2F5` | `#141318` | 页面底色、区分区块 | 不覆盖主要卡片 |
| Surface Subtle | `Surface/color-surface-subtle` | `#F7F8FB` | `#38373D` | 轻背景、筛选区 | 保持低对比 |
| Border Regular | `Line/color-line-border-regular` | `#E4E3EA` | `#38373D` | 输入框、卡片、分割 | 聚焦时换 Focus Token |
| Focus Border | `Line/color-line-border-focus` | `#5548FF` | `#5548FF` | Keyboard/输入焦点 | 不能仅靠颜色表达错误 |
| Disabled Text | `Disable/color-text-disable` | `#A5A4AA` | `#5C5B61` | 禁用文字图标 | 同时禁用交互 |
| Disabled Fill | `Disable/color-fill-disable` | `#ECECEC` | `#222126` | 禁用背景 | 不可表现为可点击 |
| Overlay | `Constant/color-constant-overlay` | `#00000080` | `#00000080` | Modal 遮罩 | 仅用于阻断式 Overlay |

### 状态色规则

- Hover 使用同语义族的 `-hover`；Active 使用 `-active`；Disabled 使用 `-disable`。
- 浅色信息面使用 `-light`，其交互仍使用 `-light-hover` / `-light-active`。
- Link 使用 `color-link`、`hover`、`active`、`visited`、`disable` 全链路，不直接复用 Primary 填充状态。
- Reverse Token 只用于深色/反差背景，不用于普通 Light Surface。
- 状态信息必须同时具备文字、图标或结构提示，不能只靠红/绿区分。

### Color Token Inventory（完整语义清单）

| Token | Light | Dark |
|---|---|---|
| Basic/color-basic-primary | #5548FF | #5548FF |
| Basic/color-basic-primary-hover | #483DD1 | #695EFF |
| Basic/color-basic-primary-active | #3E35AC | #7E74FF |
| Basic/color-basic-primary-disable | #CFCCFF | #332C87 |
| Basic/color-basic-primary-light | #F1F0FF | #1E1B3D |
| Basic/color-basic-primary-light-hover | #E4E2FF | #24204F |
| Basic/color-basic-primary-light-active | #CFCCFF | #332C87 |
| Basic/color-basic-primary-light-disable | #F1F0FF | #1E1B3D |
| Surface/color-surface-primary | #FFFFFF | #222126 |
| Surface/color-surface-subtle | #F7F8FB | #38373D |
| Surface/color-surface-secondary | #F1F2F5 | #141318 |
| Surface/color-surface-tertiary | #ECECEC | #0F0E12 |
| Surface/color-surface-hover | #0000000D | #FFFFFF0D |
| Surface/color-surface-active | #0000001A | #FFFFFF1A |
| Text icon/color-text-icon-primary | #171717 | #F5F5F5 |
| Text icon/color-text-icon-secondary | #38373D | #D2D1D8 |
| Text icon/color-text-icon-tertiary | #817F86 | #817F86 |
| Text icon/color-text-icon-quaternary | #A5A4AA | #5C5B61 |
| Line/color-line-separator-regular | #F1F2F5 | #303030 |
| Line/color-line-separator-dark | #E4E3EA | #38373D |
| Line/color-line-border-light | #F1F2F5 | #303030 |
| Line/color-line-border-regular | #E4E3EA | #38373D |
| Line/color-line-border-dark | #D2D1D8 | #5C5B61 |
| Line/color-line-border-focus | #5548FF | #5548FF |
| Disable/color-text-disable | #A5A4AA | #5C5B61 |
| Disable/color-text-light-disable | #E4E3EA | #222126 |
| Disable/color-fill-disable | #ECECEC | #222126 |
| Constant/color-constant-white | #FFFFFF | #FFFFFF |
| Constant/color-constant-black | #000000 | #000000 |
| Constant/color-constant-overlay | #00000080 | #00000080 |
| Constant/color-constant-Scrollbar | #0000004D | #0000004D |
| Constant/color-constant-transparency | #00000000 | #00000000 |
| Constant/color-constant-hover | #0000000D | #FFFFFF0D |
| Constant/color-constant-active | #0000001A | #FFFFFF1A |
| Info/color-info | #3369FF | #3369FF |
| Info/color-info-hover | #2D58D1 | #4B7BFF |
| Info/color-info-active | #284AAC | #648DFF |
| Info/color-info-disable | #C6D5FF | #233C87 |
| Info/color-info-light | #EFF3FF | #19213D |
| Info/color-info-light-hover | #E7EDFF | #1B284F |
| Info/color-info-light-active | #C6D5FF | #233C87 |
| Info/color-info-light-disable | #EFF3FF | #19213D |
| Success/color-success | #21A470 | #21A470 |
| Success/color-success-hover | #1E875E | #3CAF81 |
| Success/color-success-active | #1C7050 | #56BA92 |
| Success/color-success-disable | #C1E6D7 | #1A5942 |
| Success/color-success-light | #EDF8F4 | #162A26 |
| Success/color-success-light-hover | #DBF0E8 | #17362D |
| Success/color-success-light-active | #C1E6D7 | #1A5942 |
| Success/color-success-light-disable | #EDF8F4 | #162A26 |
| Warning/color-warning | #F98C1F | #F98C1F |
| Warning/color-warning-hover | #CB741E | #FA9A3A |
| Warning/color-warning-active | #A7601C | #FAA855 |
| Warning/color-warning-disable | #FDDFC0 | #824D1B |
| Warning/color-warning-light | #FFF6ED | #392619 |
| Warning/color-warning-light-hover | #FEEDDB | #4B301A |
| Warning/color-warning-light-active | #FDDFC0 | #824D1B |
| Warning/color-warning-light-disable | #FFF6ED | #392619 |
| Danger/color-danger | #EA423B | #EA423B |
| Danger/color-danger-hover | #BF3934 | #ED5953 |
| Danger/color-danger-active | #9D312E | #EF6F6A |
| Danger/color-danger-disable | #F9CAC8 | #7B2A29 |
| Danger/color-danger-light | #FDF0EF | #361B1E |
| Danger/color-danger-light-hover | #FCE1E0 | #471E20 |
| Danger/color-danger-light-active | #F9CAC8 | #7B2A29 |
| Danger/color-danger-light-disable | #FDF0EF | #361B1E |
| Link/color-link | #5548FF | #5548FF |
| Link/color-link-hover | #483DD1 | #695EFF |
| Link/color-link-active | #3E35AC | #7E74FF |
| Link/color-link-visited | #695EFF | #483DD1 |
| Link/color-link-disable | #CFCCFF | #332C87 |
| Surface reverse/color-surface-reverse-primary | #121212 | #FFFFFF |
| Surface reverse/color-surface-reverse-secondary | #141318 | #F1F2F5 |
| Surface reverse/color-surface-reverse-tertiary | #303030 | #E4E3EA |
| Surface reverse/color-surface-reverse-hover | #FFFFFF0D | #0000000D |
| Surface reverse/color-surface-reverse-active | #FFFFFF1A | #0000001A |
| Text icon reverse/color-text-icon-reverse-primary | #F5F5F5 | #171717 |
| Text icon reverse/color-text-icon-reverse-secondary | #D2D1D8 | #38373D |
| Text icon reverse/color-text-icon-reverse-tertiary | #817F86 | #817F86 |
| Text icon reverse/color-text-icon-reverse-quaternary | #5C5B61 | #A5A4AA |
| Line reverse/color-line-reverse-separator-regular | #38373D | #F1F2F5 |
| Line reverse/color-line-reverse-separator-dark | #5C5B61 | #E4E3EA |
| Line reverse/color-line-reverse-border-light | #38373D | #F1F2F5 |
| Line reverse/color-line-reverse-border-regular | #5C5B61 | #E4E3EA |
| Line reverse/line-reverse-border-dark | #817F86 | #D2D1D8 |

## 2.2 Typography

### Font Family

| 内容 | macOS / iOS | Windows | Harmony | Android |
|---|---|---|---|---|
| 中文 | PingFang SC | Microsoft YaHei | HarmonyOS Sans | Noto Sans |
| 英文 | SF Pro Text | Microsoft YaHei | HarmonyOS Sans | Roboto |
| 数字 | IBM Plex Sans Condensed | IBM Plex Sans Condensed | IBM Plex Sans Condensed | IBM Plex Sans Condensed |

### Type Scale（Normal Mode）

| Style / Token | Size | Weight | Line Height | Usage |
|---|---:|---:|---:|---|
| tag | 10 | 400 | 14 | 徽标数字、小型状态 |
| caption | 12 | 400 | 18 | 辅助说明、小号正文 |
| caption-B | 12 | 500 | 18 | 强调说明 |
| body | 14 | 400 | 20 | 默认正文、表格、表单 |
| body-B | 14 | 500 | 20 | 表头、Label、重点正文 |
| body-U / body-B-U | 14 | 400 / 500 | 20 | 带下划线链接或特殊强调 |
| body-l | 16 | 400 | 24 | 大号正文、Card 标题 |
| body-l-B | 16 | 500 | 24 | 强调大号正文 |
| body-xl | 18 | 400 | 26 | 页面次级标题 |
| heading-6 | 20 | 500 | 28 | 小节标题；Text Style 与 FontSize Token 已统一 |
| heading-5 | 24 | 500 | 34 | 页面标题 |
| heading-4 | 28 | 500 | 40 | 大标题 |
| heading-3 | 32 | 500 | 46 | 展示标题 |
| heading-2 | 48 | 500 | 68 | 运营展示 |
| heading-1 | 64 | 500 | 90 | 大型展示，后台页面慎用 |

规则：

- 默认 B 端正文使用 body 14/20，Label 和表头使用 14/20 Medium。
- 金额、汇率、统计数字优先使用 Number Family；表格数值右对齐并保持小数位一致。
- 字体粗细使用 Regular / Medium 为主；Bold 只用于强强调，不用粗体代替信息层级。
- 禁止新增字号；需要密度适配时切换 FontSize、LineHeight、FontWeight Mode。
- 本地存在 18 个 Text Styles；不得创建同值不同名的样式。

## 2.3 Spacing System

基础参照单位为 4px；`spacing-m = 8px` 是标准参照。1px/2px 仅用于微调和内部光学间距。

| Token | Normal | Spacious | Compact |
|---|---:|---:|---:|
| spacing-0 | 0 | 0 | 0 |
| spacing-2xs | 1 | 2 | 1 |
| spacing-xs | 2 | 4 | 2 |
| spacing-s | 4 | 8 | 4 |
| spacing-m | 8 | 12 | 8 |
| spacing-l | 12 | 16 | 10 |
| spacing-xl | 16 | 20 | 12 |
| spacing-2xl | 20 | 24 | 16 |
| spacing-3xl | 24 | 28 | 20 |
| spacing-4xl | 32 | 36 | 28 |
| spacing-5xl | 40 | 48 | 32 |
| spacing-6xl | 48 | 56 | 40 |
| spacing-7xl | 56 | 64 | 48 |
| spacing-8xl | 64 | 72 | 56 |

应用规则：

- 页面容器：Desktop 16；卡片内部 24；Mobile 容器 12、卡片 16。
- Card 间距：通常 16 或 24，取决于密度模式和内容层级。
- Component 内部：4/8/12/16；不得使用无 Token 的 6、10、14 等值，除非组件本身已有绑定。
- Form：字段组垂直 16–24；Label 与控件 8；错误说明紧邻控件。
- Table：行内左右 12–16；默认行高 52，复杂行使用现有 72/80/92/96 变体。

## 2.4 Radius & Shadow

### Radius

| Token | Normal | Small | Large | Full |
|---|---:|---:|---:|---:|
| radius-0 | 0 | 0 | 0 | 9999 |
| radius-2xs | 2 | 0 | 4 | 9999 |
| radius-xs | 4 | 2 | 8 | 9999 |
| radius-s | 6 | 2 | 10 | 9999 |
| radius-m | 8 | 4 | 12 | 9999 |
| radius-l | 10 | 6 | 14 | 9999 |
| radius-xl | 12 | 8 | 16 | 9999 |
| radius-2xl | 16 | 12 | 18 | 9999 |
| radius-3xl | 20 | 16 | 24 | 9999 |
| radius-4xl | 24 | 20 | 28 | 9999 |
| radius-full | 9999 | 9999 | 9999 | 9999 |

`radius-m = 8` 为标准。输入和小控件通常使用 xs/s；Card、Modal、Drawer 使用 m/xl；Tag、Badge 和圆形控制使用 full。

### Shadow

| Style | Effects | Usage |
|---|---|---|
| shadow-s | 0 2 6 / 8%；0 1 2 / 3% | Tooltip、Dropdown、轻浮层 |
| shadow-m | 0 8 20 / 4%；0 16 28 / 2%；0 0 8 / 5% | Popconfirm、浮层卡片、Drawer |
| shadow-l | 0 10 20 / 5%；0 20 28 / 4% | Modal、强层级浮层 |

阴影只表达层级，不替代边框或分组。页面常驻 Card 优先用 Surface + Border，避免堆叠大阴影。

# 3. Layout System（布局规范）

## 3.1 Screen 与内容宽度

| Token | Width |
|---|---:|
| Desktop Small | 1000 |
| Desktop Standard | 1440 |
| Desktop Large | 2560 |
| Desktop Extra Large | 3840 |
| Mobile Standard | 390 |

Figma 没有单独的“页面最大宽度”Token。标准桌面稿以 1440 为基准，内容区随侧栏和容器自适应；大型屏幕应使用居中容器或增加留白，不把表单无限拉伸。

## 3.2 Grid

- Desktop Container：24 columns，margin 16，gutter 16。
- Desktop Card：24 columns，margin 24，gutter 16。
- Desktop Large-density alternate：gutter 24。
- Mobile Container：12 columns，margin 12，gutter 16。
- Mobile Card：12 columns，margin 16，gutter 16。
- Desktop Form：内容宽度 572 / 720 / 900，居中或在卡片内按规则对齐。
- Table：单列伸展，卡片内 margin 24。

## 3.3 Auto Layout

- 页面、Card、筛选区、表单、操作区、表格工具栏必须使用 Auto Layout。
- 垂直页面结构用 Vertical；工具栏、按钮组、字段行用 Horizontal。
- 容器宽度优先 Fill，固定宽度只用于 Form、Drawer、Modal 和已定义列宽。
- 内容可变组件使用 Hug；长文本必须允许换行，不能以绝对定位维持对齐。
- Overlay 的 Header、Body、Footer 分层；Body 可滚动，Footer 保持操作可见。

## 3.4 典型后台布局

### Dashboard（推导）

- 使用 24 栏 Grid；KPI Card 以 4/6/8/12 栏组合。
- 第一屏顺序：页面标题与全局筛选 → KPI → 趋势/分布 → 数据表。
- 当前库没有正式 KPI Card / Chart 组件，AI 只能用已有 Card 结构和 Table 组合，不得声称复用了不存在的组件。

### List

- 左侧导航 + 内容卡片。
- 内容依次为全局 Alert（可选）、Tab、页面操作、Filter、Table、Pagination。
- 筛选区使用浅 Surface，字段标签置顶；主按钮在右侧，Reset 为弱操作。
- Table 与 Pagination 形成一个连续数据区域。

### Detail

- Breadcrumb → 页面标题/状态 → 关键操作 → Section。
- Section 使用标题 + 描述列表或 Card；复杂事件使用 Timeline。
- 危险操作与常规编辑分离，并置于页面尾部或独立风险区。

### Form

- 简单/移动表单用顶对齐；桌面密集表单可用左/右对齐。
- Form 内容宽度使用 572 / 720 / 900；单字段宽度使用 134 / 280 / 426 / 572。
- 主操作在表单底部；长表单可使用固定 Footer，但需避免遮挡错误信息。

# 4. Component Library Analysis（组件分析）

## Button

### Purpose

触发页面、模块或对象级操作。

### Variants

- Size：Large 48、Regular 40、Small 32、Text Link 24。
- Type：Primary-Filled、Secondary-Outline、Tertiary-Ghost、Primary-Filled-Reverse、Tertiary-Ghost-Reverse、Danger、Weak。
- State：默认、Hover、Active、Disabled、Loading。
- Content：文字、左右图标、纯图标；Button Group 支持横/竖向和 1–3 个按钮。

### Usage Rules

- 每个任务区最多一个 Primary-Filled。
- Secondary 用于并列次要操作；Tertiary/Weak 用于低优先级；Danger 用于危险动作。
- “极强”转化/支付确认操作使用固定 240 或 100% 宽度；普通按钮内容自适应且保留最小宽度。
- 禁止用多个 Primary 表达同等优先级；禁止用颜色自造按钮类型。

### Interaction Rules

Hover、Active、Disabled、Loading 已有完整变体。Loading 时保持原宽度并阻止重复提交；纯图标按钮必须提供 Tooltip/可访问名称。

## Input

### Purpose

文本、数字、单位、标签、搜索和文本域录入。当前文件未提供独立 Input master，统一由 Form 的 `_04_无标题` 与三种 Label 对齐组件封装。

### Variants / Properties

- Type：输入、搜索、文本域、前/后置单位、步进器、标签、标签多行、数字区间等。
- State：初始、激活、录入、禁用、录入激活、为空报错、录入报错。
- Boolean / Content：前缀图标、清除、字数、辅助说明、错误说明、单位、最多四个操作。
- 常规宽 280、高 40；紧凑控件 32；文本域高 128；错误状态附加 24–26px 信息区。

### Usage Rules

使用 Form 组件，不拆出并复制内部输入层。Label、必填、帮助、错误、字符数都由 Form Properties 控制。校验信息必须紧邻字段，不用 Toast 替代字段错误。

### Interaction Rules

Hover 仅提示可输入性；Focus / Active 使用焦点边框且不改变尺寸。Disabled 不可聚焦或提交。Loading 仅用于异步搜索/校验并保留输入值；Error 就地显示原因和修复方式，修复后及时清除。

## Select

### Purpose

用于有限选项、区域、高优选项和分段选项选择。标准下拉选择由 Form + Dropdown 组合；Select 页面主要提供区域选择、分段选择和高优项选择。

### Variants

- 区域：亚洲、欧洲、北美、南美、非洲、全球；状态含选中、禁用、默认/悬浮。
- 分段选择：2–6 项。
- 高优项：标题、说明、选中、禁用。

### Usage Rules

选项较多、需搜索或含复杂内容时使用 Dropdown；2–6 个互斥短选项可用分段选择。禁止把 Select 当作命令菜单。

### Interaction Rules

Hover 强调当前选项；Active / Selected 保持稳定勾选。Disabled 可见但不可操作；异步加载保持触发器尺寸并显示 Loading；加载或搜索失败在菜单内提供重试，不清空已选值。

## Date Picker

### Purpose

选择日期、日期区间、月份或年份。

### Variants

- 日历：日期、日期区间、月份、年份；可开启快捷选择。
- Item：默认、Hover、Selected、Current、Disabled。
- Form 状态：初始、激活、录入、禁用、录入激活、为空报错、录入报错。

### Usage Rules

交易查询默认使用日期区间并允许快捷选择；单日业务用日期。必须明确格式、时区和可选范围。禁用日期保持可见但不可选。

### Interaction Rules

Hover 预览可选日期；Active / Selected 明确区间起止与连续范围；Current 不等于 Selected。Disabled 日期不可响应。加载可用范围时显示 Loading；无效区间或超限时就地 Error，并保留用户当前选择。

## Dropdown

### Purpose

承载选择列表和对象级更多操作。

### Variants

- Item 预设：常规单/多选、国家地区、币种、状态标记、位置地址、收款人、操作。
- State：默认、禁用、Hover、Active；可带勾选、下级、前/后缀、描述与金额。
- Menu：单选、多选、国家、货币、带说明、地址；宽度 200/280/320。

### Usage Rules

菜单靠近触发器，优先向下展开；可视高度受限时滚动。危险命令分组并使用 Danger；不可将大量表单字段塞入 Dropdown。

### Interaction Rules

Hover 只高亮当前项；Active 执行或选择后按任务需要关闭。Disabled 保留原因说明。异步菜单显示 Loading / Empty / Error；Error 提供重试。键盘支持上下移动、Enter 选择、Esc 关闭并归还焦点。

## Checkbox / Radio

### Purpose

Radio 表达互斥单选；Checkbox 表达多选或独立布尔条件。

### Variants

类型、选中、禁用、部分选中；图标 16×16，选项行约 20 高，可带辅助说明。

### Usage Rules

Radio Group 至少 2 项；单个确认条件使用 Checkbox。部分选中只用于父子集合。点击区域覆盖图标与标签。

### Interaction Rules

Hover / Focus 覆盖完整标签点击区；Active 切换后即时反馈。Disabled 不响应且保持状态可辨。异步提交时可锁定整个 Group；校验失败在组选项下方显示 Error，不只改变边框颜色。

## Switch

### Purpose

立即生效的二元开关。

### Variants

44×24；On/Off × Enabled/Disabled。

### Usage Rules

用于即时设置，不用于需要“保存/提交”的表单选择；高风险开关需二次确认或说明后果。

### Interaction Rules

Hover / Focus 不改变开关尺寸；Active 后滑块与语义状态同步。Disabled 不可切换。远程保存时显示 Loading 或锁定并防止重复切换；失败回滚到原状态并显示 Error / Toast。

## Table

### Purpose

高密度结构化数据浏览、筛选、选择和批量操作。

### Variants / Properties

- Header：多选、排序、解释说明。
- Cell：单行、两行、金额、开关、商品、订单、可编辑表单、标签横/竖、图片、上传、规格、无数据。
- Action：1–4 个操作、更多操作和优先级。
- Toolbar：批量操作、选择范围、Pagination。
- Sort：默认、升序、降序。
- 默认行高 52；复杂行 72/80/92/96。列宽 Token：80/100/120/140/160/180/200/240/320/360/440/520。

### Usage Rules

- 数值右对齐，文本左对齐，状态用 Tag；操作列置右。
- 选择后才出现批量操作；Pagination 与统计保持在表格区域底部。
- 长文本省略并配 Tooltip；关键标识不应完全截断。
- 空表需保留表头和上下文，并从「08-05 为空插画」选择语义匹配的插画，同时提供恢复动作；当前无独立 Empty State 容器组件。

### Interaction Rules

Hover 突出当前行；Selected 使用稳定选中面；Sort 只能有一个主要排序状态。行内编辑必须明确保存/取消并处理 Error。

## Pagination

### Purpose

控制大数据集翻页。

### Variants

默认、迷你、极简；首/中/尾；可显示总数与前往页。页码单元 40×40，完整宽度约 707。

### Usage Rules

表格默认使用完整型；空间受限用迷你；连续浏览可用极简。第一页禁用上一页，末页禁用下一页；切页后保持筛选与排序。

### Interaction Rules

Hover / Focus 标识可点击页码；Active 显示当前页且不可重复触发。边界按钮 Disabled。切页期间保持分页宽度并显示表格 Loading；请求失败保留原页和筛选条件并提供重试。

## Modal

### Purpose

处理必须中断当前任务的确认、编辑或风险操作。

### Variants

- Desktop Modal：600×440 / 600×376；文本或图文；可选 Footer。
- Mobile Sheet：390×620 / 390×556。
- Header：默认/可返回；Footer：横向/竖向、桌面/移动，可包含 Checkbox 和说明。

### Usage Rules

仅用于强中断任务；长流程改用 Drawer 或独立页面。主操作右侧，取消在左；危险确认使用 Danger。禁止嵌套 Modal。

### Interaction Rules

打开后焦点进入 Modal，背景不可操作；Esc / 遮罩关闭仅用于可安全取消任务。提交进入 Loading 并阻止重复操作；Error 在内容区保留上下文。关闭后焦点返回触发器。

## Drawer

### Purpose

在保留页面上下文时处理详情或较长编辑任务。

### Variants

S 360、M 720、L 900；高度示例 800；Body Slot；Footer 可选。

### Usage Rules

简单详情用 S，标准表单用 M，复杂多栏信息用 L。Body 独立滚动，Header/Footer 稳定；不可与 Modal 同时争夺焦点。

### Interaction Rules

打开时保持原页面状态，焦点进入 Drawer；Body 可滚动，Header/Footer 固定。提交 Loading 时禁用重复操作；Error 就地呈现。关闭后恢复触发器焦点与底层页面滚动位置。

## Tooltip

### Purpose

解释图标、缩略内容或非显而易见的概念。

### Variants

箭头位置：上左、上右、下左、下右；箭头可隐藏；支持主内容与辅助说明。基准尺寸 192×50。

### Usage Rules

内容简短、非关键；关键错误与操作后果必须常驻显示。触发支持 Hover 与 Focus，移出/失焦后延迟关闭。

### Interaction Rules

Hover / Focus 打开，移出 / Blur / Esc 关闭；内容不可仅依赖鼠标。Tooltip 自身不承载 Loading 或 Error，禁用控件若需解释必须使用可聚焦的外层触发器。

## Tag

### Purpose

展示状态、分类、筛选条件和短标签。

### Variants

Outline / Filled；Regular、Info、Success、Warning、Error、Primary；可清除、跳转、图标；标准 40×24；Group 支持 1–8 个。

### Usage Rules

状态含义必须稳定；可交互 Tag 才显示清除或跳转。避免同一区域堆叠过多色彩，超过可读数量时折叠。

### Interaction Rules

只读 Tag 不使用 Hover / Active 外观。可清除或跳转 Tag 才提供 Hover、Focus、Active；Disabled 时隐藏或禁用操作。异步移除显示 Loading 并保留布局；失败恢复 Tag 并提示原因。

## Notification

### Purpose

承载持续时间较长、可异步到达的重要系统通知。

### Variants

360×184；P0 / P1 两个级别。

### Usage Rules

P0 用于最高优先级、需立即处理的通知；P1 用于重要但非阻断信息。短暂成功反馈优先 Toast；字段错误不使用 Notification。

### Interaction Rules

Hover 可暂停自动消失（若产品启用时限）；Focus 支持键盘读取与操作。关闭后不应立即重复出现。异步操作显示 Loading；处理失败在通知内保留 Error 和重试入口。

## Empty State

### Purpose

表达无内容、无结果、无权限、系统异常、业务结果和待完成动作，为用户解释当前状态并给出下一步。

### Available Assets

「08-05 为空插画」页已收录 38 个顶层实例：

- 通用空状态：暂无结果、暂无订单、暂无权限、暂无账户、暂无数据、暂无产品、购物车为空。
- 系统状态：网络异常、加载失败、405、406、内部服务器错误、升级维护。
- 交易结果：支付、提款、提交的成功 / 失败 / 异常。
- 任务与审核：添加账户、添加地址、上传文件、绑定证件、认证成功、审核成功 / 失败 / 进行中、开通成功 / 失败、关闭商品分销等。
- 资金类状态：成功、进行中、预警、失败，分别复用 Success / Processing / Warning / Error 状态图标。

通用插画画板统一为 240×168，使用低饱和灰紫色视觉；资金类状态为单据插画叠加语义状态图标。`Placeholder` 的头像、图片、商品、文件占位仍只用于内容加载或资源缺失，不能替代 Empty State。

### Properties / Composition

当前资产页展示的是插画实例，没有本地 `Empty State` 容器 Component Set，也没有文案、说明、按钮等可配置属性。页面级 Empty State 需作为组合 Pattern 使用：Illustration + Title + Description（可选）+ Primary Action（可选）。

### Usage Rules

- 必须按语义选择现有插画，不得为了视觉接近而错用成功、失败、权限或网络状态。
- 列表无结果应保留筛选条件与 Table Header；首次无数据可引导创建，筛选无结果优先提供“清空筛选”。
- 无权限强调权限原因或申请路径；异常类提供重试、返回或联系客服；成功/失败结果明确对象与后续动作。
- 文案使用 body / caption；最多一个主要动作，次要动作使用 Link 或 Secondary。
- 不得修改现有插画色彩、拼接新图形或声称存在完整 `Empty State Component`。

### Interaction Rules

空状态本身不响应 Hover / Active。按钮、链接按各自组件状态执行；重试操作进入 Loading 并防止重复请求，失败后保留错误上下文。

# 5. Pattern Library Analysis（页面模式）

## 5.1 List Pattern

结构：Page Header / Tabs → 操作区 → Filter → Table → Pagination。

- Filter 使用 Surface Subtle，字段标签置顶，日期区间、Select、Input 组合。
- 查询/筛选为 Primary 或 Secondary，Reset 为 Text/Weak；操作组靠右。
- Table 顶部可显示批量操作，底部显示总数、页码、每页数量、前往页。
- 行操作优先保留 1–2 个高频动作，其他放 Dropdown。
- 筛选、排序、分页应持久化，返回列表时恢复状态。

## 5.2 Detail Pattern

结构：Breadcrumb → Header（标题、Tag、关键操作）→ Summary → Sections → Timeline / Related Table → Risk Actions。

- 信息使用稳定 Label–Value 对齐；金额与汇率使用 Number Family。
- Section 间距 24/32；必要时用 Card 隔离业务块。
- Timeline 用于状态变化、审核和资金操作记录。
- 页面级操作不与字段级操作混放；危险操作独立成组。

## 5.3 Form Pattern

结构：Title / Helper → Field Groups → Inline Validation → Review / Confirmation → Footer Actions。

- 顶对齐适合移动、长 Label 和单列；左右对齐适合桌面密集录入。
- 必填符号、帮助、单位、字数和错误统一由 Form Properties 控制。
- 首次提交后显示错误；用户修改时实时清除已修复错误。
- 提交时按钮进入 Loading，成功后给结果页/Toast，失败保留输入并聚焦首个错误。
- 金融高风险提交增加确认层或安全验证，不用普通 Toast 代替确认。

## 5.4 Dashboard Pattern（受控推导）

结构：Global Filter → KPI Summary → Trend / Distribution → Recent Activity Table。

- KPI 数量建议 3–6；同一行保持统一高度和数字格式。
- Chart 必须有标题、单位、时间范围、Tooltip 和无数据状态。
- Chart 与 KPI 不是当前正式组件；优先使用现有业务数据与 Table，不复制第三方图表风格进入组件库。
- Dashboard 的复杂数据应提供跳转到 List 的入口。

# 6. B 端产品设计原则

## 信息层级

页面标题 > Section 标题 > Label > Value > Helper。优先通过布局、字号和留白建立层级，颜色只做辅助。

## 操作效率

主操作稳定、批量操作上下文出现、行操作就近、键盘 Focus 可见。减少重复弹窗和不必要的页面跳转。

## 数据展示

单位、币种、时区、小数位和空值格式全局一致。数值右对齐；状态用 Tag；长 ID 保留可复制能力。

## 风险提示

P0/P1、Warning、Danger 分级明确。危险操作说明对象、影响和不可逆性，并提供二次确认。

## 错误处理

字段错误就地显示；模块错误使用 Alert；短暂反馈用 Toast；异步重要信息用 Notification；系统级阻断才用 Modal。

## 权限状态表达

无权限操作优先隐藏；需要解释权限差异时禁用并提供原因 Tooltip。禁止展示可点击外观却在点击后才告知无权限。

# 7. Component Inventory（组件清单）

括号内为 Variant 数量；独立图标按 master 数量统计。

## Foundations / Assets

- 基础图标：`_iconGrid(4)`、`_dot(6)`、`Rating(4)`、`Notification icon(5)`、`_loading(4)`，另有 155 个独立基础图标 master。
- 业务图标：`National Flag(51)`、`Bank(36)`、`Payment Method(60)`、`Contact(12)`。
- 其他图标：`文本光标(2)`，另有 71 个鼠标、手势、操作说明 master。
- Logo：`tuotuo(4)`、`Flyway Logo(9)`、`Flyway 组合Logo(3)`、`FlyLink Logo(5)`、CamelPay。

## Base / Input

- Button：`01_Button(120)`、`02_Button Group(6)`。
- Link：`Link(8)`。
- Form：`_04_无标题(113)`、`01_表单（顶对齐）(17)`、`02_表单（左对齐）(17)`、`03_表单（右对齐）(17)`。
- Radio / Checkbox：`01_单复选项(10)`、`02_单复选图标(10)`。
- Switch：`Switch(4)`。
- Select：`区域选择(30)`、`Cell/勾选角标(5)`、`分段选择(5)`、`Cell/按钮选项(4)`、`高优项选择(4)`。
- Date Picker：`日历控件(5)`、`_item(5)`、`支持快捷选择的日期区间(7)`。
- Rating：`评分(7)`。
- Upload：`_文件类型图标(10)`、`_文件列表(12)`、`Cell/卡片样式（指定文件）(63)`、`Cell/默认样式(6)`、`03_高级样式(7)`、`02_拖拽样式(3)`、`01_表单样式(7)`。
- Dropdown：`Dropdown item(58)`、`下拉菜单(7)`，以及 4 个组合组件。

## Container / Feedback / Display

- Modal / Sheet：`Cell/Bottom(4)`、`_Body(2)`、`Cell/Header(2)`、`Modal(4)`、`Sheet（移动端）(4)`。
- Table：`01_表头(2)`、`02_单元格(13)`、`02_操作(2)`、`03_操作栏(1)`、`_Cell/排序图标(3)`、`_表格图片(7)`。
- Drawer：`Drawer(3)`；Collapse：`Collapse(2)`。
- Dialog：`Modal(4)`；Popconfirm：`Popconfirm(8)`。
- Notification：`Notification(2)`；Toast：`Toast(4)`；Alert：`Alert(8)`；Progress：`进度条(3)`。
- Tag：`01_Tag(12)`、`02_Tag Group(8)`、`03_Tag-Unusual(2)`。
- Tooltip：`Tooltips(4)`；Badge：`徽标(6)`；Placeholder：`Placeholder(4)`；Preview：`Image(3)`、`Preview(1)`。
- Empty Illustration：38 个顶层实例（34 个通用/业务场景、4 个资金类状态）；属于资产目录，尚无本地 Empty State 容器 Component Set。

## Navigation

- Tab：`_标签(16)`、`Tab(4)`。
- Breadcrumb：`Breadcrumb(1)`。
- Pagination：`_Cell/页数(14)`、`Pagination(9)`。
- Anchor：`_Cell(2)`、`Anchor(1)`。
- Steps：`_连接线(6)`、`_步骤图标(8)`、`_步骤类型(15)`、`纵向步骤条(2)`、`横向步骤条-2(3)`、`横向步骤条-1(1)`。
- Timeline：`_类型(10)`、`时间线(4)`、`_连接线(8)`。
- Scrollbar：`_Scrollbar(3)`。

## Business Components

- 国家地区：`国家地区号码(7)`、`证件类型(7)`、`国家地区(5)`、`国家地区选择下拉菜单(4)`。
- 币种金额：`币种和金额选择(20)`。
- 收款人：`飞来汇账户(8)`、`银行账户(5)`、`_收款人item(10)`、`收款人展示(2)`、`收款人下拉菜单(8)`。
- 汇率：`汇率变化(2)`、`日历控件(1)`、`_day(7)`、`关注汇率(2)`。
- 安全：`_密码输入(4)`、`安全验证(12)`、`_Body(4)`、`验证码验证(6)`、`授权(4)`。
- 银行卡：`Bank Card-2(18)`、`Bank Card-1(7)`。
- 引导与运营：`使用引导(1)`、`运营弹窗(1)`、`_指示器(2)`。

# 8. Pattern Library 文档索引

| Pattern | 必选组件 | 可选组件 | 禁止 |
|---|---|---|---|
| List | Form/Filter、Table、Pagination | Tab、Alert、Dropdown、Tag | 无分页的大数据表；行内堆叠过多按钮 |
| Detail | Breadcrumb、Section、Button | Tag、Timeline、Table、Drawer | 用表单控件伪装只读值 |
| Form | Form、Button | Alert、Upload、Date Picker、安全验证 | 自造输入框；只用 Toast 表达字段错误 |
| Dashboard | Grid、Card 结构、Table | Tag、Date Picker | 声称存在 KPI/Chart master；自造颜色/图表风格 |
| Empty State | 现有为空插画、body/caption | Button、Link、Table Header | 自造插画；错用状态语义；把 Placeholder 当空状态 |

# 9. 维护建议

1. 将 38 个为空插画统一迁入本文件的本地资产组件集，并建立完整 Empty State 容器：建议用 `Scene`、`Size`、`Action`、`Description` 等 Properties 管理；避免页面只依赖来源不透明的实例。
2. 将 Input 从 Form 内部能力明确为公开组件或在文档中正式声明仅通过 Form 使用。
3. 为所有 Component Set 补充用途、禁用场景和无障碍说明。
4. 补齐 Card、Slider、KPI Card 与 Chart 的正式组件与使用规则；在此之前维持“受控组合 Pattern”标记。
5. 为 Variables 补充 Web/iOS/Android code syntax，减少设计到代码的歧义。
