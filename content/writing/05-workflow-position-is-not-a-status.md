# Workflow Position Isn't a Status

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 5*

The most natural way to model an approval flow is often to give every step a status: waiting for the manager, waiting for finance, waiting for the general manager. One look at the status tells you where the process is.

That stays clear while the process is a straight line. Company processes don't remain straight for very long. Finance may ask the manager to review something again. Legal and finance may work in parallel. A returned document may need to start from the beginning after it changes. The same node can appear twice, and several nodes can be active at once.

We could keep adding statuses, of course. Before long, though, we would need combinations like “manager approved, finance pending, legal returned.” The status is no longer describing the document. It is trying to compress the entire process history into one field.

## Status only describes the document's stage

ORYH now keeps these two questions separate.

After a timesheet is submitted, it can remain `submitted` throughout the approval process. Approval records show which nodes have passed. Open todos show who currently has the work. The company's workflow definition says where it may go next.

Status answers a coarser question: is the document still a draft, has it been submitted or returned, or has the process finished? It no longer acts as the workflow cursor.

One immediate benefit is that the server doesn't need to know that the general manager must always follow finance. An approver records their own decision and completes their own todo. A flow agent then reads the facts, works out who should receive the next task, or decides that the process can finish.

Using fewer statuses doesn't automatically make the flow correct, though.

## We misread an approval history, too

We had a timesheet that was returned, edited across seven lines, and submitted again. When the flow agent read the complete approval history, it saw that the first approver had already approved in the previous run. It sent the changed document directly to the second approver.

But that approval applied to the old contents. If the second approver had continued, the timesheet could have finished without the first approver ever seeing the new version.

We made the round explicit in the approval records. A resubmission after a return starts a new round. When the agent asks which nodes have passed, it can only count decisions from the current round. Sequence numbers start over as well; they don't continue from the position left by the previous attempt. Unless the company's rule explicitly says a node doesn't need to review again, changed contents go back through the whole chain.

We didn't add a new status called “second-round manager review.” We recorded what had actually happened more precisely: which round this is, where a decision sits within that round, and whether it belongs before or after the returned document was changed.

## Fewer statuses, more facts

This makes the interface slightly less convenient. A `submitted` badge can no longer explain the entire progress of a document. To show where the process is, the interface has to present the approval trail and the current todos together.

We think that inconvenience is worth it. A status looks compact, but it easily hides parallel work, repeated reviews, and return-and-resubmit cycles. A richer set of facts lets both people and agents reconstruct the process from the same history.

Code still guards legal lifecycle transitions and prevents the same decision from being recorded twice on a retry. The agent decides who comes next, whether another review is needed, and when the document should enter its final state, using the company's rules.

We now think of status as a signpost in the document's lifecycle, not the workflow engine's current location. Where an approval has reached isn't the answer stored in one field. It is an answer read from the business facts.
