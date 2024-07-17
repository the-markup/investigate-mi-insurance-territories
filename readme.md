# How We Investigated Michigan Insurance Territories

This repository contains data and code to reproduce the findings featured in our story "[Michigan’s 'Fair and Reasonable' Reforms Allowed Car Insurers to Charge More in Black Neighborhoods](https://mrkup.org/l5W6g)."

Our methodology is described in "[How We Investigated Car Insurance Loopholes in Michigan](https://mrkup.org/wr1HV)."

We extracted the relevant territory tables from documents submitted to the Office of Insurance Rates and Forms of the Michigan Department of Insurance and Financial Services.

The code in this repository was used to produce and analyze the data for our investigation. The process is described in detail below for replication and inspection.

# Notebooks

This is a summary of the notebooks in the insurer directories.

## 00(a)-extract-auto-table.ipynb

This notebook extracts territory tables from PDF of insurer filing to produce tabulated data files for analysis.

## 00b-geography-experiment.ipynb

This notebook exists for State Farm and Allstate, the two insurers using custom-made gridded territory maps. It is used to run experiments to determine the optimal geography match for our analysis.

## 01-analysis.ipynb

This notebook replicates and fact checks all the data figures and findings used in publication.

# Data

The data produced for the analysis is stored in each insurer's `outputs/` directory as `INSURER_auto_clean.csv`. For example, `02_allstate/outputs/allstate_auto_clean.csv` for Allstate.

Those files contain the following columns:

| column                           | description                                                                                                                                                                                         |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `geo_id`                         | The census geographic identifier that matches onto the territory. Read more about how this value is selected in the [Show Your Work](https://mrkup.org/wr1HV).                                      |
| `geo_name`                       | The census geographic area name that matches onto the territory. Read more about how this value is selected in the [Show Your Work](https://mrkup.org/wr1HV).                                       |
| `total_pop`                      | The total population in the census geography.                                                                                                                                                       |
| `white_pct`                      | The percentage of census geography's population that is non-Hispanic/non-Latino White.                                                                                                              |
| `black_pct`                      | The percentage of census geography's population that is non-Hispanic/non-Latino Black.                                                                                                              |
| `white_tot`                      | The percentage of census geography's population count that is non-Hispanic/non-Latino White.                                                                                                        |
| `black_tot`                      | The census geography's population count that is non-Hispanic/non-Latino Black.                                                                                                                      |
| `generic_location_based_premium` | The location-fixed or location-adjusted base rate. Read more about this value in the [Show Your Work](https://mrkup.org/wr1HV).                                                                     |
| `location_effect`                | The location-fixed or location-adjusted base rate indexed to the insurer's state median. Read more about this value in the [Show Your Work](https://mrkup.org/wr1HV).                               |
| `geometry`                       | The insurance territory's point or polygon geometry.                                                                                                                                                |
| `median_income`                  | The median household income for the census geography.                                                                                                                                               |
| `density`                        | The geography's total population divided by total area sourced from TIGER shape files from the U.S. Census Bureau.                                                                                  |
| `is_along_8_mile`                | Boolean representing whether a gridded territory point is within a 1 mile buffer of 8 mile road. This value is only available for State Farm and Allstate cleaned data files.                       |
| `is_in_detroit`                  | This a boolean representing whether a territory is within Detroit.                                                                                                                                  |
| `is_north_8_mile`                | This is a boolean representing whether a gridded territory point is within a 1 mile buffer north of 8 mile road. This value is only available for State Farm and Allstate cleaned data files.       |
| `is_south_8_mile`                | This is a boolean representing whether a gridded territory point is within a 1 mile buffer south of 8 mile road. This value is only available for State Farm and Allstate cleaned data files.       |
| `bg_black_pct`                   | This is the percentage of the census block group geography's population that is non-Hispanic/non-Latino Black. This value is only available for State Farm cleaned data file.                       |
| `bg_black_tot`                   | The census geography's population count that is non-Hispanic/non-Latino Black. This value is only available for State Farm cleaned data file.                                                       |
| `bg_geo_id`                      | The Census block group geographic identifier that matches onto the territory. This value is only available for State Farm cleaned data file.                                                        |
| `bg_median_income`               | The median household income for the census block group geography. This value is only available for State Farm cleaned data file.                                                                    |
| `bg_tot_pop`                     | The total population count in census block group. This value is only available for State Farm cleaned data file.                                                                                    |
| `bg_white_pct`                   | The percentage of population that is non-Hispanic/non-Latino White in the block group. This value is only available for State Farm cleaned data file.                                               |
| `bg_white_tot`                   | The population count that is non-Hispanic/non-Latino White in the census block group geography. This value is only available for State Farm cleaned data file.                                      |
| `latitude`                       | This value is the gridded territory's latitude. This value is only available in the Allstate cleaned data file.                                                                                     |
| `longitude`                      | This value is the gridded territory's longitude. This value is only available in the Allstate cleaned data file.                                                                                    |
| `is_zcta_border`                 | This boolean representing whether Allstate gridded territory point has an adjacent territory in a different ZCTA.                                                                                   |
| `loc_rate_div_min_nn`            | This is the Allstate territory's generic_location_based_premium divided by the lowest neighboring `generic_location_based_premium`. This value is only available in the Allstate cleaned data file. |
| `nn_min_val`                     | This is the the lowest neighboring `generic_location_based_premium`. This value is only available in the Allstate cleaned data file.                                                                |

# Reproducibility

All notebooks committed have been run and display outputs.

We ran our code in a JupyterLab development environment running in a Docker container. The Docker image is derived from the [Docker Stacks `datascience-notebook` image](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html#jupyter-datascience-notebook). 

The dependencies include packages available in the `datascience-notebook` image plus `geopandas` and `tabula-py`. If needed, [install Docker Engine](https://docs.docker.com/engine/install/) to run the container.

Create and start the container by running this command in a terminal:

> docker compose up 

Copy and paste the output web address into an internet browser to open the JupyterLab development environment.
