# Varo Bank

Varo Bank is a mobile-first, FDIC-chartered digital bank offering fee-free checking and high-yield savings accounts, early direct deposit, instant cash advances, a credit-builder Visa card, and a personal line of credit. Founded as Varo Money and operating as Varo Bank, N.A., it became the first consumer fintech company to receive a national bank charter in the United States (2020).

## Products

- **Varo Bank Account** — Fee-free checking with early direct deposit (up to 2 days), 55,000+ free Allpoint ATMs, cashback rewards, and cash deposits at 7,500+ CVS locations.
- **Varo Savings Account** — High-yield savings at up to 5.00% APY on the first $5,000; 2.50% APY above that threshold.
- **Varo Advance** — Short-term cash advances from $20–$500 with a flat fee (no interest), repaid on next direct deposit.
- **Varo Personal Line of Credit** — Up to $2,000 with a single flat fee, no interest, no late fees, repayment terms up to 12 months.
- **Varo Believe** — Secured Visa credit-builder card with no annual fee or interest; reports to all major credit bureaus.

## API Architecture

Varo does not offer a public developer API. Internally, Varo runs a federated GraphQL supergraph powering 9+ subgraphs and 88+ microservices, processing over 500 million monthly requests. Third-party integrations and consumer data access are available via Open Banking aggregators such as Plaid, which Varo uses natively to let customers link external accounts and export Varo data to external financial apps.

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
