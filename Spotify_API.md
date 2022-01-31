Accessing Spotify API using R
================
31-01-2022

## Background for this project

This is a project to explore the (Music streaming app) Spotify’s API. We
will be exploring three of the biggest Afro beats albums in recent
years, namely; Made in Lagos, Twice as Tall, and A Good Time.

##Step 1: Declaring our clientid and Secret First, you will have to
create a spotify developer account in order to get your “client id” and
“secret”,which is pretty easy as long as you have the spotify regular
account.

``` r
id <- '459648c5a59e4a19bf59c5b83f9ffa38'
secret <- '6f7224e5b46143ba847adea3dd972f85'
```

## Step 2: Install and load the needed packages

``` r
install.packages("spotifyr", repos = "http://cran.us.r-project.org")
```

    ## Installing package into 'C:/Users/LENOVO/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'spotifyr' successfully unpacked and MD5 sums checked
    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\LENOVO\AppData\Local\Temp\Rtmpm0VL4H\downloaded_packages

``` r
install.packages("tidyverse", repos = "http://cran.us.r-project.org")
```

    ## Installing package into 'C:/Users/LENOVO/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'tidyverse' successfully unpacked and MD5 sums checked
    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\LENOVO\AppData\Local\Temp\Rtmpm0VL4H\downloaded_packages

``` r
library(spotifyr)
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

## Step 3: Getting spotify access token using functions from the spoitfyr package

``` r
Sys.setenv(SPOTIFY_CLIENT_ID = id)
Sys.setenv(SPOTIFY_CLIENT_SECRET = secret)

access_token <- get_spotify_access_token()
```

## Step 4: getting our album ids

This can be found on the url of the albums page on spotify web. I used
the spotify desktop app so i got it from “… \> share \> copy link”
option.

Then assign the ids

``` r
MIL = '6bCs4XCCkm9cTwlswlu0VD'
TAT = '2pANu4qucnliJuRR94eZSV'
AGT = '0s3BbZlcqsUdAD8wIYdO5n'
```

## Step 5: get all albums tracks and make them a dataframe

``` r
MIL_album <- get_album_tracks(MIL,authorization = access_token )

TAT_album <- get_album_tracks(TAT,authorization = access_token )

AGT_album <- get_album_tracks(AGT,authorization = access_token )
```

## Step 6: Lets combine all 3 data frames with rbind function

``` r
All_album <- rbind(MIL_album,TAT_album,AGT_album)
view(All_album)
```

## Step 7: Filtering the combined dataframe by selecting the needed columns

``` r
All_tracks.df <- subset(All_album, 
      select = c(name,available_markets,duration_ms,explicit,id,track_number))
 view(All_tracks.df)
```

## Step 8: Getting all tracks features

I had to copy all the track ids one by one, its a bit tedious I know.
But hey - we are beginners here, and it works lol.

``` r
 All_tracks_id = '2cuZU2ssATNb1Ey1SB1V1X,5TOoNqmK73ev73C5JiJ5yC,1i2HKpJ5A9ebyPxrbgoi3B,0N4ufAwa0NwpumEFqVXtek,1eUTZXovJXU3Eb1Gyk1ibK,430wk0UdTXB5gaOCjHHgfq,4eg9kaGGZjfQpxLb8isiO4,08jx6kRJNOggEc1QLFYacW,3IjsZ7wsE0aQgtb2crMbcC,4TqssI52mf1vE6K6ZjZq4A,7JATnENsPMMQWtvMsQnW23,1i63fAE1LEghiIVEbrTtWr,0WQb1ms6xMQ0gKrCUqraYk,0ui4TcK8tcHWZ4JnBR6lIa,60lUecrFeE2t6QMJ1Nmsve,6jdTkoEaer7XNGSblczoSu,6mAdcIFP25eb37HjkzglSh,1MZtr7IH5qtjIkqrXj8WOJ,1wtItxODWlAKjWSi40OckI,1Ni4AHXRT2LqVI9Whc8Lyf,3bOBWIdkRyN9yaGJ7uSOTf,36McH8jwS5UGpvyAlkAP2o,4sHydcUBIWRD5kVmMzci2E,5gsvgZuxT41OWmH03SBT8J,5dLqdZ4GNmd5lfQVRWBYYF,3L0LXTrJEMDDBROuc9rdPr,238Mi54IiKSoMfbZMlob2l,0zgeYAouscRmTZ90HM1NA3,1taXjBXUnhPCPunwB6xOgp,70FNZikgqoFOxAe64IHolx,4Br1LAkqDAIwgEkkuXKZxJ,2eFsasDs4w4YUHBvaKyNNZ,59r8MRjv8K2rx8W3jQ5HW2,0H9agEp8BXR4S6DI50rmTU,3AKPoi06BFR4vrK7alGjfi,5q1Go2adbGbqjgXxSD0UZS,1alvkxYJx3AcVERNyFJRmF,0WeN52xa8nBDBfKsaiKJ0i,0xr7t6jQWzFsZ9XwfcxAu7,3ICvYCODRVnpP3MRp8gfux,5CWaYPulpYMRRl1ToR6yO7,2ylO41DTQwQv1QH1mSP3cH,1hEXElwyPez2z7m5dZ56Mc,32N5JyUQ6SzkapNGe2JOMi,5BiGfGgWq4CMHmFp5cRIqm,2PdKTWP8NA6O9KMqOGqNBv,3ZJblAM95vwSKA5IUloPJh,3MYG7lZANqw54i2Du7Y0WN,5ZzXbHAHU5i8dzRpDPLFWg,7zOWMvYYVmAj5k1NoXNurV'
 
 All_tracksf <- get_track_audio_features(All_tracks_id, 
                                        authorization = access_token)
 view(All_tracksf)
```

## Step 9: Merging our dataframes; All_tracks.df and All_tracksf

``` r
Top3_data <- merge(All_tracks.df,All_tracksf, by= "id", all = TRUE)

view(Top3_data)
```

## Step 10: Cleaning the data further by removing duplicate and irrelevant columns

``` r
Top_albums.df <- subset(Top3_data,
                       select = -c(uri,track_href,available_markets, analysis_url,duration_ms.y))
view(Top_albums.df)
```

## Step 11: Saving our dataframe as a csv file

``` r
write.csv(Top_albums.df,"C:/Users/LENOVO/Documents/CREDS/Portfolio/Top3_albums.csv",row.names= FALSE)
```

###### This dataset is futher visualized on Tableau, you can check out Top afro beat albums viz [here](https://public.tableau.com/app/profile/babalola.ifeoluwa)

###### You can check out these resources which came in handy for me during this process.[Here](https://medium.com/swlh/accessing-spotifys-api-using-r-1a8eef0507c) and [here](https://msmith7161.github.io/what-is-speechiness/)
