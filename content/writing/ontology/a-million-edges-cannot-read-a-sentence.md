# A Million Edges Still Cannot Read a Sentence

*When Agents Run the Business · A development note*

The usual prescription for enterprise AI goes like this: define an ontology, then turn the company's information into a knowledge graph. Customers, orders, project owners, and purchasing approvers all become nodes and edges. When someone asks a question, traverse the graph to find the answer.

A finished graph resembles a network of knowledge in a mind. That picture makes it easy to believe the system understands the company.

But connecting the dots and understanding what someone said are different things.

## Why did we turn knowledge into graphs?

Traditional software is good at lookup, calculation, and following predetermined conditions. It cannot read meeting notes as a person would and understand what “let the project manager look at this first, but finance still needs to give final approval” means for the decision at hand.

To make that instruction usable by a program, someone first has to translate it. The project manager becomes an entity. The project is linked to a purchase order. Approval roles and actions get defined. The ontology supplies the concepts and relationships; the knowledge graph holds the actual people, documents, and connections.

In the common RDF model, a graph consists of subject, predicate, and object triples, as [W3C specifies](https://www.w3.org/TR/rdf11-concepts/). A program can query and traverse those triples. It learns which connections have been represented in the data. What those connections mean for a particular business decision still depends on how people modeled them, what information they entered, and how the program uses the query result.

There was a reason to do this translation. Without it, much older software could do little with the knowledge people wrote down. But when an Agent can read the meeting notes and the policy itself, we should ask whether all that material still needs to be rewritten as nodes, edges, and predetermined rules first.

## A path to the project is not approval authority

Suppose a purchase order belongs to Project P, and Zhou manages P. Two edges are easy to draw: Zhou manages P; the purchase order belongs to P. A query finds Zhou.

The system may then give a neat answer: “Zhou should approve this purchase.”

But the company's actual instruction might be: “The project manager checks the purpose first. Purchases over 50,000 require approval from the finance lead. While the project manager is away, the person named for that week may review the order, but may not approve it.”

Zhou's connection to the order is real. The mistake is to turn “this person is relevant” into “this person has final authority.” Traversing the graph looks like reasoning. The leap from relevance to authorization was actually made earlier, by whoever wrote the query or the rule.

Of course we can add more edges: approval authority, amount thresholds, deputies, effective dates, and exceptions. Keep going, and an instruction that a person could read becomes a model and a collection of rules that must be updated. Then the next sentence arrives: “Have someone review it this time, but do not approve it yet.”

This is not a claim that knowledge graphs cannot express complex information. They can. The problem comes when the graph is treated as the layer that understands the company. People must then anticipate how every business distinction will be represented, changed, and maintained.

## “The system knows” often means its answer sounds right

The most unsettling quality of a knowledge graph is how easily it produces a polished answer.

Ask who handles a purchase, and the program retrieves a project manager. Ask what a customer has bought, and it follows a path through customers, orders, and products. A user interface turns the result into a smooth sentence. The system seems to know the business.

Yet a processor has not come to understand the difference between “responsible,” “review,” and “approve” by retrieving a few edges. It has executed a representation and a procedure someone wrote. The output can be useful and even correct. Fluency does not prove that the underlying representation is complete.

That illusion becomes dangerous when it drives decisions. A model that omits “finance still has to approve” may still return an approver, show a workflow, and issue a task. Everything appears to work except the decision itself.

The user may not even know what was omitted. If the source meeting notes and policy sit behind the graph, the screen presents only an authoritative sounding conclusion. To understand the error, someone has to trace which words were translated into which edges and rules.

## An Agent can read the words, and still needs to check the facts

AI changes the starting point. An Agent can read “check the purpose first; finance approves purchases over 50,000,” then look at the purchase amount, the project, and the current staffing arrangements. It can explain why it proposes the next step. If the company adds “reviewers cannot approve on behalf of someone else,” the instruction need not wait for someone to invent a new relationship type before the Agent can consider it.

That does not mean the Agent will always read correctly. It may miss “over,” confuse review with approval, or pull the wrong project. We have to make it show its evidence: which policy version, which purchase order, which amount. When the evidence conflicts, it should ask. Code still enforces permissions, amount calculations, and protection against duplicate writes.

We have seen a failure on this side of the boundary too. An administrator asked an Agent to “add one condition.” The Agent replaced the current workflow definition with a short document containing only the new condition. The old version still existed, but the next person to run the workflow would read an incomplete policy. We changed the revision procedure: read the entire current text, show what will be added, changed, and deleted, and ask before removing anything the user did not request. An Agent that reads people's words can still misread their intent. The original text, its versions, and the scope of each change must remain visible.

A knowledge graph can still help. Stable links between people and documents make relevant material easier to find. Graph queries are useful for clear, structured questions. Confirmed identity mappings and relationships with sources deserve to be recorded. What we reject is making the graph a mandatory translation of the company's knowledge, with the original words hidden behind it.

That would recreate the old software path: translate the company's language into a machine format, then have the machine produce answers from that format. The graph changes the format, while the company still bears the translation work and its errors.

## Let the people who speak keep their words

The division of work can be simpler. Software records who said what, when a rule took effect, and what happened to each document. It can index and query records and check exact quantities. The Agent reads those records and the rules people wrote, judges the case in front of it, and asks when it needs confirmation. Its reasons should be recorded too, so people can review and correct them.

We need not first split “the project manager reviews, finance approves” into a network of edges and rules before the system can help. The practical questions are whether the original instruction can be found, whether the facts are accurate, and whether the Agent knows when it lacks authority to decide.

A knowledge graph can help us find a path, but the path is not the destination. An ontology can help us name things, but a name is not understanding. In Oryh, we want software to preserve the record and the Agent to reason from people's own words and checkable facts. When it is unsure, it should bring the question back to a person instead of continuing along a path that merely looks complete.
