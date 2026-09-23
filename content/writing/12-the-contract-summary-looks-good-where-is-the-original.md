# The Contract Summary Looks Good. Where Is the Original?

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 12*

While building the contract module, we put a payment clause into a test: 30% within three working days of signing, 60% before the first shipment, and the remaining 10% after acceptance.

The summary beside it read: “30% deposit, 60% before shipment, 10% after acceptance.” Nice and clear.

But what if the next question is how long we have to pay the deposit? Or whether the shipment condition refers to every shipment or the first one? The summary has dropped details that matter to the next decision.

We use this test example to work through the boundary of contract records: an agent can help people understand an agreement, but the software shouldn't retain only the agent's interpretation.

## Keep the original, the excerpt, and the interpretation separate

We separated those layers.

PDFs, scanned pages, and Word files are stored as attachments linked to the contract. The agent reads them with its own tools, using OCR for images when needed. The extracted text is saved too, so it can be searched later. Oryh itself doesn't run OCR or interpret the agreement for the agent.

The agent then copies passages about payment, delivery, acceptance, and other terms verbatim, recording the source file, page, and clause number. Its explanation goes in a separate summary. The contract's wording and the agent's reading can be consulted together.

This also addresses a practical difficulty. Rereading dozens of pages whenever someone asks about payment is slow, and each pass can miss something different. Now the agent can look up the payment clauses first and return to the original when verification is needed.

The division is straightforward: software records; agents handle business logic. The software keeps the material and its location. The agent extracts it, interprets it, and judges whether the available material is enough to answer the question.

## A payment condition doesn't establish that payment is due now

“Pay the balance after acceptance” is a condition in the contract. Whether acceptance has actually happened is a question for the business records. Who needs to confirm the next step comes from the company's rules.

The agent brings those materials together and advances the work. It might notice a missing acceptance record, ask the person to clarify, or prepare the points that need confirmation. Recording “10% after acceptance” doesn't cause the backend to generate an automatic payment rule.

We also put operating instructions into the contract and payables Skills: read the relevant clauses before answering or acting, rather than trusting conversation memory; preserve the wording verbatim and keep the interpretation separate.

If a clause lookup finds nothing, a “usual” condition must not fill the gap. The passage might not have been extracted, or the contract might genuinely say nothing about it. When further investigation is needed, search the extracted text, then return to the original file. If uncertainty remains, say so.

## Correcting an interpretation isn't changing an agreement

If the summary omitted “three working days,” the summary can be corrected. If the parties sign a supplement, its content shouldn't overwrite the earlier agreement.

Supplements and renewals get new contract records linked to the original, each with its own files and clauses. The next agent can then see both the earlier agreement and the later change.

The current code uses contract status to restrict edits to agreement fields, such as amounts, and to line items. Those are frozen after signing. Summaries, notes, and extracted clause records are not all locked down. So we cannot broadly claim that signing makes every piece of text in the system immutable. The distinction between maintaining an excerpt and changing an agreement still needs to be respected by the agent.

Likewise, code can check whether a clause's linked file belongs to the same contract. It cannot prove that the agent copied the text correctly, selected the right page, or retained every condition in its summary. Our tests verify that the original file can be retrieved and that a clause lookup returns its wording, summary, and page together. Whether the content was read correctly still requires checking against the source and, where needed, human review.

What matters to us in this iteration is whether, when someone asks “Why did you decide that?”, the agent can take them back to the material. When the software preserves the evidence, the agent's judgment can be checked, corrected, and used to continue the work.
