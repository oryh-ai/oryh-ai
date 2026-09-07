# Who Actually Took This Step?

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 8*

An approval record says “approved by the general manager.” It looks like the work can move forward. But if an agent wrote that record, there's another question: on whose behalf did it write it?

An agent preparing an employee's paperwork, one recording a manager's decision, and one moving a workflow forward may all use the same interfaces. A successful call means the system accepted an action. It doesn't make those responsibilities interchangeable.

We initially worried more about agents exceeding their authority. Then we ran into the opposite problem: an agent stopped itself from doing something it was allowed to do.

## A different job doesn't make you a different person

One user was both the workflow administrator and the general manager. They had asked their agent to carry out some administrative work, then asked it to record their own approval decision.

The agent hesitated. It treated its earlier administrative actions as evidence that it was now acting as “the administrator.” Recording the general manager's decision seemed like impersonating someone else, so it refused to continue.

That sounds cautious, but the premise was wrong. One person can hold several responsibilities. Changing a setting a moment ago doesn't turn them into a different person.

We checked the code. Attribution for a user-bound credential was already determined by the server. When recording an approval, it used the authenticated user and ignored a different approver identity supplied in the request. The agent couldn't put the action under a colleague's name just by changing a field.

What was missing was an explanation to the agent. We added one to the operating instructions: check who the current credential belongs to instead of inferring identity from previous tool calls. Roles describe what someone may do. User identity tells us whose name those actions are recorded under.

This fix didn't add another backend restriction. It corrected the agent's understanding of an existing boundary.

## “Please don't impersonate anyone” isn't enough

That doesn't mean every credential has the same safeguards.

ORYH still supports service credentials that allow explicit attribution for service integrations. These differ from personal credentials: the identity named in the call may become the identity recorded. When using one to record a person's approval, “the interface allows this” cannot stand in for “this person authorized it.”

The instructions therefore also need to explain when to stop. An agent about to record a personal decision using a service credential should pause, explain the attribution risk, and establish the appropriate identity and authorization. For everyday personal approvals, we prefer credentials bound to the person involved.

The agent advancing a workflow has its own responsibility, too. It can arrange the next task using existing approval facts. It cannot supply someone's agreement just because the process needs an approval to continue. Where a person must approve, it still waits for that person.

The software has two definite jobs here: check whether the credential has the required permission, and record the action's attribution accurately. Judgments about missing evidence, returning a document, or choosing the next recipient still belong with the agent applying the company's rules.

## The right name isn't the whole answer

Correct attribution doesn't prove that a decision was justified.

The server can establish whose credential a request used. That alone doesn't tell it whether the person reviewed the material or actually expressed agreement. If an agent reads an ambiguous remark as approval, the name on the record can be entirely correct while the decision is wrong.

That's why we don't want to treat auditing as a complete answer. Approval comments, supporting material, and the relevant business records need to remain available for review. The agent needs to ask when confirmation is insufficient, rather than substitute “I have permission” for the person's intent.

Software records; agents handle business logic. When identity enters the picture, that division needs another distinction: what an agent is authorized to do is separate from what a person has decided to do.

We now prefer to check those questions individually: who initiated the action, what the authorization permits, and whose decision the resulting record represents. “The agent handled it” leaves far too much out.
