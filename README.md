# Migrating off OpenHands: an open-source CompanyOS for work that leaves the repo

Kortix is the open-source CompanyOS: an agent team that runs company work while people verify, steer and govern it. This repository is a migration worksheet for a team that adopted OpenHands for coding agents and now needs the same agents to handle work that never becomes a pull request.

OpenHands is a self-hosted developer control center for coding agents and automations. It runs OpenHands, Claude Code, Codex, Gemini, Pi, OpenCode or any ACP-compatible agent across local, remote and cloud backends (OpenHands README, checked 2026-10-13). If every task you have ends in a commit, it fits. When the work moves into contracts, research, reporting, support and operations, the shape of the system has to change.

## What changes when the company is the user

| Question | OpenHands | Kortix |
| --- | --- | --- |
| Who is the user? | A developer with a repository | A company with a config repository of agents, skills, tools, triggers and connectors |
| Where does work happen? | A coding session on a machine | One isolated sandbox per session, each with its own machine and branch |
| How does work reach `main`? | You push a branch | Through a change request; merge is default-deny for agents |
| Who may act? | Tool permissions on the machine | Per-resource permissions for people and agents, roles, groups, and an audit trail |
| How do company systems get reached? | Custom code and keys in the environment | Connector credentials are brokered server-side and never enter the machine; 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP |
| Which models? | Your own keys per backend | Any model provider with your own keys, or the ChatGPT plan you already pay for |
| Where does it run? | Self-hosted, or OpenHands Cloud | Kortix Cloud, your VPC, or your own on-prem network; self-host is free |

## The five-step migration

1. **Inventory the work, not the code.** List the recurring jobs the team already does (weekly reporting, contract review, inbound triage, research briefs). Those are the jobs that justify a company system; coding tasks stay wherever they are.
2. **Move the agent behaviours.** An agent is one markdown file (behaviour) plus one block in `kortix.yaml` (governance). Your OpenHands agent configs become `agents/<name>.md`, and the things they may touch are declared in `kortix.yaml`.
3. **Set permissions before anyone runs anything.** Start restrictive: per-resource permissions for people and agents, with roles and groups. Approval gates are off until you set them, and merge to `main` is default-deny for agents.
4. **Connect the systems.** A connector beats a hand-rolled tool call: credentials are brokered server-side, so no key lands in the sandbox. Connect the systems the inventory named first, then add MCP or raw HTTP for the rest.
5. **Run one workflow beside the old one for a week.** Keep the OpenHands setup alive until one company workflow has run end to end, with a person verifying its output. Then retire the duplicate.

## Pricing, as published

- Free: $0 with 500 credits per month and 1 project.
- Credits: choose a monthly amount; 5,000 credits a month is $50, and members are unlimited and free.
- Self-hosting Kortix is free; Enterprise adds Cloud, VPC or on-prem deployment (contact Kortix).
- OpenHands publishes its own tiers on its pricing page; OpenHands Cloud's free tier caps conversations per day, and its self-hosted path is free.

## Sources

- Kortix: https://kortix.com (the open-source CompanyOS; 20,000+ GitHub stars on https://github.com/kortix-ai/suna, read it, fork it, audit it)
- OpenHands: https://github.com/OpenHands/OpenHands and https://www.openhands.dev/pricing
- The full comparison: https://openhands-alternative.com/openhands-vs-kortix
- Self-hosting an agent platform you own: https://openhands-alternative.com/self-hosting
- What each option costs per month: https://openhands-alternative.com/openhands-pricing
- Is OpenHands open source, and what that means for a company: https://openhands-alternative.com/is-openhands-open-source
- Kortix vs OpenHands, in full: https://kortix.com/blog/kortix-vs-openhands
- Migration notes that are not in this file live in the issues tab; open one if your stack does not fit the five steps.

## More of the decision

- [Which open source coding agent fits best](https://openhands-alternative.com/best-open-source-coding-agent) is the five-option comparison to read before a move.
- [OpenHands vs Aider](https://openhands-alternative.com/openhands-vs-aider) is the head-to-head for a team choosing between the two harnesses.
