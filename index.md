# indiacensus

An R package for accessing digitised Census of India data from 1901 to
2011.

## Installation

``` r
devtools::install_github("saketc/indiacensus")
```

## Quickstart

``` r
library(indiacensus)

# Get state-level population for 2011
get_census(2011, "state")

# Get district population for Maharashtra in 1971
get_census(1971, "district", state = "Maharashtra")

# Get data with geographic boundaries for mapping
get_census(1971, "district", state = "MH", geometry = TRUE)

# Browse available variables
list_census_variables()

# Search for specific variables
search_census_variables("literacy")

# See what data is available for each year
list_census_geographies()
```

## Examples

``` r
# State populations over time (1901-2011)
pop <- get_census(2011, "state")

library(ggplot2)

# Get 1971 district data for Maharashtra with boundaries
mh <- get_census(1971, "district", state = "Maharashtra", geometry = TRUE)

# Create a choropleth map
ggplot(mh) +
  geom_sf(aes(fill = population)) +
  scale_fill_viridis_c() +
  theme_minimal() +
  labs(title = "Population by District - Maharashtra 1971")

# What years and geographies are available?
list_census_geographies()

# What variables exist?
list_census_variables()

# Variables available for 1981
list_census_variables(year = 1981)

# Find worker-related variables
search_census_variables("worker")
```

## Data Source

Most datasets in this package are derived from:

> Jolad, Shivakumar and Singh, Madhav (2026). “Indian Census Data
> Collection, 1901-2026: Digitised Subnational Population and
> Administrative Datasets.” Harvard Dataverse.
> <https://doi.org/10.7910/DVN/ON8CP8>

The 2011 mother tongue data is derived from the census of india official
website.

## License

MIT
