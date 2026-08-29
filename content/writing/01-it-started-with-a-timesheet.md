# It Started with a Timesheet: The Origin of ORYH

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 1*

On March 11, 2026, the repository expressed only a broad ambition: to provide business applications for AI agents. The first real business capability added that day was not an ambitious ERP or CRM suite. It was a small timesheet-recording service.

It stored employees, projects, timesheet headers, line entries, and approval results. Its limits were stated plainly. It was not a full human-resources system. It did not find managers, execute approval routes, or calculate payroll. It simply allowed a web client, an API client, or an AI agent to write down timesheet facts.

In retrospect, that restraint mattered more than it appeared to at the time.

## The first problem introduced by agents was not automation

Employees do not describe a working week in database fields. They say things like:

> I mainly worked on API design for ERP Upgrade this week and handled the Globex integration on Wednesday.

An agent can turn that sentence into dates, projects, tasks, and hours, then submit structured records through an API. At first, this looks like a straightforward conversion from natural language to form fields. A person once filled out a page; now an agent calls an endpoint.

But that small interaction raised a harder question. The structured result is the agent's interpretation, not the person's original statement. The agent may select the wrong project, divide the work across the wrong dates, or convert an ambiguous sentence into a number with more confidence than the source justifies. If the system keeps only the final fields, it can no longer answer a basic question: where did this number come from?

Two weeks later, the timesheet header gained a field named `source_report_text`. Its only purpose was to retain the employee's original natural-language report. Structured entries remained useful for totals, queries, and approvals. The source text preserved the evidence that existed before interpretation.

These were not two copies of the same data. One was the operational record the system could calculate over. The other was the material a person or another agent could revisit, question, and reinterpret.

That choice became an early version of a principle ORYH would return to repeatedly: **an agent may produce an interpretation, but its interpretation must not erase the evidence.**

## Deletion should not make a business fact disappear

The same change added soft deletion and restoration for timesheet headers. The reason was equally ordinary: people make mistakes, agents make mistakes, and records are sometimes deleted by mistake. Yet the fact that a timesheet existed and was later deleted can itself matter. Removing it completely would eliminate not only the data, but also the possibility of correction and accountability.

This did not mean that every draft should be preserved forever. It meant that an agent-facing system needed an explicit path for recovery. Agents are valuable partly because they can act quickly. The record system behind them therefore has to make errors visible, recoverable, and auditable.

The lesson was not unique to timesheets. An intelligent client increases the range and speed of possible action, but it does not reduce the need for durable records. It increases it.

## The first boundary was already visible

The early service made another choice that later became important. The approval table recorded approval facts, but an approval record did not automatically move the timesheet to another state. The service could know that a particular person approved or returned a particular document at a particular time. It did not claim to know who should review it next, whether finance review was required, or whether a return should restart the entire chain.

At that point, this was not yet a complete theory of agent-native ERP. It was a practical boundary: store the facts that can be stated with certainty, and leave company-specific process judgment outside the record service.

Many later parts of ORYH grew from that boundary. Generic business objects preserved company-specific records. Todos made unfinished human work visible. Workflow definitions stored company rules as versioned prose. Skills told agents how to perform bounded business work. A workflow-driving agent read those definitions and decided what to do next. The server continued to record the result and reject actions that violated deterministic constraints.

ORYH therefore did not begin with the question, “How can AI run a company automatically?” It began with a smaller and more durable question: **when an agent starts acting on behalf of a person, what must outlive the agent's answer?**

The team's first answer was modest: a timesheet, its entries, the person's original words, and the facts left by every approval action. The system later expanded into orders, inventory, invoices, payments, policies, and payroll, but that answer remained stable.

Agents can be replaced. Models can improve. Skills and workflows can be rewritten. What a company has already done must survive outside any single conversation, in a system of record that does not depend on the continued memory or availability of the agent that happened to perform the work.
