# Population Maps

``` r
library(indiacensus)
library(dplyr)
#> 
#> Attaching package: 'dplyr'
#> The following objects are masked from 'package:stats':
#> 
#>     filter, lag
#> The following objects are masked from 'package:base':
#> 
#>     intersect, setdiff, setequal, union
library(ggplot2)
```

## State Population Over Time

``` r
years <- seq(1901, 2011, by = 10)

pop_geo <- lapply(years, function(y) {
  census_population_time_series |>
    filter(geography == "state", year == y) |>
    attach_geometry(year = y, geography = "state")
}) |> bind_rows()
#> Warning: Exact boundaries for 1901 not available.
#> ℹ Using 1941 boundaries instead.
#> Warning: Exact boundaries for 1911 not available.
#> ℹ Using 1941 boundaries instead.
#> Warning: Exact boundaries for 1921 not available.
#> ℹ Using 1941 boundaries instead.
#> Warning: Exact boundaries for 1931 not available.
#> ℹ Using 1941 boundaries instead.
```

``` r
ggplot(pop_geo) +
  geom_sf(aes(fill = population / 1e6), color = "white", linewidth = 0.1) +
  scale_fill_gradientn(colors = get_palette("viridis"), name = "Million") +
  facet_wrap(~year, nrow = 2) +
  theme_void() +
  theme(strip.text = element_text(face = "bold"), legend.position = "bottom")
```

![](population-maps_files/figure-html/facet-map-1.png)

## Decadal Growth Rate

``` r
pop <- census_population_time_series |>
  filter(geography == "state") |>
  arrange(state_name, year)

growth <- pop |>
  group_by(state_name) |>
  mutate(growth_rate = 100 * (population - lag(population)) / lag(population)) |>
  filter(!is.na(growth_rate)) |>
  ungroup()

growth_geo <- lapply(unique(growth$year), function(y) {
  growth |>
    filter(year == y) |>
    attach_geometry(year = y, geography = "state")
}) |> bind_rows()
#> Warning: Exact boundaries for 1911 not available.
#> ℹ Using 1941 boundaries instead.
#> Warning: Exact boundaries for 1921 not available.
#> ℹ Using 1941 boundaries instead.
#> Warning: Exact boundaries for 1931 not available.
#> ℹ Using 1941 boundaries instead.
#> Warning: Exact boundaries for 1910 not available.
#> ℹ Using 1941 boundaries instead.
#> Warning: Exact boundaries for 1940 not available.
#> ℹ Using 1941 boundaries instead.
#> Warning: Exact boundaries for 1950 not available.
#> ℹ Using 1951 boundaries instead.
#> Warning: Exact boundaries for 1962 not available.
#> ℹ Using 1961 boundaries instead.
#> Warning: Exact boundaries for 1960 not available.
#> ℹ Using 1961 boundaries instead.
#> Warning: Exact boundaries for 2021 not available.
#> ℹ Using 2011 boundaries instead.
#> Warning: Exact boundaries for 1948 not available.
#> ℹ Using 1951 boundaries instead.
```

``` r
ggplot(growth_geo) +
  geom_sf(aes(fill = growth_rate), color = "white", linewidth = 0.1) +
  scale_fill_gradientn(colors = get_palette("blue_red"), name = "Growth %", limits = c(-10, 50)) +
  facet_wrap(~year, nrow = 2) +
  theme_void() +
  theme(strip.text = element_text(face = "bold"), legend.position = "bottom")
```

![](population-maps_files/figure-html/growth-map-1.png)
