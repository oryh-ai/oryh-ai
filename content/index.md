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

### Ontology essays

- [Ontology Isn't the Foundation of Enterprise AI](writing/ontology/ontology-is-not-the-foundation-of-enterprise-ai.md)
- [An Ontology Starts Aging the Day It's Built](writing/ontology/an-ontology-ages-from-the-day-its-built.md)
- [Stop Worshipping Ontology](writing/ontology/facts-before-relationship-labels.md)
- [We Still Struggle with Objects. Why Bet Enterprise AI on an Ontology?](writing/ontology/if-we-cant-get-objects-right-why-build-ontology.md)
- [A Million Edges Still Cannot Read a Sentence](writing/ontology/a-million-edges-cannot-read-a-sentence.md)
- [If AI Can Draw the Company's Map, Why Make It Follow the Map?](writing/ontology/if-ai-can-draw-the-map-why-make-it-follow-the-map.md)
- [How Many Objects Are There in One Car?](writing/ontology/how-many-objects-in-one-car.md)
- [A Tire Becomes an Object Today. Who Fixes Yesterday's System?](writing/ontology/when-a-tire-becomes-an-object-who-fixes-yesterday.md)
- [Old Repair Records Have No Tire IDs. Can a New Ontology Invent Them?](writing/ontology/a-new-ontology-cannot-invent-old-tires.md)
- [One “Unless” in the Policy. What Happens to Yesterday's Approvals?](writing/ontology/one-unless-can-undo-yesterdays-answer.md)
- [The Ontology Worked. Then Nobody Dared Change It.](writing/ontology/the-ontology-worked-until-nobody-dared-change-it.md)

### FDE essays

- [Does an FDE Badge Make You an Enterprise AI Expert?](writing/fde/a-new-badge-does-not-make-an-ai-expert.md)
- [Even Mature ERP Needs Extensions. Does Calling Someone an FDE Remove Development?](writing/fde/sap-needs-extensions-a-new-title-doesnt-remove-development.md)
- [Less Customer-Specific Code, More Judgment on Site](writing/fde/less-customer-code-more-judgment.md)
- [Industry Experience Is Not a Model-Operator Certificate](writing/fde/industry-veteran-not-model-operator.md)
- [If You Do Not Know Who Decides, What Exactly Are You Deploying?](writing/fde/you-dont-know-who-decides.md)
- [Can an FDE Bootcamp Teach Industry Experience?](writing/fde/you-cant-train-experience-in-a-bootcamp.md)
- [Can an Ordinary Company Afford a Real FDE?](writing/fde/can-an-ordinary-company-afford-a-real-fde.md)
- [What Pays for a Real FDE on a Low-Bid Project?](writing/fde/low-bid-projects-cannot-grow-real-fdes.md)
- [One Hero Can Save a Project. That Is Not a Delivery Model.](writing/fde/one-hero-is-not-a-delivery-model.md)
- [A Project Manager Is Not an FDE. That Is Fine.](writing/fde/a-project-manager-is-not-a-fde-and-thats-fine.md)

## Design notes

The reasoning behind the modelling — capabilities and Skills, the device flow,
and one note per business object — ships with the code rather than living here:
[`docs/`](https://github.com/AIE-enginehub/Oryh/tree/main/docs) in the
repository. The API documents itself at `/redoc` on any running deployment.
