# How Many Objects Are There in One Car?

*When Agents Run the Business · A development note*

Imagine a modeling meeting with a sketch of a small car on the table. One person says, “Surely this is one Car object. Give it a VIN, model, and color; make tire specification and steering-wheel model properties.” Another says no: each tire needs its own identifier, replacement history, and warranty claims. The steering wheel might be repaired separately too. A third person asks, “Are we modeling the bolts as well?”

This is a thought experiment, not a customer incident. The argument, though, is familiar. Before you can draw relationships between enterprise objects, you have to decide what deserves to be an object at all.

## Existing in the world is not enough

A tire is a real thing. So are a steering wheel and a bolt. That does not mean each needs an independent identity in a business system. Otherwise, where do you stop? Rubber, steel cord, and individual nuts can be split further.

Sales wants to know who bought the car and when it was delivered. A whole car is a useful boundary for that question. A mechanic needs to know whether the front-left tire was replaced last month. For that question, one Car object is too coarse. Warranty may need to trace a batch of tires across many vehicles. Finance may register the car as a single asset and never care what the four tires are called.

None of these people is more knowledgeable than the others. They are asking different questions. The grain of an object follows the grain of the question.

In a modeling meeting, someone may suggest splitting everything into physical items now because it could all be useful later. Even a physical boundary is not stable. Is a retreaded tire still the same tire? If four tires are sold as a set and one is returned, is the set also an object? The physical world does not dictate commercial identity. Whether to track something separately depends on whether it can be traded, stored, accounted for, or claimed against on its own—and those needs change.

Trouble begins with “let's settle the enterprise definition of a car.” A meeting can settle a definition for now, but it is also choosing on behalf of future users. If a later repair process must track individual tires, a tire-specification property will not be enough. At the other extreme, if we create an object for every removable part from day one, selling a car may require people to maintain a long list of identities nobody currently uses.

## Too coarse leaves nowhere for facts; too fine gives people work for the model

The cost of a coarse model is easy to see. If the system stores only “the car was repaired,” it cannot later answer which tire was replaced or where the removed tire went. Without an identifier and installation and removal dates, the answer is simply not in the records.

The cost of a fine-grained model is less obvious. Once each tire has an ID, someone must record which car and position it occupies, when it was mounted or removed, whether it was moved to another car, and who verified its identity. Miss one scan, and a tidy relationship graph may link the wrong tire to the wrong car. Even “which tires are on this car?” becomes a question about time: “was once attached” is not the same as “is attached now.”

Should the steering wheel be managed this way too? Maybe, if there is a recall or a requirement to repair individual units. Maybe not, if it is only sold as part of a car. More objects do not automatically mean more accuracy. Fine-grained objects nobody maintains can make errors look unusually precise.

That is why I hesitate whenever someone says an enterprise ontology must come first. A local workflow can choose a grain around a known question. A single company-wide model has to make bets about questions that have not arrived yet. When those bets turn out badly, existing identities, links, and actions do not rearrange themselves.

## The same car can have several useful views

The obvious reply is to give sales a car view and maintenance a tire view. I agree. That is often better than fighting over a single “correct” car ontology. Different views can share the VIN, sales records, and repair documents while drawing out what each team needs.

But multiple views do not mean a complete underlying truth has already been captured. Imagine a repair ticket that says “replaced front-left tire,” a warranty note that says “replaced tire from batch X,” and a warehouse movement that says only “one unit shipped.” Are those three records about the same physical tire? We need evidence. Without a serial number, the best answer may be “possibly.” We should not invent a link merely because the diagram has room for one.

Even the word “car” shifts with the question. Sales means a transaction for a whole vehicle. Finance means an asset. After-sales service means a physical item in front of a mechanic. The labels match, but the identity rules may not. If a car is sold and later bought back, is it the same asset or a new one? If its engine is replaced, is it the same car? A dictionary cannot settle these questions on its own.

I would rather keep the facts stable first: the VIN, the order that sold the car, the action recorded on a repair ticket, and the document that identifies a particular tire. Give a tire its own identity when there is a reason and evidence to do so. When the evidence is insufficient, record “unknown” instead of promoting a guess into a confirmed relationship.

## Start with the decision someone needs to make

A modeler often asks, “What objects does the company have?” I would start elsewhere: “Who needs to decide what now? Which records support that decision? At what level of detail must the answer be exact?”

If the task today is selling whole cars, the car record, order items, and exact totals need to be right. If tomorrow requires tracing an individual tire recall, add tire identifiers, installation events, and sources. For older cars without identifiers, acknowledge the gap. A new requirement should change what we record going forward, not force us to invent the past.

This does not abolish structure. Orders, assets, and repair events still need clear recording formats. It changes what structure claims to be: a way to preserve known facts and answer current questions, not a promise to exhaust every meaning of “car” across the company.

Some industries do need detailed part lineage for years. In that setting, individual part identities deserve careful design and may become essential infrastructure. My objection is not to detail. It is to treating more detail as inherently more complete before testing it against an actual problem, or making every department adopt one universal cut.

We learned something similar while building Oryh. An Agent once imported products into generic objects, leaving the existing product catalog empty. We later made the server reject clear naming collisions, while the Agent must inspect existing types, explain near matches, and ask for confirmation. Software guards definite record boundaries; the Agent takes responsibility for meaning. The answer to “how many objects in one car?” should come from the work to be done and the evidence available, not from a diagram that claims to define the whole company.
