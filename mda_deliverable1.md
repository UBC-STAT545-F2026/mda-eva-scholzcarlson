Mini Data-Analysis: Deliverable 1
================

Total points available: 74

# Part 0: Getting Set Up

Let’s get ready to work on this assignment!

**0.1: Install Packages**

- Install the [`diversedata`](https://diverse-data-hub.github.io/)
  package by typing the following into your **R console**:

<!-- -->

    install.packages("pak")
    library(pak)
    pak::pak("diverse-data-hub/diversedata")

If you’re having trouble with installation, you may not have `Rtools`
installed yet. Try the following instructions (Windows):

- Close RStudio

- Download the specific version of Rtools that matches your version of R
  (for example, Rtools44 for R 4.4, or Rtools45 for newer versions) from
  the [CRAN Rtools
  page](https://cran.r-project.org/bin/windows/Rtools/). Follow the
  instructions to install.

- In RStudio, run `Sys.which("make")` to see if RTools has been
  successfully installed.

- Run
  `install.packages("pak", repos = sprintf("https://r-lib.github.io/p/pak/stable/%s/%s/%s", .Platform$pkgType, R.Version()$os, R.Version()$arch))`

**0.2: Load Packages**

Typically, R Packages are loaded in at the very beginning of the
analysis. If you later want to use other packages, please come back and
add them here:

``` r
library(tidyverse)
library(diversedata)

#--- Add any other packages below this line ---#
```

# Task 1: Choose a Data Set and Research Question

The following data sets can be used for this project from
`diversedatahub`:

- **wildfire**: This data set contains information on wildfires in
  Canada, compiled from official government sources under the Open
  Government Licence – Alberta. The data was gathered to monitor,
  assess, and respond to wildfire risks across different regions.
  Wildfires have far-reaching environmental, social, and economic
  consequences. From an equity and inclusion perspective, analyzing
  wildfire data can reveal geographic and resource-based disparities in
  detection and containment efforts, and highlight how certain
  populations face greater risks due to climate change and limited
  infrastructure. There are 26551 rows and 35 columns.

- **genderassessment**: Collected in 2023, the data allows for
  comparative evaluation across countries, sectors, and ownership types
  (e.g., Public, Private, Government). Each record represents a company
  and its corresponding evaluation across 28 detailed gender related
  indicators, offering a comprehensive snapshot of corporate gender
  equity worldwide. There are 2000 rows and 29 variables

- **globalrights**: This data set provides yearly, country-level
  information on LGBTQ+ rights, economic indicators, and education
  spending from 2001 to 2023. It is compiled from Our World in Data,
  with primary sources including Equaldex, the World Bank, and other
  open-access data sets.The data enables cross-country and temporal
  comparisons of LGBTQ+ rights and economic/education metrics,
  exploration of relationships between rights and economic development,
  and identification of regional and temporal trends. There are 2125
  rows and 10 columns, with a lot of missing data.

- **hcmst**: This data set is adapted from the original data set [How
  Couples Meet and Stay Together 2017,
  2022](https://data.stanford.edu/hcmst2017). This study, led by
  researchers from Stanford University, surveyed 1,722 U.S. adults in
  2022 to explore how relationships form and change with time and
  focused on dating habits and the impact of the COVID-19 pandemic on
  relationships. This adapted data set focuses on variables that may
  affect the quality of the relationship, considering demographic
  characteristics of the subjects, couple dynamics, as well as
  COVID-19-related variables. The COVID-19 pandemic had a [significant
  impact](https://pmc.ncbi.nlm.nih.gov/articles/PMC10009005/) on
  romantic relationships in the United States. This data set enables
  exploration of how external factors, like the health of the subjects
  and changes in income, as well as personal behaviors, like conflict
  and intimate dynamics, relate to an individual’s perception of the
  quality of the relationship. There are 1328 rows and 21 columns.

- **womensmarchmadness**: This adapted data set contains historical
  records of every NCAA Division I Women’s Basketball Tournament
  appearance since the tournament began in 1982 up until 2018, capturing
  tournament results across more than four decades of collegiate women’s
  basketball. All data is sourced from the NCAA and contains the data
  behind the story [The Rise and Fall Of Women’s NCAA Tournament
  Dynasties](https://fivethirtyeight.com/features/louisiana-tech-was-the-uconn-of-the-80s/).
  The rise in popularity of the NCAA Women’s March Madness, fueled by
  athletes like Caitlin Clark and Paige Bueckers, reflects a broader
  cultural shift in the recognition of women’s sports. Beyond
  entertainment and athletic achievement, women’s participation in sport
  has social and professional benefits. There are 2092 rows and 20
  columns.

*Note: We encourage you to use the ones in the `diversedata` package,
but if you have a data set that you’d really like to use, please check
with a member of the teaching team to see whether the data set is of
appropriate complexity. If approved, please add a brief description of
the data here.*

### 1.1: Choose 2 data sets **(2 points)**

Out of the 5 data sets listed above, choose **2** that appeal to you
based on their description. Write your choices below:

<!-------------------------- Start your work below ---------------------------->

1: hcmst

2: womensmarchmadness

<!----------------------------------------------------------------------------->

### 1.2: Explore the Data **(12 points)**

One way to narrowing down your selection is to *explore* the data sets.
Use your knowledge of `dplyr` to summarize three variables in each of
the data sets (for example, listing what levels of a categorical
variable exist, or calculating the mean of a continuous variable of
interest). Write a sentence that describes your findings for each
variable explored. You may use multiple R code chunks if preferred.

<!-------------------------- Start your work below ---------------------------->

#### Data Set 1

``` r
#str(hcmst)
#lapply(hcmst, unique) #many of the variables seem like multiple choice survey data so I viewed all unique answers in each variable in my initial dataset viewing

# variable 1: mean relationship duration
mean(hcmst$relationship_duration, na.rm = TRUE)
```

    ## [1] 27.22789

``` r
# variable 2: employment status options
employment_status <- as.factor(hcmst$subject_employment_status)
levels(employment_status)
```

    ## [1] "not_working_disabled"    "not_working_looking"    
    ## [3] "not_working_other"       "not_working_retired"    
    ## [5] "not_working_temp_layoff" "working_paid_employee"  
    ## [7] "working_self_employed"

``` r
# variable 3: min and max age of subjects
min(hcmst$subject_age)
```

    ## [1] 23

``` r
max(hcmst$subject_age)
```

    ## [1] 98

I found that the mean relationship duration for surveyed participants
was 27.23 years. There were seven options for subject employment status
with choices within “not working” including disabled, looking, other,
retired, and temporary layoff, and for “working” including paid employee
or self employed. The minimum subject age was 23 and the maximum age was
98.

#### Data Set 2

``` r
#str(womensmarchmadness)

# variable 1: number of schools included in dataset
length(unique(womensmarchmadness$school))
```

    ## [1] 284

``` r
# variable 2: range of years in dataset
firstyear <- min(womensmarchmadness$year)
lastyear <- max(womensmarchmadness$year)
firstyear
```

    ## [1] 1982

``` r
lastyear
```

    ## [1] 2018

``` r
lastyear - firstyear #number of years the dataset spans
```

    ## [1] 36

``` r
# variable 3: maximum wins and percentage of total wins
max(womensmarchmadness$total_wins)
```

    ## [1] 40

``` r
max(womensmarchmadness$total_wins_pct)
```

    ## [1] 100

Write your findings here.

The womensmarchmadness dataset includes 284 schools. It spans 36 years,
from 1982 to 2018. The maximum number of wins in a season was 40 (100%
wins).

<!----------------------------------------------------------------------------->

### 1.3: Choose 1 Data Set **(2 points)**

It’s time to choose only one data set. State the data set that you’ve
chosen, and why you’ve chosen it.

<!-------------------------- Start your work below ---------------------------->

I’ve chosen the hcmst dataset. I’m interested in the influence of a
number of variables in this dataset on relationship quality and length,
including employment status, income, and number of flirts and fights
with the partner. I was also excited to see that the relationships of
people surveyed tend to be quite long, and that there are participants
from a very wide age range.

<!----------------------------------------------------------------------------->

### 1.4: Research Question **(4 points)**

Let’s choose a primary and a secondary research question to explore.

Write your research questions **as questions**, and be specific. You can
change it later if needed.

> For example, if I had chosen a `titanic` data set for my project, I
> might ask, “(Primary) Is there a relationship between survival and the
> class of the passengers? (Secondary) Does this relationship differ by
> gender?”

<!-------------------------- Start your work below ---------------------------->

Primary: Is there a relationship between income and relationship
duration? Secondary: Does this relationship differ in same-sex couples
of either sex?

<!----------------------------------------------------------------------------->

### 1.5: Commit **(2 points)**

Commit your work and push it to GitHub. Include an informative commit
message, and include “(1.5)” in the message.

# Task 2: Further Exploring Your Chosen Data Set

### 2.1: Missing Data **(6 points)**

Missing data is inevitable, and can complicate analyses. Let’s see what
variables (if any) have missing data in your chosen data set.

Your task is to create a table that calculates the proportion of missing
values per variable. Be sure to output the table.

<!-------------------------- Start your work below ---------------------------->

``` r
# creating a new tibble with number of missing values in each variable
hcmst_missing <- hcmst |>
  summarise(
    across(
      everything(), #including all variables
      list(
      NA_prop = ~ sum(is.na(.x))/length(.x)))) #calculating proportion of NAs per variable

print(hcmst_missing)
```

    ## # A tibble: 1 × 21
    ##   subject_age_NA_prop subject_education_NA_prop subject_sex_NA_prop
    ##                 <dbl>                     <dbl>               <dbl>
    ## 1                   0                         0                   0
    ## # ℹ 18 more variables: subject_ethnicity_NA_prop <dbl>,
    ## #   subject_income_category_NA_prop <dbl>,
    ## #   subject_employment_status_NA_prop <dbl>, same_sex_couple_NA_prop <dbl>,
    ## #   married_NA_prop <dbl>, sex_frequency_NA_prop <dbl>,
    ## #   flirts_with_partner_NA_prop <dbl>, fights_with_partner_NA_prop <dbl>,
    ## #   relationship_duration_NA_prop <dbl>, children_NA_prop <dbl>,
    ## #   rel_change_during_pandemic_NA_prop <dbl>, …

``` r
#new tibble with missing data proportion for my variables of interest
hcmst_missing_myvars <- hcmst_missing |>
  select(subject_income_category_NA_prop, relationship_duration_NA_prop, same_sex_couple_NA_prop, subject_sex_NA_prop)

print(hcmst_missing_myvars)
```

    ## # A tibble: 1 × 4
    ##   subject_income_category_NA_prop relationship_duration…¹ same_sex_couple_NA_p…²
    ##                             <dbl>                   <dbl>                  <dbl>
    ## 1                               0                  0.0264                      0
    ## # ℹ abbreviated names: ¹​relationship_duration_NA_prop, ²​same_sex_couple_NA_prop
    ## # ℹ 1 more variable: subject_sex_NA_prop <dbl>

<!----------------------------------------------------------------------------->

### 2.2: Missing Data (Again) **(6 points)**

Based on your research question, will this missingness pose an issue?
For the purposes of this class (and this class only!), we will consider
missingness a problem **if there is more than 20% of a single variable
(that is of interest) is missing**.

> For example, let’s assume I wanted to explore the following research
> questions: “Is there a relationship between survival and the class of
> the passengers? Does this relationship vary by gender?”. If the
> variable indicating whether or not a person survived was missing for
> 20% or more of the passengers, then this would be a problem. However,
> if a variable indicating the colour of shirt a passenger was wearing
> was missing, this probably wouldn’t be an issue as that variable is
> quite irrelevant to my analysis!

Based on this definition, is missingness an issue for your analysis? If
so, describe how you will address this (pivoting your research question,
for example). If you will continue with a new research question, write
it here! **Do not go back to Task 1 and redo the analysis.** ).

If missingness is not an issue, describe why.

<!-------------------------- Start your work below ---------------------------->

Missingness is not an issue since income and same-sex status have no
missing values, while relationship duration is only missing 2.6% of the
data. Since relationship duration is part of my primary question, I will
not be able to use this 2.6% of data for my entire analysis, however
this is well under 20%.

<!----------------------------------------------------------------------------->

### 2.3: Tidy your Data **(10 points)**

Produce a tidy data set that could be used to answer your research
questions. **Please ensure you have at least one quantitative (numeric)
and one categorical variable in your data set. It’s okay you need to
include a less relevant variable in your tidied data to ensure this.**

To tidy your data, you should:

- Create new variables (if needed)

- Transform the data into a tidy form (if needed)

- Remove irrelevant columns (if needed)

- Comment your code throughout

Show the first 6 rows of the tidied data.

<!-------------------------- Start your work below ---------------------------->

``` r
hcmst_subset <- hcmst |>
  select(c(subject_income_category, #selecting relevant columns for my analysis
           relationship_duration, 
           same_sex_couple,
           subject_sex)) |> 
  mutate(income = #ordering levels for my income category for easier graphing and renaming with shorter name
           ordered(subject_income_category, 
                   levels = c("under_5k", "5k-7k", "7k_10k", "10k_12k", "12k_15k", "15k_20k", "20k_25k","25k_30k", "30k_35k", "35k_40k", "40k_50k", "50k_60k", "60k_75k", "75k_85k","85k_100k", "100k_125k", "125k_150k", "150k_175k", "175k_200k", "200k_250k", "over_250k")),  
         #I'm guessing there's a more efficient way to do this, such as ordering by the last part of the range, 
         #but I couldn't figure that out
         .keep = "unused", #getting rid of old subject_income_category column
         .before = relationship_duration) |>
  rename(sex = subject_sex) |>
  arrange(income) 

head(hcmst_subset)
```

    ## # A tibble: 6 × 4
    ##   income   relationship_duration same_sex_couple sex   
    ##   <ord>                    <dbl> <chr>           <chr> 
    ## 1 under_5k                13.6   no              female
    ## 2 under_5k                53.9   no              female
    ## 3 under_5k                34.2   no              male  
    ## 4 under_5k                11.4   no              female
    ## 5 under_5k                 0.417 no              female
    ## 6 under_5k                30.6   no              female

<!----------------------------------------------------------------------------->

### 2.4: Create a Table (10 points)

Use any functions from the `tidyverse` to create one table that outputs
the mean, minimum, and maximum of all numeric columns in your data,
dropping the missing values if they exist.

Show the outputted table.

<!-------------------------- Start your work below ---------------------------->

``` r
hcmst_subset_summary <- hcmst_subset |>
  summarise(across(where(is.numeric), #summarising across all numeric variables
            c(mean = mean, min = min, max = max), #using mean, min, and max functions
            na.rm = TRUE)) #excluding NA data
```

    ## Warning: There was 1 warning in `summarise()`.
    ## ℹ In argument: `across(...)`.
    ## Caused by warning:
    ## ! The `...` argument of `across()` is deprecated as of dplyr 1.1.0.
    ## Supply arguments directly to `.fns` through an anonymous function instead.
    ## 
    ##   # Previously
    ##   across(a:b, mean, na.rm = TRUE)
    ## 
    ##   # Now
    ##   across(a:b, \(x) mean(x, na.rm = TRUE))

``` r
hcmst_subset_summary
```

    ## # A tibble: 1 × 3
    ##   relationship_duration_mean relationship_duration_min relationship_duration_max
    ##                        <dbl>                     <dbl>                     <dbl>
    ## 1                       27.2                         0                      102.

<!----------------------------------------------------------------------------->

### 2.5: Commit **(2 points)**

Commit your work and push it to GitHub. , and include “(2.7)” in the
message.

# Task 3: Tidy Your Submission Overall

Check over your document and GitHub repository for the following:

### 3.1: Coherence **(2 points)**

The document should read sensibly from top to bottom, with no major
continuity errors. An example of a major continuity error is having a
data set listed for Task 3 that is not part of one of the data sets
listed in Task 1.

### 3.2: Error-free code **(2 points)**

For full marks, all code in the document should run without error and be
completely reproducible.

### 3.3 README **(6 points)**

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

- In a sentence or two, explains what this repository is, so that
  future-you or someone else stumbling on your repository can be
  oriented to the repository.
- List the files/folders contained in the repository
- In a sentence or two, briefly explains how to engage with the
  repository. You can assume the person reading knows the material from
  STAT 545A. Basically, if a visitor to your repository wants to explore
  your project, what should they know? How can they reproduce your
  report?

### 3.4 Generative AI Disclosure **(3 points)**

In this course, Generative AI can be used in the following ways:

- to clarify concepts discussed in class

- as an “advanced search engine” (i.e., searching error codes)

- debugging code that students wrote and attempted to debug on their own

Generative AI **CANNOT** be used to generate text or code (including
comments) from scratch.

Any use of Generative AI must be disclosed.

**To disclose your use, please copy and paste the following template
into the README of your GitHub Repository and fill out the relevant
details** \[in square brackets\]. BE SPECIFIC. Saying you used it to
debug your code is not enough. Explicitly describe where you got stuck

Here is an example of a specific, explicit debug:

> “I had the error `attempt to apply non-function` after running my
> code. I used Claude to help me identify that this error was due to me
> attempting to multiply two numbers together without the use of a `*`,
> i.e. `(2)(3)` instead of `2*3`.”

``` markdown

## Generative AI Statement 

Generative AI (through [LIST MODELS USED, i.e. ChatGPT, CoPilot)] was used to 
help me complete  this assignment in the following ways. 

1. [Describe here]

2. [Describe here]

...

I affirm that Generative AI was not used to generate text, code, or comments for 
my assessments. 
```

If you did not use Generative AI, please include the following in your
README:

``` markdown

## Generative AI Statement 

Generative AI was not used in any way throughout this assignment.
```

Assessments suspected of having AI-generated text and/or code, or
assignments where the Generative AI use was not disclosed, will be
flagged and temporarily assigned a grade of zero. Students will be
required to meet with the instructor to receive a grade.

### 3.5 Output **(4 points)**

All output on GitHub is readable, recent and relevant:

- All `.Rmd` files have been `knit`ted to their output `.md` files.
- All knitted `.md` files are viewable without errors on Github.
  Examples of errors: Missing plots, “Sorry about that, but we can’t
  show files that are this big right now” messages, error messages from
  broken R code
- All of these output files are up-to-date – that is, they haven’t
  fallen behind after the source (`.Rmd`) files have been updated.
- There should be no relic output files. For example, if you were
  knitting an `.Rmd` to `.html`, but then changed the output to be only
  a markdown file, then the `.html` file is a relic and should be
  deleted.

# Step 4: Submission

### 4.1: Tag a Release **(1 point)**

To submit this milestone, tag a release on GitHub and submit the link to
Canvas.
