# When Should You Post to Hacker News? Probably Whenever.

Dataquest guided project, *Exploring Hacker News Posts*. Dataset: 20,100 Hacker News submissions from a Kaggle dump covering roughly twelve months to September 2016.

Written with the Python standard library plus NumPy and Matplotlib, since this course does not install pandas.

## The two claims

1. **Ask HN posts get more comments than Show HN posts.**
2. **Post at 15:00 US Eastern**, which averages 38.6 comments against a typical hour's 10 to 15.

The first is true and much smaller than it sounds. The second fails a significance test.

## Findings

### 1. Ask HN wins by one comment, and loses on points

| Group | n | Median comments | Median points |
|---|---|---|---|
| Ask HN | 1,744 | **4** | 4 |
| Show HN | 1,162 | 3 | **6** |
| Everything else | 17,194 | 3 | **11** |

The comment difference is real (permutation test, **p = 0.0032**) and worth one comment at the median.

**On points the ranking inverts.** Show HN takes 6 against Ask HN's 4, and ordinary link posts beat both at 11. The formats are not better and worse; asking a question gets replies, showing work gets upvotes, a good link gets more upvotes than either.

### 2. The 3pm result is what chance looks like

| Statistic | Best hour | Value |
|---|---|---|
| Mean | 15:00 | 38.59 |
| Median | 07:00 | 5.5 (n=34) |

**By median, 15:00 scores 3.0, tying with eight other hours of the day.** Its mean is inflated by one 947-comment post supplying 21.2% of the hour's total. At 02:00, second by mean, a single post supplies 62.9%.

The test: shuffle comment counts between posts so posting hour has no effect by construction, then rerun the whole procedure **including the pick-the-best-of-24 step**. Across 2,000 runs the chance best-hour mean reaches 38.59 or higher **12.7% of the time**, with a median of 30.8 and a 95th percentile of 43.8.

**p = 0.127.** Removing one post from the 116 at 15:00 drops that hour by 20%.

A t-test of 15:00 against the other hours would have missed this, because it ignores that 15:00 was chosen *for being the largest*. Only a test that reproduces the selection step answers the question actually being asked.

### 3. The dataset cannot answer the question it is set

**The minimum comment count is 1 and the minimum point count is 1.** Not one of 20,100 posts received zero of either. The full Kaggle dump holds roughly 300,000 posts; this file has 20,100, filtered to submissions that got traction.

Every "what makes a post succeed?" question is therefore asked of a sample with the failures removed. The answerable version is conditional: given a post already got at least one comment and one point, what else is true of it?

### 4. Why means were the wrong tool throughout

Comments have a mean of 24.80 and a median of 3.0, a ratio of **8.3**. The top 1% of posts hold 15.5% of all comments.

This changes the headline: by mean, ordinary link posts get 26.87 comments against Ask HN's 14.04, reversing the project's first conclusion outright. By median they are 3 and 4.

## The practical answer

**Post whenever you like.** Nothing here supports a best hour. For comments, ask a question; for upvotes, post a good link. Both effects are small, and whatever actually determines how a post does is not in this file.

## What I would not claim

- **p = 0.127 is not proof that posting time is irrelevant.** It is a failure to detect an effect in a filtered sample of 1,744 posts, which is a weak test.
- **Timestamps are US/Eastern,** treated as the poster's local clock, which holds only for US posters.
- **One year to September 2016,** on a site that has changed since.
- **Title prefix matching is crude:** a question phrased without the "Ask HN:" prefix counts as "other".
- **The permutation test shuffles outcomes with hours held fixed,** so it tests whether hour predicts comments, not whether different kinds of post are written at different hours.

## Files

- `notebook.ipynb`: full analysis, executed, with two charts.

## Stack

Python standard library (csv, statistics, random, datetime, collections), NumPy, Matplotlib. No pandas.