# 2024 UK General Election: Ward-Level MRP Estimates

<img src="_output/ward_mrp_hex.png" align="right" width="190" alt="Ward MRP 2024 hex sticker with a stylised map of Great Britain in party colours">

[![CSV downloads](https://img.shields.io/github/downloads/jackobailey/ward_mrp/ward_ge2024_results.csv?displayAssetName=false&label=CSV%20downloads&color=0969da)](https://github.com/jackobailey/ward_mrp/releases)

This repository includes MRP estimates of each of the major party's vote shares in all **7,993 2022 census wards in Great Britain** at the **2024 UK general election**. Due to its different party system, Northern Ireland is not included.

**[Click here to download the estimates (CSV)](https://github.com/jackobailey/ward_mrp/releases/latest/download/ward_ge2024_results.csv)**

## About the estimates

I use **multilevel regression and poststratification (MRP)** to combine Wave 29 of the British Election Study Internet Panel with census data from England and Wales (2021) and Scotland (2022).

The process has three steps:

1. **Model vote choice.** First, I predict each how each respondent in the BES voted based on their age group, sex, ethnicity, religion, education, housing tenure, socio-economic class (NS-SEC), and economic activity, plus the election results in their constituency and information on the ward, constituency, and government office region that they lived in.
2. **Weight to local populations.** Next, I use the model to make predictions, which I then weight to match each ward's census demographic profile using the same demographic variables that I include in the model.
3. **Calibrate to election results.** Finally, I calibrate vote counts in each ward to match known constituency results, accounting for wards that cross constituency boundaries.


## What's in the CSV?

Each row represents a party's result in a given ward.

| Column | Description |
| :--- | :--- |
| `ward`, `ward_name` | ONS ward code and ward name. |
| `pcon`, `pcon_name` | Largest overlapping constituency code and name.|
| `region` | Government office region. |
| `party` | Party code (see below). |
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
