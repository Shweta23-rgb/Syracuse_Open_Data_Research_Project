# Syracuse_Open_Data_Research_Project

# Syracuse Winter Vulnerability Index

A data-driven tool to identify Syracuse neighborhoods most in need of weatherization assistance based on heating violations, rental compliance, economic vulnerability, and housing age.

---

## Project Overview

**Research Question:** Which Syracuse neighborhoods have the most vulnerable housing that needs weatherization help?

**Approach:** Integrated three public datasets to create a composite vulnerability score (0-100) for each neighborhood, combining infrastructure failures, landlord accountability, economic hardship, and building age.

---

## Data Sources

All data was collected from publicly available sources:

1. **Code Violations** (Syracuse Open Data Portal)
   - Dataset: Code Violations V2 (2017-2025)
   - 137,663 total violations → filtered to 1,647 heating-related violations
   - Used to identify neighborhoods with persistent heating problems

2. **Rental Registry** (Syracuse Open Data Portal)
   - Dataset: Syracuse Rental Registry (2024)
   - 11,085 rental properties analyzed
   - Used to measure landlord compliance with rental registration requirements

3. **Census Data** (U.S. Census Bureau)
   - Source: American Community Survey 5-Year Estimates (2019-2023)
   - Tables: DP03 (Economic Characteristics) and DP04 (Housing Characteristics)
   - 69 Census tracts mapped to 35 Syracuse neighborhoods
   - Used to measure economic vulnerability and housing age

---

## Methodology

### Phase 1: Data Collection & Cleaning
- Downloaded datasets from Syracuse Open Data Portal and Census Bureau
- Filtered code violations for heating-related issues (space heating + water heating)
- Mapped rental properties to neighborhoods using property identifiers (SBL)
- Performed spatial join to aggregate Census tract data to neighborhood level

### Phase 2: Individual Risk Scoring
Each dataset was analyzed independently and scored on a 0-1 scale:

**Heating Risk Score:**
- Historical risk: Based on total violations and unique addresses affected
- Current risk: Based on number of open/unresolved violations

**Rental Risk Score:**
- Combined rental property concentration and landlord non-compliance rate
- Higher concentration + higher non-compliance = higher risk

**Economic Vulnerability Score:**
- Scaled poverty rate, SNAP usage, and inverse of median household income
- Higher poverty and SNAP usage = higher vulnerability

**Housing Age Score:**
- Weighted combination of housing built before 1980 and before 1960
- Older housing = worse insulation and heating systems

### Phase 3: Data Integration
- Merged all three datasets using neighborhood name as the join key
- Resolved naming conflicts (e.g., "Hawley Green" vs "Hawley-Green")
- Final dataset: 32 neighborhoods, 28 with complete data across all sources

### Phase 4: Final Vulnerability Index
Combined all four risk scores using weighted formula:
```
Final Score = (Heating Risk × 25) + (Rental Risk × 20) + 
              (Economic Vulnerability × 25) + (Housing Age × 30)
```

Result: 0-100 vulnerability score for each neighborhood

---

## Key Findings

**Top 3 Most Vulnerable Neighborhoods:**
1. Northside
2. Near Westside
3. Brighton

**Patterns Identified:**
- Northside accounts for 19.5% of all heating violations citywide
- 68% of heating violations remain unresolved
- Strong correlation (0.70) between heating violations and rental non-compliance
- Neighborhoods with high heating violations also show elevated poverty rates
- 87% of heating violations are space heating (furnace/heating system failures)

## Visualizations

**Created 11 total visualizations:**
- 4 for heating violations analysis
- 3 for rental registry analysis
- 4 for final vulnerability index

All visualizations saved as high-resolution PNG files (300 DPI).

---

## Tools & Technologies

- **Python** (data cleaning, analysis, visualization)
  - pandas, numpy (data manipulation)
  - matplotlib, seaborn (visualizations)
- **R** (Census data acquisition)
  - tidycensus (Census API access)
  - sf (spatial mapping)

---

## Limitations

- 28% of rental properties could not be mapped to neighborhoods (no violations history)
- Code violations data may undercount heating problems (not all issues get reported)
- Census tract boundaries don't perfectly align with neighborhoods (requires aggregation)
- 4 neighborhoods have incomplete data (missing either Census or violations data)

---

## Use Cases

This index can be used by:
- City housing departments to prioritize weatherization funding
- Community organizations to target intervention programs
- Researchers studying housing vulnerability patterns
- Policy makers designing heating assistance programs

