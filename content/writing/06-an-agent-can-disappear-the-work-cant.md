# An Agent Can Disappear. The Work Can't.

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 6*

When several agents take part in one business process, events are an obvious starting point. A document is submitted, so emit an event. A manager approves it, so emit another. A flow agent consumes those events and moves the work forward.

There is nothing unusual about coordinating ordinary programs this way. With agents, however, we quickly ran into two awkward questions: where does the cursor live, and does reading an event mean the work was actually handled?

Imagine an agent reading “manager approved” and timing out just before it assigns the finance review. If the cursor has already advanced, the work is lost. If it hasn't, the event will be handled again. Add acknowledgements, retries, and a dead-letter queue, and we're rebuilding a messaging system without answering whether the agent understood and completed the task.

## Ask what remains undone

ORYH eventually stopped using an event stream to coordinate agents. Instead, the business state itself says whether work is still waiting.

A todo is a person's inbox. `open` means the work is waiting; `completed` means it was handled. The flow agent doesn't ask, “Which event did I read last?” It asks, “Which submitted documents currently have no open todo?” As long as a document has nobody assigned to it, every query can find it again.

An agent disappearing halfway through a process no longer erases the position. Another machine, another agent, or the same agent after a restart can read the document, its approval records, and its todos, then continue from the facts that remain.

The audit log still exists, but it answers who did what and when. It is not a delivery mechanism. A notification may wake an agent sooner, but losing the notification only adds delay. The next state check still finds the document.

## State queries can still leave half a job behind

This design didn't solve everything by itself. We had an approval fact successfully recorded while the todo asking for that approval remained open. One record said “approved”; another still said “please review this.” The process sat there in that contradiction.

A return made the weakness even clearer. Recording the return, changing the document to `returned`, and creating a rework todo for the submitter used to be three calls. If the agent disappeared between any two of them, it left a set of records that were individually legal and collectively wrong.

We moved facts that must hold together into one transaction. An approval decision closes the todo that requested it. A return can write the decision, new status, and handoff todo together. Either all of them land, or none of them do.

That doesn't move business judgment back into the server. The agent still decides who receives the handoff, where the document returns, and which status follows, using the company's rules. Code only guarantees that once the agent makes that decision, its component records cannot land halfway.

## Retrying should be ordinary

An agent can also lose the response after calling an endpoint. It doesn't know whether the server never received the request or completed the write and lost the reply on the way back.

Approval records and task assignments therefore need safe retries. When the same business fact arrives again, the server returns the existing record instead of inventing a second approval or assigning a duplicate todo. Retrying shouldn't force the agent to guess what happened.

We now treat an agent as a collaborator that may leave at any moment, not as a workflow thread that lives forever in memory. Conversations, notifications, and runtime context can disappear. Documents, approval facts, and unfinished work have to remain.

That leads naturally to the next question: if the work stays visible in a queue, who looks at it regularly and keeps it moving?
