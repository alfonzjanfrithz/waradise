# Waradise

Seed for an online store. The open-source commerce engine is [Medusa](https://medusajs.com) (TypeScript): product catalog, cart, checkout, and admin API. A Next.js storefront sits in front of it.

`index.html` is only a hello-world placeholder so this repository has a default branch. Cloud agents clone a branch; an empty GitHub repo has nothing to clone.

The Medusa app itself should be scaffolded by a Cursor cloud agent (see below), not committed by hand from a laptop, so the cloud run is the proof of concept.

## Scaffold the store with a cloud agent

After GitHub is connected in Cursor and the account can run Cloud Agents:

1. Open [cursor.com/agents](https://cursor.com/agents).
2. Select `alfonzjanfrithz/waradise` and the `main` branch.
3. Paste this prompt:

```text
Scaffold a Medusa v2 online store in this repo.

Use the official create-medusa-app flow (current Medusa v2, not v1).
Include the Next.js storefront. Use PostgreSQL.
Replace the placeholder index.html; do not leave a second competing storefront.
Add a short README section: how to start Postgres, the Medusa backend, and the storefront locally.
Open a pull request. Do not push to main.
```

4. Review the pull request the agent opens. Merge it when it looks right.

Cloud Agents and Automations need a plan that includes them (Premium, Teams, Enterprise, or a legacy paid plan). Free and Plus do not run them. Docs: https://cursor.com/docs/cloud-agent
