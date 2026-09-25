# If AI Can Draw the Company's Map, Why Make It Follow the Map?

*When Agents Run the Business · A development note*

One proposal for enterprise AI sounds sensible enough: build an ontology first. Define customers, contracts, orders, employees, projects, and the relationships among them. Then the AI will know what it is working with.

There is a map hidden in that proposal. An ordinary map marks roads and buildings. An enterprise ontology is expected to mark who owns a customer, which approval path an expense follows, and when a sentence in a contract applies. If it is meant to guide daily operations, it has to be a high-definition map.

Who draws it? And who updates it every day?

## A company's roads do not stay put

Drawing this map is much harder than listing a few types of objects. First you have to decide their boundaries. Is the thing being purchased one piece of equipment, or does every component need an identity? Is the customer the company that signs, the company that pays, or the team that actually uses the product? If one person manages a project and temporarily stands in for an approver, how many relationships should the model contain?

Then come the intersections. Who confirms a purchase within budget? Who approves one over budget? May an urgent project place an order before approval? Who reviews a purchase entered at the end of the month? The written policy may have local additions. Different teams and different dates may be governed by different versions.

That does not mean the company has no rules. It means its rules live across contracts, policies, messages, meeting notes, and everyday collaboration. Turning all of this into executable objects, relationships, and actions calls for business knowledge and a prediction about which details will matter later. Even a correct map today needs revision when the organization changes or a product is sold differently.

Many companies struggle to keep customer names consistent across their existing systems. Maintaining a map of every operational distinction is a much taller order. The easy deliverable is a tidy snapshot. The hard one is a map that stays accurate after the business moves.

## So let AI draw it

That is a fair reply, and it leads to the interesting part. Let AI read policies, contracts, documents, and historical records. Let it identify objects, infer relationships, spot contradictions, and propose rules. When the company changes its practices, it can find the affected parts of the map and draft a revision for a person to confirm.

I think this is technically plausible. It may be much faster than asking a team to start from a blank modeling sheet. But consider what the AI must do to draw the map correctly. It must read the source material directly. It must understand that “the project manager looks at this first” does not mean “the project manager has final approval.” It must decide whether yesterday's contract or today's new policy applies. It must recognize whether an apparent conflict is a version change or an exception for a particular project.

In other words, the understanding needed to draw the map is exactly the understanding we want the AI to use when handling the work.

If the AI can read the material, compare versions, recognize exceptions, and explain its reasons, why compress that understanding into a map first and then ask the AI to read the map back as business truth?

It is like asking someone who knows the neighborhood to draw today's road closures and temporary detours, then telling them to forget what residents just said and drive only by the drawing. The extra loop does not necessarily make the journey safer. It creates another chance to omit or mistranslate something.

## Correct on the map may mean correct yesterday

Take a hypothetical company. Its policy says a department head confirms the purpose of a purchase, while finance approves purchases above 50,000. Later someone adds: “A renewal that remains within an approved annual budget does not need to repeat the checks for a first-time purchase, but payment still follows the contract milestones.”

A careful reader will ask what counts as a renewal, which budget version applies, whether skipping the first-time checks also skips finance approval, and whether the payment schedule changes. If the answer is missing, they should ask.

Whoever updates the map has to ask the same questions. After that, they may also need to create a renewal type, change approval relationships, migrate old contracts, inspect processes that depend on the old rule, and make sure every map user sees the right version. Having AI draw the map does not remove the need to understand and ask. It turns a business judgment into modeling, migration, and subsequent use of the model.

The more complete the map looks, the easier it is to forget its edges. An Agent that finds a “finance approves” relationship may assume it has the whole answer. It will not automatically know that a new qualification is sitting in meeting notes and has not yet been mapped.

Direct reading can fail too. An Agent may miss “within the approved budget” or mistake “skip repeated checks” for “skip approval.” Reading the source is no free pass. The difference is that the source and the facts remain the basis for the judgment. The Agent can cite the relevant sentence, policy version, budget, and contract, and ask when it is unsure. When the map is treated as truth, the original material tends to disappear behind it.

## We need signposts, not a replica of the company

Rejecting an ontology as a mandatory middle layer is not a rejection of structure. Companies still need customer IDs, order amounts, contract versions, and payment records. Software should enforce exact totals, permissions, and protection against duplicate actions. Without dependable records, AI has nothing solid to reason from.

Search indexes, catalogs of existing objects, confirmed identity mappings, and even local relationship graphs can help an Agent find relevant material. They are signposts: they point to where the evidence lives and whom it may concern. A bad signpost can be corrected, and the original record is still available when there is no signpost at all. The problem begins when the signposts are promoted into the only business truth.

We have had a reminder on the other side of this divide during development. An administrator asked an Agent to “add one condition” to a workflow. The Agent replaced the full workflow description with a short text containing only the new condition. It could read the instruction and still lose the instruction it was supposed to preserve. We tightened the revision process: read the current text first, show each addition, change, and deletion, and stop for confirmation if something the user did not ask to remove would disappear. Keeping versions and visible differences matters more than assuming a map drawn by AI must be right.

If a fixed interface for conventional software is needed, or a particular stable relationship is worth maintaining, build a local map. Make it a view for a defined purpose, with sources that can be checked and a path to redraw it. Do not make a complete enterprise ontology the prerequisite for every decision. The next business step should still come from current facts, applicable rules, and an Agent that can explain its judgment.

In Oryh, we keep coming back to a simple division: software records facts and enforces hard boundaries such as amounts and permissions; Agents read the material, interpret the rules, advance the work, and stop when the evidence is insufficient. AI can help draw a map of the company. If it can already find its way through the source documents and the facts, we need not build an expensive map factory and require it to follow only what the factory produces.
