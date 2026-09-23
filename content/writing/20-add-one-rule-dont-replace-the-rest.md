# Add One Rule. Why Did the Others Disappear?

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 20*

“Add a condition,” a user tells the administrator's agent.

An ordinary request: keep the process, add one requirement. But in feedback from actual Oryh use, this replaced the entire active workflow definition with a short document containing only the new condition. The existing submission requirements and routing rules were absent from the current version.

The user hadn't asked to rewrite the policy. The agent had done so anyway.

We keep saying agents handle business logic, software keeps records, and customization can start with natural language. This incident was a reminder: asking users to say less doesn't mean the system has less to understand.

## The API's “publish” isn't the user's “add”

The server hadn't failed to save a line.

The publication endpoint accepts a complete workflow definition. Each publication stores a new version and marks its predecessor as superseded. It doesn't automatically append incoming text to the previous document.

The Skill responsible for authoring rules hadn't made that distinction clear. It instructed the agent to draft and publish, without explicitly requiring it to retrieve the current document and incorporate the requested change. Asked to add a condition, the agent drafted that condition and published it as the entire new definition.

The request was valid to the interface. The action was wrong for the user.

The previous version still existed; history hadn't been physically deleted. But the next agent reading the active rules would find a policy missing most of its contents. Successful storage was a long way from successful customization.

## Don't make the backend guess how to merge policy

An easy-looking fix would be automatic appending on the server. But “change five thousand to ten thousand” isn't an append. Neither is “this clause applies only to new customers.” Attaching another sentence may simply create a different conflict.

Understanding whether the user means to add, amend, or replace remains the agent's work. Software should reliably store the complete version that has been confirmed.

We changed the Skill's operating instructions: amend by default, don't rewrite. Retrieve the current text, start from it, change only what was requested, and carry the other clauses forward verbatim. Don't polish their wording or remove something because it looks outdated.

An explicit request for a full rewrite is a different operation. “Add one sentence” isn't permission to reorganize the whole policy.

## Confirmation must say what's being removed

A polished preview makes omissions hard to spot. We required policy-edit read-backs to identify three things: additions, changes from old wording to new, and removals.

The third is particularly important. If anything would disappear and the user didn't request deletion, ask before publishing.

Verification went beyond checking that the Skill contained a few new sentences. We put a real agent in front of an existing ten-line quotation policy and used the same kind of “add a rule” request.

It read the full text, noticed that the proposed clause conflicted with the first existing rule, proposed an adjustment to that rule's scope, listed additions, changes, and removals, and preserved the other lines. Then it stopped for confirmation.

No publication occurred in that verification, and the server's version remained unchanged. It demonstrated a reviewable amendment and a confirmation boundary in that case—not that every natural-language edit would now be correct. We also added checks to keep the key instructions from being lost in later edits.

## One sentence should produce a small, clear change

The response shouldn't be to make users copy the full policy, assemble a replacement, or learn the API format. They should still be able to say “add a condition.” Reading the existing rules, understanding the scope, preserving other agreements, and presenting the change for confirmation are work the agent should take on.

The difference from traditional customization isn't merely one fewer requirements document. The company's practice remains expressed in natural language for agents to interpret and carry out, rather than every change becoming another application branch.

Software preserves rules, versions, and business facts. Agents interpret what is being changed and how work should proceed. We want one-sentence customization to produce smaller, clearer changes that people can confirm—not to make one sentence an excuse to guess the entire process again.
