# One “Unless” in the Policy. What Happens to Yesterday's Approvals?

*When Agents Run the Business · A development note*

Imagine an after-sales company with a simple first policy: if a car was bought less than two years ago, tire damage can be accepted under warranty. The system marks a batch of claims as “covered.” Some have generated work items. A few may already have been approved for free replacement.

Later, customer service and the repair team add detail: individual tires may have their own claims, unless the tire was previously replaced with a customer-supplied part. The policy gains one “unless.” The questions it raises are considerably larger.

The car case is fictional. The point is not to decide the right warranty terms. It is to ask what a new rule does to judgments already made.

## A new rule is not just another column

Before rerunning every record, ask when the new policy takes effect. Does it apply only to new claims, or also to open ones? Should an approved tire replacement be reviewed again if stock has not yet shipped? Can a tire already installed on a customer's car suddenly be relabeled “not covered”?

A technical system cannot announce these answers for the company. They involve promises to customers, responsibility, and authority to change an earlier decision. Splitting Tire out as an object answers “what can the system represent?” Adding an exception raises a different question: “what do we do with decisions already made?”

We must also separate the day a policy was published from the period it says it covers. A company may issue a clarification today that explicitly applies to applications from last month; another change may take effect next Monday. Reading the latest text today does not authorize an Agent to overwrite every decision made yesterday. It needs the claim date, the decision date, and the stated scope of the policy.

At least four things need to remain separate in each claim: the facts known at the time, the policy in force at the time, the judgment made from them, and the action actually taken afterward. Learning today that a customer brought their own tire is a new fact. Publishing a new policy is a new rule. Canceling a task is a new action. Do not squeeze all four into one “current warranty status” field.

Otherwise someone opening an old claim may see a red “expired” label and assume the service team broke the rules two months ago. They may have followed the rules perfectly at the time. A later change does not automatically make past behavior wrong.

## Learning something new is not the same as retracting an answer

There is a technical illusion here too. A rule that links “the car was bought within two years” to “the tire is covered” may seem to work nicely at first. When “unless the customer supplied the part” arrives, it is tempting to believe that adding the condition will make old conclusions disappear on its own.

That is not how the problem resolves. As one bounded comparison, [W3C's RDF 1.1 Semantics](https://www.w3.org/TR/rdf11-mt/) describes monotonic entailment: adding information does not by itself cancel conclusions that followed from the weaker premises. A business “unless” may require a new decision, the expiration of an old conclusion, or the cancellation of an action that has not yet been performed.

This is not a claim that every ontology system is incapable of handling exceptions. A system can use policy versions, effective dates, state transitions, and explicit retraction mechanisms. It can preserve an old conclusion as history and calculate a different answer for the current case. The question is who defines the scope and effect of each exception, including how far back it reaches, and who connects all those pieces. Another edge in the graph does not answer that on its own.

Some cases are murkier. The customer supplied the tire but the company supplied the wheel; the service adviser wrote an incomplete note; the customer has a purchase receipt but no proof of installation date. “No evidence that it is covered” is not automatically “proven not covered.” Before an Agent proposes a denial, it should show the missing evidence and the relevant clause so someone can check.

## Executed actions do not run backward

The easiest part to miss is what has already happened. A work item can be canceled. An approval record should not be erased. A tire shipped from the warehouse cannot become “back in stock” just because the policy changed. If the new rule calls for retrospective review, that is a new business action. Who starts it, who contacts the customer, what evidence may be supplied, and whether the original decision can stand all need to be recorded.

I would rather see a timeline than one label that continually overwrites itself. The timeline says when the claim arrived, which policy and repair ticket the Agent read, who approved what, when the new rule appeared, whether it called for review, and what the review decided.

An Agent handling the case today can then read the whole sequence. It might say, “This claim was approved under the previous policy but has not shipped; the new policy requires us to confirm who supplied the tire.” Or it might say, “The new policy applies only to claims made from today, so the earlier decision stands.” Both can be reasonable, provided the company actually set the scope instead of leaving a system to guess.

Software should preserve policy versions, approvals, work items, stock movements, and who performed each action. Exact totals, permissions, and protection against duplicate actions still belong in code. The Agent relates the current rule to the claim's facts and explains why it recommends moving forward, pausing, or reviewing. If retrospective scope is unstated, it should ask.

Pending work items deserve particular care. A “replace this tire free of charge” task already sent to a warehouse should not quietly vanish because an overnight job recalculated status. Leave a cancellation or pause record. Tell the person doing the work which policy version caused the change, who approved the earlier step, and whose confirmation is needed next. Otherwise the automation may look current while a real task simply disappears from someone's queue.

## Adding one sentence must not erase the rest

We also have to admit that an Agent can add an “unless” badly. In one real development feedback case, an administrator said only “add a condition.” The Agent replaced the entire active workflow definition with a short text containing that new condition alone. The server kept the old version, but the next Agent would read an incomplete current policy. We tightened the revision procedure: read the full existing text, list additions, changes, and deletions, and ask before making an unrequested deletion.

That incident is not an ontology bug. It does show why “versioning” must be more than a label. Whether a company writes policy as a graph, a rule table, or natural language, the scope of a change must be visible; earlier decisions must remain explainable; and completed actions must remain traceable. If one latest-state field hides the history, sooner or later someone will ask, “What rule did we actually use then?”

In Oryh, we leave interpretation and progression to the Agent without letting it quietly decide how far a policy change reaches. Software remembers old and new facts; the Agent compares versions and explains what to do now. One “unless” can change the next step. It should not wipe yesterday off the books.
