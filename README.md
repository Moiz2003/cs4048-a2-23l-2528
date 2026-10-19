# CS4048 Assignment 2 - cleaned datasets

Abul Moiz Ahmed · 23L-2528 · BCS-7A · FAST-NUCES Lahore

Published **19 October 2026**, version **1.0.2**. These historical datasets are the starting point for Assignment 3 (feature selection and dimensionality reduction).

| Dataset | Rows | Columns | Version |
|---|---:|---:|---|
| [23L_2528_A2_netflix_cleaned.csv](23L_2528_A2_netflix_cleaned.csv) | 8,807 | 38 | 1.0.2 |
| [23L_2528_A2_supermarket_cleaned.csv](23L_2528_A2_supermarket_cleaned.csv) | 1,000 | 27 | 1.0.2 |

Use the immutable [1.0.2 release](https://github.com/Moiz2003/cs4048-a2-23l-2528/releases/tag/1.0.2), not a moving branch, when reproducing this submission. The CSV bytes in the release match those submitted in Assignment2_23L_2528.zip. [Data dictionary](DATA_DICTIONARY.md) · [Machine-readable manifest](manifest.json).

## Original sources

- **Netflix:** Shivam Bansal's [Netflix Movies and TV Shows on Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows). The archive was downloaded directly from Kaggle on 19 October 2026; its netflix_titles.csv has 8,807 rows and 12 columns. Latest recorded addition: 25 September 2021. It is a historical metadata snapshot, not current availability or viewing data.
- **Supermarket:** the exact instructor-provided supermarket_Sales.csv, supplied locally as supermarket_Sales - supermarket_Sales.csv. It has 1,000 rows and 17 columns covering 1 January-30 March 2019. No alternate web dataset was substituted. The source uses the full names Customer stratification rating, Cost of goods sold, Gross margin percentage and Gross income.

Original byte checksums (SHA-256):

```text
df1f4ad2027a5a14c3a33932ef0d4054565ff88adf92b7f263601b70fdc6f3f3  netflix_titles.csv
2db574a0ccc6828fe5f541ee3e7f2a7ce2604edb270e48a90c6a35b804178397  supermarket_Sales - supermarket_Sales.csv
```

The submitted notebook embeds losslessly compressed original CSV bytes and checks these hashes, allowing the four-file submission to execute offline. Dataset authorship and upstream terms remain with the original sources; no new license is asserted for third-party data.

## Netflix cleaning

1. Retain all 8,807 titles; exact row, show_id and title duplicate checks found none.
2. Preserve original title, director, cast, country, date_added, rating, duration and listed_in values in *_original fields. Add original-missing flags for director, cast, country, rating and date_added.
3. Trim outer whitespace; normalize comma-delimited credit/country/genre tokens, drop empty tokens and deduplicate exact repeated memberships while preserving order. Seven country strings contain empty tokens.
4. Move three movie runtimes (74 min, 84 min, 66 min) out of rating into their missing durations; flag those rows. The original four missing ratings plus these three become Unknown.
5. Use Unknown for missing director (2,634), cast (825), country (831) and maturity; do not invent values. Missing country_count is left blank, not zero.
6. Parse addition dates; retain 10 absent dates as missing. Derive added_year, added_month, release_decade and release_era.
7. Separate movie_minutes from tv_seasons; the inapplicable column is missing. Derive country_count and genre_count from nonempty memberships.
8. Preserve raw addition-year minus release-year gap. Flag 14 negatives and exclude only those values from release_to_addition_gap_years. Missing dates also yield missing gaps; no title is dropped.
9. Map maturity labels to descriptive Adult, Teen, General/family, Children and Unrated/unknown groups. This is not a universally equivalent or ordinal maturity scale.
10. Retain plausible extreme runtimes, season counts and years after IQR and record inspection.
11. In version 1.0.2, replace 284 U+2014 em dashes in description text with ASCII hyphens at the student's request. This is a formatting change, not an error correction; the notebook's embedded original source bytes are unchanged.

## Supermarket cleaning

1. Retain all 1,000 rows. Missing values, blank placeholders, duplicate records, duplicate IDs, categorical inconsistencies and parse failures were all zero.
2. Parse month-first Date and clock Time, retain Date_original and Time_original, and add transaction_datetime, hour, weekday_number, weekday, month, month_name, is_weekend and time_period.
3. Time periods are Morning (10-12), Afternoon (13-16), Evening (17-20). These are analytical bins with unequal lengths, not verified opening hours.
4. Retain nine high-total IQR flags: their prices/quantities are plausible and all obey Total = 1.05 × Unit price × Quantity. Arithmetic consistency does not prove real-world authenticity.
5. Preserve all monetary columns and document dependence: COGS = price × quantity, Tax = 0.05 × COGS, Total = COGS + Tax, Gross income = Tax, margin = 100 × Gross income / Total. All six checks have zero mismatches. Margin is constant at about 4.7619%; City maps one-to-one to Branch.
6. No imputation, capping or numerical corrections were applied. Units of currency and the official rating scale are not documented by the supplied CSV.

## Assignment 3 usage

CSV does not retain Python types: parse date/datetime fields explicitly, read IDs as strings, and use nullable integer features where blanks mean unknown or inapplicable. Multi-country/genre memberships overlap; explode before membership counts. Unknown is a recorded missing-category marker, not a country or genre. Exclude identifiers and provenance copies from ordinary numeric feature matrices. Avoid treating derived monetary fields, constant margin, paired Branch/City, or overlapping time features as independent information. Scale and encode appropriate variables deliberately.

## Version preservation

Version 1.0.2 is fixed. The previous 1.0.0 release remains available unchanged. Version 1.0.2 changes only Netflix description punctuation and the related documentation/version identifiers; the supermarket CSV is unchanged. Any later corrections must use a new version/tag and a documented changelog; do not replace or delete either release before grading completes. The public repository must remain accessible through grading. Work proceeds from development on feat/* or bugfix/* branches, with pull requests to development, and a tagged production release on master.

## Submitted CSV checksums

```text
5b22ac67471051e28463675210b6f4af77e77ebdd969126a9c11c47b1579642d  23L_2528_A2_netflix_cleaned.csv
7609d9bb8f952c7c7339747c97e11f1a782069d523df92a308bc1b17ee61fe66  23L_2528_A2_supermarket_cleaned.csv
```

## Validation

The full notebook executes 38 code cells with 25 saved figures, checks source checksums, row/key preservation, transformations, formula consistency and CSV round trips. The compulsory four-page PDF contains five insights and a <=150-word handoff for each dataset. Calculations and figures are reproducible in the submitted notebook.
