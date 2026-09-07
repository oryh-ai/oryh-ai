# When Product Names Don't Match, Don't Guess

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 10*

While building channel-order imports, we got stuck on a column of product names.

ORYH initially mapped a platform's product ID to a product in the internal catalog. But a merchant's downloaded order sheet might contain only listing titles and specifications, with no product IDs at all. We had a mapping table, but the material in front of us couldn't use it.

We added lookup by title, preserving the original text while letting code handle differences in case and full-width spaces. That brought us to the next question: what should happen when a title has never been mapped before?

## The top search result isn't ready for the order

In our test example, the platform title is “【官方旗舰】保温杯500ml樱花粉 便携随行杯”—roughly, “Official flagship · insulated cup 500ml, sakura pink, portable travel cup.” The internal product is simply “保温杯 500ml,” with a 350ml version nearby.

A literal search can miss it. Removing promotional words doesn't guarantee the right answer either. Get the capacity, color, or pack quantity wrong, and the order can be wrong with it.

We added a candidate search that breaks Chinese text into adjacent character pairs, combines them with English and numeric terms, and ranks products by shared terms. Names can then surface even when spaces disappear or words change order.

This is worth pausing on. Software being responsible for records doesn't mean it can only store and retrieve rows. Deterministic tools for searching, calculating, and validating still belong in code. But a search score measures vocabulary overlap. It isn't a probability that two descriptions identify the same product.

The candidate endpoint returns a list. It neither chooses a product for the agent nor writes a mapping.

## One confirmation should become a reusable record

We put the next steps in the agent's Skill: check existing mappings first; search for candidates only when no mapping exists; collect unresolved titles across the batch and ask the person together, with product codes, names, and specifications alongside them.

The questions need to be specific. Is this the 500ml sakura-pink version, or another variant? If none of the candidates fits, leave the match unresolved. Finishing an import isn't a reason to force a choice.

The agent's job here is to interpret the material, notice differences, organize the confirmation, and continue the work. Some judgments need additional business facts. Asking a person for those facts is part of moving the job forward.

Only after confirmation does the mapping get written back to ORYH: the source channel, original title, internal product, and quantity become queryable records. When the same product appears in another batch, the agent reads that record first. It doesn't need to guess again or rely on a previous agent's conversation memory.

We also adjusted permissions. Originally, only catalog administrators could maintain mappings, so every new title required a handoff. Someone authorized to record orders can now save a title-based mapping, while creating a product still requires catalog-management permission. Identifying an existing product and adding a new product to the catalog are separate acts.

## The agent runs the process; the software keeps the result

We didn't add a backend business rule saying “automatically select a product above this similarity score.” The software stores mappings and enforces permissions and record constraints. The agent uses the available records to decide whether to continue the import, investigate further, or wait for confirmation.

Mappings also have effective dates. A listing can keep its identity while the goods behind it change. The agent must query using the order's date, and the software returns the relationship valid on that date. Today's product shouldn't silently explain yesterday's order.

Our tests check that reordered names still appear among candidates, changed spacing still retrieves a saved mapping, and order-entry credentials cannot use this route to create products. Skill checks preserve the sequence of confirmation before writing a mapping. These verify boundaries in the interfaces and instructions; they don't prove that an agent will follow them in every real interaction.

An unfamiliar, unconfirmed title still interrupts a person. That's a cost of the current approach. We want to keep watching whether the question is clear, whether the answer actually becomes a record, and whether the next import needs one less question. Software records; agents handle business logic. These small decisions are where that division becomes real.
