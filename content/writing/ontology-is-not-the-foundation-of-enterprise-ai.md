# Ontology Isn't the Foundation of Enterprise AI

*When Agents Start Operating the Business: Design Explorations from ORYH — A Development Note*

A claim we hear often: before a company can make real use of AI, it needs an ontology. Customers, orders, contracts, equipment, together with their properties, relationships, and the actions that can be taken on them, get modeled into one semantic layer, and AI works on top of that layer. Without an ontology, the argument goes, enterprise AI has nothing to stand on.

We disagree. Ontologies solved real problems in the past. But the problem they were built to solve has largely gone away. Keeping the ontology as the foundation is like handing a reader who understands the original a translation instead.

## First question: who was it designed for?

When people talk about ontology in enterprise AI today, they mostly mean the idea Palantir popularized. Palantir began integrating data for intelligence agencies, governments, and large enterprises in the 2000s. Its Foundry platform later formalized that practice as the Ontology, and with AIP, Palantir positioned it as the base layer for enterprise AI. The lineage goes back further: in computing, "ontology" dates at least to knowledge engineering in the early 1990s and to the Semantic Web after it.

In other words, the approach took shape over the two or three decades before large language models arrived.

Older doesn't mean wrong. But the software methods that predate AI almost all share one assumption: computers can't read what people write. Normalized database schemas, ERP fields and state machines, the conditional expressions inside workflow engines, and ontologies are all built on it. When the assumption changes, everything built on it deserves a second look. It shouldn't be carried into a new era unchanged and relabeled "AI infrastructure."

It's the same reasoning behind our view that ERP for the AI era needs a rewrite, not an agent add-on.

## An ontology translates exactly what AI can now read

Take an ontology apart and what it does is translation.

A contract says, "The remaining 10% is payable upon acceptance." A CPU can't read that sentence. So a modeler defines a Payment Term object with a percentage and a trigger event, and links "acceptance" to a delivery object. A customer emails, "Hold this batch until we clear space in our warehouse." A program can't read that either, so someone designs a "shipment on hold" status. Three systems each name the same customer differently, and a program can't tell they're one company, so a unified customer object is needed to reconcile them.

That work was genuinely valuable. Deterministic programs can only handle deterministic structures. Human language had to be translated into something a machine could process before software could query, aggregate, or execute on it. The ontology was that translation dictionary, carrying more meaning than a set of isolated tables.

Large language models change precisely this. They can read the contract clause directly. They can pick up what an email implies without saying. They can see that two differently worded company names probably refer to the same supplier, and raise a question when they aren't sure. Content that once had to be translated by people before a machine could use it can now be read by AI as is.

Preparing a translation in advance for a reader who understands the original should itself be questioned.

## Translation always loses something

Worse, translation isn't free.

Every conversion from source material to a structured model is a selective compression. The modeler decides which properties to keep, which details to ignore, and which handful of enumerated values will stand in for reality. Those decisions can only be made at modeling time, based on the questions someone could anticipate then.

When we built contract records, one of our test cases used this payment clause: 30% within three business days of signing, 60% before the first shipment goes out, and the remaining 10% upon acceptance. Condensed to "30% upfront, 60% before shipment, 10% after acceptance," it reads smoothly and looks well structured. But how many days does the buyer have for the first payment? Is 60% due before every shipment, or only the first? Those two conditions decide what should happen next, and they're exactly what the compression dropped.

An ontology behaves the same way. If the Payment Term object has no properties for a deadline or for which shipments a condition applies to, that information never gets in. It isn't recorded wrongly; there's simply nowhere to put it. However precisely AI later queries the ontology, it only gets back what the modeler chose to keep.

And the hard problems inside a company tend to live exactly where no one thought to model: exceptions, side conditions, a concession made verbally during negotiation, displeasure in a customer's tone. The more a piece of information matters to a judgment, the harder it is to design as a property or a link in advance. If AI can read more from the original, why make it read a copy that holds less?

## So does Oryh have no structure?

It does, and quite a lot of it. That needs to be said clearly, or this piece could be read as "put data anywhere and let AI sort it out."

Oryh's division of responsibility is: software records; agents handle business logic. Order lines must add up to the order total. A payment can't be applied beyond what's owed. Without permission, a write is refused. A retried request can't be recorded twice. Who did what, and when, must be traceable. Code enforces all of that. These structures exist not because machines can't read human language, but because money has to reconcile and responsibility has to be clear. Even an AI that could read everything wouldn't make those requirements go away.

What we don't do is translate the company's meaning into a model ahead of time. The original contract is kept as an attachment. When an agent excerpts a clause, it preserves the wording verbatim and records which file, page, and clause it came from; its own interpretation goes into a separate summary, stored alongside. A company's approval rules are kept as versioned natural-language text that the agent reads before it moves work forward, rather than being translated into conditional expressions. "Days of leave left" isn't a stored field either. It's an answer the agent works out when asked, by reading the policy that applies at that point and the relevant leave requests.

The distinction is between an index and a stand-in. Clause excerpts, page references, and product-name mappings a person has confirmed are indexes that help an agent find its evidence faster, and it can always return to the original to check. An ontology, by design, aims to be the layer through which AI understands the business: AI learns the company through objects, properties, and links, while the source material recedes behind a data pipeline. A table of contents is welcome. A stand-in isn't needed.

## The hard problems haven't disappeared. They've moved.

Reading originals directly doesn't solve everything.

AI misreads, so originals stay and locations get recorded, and a person can always ask, "Why did you decide that?" There's too much material to read end to end, so retrieval and excerpts are needed, but they point to the original rather than replace it. When a rule is vague, AI shouldn't fill the gap itself; it should stop and ask whoever owns the rule. Reading source material every time also has a cost, and we're still working out that trade-off.

But these problems now sit in the right place: how to make AI read accurately, find what it needs, and remain checkable. They don't call for yet another translation layer between AI and the business, maintained for years by modeling consultants. An ontology doesn't just describe data; it models actions and business rules too. When the company changes how it works, someone has to open another modeling project. That's the old problem of rebuilding the ERP every time management practice changes, under a new name.

Ontology was once a bridge, with human language on one side and machines that couldn't read it on the other. Machines can read it now. The foundation of enterprise AI should be faithfully preserved facts, clearly written rules, and an agent that can read both directly and is willing to show its evidence.
