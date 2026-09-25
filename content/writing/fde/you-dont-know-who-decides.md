# If You Do Not Know Who Decides, What Exactly Are You Deploying?

*When Agents Run the Business · A development note*

A company hands over its project organization chart. The project manager owns delivery, the purchasing manager manages suppliers, and the finance lead approves budgets. The engineer on site loads people and roles into the system. Everything looks orderly.

The first real purchase gets stuck. The project manager says the equipment is urgent. Purchasing says the familiar supplier costs more but has a reliable delivery record. The budget owner worries that this expense will consume next month's plan. Finance asks who actually confirmed that “urgent” allows work to move early. Every line on the organization chart may be right. The chart still does not answer today's decision.

This is a thought experiment, but on-site problems often feel like this. An FDE who can import job titles but cannot tell who provides facts, who influences a decision, and who can formally approve it may merely automate the confusion.

## Influence is not approval authority

The person who knows an old supplier can have a decisive opinion about price, delivery, quality, and past failures. That knowledge deserves attention. They may not have authority to sign the purchase. Conversely, the finance lead may have formal authority but not know what a day of machine downtime will cost.

Put both into a generic “approver” role and the system will either bypass authority or lose important evidence. An Agent should ask the supplier expert for facts and bring a reasoned recommendation to the person who can decide. Software must stop someone without authority from approving. Understanding the customer's organization is not permission to evade formal process. It is knowing which informal knowledge matters and which formal boundaries remain hard.

The chart usually says “who is responsible.” It rarely says “whose concern should stop us.” In one company, a workshop supervisor knows what a machine outage means. In another, the person who has managed a customer relationship for years knows the consequences of one promise. They may have no approval button and still need to be consulted before an action. A simple role import misses this layer.

## How much can two weeks on site reveal?

At demos and kickoff meetings, a customer gives the official account. How work really moves becomes visible in exceptions: whom people call when the owner travels, who convenes conflicting departments, whether emergencies are reported before or after action, who explains a mistake to the customer. It is hard to learn this from interviews alone before seeing a few actual cases.

“After two weeks on site, our FDE understands your company” sounds confident and risky. They may remember the loudest person in the meeting while missing a budget owner who was absent but can halt a purchase. They may read “looks good” from a purchasing manager in a group chat as formal approval. Put that mistake into the Agent's instructions and every later purchase may go down the wrong path.

A capable on-site person does not claim to have decoded the customer once and for all. They build a checkable account of responsibility: who authorizes each class of action, who supplies facts, who must be informed, and where conflicting views are escalated. It is not a political map drawn once. Each exception provides a real record against which to test it.

This work may require uncomfortable conversations. A senior colleague with substantial influence but no formal approval authority should be asked for input, while the approval goes to an authorized person. Someone with signature authority may say “let the team below me decide”; that habit alone does not transfer their authority. Holding this boundary is part of enterprise delivery.

Organizations change as well. A project manager leaves, finance appoints a temporary deputy, or purchasing splits into two teams while old chat habits persist. A deployment cannot write “Wang always owns this” as a timeless relationship. Roles, delegation periods, and policy versions need sources and effective dates. When an Agent sees an old name, it should check the current appointment instead of inferring authority from the volume of old messages.

## An Agent can find a plausible person and still find the wrong one

Give an Agent the chats and organization chart and ask “who should handle this?” It can often suggest a plausible person. Plausible is not authorized. A frequently mentioned employee may be collecting evidence for everyone else. A rarely mentioned executive may be the one who gives final approval.

Finding a relevant person and executing an authorized action must be separate. The Agent might suggest asking the long-standing supplier owner to verify a delivery date. To create an approval task, it must consult the current policy and permissions. If the sources disagree, it should not quietly choose the convenient one. Software stores people, roles, approvals, and access boundaries; the Agent explains who should be consulted and who may act.

The person on site must catch a common sentence: “We normally go to Wang.” What do people go to Wang for—advice, preliminary review, delegated review, final approval, or just to locate the paperwork? Unless someone asks for the verb, the apparently precise relationship “Wang is responsible” can displace the actual division of responsibility.

## Deploy the responsibility chain as well as the system

A customer should not judge delivery solely by “approvals now run.” Replay disputed cases. Who declared urgency, verified the reason, advised on the supplier, approved the budget, and had power to pause when evidence was lacking? Each step should have a record and source that survives a personnel change.

Someone capable of owning deployment brings these boundaries into the open before launch. They leave unresolved decisions for human confirmation instead of treating a loud meeting voice as authority. That judgment cannot be manufactured by an org-chart import template or a short course.

They also leave the organization a correction path. If an Agent assigns a task to someone who should not approve it, who withdraws the task, who informs the right person, and how is the original assignment preserved? Companies may tolerate “sent to the wrong person” far less than the system team expects. Without a correction mechanism, automatic routing turns one mistaken relationship into a new chain of responsibility disputes.

In Oryh, an approval record says who approved or rejected something and when; the backend does not quietly choose the next person. An Agent reads the customer's current workflow definition and work items to advance it under real authority. This lets the company keep its own management practice, but it also makes the on-site problem plain: if nobody has established who may confirm and who may decide, a beautiful deployment can still run an unowned process.
