# Master Execution Tasks Checklist - Advanced Retirement Calculator Enhancements

## 1. Phase 1: Baseline UI & HTML Structure Audits & Synced Comma Inputs

- [/] [T001] [ ] [Scenario A] Audit `FatFIRE_Calculator.html` and update HTML layout to introduce filing status selection dropdown and three Smile-Curve expense inputs instead of single annual expenses. `FatFIRE_Calculator.html`
- [ ] [T002] [P] [Scenario C] Shrink standard icon scaling sizes in "special adjustments and draws" layout and reorganize them into compact sidebar slots to improve real estate. `FatFIRE_Calculator.html`
- [ ] [T003] [ ] [Scenario B] Add numerical type input boxes next to range-sliders letting users type explicit ages and values directly with live automatic `'input'` sanitization. `FatFIRE_Calculator.html`
- [ ] [T004] [ ] [Scenario B] Integrate dynamic comma-formatting script (`Intl.NumberFormat`) that automatically formats manually entered values in input fields and mirrors update state immediately to range-sliders (updating within 15ms). `FatFIRE_Calculator.html`
- [ ] [T005] [ ] [Scenario A] Add detailed diagnostic info icons (`.info-icon` and tooltip classes) and modern hover descriptions explaining Smile-Curve parameters and other new metrics inputs. `FatFIRE_Calculator.html`

## 2. Phase 2: Core Calculation Engine Enhancements (IRS Rules, Brackets, NIIT, Fallback Draws)

- [ ] [T006] [ ] [Scenario B] Expand internal Global `inputs` and initialization models to capture new parameters: multi-expenses (`annualExpensesTo65`, `annualExpenses66to75`, etc.), custom sequencing priorities array, and custom ages start draw controls. `FatFIRE_Calculator.html`
- [ ] [T007] [ ] [Scenario B] Modify Federal Tax calculation logic to index against 2024 Filing Status Standard Deductions (`Single $14,600`, `MFJ $29,200`, `HoH $21,900`, `MFS $14,600`) and correct corresponding tax bracket limits. `FatFIRE_Calculator.html`
- [ ] [T008] [ ] [Scenario B] Integrate the ACA 3.8% Net Investment Income Tax (NIIT) math into the annual projection system, applying it to portfolio drawings/dividends that exceed the relevant filing status bounds. `FatFIRE_Calculator.html`
- [ ] [T009] [ ] [Scenario B] Implement IRS Required Minimum Distribution (RMD) math starting exactly at age 75 for Pre-Tax deferred accounts using the standard life expectancy tables. `FatFIRE_Calculator.html`
- [ ] [T010] [ ] [Scenario B] Implement the 10% early withdrawal penalty for drawing pre-tax Tax-Deferred accounts prior to 59½, with automated SEPP (amortization, annuitization, and RMD) exception methods. `FatFIRE_Calculator.html`
- [ ] [T011] [ ] [Scenario A] Modify the annual spending schedule in the simulation function to execute the age-bracketed "Smile Curve" consumption parameters rather than any flat line расходы. `FatFIRE_Calculator.html`
- [ ] [T012] [ ] [Scenario B] Implement one-time high-ticket expense ledger inputs where specific age-slotted drawings deplete Taxable account assets completely before other accounts. `FatFIRE_Calculator.html`
- [ ] [T013] [ ] [Scenario B] Update simulation draw routines to follow user-defined Priority Ordered Account Drawdown Arrays with robust bypass-limit fallback mechanics drawing from remaining assets before flagging shortfalls. `FatFIRE_Calculator.html`

## 3. Phase 3: Table Projections columns additions, Hover Badges & Suggester Advice

- [ ] [T014] [ ] [Scenario C] Expand Projection Table structure adding separate columns for RMD, NIIT, and withdrawn sources itemized list. `FatFIRE_Calculator.html`
- [ ] [T015] [ ] [Scenario C] Center and align table column headers for the "Annual Cash Flow", "Taxes Paid", and "Withdrawn From" sections correctly. `FatFIRE_Calculator.html`
- [ ] [T016] [ ] [Scenario C] Apply dynamic `depleted-cell` high-contrast vibrant styling styles to table columns when balances drop to zero. `FatFIRE_Calculator.html`
- [ ] [T017] [ ] [Scenario C] Set up custom Suggestion advice tooltips on ⚠️ SHORTFALL badges with advanced back-calculations for tax-bracket drag to recommend precise additional draws needed to resolve the gap. `FatFIRE_Calculator.html`

## 4. Phase 4: Interactive Portfolio Charts Stack Details & End-To-End QA Verification

- [ ] [T018] [P] [Scenario C] Extend Chart.js configurations to capture individual nested values (Taxable, Deferred, Roth Roth, HK portfolios) with custom styled interactive tooltip overlays. `FatFIRE_Calculator.html`
- [ ] [T019] [ ] [All Scenarios] Complete fully automated and manual browser testing audits validating math balances, synced speeds (<15ms inputs, <100ms recalculations), and responsive visuals without layout overflows. `FatFIRE_Calculator.html`
