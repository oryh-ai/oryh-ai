# Does an FDE Badge Make You an Enterprise AI Expert?

*When Agents Run the Business · A development note*

Lately, nearly every on-site role in an enterprise AI pitch seems to be called FDE. The person writing integrations is an FDE. The person configuring workflows is an FDE. The person arranging meetings and chasing the launch date is one too. Put three letters on a badge, and an ordinary engineer is apparently transformed into an AI expert.

I have no quarrel with people doing those jobs well. On-site development is demanding; project management is demanding too. What bothers me is the suggestion that a new name means the customer has bought a different capability.

## The D is for Deployed, not Development

The D in Forward Deployed Engineer points to working close to a customer's real problem. It does not stand for “Forward Development Engineer.” Yet it would be equally dishonest to claim that FDEs never write code. [OpenAI's public role description](https://openai.com/careers/forward-deployed-engineer-%28fde%29-seattle-seattle/) covers discovery, design, building, and production rollout. [Palantir's posting](https://jobs.lever.co/palantir/c4442730-2926-41ad-8c0e-5e5a6b4d14ae) explicitly mentions coding customer applications.

So I would not call someone a fake FDE merely because they code on site. Integrations, security issues, and product gaps may require a person who owns delivery to write code themselves. The question is what they actually resolve.

An on-site developer receives a request: “Add one more approval level.” They ask the customer for a workflow diagram, add a customer-specific branch, test that it runs, and wait for sign-off. Done well, this is respectable work. It does not automatically make them the person who can independently own an enterprise AI deployment.

If they introduce themselves as an FDE, I want to ask more. Why is another approval level needed? For which documents? Who has authority to approve? What happens to requests already halfway through the old process? Will an Agent send work to the wrong person when the evidence is incomplete? Is the code filling a general product gap, or implementing a genuinely special customer rule?

If every one of those questions goes back to a product manager at headquarters, the on-site role is still largely information transfer and development execution. Sitting in the customer's office does not confer industry experience, organizational judgment, or authority to own the consequences.

## A successful demo is not a deployment

AI demos make on-site competence easy to overestimate. Connect a model, upload a contract, ask an Agent who should approve it next, and a fluent paragraph appears. Everybody nods. Only the next day does a real contract arrive: partly executed, amount revised, approver on leave. That is when the questions the demo skipped become visible.

Someone who owns deployment should understand at least four things: whether the source data can be trusted, which policy version applies, whether the Agent has authority to act, and how errors will be detected, stopped, and corrected. They need not solve every problem alone. They do need to know whom to involve, what evidence to seek, and when the process must pause.

That is a long way from “knows how to write prompts.” A prompt can make an answer sound expert. It cannot establish who may sign, whether a payment has already been sent, or whether an earlier approval should be withdrawn. In production, the dangerous failure is not an inelegant answer. It is a smooth error that turns into an executable recommendation.

Title inflation hides responsibility. The customer hears FDE and expects someone capable of making hard judgments at the site. The supplier sends someone tasked with configuration, interfaces, and schedule coordination. When something goes wrong, the person on site says, “I need to ask headquarters,” while headquarters says, “The on-site team knows the customer best.” Everybody participated; nobody owned the judgment.

That is why I care more about owning delivery than about being “good at AI.” A field lead need not know every answer on the spot. They should be able to mark the uncertainty and give the customer a temporary safety boundary: which actions may continue, which pause, and which need an authorized decision. “The model is usually accurate; let's go live and see” is not deployment judgment. It assigns the cost of learning to the customer.

Responsibility continues after launch. A failed demo can be rerun. A task issued in production, an approval written to a record, and a person already notified do not vanish when a prompt is edited. Someone calling themselves an FDE should explain how an Agent's basis is retrieved, how a bad record is corrected, and how the next owner learns what happened. “Fixed” cannot mean merely that the next answer sounds better.

## Three plain questions for the customer

Skip the certificate and title at first. Ask the candidate about a delivery judgment they personally made. Which sources conflicted? How did they confirm the applicable rule? What did the software prevent deterministically, and what did the Agent have to judge? After launch, how did they check that the decision was not amplifying an error?

Second, what happens when the customer asks for something outside the product boundary? Writing customer-specific code may be the right answer, but the candidate should explain its cost, who will maintain it after upgrades, whether it belongs in the product, and whether a simpler way of recording or running the work exists. “We can customize anything” often means postponing a difficult decision.

Third, when two people inside the customer company give different instructions, whom do they follow? Who is authorized, who supplies the facts, and who accepts responsibility for the decision? An on-site engineer must not seize the company's authority. They also cannot hide “who decides” as a vague name in the meeting notes.

Someone who can answer these questions is worth trusting whether or not they are called FDE. Someone who cannot will not be rescued by a better acronym.

Customers can put this into acceptance rather than rely on a résumé. Give the field team a case with conflicting policies and see whether they stop. Give them work partly executed and see whether they preserve its history. Ask the lead who may correct an erroneous decision. These exercises cannot prove that a person will never make a mistake, but they say more than a count of “AI projects participated in.”

## The title is not the deliverable

The problem is not that a company uses the name FDE. It can be a legitimate job title, and excellent on-site people exist. The problem is a product still relying on patches, a customer decision still lacking an owner, and a sales pitch saying only, “We'll send an AI FDE.”

If the work is gathering requirements and writing customer-specific branches, call it on-site development. If the main value is coordinating teams and keeping the launch on track, call it on-site project management. Both jobs matter. Neither needs a fashionable label to justify its existence.

In Oryh, we keep deterministic records and constraints in software while leaving the company's workflow judgments to Agents. That design does not remove on-site work. It makes it harder for a person on site to hide behind a code change: they must understand the facts, know who can authorize a decision, and catch the point where an Agent should stop. Whoever can own that judgment may deserve the FDE title. Three letters on a badge do not.
