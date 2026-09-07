# Why Do We Need a Flow Runner?

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 7*

A manager approves a document and closes their laptop. The employee's agent has finished its conversation, too. The document, approval records, and todos are all there. But someone needs to hand the work to finance. Who does that?

The previous note was about keeping work from disappearing when an agent stops. Keeping it in the system doesn't make it move on its own.

That's the job of the Flow Runner: an agent responsible for moving workflows forward. It checks for work, reads the company's rules and current records, and decides who should receive the next task or whether the process has finished. If a person needs to approve, it waits. If the rule is unclear, it stops and asks.

## You can choose who runs it

Our initial arrangement was for customers to run their own flow agent. That option remains. Customers can choose an agent that can read the rules, use ORYH's interfaces, and operate with the appropriate authorization. They can also run a dedicated Flow Runner on their own server.

But having to look after an agent just to keep business processes moving felt like an extra job for some customers. So oryh.ai offers a server-side arrangement, currently using Pi Agent.

Pi is oryh.ai's runtime choice, not a requirement ORYH places on a customer's agent. It receives a task and operating instructions, then calls the public API to read and write the same business records. Choosing a different runtime shouldn't mean rewriting the company's workflow rules in a different format.

Changing the agent does require a handover, though. If the customer's agent and the hosted agent both take responsibility for the same work, each might assign a different todo. Both API calls could be legal while the resulting work makes no sense. Choosing who drives the flow also means agreeing on their responsibilities.

## The resident program doesn't interpret the business

Building the server-side arrangement raised another question for us: with a program running all the time, were we building a workflow engine again?

We separated the two responsibilities. A dispatcher checks whether work is waiting, decides when to start a run, limits how much it can handle, and stops repeated failures. An empty queue doesn't need a model invocation.

The agent still makes judgments such as “all approvals in this round are complete” or “finance needs to review this next.” The software stores rules, documents, and approval facts, and enforces hard constraints such as permissions and legal state transitions. The dispatcher doesn't contain the business rule that one particular approver must follow another.

In our current Pi integration, the dispatcher stays resident, but each run starts a fresh agent session. Progress is read from ORYH rather than kept in an uninterrupted conversation. The code connecting the runtime is separate, too, giving us a place to replace and compare implementations.

## A clean exit doesn't mean the work got done

We ran into a surprisingly easy mistake to miss: model calls failed because a provider credential had expired, but the Pi process still exited normally. Checking only the exit code would mark that run as successful. Apparently, it just happened to advance nothing.

We added checks for errors in the runtime's event output. We also record the agent's own report separately from changes in the queue before and after a run. “I handled three items” is a claim. What changed in the system needs its own check.

Even a smaller queue doesn't prove the next approver was chosen correctly. We still need to inspect the todos and approval records left behind. Repeated runs without progress should stop and leave a visible reason for someone to investigate.

Working through this made the Flow Runner's place a little clearer to us. Giving business logic to an agent still leaves the software with execution responsibilities. It needs to keep a reliable account of attempts and resulting facts, while the agent uses the company's rules to carry the work forward.

We'd like to be able to replace Pi someday, or hand responsibility to a customer's own agent, and have the work continue. What we hand over should be the work itself, not just a prompt.
