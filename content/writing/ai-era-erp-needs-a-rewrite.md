# ERP for the AI Era Needs a Rewrite, Not an Agent Add-on

*When Agents Start Operating the Business: Design Explorations from ORYH — A Development Note*

Let's put our position plainly: ERP for the AI era isn't an existing ERP with an agent attached. The software needs to be fundamentally rewritten.

Building Oryh, this is the division of responsibility we want to change: software records; agents handle business logic. If business judgment remains embedded in the old application, the customization problem hasn't been untangled. It has acquired an interface that can talk.

## Operating the software isn't the same as working the company's way

Suppose a company normally pays an expense after its project manager confirms it. The software, however, requires an extra document and another approval round in between. Add an agent and it can complete those steps for someone.

But what if the company says, “We don't need that intermediate step”?

As long as the backend makes it mandatory, the agent can't get around it. Someone still has to change the program or change how the company works. The implementation problem remains; operating the system has become easier.

We don't want to automate the job of making companies accommodate software. Nor do we want to give every company an AI programmer that generates its own customized application faster. That would produce branches faster, with the maintenance bill still to come.

## We've made this mistake ourselves

Expense settlement in Oryh took exactly this detour.

To prevent duplicate settlement, we once required every expense claim to become a payable invoice before a payment could be applied. We closed the route that allowed settlement against the claim directly. It looked tidy technically. It also quietly chose a management practice for the company.

Some companies want that payable document. Others want to settle an approved claim without creating another one. Why should they have to choose the approach we preferred?

We restored direct settlement and changed the code to prevent the same expense from being settled through both routes. The company's chosen route is written into its rules; the agent reads those rules and proceeds. If the choice hasn't been made clear, it asks.

It was a small change with a large distinction behind it. Software should prevent the two routes from recording the same settlement twice. That doesn't entitle it to require every company to manage reimbursement the same way.

Without changing the original backend restriction, even a much smarter agent could only enforce it. That's why we say the software needs a rewrite.

## What does implementation become after that rewrite?

A rewrite doesn't mean discarding business models or handing every calculation to a language model. Order lines must add up to the order amount. A payment application must not exceed what can be settled. Permissions must hold. Code still enforces those hard constraints.

What comes out of the application is the company's way of working: who reviews first, when another approval is needed, what happens when evidence is missing, and who can confirm an exception. Software stores the facts, rules, and their versions. The agent uses those records to make business judgments and advance the work. Where a person must approve, it still waits for that person.

In our demos, we've also used the same built-in order records for a manufacturer's shipping and receipt process and a consulting team's project delivery. Their ways of working live in their respective workflow definitions and Skills. We didn't write a separate order backend for each. That's a demonstration within a concrete scope, not proof that every industry's needs are already covered.

With this separation, implementation can shift from fitting a company into a predefined process to making its practices explicit, then using actual cases to check whether an agent can follow them. A policy change needn't routinely turn into application development and a release.

Customization needs don't disappear. If the records can't represent a new business fact, the model needs work. Ambiguous rules need clarification. Migration, permissions, and verification don't complete themselves. What we want to break is the coupling that makes a different management practice require a different version of the software.

A company may choose to improve its management. It shouldn't have to substantially reorganize how it works simply because a software package has prescribed one route.

Oryh isn't our attempt to give the old ERP a smarter operator. It's an attempt to rewrite what the software is responsible for. Software keeps the records; agents judge and advance the work under the company's rules. That's why we think ERP for the AI era is worth rewriting.
