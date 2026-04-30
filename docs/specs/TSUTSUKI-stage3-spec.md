# Stage 3 – Technical Specification
## BUS-314 International Corporate Finance | Accounting & Performance Ratios

**Analyst:** [Lynne Tsutsuki]
**Date:** April 2026
**Model File:** BUS-314 Accounting & Performance Ratios – MASTER.xlsx

---

## 1. Problem Statement

This model provides a comprehensive accounting and performance ratio analysis for a publicly traded company over a two-year period (current year and prior year). The analytical objective is to evaluate the firm's financial health across five dimensions — performance, profitability, efficiency, leverage, and liquidity — and to decompose return drivers using Du Pont analysis. Outputs are intended to support an investment recommendation or internal FP&A review by enabling systematic, year-over-year comparison against industry benchmarks.

---

## 2. Inputs (Known Variables)

All inputs are sourced from the most recent annual report (10-K) and supplemented by market data.

### Balance Sheet

| Named Range | Description | Year |
|---|---|---|
| `BAL_cash_mkt_sec_CY` | Cash and marketable securities | Current |
| `BAL_cash_mkt_sec_PY` | Cash and marketable securities | Prior |
| `BAL_receivables_CY` | Accounts receivable (net) | Current |
| `BAL_receivables_PY` | Accounts receivable (net) | Prior |
| `BAL_inventory_CY` | Inventory | Current |
| `BAL_inventory_PY` | Inventory | Prior |
| `BAL_current_assets_CY` | Total current assets | Current |
| `BAL_current_assets_PY` | Total current assets | Prior |
| `BAL_total_assets_CY` | Total assets | Current |
| `BAL_total_assets_PY` | Total assets | Prior |
| `BAL_current_liabilities_CY` | Total current liabilities | Current |
| `BAL_current_liabilities_PY` | Total current liabilities | Prior |
| `BAL_LT_debt_CY` | Long-term debt | Current |
| `BAL_LT_debt_PY` | Long-term debt | Prior |
| `BAL_total_debt_CY` | Total debt (current + LT) | Current |
| `BAL_total_debt_PY` | Total debt (current + LT) | Prior |
| `BAL_total_equity_CY` | Total shareholders' equity | Current |
| `BAL_total_equity_PY` | Total shareholders' equity | Prior |
| `BAL_invested_capital_CY` | Invested capital (debt + equity) | Current |
| `BAL_invested_capital_PY` | Invested capital (debt + equity) | Prior |

### Income Statement

| Named Range | Description |
|---|---|
| `INC_sales` | Net revenue / sales |
| `INC_COGS` | Cost of goods sold |
| `INC_gross_profit` | Gross profit |
| `INC_EBIT` | Earnings before interest and taxes |
| `INC_interest_expense` | Interest expense |
| `INC_EBT` | Earnings before taxes |
| `INC_tax_expense` | Income tax expense |
| `INC_net_income` | Net income |
| `INC_depreciation` | Depreciation and amortization |

### Cash Flow Statement

| Named Range | Description |
|---|---|
| `CASH_operating` | Net cash from operating activities |
| `CASH_capex` | Capital expenditures (absolute value) |
| `CASH_free_cash_flow` | Free cash flow (operating − capex) |

### Market / Analyst Inputs

| Named Range | Description |
|---|---|
| `MKT_share_price` | Current market price per share |
| `MKT_shares_outstanding` | Diluted shares outstanding |
| `MKT_market_cap` | Market capitalization (price × shares) |
| `MKT_book_value_equity` | Book value of equity (= `BAL_total_equity_CY`) |
| `ASMP_WACC` | Weighted average cost of capital |
| `ASMP_tax_rate` | Effective or statutory tax rate |

---

## 3. Named Range Conventions

All named ranges follow the pattern: `[SOURCE]_[descriptor]_[period]`

- **Prefix codes:** `BAL_` = Balance Sheet · `INC_` = Income Statement · `CASH_` = Cash Flow · `MKT_` = Market Data · `ASMP_` = Assumption · `CALC_` = Derived/Intermediate
- **Period suffixes:** `_CY` = current year · `_PY` = prior year · *(no suffix)* = single-period income/cash flow items
- **Example:** `BAL_receivables_CY` → current-year accounts receivable from the balance sheet

Derived and intermediate values use the `CALC_` prefix (e.g., `CALC_avg_assets`, `CALC_NOPAT`, `CALC_daily_sales`).

---

## 4. Assumptions & Constraints

- **Tax rate:** Applied as `ASMP_tax_rate`; defaults to the company's effective rate; statutory 21% used if effective rate is unavailable or distorted by one-time items.
- **Interest basis:** All interest calculations assume simple annual interest; no intra-year compounding.
- **Averaging:** Average balance sheet figures (assets, equity, invested capital) are computed as a straight average of current and prior year-end balances.
- **Receivables:** Gross receivables are used where net figures are unavailable or immaterial to the allowance.
- **Debt definition:** Total debt = short-term borrowings + current portion of LT debt + long-term debt. Excludes operating lease obligations unless otherwise noted.
- **Invested capital:** Debt + equity; excludes non-interest-bearing current liabilities (accounts payable, accrued expenses).
- **Off-balance-sheet items:** Not included. Operating leases are excluded unless already capitalized per ASC 842.
- **Market data:** Share price reflects the closing price on the reporting date; analyst consensus data is not used.
- **Days basis:** 365 days per year for all collection-period and days-in-inventory calculations.

---

## 5. Calculation Flow

### 5a. Derived Inputs

```
CALC_avg_assets         = (BAL_total_assets_CY + BAL_total_assets_PY) / 2
CALC_avg_equity         = (BAL_total_equity_CY + BAL_total_equity_PY) / 2
CALC_avg_invested_cap   = (BAL_invested_capital_CY + BAL_invested_capital_PY) / 2
CALC_avg_receivables    = (BAL_receivables_CY + BAL_receivables_PY) / 2
CALC_avg_inventory      = (BAL_inventory_CY + BAL_inventory_PY) / 2
CALC_NOPAT              = INC_EBIT × (1 − ASMP_tax_rate)
CALC_daily_sales        = INC_sales / 365
CALC_NWC                = BAL_current_assets_CY − BAL_current_liabilities_CY
```

### 5b. Performance Ratios

```
MVA (Market Value Added)  = MKT_market_cap − BAL_book_value_equity
Market-to-Book            = MKT_market_cap / BAL_book_value_equity
EVA (Economic Value Added)= CALC_NOPAT − (ASMP_WACC × CALC_avg_invested_cap)
```

### 5c. Profitability Ratios

```
ROA (start-of-year)   = INC_net_income / BAL_total_assets_PY
ROA (average)         = INC_net_income / CALC_avg_assets
ROC (start-of-year)   = CALC_NOPAT / BAL_invested_capital_PY
ROC (average)         = CALC_NOPAT / CALC_avg_invested_cap
ROE (start-of-year)   = INC_net_income / BAL_total_equity_PY
ROE (average)         = INC_net_income / CALC_avg_equity
```

### 5d. Efficiency Ratios

```
Asset Turnover              = INC_sales / CALC_avg_assets
Receivables Turnover        = INC_sales / CALC_avg_receivables
Collection Period (DSO)     = 365 / Receivables Turnover
Inventory Turnover          = INC_COGS / CALC_avg_inventory
Days in Inventory           = 365 / Inventory Turnover
Gross Margin                = INC_gross_profit / INC_sales
Operating Margin            = INC_EBIT / INC_sales
Net Profit Margin           = INC_net_income / INC_sales
```

### 5e. Leverage Ratios

```
Debt-to-Assets              = BAL_total_debt_CY / BAL_total_assets_CY
Debt-to-Equity              = BAL_total_debt_CY / BAL_total_equity_CY
Equity Multiplier           = BAL_total_assets_CY / BAL_total_equity_CY
Interest Coverage (EBIT)    = INC_EBIT / INC_interest_expense
Debt Burden                 = INC_EBT / INC_EBIT
```

### 5f. Liquidity Ratios

```
Current Ratio               = BAL_current_assets_CY / BAL_current_liabilities_CY
Quick Ratio                 = (BAL_cash_mkt_sec_CY + BAL_receivables_CY) / BAL_current_liabilities_CY
Cash Ratio                  = BAL_cash_mkt_sec_CY / BAL_current_liabilities_CY
NWC-to-Assets               = CALC_NWC / BAL_total_assets_CY
```

### 5g. Du Pont Decomposition

**3-Factor ROA:**
```
ROA = Net Profit Margin × Asset Turnover
    = (INC_net / INC_sales) × (INC_sales / CALC_avg_assets)
```

**5-Factor ROE (Extended Du Pont):**
```
ROE = Tax Burden × Debt Burden × Operating Margin × Asset Turnover × Equity Multiplier
    = (INC_net / INC_EBT) × (INC_EBT / INC_EBIT) × (INC_EBIT / INC_sales)
      × (INC_sales / CALC_avg_assets) × (CALC_avg_assets / CALC_avg_equity)
```

---

## 6. Outputs

The model produces the following outputs, organized across worksheet tabs:

- **Inputs tab:** All raw financial statement data with source annotations; blue-coded hardcoded values.
- **Ratio Summary tab:** A formatted dashboard presenting all ratio categories side-by-side for current year, with year-over-year delta columns and conditional formatting (red/green) flagging directional changes.
- **Performance tab:** MVA, Market-to-Book, and EVA calculations with intermediate steps visible.
- **Du Pont tab:** Both the 3-factor and 5-factor decompositions presented in a tree/waterfall layout showing how each driver contributes to the final return metric.
- **Chart tab (optional):** Bar or spider chart comparing the company's key ratios against an industry benchmark band.

---

## 7. Model Review — What Worked & What to Improve

### What Operated as Intended

The input consolidation structure — grouping all raw financials on a single Inputs tab with clearly labeled named ranges — significantly reduced cross-sheet reference errors. Ratio formulas using named ranges (e.g., `CALC_NOPAT / CALC_avg_invested_cap`) are readable and auditable without tracing cell addresses. The dual presentation of start-of-year vs. average-based return ratios correctly captures the timing difference that affects ROE/ROA interpretation across different analysts and textbooks.

### Simplifications to Replace in a Rigorous Version

- **Tax rate hardcode:** The current model applies a single statutory rate. A revised version should compute the effective rate directly from `INC_tax_expense / INC_EBT` and flag if it deviates materially from the statutory rate.
- **Debt definition:** The current debt figure may inconsistently include or exclude capitalized lease obligations depending on the company. A robust version should explicitly reconcile debt from the balance sheet footnotes.
- **Prior-year receivables/inventory:** Some builds used only the current-year balance for turnover calculations rather than the true average, slightly overstating turnover for high-growth companies. This should be standardized to average balances throughout.

### Naming, Layout, and Auditability Improvements

- All ratio results should display both the formula in named-range notation (as a cell comment) and the computed value, enabling a reviewer to verify logic without opening the formula bar.
- The `CALC_` prefix layer (derived inputs) should be its own section on the Inputs tab — currently some derived values are embedded within ratio tabs, making the flow harder to audit.
- Column headers should include the fiscal year in every tab header row, not just the Inputs tab, to prevent confusion when the file is shared without context.

### Additional Scenarios or Metrics Worth Including

- A **cash flow adequacy** section using `CASH_operating` and `CASH_free_cash_flow` relative to debt service and capital needs.
- An **industry comparison column** with manually entered benchmark ratios, clearly coded as external inputs.
- **CAGR rows** for multi-year trend analysis if a third historical year is available.

---

## 8. Limitations & Next Steps

**Excluded from this model:**

- Off-balance-sheet obligations (operating leases pre-ASC 842, synthetic leases, pension underfunding)
- Segment-level analysis; all ratios reflect consolidated financials
- Qualitative factors (management quality, competitive moat, regulatory environment)
- Forward-looking projections; all calculations are historical

**Setup for Stage 4:**

The Calculation Flow in Section 5 is written as pseudocode using named-range notation and is directly portable to a Stage 4 AI prompt instruction block. The Model Review in Section 7 identifies the specific improvements the AI rebuild should address. The Outputs section defines the deliverable tables and charts the Stage 4 model must reproduce or surpass.

The Stage 4 prompt should instruct the AI to: (1) accept the same named-range inputs defined here, (2) compute all ratios in the sequence specified in Section 5, (3) apply the corrections identified in Section 7, and (4) return a clean ratio summary table formatted for CFO-level presentation.

---

*Prepared for BUS-314 International Corporate Finance | Shidler College of Business*
