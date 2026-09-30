# Abigail Ray | Outlier Detection on California Housing

## Objective
I built and compared three outlier detection methods on California Housing data to find and understand data corruption bugs and decide which method actually fits the problem.

## Methodology
- Found and fixed three bugs in a broken outlier detection pipeline: a modified Z-score function that used mean and standard deviation instead of median and MAD, a Tukey fence multiplier set to 1.0 instead of the standard 1.5, and an Isolation Forest contamination parameter set to 0.5 instead of a sensible value like 0.05
- Built an OutlierDetector class that runs modified Z-score, Tukey fences, or Isolation Forest through one interface, checks its own settings for validity, and reports a summary of what it flagged
- Ran all three methods on the MedInc column (and all nine columns for Isolation Forest) and compared how many rows each one flagged
- Used a Venn diagram to see how much overlap there was between the three methods
- Wrote a memo recommending Modified Z-score combined with Isolation Forest, since neither method alone catches every kind of outlier
- Built an interactive dashboard with sliders for each method's parameter, so I could see live how many rows get flagged as I change the settings

## Key Findings
- Modified Z-score on MedInc flagged 400 rows
- Tukey fences on MedInc flagged 681 rows
- Isolation Forest on all nine columns flagged 1032 rows
- All three methods agreed on 322 rows
- Out of 1,336 total unique rows flagged by at least one method, only 34.1% were flagged by two or more methods, showing the three methods disagree a lot because they're answering different questions — the univariate methods only look at one column, while Isolation Forest looks at all nine columns at once and can flag a row for an unusual combination of values even when no single value looks extreme
- Not every flagged row should be removed — some represent real, extreme housing markets that matter to the analysis, not data errors
