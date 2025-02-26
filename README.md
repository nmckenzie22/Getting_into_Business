README
================

# Download Dataset

``` r
# Define the download URL
kaggle_url <- "https://www.kaggle.com/api/v1/datasets/download/fratzcan/usa-house-prices"

# Define the output file path
output_file <- file.path("./", "usa-house-prices.zip")

# Run the cURL command in R
system(paste("curl -L -o", shQuote(output_file), shQuote(kaggle_url)))

# Optional: Unzip the file
unzip(output_file, exdir = "./usa-house-prices")

# Confirm download
list.files("~/Downloads/usa-house-prices")
```

    ## character(0)

When was the data acquired? Where was the data acquired?

How was the data acquired?

What are the attributes of this dataset? Below is R script code that loads the USA Housing Dataset and creates a data dictionary table based on the descriptions provided on Kaggle.

``` r
#install.packages("readr")   # For reading CSV files
#install.packages("dplyr")   # For data manipulation
#install.packages("knitr")   # For creating a table
#install.packages("kableExtra") # For formatting tables


library(readr)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(knitr)
library(kableExtra)
```

    ## 
    ## Attaching package: 'kableExtra'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     group_rows

``` r
# Load the dataset (update the path if needed)
dataset <- read_csv("~/Downloads/USA_Housing_Dataset.csv")
```

    ## Rows: 4140 Columns: 18

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (4): street, city, statezip, country
    ## dbl  (13): price, bedrooms, bathrooms, sqft_living, sqft_lot, floors, waterf...
    ## dttm  (1): date
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# View first few rows
head(dataset)
```

    ## # A tibble: 6 × 18
    ##   date                  price bedrooms bathrooms sqft_living sqft_lot floors
    ##   <dttm>                <dbl>    <dbl>     <dbl>       <dbl>    <dbl>  <dbl>
    ## 1 2014-05-09 00:00:00  376000        3      2           1340     1384      3
    ## 2 2014-05-09 00:00:00  800000        4      3.25        3540   159430      2
    ## 3 2014-05-09 00:00:00 2238888        5      6.5         7270   130017      2
    ## 4 2014-05-09 00:00:00  324000        3      2.25         998      904      2
    ## 5 2014-05-10 00:00:00  549900        5      2.75        3060     7015      1
    ## 6 2014-05-10 00:00:00  320000        3      2.5         2130     6969      2
    ## # ℹ 11 more variables: waterfront <dbl>, view <dbl>, condition <dbl>,
    ## #   sqft_above <dbl>, sqft_basement <dbl>, yr_built <dbl>, yr_renovated <dbl>,
    ## #   street <chr>, city <chr>, statezip <chr>, country <chr>

``` r
# Define the updated data dictionary with correct types and levels of measurement
data_dictionary <- tibble::tibble(
  Variable = c("Price", "Bedrooms", "Bathrooms", "Sqft Living", "Sqft Lot", 
               "Floors", "Waterfront", "View", "Condition", "Sqft Above", 
               "Sqft Basement", "Yr Built", "Yr Renovated", "Street", 
               "City", "StateZip", "Country", 
               "Median Area Income", "Median Area House Age", 
               "Median Area Number of Rooms", "Median Area Number of Bedrooms", "Area Population"),
  Type = c("Ratio", "Ratio", "Ratio", "Ratio", "Ratio", 
           "Ratio", "Nominal", "Ordinal", "Ordinal", "Ratio", 
           "Ratio", "Interval", "Interval", "Nominal", 
           "Nominal", "Nominal", "Nominal", 
           "Ratio", "Ratio", 
           "Ratio", "Ratio", "Ratio"),
  Description = c("Sale price of the house (in USD).",
                  "Number of bedrooms in the house.",
                  "Number of bathrooms in the house.",
                  "Total living area in square feet.",
                  "Total lot size in square feet.",
                  "Number of floors in the house.",
                  "Indicates if the house is on the waterfront (Yes/No).",
                  "A rating of the house's view quality.",
                  "Condition of the house (1-5 scale, where 5 is the best).",
                  "Square footage of the house above ground.",
                  "Square footage of the basement.",
                  "Year the house was built.",
                  "Year the house was last renovated.",
                  "Street address of the house.",
                  "City where the house is located.",
                  "State and ZIP code of the house.",
                  "Country where the house is located.",
                  "Median income of residents in the area (in USD).",
                  "Median age of houses in the area.",
                  "Median number of rooms in houses in the area.",
                  "Median number of bedrooms in houses in the area.",
                  "Population of the area.")
)

# Print the data dictionary as a formatted table
data_dictionary %>%
  kable("pipe") %>%
  kable_styling(full_width = FALSE, bootstrap_options = c("striped", "hover"))
```

<table class="table table-striped table-hover" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Variable
</th>
<th style="text-align:left;">
Type
</th>
<th style="text-align:left;">
Description
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Price
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Sale price of the house (in USD).
</td>
</tr>
<tr>
<td style="text-align:left;">
Bedrooms
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Number of bedrooms in the house.
</td>
</tr>
<tr>
<td style="text-align:left;">
Bathrooms
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Number of bathrooms in the house.
</td>
</tr>
<tr>
<td style="text-align:left;">
Sqft Living
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Total living area in square feet.
</td>
</tr>
<tr>
<td style="text-align:left;">
Sqft Lot
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Total lot size in square feet.
</td>
</tr>
<tr>
<td style="text-align:left;">
Floors
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Number of floors in the house.
</td>
</tr>
<tr>
<td style="text-align:left;">
Waterfront
</td>
<td style="text-align:left;">
Nominal
</td>
<td style="text-align:left;">
Indicates if the house is on the waterfront (Yes/No).
</td>
</tr>
<tr>
<td style="text-align:left;">
View
</td>
<td style="text-align:left;">
Ordinal
</td>
<td style="text-align:left;">
A rating of the house’s view quality.
</td>
</tr>
<tr>
<td style="text-align:left;">
Condition
</td>
<td style="text-align:left;">
Ordinal
</td>
<td style="text-align:left;">
Condition of the house (1-5 scale, where 5 is the best).
</td>
</tr>
<tr>
<td style="text-align:left;">
Sqft Above
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Square footage of the house above ground.
</td>
</tr>
<tr>
<td style="text-align:left;">
Sqft Basement
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Square footage of the basement.
</td>
</tr>
<tr>
<td style="text-align:left;">
Yr Built
</td>
<td style="text-align:left;">
Interval
</td>
<td style="text-align:left;">
Year the house was built.
</td>
</tr>
<tr>
<td style="text-align:left;">
Yr Renovated
</td>
<td style="text-align:left;">
Interval
</td>
<td style="text-align:left;">
Year the house was last renovated.
</td>
</tr>
<tr>
<td style="text-align:left;">
Street
</td>
<td style="text-align:left;">
Nominal
</td>
<td style="text-align:left;">
Street address of the house.
</td>
</tr>
<tr>
<td style="text-align:left;">
City
</td>
<td style="text-align:left;">
Nominal
</td>
<td style="text-align:left;">
City where the house is located.
</td>
</tr>
<tr>
<td style="text-align:left;">
StateZip
</td>
<td style="text-align:left;">
Nominal
</td>
<td style="text-align:left;">
State and ZIP code of the house.
</td>
</tr>
<tr>
<td style="text-align:left;">
Country
</td>
<td style="text-align:left;">
Nominal
</td>
<td style="text-align:left;">
Country where the house is located.
</td>
</tr>
<tr>
<td style="text-align:left;">
Median Area Income
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Median income of residents in the area (in USD).
</td>
</tr>
<tr>
<td style="text-align:left;">
Median Area House Age
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Median age of houses in the area.
</td>
</tr>
<tr>
<td style="text-align:left;">
Median Area Number of Rooms
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Median number of rooms in houses in the area.
</td>
</tr>
<tr>
<td style="text-align:left;">
Median Area Number of Bedrooms
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Median number of bedrooms in houses in the area.
</td>
</tr>
<tr>
<td style="text-align:left;">
Area Population
</td>
<td style="text-align:left;">
Ratio
</td>
<td style="text-align:left;">
Population of the area.
</td>
</tr>
</tbody>
</table>

Now we can take a further look at the data to gain initial insights and have an overview of the statistics. We can do this by performing a basic Exploratory Data Analysis (EDA). The code below will display the summary statistics from the dataset.

``` r
# Install required packages (if not already installed)
#install.packages("readr")      # For reading CSV files
#install.packages("dplyr")      # For data manipulation
#install.packages("ggplot2")    # For visualizations
#install.packages("skimr")      # For detailed summary statistics
#install.packages("modeest")    # For calculating mode
# Load libraries
library(readr)
library(dplyr)
library(ggplot2)
library(skimr)
library(modeest)
# Load the dataset (update the path if needed)
dataset <- read_csv("~/Downloads/USA_Housing_Dataset.csv")
```

    ## Rows: 4140 Columns: 18
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (4): street, city, statezip, country
    ## dbl  (13): price, bedrooms, bathrooms, sqft_living, sqft_lot, floors, waterf...
    ## dttm  (1): date
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# Display first few rows
head(dataset)
```

    ## # A tibble: 6 × 18
    ##   date                  price bedrooms bathrooms sqft_living sqft_lot floors
    ##   <dttm>                <dbl>    <dbl>     <dbl>       <dbl>    <dbl>  <dbl>
    ## 1 2014-05-09 00:00:00  376000        3      2           1340     1384      3
    ## 2 2014-05-09 00:00:00  800000        4      3.25        3540   159430      2
    ## 3 2014-05-09 00:00:00 2238888        5      6.5         7270   130017      2
    ## 4 2014-05-09 00:00:00  324000        3      2.25         998      904      2
    ## 5 2014-05-10 00:00:00  549900        5      2.75        3060     7015      1
    ## 6 2014-05-10 00:00:00  320000        3      2.5         2130     6969      2
    ## # ℹ 11 more variables: waterfront <dbl>, view <dbl>, condition <dbl>,
    ## #   sqft_above <dbl>, sqft_basement <dbl>, yr_built <dbl>, yr_renovated <dbl>,
    ## #   street <chr>, city <chr>, statezip <chr>, country <chr>

``` r
# Check structure of dataset
str(dataset)
```

    ## spc_tbl_ [4,140 × 18] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ date         : POSIXct[1:4140], format: "2014-05-09" "2014-05-09" ...
    ##  $ price        : num [1:4140] 376000 800000 2238888 324000 549900 ...
    ##  $ bedrooms     : num [1:4140] 3 4 5 3 5 3 4 4 3 4 ...
    ##  $ bathrooms    : num [1:4140] 2 3.25 6.5 2.25 2.75 2.5 2 1 2.5 2.5 ...
    ##  $ sqft_living  : num [1:4140] 1340 3540 7270 998 3060 2130 2520 1940 1350 2160 ...
    ##  $ sqft_lot     : num [1:4140] 1384 159430 130017 904 7015 ...
    ##  $ floors       : num [1:4140] 3 2 2 2 1 2 1 1 3 2.5 ...
    ##  $ waterfront   : num [1:4140] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ view         : num [1:4140] 0 0 0 0 0 0 0 0 0 0 ...
    ##  $ condition    : num [1:4140] 3 3 3 3 5 3 3 3 3 4 ...
    ##  $ sqft_above   : num [1:4140] 1340 3540 6420 798 1600 2130 1400 1080 1270 2160 ...
    ##  $ sqft_basement: num [1:4140] 0 0 850 200 1460 0 1120 860 80 0 ...
    ##  $ yr_built     : num [1:4140] 2008 2007 2010 2007 1979 ...
    ##  $ yr_renovated : num [1:4140] 0 0 0 0 0 ...
    ##  $ street       : chr [1:4140] "9245-9249 Fremont Ave N" "33001 NE 24th St" "7070 270th Pl SE" "820 NW 95th St" ...
    ##  $ city         : chr [1:4140] "Seattle" "Carnation" "Issaquah" "Seattle" ...
    ##  $ statezip     : chr [1:4140] "WA 98103" "WA 98014" "WA 98029" "WA 98117" ...
    ##  $ country      : chr [1:4140] "USA" "USA" "USA" "USA" ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   date = col_datetime(format = ""),
    ##   ..   price = col_double(),
    ##   ..   bedrooms = col_double(),
    ##   ..   bathrooms = col_double(),
    ##   ..   sqft_living = col_double(),
    ##   ..   sqft_lot = col_double(),
    ##   ..   floors = col_double(),
    ##   ..   waterfront = col_double(),
    ##   ..   view = col_double(),
    ##   ..   condition = col_double(),
    ##   ..   sqft_above = col_double(),
    ##   ..   sqft_basement = col_double(),
    ##   ..   yr_built = col_double(),
    ##   ..   yr_renovated = col_double(),
    ##   ..   street = col_character(),
    ##   ..   city = col_character(),
    ##   ..   statezip = col_character(),
    ##   ..   country = col_character()
    ##   .. )
    ##  - attr(*, "problems")=<externalptr>

``` r
# Basic summary statistics
summary(dataset)
```

    ##       date                            price             bedrooms  
    ##  Min.   :2014-05-02 00:00:00.00   Min.   :       0   Min.   :0.0  
    ##  1st Qu.:2014-05-27 00:00:00.00   1st Qu.:  320000   1st Qu.:3.0  
    ##  Median :2014-06-12 00:00:00.00   Median :  460000   Median :3.0  
    ##  Mean   :2014-06-10 16:24:41.74   Mean   :  553063   Mean   :3.4  
    ##  3rd Qu.:2014-06-25 00:00:00.00   3rd Qu.:  659125   3rd Qu.:4.0  
    ##  Max.   :2014-07-10 00:00:00.00   Max.   :26590000   Max.   :8.0  
    ##    bathrooms      sqft_living       sqft_lot           floors     
    ##  Min.   :0.000   Min.   :  370   Min.   :    638   Min.   :1.000  
    ##  1st Qu.:1.750   1st Qu.: 1470   1st Qu.:   5000   1st Qu.:1.000  
    ##  Median :2.250   Median : 1980   Median :   7676   Median :1.500  
    ##  Mean   :2.163   Mean   : 2144   Mean   :  14698   Mean   :1.514  
    ##  3rd Qu.:2.500   3rd Qu.: 2620   3rd Qu.:  11000   3rd Qu.:2.000  
    ##  Max.   :6.750   Max.   :10040   Max.   :1074218   Max.   :3.500  
    ##    waterfront            view          condition       sqft_above  
    ##  Min.   :0.000000   Min.   :0.0000   Min.   :1.000   Min.   : 370  
    ##  1st Qu.:0.000000   1st Qu.:0.0000   1st Qu.:3.000   1st Qu.:1190  
    ##  Median :0.000000   Median :0.0000   Median :3.000   Median :1600  
    ##  Mean   :0.007488   Mean   :0.2466   Mean   :3.452   Mean   :1831  
    ##  3rd Qu.:0.000000   3rd Qu.:0.0000   3rd Qu.:4.000   3rd Qu.:2310  
    ##  Max.   :1.000000   Max.   :4.0000   Max.   :5.000   Max.   :8020  
    ##  sqft_basement       yr_built     yr_renovated       street         
    ##  Min.   :   0.0   Min.   :1900   Min.   :   0.0   Length:4140       
    ##  1st Qu.:   0.0   1st Qu.:1951   1st Qu.:   0.0   Class :character  
    ##  Median :   0.0   Median :1976   Median :   0.0   Mode  :character  
    ##  Mean   : 312.3   Mean   :1971   Mean   : 808.4                     
    ##  3rd Qu.: 602.5   3rd Qu.:1997   3rd Qu.:1999.0                     
    ##  Max.   :4820.0   Max.   :2014   Max.   :2014.0                     
    ##      city             statezip           country         
    ##  Length:4140        Length:4140        Length:4140       
    ##  Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character  
    ##                                                          
    ##                                                          
    ## 

``` r
# Additional summary statistics using skimr
skim(dataset)
```

|                                                  |         |
|:-------------------------------------------------|:--------|
| Name                                             | dataset |
| Number of rows                                   | 4140    |
| Number of columns                                | 18      |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |         |
| Column type frequency:                           |         |
| character                                        | 4       |
| numeric                                          | 13      |
| POSIXct                                          | 1       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |         |
| Group variables                                  | None    |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| street        |         0 |             1 |   8 |  46 |     0 |     4079 |          0 |
| city          |         0 |             1 |   4 |  18 |     0 |       43 |          0 |
| statezip      |         0 |             1 |   8 |   8 |     0 |       77 |          0 |
| country       |         0 |             1 |   3 |   3 |     0 |        1 |          0 |

**Variable type: numeric**

| skim_variable | n_missing | complete_rate | mean | sd | p0 | p25 | p50 | p75 | p100 | hist |
|:---|---:|---:|---:|---:|---:|---:|---:|---:|---:|:---|
| price | 0 | 1 | 553062.88 | 583686.45 | 0 | 320000.00 | 460000.00 | 659125.0 | 26590000.00 | ▇▁▁▁▁ |
| bedrooms | 0 | 1 | 3.40 | 0.90 | 0 | 3.00 | 3.00 | 4.0 | 8.00 | ▁▇▅▁▁ |
| bathrooms | 0 | 1 | 2.16 | 0.78 | 0 | 1.75 | 2.25 | 2.5 | 6.75 | ▂▇▂▁▁ |
| sqft_living | 0 | 1 | 2143.64 | 957.48 | 370 | 1470.00 | 1980.00 | 2620.0 | 10040.00 | ▇▅▁▁▁ |
| sqft_lot | 0 | 1 | 14697.64 | 35876.84 | 638 | 5000.00 | 7676.00 | 11000.0 | 1074218.00 | ▇▁▁▁▁ |
| floors | 0 | 1 | 1.51 | 0.53 | 1 | 1.00 | 1.50 | 2.0 | 3.50 | ▇▆▁▁▁ |
| waterfront | 0 | 1 | 0.01 | 0.09 | 0 | 0.00 | 0.00 | 0.0 | 1.00 | ▇▁▁▁▁ |
| view | 0 | 1 | 0.25 | 0.79 | 0 | 0.00 | 0.00 | 0.0 | 4.00 | ▇▁▁▁▁ |
| condition | 0 | 1 | 3.45 | 0.68 | 1 | 3.00 | 3.00 | 4.0 | 5.00 | ▁▁▇▃▁ |
| sqft_above | 0 | 1 | 1831.35 | 861.38 | 370 | 1190.00 | 1600.00 | 2310.0 | 8020.00 | ▇▅▁▁▁ |
| sqft_basement | 0 | 1 | 312.29 | 464.35 | 0 | 0.00 | 0.00 | 602.5 | 4820.00 | ▇▁▁▁▁ |
| yr_built | 0 | 1 | 1970.81 | 29.81 | 1900 | 1951.00 | 1976.00 | 1997.0 | 2014.00 | ▂▃▆▆▇ |
| yr_renovated | 0 | 1 | 808.37 | 979.38 | 0 | 0.00 | 0.00 | 1999.0 | 2014.00 | ▇▁▁▁▆ |

**Variable type: POSIXct**

| skim_variable | n_missing | complete_rate | min | max | median | n_unique |
|:---|---:|---:|:---|:---|:---|---:|
| date | 0 | 1 | 2014-05-02 | 2014-07-10 | 2014-06-12 | 68 |

``` r
# Function to calculate mode
get_mode <- function(x) {
  mfv <- mfv(x, na_rm = TRUE)  # Most frequent value
  return(mfv)
}
# Calculate mode for numeric columns
numeric_cols <- dataset %>% select(where(is.numeric))
mode_values <- sapply(numeric_cols, get_mode)
# Print mode values
print(mode_values)
```

    ## $price
    ## [1] 0
    ## 
    ## $bedrooms
    ## [1] 3
    ## 
    ## $bathrooms
    ## [1] 2.5
    ## 
    ## $sqft_living
    ## [1] 1720
    ## 
    ## $sqft_lot
    ## [1] 5000
    ## 
    ## $floors
    ## [1] 1
    ## 
    ## $waterfront
    ## [1] 0
    ## 
    ## $view
    ## [1] 0
    ## 
    ## $condition
    ## [1] 3
    ## 
    ## $sqft_above
    ## [1] 1200
    ## 
    ## $sqft_basement
    ## [1] 0
    ## 
    ## $yr_built
    ## [1] 2005 2006
    ## 
    ## $yr_renovated
    ## [1] 0

Next we need to identify any missing or empty values. The code below will allow us to identify the values.

``` r
# Check for missing values (NA counts per column)
missing_values <- colSums(is.na(dataset))
# Print missing values summary
print(missing_values)
```

    ##          date         price      bedrooms     bathrooms   sqft_living 
    ##             0             0             0             0             0 
    ##      sqft_lot        floors    waterfront          view     condition 
    ##             0             0             0             0             0 
    ##    sqft_above sqft_basement      yr_built  yr_renovated        street 
    ##             0             0             0             0             0 
    ##          city      statezip       country 
    ##             0             0             0
