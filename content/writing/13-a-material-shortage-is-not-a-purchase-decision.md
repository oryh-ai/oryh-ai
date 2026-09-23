# A Material Shortage Is Not a Purchase Decision

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 13*

In contract manufacturing, “How much material does this run need?” and “What should we buy next?” look like consecutive steps. We put them in different places.

The software calculates the first. The agent handles the second.

Our test has 40 valves, each requiring one valve body. The body's recipe is written per ten units: 25 kilograms of steel, plus a 4% scrap allowance. Expanding it gives a requirement of 104 kilograms. The recorded available quantity is 100 kilograms, leaving a shortage of four.

Oryh returns that number, and the query ends. It doesn't create a purchase order along the way.

## First, get those four kilograms right

A bill of materials, or BOM, isn't necessarily written per finished unit. One recipe may be for ten units, another for a hundred. An intermediate assembly can have a recipe of its own.

The calculation above is `25 × (40 ÷ 10) × 1.04 = 104`. Use the wrong output basis or miss a level, and careful purchasing decisions will still start from a bad number.

We therefore record output quantity, component quantities, and scrap rates as structured fields. Code expands the levels and combines repeated materials at the leaves. The agent doesn't have to reconstruct that calculation in every conversation.

The records need firm boundaries too. Each product can have at most one active recipe; activating a new version archives the previous one in the same transaction. Active recipe lines cannot be edited directly—a change starts as a new draft version. Code also rejects a component chain that loops back to its own parent.

“Software records; agents handle business logic” doesn't reduce the software to a handful of storage endpoints. Versions, references, and deterministic calculations need to hold up before an agent can use their results.

## Whose material is missing, and where?

The harder part is that four kilograms doesn't tell us which supplier to order from. It doesn't even establish that we should buy the material ourselves.

If the factory supplies the materials as part of the deal, we can pass the requirement along as advice. It doesn't mean we should also place an order with a steel supplier. If the contract says we supply materials, sourcing them becomes our next concern. We explicitly separated those cases in the purchasing Skill.

Location matters too. Stock somewhere in the company isn't necessarily available at this factory. We later added a facility filter to the expansion endpoint so it can compare requirements against stock at a specified location. The agent has to establish the relevant scope, rather than treating the company-wide total as material waiting outside the factory door.

Even when we supply the material, the next step might be a transfer, waiting for an existing order to arrive, or discussing the delivery date. Those choices need orders, receipt records, and contract terms. They don't follow from the difference between two quantities.

## Let the calculation stop and the agent continue

The operating sequence lives in the Skill: find the recipe, obtain requirements and shortages, read the contract, and work out the next step using the company's rules. Before writing a purchase order, show the person the supplier, materials, quantities, and relevant conditions for confirmation. Then record the actual decision.

The expansion endpoint remains a read. It doesn't store an automatic purchasing plan or advance an approval because a shortage is positive. Software keeps the records and performs the calculation. The agent gathers the supporting material, explains the choices, obtains the required confirmation, and uses the interfaces to continue.

We also need to be precise about the current calculation's scope. It expands recipes down to their leaf materials and compares those requirements with current available stock in the selected scope. It doesn't first consume existing subassembly stock before expanding the remainder. Nor does it schedule incoming materials against a production calendar. Calling the result a complete purchasing plan would go too far.

What we want to keep watching is whether the agent can distinguish “the gap calculated for this recipe, quantity, and stock scope” from “the quantity we have decided to buy.” The first is a definite calculation. The second still needs judgment. Our job is to connect those steps without allowing an accurate subtraction to make an unconfirmed purchasing decision for the company.
