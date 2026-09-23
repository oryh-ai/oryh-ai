# ORYH

ORYH is an AI-native OA/BPM platform. The business logic does not live in the
server — it lives in the Skills an agent loads on behalf of a person, and the
server records what actually happened.

## Running it yourself

The **[user manual](manual/index.md)** covers the self-hosted product end to
end: [install it](manual/install.md), [take the credentials printed on first
boot](manual/first-boot.md), [connect an agent](manual/connect-agent.md),
[load the company's records](manual/workspace.md), and [keep it
running](manual/operations.md).

```bash
git clone https://github.com/AIE-enginehub/Oryh.git
cd Oryh
docker compose up -d --build
```

The open core is Apache-2.0 at
[AIE-enginehub/Oryh](https://github.com/AIE-enginehub/Oryh).

## Writing

*When agents start operating a business* — a series on where this came from
and why it is shaped the way it is.

1. [It Started with a Timesheet](writing/01-it-started-with-a-timesheet.md)
2. [What If the ERP User Is an Agent?](writing/02-when-agents-use-erp.md)
3. [Software Keeps the Records. Agents Handle the Logic.](writing/03-software-records-agents-decide.md)
4. [Why Company Rules Shouldn't Become a Pile of `if` Statements](writing/04-why-rules-should-not-be-if-statements.md)
5. [Workflow Position Isn't a Status](writing/05-workflow-position-is-not-a-status.md)
6. [An Agent Can Disappear. The Work Can't.](writing/06-an-agent-can-disappear-the-work-cant.md)
7. [Why Do We Need a Flow Runner?](writing/07-why-we-need-a-flow-runner.md)
8. [Who Actually Took This Step?](writing/08-who-actually-took-this-step.md)
9. [The API Exists. Why Does the Agent Still Get It Wrong?](writing/09-the-api-exists-why-does-the-agent-still-get-it-wrong.md)
10. [When Product Names Don't Match, Don't Guess](writing/10-when-product-names-dont-match-dont-guess.md)
11. [We Gave the Agent Custom Objects. It Bypassed the Business Model](writing/11-custom-objects-bypassed-the-business-model.md)
12. [The Contract Summary Looks Good. Where Is the Original?](writing/12-the-contract-summary-looks-good-where-is-the-original.md)
13. [A Material Shortage Is Not a Purchase Decision](writing/13-a-material-shortage-is-not-a-purchase-decision.md)
14. [One Bank Debit, Ten Payment Records](writing/14-one-bank-debit-ten-payment-records.md)
15. [Why “Days of Leave Left” Isn't a Field](writing/15-why-days-of-leave-left-isnt-a-field.md)
16. [Reserved Stock Hasn't Left the Warehouse](writing/16-reserved-stock-hasnt-left-the-warehouse.md)
17. [We Marked a Customer as a Dealer. What Happens Next?](writing/17-we-marked-a-customer-as-a-dealer-what-happens-next.md)
18. [Why Can't Customization Start With a Sentence?](writing/18-customization-starts-with-a-sentence.md)
19. [A New Order Channel](writing/19-a-new-order-channel-doesnt-need-a-new-workflow-engine.md)
20. [Add One Rule. Why Did the Others Disappear?](writing/20-add-one-rule-dont-replace-the-rest.md)

Outside the series:

- [ERP for the AI Era Needs a Rewrite, Not an Agent Add-on](writing/ai-era-erp-needs-a-rewrite.md)
- [ERP and CRM Are Fading into the Background](writing/ai-native-erp-crm-market.md)
- [An Ontology Starts Aging the Day It's Built](writing/an-ontology-ages-from-the-day-its-built.md)
- [Stop Worshipping Ontology](writing/facts-before-relationship-labels.md)
- [We Still Struggle with Objects. Why Bet Enterprise AI on an Ontology?](writing/if-we-cant-get-objects-right-why-build-ontology.md)
- [Ontology Isn't the Foundation of Enterprise AI](writing/ontology-is-not-the-foundation-of-enterprise-ai.md)

## Design notes

The reasoning behind the modelling — capabilities and Skills, the device flow,
and one note per business object — ships with the code rather than living here:
[`docs/`](https://github.com/AIE-enginehub/Oryh/tree/main/docs) in the
repository. The API documents itself at `/redoc` on any running deployment.
