# Tweet Analytics Dashboard — Task Report

**Prepared for:** Internship Final Submission
**Scope:** Six Power BI / DAX-based visualizations analyzing tweet engagement, interaction, and performance patterns.

---

## Task 1 — Tweet Interaction Breakdown by Category

**Objective:** Sum of URL clicks, user profile clicks, and hashtag clicks grouped by tweet category, including only tweets with at least one interaction and an even tweet date.

**Columns**

| Column | Description |
|---|---|
| Time_IST | Converts tweet time from UTC to IST |
| IsValidRow | Checks if the row has valid, readable time data |
| WordCount_T1 | Counts total words in the tweet |
| IsEvenDate_T1 | Checks if tweet date (day) is an even number |
| IsWordCountOK_T1 | Checks if word count is above 26 |
| TweetCategory_T1 | Labels tweet as "Media", "Link", or "Hashtag" |
| HasAnyInteraction_T1 | Checks if tweet has at least one interaction (URL/profile/hashtag click) |
| IncludeRow_T1 | Combines all above conditions into one final filter |
| ShowVisual_T1 | Controls chart visibility (only 3–5 PM IST) |

**Chart:** Clustered Bar Chart
- Axis: `TweetCategory_T1`
- Values: Sum of URL clicks, user profile clicks, hashtag clicks

**Filters on Visual:** `IncludeRow_T1 = 1`, `ShowVisual_T1 = 1`

**Note:** The original condition "word count > 40" was adjusted to "word count > 26" (dataset median), since no tweet in the dataset has more than 36 words. Applying ">40" as specified would return zero rows for every visual. This is a data limitation, not an implementation error.

---

## Task 2 — Engagement Rate Comparison (App Opens vs. No App Opens)

**Objective:** Compare engagement rate of tweets with app opens vs. without app opens.

**Columns**

| Column | Description |
|---|---|
| IsWeekday_T2 | Checks if tweet was posted on a weekday (Mon–Fri) |
| IsBizHours_T2 | Checks if tweet was posted between 9 AM–5 PM |
| IsOddDate_T2 | Checks if tweet date (day) is an odd number |
| IsImpEven_T2 | Checks if impressions count is an even number |
| CharCount_T2 | Counts total characters in the tweet |
| IsCharOK_T2 | Checks if character count is above 30 |
| ContainsD_T2 | Checks if tweet text contains capital "D" |
| AppOpenCategory_T2 | Labels tweet as "With App Opens" or "Without App Opens" |
| IncludeRow_T2 | Combines all above conditions into one final filter |
| ShowVisual_T2 | Controls chart visibility (only 12–6 PM & 7–11 AM IST) |

**Chart:** Clustered Column Chart
- Axis: `AppOpenCategory_T2`
- Values: Average of engagement rate

**Filters on Visual:** `IncludeRow_T2 = 1`, `ShowVisual_T2 = 1`

**Note:** After applying all filters, 14 tweets satisfy the criteria — all under "Without App Opens." "With App Opens" returns 0 tweets, since only 2 tweets in the dataset have app opens > 0, and both have odd impressions, which get excluded by the even-impressions filter. This is a data limitation, not an implementation error. Additionally, the dataset contains no tweets with a capital letter "D", so the "exclude tweets containing D" filter returns 0 exclusions — the logic is implemented correctly but has no visible effect on this specific dataset.

---

## Task 3 — Media Interaction by Day of Week

**Objective:** Dual-axis chart comparing media views and media engagements by day of week, filtered to the last quarter.

**Columns**

| Column | Description |
|---|---|
| DayOfWeek_T3 | Extracts day name (Monday, Tuesday, etc.) from tweet time |
| DayOfWeekNum_T3 | Assigns a number (1–7) to each day for correct sorting |
| CharCount_T3 | Counts total characters in the tweet |
| IsOddDate_T3 | Checks if tweet date (day) is an odd number |
| IsImpEven_T3 | Checks if impressions count is an even number |
| IsCharOK_T3 | Checks if character count is above 30 |
| ContainsH_T3 | Checks if tweet text contains capital "H" |
| IsLastQuarter_T3 | Checks if tweet falls in the most recent quarter of the dataset |
| IncludeRow_T3 | Combines all above conditions into one final filter |
| ShowVisual_T3 | Controls chart visibility (only 3–5 PM & 7–11 AM IST) |

**Chart:** Line and Clustered Column Chart
- X-axis: `DayOfWeek_T3`
- Column Y-axis: Sum of media views
- Line Y-axis: Sum of media engagements

**Filters on Visual:** `IncludeRow_T3 = 1`, `ShowVisual_T3 = 1`

**Note:** Spike days are highlighted in red using rule-based conditional formatting, where media views ≥ 141 (the average across the 43 tweets meeting all filter conditions). Days at or below this average are shown in blue. "Last quarter" was interpreted as the most recent quarter present in the dataset (Q4 2020), since the data is historical rather than live. Additionally, the dataset contains no tweets with a capital letter "H", so the "exclude tweets containing H" filter returns 0 exclusions — the logic is implemented correctly but has no visible effect on this specific dataset.

---

## Task 4 — Replies, Retweets, and Likes Comparison

**Objective:** Compare replies, retweets, and likes using SUM aggregation, filtered to tweets posted between June and August 2020.

**Columns**

| Column | Description |
|---|---|
| IsJunAug2020_T4 | Checks if tweet was posted between June 1, 2020 and August 31, 2020 |

**Chart:** Clustered Column Chart
- No axis category
- Values: Sum of replies, Sum of retweets, Sum of likes

**Filters on Visual:** `IsJunAug2020_T4 = 1`

**Note:** This task did not require a visibility time window or complex row-level logic, per the original task specification. 752 of 1,166 valid tweets fall within the June–August 2020 range and are reflected in the chart. No additional data limitations were found for this task.

---

## Task 5 — Monthly Engagement Rate Trend

**Objective:** Line chart trend of average engagement rate by month, separated into tweets with media vs. without media.

**Columns**

| Column | Description |
|---|---|
| MonthName_T5 | Extracts month name (Jun, Jul, etc.) from tweet time |
| MonthNum_T5 | Assigns a number (1–12) to each month for correct sorting |
| HasMedia_T5 | Labels tweet as "With Media" or "Without Media" based on media views |

**Chart:** Line Chart
- X-axis: `MonthName_T5`
- Legend: `HasMedia_T5`
- Values: Average of engagement rate

**Filters on Visual:** None (no visibility window or complex filtering required, per task specification)

**Note:** This task did not require time-based visibility or row-level filters, per the original specification. Data spans June–October 2020, with 435 tweets containing media and 731 without.

---

## Task 6 — Top 10 Tweets by Engagement

**Objective:** Identify top 10 tweets by combined retweets and likes, excluding weekend tweets, with associated tweet identifiers displayed.

**Columns**

| Column | Description |
|---|---|
| WordCount_T6 | Counts total words in the tweet |
| IsWeekday_T6 | Checks if tweet was posted on a weekday (Mon–Fri) |
| IsOddDate_T6 | Checks if tweet date (day) is an odd number |
| IsImpEven_T6 | Checks if impressions count is an even number |
| IsWordCountOK_T6 | Checks if word count is below 30 |
| TotalEngagement_T6 | Sum of retweets and likes for each tweet |
| IncludeRow_T6 | Combines all above conditions into one final filter |
| ShowVisual_T6 | Controls chart visibility (only 3–5 PM IST) |

**Chart:** Clustered Bar Chart
- Axis: `id`
- Values: Sum of `TotalEngagement_T6`
- Top N Filter: Top 10 by `TotalEngagement_T6`

**Filters on Visual:** `IncludeRow_T6 = 1`, `id` (Top N: 10 by Sum of `TotalEngagement_T6`), `ShowVisual_T6 = 1`

**Note:** The dataset does not contain a username or author column, so the tweet's unique `id` field was used to represent "user profile" per tweet, as specified in the task limitations. 187 of 1,166 valid tweets meet all row-level filter conditions before the Top 10 selection is applied.

---

## Summary of Data Limitations Across Tasks

| Task | Limitation | Resolution |
|---|---|---|
| 1 | Word count > 40 returns 0 rows (max word count is 36) | Threshold adjusted to > 26 (dataset median) |
| 2 | "With App Opens" returns 0 tweets after filtering | Documented as a data limitation; logic verified correct |
| 2 | No tweets contain capital "D" | Filter has no visible effect but is implemented correctly |
| 3 | No tweets contain capital "H" | Filter has no visible effect but is implemented correctly |
| 3 | "Last quarter" not defined for historical data | Interpreted as most recent quarter in dataset (Q4 2020) |
| 6 | No username/author column available | Tweet `id` used as the unique profile identifier |

---

*End of Report*
