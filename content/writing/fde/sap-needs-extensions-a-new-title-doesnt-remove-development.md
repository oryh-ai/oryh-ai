# Even Mature ERP Needs Extensions. Does Calling Someone an FDE Remove Development?

*When Agents Run the Business · A development note*

An enterprise software kickoff often includes a familiar line: “The standard product covers almost everything. We can configure the differences.” Two weeks before launch, finance brings a real reconciliation rule, purchasing adds an urgent-order path, and the warehouse explains that one document may be fulfilled in several shipments. The project team starts sorting requests: configuration, interface work, or customer-specific code?

This is not a sign that one vendor is uniquely bad. Traditional ERP puts much of the workflow into software ahead of time. However broad the product, it will not match every company's way of working. On-site development became part of delivery. Renaming its practitioners FDE does not remove code or maintenance responsibility.

## Separate three kinds of “we need to build something”

The first is genuine integration engineering. A company already uses banks, warehouse devices, commerce platforms, or tax systems. Data must move in and out. Protocols, authentication, retries, and field mapping do not vanish in the AI era. Write the code when it is needed, and make the interface maintainable. Do not imply that “deployment” always means a few configuration clicks.

The second is a missing general product capability. Suppose the system lets one bank-statement line link to one payment, while the customer has a single batch debit covering ten payment records. If that is a common, well-defined record relationship, the product should probably handle it. Writing a similar script at every customer site gives buyers a pile of project patches rather than software that can keep improving.

The third is the company's own business practice: who approves a purchase above a certain amount, which orders can move before the paperwork is complete, or which budget pays for a particular expense. If an old ERP encodes progression as program branches, each difference becomes customer-specific code. Each branch turns one company instruction into software that must be tested, upgraded, and explained later.

Mix the three together and a supplier can offer a vague promise: “Our FDE will handle it on site.” The customer cannot tell whether they are buying integration work, waiting for a product feature, or signing up to maintain their own code fork.

Temporary scripts are particularly easy to mislabel as permanent solutions. A conversion program written the night before launch may be acceptable for one import. If it moves documents every month afterward, it needs monitoring, failure handling, and an owner. Much of what is “quickly solved on site” becomes expensive after the team leaves. Calling it development, extension, or deployment does not create a maintenance plan.

## SAP does not pretend software covers everything

Mature products have extensive standard features and configuration. Serious implementation also means recognizing when extension is needed. [SAP's official learning material](https://learning.sap.com/courses/sap-s-4hana-cloud-private-edition-transportation-management/exploring-how-to-make-extensions-clean-core-compliant), for example, discusses custom or extension development when standard features and configuration cannot meet a need, along with the maintenance complexity that extensions introduce.

That does not mean every SAP project needs an on-site developer. Some customers fit the standard process; some differences are configurable; others need extension. The narrower point is enough: even a strong traditional ERP has a formal place for extension. How can a fashionable job title make on-site development disappear?

When a vendor says, “We'll send an AI-savvy FDE and take care of it,” ask what the person will actually do. If they are writing a unique approval branch, the customer should know where the code lives, who tests it, who maintains it, and how it survives a product upgrade. That is a development agreement, not magic deployment.

There is a worse kind of “no development” too: make the customer change how it runs the business. If software supports only one fixed approval line, the vendor may persuade the customer to squeeze real budget ownership, substitute approvers, and exceptions into that line. The project goes live; the company has reorganized a working process to suit the software. Zero customization is not necessarily cheaper than honest on-site development.

## AI does not erase interfaces

The AI era does offer another design. Software keeps documents, amounts, states, approvals, and permissions accurately. An Agent reads the company's natural-language rules and the current facts, then judges the next step. Many differences that previously required customer-specific branches can be handled without changing product code.

But the product must actually do its recording job. Order lines must sum correctly. Payments must not be executed twice. Inventory reservation must be distinct from physical shipment. Permissions must not be a matter of an Agent's guess. If these foundations are missing, the on-site person still has to build them, even if they should have been in the product already.

Consider “urgent orders can go first.” An Agent can read the sentence. It cannot choose, on the company's behalf, who labels an order urgent, how far it may proceed, when evidence must be supplied, or who resolves a dispute. The person on site must surface these questions and get an authorized answer before saving a rule. A new external connection still takes engineering. A change to the record structure cannot be papered over with a prompt.

So “no on-site development” is a conditional claim about product capability, not a benefit included with the FDE title. A product mature enough to let people deploy rather than invent on site needs dependable records, interfaces, permissions, auditability, and a way to hold changing business rules. If it lacks these, say clearly that development remains.

## Do not let an acronym sign the delivery schedule

At contract time, a customer can ask for a plain list: standard features, configuration, integration engineering, customer-specific development, and capabilities intended to return to the product. Who owns each item? How is it accepted? Who fixes it after an upgrade? The person's business card—FDE, implementation consultant, or developer—does not change those questions.

On-site development was normal work in the traditional era. There is no shame in naming it. What deserves criticism is using on-site code to patch product holes while pitching “AI-native delivery through FDE deployment.” Call Development Deployment and the budget, risk, and maintenance are still there, merely filed in a nicer-sounding drawer.

I would rather hear a supplier say, “This is standard, this is a one-off integration, that gap needs a product release, and this unusual rule will remain a human decision for now.” It sounds less impressive than “universal FDE,” but the customer knows whom to call when the schedule slips and who will own the next upgrade. Being able to draw that boundary is itself a delivery skill.

In Oryh, we try to hold the line more firmly: software records facts and enforces amounts and permissions; Agents judge business logic. One bank debit matching several payments is a record-capability problem, so we changed the product and checked the sum in code. How a company approves those payments is a business judgment for an Agent reading its rules. That distinction does not guarantee zero development on site. It does let the customer see whether today's work is deploying an existing capability or paying for software still to be built.
