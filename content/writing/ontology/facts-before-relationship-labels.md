# Stop Worshipping Ontology: Your Relationship Map Is Not Your Business Reality

*When Agents Run the Business: Notes on Building ORYH · A development note*

The previous two essays on ontology explored what gets lost when a business is squeezed into a model, and how that model gradually falls behind the business.

This time, we want to raise a more immediate problem: the relationship itself can be where a bad judgment begins.

Enterprise AI can create a convincing illusion. Connect the customers, suppliers, and products, and it seems to understand the business. But even a complete relationship map does not mean it knows what to do now.

## The relationship survives. The business may not.

Consider an example.

“A is a supplier to B.”

Two objects, one supply relationship. If an Agent is looking for purchasing options for B, A naturally enters the shortlist.

Now add one fact: “A last delivered goods to B five years ago.”

That changes things.

Has A changed its product lines? Is the old contact still there? What are its current prices, capacity, and lead times? We don't know. What looked like “place an order with a familiar supplier” becomes “contact a historical supplier and check the conditions again.”

Five years without a delivery does not mean A is unsuitable. It might still be the best choice. But “ready to order from” and “worth getting back in touch with” are very different judgments.

What makes that difference is not the supplier label. It is what happened, when it happened, and what remains unconfirmed.

For this decision, the fact of the last delivery matters much more than the relationship label.

## The dangerous relationship need not be false

The relationship does not even have to be wrong.

A really did supply B. But the Agent may casually make several further inferences: they have done business together, so they are familiar partners; they are partners, so the supplier has been approved; the supplier was approved, so we can buy from it now.

Each step sounds plausible. Together, they can be completely wrong.

A trial order becomes an established partnership. Experience supplying one product becomes familiarity with an entire product range. A qualification from five years ago becomes a qualification that still applies today.

The label hides those differences.

Connecting more relationships can amplify the problem. A supplies B, and B is an important customer of ours. Does that make A critical to our business? We still need to know what it supplies, in what quantities, whether alternatives exist, and whether those transactions are still happening.

Adding more edges does not supply those missing facts. Our concern is precisely this: confusing “the relationships have been modeled” with “we have enough evidence to decide.”

## A fact needs more than a confident sentence

We have to apply the same discipline to our own argument.

“The last delivery was five years ago” is not something an Agent should simply announce.

Which records did it search? Was the historical data fully migrated? Could another department still be buying from A? Did it find the last purchase order, or the last actual receipt of goods? Those are different events.

If it searched only the current system, a more accurate statement would be: “Among the receipt records currently available, the most recent is from five years ago. We still need to check for other transactions.”

Not found does not mean it never happened. A record updated today does not mean the transaction happened today, either.

This is why “software handles records” means more than putting a few statements in a database. Dates, quantities, linked documents, sources, and subsequent corrections all affect whether the Agent can use a record properly. A database row is not a guarantee that reality has been described completely or accurately.


The factual foundation we want consists of records that can be questioned, checked, and corrected—not confidence wearing a different name.

## Yes, an ontology can represent facts

An obvious response is: add timestamps, transaction details, and sources to the relationships.

Of course that is possible. Ontologies are not technically incapable of representing these things. [W3C's PROV-O](https://www.w3.org/TR/prov-o/), for example, can represent provenance and temporal information.

Our objection is not to that expressive capability. It is to treating object relationships as the foundation for enterprise AI decisions.

If meaningful decisions still require returning to actual transactions, source material, and current conditions, those facts should sit at the center. Relationships help locate and organize evidence. They do not replace it.

“This order belongs to this customer” can itself be a clear fact. We are not against links, and we certainly do not want to remove every association from the database. We object to jumping from a broad business relationship directly to a specific business decision.

## The boundary we want Oryh to maintain

In Oryh, this distinction shows up in concrete places.

The system has supplier–product associations and can record the latest price. Purchase orders and goods receipts are separate records. But “this supplier has supplied this product,” “this was the previous price,” and “these goods have now arrived” must not collapse into “this supplier is fine.”

An order is not a delivery. A delivery does not automatically establish that the next delivery will be reliable. Software connects these records so the Agent can investigate—not so it can prewrite the conclusion on the Agent's behalf.

Then comes the company's own logic.

For example, a user might say: “Get a new quote from any supplier we haven't bought from in more than two years. Urgent orders need confirmation from the purchasing lead.”

That is a natural-language requirement. It should not require building a new supplier-evaluation module. The Agent should use the instruction to examine purchasing and receipt records, identify missing information, and decide whether to request a quote, seek confirmation, or proceed.

Another company may accept a five-year-old business relationship but require a fresh capacity check for every order. Its Agent should follow that requirement instead. The two companies should not have to adopt the same management practices first.

Of course, one sentence from the user does not make every condition clear. Does “haven't bought from” refer to the order date or the receipt date? Ask when the instruction is ambiguous. Gather information when it is missing. Do not let the Agent fill the gaps with assumptions.

Software keeps accurate records and enforces essentials such as amount calculations, permissions, and protection against duplicate writes. The Agent uses those facts and the company's requirements to judge what happens next. That is the division of responsibility we want.

Following that approach, the Agent's answer to a buyer should not simply be: “I recommend A because it is an existing supplier.” A useful answer explains which historical receipts it found, how old the latest one is, which conditions remain unverified, and why the company's requirements call for a fresh quote.

This is something we need to keep checking as we build: does the Agent offer a label, or a line of reasoning someone can trace back and verify? If the decision later proves wrong, people should be able to distinguish incomplete records from unclear instructions or faulty reasoning. Otherwise, however impressive the relationship map looks, the explanation ends at “the AI decided.”

## Start with what happened

The appeal of ontology is the feeling that defining a company's objects and relationships means capturing how the company works.

But running a business is not a walk through a relationship map. It means dealing with a reality that keeps changing and is often only partly visible.

Before an Agent makes a decision, we want it to ask: What happened? When? Where is the evidence? What do we still not know?

“A supplies B” can be a starting point for investigation.

It should never be a reason to stop investigating.
