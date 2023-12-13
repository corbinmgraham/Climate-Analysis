DS202-FinalProject
================
Corbin Graham, Coleman Dimmer
2023-12-12

# DS 202 Final Project

**Title: Climate Analysis of Milan, Italy**

**Authors: Corbin Graham, Coleman Dimmer**

The goal of this project is to demonstrate skills learned, in R,
analysis of data, demonstration of data, and drawing conclusions from
data. We used data from National Centers for Environmental Information
(NCEI) for the Milan Weather Recording Station of Milan, Italy. Using
graphs, charts, and analysis, we will visualize and demonstrate patterns
and trends within the dataset.

## Introduction

The United Nations is an intergovernmental organization whose stated
purposes are to maintain international peace and security. They describe
themselves as, “the one place on Earth where all the world’s nations can
gather together, discuss common problems, and find shared solutions that
benefit all of humanity.”(1)

The United Nations, as part of its mission for international peace, has
compiled 17 goals, which it deems the most important and of the highest
priority for all nations. The goals are ordered by importance to the
organization’s purpose. However, all goals should be considered of
highest importance for every nation.

The United Nations’ thirteenth goal is on climate action. They state
that: “Every person, in every country in every continent will be
impacted in some shape or form by climate change. There is a climate
cataclysm looming, and we are underprepared for what this could
mean.”(1) Thus, this can be seen as a topic of very high importance
since, according to the United Nations, climate change will affect us
all.

Finding accurate climate data over an extended period can be difficult
since most countries did not begin practicing accurate data recording of
weather patterns, emissions, until sometime within the last 200 years.
For demonstrating, and finding accurate trends, it is important to look
at accurate, comprehensive data collection. The most reliable source for
climate data available in the United States is the United States
National Centers for Environmental Information (NCEI). All the data they
provide is extensive, and heavily scrutinized. The rigor of data quality
provides us with the best, and most accurate measurements of the
climate. Because most quality data recording began recently, we must
look outside our borders to find older data with the same accuracy. The
longest-running data record on climate comes from Milan, Italy, which
began recording weather and climate data in 1763 for the Italian
government.

Using this data, it is our goal to demonstrate climate patterns, and
find trends in those patterns. Using the trends, we may, or may not
find, we hope to find the highest correlating data available to
potentially explain the trends we see. While some trends may have no
correlation, it is of high likelihood that any trends demonstrated in
climate patterns are the result of some external event.

## Data Background

The data set we chose is monthly climate data recorded in Milan, Italy,
between January 1763 and November 2008. We can use this data to analyze
climate patterns, and possibly use these patterns to correlate with
historical/current events that may explain the changes to climate
patterns. Do keep in mind, this is one of one thousand data sets meaning
this is only a fraction of the total data resource for researchers,
scientists, and those seeking to understand and analyze climate patterns
and changes.

The original data set has different information regarding both
temperature and precipitation data, with further on more information
about specific weather observations in the months. Since this based on a
month-by-month set throughout the years, we can see patterns, even in
older years, as long as only a few data points are missing.

### Dataset

[Milan Weather Recording Station from NCEI
(https://www.ncei.noaa.gov/access/search/data-search/global-summary-of-the-month?startDate=1800-01-03T00:00:00&endDate=1800-01-03T23:59:59)](https://www.ncei.noaa.gov/access/search/data-search/global-summary-of-the-month?startDate=1800-01-03T00:00:00&endDate=1800-01-03T23:59:59)

### Column Background

**Degree Days**

- Degree Days: days in a month where the temperature is above or below
  the mean temperature for that month, measured in points where each
  point is a degree above or below the mean.

- Degree Cooling Days: days of the month with a temperature below that
  month’s mean

- Degree Heating Days: days of the month with a temperature above that
  month’s mean

**Temperature**

- TAVG: Average temperature in a month

- TMAX: Maximum temperature in a month

- TMIN: Minimum temperature in a month

- DT32: Temperature above 32 degrees celcius

**Location**

- Station: Unique station ID; where data was collected

- Name: Name of station; where data was collected

- Date: Year and month data was collected

- Latitude/Longitude/Elevation: Coordinates for station

**Precipitation**

- PRCP: Total precipitation for a month

- EMXP: Highest amount of precipitation in a given year

- EMXP: Lowest amount of precipitation in a given year

### Actual Columns

- Extreme maximum precipitation
- Extreme maximum temperature
- Precipitation
- Number days with maximum temperature greater than 90F (32.2C)
- Number days with greater than 0.10 inch (2.54mm) of precipitation
- Heating Degree Days Season to TIME
- Heating Degree Days
- Number days with maximum temperature greater than 70F (21.1C)
- Cooling Degree Days Season to Date
- Number days with greater than 0.01 inch (0.25mm) of precipitation
- Day of month of highest daily total of precipitation
- Extreme minimum temperature
- Number days with minimum temperature less than 32F (0C)
- Number days with minimum temperature less than 0F (-17.6C)
- Day of month with extreme maximum temperature
- Number days with maximum temperature less than 32F (0C)
- Number days with greater than 1.00 inch (25.4mm) of precipitation
- Cooling Degree Days
- Average Maximum Temperature
- Average Average Temperature
- Average Minimum Temperature
- Day of month of extreme minimum temperature

## Importing Data

Now that we have determined the dataset we wish to use, it is as simple
as downloading it from the official source found to the CSV format. This
allows us to easily import it as a malleable object.

#### Importanting Libraries

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(dplyr)
library(ggplot2)
```

The libraries we are using are for inline operations, and plotting.

#### Important Data from CSV

``` r
data <- read_csv("milan.csv")
```

    ## Rows: 2949 Columns: 50
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (25): STATION, DATE, NAME, CDSD_ATTRIBUTES, CLDD_ATTRIBUTES, DP01_ATTRIB...
    ## dbl (25): LATITUDE, LONGITUDE, ELEVATION, CDSD, CLDD, DP01, DP10, DP1X, DT00...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(data)
```

    ## # A tibble: 6 × 50
    ##   STATION   DATE  LATITUDE LONGITUDE ELEVATION NAME   CDSD CDSD_ATTRIBUTES  CLDD
    ##   <chr>     <chr>    <dbl>     <dbl>     <dbl> <chr> <dbl> <chr>           <dbl>
    ## 1 ITE00100… 1763…     45.5      9.19       150 MILA…   0   E                 0  
    ## 2 ITE00100… 1763…     45.5      9.19       150 MILA…   0   E                 0  
    ## 3 ITE00100… 1763…     45.5      9.19       150 MILA…   0   E                 0  
    ## 4 ITE00100… 1763…     45.5      9.19       150 MILA…   0   E                 0  
    ## 5 ITE00100… 1763…     45.5      9.19       150 MILA…   7.4 E                 7.4
    ## 6 ITE00100… 1763…     45.5      9.19       150 MILA…  78   E                70.6
    ## # ℹ 41 more variables: CLDD_ATTRIBUTES <chr>, DP01 <dbl>,
    ## #   DP01_ATTRIBUTES <chr>, DP10 <dbl>, DP10_ATTRIBUTES <chr>, DP1X <dbl>,
    ## #   DP1X_ATTRIBUTES <chr>, DT00 <dbl>, DT00_ATTRIBUTES <chr>, DT32 <dbl>,
    ## #   DT32_ATTRIBUTES <chr>, DX32 <dbl>, DX32_ATTRIBUTES <chr>, DX70 <dbl>,
    ## #   DX70_ATTRIBUTES <chr>, DX90 <dbl>, DX90_ATTRIBUTES <chr>, DYNT <dbl>,
    ## #   DYNT_ATTRIBUTES <chr>, DYXP <dbl>, DYXP_ATTRIBUTES <chr>, DYXT <dbl>,
    ## #   DYXT_ATTRIBUTES <chr>, EMNT <dbl>, EMNT_ATTRIBUTES <chr>, EMXP <dbl>, …

Since we have already downloaded our data to a CSV file, we only need to
import it from that file.

#### Data Time Frame

``` r
min(data$DATE)
```

    ## [1] "1763-01"

``` r
max(data$DATE)
```

    ## [1] "2008-11"

This function returns the first, and last date in the dataset. The first
date is January, 1763, and the final date is November, 2008.

#### Data Columns

``` r
colnames(data)
```

    ##  [1] "STATION"         "DATE"            "LATITUDE"        "LONGITUDE"      
    ##  [5] "ELEVATION"       "NAME"            "CDSD"            "CDSD_ATTRIBUTES"
    ##  [9] "CLDD"            "CLDD_ATTRIBUTES" "DP01"            "DP01_ATTRIBUTES"
    ## [13] "DP10"            "DP10_ATTRIBUTES" "DP1X"            "DP1X_ATTRIBUTES"
    ## [17] "DT00"            "DT00_ATTRIBUTES" "DT32"            "DT32_ATTRIBUTES"
    ## [21] "DX32"            "DX32_ATTRIBUTES" "DX70"            "DX70_ATTRIBUTES"
    ## [25] "DX90"            "DX90_ATTRIBUTES" "DYNT"            "DYNT_ATTRIBUTES"
    ## [29] "DYXP"            "DYXP_ATTRIBUTES" "DYXT"            "DYXT_ATTRIBUTES"
    ## [33] "EMNT"            "EMNT_ATTRIBUTES" "EMXP"            "EMXP_ATTRIBUTES"
    ## [37] "EMXT"            "EMXT_ATTRIBUTES" "HDSD"            "HDSD_ATTRIBUTES"
    ## [41] "HTDD"            "HTDD_ATTRIBUTES" "PRCP"            "PRCP_ATTRIBUTES"
    ## [45] "TAVG"            "TAVG_ATTRIBUTES" "TMAX"            "TMAX_ATTRIBUTES"
    ## [49] "TMIN"            "TMIN_ATTRIBUTES"

This function prints out all of the column names in the original
dataset.

## Cleaning Data

Now that we have successfully imported the data, we will clean up our
data object so our results are more accurate, and understandable.

#### Finding Important Variables

To ‘weed out’ invaluable variables, we will search for variables that
lack the proper time frame, are null, or incomplete.

``` r
# Determining if the location value changes
print("Latitude:")
```

    ## [1] "Latitude:"

``` r
unique(data$LATITUDE)
```

    ## [1] 45.4717

``` r
print("Longitude:")
```

    ## [1] "Longitude:"

``` r
unique(data$LONGITUDE)
```

    ## [1] 9.1892

``` r
# Determine if all variables have the same time frame
print("Number of NA values per column:")
```

    ## [1] "Number of NA values per column:"

``` r
colSums(is.na(data))
```

    ##         STATION            DATE        LATITUDE       LONGITUDE       ELEVATION 
    ##               0               0               0               0               0 
    ##            NAME            CDSD CDSD_ATTRIBUTES            CLDD CLDD_ATTRIBUTES 
    ##               0             227             238              50              50 
    ##            DP01 DP01_ATTRIBUTES            DP10 DP10_ATTRIBUTES            DP1X 
    ##            1139            1139            1139            1139            1139 
    ## DP1X_ATTRIBUTES            DT00 DT00_ATTRIBUTES            DT32 DT32_ATTRIBUTES 
    ##            1139              14              14              14              14 
    ##            DX32 DX32_ATTRIBUTES            DX70 DX70_ATTRIBUTES            DX90 
    ##              18              18              18              18              18 
    ## DX90_ATTRIBUTES            DYNT DYNT_ATTRIBUTES            DYXP DYXP_ATTRIBUTES 
    ##              18              14              14            1139            1139 
    ##            DYXT DYXT_ATTRIBUTES            EMNT EMNT_ATTRIBUTES            EMXP 
    ##              18              18              14              14            1139 
    ## EMXP_ATTRIBUTES            EMXT EMXT_ATTRIBUTES            HDSD HDSD_ATTRIBUTES 
    ##            1139              18              18             288             293 
    ##            HTDD HTDD_ATTRIBUTES            PRCP PRCP_ATTRIBUTES            TAVG 
    ##              50              50            1139            1139              27 
    ## TAVG_ATTRIBUTES            TMAX TMAX_ATTRIBUTES            TMIN TMIN_ATTRIBUTES 
    ##              27              18              18              14              14

As seen, DP values have quite a few more NA values than DT/DX values.
Since are several null-value rows, we will drow rows hat contain null
values. Also, when checking precipitation data, we see that it is
missing all dates before 1858, negating the first nearly 100 years. This
will be removed since the values will be biased towards later dates.
Location data is also not important since all of the measurements were
recorded from the same weather station.

#### Creating a Clean Object

Drop null values, drop precipitation data (due to lack of data within
timeframe), and remove location data since all of the recordings
happened from the same location.

``` r
#Grabs data and names columns to more reasonable col names. NOTE: DX and DY values are in degrees F, so changed to more accurate degrees C titles to match all other vars. 
milanClimate <- data %>%
  select(
    DATE,
    MEAN = TAVG,
    MEAN_MAX = TMAX,
    MEAN_MIN = TMIN,
    HEAT_DEG_DAYS = HTDD,
    COOL_DEG_DAYS = CLDD,
    HIGHEST_TEMP = EMXT,
    HIGHEST_DAY = EMXT_ATTRIBUTES,
    COOLEST_TEMP = EMNT,
    COOLEST_DAY = EMNT_ATTRIBUTES,
    GTE_32 = DX90,
    GTE_21 = DX70,
    GTE_00 = DX32,
    LTE_00 = DT32,
    LTE_N18 = DT00
  )

# Change the date column into a more usable format.
milanClimate$DATE <- lubridate::ym(milanClimate$DATE)

# Clean and remove unnessicary character in this attribute.
milanClimate$HIGHEST_DAY <- as.numeric(substr(gsub('\\D','',milanClimate$HIGHEST_DAY), nchar(gsub('\\D','',milanClimate$HIGHEST_DAY))-1, nchar(gsub('\\D','',milanClimate$HIGHEST_DAY))))

# Clean and remove unnessicary character in this attribute.
milanClimate$COOLEST_DAY <- as.numeric(substr(gsub('\\D','',milanClimate$COOLEST_DAY), nchar(gsub('\\D','',milanClimate$COOLEST_DAY))-1, nchar(gsub('\\D','',milanClimate$COOLEST_DAY))))

# Show cleaned data columns.
colnames(milanClimate)
```

    ##  [1] "DATE"          "MEAN"          "MEAN_MAX"      "MEAN_MIN"     
    ##  [5] "HEAT_DEG_DAYS" "COOL_DEG_DAYS" "HIGHEST_TEMP"  "HIGHEST_DAY"  
    ##  [9] "COOLEST_TEMP"  "COOLEST_DAY"   "GTE_32"        "GTE_21"       
    ## [13] "GTE_00"        "LTE_00"        "LTE_N18"

We have removed all of the null-value rows, and cleaned up the column
names for easier readability.

## Marginal Summaries

Now that we have a cleaned data object, we can begin to plot charts to
find and demonstrate different trends.

### Data Time Frame

``` r
# First Date
subset_min <- milanClimate %>%
  filter(MEAN == min(MEAN, na.rm = TRUE)) %>%
  select(DATE, MEAN, MEAN_MIN, MEAN_MAX)
# subset_min

# Final Date
subset_max <- milanClimate %>%
  filter(MEAN == max(MEAN, na.rm = TRUE)) %>%
  select(DATE, MEAN, MEAN_MIN, MEAN_MAX)
# subset_max

subset_min_max <- bind_rows(subset_min, subset_max)
subset_min_max # Highest and Lowest Temperatures
```

    ## # A tibble: 2 × 4
    ##   DATE        MEAN MEAN_MIN MEAN_MAX
    ##   <date>     <dbl>    <dbl>    <dbl>
    ## 1 1767-01-01 -4.75    -6.72    -2.77
    ## 2 2006-07-01 31.2     25.8     36.5

Above, you can see the time frame this data exists within.

### Monthly Temperature Range

``` r
ggplot(milanClimate, aes(x=DATE, y=MEAN)) +
  geom_bar(stat="identity", fill="blue", width=0.5) +
  geom_errorbar(aes(ymin = MEAN_MIN, ymax = MEAN_MAX), width = 0.2, position = position_dodge(width = 0.5)) +
  labs(x="Year", y="Temperature (C)") +
  ggtitle("Annual Temperature Ranges")
```

    ## Warning: Removed 27 rows containing missing values (`position_stack()`).

![](README_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

From this temperature range graph, you can see some trends, especially
into the 2000s.

``` r
# Create a subset
ex <- milanClimate
ex$DATE <- factor(ex$DATE)

# Extract month and year
ex$Month = month(ex$DATE)
```

    ## Warning: tz(): Don't know how to compute timezone for object of class factor;
    ## returning "UTC".

``` r
ex$Year = year(ex$DATE)
```

    ## Warning: tz(): Don't know how to compute timezone for object of class factor;
    ## returning "UTC".

``` r
ex$Year = as.numeric(ex$Year)

# Plot the data
ggplot(ex, aes(x = Month, y = MEAN, color = factor(Year))) +
  geom_point() +
  geom_line() +
  scale_x_continuous(breaks = 1:12, labels = month.abb) +  # Set breaks and labels for the x-axis
  labs(x = "Month", y = "MEAN", title = "Mean values over months") +
  theme(legend.position = "none")  # Hide the legend
```

    ## Warning: Removed 27 rows containing missing values (`geom_point()`).

    ## Warning: Removed 6 rows containing missing values (`geom_line()`).

![](README_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

This graph displays the same data as above, but highlights the
temperature trend over the year.

### Annual Temperature Trend

``` r
# Monthly averages
ggplot(milanClimate, aes(x=DATE, y=MEAN)) +
  geom_point(color='blue') +
  geom_smooth(method='lm', color='red') +
  labs(x="Year", y="Temperature (C)") +
  ggtitle("Average Temperature by Date with Trend")
```

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 27 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 27 rows containing missing values (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

The above graph shows a clear upwards trend in average temperature over
the time frame of the data. Let’s figure out what the exact difference
is.

### Increase in Average Temperature

``` r
# TODO: Coleman, calculate the average of the last and first year, subtract for average increase

firstLastYear <- milanClimate %>%
    mutate(
      year = year(DATE),
      month = month(DATE)
    ) %>% group_by(year) %>%
  select(year, MEAN) %>%
  summarise(
    averageTemp = mean(MEAN)
  ) %>% filter(
    year == 1763 | year == 2006
  )

Mean2008 <- firstLastYear[[2,2]]
Mean1763 <- firstLastYear[[1,2]]
avgIncrease <- Mean2008 - Mean1763

print(avgIncrease)
```

    ## [1] 5.541667

The above highlights an average increase of 5.54 degrees (C) from the
beginning of weather recording to the last recorded year.

### Average Annual Temperature Trend

``` r
# Extract year from date column
new_data <- milanClimate %>%
  mutate(year = lubridate::year(DATE))

# Create a summary dataframe with yearly statistics
summary_df <- new_data %>%
  group_by(year) %>%
  summarise(
    MEAN = mean(MEAN, na.rm = TRUE),
    MIN = min(MEAN_MIN, na.rm = TRUE),
    MAX = max(MEAN_MAX, na.rm = TRUE)
  )

# Print the summary dataframe
ggplot(summary_df, aes(x=year, y=MEAN)) +
  geom_bar(stat="identity", fill="blue", width=0.5) +
  geom_smooth(method='lm', color='red') +
  labs(x="Year", y="Temperature (C)") +
  ggtitle("Annual Temperature Average with Trend")
```

    ## `geom_smooth()` using formula = 'y ~ x'

![](README_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

### Other Elements

``` r
ggplot(milanClimate, aes(x=DATE, y=MEAN_MAX)) +
  geom_point(color='blue') +
  geom_smooth(method='lm', color='red') +
  labs(x="Year", y="Temperature (C)") +
  ggtitle("Average Maximum Temperature Annualy")
```

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 18 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 18 rows containing missing values (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
ggplot(milanClimate, aes(x=DATE, y=MEAN_MIN)) +
  geom_point(color='blue') +
  geom_smooth(method='lm', color='red') +
  labs(x="Year", y="Temperature (C)") +
  ggtitle("Average Minimum Temperature Annualy")
```

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 14 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 14 rows containing missing values (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-13-2.png)<!-- -->

``` r
ggplot(milanClimate, aes(x=DATE, y=HEAT_DEG_DAYS)) +
  geom_point(color='blue') +
  geom_smooth(method='lm', color='red') +
  labs(x="Year", y="Number of Days") +
  ggtitle("Heating Days")
```

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 50 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 50 rows containing missing values (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-13-3.png)<!-- -->

``` r
ggplot(milanClimate, aes(x=DATE, y=COOL_DEG_DAYS)) +
  geom_point(color='blue') +
  geom_smooth(method='lm', color='red') +
  labs(x="Year", y="Number of Days") +
  ggtitle("Cooling Days")
```

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 50 rows containing non-finite values (`stat_smooth()`).
    ## Removed 50 rows containing missing values (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-13-4.png)<!-- -->

``` r
ggplot(milanClimate, aes(x=DATE, y=GTE_32)) +
  geom_point(color='blue') +
  geom_smooth(method='lm', color='red') +
  labs(x="Year", y="Number of Days") +
  ggtitle("Temperatures above 32C")
```

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 18 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 18 rows containing missing values (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-13-5.png)<!-- -->

The average maximum temperature sees a clear annual increase, this is
very similar to the increase we saw in the previous graph, and explains
the increase of average temperatures. The minimum temperatures saw a
slight increase but it is so small, it is untelling. The number of
heating days went down, and the number of cooling days went up. This
means that there average temperatures are increasing, so, seemingly
normal temperatures appear to be much cooler. The number of days with
temperatures above 32 degrees (C) saw a massive leap beginning around
1850, falling off around 1913, and then re-rising shortly after 1950.
This is something important to explore further.

## Investigation

Now that we can see clear trends in the temperature increase, we want to
explore some potential factors that influence this shift.

### Industrialization of Italy

The industrial revolution began in Milan, Italy, around 1850 with cotton
processing. Industrialization peaked between 1897-1913. Looking back on
the previous graph, of temperatures greater than 32 degrees (C), we can
see a dramatic increase of these extreme temperatures beginning around
1841, and tapering off in 1913. What followed was World War I, and Milan
began a steady decrease in industry, and population due to multiple
wars. Following the end of World War II, around the 1950s, until 1973,
per capita GDP rose by an average of more than 5% annually, reaching a
peak of 7.72% in 1961. This time frame correlates directly to the second
increase of temperatures above 32 degrees (C). (3,4)

### Milan’s Population

Along with the economic success of Milan, and the rest of Italy, and the
return of displaced peoples following WWII, Milan’s population grew
rapidly, nearly doubling between 1950 and 1972. With year-over-year
population increases of about 5% during this time period, we can also
derive a correlation between population growth and these temperatures.
(5)

### Other Factors

While industrialization, and population growth appear to play a
significant role in the increase of average temperatures in Milan, there
are certainly other factors. Going forward, to better understand such
factors, it would be ideal to create statistical models that correlate
directly between such trends. Searching local and global news from these
time periods led us to these conclusions, but there are always
unexpected factors that can lead to the same conclusions.

## Conclusion

The United Nations’ concerns appear to have some legitimacy behind them.
From our analysis, there were clear trends showing a rise in average
temperature in Milan. Increases in average temperature, paired with new
extreme highs, as we saw in the graph showing every time the temperature
rose above 32 degrees (C), clearly demonstrate a heating climate.
Without context, this could be seen as a naturally occurring phenomena
until compared with outside sources.

When comparing economic trends, the rise of industrialization,
subsequent declination, and return, it is apparent, there is no
phenomena occurring. Instead, we see a direct correlation between the
population, GDB, economic success, and a rise in temperatures.

The United Nations defines climate change as “Climate change refers to
long-term shifts in temperatures and weather patterns. Such shifts can
be natural, due to changes in the sun’s activity or large volcanic
eruptions. But since the 1800s, human activities have been the main
driver of climate change, primarily due to the burning of fossil fuels
like coal, oil and gas.” And, as you see year-over-year increases in
temperatures, it is indication of some level of climate change.

Going forward, if more were to come of this study, broadening our data
would be the first step. To truly find and understand all
climate-related trends, we need to assess weather, temperature, local,
and global events, carbon emission, green-house gases, and much more.
Refining and cleaning data is an important step for finding clear,
understandable patterns. How can we look to Milan as an example, and
understand how similar trends affect the rest of the world? Can we use
former trends to predict future events, or how to mitigate the effects
of climate change?

## References

1.  United Nations, <https://www.un.org/sustainabledevelopment/>
2.  Milan Weather Recording Station, NCEI,
    <https://www.ncei.noaa.gov/access/search/data-search/global-summary-of-the-month?startDate=1800-01-03T00:00:00&endDate=1800-01-03T23:59:59>
3.  Industrial Revolution of Milan, Italy
    <https://www.erih.net/how-it-started/industrial-history-of-european-countries/italy#>:~:text=The%20Industrial%20Revolution%20swept%20the,plant%20near%20Naples%20in%201908
4.  Economic Growth of Italy
    <https://ideas.repec.org/p/pra/mprapa/12817.html>
5.  Milan Population 2023
    <https://worldpopulationreview.com/world-cities/milan-population>
