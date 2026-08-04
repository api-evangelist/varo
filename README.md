# Varo Bank

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Varo Bank is a mobile-first, FDIC-chartered digital bank offering fee-free checking and high-yield savings accounts, early direct deposit, instant cash advances, a credit-builder Visa card, and a personal line of credit. Founded as Varo Money and operating as Varo Bank, N.A., it became the first consumer fintech company to receive a national bank charter in the United States (2020).

## Products

- **Varo Bank Account** — Fee-free checking with early direct deposit (up to 2 days), 55,000+ free Allpoint ATMs, cashback rewards, and cash deposits at 7,500+ CVS locations.
- **Varo Savings Account** — High-yield savings at up to 5.00% APY on the first $5,000; 2.50% APY above that threshold.
- **Varo Advance** — Short-term cash advances from $20–$500 with a flat fee (no interest), repaid on next direct deposit.
- **Varo Personal Line of Credit** — Up to $2,000 with a single flat fee, no interest, no late fees, repayment terms up to 12 months.
- **Varo Believe** — Secured Visa credit-builder card with no annual fee or interest; reports to all major credit bureaus.

## API Architecture

Varo does **not** offer a public developer API or a developer portal. Probes of `developer.`, `developers.`, and `docs.varomoney.com` do not resolve, and `api.varomoney.com` (the private mobile-app backend) returns a Cloudflare origin error. The `varobank` GitHub org has a single archived, non-API public repo. Internally, Varo has described a federated GraphQL supergraph over ~88 microservices, but that contract is not published; the `graphql/` schema in this repo is a conceptual model only.

The only real seam for third-party programmatic access to Varo account data is customer-permissioned open-finance aggregation — most notably a native, documented **Plaid** integration, with data also reachable through MX, Finicity, and Akoya in the broader US ecosystem. Varo publishes no FDX conformance or CFPB Section 1033 data-access developer documentation. See `review.yml` for the full honest assessment.

## Links

- Website: https://www.varomoney.com/
- Help Center: https://support.varomoney.com/hc/en-us
- Blog: https://www.varomoney.com/blog/
- Engineering Blog: https://medium.com/engineering-varo
- LinkedIn: https://www.linkedin.com/company/varobank
- X (Twitter): https://x.com/varobank
- Open Banking Tracker: https://www.openbankingtracker.com/provider/varomoney
- Plaid Customer Story: https://plaid.com/customer-stories/varo/

## APIs.json

This repository contains an [APIs.json](apis.yml) profile (specification version 0.19) cataloging Varo Bank's consumer-facing API surface, pricing, rate limits, and FinOps reference.

Maintained by [Kin Lane](mailto:kin@apievangelist.com) / [API Evangelist](https://apievangelist.com).
