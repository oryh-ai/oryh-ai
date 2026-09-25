# Old Repair Records Have No Tire IDs. Can a New Ontology Invent Them?

*When Agents Run the Business · A development note*

Think about a car repair record that says only “replaced tires.” It does not say which tires, identify the old ones, or record the batch of the new ones. The business now wants to manage warranty claims for individual tires, so it adds a Tire object with an installation date and manufacturing batch.

New repair tickets can collect that information from today onward. What happens to the old ones?

This is a hypothetical case, not a customer incident. It illustrates a simple point: changing a model is easier than changing history. Adding an object type does not produce facts that were never collected.

## Blank does not mean no

An empty “tire ID” in an old repair ticket might mean at least three things: no tire was replaced; a tire was replaced, but the system did not ask for an ID; or a tire was replaced and its ID survives on a paper attachment that has not been entered. Compress those cases into one empty value and then count every blank as “not replaced,” and you may get a very tidy, very questionable report.

Sometimes the original documents can help. An invoice may show specification, quantity, and batch, while a warehouse issue slip gives the date. Together they might support “two tires from this batch were issued that day.” They still may not prove which one was fitted to the front-left wheel. A batch is not a single item; issuing stock is not the same event as installation. The evidence determines how far backfilling can go.

Many old records contain only “repair complete.” A person's rough memory cannot sign yesterday's receipt. AI can read invoices, compare dates, and suggest likely matches. That is useful. It cannot turn an unsupported guess into a verified component history.

One kind of progress report is especially seductive: “98 percent of historical cars migrated to the new model.” If most of them were assigned four anonymous Tire objects by a script, each with a default installation date, the number tells us how full the new table is. It does not tell us how much of the past was recovered.

## Make room for unknown

An ontology advocate might point out that formal knowledge representation does not necessarily treat missing information as false. Fair point. In OWL, for example, the [W3C primer](https://www.w3.org/TR/owl-primer/) distinguishes a fact not being stated from a fact being false. A missing statement may simply be unknown.

That principle is worth keeping. Enterprise work, however, goes beyond the semantics of a reasoner. Someone has to filter for tires under warranty, tell a customer whether replacement is free, or estimate a provision. At that point the system cannot answer merely “not disproved.” It must not quietly put “unknown” into “no problem” or “expired,” either.

I would rather see an unglamorous migration classification: confirmed from original records; inferred from several sources but not confirmed; insufficient evidence, unknown. Every backfilled detail should, where possible, point to an invoice, repair ticket, or warehouse record and say who confirmed it and when. Those states can improve over time. A required field in a new interface must not force them all to become “confirmed.”

The query interface must be honest too. Unknown claims should not appear in a filter for “confirmed covered,” yet they must not disappear from a queue for “may need manual review.” The same records can lead to different work under different questions. A convenient filter is no excuse to force unknown into yes or no.

If a model has no room for unknown, fix the model. Do not invent the history.

Backfilling also involves two different dates. A tire may have been installed three years ago, while its number was recovered from an old invoice only today. The record should say both “this happened three years ago” and “we learned this today from this invoice.” If we write only the old installation date, a later reviewer may believe the system knew the number at the time. That matters when reviewing a past decision: the customer-service agent could not have used evidence nobody had found yet.

Likewise, an AI suggestion should not overwrite the old repair ticket. It can attach a candidate, its source, and an explanation of uncertainty. A person with authority can confirm it as a supplementary record. If the invoice later turns out to have been matched to the wrong car, that supplement must be retractable rather than leaving a falsely complete old ticket behind.

## Yesterday's decision may not be reproducible at today's grain

There is another trap. The old system once labeled a car “under warranty” based on the vehicle purchase date. The new rule considers each tire's batch, replacement date, and position. Someone proposes rerunning every old case under the new rule to give historical reports a consistent definition.

But the old cases do not contain the new inputs. Is the resulting warranty status calculated from facts, or from defaults entered into blank fields? If today's rule turns yesterday's approved repair into “should never have been covered,” the policy shown to the customer at the time may also have been different. Overwriting the old judgment can be wrong and can erase the reason the company acted as it did.

A safer approach preserves what happened: the rule version used, the evidence available then, the decision made, and any later discovery of new evidence. We can run a new-rule retrospective analysis, but it is a new analysis, not the original decision in disguise. History is not a cache waiting to be overwritten by the latest model.

That is where the division between software and Agent matters. Software may not have perfect old records, but it can preserve honestly what was recorded and what was not. An Agent can search for supporting documents, explain the difference between policy versions, and recommend a review. At the break in the evidence, it should stop. It should not draw a neat link to fill the gap.

## Migration rate is not fact recovery rate

A careful migration team can ask concrete questions. How much backfilled information points to an original source? Have “batch known” and “individual tire known” been kept distinct? Does an old blank mean nothing happened, nothing was recorded, or the papers were lost? Do new reports show those differences?

These details matter more than the number of objects added to a graph. Each link should ideally open a supporting document. If it cannot, at least label it an inference. Asked whether an old tire is covered, an Agent's best answer might be neither yes nor no: “This repair ticket does not identify the individual tire; we need the original paper record.”

We have already faced a similar time problem with product mappings in Oryh. The same marketplace listing can later represent a different product. We preserve the original title and the effective dates of each mapping so an Agent can use the relationship that applied when an order was placed, not today's product to explain yesterday's order. The tire example is fictional. The rule against making a new model testify for old facts is not.
