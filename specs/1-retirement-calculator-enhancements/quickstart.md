# Quickstart & Testing Scenarios - Retirement Calculator

## 1. Quickstart Verification
After making these single-file enhancements to `FatFIRE_Calculator.html`, you can open the portal directly in any modern Chrome/Chromium, Firefox, or Safari web browser. All animations, slider sync elements, and chart visualizations operate entirely client-side out of the box.

---

## 2. Critical Core Validation Scenarios

### Scenario 1: 2024 Filing Status & Standard Deductions Sync
- **Input Action**: Change Filing Status selection from "Single" to "Married Filing Jointly" (MFJ) inside the tax inputs group.
- **Verification Steps**:
  1. Confirm the Standard Deduction indicator displays exactly `$29,200` (instead of `$14,600`).
  2. Slider inputs correctly handle larger combined sums.
  3. The Federal tax columns recalculate immediately to align with the expanded MFJ tax brackets.

### Scenario 2: Early Withdrawals 10% Penalty Check
- **Input Action**: Adjust the pre-tax Tax-Deferred account drawing priority and start drawing early (e.g., age 50) before 59½ with SEPP disabled.
- **Verification Steps**:
  - Projection row years from age 50 to 59 show the `taxEarlyPenalty` values matching precisely `10%` of the gross deferred drawing sums.

### Scenario 3: Custom Sequencing Withdrawal Priorities
- **Input Action**: Reorder the dragging priority sequence from elements [Taxable → Pre-Tax Deferred → Tax-Free Roth] to [Tax-Free Roth → Taxable → Pre-Tax Deferred].
- **Verification Steps**:
  - Verify the Projection schedule draws Roth balances to `$0` first, before tapping Taxable and Pre-Tax Deferred portfolios.

### Scenario 4: Smile Curve Spending Adjustments
- **Input Action**: Set "Active Expenses to Age 65" to `$250,000`, "Age 66 to 75" to `$200,000`, and "Age 76 to 85" to `$150,000`.
- **Verification Steps**:
  - Verify the "Expenses Required" table column shifts precisely on years crossing these age transitions.
