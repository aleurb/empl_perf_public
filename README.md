# Gender Equity in Performance Ratings and Promotions

Exploratory and statistical analysis of whether mid-year performance ratings and promotion decisions are distributed equitably by gender, using synthetic HR data for a fictional company. Built as a take-home exercise for a People Analytics role.

## TL;DR
- On 3,709 eligible employees, there is no statistically significant gender difference in performance ratings (t-test, p = 0.361) or promotion rates (chi-square, p = 0.748).
- Average promotion rate is 9.3% (9.5% non-men vs 9.2% men). Rates vary little by job level (7.6% to 11.0%), role or rank.
- Top-rated employees (rank 5) show a possible gap (11.3% vs 8.0%). It is untested and rests on small groups.
- Gender mix differs strongly by function (about 90% men in Engineering), which is worth monitoring separately.
- Recommendation: standardise evaluation criteria, set a baseline promotion rate with an allowed deviation, and collect more data before acting on sub-group differences.

![Promotion rate by performance rank and gender](img/<your-chart>.png)

## Problem
Leadership wanted to know if ratings and promotions are equitably distributed by gender before finalising a mid-year cycle. The hypothesis was that no gap exists, and the task was to find where one might hide.

## Data
Synthetic HR data for a fictional company: a roster of about 8,000 employees (hire date, job level, function, region, gender, age) and mid-year outcomes (performance rating, promotion decision). The file came from the exercise and is not included in this repository, so the notebook will not run as-is.

Assumptions:
- Source values are correct and need no validation.
- The sample represents the whole population.
- Gender gaps are unknown in advance.
- Employees need at least 1.5 years of tenure on 2023-09-30 to be promotion-eligible.
- **My own assumption:** employees rated 1-2 are excluded as non-performers. The exercise does not require this, and it removes 3,774 rows.

## Method
1. **Prepare:** Recode promotion to a 0/1 flag, rating to a numeric rank, gender to men / non-men, and split job level into role and rank.
2. **Filter:** Each step prints rows removed.

   | Step | Rows removed | Remaining |
   |---|---|---|
   | Merged roster and outcomes | - | 8,012 |
   | Rating below 3 | 3,774 | 4,238 |
   | Tenure under 1.5 years | 510 | 3,728 |
   | Duplicates | 19 | 3,709 |

3. **Explore:** Cross-tabulations and charts by gender, level, function, region and rating.
4. **Test:** t-test on ratings by gender, chi-square on promotion rates by gender.

The first pass used Excel (cross-tabulations, dashboard). It was then automated in Python (pandas, SciPy, seaborn).

## Results
- Mean rating is 3.55 for non-men and 3.57 for men. The difference is not significant.
- Promotion rates by level range from 7.6% (T7) to 11.0% (T6). By role they are 9.2% (I) and 9.6% (T).
- At rating 5, promotion is 11.3% for non-men and 8.0% for men.
- Smaller groups swing more, so sub-group gaps need cautious reading.

## Limitations
- A non-significant result does not prove there is no gap. With a ~9% base rate, small differences are hard to detect.
- "Non-men" combines women and non-binary employees.
- Many comparisons increase the chance of a spurious difference.
- The age range is narrow (27 to 35), and the data covers one cycle.
- The rating filter is an assumption of mine.

## Recommendations
1. Review and standardise performance evaluation criteria.
2. Set a baseline promotion rate and an allowed deviation per group.
3. Review small groups with extra care.
4. Add data to confirm or reject the rank-5 pattern.
5. Move collection and merging into SQL for repeatability.

## Repository
| Path | Description |
|---|---|
| `analysis.ipynb` | Full notebook with outputs |
| `code/` | Python analysis |
| `img/` | Charts |
| `report/` | Executive summary (PDF) |
| `setup.md` | Environment setup |

## Setup
```bash
pip install -r requirements.txt
jupyter notebook analysis.ipynb
```
Requires the original data file, which is not included.

## Author
Aleksandras Urbonas · [LinkedIn](https://www.linkedin.com/in/aleksandrasurbonas/)
