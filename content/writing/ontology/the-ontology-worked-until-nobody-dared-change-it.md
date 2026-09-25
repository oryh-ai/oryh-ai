# The Ontology Worked. Then Nobody Dared Change It.

*When Agents Run the Business · A development note*

Imagine the first phase of an ontology project. The team models car sales neatly: cars, customers, orders, deliveries, and stores all have their objects and links. In a demo, you open a car and follow its sales history to the responsible person. Someone says, “At last, the business is clearly described.”

In phase two, after-sales service needs to track individual tires. In phase three, warranty must distinguish customer-supplied parts. Later, finance points out that “sale completed” and “revenue recognized” are not the same date. Every request is reasonable. Every request is worth addressing. The once-clean diagram is simply becoming harder to change.

This is a possible trajectory, not a report about a real customer. The question is why an ontology may eventually be set aside. It need not fail because nobody knows how to build one. It may be built successfully, then become too costly to maintain.

## An easy start, a meeting for every later change

“Make tires separate objects” sounds small to the service team. The data team asks how to migrate old repairs. Developers ask who will change the interface that queries car-level warranty. Customer service asks whether earlier promises of coverage still stand. Finance asks whether historical reports should be recalculated. The business owner, busy with today's claims, may not have time to coordinate all of this on behalf of a model.

Nobody is deliberately slowing things down. Their risks differ. Data people do not want to manufacture false history. Developers fear a screen that continues working while silently giving the wrong answer. Customer service fears contradicting an earlier answer to a customer. Management wants to know why a metric moved after the model changed. Bringing everyone together costs more than “add an object.”

If a company often changes products, contracts, channels, and approval practices, the meetings multiply. The first change gets a careful review. The second gets a shorter one. By the third, someone says, “Let's put this in a note for now; the main process can stay as it is.” That is not necessarily laziness. It may be a practical response to the cost everyone has seen.

As the notes grow, the model knows a little less of the live business. The old objects and relationships are still there, looking official. If an Agent reads only the ontology, it misses the new practice in the notes. If it always has to read notes, email, and source documents too, the case for treating the ontology as the company's sole understanding layer grows weaker.

## One workaround makes the next one easier

The first workaround is temporary: there is no time to remodel a warranty exception, so customer service writes it in a claim note. The next adviser follows that note. Later the team creates a shared table called “cases not covered by the model.” It may be maintained carefully, but it is outside the graph.

Now there are two realities. The graph holds the business as formally defined. The table holds some of the business that happened most recently. A project report can still say the ontology covers cars, tires, orders, and warranties. The people doing the work know they must check the table before deciding whether a claim will be paid. The more they use the workaround, the less complete the ontology becomes. The less complete it becomes, the less comfortable anyone is changing it and claiming the result is authoritative.

This is an ordinary organizational loop, not a mysterious technical collapse. The software and data still exist. The situations requiring the most judgment have drifted outside the model. Eventually a person who queries the graph and believes it is complete may make a worse decision than someone who knows about the extra table.

I would watch a few signals closely. How many new requirements end up in notes? How long does a model change take from request to actual use? How many teams must sign off? How many old fields can no one explain? When an Agent makes a decision, does it trust the graph, or does it always have to ask a person afterward? These say more about whether the system is alive than the number of objects and edges.

## “Who maintains it?” cannot be waved away

In theory, you can assign model ownership to one team. In practice, the work crosses boundaries. The modelers know structure but may not know that the meaning of “delivery” in a contract changed this month. Frontline staff know the customer but may not know that one altered link affects ten reports. Developers know the interface dependencies but cannot decide on finance's behalf whether old revenue should be recalculated.

AI assistance does not dissolve responsibility. It can read a new policy, identify likely changes, list affected objects and processes, and draft a migration. Someone still has to confirm the intended meaning, decide whether old orders are in scope, and accept the migration result. Skip those confirmations and you save review time while producing a map nobody feels safe trusting.

Not every ontology follows this path. A narrow catalog of stable objects or a sourced set of customer–contract relationships may be maintained very well. Trouble comes when the model is raised to a complete mirror of how the company runs and every decision is routed through it. The larger the mirror, the more dispersed its maintenance responsibility. The more dispersed that responsibility, the easier it is for each person to say, “Let's not touch it yet.”

To decide whether a graph is still worth maintaining, try a plain audit. Of the new business practices from the past three months, how many made it into the graph? Who keeps track of the ones that did not? When someone reports a wrong link, how long does correction take? If the team can answer, the model is probably being tended. If not, but Agents are still told to “treat the ontology as truth,” we are asking them to trust a map that nobody owns updating.

## Keep “we do not know” in plain view

We could start elsewhere. Software records transactions, approvals, repairs, and payments accurately. It keeps the original documents, dates, versions, and evidence. Code enforces hard constraints such as exact totals, permissions, and no duplicate shipment. The Agent reads the records and policies relevant to the present question and proposes the next step. If the policy is unclear or historical evidence is missing, it says so.

This still uses structures, indexes, and links. They can be local and revisable, pointing back to facts rather than pretending to be a master diagram that must stay ahead of the business forever. If one workflow needs to track individual tires, track them seriously there. Other teams do not have to model every bolt just to satisfy a company-wide idea of a “consistent grain.”

This approach does not abolish maintenance either. Agent instructions need care, search can retrieve the wrong document, and old facts may need a person's confirmation. The difference is that a company changing one practice need not first decide whether it can safely redraw an entire map. Record the new fact honestly, explain and review the new judgment, then decide which structure is worth making durable.

In Oryh, we have seen the cost of a parallel recording path. An Agent imported customers, products, and business documents as generic objects while the dedicated customer and product catalogs remained empty. We later blocked clear naming collisions and asked the Agent to inspect near matches and seek confirmation. That experience leaves me unmoved by “we just need a complete business graph.” A graph can help find a route. Record identity and facts must stay sound, while new business instructions must be readable by the Agent and confirmable by people. Otherwise the graph remains, but it is no longer the road anyone actually travels.
