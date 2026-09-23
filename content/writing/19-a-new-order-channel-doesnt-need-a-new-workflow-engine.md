# A New Order Channel: Change the Rules or Change the Software?

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 19*

Last time, we discussed customization starting with a user's own words. Here's a problem we actually encountered: what happens when those words meet an older rule?

In an e-commerce order scenario test, the administrator's request was direct: platform orders don't require a contract number; use the platform order number, require a shipping address, reserve stock after confirmation, and ship without a picking step.

These sentences describe how the company works. They aren't just a feature list waiting for a programmer. We want the agent to interpret them and use existing order, reservation, and shipping capabilities. Software keeps the rules and the facts produced along the way.

## The new rule arrived; the old rule stayed

The administrator also asked to retain the existing rules and append the e-commerce section. The resulting workflow definition contained both “source quotation number required” and “use the platform order number.”

The original business began with an accepted quotation, so requiring that reference made sense. A platform order, however, could come directly from a consumer's purchase without a quotation first.

In this run, the agent interpreted the channel-specific clause as allowing the platform number to replace the quotation number, and proceeded. That didn't prove the issue was resolved. Would another agent follow the general requirement and return the same order?

Adding a backend branch exempting e-commerce orders would address the immediate case. But another company's exception would invite another branch. Natural language would merely collect requirements; the program would still decide how business works.

The division we want is the opposite: agents handle business logic; software keeps records. Interpreting company policy shouldn't quietly move back into the backend.

## We needed clearer instructions for reading rules

We updated the order-progression Skill: where the definition explicitly covers this kind of order, apply that specific clause and state which sentence supported the decision. “Confirmed” alone hides the judgment that got us there.

If the definition doesn't authorize replacing the quotation reference with a platform number, don't invent that equivalence. Return the order, identify the missing channel-order rule, and have someone authorized clarify it.

This isn't “whatever was written last wins.” Nor does seeing “e-commerce” permit skipping checks. The agent must establish the order's context and whether the rule actually covers it. If the conflict remains unresolved, explain it to a person.

The user doesn't need to learn a workflow engine to clarify the scope. They can say, for example, “Orders placed directly on a platform don't need a source quotation; orders won through offline quotations still need that link.” That's a clarification to propose and confirm, not one the agent should silently invent.

Software stores a new version while retaining the old one. The agent reads the applicable rules and order facts, then decides the next step. What changes first is the company's own description of its practice, not a separate order-processing application.

## Some changes still belong in software

This round wasn't only about wording. Testing also found that the same platform order number could be attached to another order, potentially recording a repeated import as two transactions.

We addressed that in code. An external number for the same source and document kind already linked to another order is rejected, with the existing order identified. An intentional split must be explicitly declared in the call. The agent decides whether splitting is appropriate; software records the explicit action and checks the links.

“Does a platform order need a quotation number?” and “Where is this platform number already linked?” are different questions. One concerns company practice. The other concerns a verifiable relationship between records.

That's the value of natural-language customization: another way of working needn't automatically require another application variant. People state their rules; agents interpret, clarify, and execute them. Software keeps the facts and enforces definite constraints.

Updating a Skill doesn't guarantee every agent will interpret every case correctly. We've made the handling principle explicit; different orders and phrasings still need testing. The aim isn't to make natural language sound magical. It's to let companies change their practices in their own words—and see why the agent acted as it did.
