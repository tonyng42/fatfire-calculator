# Specification: Advanced FIRE Calculator Enhancements

## 1. Purpose & User Value

The objective of this feature is to transform the existing FatFIRE Calculator into a fully comprehensive, advanced planning dashboard. The calculator will accurately capture multi-phase retirement expenses (the "Smile Curve" model), advanced tax structures (e.g., Net Investment Income Tax/NIIT, Federal 0% Standard Deduction thresholds, custom filing status thresholds, and Medicare IRMAA warning boundaries), manual withdrawals, age controls, and custom withdrawal account sequencing. 

### User Value Propositions
- **Realistic Spending Projections**: Retirement spending is rarely flat. Users will be able to model the actual "Smile Curve" of high early-retirement spending, lowering mid-retirement spending, and rising healthcare/late-retirement spending.
- **Advanced Tax and Penalty Modeling**: Prevents users from incurring unexpected 10% IRS early withdrawal penalties or pushing themselves into higher NIIT / Medicare brackets.
- **Highly Interactive Exploration**: Provides instantly responsive UI controls for manual numeric entries, hover visualizations of account drawdowns, and specific, actionable suggestions to resolve portfolio shortfalls.

---

## 2. User Scenarios & Acceptance Criteria

### Scenario A: Setting up a Realistic Multi-Stage Retirement Plan (The Smile Curve)
- **Given** the user is aged 52 planning to retire at 55, and wishes to plan for different lifestyle stages (active retirement, slow-down, and elevated late-life health costs).
- **When** the user goes to "Annual Expenses", they see three separate controllable fields instead of one:
  1. **Annual Expenses to 65** (Default: `$200,000`)
  2. **Annual Expenses (66-75)** (Default: Same as "to 65")
  3. **Annual Expenses (76-85)** (Default: Same as "to 65")
- **Then** the math calculations apply each rate to the respective ages in the projection table and graphs.
- **And** an interactive informative icon next to each field provides the background on why spending varies.

### Scenario B: Defining Precise Withdrawal Start Ages & Sequences
- **Given** a user wishes to defer drawing from their Tax-Deferred account until Age 60, while starting Taxable withdrawals immediately upon retirement at 55, and Tax-Free Roth withdrawals at 59.
- **When** the user navigates to the Withdrawals Input controls, they can manually type in their custom start ages for Tax-Deferred and Tax-Free withdrawals, beside their standard manual withdrawal rate entries.
- **And** they can customize the priority ordering of their accounts (e.g., Draw Taxable first, then Tax-Deferred, then Tax-Free, or any custom sequence).
- **Then** the withdrawal simulation honors these parameters precisely. If early drawings from Tax-Deferred accounts (before Age 59 1/2) are requested outside of standard SEPP, a 10% federal early withdrawal penalty is calculated, highlighted and warnings appear in the user's dashboard.

### Scenario C: Accessing Dynamic Hover Breakdown & Rich UI Feedback
- **Given** a user is examining a projected year where their planned retirement income fails to meet their baseline spending.
- **When** the user hovers over the "⚠️ SHORTFALL" badge in the Withdrawn From column of the table, they see:
  1. The precise dollar amount of the shortfall.
  2. A specific suggestion recommending exact percentages and account sources to draw from to eliminate the shortfall, factoring in federal, state, and local tax impacts for the recommendation.
- **When** the user hovers over the main Portfolio chart, they instantly see the specific balance breakdown for each account type (Taxable, Tax-Deferred, Tax-Free, HK portfolios) for the corresponding year.

---

## 3. Functional Requirements

### 3.1 Advanced Dashboard and Visualizations
- **Interactive Portfolio Breakdown**: Chart must display absolute visual values for each account category (Taxable, Tax-Deferred, Tax-Free, Hong Kong) stacked/combined. Activating hover interactions anywhere on the chart must trigger standard tooltip readouts displaying specific amounts for each account category in that year.
- **Adjustable Controls Layout**: Decrease standard size of the icons in the "special adjustments and draws" section to approximately one-quarter of their original dimensions and position them compactly to the side to improve screen space utilization.

### 3.2 Enhanced User Inputs System
- **Manual Number Entry in Comma Format**: Allow users to manually type precise values into all numerical input fields. Any manually typed numbers must automatically be formatted with commas (e.g., `2,000,000` or `200,000`). Numerical inputs and slider rules must stay in immediate real-time synchronization.
- **Custom Account drawing Order Selector**: Provide interactive controls letting users arrange the drawdown hierarchy of Taxable, Tax-Deferred, and Tax-Free accounts. By default, the priority sequence must be: 1. Taxable → 2. Tax-Deferred → 3. Tax-Free.
- **Filing Status selector**: Incorporate a "Tax Filing Status" dropdown input offering options for `Single`, `Married Filing Jointly (MFJ)`, `Married Filing Separately (MFS)`, and `Head of Household (HoH)`. Default must be set to `Single`.
- **Smile Curve Brackets Support**: Replace the single Annual Expenses input field with three age-specific input fields:
  - **Annual Expenses to Age 65**  (Default initial value `$200,000`)
  - **Annual Expenses Age 66 to 75** (Defaults to matching the "to 65" entry)
  - **Annual Expenses Age 76 to 85** (Defaults to matching the "to 65" entry)
- **Ages Start Controls**: Add numerical input fields for users to explicitly type in the specific ages they want to begin normal withdrawals from:
  - Tax-Deferred Accounts
  - Tax-Free Accounts
- **SEPP Withdrawal Automation Options**: Expand the SEPP input control to demand an explicit start age and a selection among three standard IRS-approved calculation methodologies (Amortization, Annuitization, or Required Minimum Distribution/RMD standard calculations).
- **One-Time Large Ticket Items System**: Allow users to specify a counter for a high-ticket one-time spend (e.g., weddings, vacation home) and collect individual details (custom age, custom amount, and custom description label) for each one-time item. These drawings must deplete the Taxable account exclusively.
- **Interactive Diagnostic Info Icons**: Add a visual information icon next to every key system setting field. Hovering over the icon must render a brief, informative explanation of what the parameter controls.

### 3.3 Core Calculation Logic Upgrades
- **Enforced Early Drawing Penalty**: If Tax-Deferred withdrawals occur before Age 59 1/2 (outside of a properly configured SEPP timeline), apply a 10% early withdrawal penalty to the Gross Draw, adding this value to the annual taxes or shortfall logic.
- **Required Minimum Distributions (RMD)**: Implement mandatory RMD rule starting exactly at Age 75. The calculated mandatory distribution amount per year must be withdrawn from the Tax-Deferred accounts and adjusted on the dashboard metrics and in the Projection table. 
- **Qualified Dividends & NIIT Protection Rule**: Tax calculations must support Net Investment Income Tax (NIIT) logic, applying a 3.8% tax surcharge on investment earnings or drawings that exceed the filing-status thresholds (e.g., $200,000 MAGI for Single filers).
- **Federal 0% Tax Threshold Bracket**: Federal tax calculations must factor in a standard $14,600 (Single status) zero-percent margin (Standard Deduction equivalent) before standard income tax brackets apply, ensuring actual federal tax liabilities are realistically low.
- **Shortfall Fallback drawing Logic**: If a planned withdrawal rate for an account is insufficient to reach the required stage expenses, the engine must automatically attempt to draw bypass-limit fallback amounts from another eligible account in the priority sequence to sustain the retiree's lifestyle before declaring a shortfall.
- **Shortfall Advice Calculator Engine**: When a year experiences a cash flow shortfall (meaning all accounts are depleted and cannot satisfy baseline expenses):
  - The system must compute the exact percentage boost or specific account type draws needed to close the gap.
  - The suggestion must proactively calculate and incorporate subsequent Federal, State, and Local tax drag of the newly recommended draw.

### 3.4 Advanced Table Projections Column Additions
- **Red Account Depletion Indicators**: If any account type (Taxable, Tax-Deferred, Tax-Free, HK Portfolio) is depleted to $0 during the plan, its respective cell in the Projection table must turn vibrant red.
- **Sources column detail**: Display exactly what accounts were drawn from and the absolute dollar amount from each account.
- **Actual RMD Column**: A dedicated column showing the annually computed required RMD amount for the Tax-Deferred accounts.
- **Dedicated NIIT Column**: A new column tracking the absolute dollar amount of the 3.8% NIIT limit triggered for the year.
- **Indicators Hierarchy**: Align and center column headers with their corresponding value cells for the sections: `"Annual Cash Flow"`, `"Taxes Paid"`, and `"Withdrawn From"`.

---

## 4. Scope Boundaries

### Included In Scope
- Complete implementation of UI element syncing (type numeric fields inside current HTML + update slider positions).
- Full implementation of RMD rules under standard IRS guidelines at age 75 using standard lookups.
- Dynamic hover tooltip math computing suggested fixes for any shortfall year.
- Complete client-side rendering in FatFIRE_Calculator.html including styling update.

### Excluded From/Out Of Scope
- Multi-state tax modeling outside standard NY State and NYC definitions (will preserve NY State/NYC as primary models, with Filing Status thresholds).
- Live web scraping for standard stock market indexes pre-defined styles (growth rate selections will utilize pre-computed, standard historical averages of the last 30 years defined in standard Javascript variables).

---

## 5. Technical Assumptions & Constraints

### Assumptions
- **Inflation Indexing**: Brackets and fixed IRS limits (Standard deduction, NIIT thresholds) remain in real terms, or grow at the core inflation assumption index to avoid complex historical indexing tables.
- **Single Tax Calculation Standard**: Core federal tax code will focus on the standard deduction limits for the user's chosen Filing Status.

### Constraints
- **Single-File Portability**: The application must remain a 100% self-contained, portable HTML page with inline Javascript and CSS, requiring zero external build processors.
- **Responsive Web Design**: Needs to be visually impressive on standard modern monitors and laptops, using high-contrast typography, modern styling tokens, and seamless layout structures.

---

## 6. Success Criteria

### Technology-Agnostic Measurable Results
- **100% Verification Verification**: All mathematical draw calculations (Standard Draw, Fallback drawing, RMD distributions) in the Projection table must sum to exactly the spending requirement in years with no budget shortfalls.
- **Penalty Enforcement Validity**: Withdrawals scheduled from Tax-Deferred accounts before Age 59.5 without an active SEPP trigger an immediate, correct 10% federal penalty on every year of early drawings.
- **100% Input Synchronization**: Manually entering standard integers into any input text box updates the associated range-sliders instantly within 15 milliseconds and renders the Projection table recalculations under 100 milliseconds.
- **Visual Premium Layout**: Zero overlapping headers or broken columns; centered headers for Cash Flow, Taxes, and Withdrawn From, with Red account depletion markers showing clearly on 100% of mobile and standard desktop viewports.
