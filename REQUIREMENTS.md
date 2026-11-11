# PayPal AI Hackathon — Requirements (researched 11 Nov 2026)

Source: Official Devpost page https://paypalaihackathon.devpost.com/ and Official Rules
https://paypalaihackathon.devpost.com/rules — fetched live 11 Nov 2026 ~14:00 IST.
Cross-checked against secondary coverage (Reconscribe, The Gen AI Magazine) — consistent.

## At a glance

| Item | Official value |
|---|---|
| Name | PayPal AI Hackathon — "Build what's next with PayPal and AI" |
| Sponsor / Admin | PayPal Inc. / Devpost, Inc. |
| Format | Global, online, Devpost |
| Submission period | Thu 1 Oct 2026 9:15am PT – **Thu 12 Nov 2026 12:00pm PT** |
| Deadline in India | **13 Nov 2026, 01:30 IST** (12 Nov 20:00 UTC) |
| Judging | 1–15 Dec 2026 · Winners ~21 Dec 2026 |
| Prizes | $67,500 cash + $2,250 Render credits = **$69,750 headline** (23 prizes) |
| Entry fee | Free. No purchase necessary |
| Who can enter | Age of majority, solo / team (any size) / organisation |
| India eligible? | **Yes.** Excluded only: Brazil, Quebec, Russia, Crimea, Cuba, Iran, North Korea + comprehensively OFAC-sanctioned places |

## Themes / tracks — there are NONE

> "There are no prescribed problem statements and no set of tracks. Build an agent, an app,
> an automation, a new payment experience, a business tool, a social product, or something
> we haven't thought of yet."

The **only fundamental requirement**:

> **Your project must meaningfully use both PayPal and AI.**

Special / honourable-mention awards reward angles without being formal tracks:
Best Use of PayPal + AI ($5,000), Best Use of Agentic Commerce ($5,000), Most Creative
($5,000), Most Impactful ($5,000), Best Demo Delivery ($5,000) — plus sponsor prizes for
AG Grid, APIMatic, Bryntum, Channel3 and Render (optional; not required).

## What to build (Project Requirements)

Build or update an application that:

1. **Integrates the PayPal developer platform using the free sandbox environment**, plus
   an AI tool / model / platform of your choice. "PayPal" includes Venmo, Braintree, Xoom,
   Zettle, etc., but the core PayPal APIs are the expected route.
2. Meaningfully integrates **at least one** PayPal technology / API / SDK / product.
3. Meaningfully incorporates AI into the experience or functionality.
4. Is a **working prototype / proof of concept** — a design mockup, static prototype or
   non-functional demo **does not** meet the requirement.
5. Is sufficiently documented for judges to understand and evaluate it.
6. New projects, or existing projects **significantly updated** during the submission period.

Optional sponsor tools (welcome, **not** required): AG Grid, APIMatic, Astropods, Bryntum,
Channel3, Elastic, KERNEL, Postman, Render, Zapier. Any AI tool works "as long as PayPal
integration is central to the project."

## Is a real PayPal API / sandbox integration mandatory or optional?

**Mandatory in substance.** Official wording (both the overview and §4 of the rules):

> "Entrants must build or update an application that integrates the PayPal developer
> platform (**using the free sandbox environment**) along with an AI tool, model, or
> platform of their choice."
> "To access the PayPal sandbox environment, use your existing PayPal account or create a
> free account at developer.paypal.com."

Stage One judging is an explicit pass/fail check that the project "reasonably applies the
required APIs/SDKs featured in the Hackathon." A project with no PayPal integration at all
fails Stage One.

**Practical implication for this entry:** we have no PayPal developer sandbox credentials
on file for the entrant, and inventing credentials is not allowed. PayPilot therefore:

- implements the **full PayPal Checkout + Invoicing flow as a clearly-labelled sandbox
  simulation** (create order → buyer approves → capture; invoice → send → paid), with the
  exact production integration points stubbed in code and documented (see README →
  "Going live with the real PayPal sandbox");
- maps every simulated step 1:1 to the real PayPal Orders v2 API / Invoicing API calls, so
  swapping in a real sandbox `client-id` is a config-only change;
- states this honestly in the Devpost description and README. Judges can run the complete
  end-to-end flow with zero setup, which the rules explicitly allow ("Your project does not
  need to be publicly hosted… judges must be able to actually run or interact with a working
  build").

Residual risk (flagged for the parent): a strict Stage One reviewer could score the
Technological Implementation criterion lower for a simulated vs. live sandbox call. The
mitigation is transparency + the documented, code-level integration stubs. If the entrant
creates a free developer.paypal.com sandbox app before submitting, the parent can drop the
client-id into `index.html` (`PAYPAL_CONFIG` block at the top of the script) and the same
file calls the real sandbox with no other changes.

## What to submit (Submission Requirements — §4)

All of the following, via the "Enter a Submission" page on Devpost before the deadline:

1. **Project** — built with the required tools, meeting the requirements above, functioning
   as depicted in the video and described in the text.
2. **Text description** — explains the project's features and functionality (Devpost project
   story: problem / what it does / how it was built).
3. **Functional demo** — judges must be able to run/interact with a working build, via
   EITHER clear, complete setup + run instructions in the repo OR a hosted demo URL.
4. **Tools statement** — identify which AI tools / models / services were used and explain
   how they were used in the project (separate required field).
5. **Public code repository** — on GitHub, GitLab or Bitbucket:
   - contains all source code, assets and instructions needed to run the project;
   - **public and open source, with a licence file detectable/visible at the top of the
     repo (About section)** — this repo ships an MIT `LICENSE` for that reason.
6. **Demo video**:
   - **under 3 minutes** (judges are not required to watch past 3:00);
   - shows the project functioning on the device it was built for;
   - uploaded to **YouTube, publicly visible**, link pasted on the submission form;
   - no third-party trademarks or copyrighted music/material without permission.
7. All submission materials in **English** (or with English translations).

Standard Devpost form fields the parent will also need: project name, tagline/elevator
pitch, "Built with" tags, repo URL, demo/live URL, video URL, screenshots/images for the
project gallery (Devpost requires at least a thumbnail; screenshots strongly recommended),
and the hackathon-specific questions incl. the AI-tools statement above.

## Judging criteria (Stage Two — five equally weighted)

1. **Technological Implementation** — how thoroughly/skillfully PayPal + AI are used;
   genuine effort, working, non-trivial implementation.
2. **Design** — complete, coherent product experience, not just a technical PoC.
3. **Potential Impact** — credible, specific case for a real problem for a real audience,
   addressed by what's actually demonstrated.
4. **Innovation / Idea** — creative, novel, different from existing concepts.
5. **Presentation** — video demonstrates the project end-to-end; pitch communicates the
   problem, who it's for, and why it matters; easy to follow.

## Prize structure

- Grand: 1st $12,000 · 2nd $8,000 · 3rd $5,000
- Honourable mentions ($5,000 each): Most Creative · Most Impactful · Best Demo Delivery ·
  Best Use of PayPal + AI · Best Use of Agentic Commerce
- Sponsor: AG Grid $5,000/$2,000/$1,000×3 · APIMatic $1,000×3 + subscription ·
  Bryntum $1,000×3 · Channel3 $1,500 · Render $1,000/$750/$500 in credits
- A project can win at most one Grand *or* Honourable Mention prize + one Sponsor prize.

## Other rules that matter

- Multiple submissions allowed, each must be unique/substantially different.
- Submission must be the entrant's original work; open-source components allowed under
  their licences.
- Project must be available free, without restriction, for judging until the judging
  period ends; include any test credentials / sandbox details needed in the README.
- Drafts can be edited on Devpost until the submission period ends; no changes after.
