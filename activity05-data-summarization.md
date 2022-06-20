Activity 5
================
Sajal

## Data and packages

Again, we will load all of the `{tidyverse}` for this Activity.

``` r
library(tidyverse)
```

We continue our exploration of college majors and earnings from the data
behind the FiveThirtyEight story [The Economic Guide To Picking A
College
Major](https://fivethirtyeight.com/features/the-economic-guide-to-picking-a-college-major/).
Remember that there are many considerations that go into picking a
major. Earning potential and employment prospects are two (important) of
these considerations, but they do not tell the entire story.

We read in the same data from Activity 4 below, but notice that this
code is now surrounded in parentheses.

``` r
(college_recent_grads <- read_csv("data/recent-grads.csv"))
```

    ## # A tibble: 173 x 21
    ##     rank major_code major           major_category total sample_size   men women
    ##    <dbl>      <dbl> <chr>           <chr>          <dbl>       <dbl> <dbl> <dbl>
    ##  1     1       2419 Petroleum Engi… Engineering     2339          36  2057   282
    ##  2     2       2416 Mining And Min… Engineering      756           7   679    77
    ##  3     3       2415 Metallurgical … Engineering      856           3   725   131
    ##  4     4       2417 Naval Architec… Engineering     1258          16  1123   135
    ##  5     5       2405 Chemical Engin… Engineering    32260         289 21239 11021
    ##  6     6       2418 Nuclear Engine… Engineering     2573          17  2200   373
    ##  7     7       6202 Actuarial Scie… Business        3777          51  2110  1667
    ##  8     8       5001 Astronomy And … Physical Scie…  1792          10   832   960
    ##  9     9       2414 Mechanical Eng… Engineering    91227        1029 80320 10907
    ## 10    10       2408 Electrical Eng… Engineering    81527         631 65511 16016
    ## # … with 163 more rows, and 13 more variables: sharewomen <dbl>,
    ## #   employed <dbl>, employed_fulltime <dbl>, employed_parttime <dbl>,
    ## #   employed_fulltime_yearround <dbl>, unemployed <dbl>,
    ## #   unemployment_rate <dbl>, p25th <dbl>, median <dbl>, p75th <dbl>,
    ## #   college_jobs <dbl>, non_college_jobs <dbl>, low_wage_jobs <dbl>

Compare this code output to the `load_data` chunk in your knitted
Activity 4 `.md` report. What does enclosing an assignment code (i.e.,
`object_name <- r_code`) in parentheses do?

**Response**: Executes the response into console. Shows the datatable.

### Data Codebook

Descriptions of the variables are again provided below. Again note that
the ACS only asks [one
question](https://www.census.gov/acs/www/about/why-we-ask-each-question/sex/)
about a person’s sexual identity.

| Header                         | Description                                                                 |
|:-------------------------------|:----------------------------------------------------------------------------|
| `rank`                         | Rank by median earnings                                                     |
| `major_code`                   | Major code, FO1DP in ACS PUMS                                               |
| `major`                        | Major description                                                           |
| `major_category`               | Category of major from Carnevale et al                                      |
| `total`                        | Total number of people with major                                           |
| `sample_size`                  | Sample size (unweighted) of full-time, year-round ONLY (used for earnings)  |
| `men`                          | Male graduates                                                              |
| `women`                        | Female graduates                                                            |
| `sharewomen`                   | Women as share of total                                                     |
| `employed`                     | Number employed (ESR == 1 or 2)                                             |
| `employed_full_time`           | Employed 35 hours or more                                                   |
| `employed_part_time`           | Employed less than 35 hours                                                 |
| `employed_full_time_yearround` | Employed at least 50 weeks (WKW == 1) and at least 35 hours (WKHP &gt;= 35) |
| `unemployed`                   | Number unemployed (ESR == 3)                                                |
| `unemployment_rate`            | Unemployed / (Unemployed + Employed)                                        |
| `median`                       | Median earnings of full-time, year-round workers                            |
| `p25th`                        | 25th percentile of earnings                                                 |
| `p75th`                        | 75th percentile of earnings                                                 |
| `college_jobs`                 | Number with job requiring a college degree                                  |
| `non_college_jobs`             | Number with job not requiring a college degree                              |
| `low_wage_jobs`                | Number in low-wage service jobs                                             |

The questions we will answer in this activity are:

-   How do the distributions of median income compare across major
    categories?
-   Do women tend to choose majors with lower or higher earnings?

## Analysis

### Median Earnings Description

### Median … Median Earnings

For the rest of this semester, I will no longer provide you with R code
chunks. Have no fear! There are a number of ways to create a code chunk:

-   Tired: Copy-and-paste a previous code chunk, delete the code, then
    add your new code. **This is likely to create more work for you and
    I strongly encourage you not to use this method.**
-   Wired: Click on the ![new chunk icon](README-img/new-chunk-icon.png)
    and select ![r chunk icon](README-img/r-chunk-icon.png) (notice all
    the different types of code chunks that you can use within an
    RMarkdown file!)
-   Inspired: Ctrl/Command + Alt/Option + I. *This is my preferred
    method.*

1.  Below, create a code chunk and name it `median_earnings`. Make sure
    there is an empty line above and below the code chunk.
2.  In your newly created R code chunk, verify that the median income
    for all majors was $36,000.

-   Specify that you want to use the `college_recent_grads` dataset,
    *then*, using the appropriate functions from `{dplyr}`, obtain the
    *median* summary statistic for the variable “median earnings of
    full-time, year-round workers” (this very wordy variable is simply
    `median` in the dataset).
-   In the appropriate *summarizing* step, refer to your numerical
    summary `median_earnings`.

``` r
median_earnings <- college_recent_grads %>%
  summarise(
    median_full_time = median(median), 
  )

print(median_earnings)
```

    ## # A tibble: 1 x 1
    ##   median_full_time
    ##              <dbl>
    ## 1            36000

![](README-img/noun_pause.png) **Planned Pause Point**: If you have any
questions, contact your instructor. Otherwise feel free to continue on.

### Additional Summaries of Median Earnings

Often we would like more information than the median to help us to
better understand the distribution of a variable. Note that wWhen I
obtain numerical summaries for variables, I like to include the variable
name in my summary name (e.g., `median_earnings = median(median)`).

1.  Below, create a code chunk and name it `summary_earnings`. Make sure
    there is an empty line above and below the code chunk.
2.  Specify that you want to use the `college_recent_grads` dataset,
    *then*, using the appropriate functions from `{dplyr}`, obtain the
    sample size (i.e., *n*umber of observations), *mean*, *s*tandard
    *d*eviation, *min*imum, *median*, and *max*imum summaries for the
    variable “median earnings of full-time, year-round workers”.

``` r
college_recent_grads %>%
  summarise(
    count = n(),
    sd_earn = sd(median),
    minimum_earn = min(median),
    maximum_earn = max(median),
    mean_earn = mean(median),
    median_earn = median(median), 
  )
```

    ## # A tibble: 1 x 6
    ##   count sd_earn minimum_earn maximum_earn mean_earn median_earn
    ##   <int>   <dbl>        <dbl>        <dbl>     <dbl>       <dbl>
    ## 1   173  11470.        22000       110000    40151.       36000

-   Be careful when you name your output summaries as we are dealing
    with things that could use the same name as functions that you will
    be using (i.e., “median”).

Provide a discussion on what you believe the distribution of median
earnings will look like. You should discuss the measures of center,
spread, and potential shape only using these values. DO NOT create any
data visualizations here. Use your understanding of how these numerical
summaries are related to the measures of center, spread, and potential
shape.

**Response**: The average earning is 36000, but there is a low variation
in the data set comparatively.

### Median Earnings by Major Category

Now we will see how the different major categories compare to the
overall distribution of median earnings.

*Arrange* this summary table by the median earning.

1.  Below, create a code chunk and name it `major_earnings`. Make sure
    there is an empty line above and below the code chunk.
2.  Specify that you want to use the `college_recent_grads` dataset,
    *then*, using the appropriate functions from `{dplyr}`, obtain the
    similar summaries of the variable “median earnings of full-time,
    year-round workers” as your `summary_earnings` code chunk, except
    now *by* each `major_category`.

``` r
college_recent_grads %>%
  group_by(major_category) %>%
  summarise(
    count = n(),
    sd_earn = sd(median),
    minimum_earn = min(median),
    maximum_earn = max(median),
    mean_earn = mean(median),
    median_earn = median(median), 
  ) %>%
  knitr::kable()
```

| major\_category                     | count |  sd\_earn | minimum\_earn | maximum\_earn | mean\_earn | median\_earn |
|:------------------------------------|------:|----------:|--------------:|--------------:|-----------:|-------------:|
| Agriculture & Natural Resources     |    10 |  6935.416 |         29000 |         53000 |   36900.00 |        35000 |
| Arts                                |     8 |  7223.165 |         27000 |         50000 |   33062.50 |        30750 |
| Biology & Life Science              |    14 |  4528.912 |         26000 |         45000 |   36421.43 |        36300 |
| Business                            |    13 |  7774.053 |         33000 |         62000 |   43538.46 |        40000 |
| Communications & Journalism         |     4 |  1000.000 |         33000 |         35000 |   34500.00 |        35000 |
| Computers & Mathematics             |    11 |  5108.691 |         35000 |         53000 |   42745.45 |        45000 |
| Education                           |    16 |  3892.728 |         22000 |         41000 |   32350.00 |        32750 |
| Engineering                         |    29 | 13626.080 |         40000 |        110000 |   57382.76 |        57000 |
| Health                              |    12 |  5776.461 |         28000 |         48000 |   36825.00 |        35000 |
| Humanities & Liberal Arts           |    15 |  3393.032 |         27000 |         40000 |   31913.33 |        32000 |
| Industrial Arts & Consumer Services |     7 |  7290.829 |         29000 |         50000 |   36342.86 |        35000 |
| Interdisciplinary                   |     1 |        NA |         35000 |         35000 |   35000.00 |        35000 |
| Law & Public Policy                 |     5 |  9066.422 |         35000 |         54000 |   42200.00 |        36000 |
| Physical Sciences                   |    10 |  8251.660 |         35000 |         62000 |   41890.00 |        39500 |
| Psychology & Social Work            |     9 |  5381.914 |         23400 |         40000 |   30100.00 |        30000 |
| Social Science                      |     9 |  4750.556 |         32000 |         47000 |   37344.44 |        38000 |

Is anything noteworthy when comparing your output from
`summary_earnings` to `major_earnings`? Also, compare your code in
`summary_earnings` to `major_earnings`. What is the same? Different?

**Response**: You can have insight on individual major earnings. For
instance, engineering has the highest maximum earnings as well as count.

Before we continue, knit your document and take note of what the output
for your `major_earnings` code chunk looks like.

Now, add the following to the end of your pipeline (you will need to
pipe first) in your `major_earnings` code chunk:

    knitr::kable()

Knit your document and look at the output for your `major_earnings` code
chunk. What changed about the output? When would this `knitr::kable`
code be useful?

**Response**: The output looks is well formatted in tabular structure
which is good for presentations and analysis.

![](README-img/noun_pause.png) **Planned Pause Point**: If you have any
questions, contact your instructor. Otherwise feel free to continue on.

### Visualize Median Earnings by Major Category

Let us see how well your descriptions in the [Median Earnings by Major
Category](#median-earnings-by-major-category) section compare to the
actual distributions.

1.  Below, create a code chunk and name it `major_boxplot`.
2.  Plot the distribution of the variable `median` earnings of
    full-time, year-round workers for each `major_category` using the
    *boxplot* and *jitter* geometries.

Provide a discussion on how your descriptions in the Median Earnings by
Major Category section compares.’

``` r
ggplot(
  college_recent_grads, mapping = aes(y = median, x = major_category)) +
  geom_boxplot() +
  geom_jitter() +
  theme(text = element_text(size = 8))
```

![](activity05-data-summarization_files/figure-gfm/major_boxplot-1.png)<!-- -->

**Response**:

<img src="README-img/noun_pause.png" alt="pause" width="20"/> <b>Planned
Pause Point</b>: If you feel that you have a good understanding of these
commands, feel free to start working on your project. The remainder of
this activity will help to expand these commands.

### Multiple Rankings

#### Ranking by `major_category`

The current rankings provided in the data are by `major`. Here we will
develop a series of rankings to see how the `major_category` levels
perform.

1.  Below, create a code chunk and name it `category_rankings`.
2.  In this code chunk,

-   Group `college_recent_grads` by `major_category`.
-   Summarize the variable `total` as the *sum* across all majors (to
    get the total number of majors within a `major_category`) and the
    following variables by their *median* value: `sharewomen`,
    `unemployment_rate`, and `median` earnings. Provide a meaningful
    name to each summarized value.
-   Assign/create a *rank* for each summarized value (rank for `total`,
    rank for `sharewomen`, etc.) and provide a meaningful name to each
    ranked column value. This ranking function might be confusing. Read
    the help documentation and ask for clarification.
-   Arrange the results so that `major_category` appear in alphabetical
    order (“A” at the top).

``` r
college_recent_grads %>% 
  group_by(major_category) %>% 
  summarize(
    total = sum (total), 
    median_sharewomen = median(sharewomen), 
    median_unemployment_rate = median(unemployment_rate), 
    median_earn = median(median)
  ) %>% 
  arrange(major_category) %>% 
  knitr::kable()
```

| major\_category                     |   total | median\_sharewomen | median\_unemployment\_rate | median\_earn |
|:------------------------------------|--------:|-------------------:|---------------------------:|-------------:|
| Agriculture & Natural Resources     |      NA |                 NA |                  0.0553146 |        35000 |
| Arts                                |  357130 |          0.6665767 |                  0.0894636 |        30750 |
| Biology & Life Science              |  453862 |          0.5827521 |                  0.0679693 |        36300 |
| Business                            | 1302376 |          0.4413556 |                  0.0697490 |        40000 |
| Communications & Journalism         |  392601 |          0.6715709 |                  0.0721767 |        35000 |
| Computers & Mathematics             |  299008 |          0.2691939 |                  0.0908233 |        45000 |
| Education                           |  559129 |          0.7693684 |                  0.0487851 |        32750 |
| Engineering                         |  537583 |          0.2271179 |                  0.0598242 |        57000 |
| Health                              |  463230 |          0.7833359 |                  0.0642609 |        35000 |
| Humanities & Liberal Arts           |  713468 |          0.6901107 |                  0.0817422 |        32000 |
| Industrial Arts & Consumer Services |  229792 |          0.2324435 |                  0.0556769 |        35000 |
| Interdisciplinary                   |   12296 |          0.7709011 |                  0.0708609 |        35000 |
| Law & Public Policy                 |  179107 |          0.4764612 |                  0.0824522 |        36000 |
| Physical Sciences                   |  185479 |          0.5204274 |                  0.0510984 |        39500 |
| Psychology & Social Work            |  481007 |          0.7989198 |                  0.0651122 |        30000 |
| Social Science                      |  529966 |          0.5434054 |                  0.0972439 |        38000 |

Provide a discussion on how the `major_category` rankings compare.

**Response**: Business major category has the highest graduates.
Computer and mathematics has most earnings.

![](README-img/noun_pause.png) **(Final) Planned Pause Point**: If you
have any questions, contact your instructor. Otherwise feel free to
continue on.

Knit, then stage everything listed in your **Git** pane, commit (with a
meaningful commit message), and push to your GitHub repo. Go to GitHub
and verify that your `activity04-data-pieplines.Rmd` file appears as you
intended it to.

You can now go back to the `README` file.

## Attribution

This activity is inspired by a lab from [Dr. Mine
Çetinkaya-Rundel](http://www2.stat.duke.edu/~mc301/)’s STA 199 course.