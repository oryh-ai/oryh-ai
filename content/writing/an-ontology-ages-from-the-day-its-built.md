# An Ontology Starts Aging the Day It's Built

*When Agents Start Operating the Business: Design Explorations from ORYH — A Development Note*

In our last note we argued that ontology shouldn't be the foundation of enterprise AI. A fair challenge came back: you say it loses information — what exactly does it lose?

So let's put the material on the table. Every example below comes out of building Oryh, and some of them are holes we dug ourselves. There's a direct way to judge an ontology: set the source material next to the objects built from it and ask, line by line, "is this still here?"

## Properties: whatever wasn't imagined on modeling day is gone

When we built the contract module, one test case carried this payment clause: 30% within three business days of signing, 60% before the first shipment goes out, and the remaining 10% upon acceptance.

Model it the ontology way and you get a Payment Term object with a percentage and a trigger event: 30%/signing, 60%/shipment, 10%/acceptance. It looks complete.

Except "within three business days" has nowhere to live, and neither does "the first." So when someone later asks whether that first payment is overdue, or whether 60% is due again before the second shipment, the model has no answer. Not a wrong answer — those two conditions were never allowed in.

Want to add them? That isn't one more column. The object type changes, the pipeline changes, objects already built need backfilling, and everything downstream follows. And the condition nobody thought of is different in every contract.

Now take leave. One test case is a request from Friday through Monday, recorded as two days.

If a LeaveRequest object carries a `days` property, is that two or four? The answer isn't in the object. It's in a particular version of the company's policy text: whether weekends count, and how they're converted. The model can store one number, and which convention that number follows is a decision the modeler made on behalf of the whole company.

"Days of leave left" is even less of a property. One example in our Skill reads: 4 days available = 10 days accrued (policy v3) − 5 days approved − 1 day pending. That 4 is an answer computed from the applicable policy version, the hire date, and the relevant requests, and it's reported with the arithmetic and the policy version beside it. Freeze it into a field and the moment the policy changes, the number starts lying — without mentioning that it has.

## Cardinality: one bank debit, ten payment records

Pay ten people their salaries and you get ten payment records internally and, on the bank statement, a single aggregate debit.

Our first version of payment reconciliation could only link a statement line to one payment. Link it to one person and the other nine are unexplained. Leaving it in the unreconciled list wasn't because the money hadn't moved; the record structure simply couldn't say what happened.

That wasn't AI misunderstanding anything. It was a cardinality decision frozen on modeling day, and changing it meant touching the API, the data, and every link already made. We now let a statement line reference a whole payment batch, with code holding the hard checks: in the test, three payments of 300, 200, and 150 total 650; a 650 debit can be linked, a 640 debit is rejected with "three payments, total 650, off by 10."

Inventory shows it even more plainly. A single stock number quietly merges two different facts: the goods are still in the warehouse, and the goods can still be promised to someone else.

In our test, a location holds ten units, and three are reserved for an order: on hand stays ten, available drops to seven. When those three actually ship, deducting three again would leave seven on hand and four available — the goods moved once, but availability was charged twice. So the server consumes that order's reservation and records the issue in the same transaction, leaving seven on hand and seven available. Split shipments matter too: reserve three, ship two, then ship two more, and the second shipment can only consume the one remaining reservation while the other unit comes from unreserved stock.

Code has to get that arithmetic right. But it can only do so because reservations and stock movements are two distinct kinds of fact in the model. If modeling day left a single "quantity" property, even the sharpest AI can only reason over a number that has already conflated two things.

An ontology isn't the truth of the business. It's what the modeler believed the truth was, on one particular day.

## Boundaries: the more complete the ontology, the easier it is to route around

During one historical data import, an agent wrote roughly 150,000 records — customers, products, quotes, sales orders. All apparently imported. Meanwhile Oryh's own customer list, product catalog, and business documents were still empty.

It had created a custom object type for each of them, named customer, product, quote, and sales_order, and written straight in. It never stopped to ask, and the software didn't stop it either.

Anyone betting on an ontology should sit with that. Any model claiming to cover an enterprise has to leave an escape hatch — custom objects, extension fields, free text. And escape hatches get used, comfortably. The import "succeeded" while none of the existing links, queries, or business capabilities came into play.

How we fixed it is just as telling. The server now blocks only unambiguous name collisions: `product` is rejected with a pointer to where the data belongs, while `merchandise` still goes through. The rest of the work went back to the agent: read the list of existing types first, compare business meaning, explain why the existing structure isn't enough, wait for a person to confirm, and write that reason into the type definition.

Which means the judgment — is "goods master" just the product catalog? — still comes down to reading text, comparing meaning, and asking someone. An ontology promises to settle that once and for all. It settles part of it, and the part it doesn't settle never goes away on its own.

## Actions: an ontology freezes the business logic too

This layer deserves the most suspicion. An enterprise ontology doesn't only describe data; it models executable actions and business rules as well. Business logic becomes, once again, a layer of software that has to be modeled, reviewed, and released.

Take a concrete request. An administrator says: from now on, once an expense claim is approved, settle it directly instead of turning it into a payable first.

In our setup, that sentence is stored as the company's supplementary note on the payment Skill. The payment agent reads it before it reads the expense claim's workflow definition, and if the two conflict, it stops and asks. Code still prevents the same expense from being settled through both routes. The company changed its practice; the product didn't fork.

Model the action instead, and that sentence becomes a modeling change: edit the action, pass review, cut a release, migrate. Every change in practice opens a project. That is exactly the old problem of rebuilding the ERP whenever management practice changes, under a newer name.

Rule growth works the same way. "Over 10,000 needs the GM's approval" is one easy condition — until equipment purchases need the extra approval but renewals don't, some projects check budget first, missing quotes get sent back, and urgent purchases take another route. One condition grows into a rules engine, and the agent's job is reduced to pressing its start button.

## The strongest objections, stated properly

**"AI misreads, so it needs an ontology underneath it."** AI does misread. The remedy is keeping the original, recording where the evidence sits, and letting a person ask "what made you decide that?" — not handing it a condensed copy that can be wrong in exactly the same way. A summary can drop "three business days"; so can an ontology. The difference is that the summary sits next to the original and a page number.

**"Context can't hold an entire enterprise."** Hence indexes: clause excerpts, page references, product-title mappings a person has confirmed. The difference is that an index points back to the original while an ontology replaces it. We keep the platform's raw product title, and look up the mapping that was valid on the order's own date — the listing link may not have changed while what it sells did. Explaining yesterday's order with today's product is another avoidable error.

**"Permissions, audit, and amounts need structure."** They do, and we have it: direction and total checks, idempotency, attribution of who acted, reservation and shipment settled in one transaction. Those are constraints on facts, not translations of meaning. Making the money reconcile doesn't require modeling what "dealer" means first. And for candor: we still have an open hole of our own — in a concurrency test, ten units available, two requests each reserving seven, both succeeded, leaving availability at minus four. That side needs work too. It's just work on records, not on meaning.

**"An ontology makes AI faster and cheaper."** Reading source material does cost something, and we're still working out that trade-off. But what you save is tokens, and what you spend is information — and you don't find out where you spent it until someone asks a question nobody modeled for.

## Three questions

So show us an ontology, and we'll ask three things.

Which sentence in the source material did this property come from, and can that source still be opened?

The company changed a practice six months ago — what did the model keep, or did a new value overwrite the old one?

Someone asks a question today that nobody anticipated at modeling time. Is the answer in the model, or in the part the model discarded?

Answer all three and what you have is an index. Keep it. Fail them, and what you have is an intermediary standing between AI and the facts — aging from the day it was built, and never announcing it.
