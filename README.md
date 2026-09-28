# 2024 Election: Ward Estimates

Estimates of party vote shares at the **2024 UK general election**, covering **7,993 census wards across Great Britain**.

**[Download the estimates (CSV)](https://github.com/jackobailey/ward_mrp/raw/refs/heads/main/_output/ward_ge2024_results.csv)** · 47,376 rows · 95% uncertainty intervals

> **Geography:** These estimates use **2022 census ward boundaries**, which may differ from those in use at the 2024 election. Northern Ireland is not included.

## About the estimates

I use **multilevel regression and poststratification (MRP)** to combine Wave 29 of the British Election Study Internet Panel with census data from England and Wales (2021) and Scotland (2022).

1. **Model vote choice.** Predict each respondent's party choice using age group, sex, ethnicity, religion, education, housing tenure, socio-economic class (NS-SEC), and economic activity. The model also includes constituency-level 2024 election results and varying effects for wards, constituencies, and government office regions.
2. **Weight to local populations.** Weight predictions to each ward's census demographic profile using the same demographic variables.
3. **Calibrate to election results.** Adjust vote counts to match known constituency results, accounting for wards that cross constituency boundaries.

Within each constituency and posterior draw, calibration preserves between-ward odds ratios for parties with positive vote targets. It adjusts overall levels while retaining the modelled differences between wards.

## What's in the CSV?

Each row represents a **ward–party combination with a positive estimated vote share**. Exactly zero-share rows are omitted; small positive estimates are retained. Shares and uncertainty bounds are proportions: **0.25 means 25%**.

| Column | Description |
| :--- | :--- |
| `ward`, `ward_name` | ONS ward code and ward name. |
| `pcon`, `pcon_name` | Main constituency code and name; see the note on split wards below. |
| `region` | Government office region; Scotland and Wales are recorded as regions. |
| `party` | Party code, listed below. |
| `est` | Estimated share of valid votes. |
| `lci`, `uci` | Lower and upper bounds of the 95% uncertainty interval. |
| `votes` | Estimated party votes in the ward. |
| `voters` | Estimated total valid votes in the ward, repeated across parties. |

### Party codes

| Code | Party | Code | Party |
| :--- | :--- | :--- | :--- |
| `con` | Conservative | `grn` | Green |
| `lab` | Labour | `snp` | SNP |
| `ld` | Liberal Democrat | `pc` | Plaid Cymru |
| `ref` | Reform UK | `oth` | Other parties and independents |

## Using the estimates

- **Count voters once per ward.** The `voters` value is repeated on every party row, so summing this column across all rows would overcount valid votes.
- **Treat the constituency field as a label.** It identifies the constituency containing the largest share of the ward's census adult population, with exact ties resolved by constituency code. It does not allocate all of a split ward's votes to that constituency. Do not aggregate the CSV by this label to check constituency totals: whole-ward shares cannot recover the separate constituency contributions of split wards.
- **Distinguish calibration from accuracy.** Matching constituency results does not establish ward-level accuracy. These are modelled estimates, with uncertainty bounds supplied in the CSV.
