# One Hero Can Save a Project. That Is Not a Delivery Model.

*When Agents Run the Business · A development note*

Many of us have seen a project like this: the customer is complicated, and one exceptional person on site lives inside the problem for months. They learn the workflows, bring departments together, and get the system live. It succeeds, and the supplier announces, “Our FDE model works.”

I do not doubt the person's ability. Precisely because they are exceptional, we should ask an unpleasant question: will the system still work after they leave? If the answer is “call them back whenever something happens,” a great person saved a project. That is not a repeatable delivery model.

## Star projects often forget the handoff

The hardest judgments tend to live in someone's head. Why does this customer settle a particular expense directly instead of making it a payable first? Why must a warehouse reservation not be released immediately when an order is canceled? Which finance lead reviewed a special case, and which kind of payment still requires a phone call? The senior person handles these naturally because they know the history.

At handoff, the team may leave system accounts, meeting notes, and a project checklist. A replacement can operate the software but cannot explain why one step was left manual. After people inside the customer company change roles, “we've always done it this way” is even less useful.

I am not asking an FDE to turn every insight into a huge implementation manual. Some judgment cannot be written as a universal recipe. But every customer-specific rule that affects system behavior should at least preserve the original instruction, its scope, the person who confirmed it, its version, and one real case. Every “ask a person for now” stopping point should identify whom it is waiting for. A replacement should not have to borrow authority from the departed person's memory.

The handoff should also say what the team tried and chose not to do. A field lead may have evaluated automatic payment, found that old payment records lacked verifiable account details, and left the action for finance confirmation. If the handoff shows only the final configuration, a successor may assume automation was merely unfinished and reopen the same risk. Rejected paths and their reasons are project assets.

## Do we replicate a person or a capability?

If a real FDE is the intersection of industry experience, engineering skill, and organizational judgment, they will be scarce. After one or two successful projects, a vendor can easily mistake that success for a scalable “FDE delivery process” and try to expand it by adding bootcamp seats. A process may be copied. Judgment cannot be wholesale distributed by headcount.

The better thing to replicate is product capability. If one field lead encounters a bank debit that covers several payment records, every later customer should not inherit a private reconciliation script. If the product can record a payment batch and check direction and totals, the next team does not have to rediscover the problem. The field finds a gap once; product fixes it once. That can scale.

Other experience belongs in a method rather than hard-coded software. Take “urgent orders can go ahead.” A useful method asks how far ahead, who may declare urgency, when evidence arrives, and where a human stop is needed. The method does not give every customer the same answer. It helps every on-site person ask the important questions.

Some decisions cannot be replicated and need a senior person. Major organizational conflict, risky payment paths, and product architecture tradeoffs may require their direct attention. State which projects will get that time and price the time honestly. Do not put the expert's photo in every proposal if they will attend only the first fifteen minutes.

The supplier also needs a relay. Can a second colleague reproduce the key judgment from existing records? Can the product team see whether a field patch applies only to one customer? If only the hero can explain it, their experience has not become organizational capability. Hiring another equally gifted person may shorten the queue for a while, but it does not make the earlier project easier to maintain.

## Measure how long a project can live without its hero

A supplier counting “customers per FDE per year” may be using the wrong unit. The person's commitment does not end at go-live. New policies, product upgrades, staff departures, and unusual data imports all call for judgment again. If every event returns to the same hero, more customers mean a longer wait for everyone already served.

The familiar degradation follows: the first project is led by a star, later projects copy a template, and anything outside the template queues for the star. Sales still says the FDE model scales. Customers receive an ever-longer expert booking calendar.

Try a “lead is on leave” test. For two weeks, can the customer handle an ordinary rule change? Can a replacement find the evidence for an earlier decision? When an Agent sees an unfamiliar case, does it stop to ask or continue under stale configuration? Only when these things work is project success less dependent on one person remaining present.

Track a less flattering measure too: how often must the departed lead return for an old customer? One return is not failure; difficult exceptions may genuinely require expertise. But if changing an approver, confirming a product mapping, or explaining an old document all require booking that person's calendar, delivery was not really finished. Acceptance should include “a new team can carry this,” not only “the system runs today.”

The customer might eventually change suppliers altogether. If every business rule exists only in the original team's heads, it cannot even take an explanation of its own system with it. Good delivery should not turn personal expertise into permanent customer lock-in. It should leave the customer able to inspect and revise its own records and rules.

This does not require every colleague to become a super-individual. It asks software and documents to carry the memory they should carry. Software preserves facts, versions, and actions; Agents read current customer rules and explain their judgment. Senior people appear when a real tradeoff requires them. Put repeatable work in the product so scarce judgment is spent where it matters.

In Oryh, we do not want a customer's way of working hidden in an on-site engineer's private code branch. Workflow definitions are versioned natural-language records; approvals and work items remain facts; Agents use the current rules to advance work. Good people are still needed to establish those rules and test the risks, but a successor can at least read why the system behaves as it does. A hero can rescue a launch. Whether the project continues after they leave is a joint test of the product and delivery model.
