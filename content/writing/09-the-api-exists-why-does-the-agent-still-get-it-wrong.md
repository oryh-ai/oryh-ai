# The API Exists. Why Does the Agent Still Get It Wrong?

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 9*

We once had an agent fill out an expense claim. All three lines had been written successfully through the API. The agent then told the user, “The third line hasn't been saved, so I can't submit this yet.”

The API had returned no error, and the database really did contain all three lines. The agent was still trusting its memory from several turns earlier.

That incident made us realize that building a good API for agents only gets us halfway there. An interface can make each call precise, but something still needs to explain when to call it, what to read first, and how to verify the result afterward.

## The API makes individual actions reliable

APIs are good at answering definite questions. Can this field be changed? Does this credential have permission? Do the amounts add up? Will retrying this request create a duplicate entry?

If a request is valid, the service should record the fact accurately. If it isn't, the service should reject it clearly. It shouldn't guess what the caller really meant or relax a constraint because the agent sounds confident.

A collection of correct interfaces, however, doesn't automatically add up to a correctly completed job.

After writing the expense lines, the agent needed to read the whole claim again, show the stored result to the user, and wait for confirmation before submitting it. Our Skill said to “repeat the complete claim,” but it didn't say where that complete version had to come from. The agent naturally repeated its own recollection and described a successful write as if it had never happened.

We later added a shared rule to every Skill that writes a record and then makes a decision: read the record again before deciding. If memory disagrees with the read result, the record wins.

That change didn't add business logic to the API. It taught the agent how to use a system of record.

## A Skill isn't an API directory

We now find it useful to think of the API, the Skill, and the company's rules as three separate things.

The API provides actions and enforces hard boundaries. A Skill teaches the agent how to complete a kind of work: where to find the records, how several calls fit together, when to read back, and when uncertainty needs a person's answer. Company rules say how this particular business wants the work handled, such as which evidence is required or which amount needs another review.

They refer to one another, but they can't replace one another.

Hand an agent the entire interface reference and it may know that a submit action exists without knowing that a person should review the document first. Put the company's approval policy inside the Skill and every policy change becomes a software release. Give the agent only a natural-language policy, without permission and amount constraints in the API, and one misunderstanding can create a record that should never have existed.

We have also seen the opposite kind of mistake. Someone asked, “What todos do I have?” The agent followed the procedure for processing those todos: it opened every underlying document, approval trail, and attachment, then returned a small investigation report. The answer wasn't wrong, but it performed work nobody requested. It also created more opportunities to expose irrelevant information or form a new mistaken interpretation.

Our Skills now distinguish between answering a fact question and carrying out a business operation. If someone asks for a list, return the list first. Read the supporting material when they actually ask to process an item.

## Operating instructions are part of the product

In conventional software, the interface constrains the path. Buttons appear at particular times, confirmation dialogs explain the next step, and the updated page shows what was saved. An agent doesn't follow one fixed path, so a Skill carries some of that responsibility.

Changing the service is therefore not enough when an API changes. If fields, action order, read-back behavior, or permissions move, the related Skills need to be checked as well. They need tests, revisions based on real failures, and enough editing that the important boundaries don't disappear inside pages of instructions.

“Software records; agents handle business logic” doesn't leave an empty gap between the two. The Skill sits in that gap. It teaches the agent how to read and write records reliably while leaving each company's judgments in its own rules.

When an agent mishandles something now, we ask one more question: did the interface permit a record that should have been impossible, or was the agent never taught how to complete the job? Both can look like “the agent used it wrong,” but they require very different fixes.
