# Less Customer-Specific Code, More Judgment on Site

*When Agents Run the Business · A development note*

If enterprise software stops encoding every customer's approvals, missing paperwork, and exceptions as customer-specific code, does the engineer on site have an easier job? I suspect the opposite. With fewer branches to write, “the request has been developed” can no longer stand in for understanding the business.

Imagine a customer saying, “Urgent orders can go ahead; we'll supply the paperwork at month-end.” In a traditional project, that can become a checkbox: mark the order urgent and bypass a validation step. In an AI project, the same sentence may be given to an Agent. If neither approach asks how far “go ahead” extends, both can move a sensitive case too far.

## The real work starts with a question

Who gets to mark an order urgent? Is a sales representative's worried customer enough? Does a production line waiting for a component count? May the company reserve stock, create a purchase order, ship goods, or even pay before the documents arrive? Does “paperwork at month-end” mean a quotation, an approval, or a signed contract? If it is still missing at month-end, who stops the next action?

These are not model settings. They are the customer's way of governing work. A person capable of delivering the system has to put the departments' different meanings of “urgent” side by side, identify conflicts, establish formal authority, and agree on what may happen early and what must not. Uploading the interview transcript to an Agent is not implementation.

If the customer cannot yet answer, the person on site should be able to say, “Let's not automate that step.” Start with lower-risk actions: record the reason, remind the owner to supply evidence, create a task. For shipping, payment, or promising a delivery date, require a named confirmation first. Drawing that line is more valuable than writing an impressive prompt.

## Software records; an Agent judges the next step

The AI era calls for a different division in ERP. Software keeps reliable records: whose order this is, its lines and amount, how many units have actually shipped, and who approved what and when. Exact line totals, protection against double payment, and permission boundaries belong in code.

The Agent reads the customer's rules alongside the order, approval history, stock, and current staffing, then judges what to do now. Those rules can remain in natural language rather than being compiled into a customer-specific branch each time. If the customer later says, “Equipment emergencies may reserve stock early, but payment still waits for finance,” the Agent can read that sentence on the next decision. Software still stores the rule version and the action record.

This architecture is not complete just because someone says “AI understands.” Where does the rule live? How does the Agent find the right version? Can a paginated query omit a relevant older approval? What happens when two instructions conflict? Will the server reject an unauthorized action? The person on site should test standard cases, missing-document cases, freshly changed rules, and work already halfway through a process.

This is where the distinction between an FDE and an on-site colleague who can configure an Agent becomes clear. The latter may paste a sentence into a system. The former should know whether that sentence is sufficient authority for a system to touch money, stock, or a customer promise. They do not decide for the customer; they identify the decision the customer has not yet made.

Rules change, which makes the job harder. In week one the customer says “urgent orders may reserve stock.” In week two it discovers that some orders were marked urgent merely to meet a sales target, so it adds “only production stoppages or contract deadlines qualify.” The person on site cannot just edit a prompt. They have to review stock reserved under the old instruction, orders not yet shipped, and downstream tasks: which remain, which need review, and who may cancel them? The Agent can judge future work under the new rule; past actions must remain on the record.

## Less code does not mean less engineering

Moving orders from an old ERP still requires data engineering: matching customers, preserving approvals, and identifying duplicates. Connecting a warehouse device or bank still requires interfaces, authentication, and retries. If a product collapses stock reservation and physical shipment into one quantity, a clever Agent cannot restore the missing distinction. The record layer has to be fixed.

Likewise, after an Agent decides that an urgent order may reserve stock, the server must check availability and write the reservation transactionally. Two concurrent requests must not both take the same stock. Great business judgment does not replace database constraints or failure recovery.

When I say AI can reduce customer-specific code, that is a demand on product architecture, not a license for vendors to skip engineering. Writing a rule in natural language does not conjure missing permissions, audit trails, or record types beneath it.

## An expert on site does not personally do everything

A senior person on site is often someone who can separate problems. “We lack a record type” goes to product. “We need a connection” goes to engineering. “The company has not said who approves” goes to a business owner. “The Agent is unsure” calls for evidence and human confirmation. In a meeting all four may sound like “the system doesn't work yet.” The remedies are different.

They also need to leave decisions with the right people. If the customer wants a risky but authorized practice, the engineer cannot quietly replace it with a supposed best practice. If someone asks to bypass a hard permission boundary, “the customer said so” is not enough. A real super-individual does not replace every role. They can tell precisely whose decision each part is.

The test is practical. Before launch, ask them to choose a few difficult historical orders and explain which facts the Agent will read, which rule version it will cite, what action it will take, and where it will stop. After launch, compare actual runs with those predictions. People who can deliver this way are rarer than people who can demo “AI processed a hundred orders.”

A deployment report should not give only a “success rate.” Separate Agent-proposed actions into those executed automatically, those awaiting human confirmation, and those stopped for missing evidence. Check each class for mistaken progression and needless delay. A stop is not always failure. Knowing what it does not know before shipping or paying is a useful boundary. The field lead must explain that boundary instead of removing every stop to make a demo metric look good.

In Oryh, we insist that software handles records and Agents handle business logic. One inventory test showed why: treating stock reservation and shipment as the same deduction made available stock fall twice even though the goods moved once. Code had to fix that quantity relationship. Whether a company releases a reservation after an order is canceled, however, depends on its actual rules, which an Agent reads. A person on site who cannot separate these problems is not a genuine FDE even if they write no customer-specific code at all.
