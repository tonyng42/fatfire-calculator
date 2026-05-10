# Technical & IRS Rule Design Research - Advanced Retirement Calculator

## 1. Federal Tax Stand Deductions & Multi-Filing Brackets (2024)

### Decision
We will support four Federal filing statuses: Single, Married Filing Jointly (MFJ), Married Filing Separately (MFS), and Head of Household (HoH). The 2024 baseline IRS parameters are:
- **Single / MFS**: `$14,600` standard deduction.
- **MFJ**: `$29,200` standard deduction.
- **HoH**: `$21,900` standard deduction.

### Rationale
The prior engine defaulted to a single deduction threshold regardless of actual marital or head-of-household status, which created major projection errors for high-income FatFIRE couples or single earners.

### Alternatives Considered
- **Static Average Deduction**: Hardcoding field to `$20,000`. *Rejected*: FatFIRE projections span 40+ years; precise standard deductor bounds ensure actual tax brackets scale with household profiles correctly.

---

## 2. IRS Early Drawing Penalty Exemptions & SEPP Rules (Section 72(t))

### Decision
We will implement early withdrawal logic for traditional Tax-Deferred accounts prior to age 59½, adding a 10% federal tax penalty, but will implement a full SEPP (Substantially Equal Periodic Payments) exception mechanism. SEPP options will include the following calculation methods:
- **Amortization Method**: Periodic payments are computed via a fixed interest rate (limited to 120% of the mid-term Applicable Federal Rate).
- **Annuitization Method**: Uses annuity factors from IRS actuarial tables.
- **RMD Method**: Re-calculates distributions annually by dividing balance by remaining life expectancy.

### Rationale
Portfolios relying heavily on pre-tax deferred accounts need a compliant access method without paying the 10% early usage penalty. SEPP is the primary mechanism utilized under IRS Code Section 72(t).

### Alternatives Considered
- **Bypassing 10% Penalties**: Bypassing calculations. *Rejected*: Fails to accurately represent real-life tax penalties for users who do not plan appropriate bridging strategies.

---

## 3. Net Investment Income Tax (NIIT)

### Decision
Calculate Net Investment Income Tax (NIIT) at a rate of 3.8% above statutory MAGI limit boundaries matching each filing status:
- **Single / HoH**: `$200,000`
- **MFJ**: `$250,000`
- **MFS**: `$125,000`

### Rationale
FAT (FAT-FIRE) retirees often live on high capital gains and dividend draws. These distributions trigger the 3.8% surcharge under ACA rules once they exceed these thresholds.

### Alternatives Considered
- **Flat Tax Surcharges**: Generalizing to all investment gains. *Rejected*: Taxing low earners who are under MAGI thresholds is incorrect and distorts early retirement safety margins.
