# Can an FDE Bootcamp Teach Industry Experience?

*When Agents Run the Business · A development note*

The “FDE training” now being sold can look complete: a few days on models, a few days on Agents, a customer-style demo, and a certificate. A course can teach tools. I do not believe it can turn people without industry or organizational experience into independent enterprise AI deployment experts in batches.

That does not mean newcomers do not belong in enterprise software. They need to learn, and veterans need to keep learning. My objection is to the business of presenting “can operate this set of tools” as “can own a customer's deployment.”

## Be clear about what a course can teach

Deployment steps can be taught: connect a model, configure permissions, import test data, observe failed calls. Interviewing can be practiced: instead of asking “which feature do you want?”, ask what happened the last time an unusual order appeared. Product boundaries, common failure modes, and launch checklists make good training materials.

This learning can shorten the path to useful work. An engineer who completes it may be much better at helping a senior lead deliver. An industry consultant can learn to discuss the system's real capabilities with developers. I have no contempt for people learning the tools.

A course can also teach people to read an Agent trace: which policy it opened, which document it queried, why it proposed the next step, and which API rejected an action. Teach those methods well. But tests usually come with neat materials, known roles, and a prepared answer. Customer sites are the reverse: a policy may be expired, the actual approver absent from the meeting, and an old document only partly available. Solving a case with complete materials does not show that you can notice when materials are incomplete.

A course cannot give them the memory of a cross-department approval dispute, a stock discrepancy, a customer complaint, or a payment reconciliation they personally owned. Nor can it grant a customer's trust. When they say, “Let's not automate this step yet,” why would the customer listen? A stamp on a certificate is not the answer.

Suppose a customer says, “Once this kind of expense claim is approved, settle it directly instead of converting it into a payable first.” A recent platform trainee may immediately paste the sentence into an Agent's instructions. Someone who has lived through payment and reconciliation will ask more. What about claims already converted? Could one expense travel down two payment paths? Who confirms exactly which category the new rule covers? What happens if it conflicts with the existing approval policy?

Both people can operate the platform. Their ability to manage delivery risk is not the same. The difference is not vocabulary; it is knowing which omission can cause a real loss.

## Experience is not an answer key

A trainer can turn incidents into exercises: when materials are short, check inventory; when an approval is disputed, ask the owner. Useful, perhaps, but the hardest live cases have incomplete problem statements. Inventory says stock exists while another order has reserved it. The “owner” changed jobs and an old group chat still names Wang. Following the exercise mechanically can fail on the very fact the exercise omitted.

Senior experience is not magic either. Veterans must check evidence and can still be wrong. What distinguishes the good ones is knowing what they lack and stopping action at the gap. A course can teach “escalate when uncertain.” It is much harder to teach, in a few weeks, when one's own certainty is misplaced.

Growth can be supported: mentoring, joint delivery, reviewing failures, and gradually increasing responsibility. A newcomer may genuinely become an excellent FDE after years of practice. When I say “FDEs cannot be trained,” I mean they cannot be manufactured by a short course in the way a tool certificate is awarded. A person formed through experience is not the same as one mass-produced by a bootcamp.

I trust a slower path: let a newcomer start with reversible data cleanup and test environments, then handle real exceptions beside a senior colleague, and only later own a lower-risk workflow alone. At each step, assess whether they can explain evidence, authority, consequences, and correction—not how many classes they attended. This can be called training. It is not a product that says “pay, graduate, and deploy independently.”

## Beware of selling expert status

A customer can buy training to improve skills; a vendor can develop staff through practice and assessment. But if a course promises “graduate as an FDE” or “deliver independently with no industry background,” ask who owns the cost of the graduate's first mistake. Who resolves a wrongly issued payment instruction? Who answers for a missing permission boundary?

Serious development should have graduated authority. A junior can research, build an interface, and draft candidate rules. A critical workflow needs review by people who understand both the business and the product. Ask the trainee to explain a difficult document down to the source sentence, applicable date, and authorized owner. If they cannot, they should not independently press Publish. That is less marketable than a bootcamp promise and more like professional formation.

Training pitches also blur “participated in delivery” with “owned delivery.” A trainee who works beside a veteran on a successful project may learn a great deal. The project result does not prove they could make the same judgments alone for the next customer. A review should say who spotted the key risk, who discussed authority with the customer, and who chose to pause automation. Crediting a whole team's experience to one graduate serves neither the customer nor the graduate.

If a training provider wants to be accountable, let it name the role it actually produces: tool operator, implementation collaborator, or independent owner of a particular business workflow. The first two are useful jobs with real demand. The third needs industry experience and a record of responsibility, not a marketing promise. Selling the first two as the third is what makes “FDE training” so hard for me to respect.

I do not object to companies turning field lessons into training. Demanding work needs good teaching. Teaching materials, however, carry only what their authors can articulate. The real test comes when the manual has no page for the case in front of you: can the person identify risk, verify facts, involve someone with authority, and own the review if the decision goes wrong?

We saw this distinction while building Oryh. An administrator asked an Agent to “add a condition”; the Agent replaced the active workflow with a short text containing only that condition. We later required reading the full rule, displaying additions, changes, and deletions, and asking before an unexpected deletion. Training can teach those steps. A delivery lead must also recognize the risk between the customer's word “add” and an interface that replaces a whole document, then test it before launch. Calling that judgment an “FDE fast-track skill” makes the course sound much bolder than the evidence.
