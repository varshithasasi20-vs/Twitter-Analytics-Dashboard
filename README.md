# Twitter Analytics Dashboard – Power BI Internship Project

## Domain
Data Analytics

## Tool Used
Microsoft Power BI

## Dataset
Twitter Analytics Dataset (Training Project Dataset)

## Project Overview
This project is an extension of the Twitter Analytics training dashboard, developed as part of a Data Analytics internship.
All internship tasks have been implemented as additional report pages using the same dataset, in accordance with internship guidelines.

The dashboard analyzes tweet engagement, interactions, and trends using calculated columns, time-based filters, and business rules.

## Internship Tasks Implemented

**Task 1: Tweet Interaction Breakdown by Category**
- Clustered bar chart showing the sum of URL clicks, user profile clicks, and hashtag clicks grouped by tweet category (Media, Link, Hashtag)
- Includes only tweets with at least one interaction type
- Filters: even tweet date, word count condition
- Visible only 3 PM – 5 PM IST
- **Note:**
  - Word count condition was adjusted from ">40" to ">26" (dataset median)
  - No tweet in the dataset exceeds 36 words
  - This is a data limitation, not an implementation error

**Task 2: Engagement Rate Comparison – App Opens**
- Clustered column chart comparing average engagement rate for tweets with vs. without app opens
- Filters: weekdays, business hours, odd date, even impressions, character count > 30, excludes tweets with capital "D"
- Visible only 12 PM – 6 PM IST and 7 AM – 11 AM IST
- **Note:**
  - 14 tweets satisfy all criteria, all under "Without App Opens"
  - "With App Opens" returns 0 tweets, since only 2 tweets in the dataset have app opens > 0, and both are excluded by the even-impressions filter
  - The dataset contains no tweets with a capital "D," so that exclusion filter has no visible effect, though the logic is implemented correctly

**Task 3: Media Interaction by Day of Week**
- Dual-axis chart (line + column): media views and media engagements by day of week, last quarter of data
- Spike days highlighted via conditional formatting
- Filters: odd date, even impressions, character count > 30, excludes tweets with capital "H"
- Visible only 3 PM – 5 PM IST and 7 AM – 11 AM IST
- **Note:**
  - Spike days are highlighted in red where media views ≥ 141 (the average across the 43 tweets meeting all filter conditions)
  - "Last quarter" was interpreted as the most recent quarter in the dataset (Q4 2020), since the data is historical
  - The dataset contains no tweets with a capital "H," so that exclusion filter has no visible effect, though the logic is implemented correctly

**Task 4: Replies, Retweets, and Likes Comparison**
- Clustered column chart: sum of replies, retweets, and likes
- Filter: tweets posted between June–August 2020
- Simple aggregation, beginner-level task
- **Note:**
  - 752 of 1,166 valid tweets fall within the June–August 2020 range and are reflected in the chart
  - No data limitations were found for this task

**Task 5: Monthly Engagement Rate Trend**
- Line chart: average engagement rate by month
- Two lines: tweets with media vs. without media
- No time-window or complex filters applied
- **Note:**
  - Data spans June–October 2020
  - 435 tweets contain media, 731 do not

**Task 6: Top 10 Tweets by Engagement**
- Clustered bar chart: top 10 tweets by combined retweets + likes, using tweet ID as identifier
- Excludes weekend tweets
- Filters: odd date, even impressions, word count < 30
- Visible only 3 PM – 5 PM IST
- **Note:**
  - The dataset does not contain a username/author column, so the tweet's unique `id` field was used to represent "user profile" per tweet
  - 187 of 1,166 valid tweets meet all row-level filter conditions before the Top 10 selection is applied

## Data Transformations & Calculated Columns
- WordCount_Tx / CharCount_Tx (per-task word and character counts)
- IsOddDate_Tx / IsEvenDate_Tx
- Time-based columns (Time_IST, IsValidRow, IsBizHours_Tx, IsLastQuarter_T3)
- Interaction and category flags (HasAnyInteraction_T1, TweetCategory_T1, AppOpenCategory_T2, HasMedia_T5)
- Text-based exclusion columns (ContainsD_T2, ContainsH_T3)
- Visibility control columns (ShowVisual_T1, ShowVisual_T2, ShowVisual_T3, ShowVisual_T6)
- Aggregation columns (TotalEngagement_T6, IncludeRow_Tx)

## Project Files
- **Power BI Report:** Twitter Analytics Dashboard - Varshitha.pbix
- **Screenshots:** Available in the `screenshots` folder
- **Documentation:** Complete project report available in the `documentation` folder

## Note
Some visuals may appear blank or limited after applying all business constraints due to limited data availability within specific conditions (e.g., strict thresholds like word count > 40, or filters combined with sparse fields such as app opens).
This reflects strict business rules and dataset limitations rather than implementation issues. Full details are documented in the accompanying project report.
