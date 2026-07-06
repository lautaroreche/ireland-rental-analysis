# NOTES

---

## Key decisions
- Geographic level: county. The Location field mixes counties, districts and neighbourhoods. Keeping only rows at county level for a clean comparison; sub-zones are discarded.
- The STATISTIC and UNIT columns are removed during data cleaning since they contain the same value for every record.
- Only records with a plain county name in Location are kept, since the RTB already computes the county-level average when producing the table.
- Aggregated categories in Number of Bedrooms and Property Type are removed; only individual values are kept to avoid double counting.
- Null values in the VALUE field are removed since they correspond to combinations with no official RTB data.
- The analysis of apartment price increases in large urban areas is excluded to keep the focus of the objective; it stays recorded as a possible future analysis (details in Findings).

---

## Open problems / doubts
- [x] Check whether STATISTIC Label has more than one value
- [x] Confirm how counties and sub-zones coexist in Location
- [x] Review the 7 values of Number of Bedrooms and 6 of Property Type to confirm whether any category aggregates others (totals, ranges)
- [x] Confirm whether the 26 Irish counties exist as standalone values in addition to the "neighbourhood – county" format

---

## Findings
- STATISTIC Label has a single value for every record: "RTB Average Monthly Rent Report".
- Each Location has exactly 2,310 possible records, resulting from combining Quarter, Number of Bedrooms and Property Type — regardless of whether the value is populated, blank or null.
- Some fields contain categories that aggregate other categories, either as ranges or totals. For example, in Property Type the option "All property types" covers every individual type (Apartment, Detached house, Semi detached house, Terrace house and Other flats). The same happens in Number of Bedrooms, where options such as "1 to 3 bed" overlap with "One bed", "Two bed" and "Three bed".
- The 26 counties exist as standalone values, confirming the decision to work at county level.
- Semi-detached houses grew the most in price, by 134% between 2012 and 2025, above the general average of 124%. The type that grew the least was Apartment, at 112.87%. The spread between the top and bottom is narrow, so the overall reading is that every property type grew strongly and fairly evenly.
- Possible future analysis: at national level Apartment is the type that grew the least over the period, but this pattern reverses in large urban centres like Dublin, Cork and Galway, where Apartment becomes the type with the highest rent increase. Hypothesis: strong demand for this type of housing in large cities. Not verified in this analysis; left for a separate future analysis.
- The most affordable county for family housing (3+ beds) is Donegal. Hypothesis: explained by its distance from major urban and economic centres. Not verified with this dataset, which only contains rent data.
- Dublin is the county with the highest average rent over the period and grows more than proportionally compared to counties like Donegal. This gap widens further when filtering for family homes (3+ beds). (Pending: quantify the gap with a concrete number to close the secondary question.)

---

## Logs

### 18/06/2026
- Downloaded the RIQ02 dataset from the CSO in CSV format.
- Columns: STATISTIC Label, Quarter, Number of Bedrooms, Property Type, Location, UNIT, VALUE.
- Detected that the Location field mixes geographic levels, since the file covers national data including counties, districts and neighbourhoods. Decided to keep the county level for the scale of the analysis, discarding sub-zones.

### 21/06/2026
- Confirmed that the 26 counties exist as standalone values in the Location field.

### 22/06/2026
- Cleaned the data using Power Query. The STATISTIC and UNIT columns were removed, the VALUE field was set to currency type, and rows whose Location did not exactly match one of the 26 Irish counties were discarded.
- Aggregated categories in Number of Bedrooms and Property Type were removed; only individual values were kept to avoid double counting.
- Null values in the VALUE field were removed since they were combinations with no official RTB data.
- The Quarter column was split in two: Year and Quarter.

### 24/06/2026
- Built the dashboard in Power BI using a Windows 11 virtual machine.
- Created the calculated measure for average rent by location; Dublin has the highest value by a clear margin.

### 29/06/2026
- Continued the Power BI dashboard on a Windows 11 environment without a virtual machine.
- Created calculated measures to obtain average rents, the general average for the first and last year, and the property type with the highest increase.
- Detected a possible future analysis, explained in Findings.
- Both main hypotheses of the analysis were answered.