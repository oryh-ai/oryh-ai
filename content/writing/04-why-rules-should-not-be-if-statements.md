# Why Company Rules Shouldn't Become a Pile of `if` Statements

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 4*

Once business logic moves to the agent, the next question arrives almost immediately: where do the company's rules live?

The easiest answer is to let the agent remember them. Tell it, “A manager approves anything up to 10,000; above that, add the general manager.” With one agent and a handful of rules, that can work.

It gets less comfortable when different agents prepare the document, handle the approval, and move the process forward. One may remember yesterday's rule. Another may have the revised version. A third may not know that anything changed. They can all claim to have followed the process, while nobody can say which version they followed.

If memory isn't enough, the natural engineering response is to put the rules in code.

## One condition quickly grows into a system

“Add the general manager above 10,000” is an easy `if` statement. Then come the qualifications: only for equipment purchases, but not renewals; check the project budget first; return the request if quotations are missing; let urgent purchases take a different route.

One condition becomes a set of conditions. Soon the set needs a configuration screen, operators, priorities, and a way to handle exceptions. Every change in company practice becomes a question about whether the code covers the new case.

This is perfectly buildable. Conventional workflow products have been doing it for years. But if ORYH follows the same path, the agent ends up triggering a rule machine. The company's process logic hasn't really left the software.

Our current approach is to keep a workflow definition as a natural-language record. It can state what a document must contain when submitted, who looks at it first, when another approval is needed, and what happens after a return. Before moving the process, the agent reads that definition alongside the document and the approval facts already recorded.

Changing the rule publishes a new version instead of overwriting the old text. Previous versions remain available, and an agent assigning the next piece of work records which version it consulted. That gives us an answer to a very ordinary question: why was this document sent to this person at that time?

## Natural language isn't permission to improvise

Writing the rule as prose doesn't mean the agent gets to interpret it however it likes.

“Add the general manager when the amount exceeds 10,000” is fairly precise. “For larger amounts, it would be better to have a leader look, unless it's urgent” leaves quite a lot unstated. How large is larger? Which leader? What counts as urgent? The agent shouldn't quietly fill those gaps.

The constraint we use is simple: if there is no rule, don't invent a process. If the rule conflicts with itself or omits something essential, stop and ask. The question belongs with the person who defines the rule. An agent can interpret text, but interpretation shouldn't become a way to create company policy on its own.

Code still guards the other side of the boundary. Someone without permission can't approve. An illegal lifecycle transition is refused. Retrying the same approval fact doesn't record it twice. These constraints don't change with the company's wording, and they don't need agent judgment.

## The hard part moved rather than disappeared

We used to discuss whether the conditional expression was correct. Now we spend more time asking whether a sentence is clear enough for the submitting agent, the flow agent, and the approver to reach the same understanding.

That doesn't make process design automatically easy. Natural language can be ambiguous. Rules can conflict, and a new version can appear while work is already under way. The difference is that these problems now appear where they belong: in the company's rule text, rather than scattered across backend branches.

For ORYH, a rule is another durable business record. The software keeps the text and its versions. Agents read and apply it. People can inspect the result, challenge the interpretation, and publish a clearer version when the wording isn't good enough.
