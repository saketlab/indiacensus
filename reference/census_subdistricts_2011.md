# Subdistrict Directory with 2011 Census Data

Administrative subdistrict (tehsil/taluka) level data linked to 2011
Census population figures. Based on 2011 administrative boundaries.

## Usage

``` r
census_subdistricts_2011
```

## Format

A tibble with 7,074 rows and 15 columns:

- year:

  Census year for population data (2011)

- geography:

  Geographic level ("subdistrict")

- state:

  Name of the state

- state_name_harmonized:

  Harmonized state name for joining across datasets

- district:

  Name of the district

- subdistrict:

  Name of the subdistrict (tehsil/taluka)

- population:

  Total population

- males:

  Male population

- females:

  Female population

- households:

  Number of households

- inhabited_villages:

  Number of inhabited villages

- uninhabited_villages:

  Number of uninhabited villages

- towns:

  Number of towns

- area_km2:

  Area in square kilometers

- density:

  Population density per square kilometer

## Source

Jolad, Shivakumar and Singh, Madhav (2026). "Indian Census Data
Collection, 1901-2026: Digitised Subnational Population and
Administrative Datasets." Harvard Dataverse.
[doi:10.7910/DVN/ON8CP8](https://doi.org/10.7910/DVN/ON8CP8) .
