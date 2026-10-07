# Canadian Mortgage Market Analysis

A Power BI analysis of outstanding residential mortgage balances and balance-weighted interest rates for Canadian chartered banks.

[Read the project report](Canadian-market-dashboard-report.pdf) · [Download the Power BI file](MortgageMarket.pbix)

## Business Question

How have outstanding residential mortgage balances and balance-weighted interest rates evolved among Canadian chartered banks, and how has the fixed–variable rate gap changed?

The report is intended for banking, market research, and BI analysts exploring aggregate mortgage-market trends.

## Dashboard Preview

### Mortgage Market Overview

Tracks monthly outstanding balances and weighted interest rates. Summary cards display the latest available reporting month within the selected period.

![Mortgage Market Overview](Images/mortgage-overview.png.png)

### Mortgage Type Comparison

Compares weighted fixed and variable mortgage rates and displays their difference in percentage points.

The Year slicer controls the reporting period. The Rate Type slicer changes the chart series while preserving the comparison cards.

![Mortgage Type Comparison](Images/mortgage%20type%20comparison.png.png)

## Key Findings

- Outstanding balances increased from approximately **CAD 1.516 trillion in January 2024** to **CAD 1.564 trillion in December 2024**, an increase of approximately **3.2%**.
- During that period, the weighted variable rate declined from **6.62% to 4.69%**, while the weighted fixed rate increased from **3.68% to 4.10%**.
- The variable-minus-fixed gap narrowed from **+2.94 percentage points to +0.59 percentage points**.
- By **July 2026**, balances reached approximately **CAD 1.632 trillion**. The weighted variable rate was **3.74%**, compared with **4.39%** for fixed mortgages, giving a gap of **−0.65 percentage points**.

These figures describe outstanding mortgage balances and rates, rather than advertised offers for new mortgages.

## Data and Method

**Source:** [Statistics Canada Table 10-10-0006-01](https://doi.org/10.25318/1010000601-eng)

**Analytical period:** July 2016–July 2026, using the downloaded CSV snapshot.

**Coverage:** Canadian chartered banks in aggregate, including insured and uninsured residential mortgages.

The workflow included:

1. Importing and preparing the CSV with Power Query.
2. Deriving insurance status, rate type, lending measure, and mortgage-term categories.
3. Separating balance and interest-rate observations by their units.
4. Connecting the mortgage table to a Calendar table.
5. Creating DAX measures for balances, weighted rates, the rate gap, and reporting month.
6. Designing two report pages and a mobile layout.
7. Independently recalculating selected figures from the source CSV.

### Calculation Principles

- Balances are expressed in **CAD millions**.
- Monthly outstanding balances are snapshots and are not summed across months.
- Rates are weighted by their corresponding outstanding balances.
- The Total category is excluded from fixed–variable calculations to avoid double counting.
- The rate gap is **Variable − Fixed**, expressed in **percentage points (pp)**.

## Validation

Independent CSV calculations matched all five December 2024 dashboard values at their displayed precision:

| Metric | Dashboard value |
|---|---:|
| Outstanding balance (CAD millions) | 1,563,705.00 |
| Weighted overall rate | 4.26% |
| Weighted fixed rate | 4.10% |
| Weighted variable rate | 4.69% |
| Variable − Fixed gap | +0.59 pp |

Within the populated outstanding-mortgage period:

- All **121 months** contained the expected **12 mortgage components**.
- All **1,452 component-month groups** contained balance and rate observations.
- No duplicate month–component–unit keys or non-positive balances were found.

Applying the documented classification rules to residential mortgage records produced no Unknown categories. Year filtering and Fixed/Variable slicer interactions were also checked.

## Tools

- **Power BI Desktop:** data modelling and report design
- **Power Query:** data preparation
- **DAX:** measures and filter-context calculations
- **Python/pandas:** independent source reconciliation
- **Quarto:** project documentation

## How to Explore the Project

1. Download `MortgageMarket.pbix` and open it in Power BI Desktop.
2. Explore both report pages using the Year and Rate Type slicers.
3. Open **View → Mobile layout** to inspect the phone layout.
4. Read the PDF for methodology, findings, limitations, and technical details.

The imported data is stored in the Power BI file. To refresh it, download the source CSV and update the local file location in Power Query.

To render the Quarto report, download the `.qmd` file and the `Images` folder together, preserving their relative paths. PDF rendering requires Quarto and a compatible LaTeX installation.

## Limitations and Future Development

The report does not identify individual banks or borrowers and does not directly measure affordability, arrears, or default risk.

Potential extensions include incorporating policy rates, mortgage arrears, household debt-service indicators, and housing prices. Additional datasets would require compatible definitions, reporting periods, and geographic coverage.

A mobile layout has been prepared. Publishing to Power BI Service and testing on a physical phone remain pending.

## Author

**Definate Mudarikwa**

Portfolio project demonstrating financial data preparation, Power BI modelling, weighted calculations, validation, and analytical communication.
