# Assignment 03: Libraries

| ![lib](https://bpldcassets.blob.core.windows.net/derivatives/images/commonwealth:c821gx86v/image_access_800.jpg) |
| :----------------------------: |
| *[Boston Public Library, June 1928](https://www.digitalcommonwealth.org/search/commonwealth:c821gx85k)* |

## What you should submit

A **20"x30" poster** in `jpeg` format created using Microsoft Publisher that includes the following:
- 1 heat map showing 2019 public libraries in the U.S.
- 3 "small multiple" choropleth maps, each including a title and legend:
  - 1 bivariate map showing public libraries and U.S. county population
  - 1 bivariate map showing public libraries and one variable of your choice from the social vulnerability index (SVI) dataset
  - 1 graduated color map showing the increase/decrease by U.S. county of public libraries between 2019 and 2021
- 2 sections of written text:
  - 50-100 words summarizing your methods
  - 50-100 words describing your observations

## Introduction and context

Libraries are a public good that we encounter in one way or another almost every day, but what is their geography? What kinds of spatial relationships do libraries have to other demographic variables like population or income, and how can we use spatial reasoning visualize those relationships?

In this assignment, you'll answer this question using two datasets:

1. Every year since 2006, the [Institute of Museum and Library Services](https://www.imls.gov/) (IMLS) collects a [**public libraries survey**](https://www.imls.gov/research-evaluation/data-collection/public-libraries-survey) which attempts to "provide information that policymakers and practitioners can use to make informed decisions about the support and strategic management of libraries." They have made this data available for free to the public. In addition to containing off-the-shelf spatial data in the form of latitudes and longitudes, this spreadsheet also contains tons of other useful information.
2. The Center for Disease Control (CDC), in collaboration with a bunch of other federal agencies, has created a **[social vulnerability index (SVI)](https://www.atsdr.cdc.gov/placeandhealth/svi/documentation/SVI_documentation_2020.html)** in order "to help public health officials and emergency response planners identify and map the communities that will most likely need support before, during, and after a hazardous event." The index breaks down into [four main categories](https://www.atsdr.cdc.gov/placeandhealth/svi/documentation/pdf/SVI2020Documentation_08.05.22.pdf): *socioeconomic status*, *household characteristics*, *racial & ethnic minority status*, and *housing & transportation type*. Each of these categories contains 4-5 demographic variables.

Between the IMLS and CDC data, there are tons of data points we could dig into here. When you need to communicate lots of information 

Like last week's lab, this assignment does not dive deeply into spatial analysis (e.g., geostatistics, regression). Rather, the goal is for you to continue sharpening established skills—such as field calculation, attribute/location querying, and thoughtful symbolization—while dipping your toes into the not insignificant challenge of designing a small poster.

**Follow the instructions below**

## Download the data

Data for this assignment is located in 3 places:
1. IMLS
2. [CDC SVI data](https://www.atsdr.cdc.gov/placeandhealth/svi/data_documentation_download.html)—be sure to download 2020

3. Download data from Canvas
4. Create + open ArcGIS Pro project
5. Set a suitable projection for contiguous 48 United States
6. Load 2019 data into ArcGIS Pro project using **XY Table to Point**
7. Download Census counties data and add to project
8. **Summarize Within**
   1. Input polygon = `counties_projected`
   2. Input summary features = `libraries_fy19`
   3. Output feature class = `lib_19_smrz`
   4. Check "Keep all input features"
   5. Summary fields
      1. Field = `CNTYPOP`, Statistic = `Mean`
   6. Check "Add shape summary attributes"
9. 