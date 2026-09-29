# Changelog

## riem (development version)

## riem 1.0.0

CRAN release: 2025-01-31

- Breaking change: `date_start` and `station` no longer have default
  values.

- New arguments `data`, `latlon`, `report_type`, `elev`
  ([\#48](https://github.com/ropensci/riem/issues/48),
  [@JElchison](https://github.com/JElchison)).

- Breaking change: `latlon` default to `FALSE`: you need to explicitly
  set it to `TRUE` for the latitude and longitude of the station to be
  included in the output.

## riem 0.3.2

CRAN release: 2024-07-26

- Remove last usage of vcr as the choice was made to use httptest2
  instead.

## riem 0.3.1

CRAN release: 2024-04-04

- set tz=UTC on request to ensure tz result
  ([\#43](https://github.com/ropensci/riem/issues/43),
  [@akrherz](https://github.com/akrherz))

- Fixes timestamp parsing bug in riem_measures() caused by a lubridate
  1.9.0 bug ([\#40](https://github.com/ropensci/riem/issues/40),
  [@BenoitFayolle](https://github.com/BenoitFayolle))

## riem 0.3.0

CRAN release: 2022-02-08

- Switches to httr2 and httptest2 under the hood.
- Improves error messages.

## riem 0.2.0

CRAN release: 2021-12-17

- Switches to newer IEM metadata web services
  ([\#35](https://github.com/ropensci/riem/issues/35),
  [@akrherz](https://github.com/akrherz))

## riem 0.1.1

CRAN release: 2016-09-10

- Eliminates a few dependencies (dplyr, lazyeval, readr) to make
  installation easier.

- Now the default end date for `riem_measures` is the current date as
  given by [`Sys.Date()`](https://rdrr.io/r/base/Sys.time.html).

## riem 0.1.0

CRAN release: 2016-05-28

- Added a `NEWS.md` file to track changes to the package.
