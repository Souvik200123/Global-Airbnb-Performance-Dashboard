# DAX Measures & Calculated Columns

This document contains the main DAX calculations used in the **Global Airbnb Performance Dashboard** built with Microsoft Power BI.

The calculations cover KPI development, room-type analysis, ratings, city ranking, reviewer analysis, cumulative calculations, and Pareto-style review-frequency analysis.

---

## 1. Listing KPIs

### Total Listings

Counts the unique Airbnb listings in the dataset.

```DAX
Total Listing =
DISTINCTCOUNT(Listings[listing_id])
```

---

## 2. Room-Type Analysis

The following calculations count listings for specific room types.

### Private Room

```DAX
Private Room =
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[room_type] = "Private room"
)
```

### Entire Place

```DAX
Entire Place =
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[room_type] = "Entire place"
)
```

### Hotel Room

```DAX
Hotel Room =
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[room_type] = "Hotel room"
)
```

### Shared Room

```DAX
Shared Room =
CALCULATE(
    COUNT(Listings[listing_id]),
    Listings[room_type] = "Shared room"
)
```

> 
---

## 3. Rating Analysis

Average customer scores are calculated for different service dimensions.

### Accuracy

```DAX
Accuracy =
AVERAGE(Listings[review_scores_accuracy])
```

### Communication

```DAX
Communication =
AVERAGE(Listings[review_scores_communication])
```

### Location

```DAX
Location =
AVERAGE(Listings[review_scores_location])
```

### Value

```DAX
Value =
AVERAGE(Listings[review_scores_value])
```

### Cleanliness

```DAX
Cleanliness =
AVERAGE(Listings[review_scores_cleanliness])
```

These measures allow cities and listings to be compared across multiple customer-rating dimensions.

---

## 4. City Ranking

Ranks cities according to the total number of listings.

```DAX
City Rank =
RANKX(
    ALL(Listings[city]),
    [Total Listing],
    ,
    DESC,
    DENSE
)
```

### Explanation

- `ALL(Listings[city])` removes the current city filter.
- `[Total Listing]` provides the metric being ranked.
- `DESC` ranks the highest listing count first.
- `DENSE` prevents gaps in ranking when values are tied.

---

## 5. Reviewer Analysis

### Reviews per Reviewer

This is a **calculated column**, not a measure.

It calculates how many reviews are associated with each reviewer.

```DAX
Reviews per Reviewer =
CALCULATE(
    COUNT(Reviews[review_id]),
    ALLEXCEPT(
        Reviews,
        Reviews[reviewer_id]
    )
)
```

### Reviewers

Counts unique reviewers.

```DAX
Reviewers =
DISTINCTCOUNT(Reviews[reviewer_id])
```

### Total Reviewers

Calculates the overall unique reviewer population while removing the review-frequency filter.

```DAX
Total Reviewers =
CALCULATE(
    DISTINCTCOUNT(Reviews[reviewer_id]),
    REMOVEFILTERS(Reviews[Reviews per Reviewer])
)
```

---

## 6. Cumulative Reviewer Analysis

### Cumulative Reviewers

Calculates the cumulative number of reviewers up to the current review-frequency category.

```DAX
Cumulative Reviewers =
VAR CurrentReviews =
    MAX(Reviews[Reviews per Reviewer])
RETURN
CALCULATE(
    [Reviewers],
    FILTER(
        ALL(Reviews[Reviews per Reviewer]),
        Reviews[Reviews per Reviewer] <= CurrentReviews
    )
)
```

### Cumulative % Review Frequency

Calculates the cumulative percentage of reviewers.

```DAX
Cumulative % Review Frequency =
DIVIDE(
    [Cumulative Reviewers],
    [Total Reviewers]
)
```

This measure is formatted as **Percentage** in Power BI, typically with one decimal place.

---

## 7. Review-Frequency Chart Filter

This calculated column is used to control which review-frequency categories are displayed in the Pareto-style chart.

```DAX
Show in Review Frequency Chart =
IF(
    Reviews[Reviews per Reviewer] <= 6
        || Reviews[Reviews per Reviewer] > 85,
    1,
    0
)
```

The column can be added to the visual-level filter and set to:

**is 1**

This keeps the chart readable while retaining the selected low-frequency and high-frequency categories.

---

## 8. Common DAX Functions Used

| Function | Purpose |
|---|---|
| `CALCULATE()` | Changes filter context before evaluating an expression |
| `COUNT()` | Counts values in a column |
| `COUNTROWS()` | Counts rows in a table |
| `DISTINCTCOUNT()` | Counts unique values |
| `AVERAGE()` | Calculates the arithmetic mean |
| `FILTER()` | Returns a filtered table |
| `ALL()` | Removes filters from a table or column |
| `ALLEXCEPT()` | Removes filters except those specified |
| `REMOVEFILTERS()` | Explicitly removes filters |
| `RANKX()` | Calculates rankings |
| `DIVIDE()` | Performs division safely |
| `IF()` | Applies conditional logic |
| `MAX()` | Returns the maximum value in the current context |
| `VAR` | Stores an intermediate calculation |

---

## 9. DAX Concepts Demonstrated

The project demonstrates practical understanding of:

- Measures vs. calculated columns
- Filter context
- Context modification with `CALCULATE`
- Removing and preserving filters
- Ranking
- Aggregation
- Conditional logic
- Cumulative calculations
- Percentage calculations
- Reviewer segmentation
- Pareto-style analysis

---

## 10. Important Implementation Notes

### Measures vs. Calculated Columns

`Reviews per Reviewer` is intentionally a **calculated column** because the review frequency needs to exist at the reviewer-row level and be used as a category in the review-frequency analysis.

`Reviewers`, `Total Reviewers`, `Cumulative Reviewers`, and `Cumulative % Review Frequency` are **measures** because their values need to respond dynamically to the visual's filter context.

### Formatting

For:

```DAX
Cumulative % Review Frequency
```

use:

**Measure tools → Format → Percentage**

and set the desired number of decimal places.

---

## 11. Dashboard Visual Mapping

### Review Frequency Pareto Chart

**Visual:** Line and clustered column chart

**X-axis:**
```text
Reviews per Reviewer
```

**Column Y-axis:**
```text
Reviewers
```

**Line Y-axis:**
```text
Cumulative % Review Frequency
```

This creates a Pareto-style visualization showing reviewer frequency as columns and cumulative reviewer percentage as the line.

---

## 12. Project Skills Demonstrated

This DAX implementation demonstrates practical Power BI skills in:

- Data aggregation
- KPI development
- Filter-context management
- Calculated columns
- Measures
- Ranking
- Segmentation
- Cumulative analysis
- Percentage calculations
- Interactive dashboard development
- Business-oriented data visualization

