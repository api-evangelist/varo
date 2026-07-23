# Varo Bank

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
