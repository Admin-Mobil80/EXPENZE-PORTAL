# EXPENZE-PORTAL

The Expenze console, served at **expenze.ai**.

Three files, no build step, no framework:

| | |
|---|---|
| `index.html` | the marketing site |
| `login.html` | sign-in |
| `app.html` | the console — submitting, reviewing, settling, reports, policy, people |

`app.html` carries its own port of the policy engine so a reviewer sees a
verdict recompute as they change an expense type. It is a *preview*: what
anybody is actually paid comes from `policy.py` in EXPENZE-BACKEND, and the two
must be kept in step.

## Part of Expenze

* **EXPENZE-PORTAL** — this, what customers use
* **EXPENZE-BMS** — what we run the platform from
* **EXPENZE-BACKEND** — the CDK app, the Lambdas, the policy engine, the tests

The backend deploys this one: its `app.py` points a CloudFront site stack at
`../PORTAL`, so the three check out as siblings under one folder.

## Deploying

From EXPENZE-BACKEND:

```bash
AWS_PROFILE=cloudmeter npx cdk deploy ExpenzeSite
AWS_PROFILE=cloudmeter aws cloudfront create-invalidation \
  --distribution-id E3F4MLCVNAXPPE --paths "/*"
```

Nothing is visible until the invalidation completes.
