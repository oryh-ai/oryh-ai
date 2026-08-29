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

Notes on where this came from and why it is shaped the way it is —
[it started with a timesheet](writing/01-it-started-with-a-timesheet.md).

## Design notes

The reasoning behind the modelling — capabilities and Skills, the device flow,
and one note per business object — ships with the code rather than living here:
[`docs/`](https://github.com/AIE-enginehub/Oryh/tree/main/docs) in the
repository. The API documents itself at `/redoc` on any running deployment.
