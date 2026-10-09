# Tata Steel Limited: Credit Risk Model (Altman Z-Score)

![Excel](https://img.shields.io/badge/Built%20with-Microsoft%20Excel-217346?logo=microsoftexcel&logoColor=white)
![Model](https://img.shields.io/badge/Model-Altman%20Z--Score%20(1968)-blue)
![Sector](https://img.shields.io/badge/Sector-Indian%20Steel-orange)
![FY](https://img.shields.io/badge/Fiscal%20Year-FY2026-lightgrey)

An Excel-based credit risk model that assesses the bankruptcy risk of **Tata Steel Limited (NSE: TATASTEEL)** using the **Altman Z-Score (1968)**. It converts the score into a credit zone, an implied credit rating and a recommendation, stress-tests the result under recession scenarios, and benchmarks Tata Steel against four Indian steel peers.

> **Disclaimer:** This project is for academic and analytical purposes only. It is not investment advice.

---

## Table of Contents

1. [Key Results](#key-results)
2. [Project Overview](#project-overview)
3. [Methodology](#methodology)
4. [Workbook Structure](#workbook-structure)
5. [Inputs Used](#inputs-used)
6. [Detailed Findings](#detailed-findings)
7. [Stress Test](#stress-test)
8. [Peer Comparison](#peer-comparison)
9. [How to Use the Model](#how-to-use-the-model)
10. [Adapting the Model to Another Company](#adapting-the-model-to-another-company)
11. [Assumptions and Limitations](#assumptions-and-limitations)
12. [Data Sources](#data-sources)
13. [Repository Contents](#repository-contents)
14. [Author](#author)

---

## Key Results

| Metric | Result |
|---|---|
| **Altman Z-Score** | **2.08** |
| **Credit Zone** | Grey Zone (1.81 to 2.99) |
| **Credit Grade (0 to 10 scale)** | 6 |
| **Implied Credit Rating** | BB/B |
| **Recommendation** | Neutral: monitor for deterioration, limit credit exposure |
| **Peer Rank** | 3rd of 5 Indian steel companies |
| **Z-Score under Severe Recession** | 1.83 (just above the 1.81 distress line) |

---

## Project Overview

**Objective:** Quantify the financial health of Tata Steel and estimate its probability of financial distress using a transparent, formula-driven model.

**What the model does:**

- Takes a small set of balance sheet, P&L and market inputs
- Calculates the five Altman component ratios (X1 to X5)
- Computes the weighted Z-Score and classifies the company into Safe, Grey or Distress zones
- Maps the score to a 0 to 10 credit grade, an implied rating band and a recommendation
- Stress-tests the Z-Score under mild and severe recession scenarios
- Ranks Tata Steel against JSW Steel, SAIL, Jindal Steel and NMDC Steel
- Presents everything on a one-page dashboard with an analyst commentary

**Why Altman Z-Score?** It is a widely used, interpretable early-warning model for corporate distress. The original 1968 version was built for publicly traded manufacturing companies, which makes it a reasonable fit for a listed steel producer.

---

## Methodology

### The Z-Score formula

```
Z = 1.2·X1 + 1.4·X2 + 3.3·X3 + 0.6·X4 + 1.0·X5
```

| Ratio | Definition | Weight | What it measures |
|---|---|---|---|
| **X1** | Working Capital / Total Assets | 1.2 | Short-term liquidity |
| **X2** | Retained Earnings / Total Assets | 1.4 | Cumulative profitability and age of firm |
| **X3** | EBIT / Total Assets | 3.3 | Operating profitability of assets |
| **X4** | Market Cap / Total Liabilities | 0.6 | Market-implied solvency cushion |
| **X5** | Revenue / Total Assets | 1.0 | Asset turnover and efficiency |

Where **Working Capital = Current Assets − Current Liabilities**.

### Zone classification

| Z-Score | Zone | Interpretation |
|---|---|---|
| Above 2.99 | **Safe Zone** | Low bankruptcy risk |
| 1.81 to 2.99 | **Grey Zone** | Monitor closely |
| Below 1.81 | **Distress Zone** | High bankruptcy risk |

### Credit grade, rating and recommendation mapping

The model converts the Z-Score into a 0 to 10 grade, then into a rating band and recommendation.

| Z-Score | Grade | | Grade | Implied Rating | | Grade | Recommendation |
|---|---|---|---|---|---|---|---|
| 4.00 and above | 10 | | 9 to 10 | AAA/AA | | 7 and above | Buy / Hold |
| 3.50 to 3.99 | 9 | | 7 to 8 | A/BBB | | 4 to 6 | Neutral |
| 2.99 to 3.49 | 8 | | 5 to 6 | BB/B | | Below 4 | Sell / Avoid |
| 2.50 to 2.98 | 7 | | 3 to 4 | CCC/CC | | | |
| 2.00 to 2.49 | 6 | | Below 3 | D/Default Risk | | | |
| 1.81 to 1.99 | 5 | | | | | | |
| 1.50 to 1.80 | 4 | | | | | | |
| 1.20 to 1.49 | 3 | | | | | | |
| 0.80 to 1.19 | 2 | | | | | | |
| Below 0.80 | 1 | | | | | | |

> The grade-to-rating mapping is an **illustrative heuristic** created for this project. It is not an official credit rating.

---

## Workbook Structure

`Tata_Steel_Credit_Risk_Model.xlsx` contains nine sheets:

| Sheet | Purpose |
|---|---|
| **COVER** | Title page: company, ticker, analysis date, fiscal year end, currency, model used, data source, analyst, and headline Z-Score result |
| **INPUTS** | The only sheet you need to edit. Balance sheet, P&L and market data entered manually, with a note beside each cell saying where to find it |
| **RATIOS** | Calculates X1 to X5, applies the weights, and gives a plain-English interpretation of each ratio. Includes a bar chart |
| **ZSCORE** | Final output: Z-Score, credit zone, 0 to 10 credit grade, implied rating and recommendation |
| **STRESS_TEST** | Base, Mild Recession and Severe Recession scenarios, each with a recalculated Z-Score. Includes a chart against the distress and safe lines |
| **PEER_COMP** | Z-Score comparison and ranking of Tata Steel, JSW Steel, SAIL, Jindal Steel and NMDC Steel. Includes a bar chart |
| **DASHBOARD** | One-page summary: headline score, rating, recommendation, ratio table, stress-test summary and written credit commentary |
| **Account statement** | Raw consolidated balance sheet and P&L (FY2025 and FY2026) for Tata Steel, plus a peer data table, copied from Screener.in |
| **Sheet8** | A second copy of the raw financial data and peer table used while collecting inputs |

**Flow of data:**

```
Account statement / Sheet8 (raw data)
            │
            ▼
         INPUTS  ──►  RATIOS  ──►  ZSCORE  ──►  DASHBOARD / COVER
            │                          ▲
            └────────►  STRESS_TEST ───┘
                         PEER_COMP (standalone peer inputs)
```

---

## Inputs Used

All figures are **consolidated, in ₹ Crores**, for the fiscal year ended **March 2026**.

| Input | Value (₹ Cr) | Source line |
|---|---|---|
| Total Current Assets | 81,021 | Balance Sheet: Current Assets |
| Total Current Liabilities | 1,01,965 | Balance Sheet: Current Liabilities |
| Total Assets | 2,96,515 | Balance Sheet: Total Assets |
| Total Liabilities | 2,96,515 | Balance Sheet: Total Liabilities |
| Retained Earnings | 1,00,920 | Balance Sheet: Reserves & Surplus |
| Revenue (Net Sales) | 2,32,140 | P&L: Net Sales |
| EBIT (Operating Profit) | 34,352 | P&L: Operating Profit |
| Market Capitalisation | 2,58,146 | Screener.in company page |

---

## Detailed Findings

| Ratio | Value | Weight | Weighted Score | Assessment |
|---|---|---|---|---|
| **X1** Working Capital / TA | −0.071 | 1.2 | −0.085 | **Distress**: negative working capital |
| **X2** Retained Earnings / TA | 0.340 | 1.4 | 0.476 | **Healthy**: strong retained profits |
| **X3** EBIT / TA | 0.116 | 3.3 | 0.382 | **Moderate**: low return on assets |
| **X4** Market Cap / Liabilities | 0.871 | 0.6 | 0.522 | **Distress**: market-to-liabilities below 1 |
| **X5** Revenue / TA | 0.783 | 1.0 | 0.783 | **Moderate**: average asset efficiency |
| **Z-Score** | | | **2.079** | **Grey Zone** |

**Reading the result:**

- **Strength:** A large retained earnings base (X2) gives the balance sheet resilience.
- **Weakness:** Current liabilities exceed current assets (X1), and the market values the company below the book value of its liabilities (X4).
- **Middle ground:** Profitability (X3) and asset turnover (X5) are adequate but not strong, which is typical of a capital-intensive, cyclical steel business.
- **Overall:** The profile is bifurcated. The company is not in imminent distress, but there is limited headroom, so ongoing monitoring is warranted.

---

## Stress Test

Three scenarios are applied to revenue, EBIT and working capital, then the Z-Score is recalculated using the same weights.

| Assumption | Base Case | Mild Recession | Severe Recession |
|---|---|---|---|
| Revenue shock | 0% | −15% | −30% |
| EBIT shock | 0% | −5% | −12% |
| Working capital shock | 0% | −20% | −40% |
| Stressed Revenue (₹ Cr) | 2,32,140 | 1,97,319 | 1,62,498 |
| Stressed EBIT (₹ Cr) | 34,352 | 32,634 | 30,230 |
| Stressed Working Capital (₹ Cr) | −20,944 | −16,755 | −12,566 |
| **Stressed Z-Score** | **2.08** | **1.96** | **1.83** |
| **Zone** | Grey | Grey | Grey (near distress line) |

Even under severe stress, the score stays marginally above the 1.81 distress threshold, but with very little buffer.

---

## Peer Comparison

| Rank | Company | Z-Score | Zone |
|---|---|---|---|
| 1 | JSW Steel | 2.48 | Grey |
| 2 | Jindal Steel | 2.31 | Grey |
| 3 | **Tata Steel** | **2.08** | **Grey** |
| 4 | SAIL | 2.05 | Grey |
| 5 | NMDC Steel | 1.38 | Distress |

Tata Steel sits mid-pack. No peer reaches the Safe Zone, which reflects the leverage and cyclicality of the Indian steel sector as a whole.

---

## How to Use the Model

### Requirements

- Microsoft Excel (2016 or later recommended). LibreOffice Calc or Google Sheets can open the file, but charts and conditional formatting may look different.

### Steps

1. **Download** `Tata_Steel_Credit_Risk_Model.xlsx` from this repository (click the file, then the download icon).
2. **Open** the file in Excel. If you see a "Protected View" banner, click **Enable Editing**. If Excel asks about updating links, choose **Don't Update** (see [Limitations](#assumptions-and-limitations)).
3. **Go to the `INPUTS` sheet.** Edit the values in column B. Column C tells you where each figure comes from.
4. **Check the other sheets update:** `RATIOS`, `ZSCORE`, `STRESS_TEST` and `DASHBOARD` recalculate automatically.
5. **Edit stress assumptions** (optional) in the blue/input cells of `STRESS_TEST` (rows 4 to 6).
6. **Read the results** on the `DASHBOARD` sheet.

> Note: the **Analysis Date** on `INPUTS` uses `=TODAY()`, so it changes every time you open the file.

---

## Adapting the Model to Another Company

1. Make a copy of the workbook.
2. In `INPUTS`, change the company name, ticker, currency and fiscal year end.
3. Replace the eight financial inputs (current assets, current liabilities, total assets, total liabilities, retained earnings, revenue, EBIT, market cap) with the new company's figures.
4. Update the peer data in `PEER_COMP`.
5. Rewrite the commentary on `DASHBOARD`, which is static text and will not update automatically.

> The original 1968 Z-Score is calibrated for **listed manufacturing** firms. For non-manufacturing or private companies, use the Z′ or Z″ variants with different weights and cut-offs. For banks and NBFCs, the Z-Score is not appropriate.

---

## Assumptions and Limitations

**Model limitations**

- The 1968 Altman model was calibrated on US manufacturers. Applying it to an Indian steel company is an approximation.
- It is a **point-in-time** measure using one year's accounts and does not capture forward-looking cash flows, debt maturity profile or covenants.
- **X4 uses total liabilities as reported by Screener.in**, which equals total assets in this dataset (it includes equity and reserves). This overstates liabilities and understates X4. A stricter version would use borrowings plus other true liabilities only.
- The implied rating (BB/B) and the 0 to 10 grade are **heuristic mappings**, not official agency ratings.
- The stress test shocks only revenue, EBIT and working capital. Retained earnings, market capitalisation and total assets are held constant, which understates how stress would really propagate (equity values typically fall in a downturn).
- EBIT shocks are applied as a percentage reduction in EBIT, not as percentage-point cuts to the margin.
- Market capitalisation changes daily, so X4 and the Z-Score are sensitive to the date of data collection.
- The dashboard commentary is written text and must be updated manually if inputs change.

**Data notes**

- Figures are consolidated and taken from Screener.in. Small differences exist between the raw data tabs (for example, current liabilities and market cap appear slightly differently in `Account statement` and `Sheet8`). The `INPUTS` sheet is the source of truth for the main calculation.
- `PEER_COMP` ratios are entered as hard-coded values, so peer Z-Scores will not update when `INPUTS` changes. Tata Steel's row there is a rounded snapshot of the main model.
- Some cells (cover page, dashboard) reference an external copy of the workbook. This is why Excel may show an "update links" prompt.

---

## Data Sources

- **Screener.in**: consolidated balance sheet, P&L and market capitalisation
- **NSE India**: ticker and listing information
- Altman, E. I. (1968). *Financial Ratios, Discriminant Analysis and the Prediction of Corporate Bankruptcy.* The Journal of Finance, 23(4), 589 to 609.

---

## Repository Contents

```
tata-steel-credit-risk-model/
├── Tata_Steel_Credit_Risk_Model.xlsx   # The full Excel model
├── README.md                           # This file
└── screenshots/                        # (optional) images of the dashboard and charts
```

### Screenshots (add yours here)

After uploading images to a `screenshots` folder, display them with:

```markdown
![Dashboard](screenshots/dashboard.png)
![Stress Test](screenshots/stress-test.png)
![Peer Comparison](screenshots/peer-comparison.png)
```

---

## Author

**Helan Preethi**
Credit risk and financial modelling project | FY2026 analysis

If you found this useful, please give the repository a ⭐.

---

*For academic and analytical purposes only. Not investment advice.*
