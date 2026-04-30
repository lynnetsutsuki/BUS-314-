# Stage 4 – AI Regeneration Prompt
## BUS-314 International Corporate Finance | Accounting & Performance Ratios
**Analyst:** Lynne Tsutsuki | **Company:** Apple Inc. (AAPL) | **Date:** April 2026

---

# GOAL

You are a financial analyst assistant. Rebuild a complete, auditable Excel ratio model for **Apple Inc. (AAPL)** based on FY2024 (Sep 28, 2024) and FY2023 (Sep 30, 2023) annual report data. The model must be structured across five worksheet tabs: **Balance Sheet**, **Income Statement**, **Cash Flow Statement**, **Ratios**, and **Notes**.

All figures are in **millions of US dollars** unless noted. Use the named range system defined below as the single source of truth — every ratio must reference named ranges, not raw cell addresses. The finished workbook must be zero-error (no #REF!, #DIV/0!, #VALUE!, or #NAME? errors) and formatted for CFO-level review.

**Color coding standard:**
- Blue text = hardcoded analyst assumptions
- Yellow background = raw financial data inputs (from 10-K)
- Black text = all formula outputs

---

# DATA

## Analyst Assumptions (Blue — hardcoded inputs)

| Named Range | Value | Description |
|---|---|---|
| `yearCurrent` | 2024 | Current fiscal year |
| `yearStart` | 2023 | Prior fiscal year (= yearCurrent − 1) |
| `share_price` | 226.51 | End-of-fiscal-year closing price ($) |
| `shares_outstanding` | 15,204 | Diluted shares outstanding (millions) |
| `cost_capital` | 0.090 | Estimated WACC |
| `tax_rate` | 0.241 | Effective tax rate (24.1%) |

---

## Balance Sheet Inputs — FY2024 / FY2023 ($M)

| Named Range (CY) | FY2024 | Named Range (PY) | FY2023 | Line Item |
|---|---|---|---|---|
| `BAL_cash_marketable_securities_2024` | 65,171 | `BAL_cash_marketable_securities_2023` | 61,555 | Cash and marketable securities |
| `BAL_receivables_2024` | 33,410 | `BAL_receivables_2023` | 29,508 | Receivables (net) |
| `BAL_inventories_2024` | 7,286 | `BAL_inventories_2023` | 6,331 | Inventories |
| `BAL_other_current_assets_2024` | 47,120 | `BAL_other_current_assets_2023` | 46,172 | Other current assets |
| `BAL_assets_current_2024` | 152,987 | `BAL_assets_current_2023` | 143,566 | Total current assets |
| `BAL_PP&E_gross_2024` | 119,128 | `BAL_PP&E_gross_2023` | 109,528 | Property, plant & equipment (gross) |
| `BAL_accum_depreciation_2024` | 73,448 | `BAL_accum_depreciation_2023` | 65,813 | Less accumulated depreciation |
| `BAL_PP&E_net_2024` | 45,680 | `BAL_PP&E_net_2023` | 43,715 | Net tangible fixed assets |
| `BAL_other_assets_2024` | 166,313 | `BAL_other_assets_2023` | 165,302 | Other (long-term) assets |
| `BAL_assets_total_2024` | 364,980 | `BAL_assets_total_2023` | 352,583 | **Total assets** |
| `BAL_debt_current_2024` | 10,912 | `BAL_debt_current_2023` | 9,822 | Debt due for repayment (current) |
| `BAL_accounts_payable_2024` | 68,960 | `BAL_accounts_payable_2023` | 62,611 | Accounts payable |
| `BAL_other_current_liab_2024` | 96,520 | `BAL_other_current_liab_2023` | 72,875 | Other current liabilities |
| `BAL_liabilities_current_2024` | 176,392 | `BAL_liabilities_current_2023` | 145,308 | **Total current liabilities** |
| `BAL_debt_long_term_2024` | 85,750 | `BAL_debt_long_term_2023` | 95,281 | Long-term debt |
| `BAL_other_LT_liab_2024` | 45,888 | `BAL_other_LT_liab_2023` | 49,848 | Other long-term liabilities |
| `BAL_liabilities_total_2024` | 308,030 | `BAL_liabilities_total_2023` | 290,437 | **Total liabilities** |
| `BAL_common_stock_2024` | 83,276 | `BAL_common_stock_2023` | 73,812 | Common stock & paid-in capital |
| `BAL_retained_earnings_2024` | -26,326 | `BAL_retained_earnings_2023` | -11,666 | Retained earnings |
| `BAL_equity_shareholders_2024` | 56,950 | `BAL_equity_shareholders_2023` | 62,146 | **Total shareholders' equity** |

---

## Income Statement Inputs — FY2024 ($M)

| Named Range | Value | Line Item |
|---|---|---|
| `INC_sales` | 391,035 | Net sales |
| `INC_cost_goods_sold` | 210,352 | Cost of goods sold |
| `INC_gross_profit` | 180,683 | Gross profit (= sales − COGS) |
| `INC_SGA` | 26,097 | Selling, general & administrative |
| `INC_depreciation` | 11,445 | Depreciation & amortization |
| `INC_ebit` | 143,141 | **EBIT** |
| `INC_other_income` | 3,764 | Other income |
| `INC_interest_expense` | 3,931 | Interest expense |
| `INC_ebt` | 142,974 | Taxable income (EBT) |
| `INC_taxes` | 29,749 | Income tax expense |
| `INC_net` | 113,225 | **Net income** |
| `INC_dividends` | 15,234 | Dividends paid |
| `INC_retained_addition` | 97,991 | Addition to retained earnings |

---

## Cash Flow Statement Inputs — FY2024 ($M)

| Named Range | Value | Line Item |
|---|---|---|
| `CASH_net_income` | 113,225 | Net income |
| `CASH_depreciation` | 11,445 | Depreciation add-back |
| `CASH_delta_receivables` | -3,788 | Change in accounts receivable |
| `CASH_delta_inventory` | -1,046 | Change in inventories |
| `CASH_delta_other_current_assets` | -10,375 | Change in other current assets |
| `CASH_delta_AP` | 6,020 | Change in accounts payable |
| `CASH_delta_other_current_liab` | 15,552 | Change in other current liabilities |
| `CASH_working_capital_change` | 6,363 | Total change in working capital |
| `CASH_operating` | 131,033 | **Cash from operations** |
| `CASH_capex` | -9,447 | Capital expenditures |
| `CASH_LT_asset_sales` | 13,690 | Sales of long-term assets |
| `CASH_other_investing` | -1,308 | Other investing activities |
| `CASH_investing` | 2,935 | **Cash from investing** |
| `CASH_ST_debt_change` | -9,958 | Change in short-term debt |
| `CASH_LT_debt_change` | 3,960 | Change in long-term debt |
| `CASH_dividends_paid` | -15,234 | Dividends paid |
| `CASH_stock_repurchase` | -94,949 | Stock repurchases (net) |
| `CASH_other_financing` | -5,802 | Other financing |
| `CASH_financing` | -121,983 | **Cash from financing** |
| `CASH_net_change` | 11,985 | Net change in cash |

---

# RATIOS

Build the **Ratios** tab using the following exact sequence. All intermediate `CALC_` values must appear in a visible "Derived Inputs" section before the ratio output tables.

## Derived Inputs (CALC_ layer)

```
market_capitalization           = share_price × shares_outstanding
                                → 226.51 × 15,204 = 3,443,858.04

startYear_equity                = BAL_equity_shareholders_2023       → 62,146
startYear_inventory             = BAL_inventories_2023               → 6,331
startYear_receivables           = BAL_receivables_2023               → 29,508
startYear_total_assets          = BAL_assets_total_2023              → 352,583
startYear_total_capitalization  = BAL_debt_long_term_2023
                                  + BAL_equity_shareholders_2023     → 157,427

currentYear_after_tax_op_income = INC_net + (1 − tax_rate) × INC_interest_expense
                                → 113,225 + 0.759 × 3,931 = 116,208.63

currentYear_daily_sales_average = INC_sales / 365                    → 1,071.33
currentYear_cost_goods_sold_daily = INC_cost_goods_sold / 365        → 576.31
currentYear_equity              = BAL_equity_shareholders_2024       → 56,950
currentYear_cash_mkt_sec        = BAL_cash_marketable_securities_2024→ 65,171
currentYear_assets_current      = BAL_assets_current_2024            → 152,987
currentYear_liabilities_current = BAL_liabilities_current_2024       → 176,392
currentYear_debt_long_term      = BAL_debt_long_term_2024            → 85,750
currentYear_working_capital_net = currentYear_assets_current
                                  − currentYear_liabilities_current  → -23,405
currentYear_assets_total        = BAL_assets_total_2024              → 364,980
currentYear_total_capitalization= BAL_debt_long_term_2024
                                  + BAL_equity_shareholders_2024     → 142,700
currentYear_liabilities_total   = BAL_liabilities_total_2024         → 308,030

avg_equity                      = AVERAGE(startYear_equity,
                                          currentYear_equity)         → 59,548
avg_total_assets                = AVERAGE(startYear_total_assets,
                                          currentYear_assets_total)  → 358,781.5
avg_total_capitalization        = AVERAGE(startYear_total_capitalization,
                                          currentYear_total_capitalization) → 150,063.5
```

---

## Performance Ratios

```
MVA (Market Value Added)    = market_capitalization − currentYear_equity
                            → 3,443,858.04 − 56,950 = 3,386,908.04

Market-to-Book Ratio        = market_capitalization / currentYear_equity
                            → 3,443,858.04 / 56,950 = 60.47×

EVA (Economic Value Added)  = currentYear_after_tax_op_income
                              − (cost_capital × startYear_total_capitalization)
                            → 116,208.63 − (0.09 × 157,427) = 102,040.20
```

---

## Profitability Ratios

```
ROA (start-of-year)   = currentYear_after_tax_op_income / startYear_total_assets
                      → 116,208.63 / 352,583 = 32.96%

ROA (average)         = currentYear_after_tax_op_income / avg_total_assets
                      → 116,208.63 / 358,781.5 = 32.39%

ROC (start-of-year)   = currentYear_after_tax_op_income / startYear_total_capitalization
                      → 116,208.63 / 157,427 = 73.82%

ROC (average)         = currentYear_after_tax_op_income / avg_total_capitalization
                      → 116,208.63 / 150,063.5 = 77.44%

ROE (start-of-year)   = INC_net / startYear_equity
                      → 113,225 / 62,146 = 182.19%

ROE (average)         = INC_net / avg_equity
                      → 113,225 / 59,548 = 190.14%
```

---

## Efficiency Ratios

```
Asset Turnover              = INC_sales / startYear_total_assets
                            → 391,035 / 352,583 = 1.109×         [RATIO_asset_turnover]

Receivables Turnover        = INC_sales / startYear_receivables
                            → 391,035 / 29,508 = 13.25×

Avg Collection Period (DSO) = startYear_receivables / currentYear_daily_sales_average
                            → 29,508 / 1,071.33 = 27.54 days

Inventory Turnover          = INC_cost_goods_sold / startYear_inventory
                            → 210,352 / 6,331 = 33.23×

Days in Inventory           = startYear_inventory / currentYear_cost_goods_sold_daily
                            → 6,331 / 576.31 = 10.99 days

Profit Margin               = INC_net / INC_sales
                            → 113,225 / 391,035 = 28.96%

Operating Profit Margin     = currentYear_after_tax_op_income / INC_sales
                            → 116,208.63 / 391,035 = 29.72%     [RATIO_operating_profit_margin]
```

---

## Leverage Ratios

```
LT Debt Ratio               = currentYear_debt_long_term
                              / (currentYear_debt_long_term + currentYear_equity)
                            → 85,750 / 142,700 = 60.09%

LT Debt-to-Equity           = currentYear_debt_long_term / currentYear_equity
                            → 85,750 / 56,950 = 1.506×

Total Debt Ratio            = currentYear_liabilities_total / currentYear_assets_total
                            → 308,030 / 364,980 = 84.40%

Times Interest Earned       = INC_ebit / INC_interest_expense
                            → 143,141 / 3,931 = 36.41×

Cash Coverage Ratio         = (INC_ebit + INC_depreciation) / INC_interest_expense
                            → (143,141 + 11,445) / 3,931 = 39.32×

Debt Burden                 = INC_net / currentYear_after_tax_op_income
                            → 113,225 / 116,208.63 = 97.43%     [RATIO_debt_burden]

Leverage Ratio              = currentYear_assets_total / currentYear_equity
                            → 364,980 / 56,950 = 6.409×         [RATIO_leverage]
```

---

## Liquidity Ratios

```
NWC-to-Assets               = currentYear_working_capital_net / currentYear_assets_total
                            → -23,405 / 364,980 = -6.41%

Current Ratio               = currentYear_assets_current / currentYear_liabilities_current
                            → 152,987 / 176,392 = 0.867×

Quick Ratio                 = (currentYear_cash_mkt_sec + BAL_receivables_2024)
                              / currentYear_liabilities_current
                            → (65,171 + 33,410) / 176,392 = 0.559×

Cash Ratio                  = currentYear_cash_mkt_sec / currentYear_liabilities_current
                            → 65,171 / 176,392 = 0.369×
```

---

## Du Pont Decomposition

**3-Factor ROA:**
```
ROA (Du Pont) = RATIO_asset_turnover × RATIO_operating_profit_margin
              = 1.109 × 29.72% = 32.96%

  └── Asset Turnover:         1.109×   [→ from Efficiency]
  └── Operating Profit Margin: 29.72%  [→ from Efficiency]
```

**4-Factor ROE:**
```
ROE (Du Pont) = RATIO_leverage × RATIO_asset_turnover
                × RATIO_operating_profit_margin × RATIO_debt_burden
              = 6.409 × 1.109 × 29.72% × 97.43% = 205.81%

  └── Leverage Ratio:          6.409×  [→ from Leverage]
  └── Asset Turnover:          1.109×  [→ from Efficiency]
  └── Operating Profit Margin: 29.72%  [→ from Efficiency]
  └── Debt Burden:             97.43%  [→ from Leverage]
```

---

# VERIFY

After building the model, confirm the following checks before delivery. Each must pass with zero tolerance.

## Structural Checks

- [ ] **Balance sheet balances:** `BAL_assets_total_2024 − BAL_liabilities_total_2024 − BAL_equity_shareholders_2024 = 0` (FY2024 and FY2023)
- [ ] **Net income ties:** Cash Flow `CASH_net_income` = Income Statement `INC_net` = 113,225
- [ ] **Market cap formula:** `market_capitalization = share_price × shares_outstanding` = 3,443,858.04
- [ ] **NOPAT formula:** `currentYear_after_tax_op_income = INC_net + (1 − tax_rate) × INC_interest_expense` = 116,208.63
- [ ] **NWC formula:** `currentYear_working_capital_net = currentYear_assets_current − currentYear_liabilities_current` = -23,405

## Ratio Spot-Checks (Exact Values)

| Ratio | Expected Output |
|---|---|
| MVA | 3,386,908.04 |
| Market-to-Book | 60.47× |
| EVA | 102,040.20 |
| ROE (start-of-year) | 182.19% |
| ROC (start-of-year) | 73.82% |
| Asset Turnover | 1.109× |
| DSO | 27.54 days |
| Days in Inventory | 10.99 days |
| Times Interest Earned | 36.41× |
| Current Ratio | 0.867× |
| Quick Ratio | 0.559× |
| ROA (Du Pont) | 32.96% |
| ROE (Du Pont) | 205.81% |

## Formula Hygiene

- [ ] Zero formula errors across all tabs (#REF!, #DIV/0!, #VALUE!, #NAME?)
- [ ] All ratio cells reference named ranges — no hardcoded values in formula cells
- [ ] `CALC_` derived inputs are isolated in their own section on the Ratios tab
- [ ] Every tab header row includes "FY2024" / "FY2023" labels
- [ ] Hardcoded assumption cells are blue text; input data cells have yellow background; all formula outputs are black text
- [ ] Cell comments on complex formulas (NOPAT, EVA, Du Pont factors) document the named-range logic

## Improvements to Apply (from Stage 3 Model Review)

- Compute effective tax rate as `INC_taxes / INC_ebt` and display alongside the analyst assumption; flag if delta > 2pp
- Standardize all turnover ratios to use average balances `(CY + PY) / 2`, not start-of-year balances, and label clearly
- Move all `CALC_` intermediates to a dedicated "Derived Inputs" block — remove any derived values embedded inside ratio-specific sections
- Add a `CASH_free_cash_flow` line: `CASH_operating + CASH_capex` = 121,586 for reference in the leverage/coverage section

---

*Source: Apple 10-K FY2024, SEC EDGAR | BUS-314 International Corporate Finance | Shidler College of Business*
