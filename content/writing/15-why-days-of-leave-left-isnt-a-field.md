# Why “Days of Leave Left” Isn't a Field

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 15*

When we first built leave requests, we hit a slightly awkward problem: our demo data had no published leave policy. Ask “How many days of annual leave do I have left?” and the agent had no basis for an answer.

More API calls wouldn't help. A document that determined the answer was missing. The right response was “I haven't found the company's policy,” not a number based on some familiar practice.

We added policies, employee hire dates, and requests in different states: approved, pending, cancelled, and others. The two demo setups deliberately used different rules. We wanted to test whether the agent could answer under this company's practices, not whether it could subtract.

## First, distinguish the number that is a record

Oryh doesn't add a “remaining annual leave” field to the employee. Software records who requested which kind of leave, the date range, its duration, and the subsequent approvals and states.

One test files a Friday-to-Monday request with a duration of two days. The server doesn't count four calendar days and replace the two with four. Whether weekends count depends on the applicable policy. The agent needs to explain the basis for this request's duration and have the person confirm it.

Those are two different kinds of number. “Two days were approved for this request” is an agreed record. “How many days are available now?” is an answer derived from rules and records.

The second can be recalculated. The first shouldn't silently change because the policy changed. Our Skill instructs agents to cancel an approved request and file a linked replacement when rescheduling, rather than overwrite its original dates.

## Four days needs an explanation

Before calculating a balance, establish the query date and period, find the applicable policy version, and read the hire date and relevant leave requests. Policy determines the allowance, carry-over, and conversion rules. The agent interprets those conditions; arithmetic can be delegated to a calculation tool.

The Skill includes this example:

> 4 days available = entitlement of 10 (policy v3) − 5 approved − 1 pending.

These are illustrative numbers, not a default allowance for every company.

That pending day matters. Otherwise, when two requests are submitted before either is approved, the second balance check can show the same days as still available. Once cancelled, a request no longer contributes to the pending or approved total. Its record survives. There's no balance field that needs a day “refunded” into it.

A request crossing New Year also can't be found reliably by filtering only on its start date. Our interface returns requests whose date ranges overlap the query period, so one beginning last year and ending this year isn't lost. Which year gets which days still needs the agent's interpretation of the policy.

## Explainable doesn't mean a long explanation

Usage feedback prompted another Skill change. People asked for a number; agents tended to recite design reasoning and related reminders. We changed the instruction to lead with the answer, followed on the same line by the arithmetic and the policy's code and version. Expand when someone has a question.

When two answers disagree, there's something specific to compare: different policy versions, a missing hire date, or an overlooked pending request. “The model is unstable” isn't a useful substitute for checking those inputs.

Showing the arithmetic isn't a complete safeguard, though. There is currently no server-side leave allowance lock. Reading pending requests isn't an atomic reservation and doesn't guarantee concurrent requests can't exceed the allowance. We require the agent advancing approvals to recalculate when assigning the review and give the approver the basis and any shortfall.

A request exceeding the allowance isn't itself an invalid record. The agent should explain the excess and follow the policy to the authorized decision-maker, not impose a blanket refusal on the company's behalf.

“Software records; agents handle business logic” becomes concrete here. Code guards date order, positive durations, and write permissions. Software keeps the facts and policies. The agent determines how the rules apply, explains the result, and advances the confirmation. We don't need a balance field that merely looks definitive. We need an answer whose basis we can inspect.
