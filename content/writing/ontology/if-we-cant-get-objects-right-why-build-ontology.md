# We Still Struggle with Objects. Why Bet Enterprise AI on an Ontology?

*When Agents Run the Business · A development note*

Whenever the conversation turns to enterprise AI, someone says: build the ontology first. Define the customers, orders, products, departments, and approval actions. Then let the Agent work on top of them. It sounds reassuring. Once every object and relationship is in place, surely the Agent will stay on track.

It always makes me think of object oriented programming.

An ontology is not the same thing as an object oriented program. Nor does anyone need to master class hierarchies before discussing an ontology. The comparison raises a simpler question: are we really that good at deciding the boundaries of a business in advance?

## Does writing a class make a program object oriented?

Anyone who has spent time with software has seen the pattern. Put a collection of functions inside `OrderManager`, turn shared variables into instance variables, wrap the whole thing in a `class`. The syntax looks object oriented, but the program still follows one long procedural sequence. When a requirement changes, another branch appears inside the class.

That does not necessarily mean the programmer was careless. Deciding what an order is responsible for, where payment begins, or whether a concept needs its own identity is genuinely difficult. The business keeps producing new answers. A good class name does not settle the boundary.

Software teams spend a surprising amount of time asking whether something is a property or an object, whether it belongs to the order or to fulfillment, and whether inheritance or composition expresses what is really happening. Often, the missing piece is an agreed understanding of the business facts.

An enterprise ontology makes that problem larger. [Ontology management tools](https://www.palantir.com/docs/foundry/ontology-manager/overview) let people configure object types, properties, links, and actions. They cannot decide for a company what counts as an “active customer,” whether a trial order establishes an ongoing relationship, or which department's “completed” means the finance team considers a transaction complete.

Sales, the warehouse, and finance may give different answers. Who gets to decide? When the practice changes, who notices that the old definition no longer applies? Those are the labor intensive parts of building an ontology.

I do not have a study showing that most programmers misunderstand object oriented design, or that most companies cannot build an ontology. Still, the comparison should make us cautious. If the boundary of one object in a software system is often debatable, why assume a one time modeling exercise will correctly define the boundaries of an entire company?

## A mistaken model makes the mistake look official

We ran into this ourselves. During an import of historical records, an Agent put customers, products, quotations, and sales orders into generic objects. The data was present, but the system's existing customer, product, and order records were still empty. The Agent even named its new types `customer` and `product`.

There was no deep philosophical dispute. We had not established whether “product” in the imported material meant the product already supported by the system, yet the import proceeded. We later made the server reject clear naming collisions. When the words differ but the meanings may overlap, the Agent now has to inspect existing types, explain its choice, and get a person to confirm it.

That change did not magically resolve every question of meaning. It acknowledged that code can enforce some boundaries, while others require reading the material and asking someone who knows the business. The ability to create an object in a user interface does not mean that object has acquired the right meaning.

Add links and executable actions to such an object, and the error begins to look increasingly official. “These seem to be the same product” can quietly become “the system says they are the same product.” Once a guess becomes infrastructure, it can be harder for the next person to question it.

## Why did older software need to map everything first?

There was a good reason for this approach.

For software to make a decision by itself, someone had to specify what the fields meant, which values were possible, and which branch to take when a condition held. A processor cannot read a customer email and work out, on the spot, whether the customer wants to cancel an order or only delay delivery. People translated business practices into data structures, states, and rules so programs could execute them.

An ontology is a more ambitious version of that approach. It attempts to organize an organization's objects, links, and actions across systems, rather than just the fields of one application. It has solved real problems and can still be useful when teams need consistent terminology, efficient queries, or coordination across systems.

Today, though, an Agent can read the email, the contract, and the company's written instructions, then examine the relevant records. It can make mistakes and needs evidence and checks. But it no longer has to wait for every business meaning to be translated into a fixed type and a predefined branch before it can begin.

That challenges a large class of software whose main job is to advance work according to rules chosen in advance. When we say AI is displacing that software, we mean the approach that puts a company's working practices into program logic and requires a software change whenever those practices change. Processors still calculate totals, store records, and enforce permissions. AI systems run on computers too. What is becoming obsolete is the assumption that business meaning must first be fully translated into instructions a processor can execute.

If a company is now told to model its entire business as an ontology before Agents may act, it can easily end up in a familiar implementation cycle: interviews, terminology alignment, diagrams, data mappings, model revisions. First adapt the company's way of working to the software; then the software can go live.

That is exactly the part of traditional ERP implementation we want to leave behind.

## Understanding the business should not become another configuration project

That experience made us pay closer attention to a simple division of responsibility: software records; Agents handle business logic.

The system must accurately record who owns an order, its line items, how much was received, and who approved what and when. Code must enforce determinate constraints such as adding up order amounts, checking permissions, and preventing duplicate writes. Records need links and identifiers; an Agent cannot run a business without them.

But if one company says, “For urgent orders, ask the purchasing manager first; otherwise wait for a complete quotation,” that should not require a new collection of objects, action types, or a custom program. Save the instruction and its scope. Let the Agent read the relevant orders, quotations, and current rules, explain what it proposes, and ask the person who wrote the policy if “urgent” is unclear.

This does not mean an Agent naturally understands every company. Ours once put business records in the wrong place. Giving it responsibility for business logic means also giving it ways to find facts, read current rules, record the basis for its decisions, and stop when an instruction is ambiguous.

Building an ontology does not remove that work. Someone still has to decide what each type means, where the data comes from, and when an action is permitted. Hiding those judgments in a model may only delay the moment the team sees a disagreement.

## Is there still room for an ontology?

Of course. A confirmed glossary, stable links, and indexes pointing back to original material can all be useful. Some industries have well defined, durable concepts worth modeling carefully.

What I reject is treating “finish the enterprise ontology” as the entrance requirement for enterprise AI. A company has no complete, permanent picture of itself waiting to be drawn. Asking people to settle every ambiguous practice for the Agent before the Agent can help sets an enormous threshold in the wrong place.

We would rather record what happened accurately, preserve the company's own words, and let the Agent read, check, and ask about the specific decision at hand. Its evidence should be reviewable. When it gets something wrong, we can correct the record, clarify the rule, or improve the tool. A company should not have to wait for a “complete model of itself” before using AI.

Object oriented syntax never guaranteed good design. Ontology objects, links, and actions do not guarantee an understanding of the enterprise either. If an Agent can already read a company's own words, why insist that translating the entire company for a machine must come first? That is a question we keep asking as we build Oryh: let software record what happened, then let the Agent use those facts and the company's own words to decide what to do next.
