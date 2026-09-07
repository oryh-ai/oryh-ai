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

Separately, on where the category is going:
[ERP and CRM Are Fading into the Background](writing/ai-native-erp-crm-market.md).

## Design notes

The reasoning behind the modelling — capabilities and Skills, the device flow,
and one note per business object — ships with the code rather than living here:
[`docs/`](https://github.com/AIE-enginehub/Oryh/tree/main/docs) in the
repository. The API documents itself at `/redoc` on any running deployment.
