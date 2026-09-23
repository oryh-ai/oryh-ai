# One Bank Debit, Ten Payment Records

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 14*

Pay ten people and the system may hold ten individual payment records, while the bank statement shows a single debit. A supplier payment run can have the same shape.

Our original payment link could point to only one record. Linking the bank debit to one person's payment didn't explain the other nine. Leaving it in the reconciliation queue didn't mean the money hadn't gone out. Our record structure couldn't express what had happened.

That reminded us of something basic about “software records”: the records have to accommodate the actual event. An agent shouldn't have to imagine ten bank transactions just to fit an interface.

## First, record the one-to-many relationship

The payments could already share a batch reference. We allowed a bank-register line to link to that reference, identifying the whole batch. Each person's payment remains separate, and the bank's single line stays a single line.

We didn't build another batch-approval workflow to do this. The missing piece was a relationship between records. Finding that relationship, deciding when to confirm it, and investigating differences remain work for the agent.

Code handles the definite checks: the batch must exist, every payment must move money in the same direction as the bank line, and the amounts must add up. A line cannot link to both an individual payment and a batch at once.

Our test uses three small amounts: 300, 200, and 150, totaling 650. Linking them to a debit of 650 succeeds. A debit of 640 is rejected, with the payment count, total, and difference of ten returned. Linking the same outbound batch to an incoming bank transaction is rejected too.

We want an error to help the next step happen, rather than merely say “matching failed.”

## The person shouldn't have to know the batch number

Once the interface could represent the relationship, the agent still needed to know how to use it.

Someone might simply say, “That debit is the salaries.” They may not remember a batch number, and they shouldn't need to learn a field name before the agent can help.

We later updated the Skills on both sides. The agent recording payroll payments uses a consistent batch reference and states it in the read-back. An agent reconciling the bank line can look for payments recorded as paid near the debit's date, group them by reference, calculate the totals, and propose a candidate even when no batch number was supplied.

The proposal should be expressed in business terms: how many payments, their total, whether the dates and descriptions fit, and which bank debit will be linked. After the person confirms, the agent saves the relationship.

An equal amount is a useful search clue and a necessary check here. It isn't all the evidence. If two batches happen to total the same amount, the agent still needs the bank receipt, dates, and payment details. Handling business logic includes recognizing when there isn't enough information to decide.

## Explain the difference; don't erase it

A difference of ten could mean the wrong batch, incomplete records, a returned payment, or a charge. The software doesn't guess which. Nor should the agent label it a “bank fee” just to get a request accepted.

A separately listed bank charge is recorded as a fee transaction, supported by the actual material. When evidence is missing, investigate further or bring the difference to the person. The current batch link requires matching totals. It isn't a reconciliation engine that automatically handles every fee, return, and split.

The bank line's amount cannot be edited while linking it, either. A relationship can be corrected or cleared, but “our explanation changed” must not become “the bank originally debited a different amount.”

Once linked, the line leaves the unlinked queue. We don't store a separate “reconciled” switch; the list is derived from the relationships. Leaving that list means an explanation has been recorded, not that the agent's judgment is beyond review.

The division we refined here is concrete: software records the bank facts, payment facts, and their relationship, enforcing direction and amount checks. The agent finds evidence, explains differences, organizes confirmation, and advances the records. Connecting one debit to ten payments takes both sides doing their part.
