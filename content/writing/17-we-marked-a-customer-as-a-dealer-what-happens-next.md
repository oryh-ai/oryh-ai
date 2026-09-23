# We Marked a Customer as a Dealer. What Happens Next?

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 17*

While building customer records, we ran into a problem: one customer book could contain both retail members and hospital groups, but our records couldn't express that distinction.

A separate membership module was an obvious option. Yet both groups needed quotations, orders, invoices, and payments. Splitting the transaction records because their customer profiles differed seemed to take us too far.

We kept one customer record structure and separated describing a customer from deciding how to treat them. Software handles the records; agents handle the business logic. That boundary matters more than adding a few category options.

## Don't confuse identity with segmentation

We introduced two fields. One records whether the customer is a person or an organization. The other records the company's own segmentation: retail, dealer, group buyer, and so on.

An organization isn't necessarily a dealer. Nor does being a dealer imply a fixed set of commercial terms. These are different questions, not one dropdown—and neither should quietly become a permission or discount switch.

Unknown information stays unknown. If an imported list doesn't state the customer's kind, filling every row with “company” doesn't improve the data. It creates false facts that later reports will repeat.

We added a test for that: an omitted kind stays empty when read back, and updating only the phone number doesn't silently fill it with a default. The agent's job is to find evidence and ask, not turn uncertainty into an invented fact.

## One category label rejected the whole import

Extensible categories sound straightforward. Testing exposed a gap between people's language and the interface.

A spreadsheet used the Chinese label “团购,” meaning group buying. Passing that text directly into the category field rejected the entire request. No rows were written. The interface expected the category's internal name, not its human-readable Chinese title.

That differs from sending a valid internal name that the company hasn't defined yet. In a bulk import configured to skip failing rows, the latter can identify the individual row's problem. The former doesn't pass request validation at all.

We put the distinction into the Skill. The agent first reads existing categories and maps the spreadsheet's wording to their internal names. If nothing matches, it explains the gap, asks whether to add “group buyer,” and has an authorized person define it. It must not silently substitute “wholesale” just to make the import succeed.

Code still validates names and whether categories exist. Understanding what this company means by group buying isn't a question the backend should quietly answer for it.

## A dealer label doesn't grant a price

This is where it's easy to slip back: now that there's a category, why not add “dealers get twenty percent off” to the program?

Who decided that discount? Does a new dealer get the same terms as a long-standing customer? What if a product already has a separately agreed price? Put those answers into backend branches and a change in business practice becomes a software change again.

Oryh doesn't make customer categories directly trigger pricing or payment-term decisions. Negotiated customer-product prices have their own records. The quotation Skill instructs the agent to look up those agreements, not apply a price simply because the customer is labelled a dealer.

One test records a price of 88 for one customer and 79.5 for another, for the same product. Software preserves their respective agreements. It doesn't infer which category deserves a lower price. The agent uses the agreements, company rules, and current request to advance the quotation. Conflicts or exceptions requiring a decision go to an authorized person.

An unclear rule isn't permission for the agent to invent “dealers usually get credit,” either. Handling business logic includes recognizing when it cannot yet reach a conclusion.

What we addressed wasn't just two missing profile fields. Categories need to express how a company understands its customers without making commercial decisions on its behalf. Software keeps customers, classifications, and confirmed agreements, enforcing references, permissions, and amount calculations. Agents read those records, apply company rules, and advance the work. A label is an input to judgment, not the judgment itself.
