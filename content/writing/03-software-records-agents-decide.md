# Software Keeps the Records. Agents Handle the Logic.

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 3*

While building ORYH, we've found ourselves coming back to one sentence: the software keeps the records; the AI agent handles the logic.

In a conventional ERP project, a new requirement tends to send us straight to familiar questions. Which fields do we add? How do we configure the workflow? Which condition sends execution down which branch? The company's way of working gets translated into rules the software can execute. Add an agent on top, and if all those decisions still belong to the application, the agent is mostly another way to operate it.

We want to try moving the boundary further. Apart from hard constraints such as arithmetic, permissions, and data integrity, business judgment and the work of moving a process forward should mostly belong to the agent. ORYH remains the system of record. It stores business facts and the company's written rules, but it doesn't interpret those rules.

That's easy enough to say. When writing code, we still find ourselves slipping back into old habits.

## We made a decision that wasn't ours to make

Expense reimbursement gave us one fairly concrete lesson. Some companies turn an approved expense claim into a payable document, then apply the payment to that document. Others would rather apply the payment directly to the expense claim, without creating another document in between.

At one point, we removed the second route and required everyone to create the payable first. It looked tidy, and it avoided the risk of settling the same expense through both routes.

But why did every company have to work the way we'd chosen?

The thing code actually needed to prevent was double settlement. Take a claim for 1,300. Apply 1,300 to the claim and another 1,300 to its payable, and neither document individually looks over-settled. Together, though, the records say that 2,600 has been applied to one expense.

We restored direct settlement and made the two routes mutually exclusive. The agent reads the company's rules and follows the appropriate route. Once a claim has taken one route, the server refuses an attempt to settle it again through the other.

“How does our company handle reimbursement?” and “this expense must not be settled twice” turned out to be different questions. We shouldn't have quietly answered the first one for everyone while fixing the second.

## So what logic stays in the software?

Quite a bit, of course. The server should calculate an order's line-item total accurately. That's not a number we want a model to improvise. A payment must not be over-applied. Someone without permission must not be able to write. Retrying the same ledger request must not record it twice.

These are conditions for trustworthy records, not opportunities for agent judgment.

Whether a document needs to go back for more information, whether a discrepancy needs someone's confirmation, and who should approve the next step are different kinds of questions. Company rules can change. There may be exceptions. The agent needs to read those rules against the facts and work out how to proceed. Where a person needs to approve, it still waits for that person.

So “the agent handles the logic” doesn't mean it does every calculation, or gets to make everyone's decisions for them. It means business judgment moves out of the application code.

## The rules need a durable home, too

That raises another question: if the logic belongs to the agent, does every run become an improvisation?

It can't. The company's rules need to be written down. ORYH stores versioned workflow definitions. The agent reads them alongside the document, approval history, and open work items to decide what comes next. If something is unclear, it asks. If the necessary basis is missing, it stops. It shouldn't invent a process to fill the gap.

And records need to contain more than a document's final status. Who approved what, and which version of the rules a routing decision followed, need to remain inspectable. Otherwise, the agent can say “all done,” and we still won't know what it actually did.

These days, a new requirement prompts a question before we start implementing: are we ensuring that the records are correct, or deciding how the company should conduct its business?

We're still learning to tell those apart. Adding a backend condition can feel like an obvious fix, while quietly freezing a practice the company should be able to change. That's the separation we're exploring with ORYH: software that keeps the facts straight, and agents that move the work forward under the company's rules.
