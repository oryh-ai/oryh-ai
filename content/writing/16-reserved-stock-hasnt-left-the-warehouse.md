# Reserved Stock Hasn't Left the Warehouse

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 16*

Sales promises to hold three units for a customer, but the warehouse hasn't shipped them. Should inventory go down?

One number makes this awkward. Reduce it and the goods are still on the shelf. Leave it unchanged and someone else may promise the same goods to another customer.

Oryh records these as separate facts. In our test, a stock position starts with ten units. Reserving three for an order leaves ten on hand and seven available to promise. The reservation names the order whose goods are held. It doesn't pretend that anything has left.

## Don't deduct availability again when shipping

When those three units actually ship, there's an easy detail to miss: availability has already been reduced.

Deduct another three from both quantities and we'd end with seven on hand but only four available. The goods left once; availability was reduced twice.

We put that coordination in code. When posting a shipment to inventory, the server calculates what the order still holds at that position, releases the portion consumed by this shipment, and records the actual issue. Both ledger entries land in one transaction. The result is seven on hand and seven available.

“Release” here doesn't mean goods came back to the warehouse. It means actual shipping has consumed the earlier reservation.

We also added a test with two parcels: reserve three, ship two, then ship another two. The second shipment can consume only the one unit still held; its other unit comes from unreserved stock. Releasing against the original three every time would invent availability.

An agent shouldn't have to assemble this arithmetic afresh for every shipment. Recording correctly includes calculating the definite quantity relationships between records.

## Later, we removed direct ledger writes

Another shortcut appeared in use. An order operator said “ship it,” and the agent skipped the order and shipment records, appending a stock deduction directly to the ledger.

The number changed, but the business event behind that change wasn't captured through the proper document chain. A Skill reminder to confirm before writing wasn't enough to prevent it.

We removed the generic inventory-movement write endpoint. Reservations and releases now use dedicated actions on the order. Customer shipments affect stock through shipment posting, with the server generating the ledger entries. The agent no longer picks a reason, supplies two deltas, and calls the work done.

We also added quantity checks. If current availability is insufficient, a reservation reports the shortfall. If the order holds only one unit at that position, it cannot release two. An error should tell the agent what needs discussing with a person, not encourage it to adjust a number and retry.

## When to reserve still isn't the code's decision

Some companies reserve when an order is confirmed. Others ship straight from the shelf. Whether to release a cancelled order's hold, or how much to release after a partial cancellation, starts with establishing the actual decision. The agent reads company rules, the order, and delivery arrangements, obtains any required confirmation, and calls the appropriate action. Releasing a cancelled order's hold doesn't change on-hand stock. The agent must not separately release what shipment posting has already consumed.

There's also an unfinished gap to acknowledge. A recent local database concurrency test started with ten available units. Two simultaneous requests each reserved seven, both succeeded, and availability ended at minus four. Having a quantity check for an individual request doesn't make concurrent requests safe.

That issue remains to be fixed. Code needs to protect the check and the write together. Asking agents “please don't act at the same time” isn't an inventory safeguard.

So “software records; agents handle business logic” doesn't hand every inventory problem to the model. When to hold goods, for whom, and how to coordinate a shortage are judgments the agent advances under company rules. How much is held, remains available, or has left are facts and quantity relationships the software must protect. “Are the goods still here?” and “Can we promise them to someone else?” can finally have separate answers. Neither side of that division gets to skip the engineering.
