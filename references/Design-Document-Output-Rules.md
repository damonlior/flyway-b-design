# 常规设计文档输出规则

> 用途：约束设计师或 AI 在 Figma 中输出可供设计评审的完整方案文档。
>
> 本文件负责回答“设计方案应如何组织、展示和说明”，不替代产品需求文档、Design System、接口文档或研发技术方案。

## 1. Role

你是一名企业级产品设计文档输出助手。你的任务不是只生成若干独立 UI 页面，而是将业务需求整理成结构清晰、流程完整、状态可检查、修改可追溯的 Figma 设计文档，使产品、设计、研发、测试和业务相关方能够完成设计评审。

## 2. Source Basis

本规则归纳自：

- 飞书文档《设计团队对于设计文档的输出规范》。
- Figma 样本文档《商家端 · FlyLink（新）》中的页面组织、模块拆分、流程说明、组件管理和历史迭代实践。

当本规则与项目 Design System 冲突时：

- 页面结构、版本管理和交付组织以本规则为准。
- 颜色、字体、间距、组件、布局和状态外观以项目 Design System 为准。
- 业务目标、范围和文案以已确认的产品需求为准。

## 3. Design Tool

1. 设计方案优先使用 Figma 输出。
2. 设计交付和协作使用同一个可访问的 Figma 链接。
3. 正式方案必须使用可编辑 Frame、Section、Component Instance 和 Auto Layout，不得只放截图或不可编辑图片。
4. 参考资料、旧稿和废弃方案不得与正式方案混放或冒充当前版本。

## 4. File Structure

常规设计文件应根据项目复杂度包含以下页面。标记为“建议”的页面可以在确实无内容时省略。

### 4.1 Cover

必须包含：

- 项目或需求名称。
- 当前版本号。
- 当前阶段或状态。
- 创建或最近更新时间。
- 设计负责人。

### 4.2 Document Guide（建议）

用于说明：

- 文件目录和阅读顺序。
- 画板、连线、标记、颜色或状态符号的含义。
- 当前评审范围和明确不在本期范围内的内容。
- 相关 PRD、需求文档和项目链接。

### 4.3 Analysis（建议）

用于保留必要的设计推导，包括：

- 业务背景与问题。
- 用户角色与核心任务。
- 设计目标与成功标准。
- 关键约束、风险与设计策略。
- 信息架构或任务拆解。

分析只保留能够解释最终方案的内容，不得让评审者必须读完长篇分析才能理解方案。

### 4.4 References（建议）

用于放置：

- 竞品或同类功能参考。
- 现有产品截图。
- 已确认的业务规则、文案或数据样例。

每项参考应标记来源、用途和可借鉴点；参考内容不得直接作为正式方案。

### 4.5 Design Solution

设计方案主体。必须按照“模块 → 细分场景/任务流 → 页面或状态”的层级组织。

复杂项目可按业务模块拆为多个 Figma Page；单个需求可在一个 Page 内用 Section 拆分模块和流程。

### 4.6 Components（按需）

当项目存在页面级组合组件、业务组件或尚未进入正式组件库的局部资产时，应独立放置并说明：

- 组件名称和用途。
- Variants、Properties 和状态。
- 复用范围。
- 正式组件、组合 Pattern 或临时资产的身份。

不得复制页面图层伪装成组件，也不得把临时资产声明为正式 Design System 组件。

### 4.7 History / Time Machine

用于保存已经正式发布或完成评审的历史版本。历史内容应包含版本号和日期，不得覆盖当前方案。

### 4.8 Trash

用于暂存被否决、废弃或可能需要找回的页面。废纸篓内容不得参与当前评审，也不得作为正式 Pattern 被复用。

## 5. Version Management

### 5.1 Version Format

版本格式使用：

```text
V A.B.xx
```

第一版建议命名为 `V1.0.01`。

- `A`：主版本号。仅在功能结构或需求发生重大调整时更新。
- `B`：子版本号。主干功能、核心流程或主要方案发生变化时更新。
- `xx`：小版本号。细节、交互、文案或局部 UI 调整时更新。

### 5.2 Page Naming

正式需求页建议使用：

```text
状态标记 + 功能/需求名称 + 阶段或期数 + （YY-MM）
```

示例：

```text
---- ✅ 快捷订单（一期）（25-09）
```

状态标记必须在文档说明页统一解释，不得让不同项目自行猜测。

### 5.3 Change Synchronization

设计方案通过评审，或项目推进中发生方案变化后，必须在对应项目群同步。

同步内容必须包含：

```text
【设计更新】YYMMDD
设计方案：Figma 链接
修改点：
- 【修改】……
- 【新增】……
- 【删除】……
@相关人员
```

修改记录必须描述用户可感知或实现相关的变化，禁止只写“细节优化”。

## 6. Information Hierarchy

### 6.1 Mandatory Hierarchy

设计方案必须按以下层级拆分：

```text
Module
→ Scenario / Task Flow
→ Screen / State
→ Local Interaction Detail
```

### 6.2 Module

模块对应一个相对独立的业务目标，例如：

- 订单管理。
- 创建任务。
- 客户端展示。
- 消息通知。
- 日志审计。

模块使用顶层 Section 或独立 Page 表达。

### 6.3 Scenario / Task Flow

大型模块按用户任务或业务场景拆分，例如：

- 创建订单。
- 克隆订单。
- 查看物流。
- 修改资料。
- 审核驳回后重新提交。

一个任务流只表达一个清晰目标。延伸出的独立任务应另起一个流程，不得将多个任务编织成难以追踪的网状流程。

### 6.4 Screen / State

每个页面或关键状态必须使用语义化名称，并按流程顺序编号。

推荐格式：

```text
00｜入口
01｜默认状态
02｜输入完成
03｜提交中
04｜提交成功
05｜提交失败
```

页面名称必须描述当前状态或用户动作，禁止仅使用 `Frame 1`、`方案A`、`页面2` 等无业务含义名称。

## 7. Canvas Organization

1. 同一任务流的页面按操作顺序从左到右排列；复杂流程可以分行，但必须保持明确阅读顺序。
2. 不同模块、任务流和状态组使用 Section 隔离。
3. 同一流程的画板尺寸、基线和间距保持一致。
4. 页面之间使用流程说明或连线表达跳转关系；不得让评审者依靠猜测理解顺序。
5. 页面附近只放与该状态直接相关的说明；跨流程规则放到模块说明或文档说明页。
6. 主方案、组件、参考、历史和废纸篓必须在画布空间上明显隔离。
7. 正式评审区不得保留无标题散落图层、重复草稿或互相遮挡内容。

## 8. Task Flow Completeness

每个任务流至少检查以下内容。

### 8.1 Positive Flow

- 入口在哪里。
- 用户完成哪些操作。
- 系统如何响应。
- 最终到达哪里。
- 数据是否保存、提交或记住。
- 成功后下一步是什么。

### 8.2 Reverse Flow

- 取消、返回、关闭和退出分别回到哪里。
- 已输入内容是否保留。
- 是否需要未保存提醒。
- Overlay 关闭后焦点和底层页面状态是否恢复。

### 8.3 Exception Flow

- 输入或校验错误。
- 请求失败、超时、无网或弱网。
- 无数据、无搜索结果或资源不存在。
- 无权限或登录状态变化。
- 操作冲突、重复提交或业务状态已改变。
- 高风险操作和不可逆结果。
- 失败后的恢复、重试或人工处理路径。

### 8.4 Flow Rule

一个任务流应尽量保持线性：

```text
Entry → Action → Processing → Result
```

分支较多时，主流程保留在原任务流，独立异常或延伸任务另起 Section，并标注从哪个状态进入、处理后返回哪里。

## 9. Required State Coverage

所有与任务有关的组件和页面必须检查以下状态；不适用时标记 `N/A`，不得静默遗漏。

1. Initial / Default。
2. Hover。
3. Active / Selected。
4. Focus。
5. Input / Filled。
6. Loading / Processing。
7. Disabled。
8. Empty / No Result。
9. Validation Error。
10. Business Error。
11. Warning / Confirmation。
12. Timeout。
13. Offline / Weak Network。
14. Permission。
15. Limit / Overflow。
16. Success / Result。

页面无需为每个微小组件状态单独复制整屏，但关键业务状态、结构变化和异常恢复必须提供独立画板或清晰状态矩阵。

## 10. Interaction Annotation

关键交互必须就近说明。每条说明至少回答：

```text
Trigger：什么条件或操作触发？
Action：用户执行什么操作？
System Response：系统即时反馈什么？
State Change：界面和业务状态如何变化？
Destination：跳转、弹层或返回哪里？
Persistence：输入、筛选、选择和滚动位置是否保留？
Failure Recovery：失败后如何恢复？
```

必须说明的常见交互包括：

- 点击、双击、Hover、Focus、键盘操作。
- 页面跳转、新标签页、Drawer、Modal、Dropdown 和 Popover。
- 展开、收起、分页、筛选、排序和滚动。
- 保存、提交、撤销、取消、删除和关闭。
- Loading、防重复提交和成功反馈。
- 权限限制、风险确认和异常恢复。

禁止仅写“点击后处理”“同线上逻辑”或“研发自行判断”。

## 11. Environment & Responsive Coverage

根据业务范围明确：

- 未登录与已登录。
- 不同用户角色和权限。
- 不同语言及长文本。
- Desktop、Compact Desktop 和 Mobile。
- Light / Dark（项目支持时）。
- 正常网络、弱网和离线。

如果某个终端或环境不在本期范围内，必须在文档说明中明确标记为 Out of Scope。

Mobile 必须表达结构转换，不得直接缩小 Desktop 页面。

## 12. Content & Data Rules

1. 页面必须使用接近真实业务的数据，不用无意义的 `xxx`、`test` 代替关键内容。
2. 产品功能文案必须在设计稿中确定，包括标题、按钮、提示、错误、警告、确认和结果文案。
3. 金额必须包含币种，日期时间包含必要格式和时区，编号展示完整或提供查看完整值的方式。
4. 敏感信息应按权限脱敏。
5. 空值、异常值、长文本、超长数字、多语言和极端数据必须验证布局。
6. 风险提示必须说明对象、原因、影响、后果和恢复方式。

## 13. Component & Design System Rules

1. 优先复用项目已有 Component、Variant、Property 和 Token。
2. 页面中的复用组件保持实例身份，不拆复制内部图层制作相似控件。
3. 关键页面级组合可标记为 Composition Pattern。
4. 缺少能力时标记 Needs Extension，并说明业务理由、建议属性和影响范围。
5. 页面方案不得未经授权修改正式 Component Master、Variables、Styles 或 Token。
6. 同一功能在不同页面和状态中的组件、文案和交互语义必须一致。

## 14. Review-ready Output Contract

一次可进入设计评审的输出至少包含：

1. 项目名称、版本、状态和更新时间。
2. 本期目标、范围、用户角色和关键约束。
3. 模块与任务流目录。
4. 主流程完整 UI。
5. 入口、过程、结果和后续去向。
6. 取消、返回、关闭和退出路径。
7. Loading、Empty、Error、Disabled、Permission、Limit 等相关状态。
8. 关键交互就近说明。
9. 最终产品文案。
10. Desktop / Compact / Mobile 或明确的 Out of Scope。
11. 复用组件与需扩展资产说明。
12. 当前版本修改点和待确认问题。

## 15. Definition of Done

### 15.1 Structure

- [ ] 文件具有明确封面、正式方案区和版本信息。
- [ ] 方案遵循“模块 → 任务流 → 页面/状态”的层级。
- [ ] 每个任务流有唯一主目标，阅读顺序明确。
- [ ] 参考、历史、废纸篓和正式方案已隔离。

### 15.2 Flow

- [ ] 入口、过程、结果和后续动作完整。
- [ ] 取消、返回、关闭和退出路径完整。
- [ ] 关键异常有恢复或人工处理路径。
- [ ] 页面跳转、Overlay 和状态变化均已标注。

### 15.3 State

- [ ] 已检查 Default、Hover、Active、Focus、Loading 和 Disabled。
- [ ] 已检查 Empty、Error、Warning、Permission、Limit 和 Success。
- [ ] 不适用状态已标记 N/A。
- [ ] 失败后保留必要输入和任务上下文。

### 15.4 Content

- [ ] 产品功能文案已经确定。
- [ ] 业务数据真实且包含必要单位、币种、日期和状态。
- [ ] 长文本、多语言、空值和极端数据下布局成立。
- [ ] 风险、权限和错误不只依赖颜色表达。

### 15.5 Components & Responsive

- [ ] 优先复用已有组件和 Token。
- [ ] 不存在的能力已标记 Composition Pattern 或 Needs Extension。
- [ ] Desktop、Compact Desktop 和 Mobile 已覆盖或明确排除。
- [ ] 关键操作具备可见 Focus 和可访问名称。

### 15.6 Governance

- [ ] 当前版本号符合 `V A.B.xx`。
- [ ] 修改、新增和删除内容可追溯。
- [ ] 历史版本未被覆盖。
- [ ] 正式评审区没有散落草稿或废弃页面。

只有以上检查通过后，才能将方案标记为 `Review Ready`。

## 16. AI Execution Protocol

AI 被要求输出设计方案时，必须按以下顺序执行：

1. 读取项目需求、Design System、Pattern Library 和本文件。
2. 明确 Business Goal、User Role、Scope、Target Viewports 和 Risk Level。
3. 将需求拆成 Module、Scenario / Task Flow 和 Screen / State。
4. 为每个任务流确定入口、主流程、逆向流程、异常流程和结果。
5. 映射现有组件、Variant、Property、Token 和页面 Pattern。
6. 先输出页面骨架和主流程，再补齐状态和交互说明。
7. 使用真实业务文案和代表性数据完成 UI。
8. 检查响应式、权限、风险、无障碍和异常恢复。
9. 按 Definition of Done 自检。
10. 输出版本、修改记录、待确认问题和验证结果。

AI 禁止：

- 只输出一张理想状态页面并声称方案完整。
- 用长篇评审文档代替实际 UI 和状态页面。
- 将多个独立任务塞进一个网状流程。
- 省略取消、返回、关闭、失败和恢复路径。
- 使用未确认的临时文案或无意义占位数据交付评审。
- 将参考截图、旧稿或废纸篓内容纳入正式方案。

## 17. AI Design Declaration

开始设计前必须形成以下判断：

```text
Project / Requirement:
Current Version:
Business Goal:
User Role:
Scope:
Out of Scope:
Primary Module:
Task Flows:
Target Viewports:
Component / Pattern Mapping:
State Coverage:
Risk & Permission:
Reused Assets:
Missing Assets / Extension:
Open Questions:
```

## 18. Recommended Figma Skeleton

```text
Cover
Document Guide
Analysis（optional）
References（optional）

Design Solution
├─ Module 01
│  ├─ Flow 01｜Primary Flow
│  │  ├─ 00｜Entry
│  │  ├─ 01｜Default
│  │  ├─ 02｜Processing
│  │  ├─ 03｜Success
│  │  └─ Interaction Notes
│  ├─ Flow 02｜Reverse Flow
│  └─ Flow 03｜Exception Flow
├─ Module 02
└─ Cross-module Changes

Components（as needed）
History / Time Machine
Trash
```

## 19. Delivery Boundary

本文件的完成标准是“达到设计评审程度”，包括 UI、流程、状态、文案、响应式和交互规则。

进入研发技术方案和开发前，项目仍应根据复杂度补充：

- 接口和数据结构。
- 错误码映射。
- 埋点和监控。
- 数据留存与安全策略。
- 可执行验收用例。

这些内容可以位于 PRD、接口文档或技术方案中，不要求全部堆叠在 Figma 画布内，但必须与设计状态保持一致。
