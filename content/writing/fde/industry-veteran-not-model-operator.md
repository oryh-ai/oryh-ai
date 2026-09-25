# Industry Experience Is Not a Model-Operator Certificate

*When Agents Run the Business · A development note*

“This order is complete” sounds straightforward. Sales, the warehouse, and finance may hear three different things. Sales may mean the customer confirmed. The warehouse may mean the goods have left. Finance may still be looking for an invoice and payment. If someone on site takes one system status as the company's universal definition of “complete,” an Agent may advance the work faster and in the wrong direction.

Some say an FDE need not know the industry: bring a strong model and ask the customer. I do not buy it. A model can read material, but who knows what to ask, which answer remains incomplete, and which action passes risk downstream? That knowledge is more than an industry glossary.

## Experience is not a list of acronyms

Consider a manufacturing order. Sales has customer confirmation, production is scheduled, but the warehouse is short by four kilograms of steel. Someone unfamiliar with the work may say, “Shortage detected; create a purchase order.” A shortage is not yet a purchasing decision. Can another material be substituted? How much stock is reserved for a different order? Can the supplier arrive in time? May the customer accept partial delivery? Was the bill of materials expressed per unit, or per batch of ten?

Different answers produce different next steps. Sometimes reschedule production, sometimes verify reservations, sometimes buy material. The senior person's value is not the ability to recite BOM, MRP, and WMS. It is seeing the possible causes and consequences behind a number.

Retail has its own forks. “Sold” is not a single event: marketplace payment, merchant shipment, delivery to the customer, end of the return period, and settlement from the platform may happen on different dates. Using today's product title to explain last month's order may substitute a changed listing for what was actually sold then. Without a feel for these distinctions, a fast Agent can just blend facts from different times faster.

Nobody knows every industry. That is why I dislike the promise that learning an Agent platform makes someone ready to be an FDE anywhere. Connecting models and APIs is a tool skill. Knowing where a business error will cause loss is a judgment built over time in an industry.

## Do not use the customer as an introductory course

A customer can teach the person on site its particular practices. It should not have to teach basic industry mechanics from the beginning. When a purchasing lead explains why a shortage does not always mean placing an order, that should be a discussion of this company's decision process. If they first need to explain that reserved stock and stock on hand are different numbers, the supplier's “enterprise AI expert” has some catching up to do.

Industry experience is not infallibility, either. A veteran can import habits from a previous employer and assume everyone works that way. The good ones use experience as a set of questions, not a ruling. They know where to check contracts and original records and where their own authority ends.

For example, a customer says, “Once goods ship, the sales order is complete.” Someone who knows fulfillment will not immediately encode that as a rule or reject it. They ask about split shipments, refused delivery, later replenishment, and whether “complete” merely clears a sales dashboard or also ends finance reconciliation. The answers determine whether an Agent can close a task, release a reservation, or prompt invoicing.

Those questions are not just conversation. They determine which facts the record layer must keep, what an Agent can infer, and what still needs a person's confirmation. Without that judgment, the on-site person can turn the customer's shorthand into one all-purpose status and flatten away the differences that matter.

An industry veteran is also more likely to notice that the same word requires different evidence at different stages. “Shipped” in the warehouse may need an issue slip and carrier record. “Delivered” in sales may require customer acceptance. “Settled” in finance may require payment or an offset entry. A person on site need not process every document themselves. But if they compress all three into one Completed status, the Agent loses the material needed to explain why sales has finished while finance is still collecting money.

## Give judgment to Agents, not industry responsibility

We want AI-era software to stop hard-coding every company's practices. Software records orders, materials, reservations, actual shipments, invoices, and receipts; code calculates exact amounts and quantities. An Agent reads the company's rules and the present facts, then decides whether to chase missing evidence, create a work item, or suggest procurement.

That division gives customers more flexibility and gives the person on site more responsibility. They must recognize when an imported fact changed meaning, when a written policy is incomplete, and when a recommendation belongs on a review list rather than being executed. When a model says “buy more,” they should ask whether it used a real shortage or subtracted reserved stock twice. A wrong inventory query followed by procurement moves money and goods, not just words on a screen.

Someone who operates an AI platform can help deploy it and deserves respect. But “can connect a model” and “can take responsibility for a manufacturer's purchasing workflow” are not separated by one course or one job title. One is a skill; the other is experience, judgment, and continuing responsibility for outcomes.

## Choose the industry before the FDE title

If a supplier really uses an FDE model, let it say which industries and workflows its people understand deeply. A brochure that says “we serve every industry” is not evidence of that depth. Customers can ask which business exception the on-site lead personally handled, where they have stopped a bad step from happening, and what they do when the answer is outside their expertise: bring in a domain owner or push a generic-looking process forward.

Cross-industry learning is valuable, but only when one understands the differences. A retail veteran at a factory has to admit a learning area. A manufacturing expert entering services must relearn what “delivery complete” means. Printing FDE on a badge gives neither of them all industries at once.

Customers can ask a harder question than “how many companies have you served?” In which specific workflow did you change a deployment plan, and why? If the answer is always “I automated the process,” with no account of an unreliable record or a step that could not safely be automated, the experience may be with the platform rather than the industry. An honest statement of unfamiliar territory is often more reassuring than a claim to know every vertical.

In Oryh, we separated the calculation of a material shortage from the decision to purchase. The server calculates the bill of materials, expected loss, stock, and shortfall; the Agent reads the company's purchasing rules to determine the next step. Four kilograms short is a fact, not a command. Someone on site who cannot feel the difference should not be sold as an FDE for enterprise decision-making.
