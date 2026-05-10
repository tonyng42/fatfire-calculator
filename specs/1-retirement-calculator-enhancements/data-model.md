# Data Model Specification - Retirement Calculator Enhancements

## 1. Entities & Structural Schema

All entities reside inside standard JavaScript memory objects.

### `Inputs` Map
Extends basic options with advanced tax options, sequencing priority arrays, Custom Expenses, and SEPP rules.

| Field Name | Type | Description | Validation Bounds |
| :--- | :--- | :--- | :--- |
| `annualExpensesTo65` | `Number` | Spending required from start age up to age 65. | `[0, 10000000]` |
| `annualExpenses66to75` | `Number` | Spending required from age 66 to 75. | `[0, 10000000]` |
| `annualExpenses76to85` | `Number` | Spending required from age 76 to 85. | `[0, 10000000]` |
| `filingStatus` | `String` | IRS Marital Tax filing configuration. | `Single`, `MFJ`, `MFS`, `HoH` |
| `accountPriority` | `Array` | Priority-ordered list for asset drawdowns. | Elements must match valid account names. |
| `seppEnabled` | `Boolean` | Active status of IRS Early Exemption payments. | `true` or `false` |
| `seppStartAge` | `Number` | Age at which user elects to initiate SEPP. | `[18, 59]` |
| `seppMethod` | `String` | IRS compliant Periodic payout algorithm. | `amortization`, `annuitization`, `rmd` |
| `oneTimeExpenses` | `Array` | Set of objects describing large-ticket expenses. | Pushes `{ id, age, amount, label }` arrays. |

### `ProjectionRow` Item
Defines table cells output on each calculated year.

| Field Name | Type | Description |
| :--- | :--- | :--- |
| `age` | `Number` | Target simulation age. |
| `expensesRequired` | `Number` | Derived consumption standard including Smile-Curve curves. |
| `oneTimeSpend` | `Number` | Large ticket item sums hitting target year. |
| `ssOffset` | `Number` | Derived Social Security offset. |
| `grossDrawRequired` | `Number` | Sum needed to clear consumption targets: `Required + OneTime - SS`. |
| `rmdAmount` | `Number` | Mandated annual draw once age criteria >= 75 are met. |
| `niitAmount` | `Number` | Calculated Net Investment ACA IRS Taxes. |
| `taxEarlyPenalty` | `Number` | Derived 10% IRS early penalties. |
| `totalTaxBill` | `Number` | Sum of Fed + State + Local + NIIT + Penalties. |
| `shortfall` | `Number` | Extracted gap between draw capabilities and spends. |

---

## 2. Validation Rules & State Relationships
- **Drawing Validation**: Drawing cannot happen from depleted accounts. Any account balance ending negative forces immediate fallback processing.
- **Priority Sequence Restructuring**: Priority list cannot contain duplicate elements and must contain every eligible account.
