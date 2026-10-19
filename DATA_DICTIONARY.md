# Cleaned data dictionary - version 1.0.2

Storage types below are inferred on CSV reload; dates and nullable features require explicit parsing. Blank fields represent missing or inapplicable information.

## 23L_2528_A2_netflix_cleaned.csv

| Column | CSV-inferred dtype | Meaning |
|---|---|---|
| `show_id` | str | Unique title identifier; exclude from analytical features. |
| `type` | str | Movie or TV Show; determines duration units. |
| `title` | str | Title text; label for interpretation and record review. |
| `director` | str | Comma-separated director memberships or Unknown. |
| `cast` | str | Comma-separated cast memberships or Unknown. |
| `country` | str | Comma-separated country memberships or Unknown. |
| `date_added` | str | Parsed addition date in YYYY-MM-DD; missing retained. |
| `release_year` | int64 | Recorded release year, discrete numeric. |
| `rating` | str | Maturity label, including explicit Unknown. |
| `duration` | str | Repaired duration text with min / Season(s) units. |
| `listed_in` | str | Comma-separated genre memberships. |
| `description` | str | Synopsis text; requires separate text processing. |
| `title_original` | str | Unmodified source value for title; provenance only. |
| `director_original` | str | Unmodified source value for director; provenance only. |
| `cast_original` | str | Unmodified source value for cast; provenance only. |
| `country_original` | str | Unmodified source value for country; provenance only. |
| `date_added_original` | str | Unmodified source value for date_added; provenance only. |
| `rating_original` | str | Unmodified source value for rating; provenance only. |
| `duration_original` | str | Unmodified source value for duration; provenance only. |
| `listed_in_original` | str | Unmodified source value for listed_in; provenance only. |
| `director_was_missing` | bool | Original source missingness flag for director. |
| `cast_was_missing` | bool | Original source missingness flag for cast. |
| `country_was_missing` | bool | Original source missingness flag for country. |
| `rating_was_missing` | bool | Original source missingness flag for rating. |
| `date_added_was_missing` | bool | Original source missingness flag for date_added. |
| `rating_duration_repaired` | bool | True for the three rows with runtime moved from rating. |
| `added_year` | float64 | Calendar year of addition; nullable when date is absent. |
| `added_month` | float64 | Calendar month 1-12 of addition; nullable. |
| `release_decade` | int64 | Release year rounded down to the decade. |
| `release_era` | str | Before 2000, 2000-2009, or 2010-2021 release cohort. |
| `country_count` | float64 | Number of nonempty recorded country memberships; missing for Unknown. |
| `genre_count` | int64 | Number of distinct nonempty genre memberships. |
| `movie_minutes` | float64 | Movie runtime in minutes; missing for TV Shows. |
| `tv_seasons` | float64 | TV season count; missing for Movies. |
| `release_to_addition_gap_raw` | float64 | Addition year minus release year; retains negative anomalies. |
| `negative_gap_flag` | bool | True when raw year gap is negative; False when date is missing. |
| `release_to_addition_gap_years` | float64 | Nonnegative calendar-year gap; missing for negative or absent-date cases. |
| `maturity_group` | str | Coarse nonordinal grouping of observed rating labels. |

## 23L_2528_A2_supermarket_cleaned.csv

| Column | CSV-inferred dtype | Meaning |
|---|---|---|
| `Invoice ID` | str | Unique invoice identifier; not a customer identifier. |
| `Branch` | str | Store code A, B or C; one-to-one with City. |
| `City` | str | Store city; redundant with Branch. |
| `Customer type` | str | Member or Normal transaction segment. |
| `Gender` | str | Recorded gender category. |
| `Product line` | str | Product category for invoice. |
| `Unit price` | float64 | Price per unit in unspecified source currency units. |
| `Quantity` | int64 | Whole-number units purchased. |
| `Tax 5%` | float64 | 0.05 × Unit price × Quantity. |
| `Total` | float64 | 1.05 × Unit price × Quantity, tax-inclusive. |
| `Date` | str | Parsed transaction date, exported with midnight clock component. |
| `Time` | str | Parsed clock time, exported as HH:MM:SS. |
| `Payment` | str | Cash, Credit card or Ewallet. |
| `Cost of goods sold` | float64 | Equals Unit price × Quantity in supplied data. |
| `Gross margin percentage` | float64 | Constant approximately 4.7619; no observed variance. |
| `Gross income` | float64 | Equals Tax 5%; mathematically redundant. |
| `Customer stratification rating` | float64 | Observed customer rating, 4.0-10.0; official scale unspecified. |
| `Date_original` | str | Unmodified source value for Date; provenance only. |
| `Time_original` | str | Unmodified source value for Time; provenance only. |
| `transaction_datetime` | str | Combined parsed date and clock time; no timezone supplied. |
| `hour` | int64 | Transaction hour, observed 10-20. |
| `weekday_number` | int64 | Monday=0 through Sunday=6. |
| `weekday` | str | English weekday name. |
| `month` | int64 | Calendar month number, observed 1-3. |
| `month_name` | str | English month name. |
| `is_weekend` | bool | True for Saturday or Sunday. |
| `time_period` | str | Morning 10-12, Afternoon 13-16, Evening 17-20. |

