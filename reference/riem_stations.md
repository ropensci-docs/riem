# Get stations of an ASOS network

Get stations of an ASOS network

## Usage

``` r
riem_stations(network)
```

## Arguments

- network:

  A single network code, see riem_networks() for finding the code
  corresponding to a name.

## Value

a data.frame (tibble tibble) with the id, name, longitude (lon) and
latitude (lat) of each station in the network.

## Details

You can see a map of stations in a network at
<https://mesonet.agron.iastate.edu/request/download.phtml>.

## Examples

``` r
if (FALSE) { # \dontrun{
riem_stations(network = "IN__ASOS")
} # }
```
