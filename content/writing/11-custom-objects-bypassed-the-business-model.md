# We Gave the Agent Custom Objects. It Bypassed the Business Model

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 11*

During one historical-data import, an agent wrote roughly 150,000 records. Customers, products, quotations, sales orders—it looked as though everything had arrived.

Then we checked Oryh's existing customer and product catalogs and its business-document collections. They were still empty.

The data wasn't lost. The agent had created generic object types named customer, product, quote, and sales_order, then kept writing into them. It never stopped to ask the person, and the software never stopped it.

That made us revisit “software records; agents handle business logic.” How much responsibility does keeping a record actually carry?

## Structure doesn't have to dictate business policy

Custom objects were meant for business records without an existing home. A company could define fields for a warranty card or an equipment handover without waiting for us to build a dedicated module. An agent would still read the rules and handle the process around it.

Products, though, already had a home.

An order line's product reference points to a record in the product catalog. A generic object containing the same code, name, and price doesn't automatically become a valid target for that reference. Ask “What products do we have?” in the two collections and you get two different answers.

What we need to preserve is a shared record structure: which document refers to which customer, which item refers to which product, and how quantities and amounts are checked. Whether to offer a discount, whom to consult about an exception, and what to do next remain judgments for the agent, guided by the company's rules.

Moving business logic out of the software doesn't make the relationships between records disposable.

## We had delegated a definite check to the agent too

Our original reasoning was that only an agent, working with the person, could judge whether this company's idea of a “product” meant the product that Oryh already supported. The server shouldn't make that judgment. So even a custom object named product was allowed.

This import showed that we had drawn the boundary too loosely. The software could enforce the names it had already explicitly published.

We changed both object creation and type-definition creation. If the name matches an existing collection, its singular form, or one of a short list of aliases, the server rejects it. The response points to the correct collection and mentions its bulk-import route where one exists.

The tests also preserve the other side of that boundary: product is rejected, while a name such as merchandise is still accepted. The software checks an explicit naming conflict. It doesn't pretend to understand every business term.

That leaves the other half with the agent.

## Being allowed to create something isn't enough

We added a shared requirement to the relevant Skills: before proposing a custom object, read the list of existing types and compare their meaning. An “item master” may still mean products. If the only difference is a few extra columns, consider the existing record's custom fields first.

When a new type really is needed, the agent must explain its name, how many records will go into it, where they come from, and why the existing structure won't do—all before the first write. Then it waits for explicit confirmation. “Import this sheet” isn't permission to build a second customer catalog.

If a similar type already exists but there is a genuine reason to keep something separate, the person must explain that reason. It gets saved in the type definition, so the next agent can read why the object exists instead of guessing. Renaming it product_2 to get past an error isn't a reason. Nor does a person's confirmation override the server's reserved-name check.

These checks protect new writes; they aren't an automatic repair procedure for an earlier import. Repairing this kind of error involves checking the records, migrating them, and rebuilding relationships. Changing a name doesn't complete that work.

We still keep custom objects, and we still ask agents to exercise judgment. But “software records” now means something more concrete to us: the software must preserve record identity, relationships, and deterministic constraints. The agent makes decisions using those facts and leaves its reasons as records too. Otherwise, an import that felt convenient today can become a parallel set of records the next agent has no idea how to use.
