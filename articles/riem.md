# riem

The riem package allows to get weather data from ASOS stations
(airports) via the awesome website of the [Iowa Environment
Mesonet](https://mesonet.agron.iastate.edu/request/download.phtml?network=IN__ASOS).

## Installation

Install the package with:

``` r

install.packages("riem")
```

Or install the development version using
[devtools](https://github.com/hadley/devtools) with:

``` r

library("devtools")
install_github("ropenscilabs/riem")
```

## Get available networks

``` r

library("riem")
riem_networks()
```

    ## # A tibble: 266 × 2
    ##    code     name                     
    ##    <chr>    <chr>                    
    ##  1 AE__ASOS United Arab Emirates ASOS
    ##  2 AF__ASOS Afghanistan ASOS         
    ##  3 AG__ASOS Antigua and Barbuda ASOS 
    ##  4 AI__ASOS Anguilla ASOS            
    ##  5 AK_ASOS  Alaska ASOS              
    ##  6 AL__ASOS Albania ASOS             
    ##  7 AL_ASOS  Alabama ASOS             
    ##  8 AM__ASOS Armenia ASOS             
    ##  9 AN__ASOS Netherlands Antilles ASOS
    ## 10 AO__ASOS Angola ASOS              
    ## # ℹ 256 more rows

## Get available stations for one network

``` r

riem_stations(network = "IN__ASOS")
```

    ## # A tibble: 145 × 22
    ##    index id    synop name    country elevation network online plot_name modified
    ##    <int> <chr> <dbl> <chr>   <chr>       <dbl> <chr>   <lgl>  <chr>     <chr>   
    ##  1     0 VEAT  99999 Agarta… IN            16  IN__AS… TRUE   "AGARTAL… 2023-12…
    ##  2     1 VOAT     NA Agatti… IN            -2  IN__AS… TRUE   "Agatti"  2020-06…
    ##  3     2 VIAG  99999 Agra    IN           169  IN__AS… TRUE   "AGRA (I… 2023-12…
    ##  4     3 VAAH  99999 Ahmeda… IN            55  IN__AS… TRUE   "AHMADAB… 2023-12…
    ##  5     4 VELP     NA Aizwal  IN           428. IN__AS… TRUE   "Lengpui" 2020-06…
    ##  6     5 VIAH     NA Aligarh IN           182  IN__AS… TRUE   "Aligarh" 2026-07…
    ##  7     6 VIAL  99999 Allaha… IN            98  IN__AS… FALSE  "ALLAHAB… 2023-12…
    ##  8     7 VEAB     NA Allaha… IN           100  IN__AS… TRUE   "Allahab… 2023-01…
    ##  9     8 VIAR  99999 Amrits… IN           234  IN__AS… TRUE   "AMRITSA… 2023-12…
    ## 10     9 VOAR     NA Arkonam IN            80  IN__AS… TRUE   "Arkonam" 2024-05…
    ## # ℹ 135 more rows
    ## # ℹ 12 more variables: spri <int>, tzname <chr>, iemid <int>,
    ## #   archive_begin <chr>, metasite <lgl>, wigos <chr>, longitude <dbl>,
    ## #   latitude <dbl>, state <chr>, archive_end <chr>, lon <dbl>, lat <dbl>

## Get measures for one station

Possible variables are (copied from
[here](https://mesonet.agron.iastate.edu/request/download.phtml), see
also the [ASOS user
guide](http://www.nws.noaa.gov/asos/pdfs/aum-toc.pdf))

- station: three or four character site identifier

- valid: timestamp of the observation (UTC)

- tmpf: Air Temperature in Fahrenheit, typically @ 2 meters

- dwpf: Dew Point Temperature in Fahrenheit, typically @ 2 meters

- relh: Relative Humidity in %

- drct: Wind Direction in degrees from north

- sknt: Wind Speed in knots

- p01i: One hour precipitation for the period from the observation time
  to the time of the previous hourly precipitation reset. This varies
  slightly by site. Values are in inches. This value may or may not
  contain frozen precipitation melted by some device on the sensor or
  estimated by some other means. Unfortunately, we do not know of an
  authoritative database denoting which station has which sensor.

- alti: Pressure altimeter in inches

- mslp: Sea Level Pressure in millibar

- vsby: Visibility in miles

- gust: Wind Gust in knots

- skyc1: Sky Level 1 Coverage

- skyc2: Sky Level 2 Coverage

- skyc3: Sky Level 3 Coverage

- skyc4: Sky Level 4 Coverage

- skyl1: Sky Level 1 Altitude in feet

- skyl2: Sky Level 2 Altitude in feet

- skyl3: Sky Level 3 Altitude in feet

- skyl4: Sky Level 4 Altitude in feet

- presentwx: Present Weather Codes (space seperated), see e.g. [this
  manual](http://www.ofcm.gov/fmh-1/pdf/H-CH8.pdf) for further
  explanations.

- feel: Apparent Temperature (Wind Chill or Heat Index) in degF

- ice_accretion_1hr: Ice Accretion over 1 Hour in inch

- ice_accretion_3hr: Ice Accretion over 3 Hour in inch

- ice_accretion_6hr: Ice Accretion over 6 Hour in inch

- relh: Relative Humidity in %

- metar: unprocessed reported observation in METAR format

- peak_wind_gust: Wind gust in knots from the METAR PK WND remark, this
  value may be different than the value found in the gust field. The
  gust field is derived from the standard METAR wind report.

- peak_wind_drct: The wind direction in degrees North denoted in the
  METAR PK WND remark.

- peak_wind_time: The timestamp of the PK WND value in the same timezone
  as the valid field and controlled by the tz parameter.

``` r

measures <- riem_measures(station = "VOHY", date_start = "2000-01-01", date_end = "2016-04-22")
```

    ## Warning in scan(file = file, what = what, sep = sep, quote = quote, dec = dec,
    ## : EOF within quoted string

``` r

head(measures)
```

    ## # A tibble: 6 × 30
    ##   station valid                tmpf  dwpf  relh  drct  sknt  p01i  alti  mslp
    ##   <chr>   <dttm>              <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 VOHY    2000-01-01 00:00:00  61.5  57.4  86.3     0     0    NA  29.9 1014.
    ## 2 VOHY    2000-01-01 01:40:00  64.4  60.8  88.1     0     0    NA  30.0   NA 
    ## 3 VOHY    2000-01-01 02:40:00  69.8  60.8  73.1   140     5    NA  30.1   NA 
    ## 4 VOHY    2000-01-01 03:00:00  68    61.7  80.3   140     4    NA  30.0 1016.
    ## 5 VOHY    2000-01-01 03:40:00  71.6  62.6  73.3   140     5    NA  30.1   NA 
    ## 6 VOHY    2000-01-01 05:40:00  75.2  55.4  50.2    90     6    NA  30     NA 
    ## # ℹ 20 more variables: vsby <dbl>, gust <dbl>, skyc1 <chr>, skyc2 <chr>,
    ## #   skyc3 <chr>, skyc4 <chr>, skyl1 <dbl>, skyl2 <dbl>, skyl3 <dbl>,
    ## #   skyl4 <dbl>, wxcodes <chr>, ice_accretion_1hr <lgl>,
    ## #   ice_accretion_3hr <lgl>, ice_accretion_6hr <lgl>, peak_wind_gust <lgl>,
    ## #   peak_wind_drct <lgl>, peak_wind_time <lgl>, feel <dbl>, metar <chr>,
    ## #   snowdepth <lgl>

For conversion of wind speed or temperature into other units, see [this
package](https://github.com/geanders/weathermetrics/).
