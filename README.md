# Budget Bouncer

**What default per-user spend cap should an AI gateway ship with once every business user can call models?**
A Monte Carlo decision prototype from **APM Lab** by Shriya Shekatkar (UCLA · Stats 102C Monte Carlo Methods).

- **Live demo:** https://shriyashekatkar25-byte.github.io/budget-bouncer/
- **Gallery:** https://shriyashekatkar25-byte.github.io/apm-lab/

## The launch that inspired it

On **Oct 15, 2026**, Databricks' platform release notes announced that *consumer access to query Unity Gateway services is generally available*: users with the consumer access entitlement no longer need an account admin to enable a preview. The notes say this may increase model traffic, and that admins can limit it with budgets, rate limits, or by turning off direct model access.
Source: [Databricks platform release notes, October 2026](https://docs.databricks.com/aws/en/release-notes/product/2026/october)

## The PM decision

Imagine I'm the PM for the gateway. Thousands of analysts and business users just got model access. **Which default per-user monthly cap should a newly opened workspace come with?**

- **Customer problem:** an admin wants everyone to try AI, but she owns the bill, and a few heavy agent builders can outspend hundreds of casual users.
- **Success metric:** monthly active AI users per entitled user, with the org's P90 monthly bill inside budget.
- **Guardrails:** users hitting the cap ≤ 3% · power users capped ≤ 25% · P(bill > budget) ≤ 10% · cap-related tickets ≤ 1 per 100 users.
- **Stakeholders:** workspace/account admins, business users, agent builders, FinOps, Support, gateway engineering, model partners.

The page simulates 300 months for up to 5,000 users, sweeps 12 candidate caps, picks the cheapest default that keeps the user-side guardrails green, and writes a director memo (plus a one-sentence VP summary) that updates with every run.

## What this shows about product judgment

| Databricks APM skill | Where it shows up |
|---|---|
| Customer problem framing | Admin-owns-the-bill problem, personas, and guardrails that protect the users who create the most value |
| Prototyping | Interactive single-file simulator with seeded runs, a cap sweep and a self-writing memo |
| SQL / Python | Illustrative SQL for per-user monthly spend and Python that fits a 3-persona mixture and replays the sweep |
| Data-driven decisions | Recommendation chosen from the guardrail table, not intuition; flags when the budget, not the cap, is the real problem |
| Clear writing | Director memo: decision, evidence, risks, rollout plan, next step, one-line VP summary |

## Methods (Stats 102C)

| Method | Chapter | Used for |
|---|---|---|
| Mixture sampling (pick a component, then sample) | Ch5 Composition | Casual / regular / builder personas |
| Discrete sampling by partitioning [0,1] | Ch3 Inverse CDF | Assigning each user a persona from cumulative weights |
| Box-Muller normals → lognormal spend | Ch5 Composition | Per-user monthly spend with a long right tail |
| Convolution (sum of random variables) | Ch5 Composition | Org bill = sum of capped spends, with a shared monthly shock |
| Monte Carlo percentiles from a seeded RNG | Ch1 | P50/P90 bill, P(over budget), share of users capped |

## Design baseline

Four pins from Shriya's Pinterest home feed were used as design input. Everything was redrawn in SVG/CSS/canvas, and no pin images are used.

- **Hero** ← [saffron book-cover pin by Sivakumar Surampudi](https://www.pinterest.com/pin/543246773814121440/): saffron field (#E8643A), cream, sky blue and gold, bold black brush linework, and big watchful eyes (redrawn as generic eyes above a spend meter).
- **Cards & buttons** ← ["Don't be so hard on yourself" doodle by Simply_Flo](https://www.pinterest.com/pin/788200372329260114/): cobalt speech-bubble blue, tomato red, peach, leaf green and blossom pink, with wobbly thick black outlines and hand-lettered caps.
- **KPI badges** ← [oval rabbit sticker saved by Arleth](https://www.pinterest.com/pin/395964992262896811/): powder-blue oval stickers with a parchment center, cocoa outline, ribbon banners and a white die-cut border.
- **Simulation room** ← ["2026 Career" collage](https://www.pinterest.com/pin/732116483227898155/): dark dashboard tiles, contribution-grid greens and neon purple, laid out as a collage.

---

Unofficial concept prototype by Shriya Shekatkar. All data is simulated. Not affiliated with any company.
