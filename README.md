# UK General Election, 2024: Ward-level Estimates in Great Britain

This repository includes estimates of party vote shares in the 7,993 2022 census ward areas across Great Britain at the 2024 UK general election.

To estimate these figures, I use multilevel regression and poststratification (MRP), combining data from Wave 29 of the British Election Study Internet Panel with census data from England and Wales (2021) and Scotland (2022). The model predicts vote choice based on each respondent's **age group, sex, ethnicity, religion, education, housing tenure, socio-economic class (NS-SEC), and economic activity**, alongside constituency-level 2024 election results and varying effects for each ward, constituency, and government office region.

I weight predictions from each ward according to the area's census demographic profile on the same variables that I include in the model. I then calibrate the vote counts to match the known constituency-level results, accounting for wards that cross constituency boundaries. Within each constituency and posterior draw, calibration preserves between-ward odds ratios for parties with positive vote targets; it adjusts their overall levels while retaining the modelled differences between wards.

The estimates are available in [`_output/ward_ge2024_results.csv`](_output/ward_ge2024_results.csv), with one row for each party with a positive estimated vote share in each ward:

- `ward`, `ward_name`: ONS ward code and ward name.
- `pcon`, `pcon_name`: Code and name of the constituency containing the largest share of the ward's census adult population. Exact ties are resolved by constituency code. This label does not allocate the whole ward's votes to that constituency.
- `region`: Government office region (Scotland and Wales are recorded as regions).
- `party`: `con` (Conservative), `lab` (Labour), `ld` (Liberal Democrat), `ref` (Reform UK), `grn` (Green), `snp` (SNP), `pc` (Plaid Cymru), or `oth` (other parties and independents).
- `est`, `lci`, `uci`: Estimated share of valid votes and lower/upper 95% uncertainty bounds, expressed as proportions from 0 to 1.
- `votes`, `voters`: Estimated party votes and total valid votes in the ward. `voters` is repeated across parties; count it only once per ward.

Rows with exactly zero estimated share are omitted from the CSV; small positive estimates are retained.

Whole-ward shares cannot recover the separate constituency contributions of split wards, so do not aggregate the CSV by its main-constituency label to check constituency totals. Matching constituency totals does not establish ward-level accuracy.

These estimates use 2022 census ward boundaries, which may differ from those in use at the 2024 election. Northern Ireland is not included.
