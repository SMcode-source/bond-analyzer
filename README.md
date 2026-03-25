# Bond Portfolio Analyzer

A single-file web app for analyzing corporate and government bond portfolios. Upload a CSV of bonds, calculate implied yield to maturity (YTM), and compare owned vs available bonds with similarity matching.

## Features

- **CSV Upload** — Drag & drop or browse for your bond data
- **YTM Calculation** — Newton-Raphson solver computes implied yield to maturity for each bond
- **Owned vs Available** — Toggle ownership per bond; filter and compare the two groups
- **Similarity Matching** — Bonds are scored against each other using weighted factors (maturity 30%, yield 30%, coupon 20%, type 20%) and the top matches are shown inline
- **Side-by-Side Comparison** — Click any similar bond tag to see a detailed comparison panel with yield/price differentials
- **Sort, Search, Filter** — Sort by any column, free-text search, filter by ownership status and bond type
- **Add Bonds Manually** — Use the built-in form to add individual bonds
- **Export** — Download the full table including computed YTM as a CSV

## CSV Format

Your CSV should have these columns (header names are flexible):

```
Name, Type, Coupon(%), Maturity, FaceValue, Price, Owned
```

| Column | Description | Example |
|--------|-------------|---------|
| Name | Bond identifier | `Apple Inc 2030` |
| Type | `Corporate` or `Government` | `Corporate` |
| Coupon(%) | Annual coupon rate as percentage | `4.50` |
| Maturity | Maturity date (YYYY-MM-DD) | `2030-06-15` |
| FaceValue | Par/face value in dollars | `1000` |
| Price | Current market price in dollars | `985.50` |
| Owned | Whether you hold this bond | `Yes` or `No` |

## Sample Data

The included `sample_bonds.csv` contains 179 bonds:
- 126 Corporate bonds (from 70 issuers including Apple, Microsoft, JPMorgan, etc.)
- 53 Government bonds (US Treasury, UK Gilt, German Bund, Japan JGB, etc.)
- 71 marked as owned, 108 as available
- Maturities ranging from 2026 to 2056
- Coupons from 0.1% to 8.5%

## Usage

1. Open `bond-analyzer.html` in any modern browser
2. Upload your CSV or click **"Load sample data"** to try the built-in demo
3. Toggle the **Owned / Available** filters to focus your view
4. Click **similar bond tags** on any row to compare side-by-side
5. Check/uncheck the **Own** checkbox to reclassify bonds

## YTM Calculation

Yield to maturity is computed using the Newton-Raphson iterative method, solving for the discount rate `y` in:

```
Price = Σ(Coupon / (1+y)^t) + FaceValue / (1+y)^n
```

where `t` ranges from 1 to `n` (years to maturity). The solver converges to 10 decimal places within 200 iterations.

## License

MIT
