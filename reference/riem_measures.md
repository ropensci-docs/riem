# Get weather data from one station

Get weather data from one station

## Usage

``` r
riem_measures(
  station,
  date_start,
  ...,
  date_end = as.character(Sys.Date()),
  data = "all",
  elev = FALSE,
  latlon = FALSE,
  report_type = NULL
)
```

## Arguments

- station:

  station ID, see riem_stations()

- date_start:

  date of start of the desired data, e.g. "2016-01-01"

- ...:

  These dots are for future extensions and must be empty.

- date_end:

  date of end of the desired data, e.g. "2016-04-22". Default value is
  today. \# nolint: line_length_linter

- data:

  A vector of strings, representing the data columns to return. The
  available options are: all, tmpf, dwpf, relh, drct, sknt, p01i, alti,
  mslp, vsby, gust, skyc1, skyc2, skyc3, skyc4, skyl1, skyl2, skyl3,
  skyl4, wxcodes, ice_accretion_1hr, ice_accretion_3hr,
  ice_accretion_6hr, peak_wind_gust, peak_wind_drct, peak_wind_time,
  feel, metar, snowdepth \# nolint: line_length_linter Default value is
  \`all\`.

- elev:

  If TRUE, the elevation (m) of the station will be included in the
  output, in an \`elevation\` column. \# nolint: line_length_linter
  Default value is \`FALSE\`.

- latlon:

  Default to \`FALSE\` since riem 1.0.0. If \`TRUE\`, the latitude and
  longitude of the station will be included in the output, in \`lat\`
  and \`lon\` columns. \# nolint: line_length_linter Default value is
  \`FALSE\`.

- report_type:

  A vector of strings, representing report types to query. The available
  options are \`"hfmetar"\`, \`"routine"\`, \`"specials"\`. Default
  value is \`c("routine", "specials")\`.

## Value

a data.frame (tibble tibble) with measures, the number of columns can
vary from station to station, but possible variables are

- station: three or four character site identifier

- valid: timestamp of the observation (UTC)

- tmpf: Air Temperature in Fahrenheit, typically @ 2 meters

- dwpf: Dew Point Temperature in Fahrenheit, typically @ 2 meters

- relh: Relative Humidity in

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

- presentwx: Present Weather Codes (space seperated), see e.g. Chapter 8
  of \[this
  manual\](https://www.ofcm.gov/publications/fmh/FMH1/FMH1.pdf) for
  further explanations.# nolint: line_length_linter

- feel: Apparent Temperature (Wind Chill or Heat Index) in degF

- ice_accretion_1hr: Ice Accretion over 1 Hour in inch

- ice_accretion_3hr: Ice Accretion over 3 Hour in inch

- ice_accretion_6hr: Ice Accretion over 6 Hour in inch

- relh: Relative Humidity in

- metar: unprocessed reported observation in METAR format

- peak_wind_gust: Wind gust in knots from the METAR PK WND remark, this
  value may be different than the value found in the gust field. The
  gust field is derived from the standard METAR wind report.

- peak_wind_drct: The wind direction in degrees North denoted in the
  METAR PK WND remark.

- peak_wind_time: The timestamp of the PK WND value in the same timezone
  as the valid field and controlled by the tz parameter.

## Details

The data is queried through
<https://mesonet.agron.iastate.edu/request/download.phtml>.# nolint:
line_length_linter

## Examples

``` r
if (FALSE) { # \dontrun{
riem_measures(
  station = "VOHY",
  date_start = "2016-01-01",
  date_end = "2016-04-22"
)
} # }
```
