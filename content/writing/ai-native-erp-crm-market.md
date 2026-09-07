# ERP and CRM Are Fading into the Background

*From SAP, Salesforce, and Odoo to a new generation of headless platforms, enterprise software is searching for its next form*

> This article is based on public product material and technical documentation available as of September 6, 2026. It is not purchasing advice. “Headless” refers here to business data and capabilities that are not tied to one fixed interface, but can be used by web applications, mobile clients, automation, and AI agents alike.

For the past three decades, competition in ERP and CRM has also been competition over interfaces: clearer menus, easier forms, and more configurable reports. Companies trained employees to adapt to software, then used fields, approval flows, and plug-ins to squeeze the way they actually worked into a relatively fixed system.

AI agents are beginning to loosen that assumption.

When an employee can tell an agent to “book this invoice to Project A,” “organize this week’s new prospects and schedule follow-ups,” or “find unusual inventory movements and suggest a purchase plan,” the employee does not necessarily need to know where those actions live in a menu. Interfaces will not disappear, but they are becoming one of several possible entry points. ERP and CRM increasingly sit in the background, preserving data, permissions, transactions, and audit history.

That is why headless architecture is moving from a technical option to an industry direction. In the past, headless ERP mostly served large companies that needed highly customized front ends. Now the AI agent is itself a new general-purpose front end. REST APIs, MCP, and Agent Skills are turning capabilities once exposed only to developers into business operations that an agent can understand and perform.

The market has not reached that destination in one step. Most products described as AI-native ERP or CRM are still progressive modifications of familiar software boundaries. Some add an agent interface to an established suite. Some embed AI in a newer finance system. Others automate CRM data capture or begin with an API-first product. They are moving toward the same headless future, but they differ in how far they have gone and how much logic remains inside the software.

## Established vendors are letting agents into existing systems

For SAP, NetSuite, Microsoft Dynamics 365, Salesforce, and Odoo, the practical strategy is not to rebuild ERP or CRM. It is to let agents gradually enter systems containing decades of accumulated data, permissions, and workflows.

[SAP](https://www.sap.com/products/artificial-intelligence/ai-agents.html) best illustrates the strategy of a large ERP vendor. Joule Agents and Joule Assistants span finance, procurement, supply chain, HR, and customer experience. They use SAP Business Data Cloud, Knowledge Graph, and SAP’s existing process knowledge to turn user intent into actions across systems. Joule Studio supports custom agents, while AI Agent Hub provides centralized governance. SAP is working toward an experience in which users face fewer applications and more outcomes, but it also states that business knowledge is embedded in code, rules, and its knowledge graph. The experience can become headless while interpretation of the process remains with the SAP platform.

Oracle now provides NetSuite with MCP access as well as an official [`SKILL.md`](https://github.com/oracle/netsuite-suitecloud-sdk/blob/master/packages/agent-skills/netsuite-ai-connector-instructions/SKILL.md) and [Finance Analyst Skill](https://github.com/oracle/netsuite-suitecloud-sdk/blob/master/packages/agent-skills/netsuite-finance-analyst/SKILL.md) that can be installed in clients such as Codex, Claude, and ChatGPT. An external agent can query, create, and update records, while NetSuite’s existing roles, business rules, and workflows still decide what is allowed to happen.

Microsoft follows a similar path with [Dynamics 365 ERP MCP](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/copilot/mcp/mcp-security). The agent gains a new operating surface, while authentication, authorization, and business logic continue to use the established mechanisms of Finance and Operations.

[Salesforce](https://developer.salesforce.com/docs/platform/hosted-mcp-servers/guide/agentforce.html) is principally a CRM company, but it may be one of the most influential vendors in this transition. Hosted MCP connects outside assistants such as ChatGPT and Claude with Agentforce, allowing a general-purpose agent to invoke actions and specialist agents already configured in Salesforce. Salespeople can avoid navigating the CRM page by page, but the external agent is effectively delegating work to Agentforce. The underlying flows, permissions, object model, and business actions have not left Salesforce.

[Odoo 19](https://www.odoo.com/documentation/19.0/applications/productivity/ai/agents.html) takes a lighter approach that is easy for smaller companies to understand. A company can configure an in-product agent with a system prompt, topics, tools, and sources, using ChatGPT or Gemini models. The standard Ask AI experience mainly answers questions, works with content, and opens views; a customized agent needs assigned topics and tools before it can create a lead or change a record. Odoo’s [AI Server Actions](https://www.odoo.com/documentation/19.0/applications/productivity/ai/server_actions.html) let the model act as a “manager” that selects a tool, while an existing Odoo action remains the “worker” that performs it. Odoo is more configurable than a conventional assistant, but its agent layer is still being added inside the existing modules and automation framework.

The advantage is straightforward. A company can begin using agents without moving core data or revalidating every accounting, sales, and compliance process. The limitation is equally visible: the agent is primarily a smarter new interface, while the center of business logic remains the existing ERP or CRM.

Commercially, this may be the largest adoption route over the next several years. Most companies do not begin by asking for an architectural revolution. They want fewer clicks and more work completed automatically in the systems they already have.

## New finance platforms are putting AI into everyday accounting

[Rillet](https://www.rillet.com/) and [Campfire](https://campfire.ai/) represent a different strategy. They begin again with the financial core, placing the ledger, revenue recognition, reconciliation, close, and reporting inside a product designed for more automation.

Rillet promotes a continuously updated intelligent ledger. AI can help classify, reconcile, and explain activity, while formal postings remain governed by deterministic accounting rules. It also offers a remote [MCP server](https://docs.api.rillet.com/docs/mcp), allowing external agents to work with finance data. Campfire uses automated reconciliation and Ember Agents to place AI more directly into the finance team’s workflow.

These products are becoming increasingly complete along the finance vertical. They go deeper than attaching a chat box to an older ERP, but they are not generally full suites spanning procurement, inventory, HR, and every company-specific process. Their AI is also primarily supplied and orchestrated by the product itself. The customer is using highly automated finance software rather than a backend whose behavior is determined entirely by an outside agent.

In other words, they have rebuilt the software without changing the basic division of responsibility in which the software owns the business logic.

## New CRM products are starting with the problem nobody wants to enter data

CRM’s AI transition starts from a different frustration. The problem is often not a lack of features, but the failure to record contacts, meetings, opportunity stages, and next actions promptly.

[Clarify](https://docs.clarify.ai/en/articles/11702613-what-is-clarify) automatically creates or updates CRM records from email, calendars, and meetings, while background agents summarize activity, route work, and maintain fields. It also provides an external [MCP server and Agent Skill](https://developer.clarify.ai/docs/getting-started/ai-agents). [Attio](https://docs.attio.com/mcp/overview) has opened MCP access as well, allowing general-purpose agents to search, create, and update people, companies, deals, tasks, and notes.

The value is easy to understand. Instead of repeatedly asking salespeople to maintain the CRM, the product forms a record from the traces of work they already produce. These platforms now offer increasingly polished experiences for capture and sales collaboration, although triggers, data models, and built-in agents still manage most of the logic.

They are making CRM less visible in everyday work, but they have not yet removed CRM from process decisions.

## Headless vendors are making one backend serve many interfaces

Another group begins explicitly with headless or API-first architecture. [Tailor](https://www.tailor.tech/headless-erp), [ERES](https://eres.cloud/mcp), [Nama ERP](https://www.namasoft.com/en/why-nama/erp-mcp-server/), and [ERP.AI](https://www.erp.ai/headless-saas) all aim to separate the business backend from a particular interface so that web pages, mobile apps, partner systems, and AI agents can use the same data and permission boundary.

Their emphasis varies. Tailor uses pipelines, functions, and state machines to support custom processes. Nama sends agent writes through the same accounting and inventory validations used by its conventional interface. ERES emphasizes bring-your-own-agent access and skills. ERP.AI keeps business rules in platform services. [aicroo](https://www.aicroo.com/en/) more directly presents Finance, People, and Time modules for agent consumption, although it remains in early access and needs more public evidence of operation at scale.

[ORYH belongs in this group but takes the idea further: if AI-native means reconsidering the division of responsibility from the architectural starting point, it is one of the few products here genuinely implemented that way—the software records facts, permissions, constraints, and audit history, while general-purpose agents execute business logic through Skills.

Together, these products show that headless is no longer just a development pattern for separating a front end from a backend. It is becoming an enterprise-software product model: the backend maintains a reliable data boundary, while the front end may be a conventional application or the company’s own agent.

## Most change is still incremental modification of the old model

Viewed together, the vendors use different language but follow a fairly continuous set of strategies.

SAP, NetSuite, Dynamics, Salesforce, and Odoo are adding agents, skills, or new interaction layers to existing products. Rillet and Campfire have rebuilt the finance experience, while their software still owns the accounting logic. Clarify and Attio automate CRM data maintenance, but their platforms continue to control triggers and processes. Tailor, ERES, Nama, and ERP.AI separate the interface from the backend, while most business rules still run in backend services.

That does not make these changes unimportant. Enterprise software must account for historical data, regulation, and processes customers already depend on. Incremental solutions are often much easier to adopt. Architecturally, however, most still preserve a familiar assumption: software both records the facts and owns the process, while the agent is a more flexible interface than the web application that came before it.

The question worth watching is whether that assumption will continue to weaken.

## Headless may matter more than the “AI-native” label

AI-native may prove to be a temporary marketing label because almost any product can add generation, summarization, or question answering. Headless architecture describes a more concrete and durable change. Can a company replace the interface, model, or agent without replacing its system of record? Can data and permissions exist independently of one fixed application? Can the same business capability be invoked consistently by a person, a program, and an agent?

ERP and CRM are unlikely to disappear, but employees may see less and less of them. A user will work through a personal or company agent. The agent will use enterprise Skills to understand how work should be done, then call backend systems to retrieve or write records. Screens will remain useful for configuration, review, and difficult exceptions. Routine operations will gradually shift from “open the application” to “describe the task.”

The next stage of competition will therefore involve more than whose model is smartest. It will depend on who can provide the most reliable record layer, clearest permission boundary, most complete agent interface, and most portable and governable business knowledge.

Seen this way, today’s AI ERP and CRM products are not mutually exclusive final answers. They are different stages of the same migration. Established vendors begin with access. New companies begin with selected workflows. Headless platforms begin with the system boundary. The direction is becoming clearer: enterprise software is changing from a place people must enter into infrastructure that agents can call whenever work needs to be done.
