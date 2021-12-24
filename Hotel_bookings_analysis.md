Hotel bookings
================
Ifeoluwa
12/20/2021

## Background for this project

In this project,I reviewed a scenario, added annotations to a data
visualization with ggplot2. I also saved images from ggplot2
visualizations so I can add them directly to presentations

## The Scenario

As a junior data analyst for a hotel booking company,your stakeholder
asks you to add annotations to your visualizations to help explain your
findings in a presentation.

## Step 1: Import your data

Import my data with the read.csv function

``` r
hotel_bookings <- read.csv("hotel_bookings.csv")
```

## Step 2: Browse through our data

Lets get familiar with this data set with the `head()` and `colnames()`
functions. Run two code chunks below to get at a sample of the data and
also preview all the column names

``` r
head(hotel_bookings)
```

    ##          hotel is_canceled lead_time arrival_date_year arrival_date_month
    ## 1 Resort Hotel           0       342              2015               July
    ## 2 Resort Hotel           0       737              2015               July
    ## 3 Resort Hotel           0         7              2015               July
    ## 4 Resort Hotel           0        13              2015               July
    ## 5 Resort Hotel           0        14              2015               July
    ## 6 Resort Hotel           0        14              2015               July
    ##   arrival_date_week_number arrival_date_day_of_month stays_in_weekend_nights
    ## 1                       27                         1                       0
    ## 2                       27                         1                       0
    ## 3                       27                         1                       0
    ## 4                       27                         1                       0
    ## 5                       27                         1                       0
    ## 6                       27                         1                       0
    ##   stays_in_week_nights adults children babies meal country market_segment
    ## 1                    0      2        0      0   BB     PRT         Direct
    ## 2                    0      2        0      0   BB     PRT         Direct
    ## 3                    1      1        0      0   BB     GBR         Direct
    ## 4                    1      1        0      0   BB     GBR      Corporate
    ## 5                    2      2        0      0   BB     GBR      Online TA
    ## 6                    2      2        0      0   BB     GBR      Online TA
    ##   distribution_channel is_repeated_guest previous_cancellations
    ## 1               Direct                 0                      0
    ## 2               Direct                 0                      0
    ## 3               Direct                 0                      0
    ## 4            Corporate                 0                      0
    ## 5                TA/TO                 0                      0
    ## 6                TA/TO                 0                      0
    ##   previous_bookings_not_canceled reserved_room_type assigned_room_type
    ## 1                              0                  C                  C
    ## 2                              0                  C                  C
    ## 3                              0                  A                  C
    ## 4                              0                  A                  A
    ## 5                              0                  A                  A
    ## 6                              0                  A                  A
    ##   booking_changes deposit_type agent company days_in_waiting_list customer_type
    ## 1               3   No Deposit  NULL    NULL                    0     Transient
    ## 2               4   No Deposit  NULL    NULL                    0     Transient
    ## 3               0   No Deposit  NULL    NULL                    0     Transient
    ## 4               0   No Deposit   304    NULL                    0     Transient
    ## 5               0   No Deposit   240    NULL                    0     Transient
    ## 6               0   No Deposit   240    NULL                    0     Transient
    ##   adr required_car_parking_spaces total_of_special_requests reservation_status
    ## 1   0                           0                         0          Check-Out
    ## 2   0                           0                         0          Check-Out
    ## 3  75                           0                         0          Check-Out
    ## 4  75                           0                         0          Check-Out
    ## 5  98                           0                         1          Check-Out
    ## 6  98                           0                         1          Check-Out
    ##   reservation_status_date
    ## 1              2015-07-01
    ## 2              2015-07-01
    ## 3              2015-07-02
    ## 4              2015-07-02
    ## 5              2015-07-03
    ## 6              2015-07-03

``` r
colnames(hotel_bookings)
```

    ##  [1] "hotel"                          "is_canceled"                   
    ##  [3] "lead_time"                      "arrival_date_year"             
    ##  [5] "arrival_date_month"             "arrival_date_week_number"      
    ##  [7] "arrival_date_day_of_month"      "stays_in_weekend_nights"       
    ##  [9] "stays_in_week_nights"           "adults"                        
    ## [11] "children"                       "babies"                        
    ## [13] "meal"                           "country"                       
    ## [15] "market_segment"                 "distribution_channel"          
    ## [17] "is_repeated_guest"              "previous_cancellations"        
    ## [19] "previous_bookings_not_canceled" "reserved_room_type"            
    ## [21] "assigned_room_type"             "booking_changes"               
    ## [23] "deposit_type"                   "agent"                         
    ## [25] "company"                        "days_in_waiting_list"          
    ## [27] "customer_type"                  "adr"                           
    ## [29] "required_car_parking_spaces"    "total_of_special_requests"     
    ## [31] "reservation_status"             "reservation_status_date"

## Step 3: Install and load the ‘ggplot2’ and ‘tidyverse’ packages (optional)

If you haven’t already installed and loaded the `ggplot2` package, you
will need to do that before you can use the `ggplot()` function. You
only have to do this once though, not every time you call `ggplot()`.

You can also skip this step if you haven’t closed your RStudio account
since doing the last activity. If you aren’t sure, you can run the code
chunk and hit ‘cancel’ if the warning message pops up telling you that
have already downloaded the `ggplot2` package.

Run the code chunk below to install and load `ggplot2`. This may take a
few minutes!

{r loading and installing ggplot2, echo=FALSE, message=FALSE}
install.packages(‘ggplot2’) library(ggplot2)

If you haven’t installed and loaded tidyverse in this RStudio session,
you can run the code chunk below. This may take a few minutes!

``` r
#install.packages('tidyverse')
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.6     v dplyr   1.0.7
    ## v tidyr   1.1.4     v stringr 1.4.0
    ## v readr   2.1.0     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

## Step 4: Annotating your chart

Your stakeholder asked a visualization breaking down payment type by
city because it will help inform how the company targets promotions in
the future. They ask you to create a cleaned and labeled version and
save it as a .png file for them to include in a presentation

``` r
ggplot(data = hotel_bookings) +
  geom_bar(mapping = aes(x = market_segment)) +
  facet_wrap(~hotel) +
  labs(title="Comparison of market segments by hotel type for hotel bookings")
```

![](Hotel_bookings_analysis_files/figure-gfm/faceting%20a%20plot%20with%20a%20title-1.png)<!-- -->

This code chunk will generate a decent chart but you may also want to
add another detail about what time period this data covers. To do this,
you need to find out when the data is from.

You realize you can use the `min()` function on the year column in the
data:

``` r
min(hotel_bookings$arrival_date_year)
```

    ## [1] 2015

And the `max()` function:

``` r
max(hotel_bookings$arrival_date_year)
```

    ## [1] 2017

I saved them as variables in order to easily use them in labeling; the
following code chunk creates two of those variables:

``` r
mindate <- min(hotel_bookings$arrival_date_year)
maxdate <- max(hotel_bookings$arrival_date_year)
```

Now, I added in a subtitle using `subtitle=` in the `labs()` function.
Then, I used the `paste0()` function to use the newly-created variables
in the labels.I also used the ‘Theme()’ function to rotate the label on
the x axis to correct the obvious clumsiness from the previous graph :

``` r
ggplot(data = hotel_bookings) +
  geom_bar(mapping = aes(x = market_segment)) +
  facet_wrap(~hotel) +
  theme(axis.text.x = element_text(angle = 45)) +
  labs(title="Comparison of market segments by hotel type for hotel bookings",
       subtitle=paste0("Data from: ", mindate, " to ", maxdate))
```

![](Hotel_bookings_analysis_files/figure-gfm/city%20bar%20chart%20with%20timeframe-1.png)<!-- -->
This code chunk added the subtitle ‘Data from: 2015 to 2017’ underneath
the title I added earlier to the chart.

I decided to change the `subtitle` to a `caption` which will appear in
the bottom right corner instead.

``` r
ggplot(data = hotel_bookings) +
  geom_bar(mapping = aes(x = market_segment)) +
  facet_wrap(~hotel) +
  theme(axis.text.x = element_text(angle = 45)) +
  labs(title="Comparison of market segments by hotel type for hotel bookings",
       caption=paste0("Data from: ", mindate, " to ", maxdate))
```

![](Hotel_bookings_analysis_files/figure-gfm/city%20bar%20chart%20with%20timeframe%20as%20caption-1.png)<!-- -->
This code chunk made a slight change to the visualization I created in
the last chunk; now the “data from: 2015 to 2017” subtitle is in the
bottom right corner.

Now I cleaned up the x and y axis labels to make sure they are really
clear. To do that, I added to the `labs()` function and use `x=` and
`y=`. Feel free to change the text of the label and play around with it:

``` r
ggplot(data = hotel_bookings) +
  geom_bar(mapping = aes(x = market_segment)) +
  facet_wrap(~hotel) +
  theme(axis.text.x = element_text(angle = 45)) +
  labs(title="Comparison of market segments by hotel type for hotel bookings",
       caption=paste0("Data from: ", mindate, " to ", maxdate),
       x="Market Segment",
       y="Number of Bookings")
```

![](Hotel_bookings_analysis_files/figure-gfm/city%20bar%20chart%20with%20x%20and%20y%20axis-1.png)<!-- -->
Now I have the data visualization from earlier, but now the x and y axis
labels have been changed from ‘market_segment’ and ‘count’ to ‘Market
Segment’ and ‘Number of Bookings’ so that the chart is clearer
