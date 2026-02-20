
## Functional Requirements

- Add an expense
- View expenses
- Update an expense
- View balances (who owes whom)
- Simplify debts

## Supported Split Types

- **EQUAL** — split equally
- **EXACT** — exact amount per user
- **PERCENT** — percentage-based split
    

## Assumptions

- Currency specified per expense
- Decimal precision up to 2 places
- Balances can be negative
- Expense creator is included
- Creator is the default payer
    

## Out of Scope

- User authentication & authorization
- UI / frontend
- Real payments / gateways
- Persistence (DB)
- Notifications / reminders


### Entities

User -> Represent person in the system
Expense -> represent shared expense for user
Split -> represent split for a particular expense 
SplitType -> Equal, Exact, Percent
Balances -> paidBy, paidTo, amount (can use Map<String, Map<String, double>> balances)


