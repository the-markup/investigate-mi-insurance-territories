# 01_demographics

This directory contains notebooks producing demographic and geographic data for use in our analysis. 

# Inputs
Here is an overview of the data stored in the inputs directory:
```
01_demographics/inputs
├── census_data
├── column_mappings
├── crosswalk
│   ├── nhgis_bg2020_bg2010_26.zip
│   └── nhgis_bg2020_tr2010_26.zip
└── tiger_files
```

The sources for the data sets are:
- data.census.gov
- [National Historical Geographic Information System](https://www.nhgis.org/geographic-crosswalks#availability)
- https://www2.census.gov/geo/tiger/TIGER2020/
- https://www2.census.gov/geo/tiger/TIGER2010/

# Outputs

This directory contains files with the demographic data for different geographies in a CSV and GeoJSON format generated in the Jupyter notebooks. 

# Notebooks

## 00-demographic-data.ipynb

This notebook takes census data and the manually produced column mappings to create filtered and cleaned data sets to join with the territory tables for analysis.

## 01a-crosswalk-bg-tract.ipynb

This notebook takes 2022 American Community Survey (ACS) block group data and interpolates the population counts from 2020 block groups to 2010 tracts.

## 01b-crosswalk-bg-bg.ipynb

This notebook takes 2022 American Community Survey (ACS) block group data and interpolates the population counts from 2020 block groups to 2010 block groups.