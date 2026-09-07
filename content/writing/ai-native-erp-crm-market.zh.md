# ERP/CRM 正在“隐身”：AI Agent 推动企业软件走向无头化

*从 SAP、Salesforce、Odoo 到新一代无头平台，企业软件正在寻找下一种形态*

> 本文基于截至 2026 年 9 月 6 日公开的产品资料与技术文档，不构成采购建议。文中所称“无头化”，是指业务数据和能力不再依赖固定界面，而是可以被网页、移动端、自动化程序或 AI Agent 共同调用。

过去三十年，ERP 和 CRM 的竞争很大程度上也是界面的竞争：菜单是否清楚，表单是否好填，报表是否容易配置。企业花费大量时间培训员工适应软件，再通过审批流、字段和插件，把真实的工作方式塞进一个相对固定的系统。

AI Agent 出现以后，这个前提开始松动。

当员工可以直接对 Agent 说“把这张发票登记到项目 A”“整理本周新客户并安排跟进”或者“找出库存异常并给采购建议”时，他未必还需要知道这些操作位于哪一级菜单。界面不会完全消失，但它会从唯一入口变成众多入口之一。ERP 和 CRM 则逐渐退到后台，负责保存数据、权限、交易和审计。

这正是“无头化”从技术选项变成行业趋势的原因。过去，无头 ERP 通常服务于需要高度定制前端的大型企业；现在，AI Agent 本身就是一个新的通用前端。REST API、MCP 和 Agent Skills 正在把原来只对程序员开放的系统能力，变成 Agent 可以理解和操作的业务能力。

不过，行业并没有一步走到终点。今天被称为“AI 原生”的 ERP/CRM，大多仍是在原有软件边界上做渐进式改造：有的给旧系统增加 Agent 接口，有的把 AI 嵌进新的财务模块，有的让 CRM 自动收集数据，还有的先把产品做成 API-first。它们的共同方向是无头化，区别只是走了多远，以及把多少逻辑留在软件内部。

## 成熟厂商：先让 Agent 进入现有系统

对 SAP、NetSuite、Microsoft Dynamics 365、Salesforce 和 Odoo 来说，最现实的策略不是重写 ERP 或 CRM，而是让 Agent 逐步进入已经积累多年的数据、权限和工作流。

[SAP](https://www.sap.com/products/artificial-intelligence/ai-agents.html) 的路线最能体现大型 ERP 厂商的思路。Joule Agents 和 Joule Assistants 覆盖财务、采购、供应链、人力资源和客户体验，并借助 SAP Business Data Cloud、Knowledge Graph 以及 SAP 原有的流程知识，把用户意图转成跨系统动作。Joule Studio 允许企业定制 Agent，AI Agent Hub 则负责集中治理。SAP 正在努力让用户少面对应用、多面对任务，但它也明确把业务知识嵌在代码、规则和知识图谱中：体验可以逐渐无头，流程的解释权仍属于 SAP 平台。

Oracle 已经为 NetSuite 提供 MCP 接口，以及可以安装在 Codex、Claude、ChatGPT 等客户端中的 [`SKILL.md`](https://github.com/oracle/netsuite-suitecloud-sdk/blob/master/packages/agent-skills/netsuite-ai-connector-instructions/SKILL.md) 和 [Finance Analyst Skill](https://github.com/oracle/netsuite-suitecloud-sdk/blob/master/packages/agent-skills/netsuite-finance-analyst/SKILL.md)。外部 Agent 可以查询、创建和更新记录，但最终仍由 NetSuite 的角色权限、业务规则和工作流决定什么能够发生。

Microsoft 的 [Dynamics 365 ERP MCP](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/copilot/mcp/mcp-security) 采取相似策略：Agent 获得新的操作入口，认证、授权和业务逻辑继续复用 Finance and Operations 的既有机制。

[Salesforce](https://developer.salesforce.com/docs/platform/hosted-mcp-servers/guide/agentforce.html) 虽然主要是 CRM，却可能是这场变化中影响最大的厂商之一。它通过托管 MCP 把 ChatGPT、Claude 等外部助手接入 Agentforce，让通用 Agent 可以调用 Salesforce 内已经配置的动作和专用 Agent。销售人员因此可以不再逐页操作 CRM，但外部 Agent 实际上是把任务委托给 Agentforce，底层 Flow、权限、对象模型和业务动作并没有离开 Salesforce。

[Odoo 19](https://www.odoo.com/documentation/19.0/applications/productivity/ai/agents.html) 的做法更轻量，也更容易被中小企业理解。企业可以为内置 Agent 配置 System Prompt、Topics、Tools 和 Sources，并选择 ChatGPT 或 Gemini 模型；普通 Ask AI 主要负责问答、内容处理和打开视图，获得 Topics 与 Tools 的定制 Agent 才能创建线索或修改记录。它的 [AI Server Actions](https://www.odoo.com/documentation/19.0/applications/productivity/ai/server_actions.html) 已经允许模型充当“Manager”选择工具，但实际执行仍依赖 Odoo 中已有的“Worker”动作。Odoo 因而比传统助手更可配置，仍然是在原有模块和自动化框架中加入一层 Agent 能力。

这条路线的优势很务实。企业不必迁移核心数据，也不必重新验证所有会计、销售和合规流程，就能让员工开始使用 Agent。它的局限同样明显：Agent 更像一个聪明的新界面，业务逻辑的中心仍然是原来的 ERP/CRM。

从商业上看，这很可能是未来几年采用量最大的路线。大多数企业首先需要的不是一场架构革命，而是让现有系统少一些点击、多一些自动执行。

## 新一代财务软件：把 AI 放进日常核算

[Rillet](https://www.rillet.com/) 和 [Campfire](https://campfire.ai/) 代表另一种做法。它们从财务核心重新起步，把总账、收入确认、对账、关账和报表放进一个更适合自动化的产品中。

Rillet 强调持续更新的智能总账，AI 可以参与分类、对账和解释，但正式入账依然受到确定性会计规则约束。它也已经提供远程 [MCP Server](https://docs.api.rillet.com/docs/mcp)，让外部 Agent 能够访问财务数据。Campfire 则通过自动对账和 Ember Agents，把 AI 更直接地放进财务团队的工作流。

这类产品目前的状态，是在财务这一条垂直链路上做得越来越完整。它们比“旧 ERP 加聊天框”更深入，却通常还不是覆盖采购、库存、人事和复杂企业流程的完整 ERP。AI 也主要由产品自身提供和编排，用户使用的是一套高度自动化的财务软件，而不是一个完全由外部 Agent 决定行为的后端。

换句话说，它们重做了软件，但没有改变软件拥有业务逻辑这一基本分工。

## 新一代 CRM：先解决“没有人愿意录数据”

CRM 的 AI 化从另一个痛点开始。销售系统的问题往往不是功能太少，而是联系人、会议、商机阶段和下一步行动没有被及时记录。

[Clarify](https://docs.clarify.ai/en/articles/11702613-what-is-clarify) 会从邮件、日历和会议中自动建立或更新 CRM 记录，并通过后台 Agent 完成总结、路由和字段维护。它还提供面向外部客户端的 [MCP Server 和 Agent Skill](https://developer.clarify.ai/docs/getting-started/ai-agents)。[Attio](https://docs.attio.com/mcp/overview) 也开放了 MCP，使通用 Agent 能够搜索、创建和更新联系人、公司、交易、任务与笔记。

这类产品的价值很容易理解：与其提醒销售人员填写 CRM，不如让系统从工作痕迹中自动形成记录。当前它们已经在信息采集和销售协作上展现出成熟体验，但逻辑仍主要由平台的触发器、数据模型和内置 Agent 管理。

因此，它们正在让 CRM 变得更“无感”，却还没有让 CRM 真正退出流程决策。

## Headless 厂商：让一个后端服务更多入口

还有一批公司从一开始就强调 headless 或 API-first。[Tailor](https://www.tailor.tech/headless-erp)、[ERES](https://eres.cloud/mcp)、[Nama ERP](https://www.namasoft.com/en/why-nama/erp-mcp-server/) 和 [ERP.AI](https://www.erp.ai/headless-saas) 都希望把业务后台与具体界面分开，让网页、移动应用、合作伙伴系统和 AI Agent 使用同一套数据与权限。

它们之间也有不同侧重。Tailor 用 Pipeline、Function 和状态机承载定制流程；Nama 让 Agent 的写入经过与传统界面相同的会计和库存校验；ERES 强调自带 Agent 和 Skills；ERP.AI 则把业务规则保留在平台服务中。[aicroo](https://www.aicroo.com/en/) 更强调为 Agent 直接提供 Finance、People 和 Time 模块，但产品仍处于 early access，实际运行能力还有待更多公开案例验证。

[ORYH 也位于这组产品之中，但走得更彻底一些：如果把“AI native”理解为从架构起点重新分工，那么它是这里少数真正按这个思路实现的产品——软件本身负责记录事实、权限、约束和审计，业务逻辑则由通用 Agent 通过 Skills 执行。

这批产品说明，无头化已经不只是“前后端分离”的开发概念。它正在变成企业软件的产品形态：后端保留可靠的数据边界，前端可以是传统页面，也可以是企业自己的 Agent。

## 大多数变化，仍然是对旧范式的渐进改造

把这些产品放在一起看，会发现厂商的宣传虽然各不相同，实际策略却相当连续。

SAP、NetSuite、Dynamics、Salesforce 和 Odoo 在现有产品上增加 Agent、Skills 或新的交互层；Rillet 和 Campfire 重建了财务体验，却仍由软件掌握会计逻辑；Clarify 和 Attio 自动完成 CRM 数据维护，平台仍然控制触发器和流程；Tailor、ERES、Nama 与 ERP.AI 拆开了界面和后端，但业务规则大多仍运行在后端服务中。

这些改造并非没有价值。恰恰相反，企业软件的每一步演进都需要兼顾历史数据、合规要求和客户已有流程，渐进式方案往往更容易落地。只是从架构角度看，它们大多仍延续一个熟悉的前提：软件既保存事实，也拥有流程；Agent 只是比网页更灵活的新入口。

真正值得观察的变化，是这个前提会不会继续松动。

## 无头化可能比“AI 原生”更重要

“AI 原生”很容易成为一个阶段性的营销标签，因为几乎所有产品都能增加生成、总结或问答功能。无头化则是一项更具体、也更长期的变化：企业是否能够在不更换记录系统的情况下，更换操作它的界面、模型和 Agent；数据与权限是否能够脱离某一个固定应用独立存在；同一项业务能力是否能被人、程序和 Agent 一致调用。

未来的 ERP/CRM 未必会消失，但可能越来越少被员工直接看见。用户面对的是自己的 Agent，Agent 根据企业 Skills 理解怎样工作，再调用后台系统完成查询和写入。页面仍会存在，用于配置、复核和处理复杂例外；日常操作则逐渐从“打开软件”变成“交代任务”。

这也意味着，厂商下一阶段的竞争不会只是谁的模型更聪明，而是谁能提供更稳定的记录层、更清晰的权限边界、更完整的 Agent 接口，以及更容易迁移和治理的业务知识。

从这个角度看，今天市场上的各种 AI ERP/CRM 并不是互相排斥的终局方案，而是同一场迁移的不同阶段。成熟厂商从入口开始，新公司从局部流程开始，headless 产品从系统边界开始。方向已经越来越清楚：企业软件正在从一个需要人进入的地方，变成一个随时可以被 Agent 调用的基础设施。
