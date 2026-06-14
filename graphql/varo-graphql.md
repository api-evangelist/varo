# Varo Money GraphQL Schema

## Overview

This document describes a conceptual GraphQL schema for Varo Money (Varo Bank), a mobile-first, FDIC-chartered digital bank. Varo offers fee-free checking and high-yield savings accounts, early direct deposit, instant cash advances, a credit-builder card, and a personal line of credit. While Varo does not publish a public GraphQL API, this schema represents the data structures and relationships that underpin Varo's consumer banking platform, as accessible through Open Banking aggregators such as Plaid.

**Schema File:** [varo-schema.graphql](varo-schema.graphql)

## Provider Context

- **Provider:** Varo Bank (formerly Varo Money)
- **Type:** Neobank / Digital-only FDIC-chartered bank
- **Primary Products:** Checking, High-Yield Savings, Cash Advance, Credit Builder Card, Line of Credit
- **Third-party Integration:** Open Banking aggregators (Plaid, MX, Finicity)
- **Human URL:** https://www.varomoney.com/
- **Support:** https://support.varomoney.com/hc/en-us

## Schema Summary

### Core Account Types

| Type | Description |
|------|-------------|
| `Account` | Base account interface shared by all Varo account types |
| `CheckingAccount` | Fee-free checking account with debit card and ATM access |
| `SavingsAccount` | High-yield savings account (up to 5.00% APY on first $5,000) |
| `VaroAdvance` | Short-term cash advance ($20–$500) repaid on next direct deposit |
| `CreditCard` | Varo Believe secured credit card for credit building |
| `AccountBalance` | Composite balance model covering available, pending, and actual balances |

### Balance Types

| Type | Description |
|------|-------------|
| `Available` | Funds currently available for spending or withdrawal |
| `Pending` | Transactions posted but not yet settled |
| `Actual` | Settled ledger balance |
| `Savings` | Total savings balance snapshot |
| `SavingsGoal` | Named savings target with progress tracking |
| `SavingsRate` | Current applicable savings interest rate |
| `APY` | Annual percentage yield data including tier thresholds |

### Transaction Types

| Type | Description |
|------|-------------|
| `Transaction` | Base transaction interface |
| `CheckingTransaction` | Debit/credit activity on checking accounts |
| `SavingsTransaction` | Deposits and withdrawals on savings accounts |
| `CardTransaction` | Debit or credit card purchase transactions |
| `TransactionType` | Enumeration of transaction categories (purchase, transfer, deposit, etc.) |
| `Merchant` | Merchant name and identifier associated with a card transaction |
| `MerchantCategory` | MCC-based merchant category classification |
| `MerchantLocation` | Geographic location of a merchant |

### Card Types

| Type | Description |
|------|-------------|
| `Card` | Base card type (debit or credit) |
| `CardDetails` | Full card number, expiry, CVV (tokenized) |
| `CardStatus` | Enum: active, locked, blocked, cancelled |
| `CardType` | Enum: debit, credit, virtual |
| `VirtualCard` | Disposable or persistent virtual card number |
| `CardLock` | Lock/unlock state and reason for a card |

### Payment and Transfer Types

| Type | Description |
|------|-------------|
| `Payment` | Generic outbound payment |
| `Transfer` | Internal or external fund movement |
| `ACH` | ACH pull or push transfer to/from external bank |
| `P2P` | Peer-to-peer instant transfer between Varo users |
| `BillPayment` | Bill payment to a registered payee |
| `BillPayee` | Registered biller (utility, landlord, etc.) |
| `ScheduledPayment` | Future-dated or recurring payment |

### Deposit Types

| Type | Description |
|------|-------------|
| `DirectDeposit` | Payroll or government benefit deposit |
| `Payroll` | Employer payroll direct deposit details |
| `EmployerDeposit` | Single employer deposit event |
| `Benefits` | Government benefit deposit (SSA, unemployment, etc.) |

### Rewards and Cashback

| Type | Description |
|------|-------------|
| `CashBack` | Cashback reward earned on eligible debit purchases |
| `Reward` | Generic reward record |
| `PointValue` | Monetary value of a reward point |
| `VaroExcelerator` | Varo Believe cashback accelerator program tier |
| `ExceleratorStatus` | Current tier and qualifying criteria status |

### Notifications and Alerts

| Type | Description |
|------|-------------|
| `Notification` | Platform notification sent to a user |
| `Alert` | Account alert triggered by a threshold or event |
| `SpendingAlert` | Threshold-based spending notification |
| `DepositAlert` | Direct deposit arrival or large deposit notification |

### Advance (Cash Advance) Types

| Type | Description |
|------|-------------|
| `Advance` | Cash advance record ($20–$500) |
| `AdvanceStatus` | Enum: eligible, active, repaid, defaulted |
| `AdvanceFee` | Flat fee associated with a cash advance tier |
| `RepaymentSchedule` | Repayment terms and expected repayment date |

### Auth and Integration Types

| Type | Description |
|------|-------------|
| `Auth` | Authentication session or token container |
| `Token` | OAuth 2.0 access or refresh token |
| `Webhook` | Registered webhook endpoint for event notifications |

## Key Queries

```graphql
# Retrieve an account by ID
query GetAccount($id: ID!) {
  account(id: $id) {
    id
    type
    status
    balance {
      available { amount currency }
      pending { amount currency }
      actual { amount currency }
    }
  }
}

# List recent transactions with merchant detail
query ListTransactions($accountId: ID!, $limit: Int, $cursor: String) {
  transactions(accountId: $accountId, limit: $limit, cursor: $cursor) {
    edges {
      node {
        id
        amount
        currency
        postedAt
        merchant { name category { name mcc } location { city state } }
      }
    }
    pageInfo { hasNextPage endCursor }
  }
}

# Check cash advance eligibility and amount
query GetAdvance($accountId: ID!) {
  advance(accountId: $accountId) {
    id
    status
    eligibleAmount
    fee { amount flatFee }
    repaymentSchedule { dueDate method }
  }
}
```

## Key Mutations

```graphql
# Transfer funds between checking and savings
mutation TransferFunds($input: TransferInput!) {
  transfer(input: $input) {
    id
    amount
    currency
    fromAccount { id type }
    toAccount { id type }
    status
    createdAt
  }
}

# Lock or unlock a card
mutation SetCardLock($cardId: ID!, $locked: Boolean!, $reason: String) {
  setCardLock(cardId: $cardId, locked: $locked, reason: $reason) {
    id
    status
    lock { locked reason lockedAt }
  }
}

# Register a webhook endpoint
mutation RegisterWebhook($input: WebhookInput!) {
  registerWebhook(input: $input) {
    id
    url
    events
    secret
    createdAt
  }
}
```

## Notes

- This is a conceptual schema derived from Varo Bank's publicly documented product features. Varo does not currently offer a public developer GraphQL API.
- Balance amounts are represented in minor units (cents) with an explicit currency code (ISO 4217).
- Pagination follows the Relay Cursor Connection specification.
- All monetary values use the `Money` scalar (amount in cents + ISO currency code).
- Authentication follows OAuth 2.0 with scopes per product area (accounts:read, transactions:read, transfers:write, cards:write).
- Real-time account data is available through Open Banking aggregator partnerships (Plaid, MX, Finicity).
