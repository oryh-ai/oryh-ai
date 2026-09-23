# Why Can't Customization Start With a Sentence?

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 18*

Suppose an administrator says, “From now on, settle approved expenses directly against the claim. Don't create a separate payable invoice first.”

We want that sentence to be the entry point for customization. The person describes their practice; the agent understands, confirms, and saves it, then follows it. No requirements document waiting to be translated into another version of the application.

The reason isn't that AI writes code faster. The responsibilities have changed: agents handle business logic; software keeps records. When the company's way of working isn't entirely embedded in the backend, changing that practice needn't mean changing the application.

Building Oryh, though, we've found plenty of work between “supports natural language” and making that sentence actually matter.

## Saving a sentence doesn't tell an agent how to use it

We already supported both reimbursement routes: settling the claim directly, or creating a payable invoice first. Code still prevents the same expense from being settled through both routes.

But the instructions weren't connected properly. The agent changing company rules wasn't explicitly told where this request belonged. The agent handling payments was told to read the rules, but lacked a clear lookup order. One pointer even directed it to the wrong document family's workflow definition.

Where a perfectly reasonable sentence landed still depended on the agent guessing.

We made both ends explicit in the Skills. This preference about an existing capability belongs in the company's supplemental instructions on the payables Skill. The payment agent reads that section in its own instructions first, then the expense claim's workflow definition. If they disagree, it points out the conflict and asks rather than choosing silently.

Software stores the sentence; the agent interprets it. We didn't add a company-specific backend branch for “this company settles claims directly.”

## Don't copy the whole system to change one sentence

There's another tempting detour: copy the original Skill and edit a customer-specific version.

That appears to deliver customization, but a single changed preference separates the entire set of operating instructions from the product version. Later fixes to the standard Skill may not reach the customer's copy. The familiar maintenance burden of custom versions returns in another form.

We therefore store company-specific instructions separately, without editing the standard Skill's files. They're appended when the agent's instruction bundle is generated. The product capability can keep receiving updates while the company's practice remains intact.

Our test first saves direct settlement, then switches to invoice-first settlement. It checks that the new sentence appears in the rendered instructions, the old one is absent, and the version increases. It also checks that the Skill hasn't become a separate custom fork.

The version change lets installed copies discover the update on a subsequent sync. It doesn't instantly replace every running agent's memory. This test verifies that the rule is stored and delivered correctly; business scenarios still need to check its execution.

## Users shouldn't have to learn where we store rules

To a user, “add another approval above this amount” and “settle expenses directly” are both descriptions of how they work.

The first belongs in a workflow definition; the second can be supplemental instructions for an existing Skill. Distinguishing them, finding the current records, and explaining the proposed change are the agent's job. A user shouldn't have to learn field names and endpoints before customizing a process.

If something is ambiguous, ask: which department, effective when, and what happens to requests already in progress? That remains a conversation about the business. It shouldn't routinely become a development project.

The advantage is concrete. For rule changes within existing capabilities, companies can change their practices in their own words, without maintaining another application variant for every difference or accommodating a management process prescribed by the software.

A sentence cannot conjure an external integration that doesn't exist, of course. Nor can it override permissions, amount calculations, or duplicate-settlement guards. New tools and record structures still require engineering.

We want that engineering to build the product's capabilities while leaving companies in control of how they use them. People state the rules. Software keeps the rules and facts. Agents interpret them and advance the work. Natural language isn't merely a draft specification here. It's part of the customization itself.
