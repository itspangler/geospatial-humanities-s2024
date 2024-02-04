# Activity 02: Historic population in Africa, 1850-1950 <!-- omit in toc -->
*Understanding quantitative cartography and interpolated sources with historic population data*

# Table of contents <!-- omit in toc -->

- [Introduction and context](#introduction-and-context)
- [Set up your workspace](#set-up-your-workspace)
- [Download the activity data](#download-the-activity-data)
  - [Tabular data](#tabular-data)
  - [Feature data](#feature-data)
  - [Load the data](#load-the-data)
- [Making the data work for you](#making-the-data-work-for-you)
  - [Dissolving by field](#dissolving-by-field)
  - [Deleting spurious geometries with field calculator](#deleting-spurious-geometries-with-field-calculator)
- [Joining your data](#joining-your-data)
  - [The table join](#the-table-join)
  - [Building a common field](#building-a-common-field)
- [Classification](#classification)
- [Activity deliverables](#activity-deliverables)

# What you should submit <!-- omit in toc -->

Before **6:30pm on Tuesday, 2/20**, you should submit to Canvas:
* A document in `pdf` or `docx` format, answering all the questions that are tagged with ![q], and which are summarized in the [activity deliverables](#activity-deliverables) section
* A map in `png` format, exported at 300 DPI, as directed at the end of the lab

# Introduction and context

This activity will walk you through techniques and best practices associated with representing quantitative and qualitative geographical data using ArcGIS Pro. You'll use a pre-processed dataset that interpolates population data for African countries to visualize population change over the course of a century across the entire African continent.

Major learning objectives include:
* best practices in cartographic representation
* distinguishing between kinds of maps
* understanding visual hierarchy
* assessing map variables
* basic color theory
* table joins

# Set up your workspace

At this point, you should be getting pretty good at starting a new project in ArcGIS Pro. Follow these instructions to set up your workspace:

1. First, I recommend creating a directory in your `H: drive` for `week04`, and inside that directory, make two folders for `data` and `workspace`. When I do this, it resembles:

        ├─ gisusers$ (H:)/   
          ├─ week03/   
            ├─ lab02_slave-trade/
              ├─ workspace/
              ├─ submission/

    You should pick a directory structure that makes sense for how you work, but the key thing to bear in mind is to pick a structure that is as *futureproof as possible.*

    To give a concrete example, I like to store my original datasets in a separate `data` folder in case I accidentally corrupt my data and need to get a fresh copy.
2. Open **ArcGIS Pro**.
3. Sign in with your ArcGIS organization URL.
4. Start a new project by clicking **Map**.
5. Name your project something like `activity02_africaHistoricPop`.
6. Save the new project in your `workspace` folder, leaving the "Create a new folder for this project" box checked.

You should now be looking at a fresh ArcGIS Pro project, with the two default layers of a world hillshade and world topo map.

# Download the activity data

In this activity, you'll be working with two kinds of geographic data in this activity: **tabular data** and **feature data**.

Tabular data refers to data that is saved in table or spreadsheet format. Commonly you'll encounter this as an `xls` or `csv` file. Tabular data is "geographic" when it contains geographic indicators – such as latitude and longitude or an address – but that doesn't mean it's *spatial* data. In order to display it in a GIS like ArcGIS Pro, there are further steps we need to take. Right now it's only *describing* these geographies.

Feature data refers to data that is encoded in a spatial format. Common spatial formats include the shapefile (`shp`), GeoJSON (`geojoson`), and geodatabase (`gdb`). All of these formats contain structured spatial data that can be read inherently by many geographic information systems without any further processing. When you load spatial data into ArcGIS Pro, it is automatically recognized and can be instantly plotted as features on the map; hence, *feature* data.

> ![imp]
>
> Almost always, feature data contains some kind of tabular data as well, usually in the form of an **attribute table** like the kind you explored extensively in Lab 02.

## Tabular data

Download the tabular data containing estimated populations in African countries between 1850 and 1950 from Canvas.

It's a slightly processed version of [this dataset](https://dataverse.harvard.edu/dataset.xhtml?persistentId=hdl:1902.1/15281&studyListingIndex=3_bbe301ac817a8f240616b94fcc83). The author has written (Manning 2010:246) about why he composed this dataset:

> The findings... draw attention to the widespread assumptions of past observers that African populations were relatively small and that they were growing rapidly—in both colonial and precolonial eras. These pervasive assumptions were more than demographic estimates: they emerged out of ideologies that treated African societies as technically backward, politically immature, and socially elemental. Such views of African societies enabled observers to make aggregate generalizations without exploring the details of African social interaction.

When you encounter a new dataset, your first questions should always be: why does this exist? Where did the data come from? How was it computed? If you want, you can read more about how this dataset was actually created in Appendix A of the original `xls` spreadsheet: <https://doi.org/10.7910/DVN/ZP3PP1>

Take a moment to open this dataset in Microsoft Excel. You should see something like:

![data](images/image002.png)

## Feature data

There are lots of places where you could download spatial data of African countries. For this activity, we'll use [Stanford University's EarthWorks portal](https://earthworks.stanford.edu/), a massive discovery tool for geospatial data. (Alternatives include the [Tufts GeoData portal](https://geodata.tufts.edu/), [Harvard's Dataverse](https://dataverse.harvard.edu/), [Princeton's Maps & Geospatial Data Portal](https://maps.princeton.edu/?utf8=%E2%9C%93&search_field=all_fields&q=&featured=geospatial), and the [Big Ten Academic Alliance's Geoportal.](https://geo.btaa.org/))
1. Go to [EarthWorks](https://earthworks.stanford.edu/)
2. Search for `africa country boundaries`
3. Click "Detailed World Polygons (LSIB), Africa, 2013" – it should be the first hit
4. Export it as a `shapefile`

    ![export](images/image001.png)
5. It will download as a `zip` file. Extract it and move the contents into your `data` folder
6. Delete any spurious folders before you load the data into ArcGIS

## Load the data

Go ahead and bring the feature data (countries) into ArcGIS Pro, either by:

1. **Map** tab ➡️ "Add Data" 
2. **Catalog** pane ➡️ navigate to your `data` folder (or wherever you saved the data) ➡️ drag and drop from **Catalog** into map/data frame

![add](images/image003.png)

Then, add the tabular data (spreadsheet) using the same method. Once you're done, you should see both layers displayed in your **Contents** pane, which will have a new category for "standalone tables":

![standalone](images/image004.png)

Open the `africa_pop_est_1850-1950_cleaned` file by **right-click** ➡️ "Open" (or `ctrl`+`T`). Some general observations:
* for now, `gisname` field is supposed to be empty
* `ST_region` means "Slave trade region"
* `pop_` columns show decennial population estimates, and they don't seem to follow changes in historical geographies; rather, they're all mapped to modern territorial boundaries

Although *we* understand intuitively how this "standalone table" should be mapped – e.g., we want to associate the values in the `pop_` columns with geographic features on the map, based on the country name – that isn't enough for ArcGIS Pro. **A country name is not inherently spatial data: it's just geographic information.**

Turning geographic information into spatial data is one of the most fundamental and powerful aspects of GIS software. Typically, we call the process of connecting tabular data with spatial data a **table join** – but before we get to that workflow, let's take a moment to explore our spatial data as well.

# Making the data work for you

Even the tidiest datasets will often need further pruning, massaging, and TLC. Our two datasets for this activity are no exception.

Take the countries shapefile, for instance, currently displayed as `Africa` in your contents pane. Now might be a good time to rename the layer to something like "African Countries," which I'm going to do.

Open the `African Countries` layer's **attribute table**.

Hachi machi! Why, pray tell, are there nearly 5,000 records in this shapefile of African countries?

![fivek](images/image005.png)

Go ahead and zoom into one of those features by **double-clicking** on the table row number on the attribute table's left-hand side...

![zoom](images/image006.png)

... and you'll probably find yourself looking at a tiny polygon off the coast, like this:

![coast](images/image007.png)

In addition to being pretty [heavily generalized](https://www.axismaps.com/guide/scale-and-generalization), as the jagged edges along the coast suggest, this shapefile appears to have encoded *every little island off the coast as a separate record*.

There's nothing wrong with that per se, but for our purposes today, that's *way* too detailed: ideally, we just want a shapefile that contains one record for every country in the African continent.

Two methods come to mind for making this data work for you.

## Dissolving by field

ArcGIS Pro offers a wide range of **geoprocessing** tools for data management. A classic is **Dissolve**.

**Dissolve** aggregates features based on specific attributes. For example, the abstract illustration below consolidates features of like color into a single geometry:

| ![dissolve](images/image008.png) |
| :--------------------: |
| *Dissolve tool, from [Esri](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/dissolve.htm)* |

Let's make that abstract example more concrete by applying it to the `African Countries` layer.

1. Open the **Dissolve** tool by clicking into the **Analysis** pane ➡️ click **Tools**

    ![tools](images/image009.png)

2. Search for the **Dissolve** tool by typing "dissolve" into the search bar of the **geoprocessing pane** that opens. Click **Dissolve**.

    ![dissolve](./images/image010.png)

3. Set the tool's parameters like so...
   
   1. Input features =  `African Countries`
   2. Output feature class = `AfricanCountries_Dissolved` – save this to `africanHistoricalPopulation.gdb`
   3. Dissolve fields = `NAME`
   4. ![imp] Make sure you clear ![clear](images/image013.png) any records that might be selected. If you have any records selected, *the geoprocessing operation will only be performed on them.*
   
   ... and click **Run**.

4. Now you should have a new layer in your **contents** pane for `AfricanCountries_Dissolved`. Open its attribute table – you should now see only 70 records.

    ![seventy](images/image011.png)

5. Select one of the records and zoom into the coast until you find a few islands. Notice how *all* the geometries that shared a value in the `NAME` field have been consolidated even if they're not touching one another. This is called a **multipart feature** – or a single feature that contains noncontiguous elements and is represented in the attribute table as one record – and it's a common result of running the **Dissolve** tool: 

    | ![islands](images/image012.png) |
    | :-----------------------------: |
    | *The coast of Algeria as a multipart feature*  |

> ![q]
>
> 1. There are 54 countries in Africa and our dissolved layer has 70 – still more records than we would expect. Use the attribute table to figure out why that is, and write down an example of a feature that is inflating the feature count. Why does it seem like this feature exists? Do you think you need to keep it for this exercise?

## Deleting spurious geometries with field calculator

The **Dissolve** tool is a handy way to automate consolidating features, but sometimes it's important to get a little bit more precise. For example, let's say we didn't want to include all those little islands along the coast *at all* – can we just delete them?

Obviously, you wouldn't want to pan through the map, selecting and deleting all nearly 5,000 extra geometries by hand. To delete these features quickly, you'd want to:
1. compute their area using the **field calculator**
2. sort the attribute table by that new field
3. manually remove features you don't want

Let's try...

1. Close the attribute table for `AfricanCountries_Dissolved` and open the attribute table for your original shapefile, `African Countries`
2. Click the "Add" button in the header of the attribute table.
3. Fill out the fields so that
   1. Field Name = `area`
   2. Alias = `area`
   3. Data Type = `double`
   4. Number Format = `Numeric`
   
   And save it, either with the **Save** button in the **Fields** tab at the top of your screen or by **right-clicking** in row itself and choosing "Save" (as highlighted below).

   ![save](images/image014.png)

4. Back in the attribute table for `African Countries`, **right-click** the `area` ➡️ "Calculate Geometry". This will automatically open the **Calculate Geometry** geoprocessing tool. Set the parameters to:
   1. Input Features = `African Countries`
   2. Field = `area`, while Property = `Area (geodesic)`
   3. Area Unit = `Square kilometers`
   4. Coordinate System = `GCS_WGS_1984` (you can select this by clicking on the graticule ![grat](images/image015.png) icon next to the box)
5. Click **OK** and you should see the `area` field populate with a bunch of values. **Go ahead and sort those values in descending (highest to lowest) order** with **right-click** ➡️ "Sort Descending".

> ![q]
>
> 2. Scroll through the attribute table and examine the sorted data, double-clicking on record numbers to zoom into different features. Is there a break point after which it seems like you could delete most of the smaller features without erasing any actual countries? Where is that break point, and why did you choose it? Specify it with the record number and FID (e.g., "Record #90, FID `3500`.")

For the purposes of this activity, we'll proceed with the dissolved layer. Go ahead and remove the `African Countries` layer from your project and rename `AfricanCountries_Dissolved` to `African Countries`.

# Joining your data

## The table join

The table join is a crucial GIS workflow. Esri [describes it as such](https://pro.arcgis.com/en/pro-app/3.1/help/data/tables/joins-and-relates.htm):

> Through a common field, known as a key, you can associate records in one table with records in another table. For example, you can associate a table of parcel ownership information with the parcels layer, because they share a parcel identification field.
> 
> You can make these associations in several ways, including by joining or relating tables temporarily in your map or by creating relationship classes in your geodatabase that maintain more permanent associations. Joins can also be based on spatial location.

|                                                                                                                                          ![imp]                                                                                                                                           |
| :- |
| Joins only work if the common identifier is **exactly the same in both tables**: there can be **absolutely no differences** between the common field in either table, or else the data for that record won't be joined. For example, `Senegal` would not join to `SENEGAL` because the latter is all caps. For this reason, it's typically ideal to use a numerical key rather than a string (e.g., text-based) key.|

| ![joins](images/image016.png) |
| :---------------------------: |
| *A drawing showing how attributes (the numbers) and features (the shapes) are joined together. The dotted lines represent the "common field" that links the two data (by [Tess McCann](https://cartinal.leventhalmap.org/guides/making-sense-maps-data/session-2/part-4.html#how-do-features-and-attributes-get-together), 2021)*.|

This is precisely what we want to do with our data: we want to join the "standalone table" of population data to the `African Countries` layer.

So, the major question is, do we have such a common field in our two tables?

Well, we have information for country name in both tables, but is it actually *joinable* as as common ID?

1. Open both attribute tables, one for the `African Countries` layer and one for your standalone table `africa_pop_est_1850-1950_cleaned`
2. Click and drag one of those tables into the side-by-side view (an option for "pinning" the table in various locations should open up once you're begun to drag it), as shown in the gif below:

    ![sidebyside](images/image017.gif)

3. Sort the `NAME` field in the `African Countries` table in alphabetical order, from first to last (you can do this by double-clicking on the field name). Do the same with the `territory` field in the `africa_pop_est_1850-1950_cleaned` table.
4. Scroll through, comparing the two fields.

> ![q]
>
> 3. Why won't this work as a common field for our table join?

## Building a common field

It looks like we're going to have to make a common ID field on our own. Because we're working with historical data, this will require some extra considerations, but our goal is straightforward: We want to populate the `gisname` field in the `africa_pop_est_1850-1950_cleaned` tablae with values that conform exactly to the `NAME` field of the `African Countries` layer. To accomplish this, we will:
1. Use Microsoft Excel to copy values from the `territory` field into the `gisname` field
2. Read through the new `gisname` values and correct any spelling or nomenclature discrepancies

Let's get started...

1. First, open `africa_pop_est_1850-1950_cleaned` in Microsoft Excel. (You might need to right-click on the file and select "Open with"...)
2. Go back to ArcGIS Pro. Select all the records in your `Africa Countries` layer and click the **Copy** button in the header of the attribute table.

    ![copy](images/image018.png)

3. Paste the copied values somewhere in your Excel spreadsheet. Here's where I dumped mine:

    ![excel](images/image019.png)

    What we're going to do now is treat our Excel spreadsheet like a working document. We'll move a bunch of things around, with the goal of making that currently empty `gisname` field conform *exactly* to the `NAME` fields to which we want this data joined. By the time we're done, it will be fully joinable and **GIS friendly**.
4. Now, right-click on the header above the `NAME` field, and select "Copy". That field was in the `R` column for me, but it might be in a different column for you.

    ![copy](images/image020.png)

5. Once it's copied, right-click on your `territory` field – it should be the `A` column – and click "Insert copied cells." This will paste the copied column *to the left* of the existing data.

    ![pastecopied](images/image021.png)

    Now you should have a list of the *destination field* (e.g., the `NAME` field to which we want to join our spreadsheet data) right next to the *input field* (e.g., the `territory` field that we must conform to the `NAME` field before it's actually joinable).

    You can delete the leftover cells copied from ArcGIS Pro. Your screen should resemble:

    ![excel](images/image022.png)

6. Click into the `Q2` cell – it should be to the right of your data – and paste the following expression:

        =UPPER(B2)

    This expression will paste the value from the `B2` cell into the `Q2` cell, but capitalized.

7. **Copy** the `Q2` cell itself by right-clicking on the cell ➡️ "Copy" (or `ctrl`+`V`) and then **paste** the contents into cells `Q3:Q50` (using either right-click ➡️ "Paste" or `ctrl`+`V`), as shown in the GIF below:

    ![paste](images/image023.gif)

8. Now that you have all your values capitalized, it's time to paste them where they belong. Copy the new column (cells `Q2:Q50` for me) and then select the pasting destination: the `gisname` field, column `C`, cells `2:50`. Again, the GIF below demonstrates:

# Classification

# Activity deliverables

<!-------------------------------------[ Links ]
---------------------------------------->

[l]: #

<!---------------------------------[ Buttons ]--------------------------------->

[imp]: https://img.shields.io/badge/IMPORTANT!-red?style=plastic
[q]: https://img.shields.io/badge/Question-blue?style=plastic
[qs]: https://img.shields.io/badge/All_Questions-blue?style=plastic