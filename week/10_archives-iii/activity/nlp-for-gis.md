# Activity 05: NLP for GIS <!-- omit in toc -->

| ![engrossed](https://iiif.digitalcommonwealth.org/iiif/2/commonwealth:02872091q/full/1200,/0/default.jpg) |
| :------------------------------------------------------------------------------------------------------------: |
| *"Three children engrossed by books," from the [Boston Public Library Arts Department](https://www.digitalcommonwealth.org/search/commonwealth:02872090f)* |

## Table of contents <!-- omit in toc -->

- [Introduction and context](#introduction-and-context)
- [Set up your workspace](#set-up-your-workspace)
  - [Directory stuff](#directory-stuff)
  - [Open QGIS!](#open-qgis)
- [Getting the data ready](#getting-the-data-ready)
  - [Download the data](#download-the-data)
  - [Pre-processing](#pre-processing)
- [Geocoding children's book publishers](#geocoding-childrens-book-publishers)
  - [OpenStreetMap, Nominatim, and MMQGIS](#openstreetmap-nominatim-and-mmqgis)
  - [Running the geocoder](#running-the-geocoder)
- [Natural language processing "by hand"](#natural-language-processing-by-hand)
- [Symbolize your data](#symbolize-your-data)
- [Activity deliverables](#activity-deliverables)

## What you should submit <!-- omit in toc -->

Before **11:59pm on Tuesday, 4/2**, you should submit to Canvas:
* A document in `pdf` or `docx` format, answering the question tagged with ![q]
* A screenshot in that document of your geocoded and symbolized data in QGIS

## Introduction and context

In this activity, you'll **geocode** historical address data. In this case, you'll work with data from the 19th century American children's book trade directory. The directory contains 2,600 entries documenting the activity of individuals and firms involved in the manufacture and distribution of childrens books in the United States chiefly between 1821 and 1876. It's [searchable online](https://www.americanantiquarian.org/btdirectory.htm), and—more importantly for us—you can [download the data](https://repository.upenn.edu/entities/dataset/16705c2f-023b-495e-baf4-dee805eae59f) from the University of Pennsylvania's Scholarly Commons.

The major difference between this activity and previous ones is that you'll be using a different geographic information system: QGIS!

![qgis](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c2/QGIS_logo%2C_2017.svg/2560px-QGIS_logo%2C_2017.svg.png)

[QGIS](https://www.qgis.org/en/site/) is a powerful, free, and open-source GIS software. You can do lots of the things in QGIS that you can do in ArcGIS Pro, including sophistiated vector and raster visualization/analysis.

QGIS is available on the Data Lab computers. Part of this activity will involve teaching yourself how to use it—now that you know your way around ArcGIS Pro, the learning curve for this will be less steep.

> ![imp]
>
> If you're unsure how to do something in QGIS—for example, adding vector data—your first step should be to just Google it (e.g., `qgis load vector data`). We also have a guide from the Leventhal Center on [getting started with QGIS](https://cartinal.leventhalmap.org/guides/get-started-qgis/), which may come in handy. There are also a *ton* of resources on [getting started with QGIS from Tufts](https://sites.tufts.edu/gis/quantum-gis-qgis-tutorials-tip-sheets/).

## Set up your workspace

### Directory stuff

No need to give you a ton of details at this point. You know what works for you. Set up a workspace for this activity!

### Open QGIS!

Open QGIS by typing "QGIS" into the search bar at the bottom left-hand side of the screen. Click the application when it appears.

When it opens, you'll be invited to start a "New empty project." Go ahead and double-click it:

![empty](./images/image05.png)

Once you're in QGIS, the interface should look fairly familiar. Here are the main components:

![components](https://cartinal.leventhalmap.org/assets/img/1-qgis-labeled.e4e44daa.gif)

In the **Browser panel**, double-click "XYZ tiles" and then double-click "OpenStreetMap". This should add an OpenStreetMap base map layer to your **map canvas**, and a layer will appear in the **layers list** underneath the browser panel:

![empty](./images/image06.png)

Now that you've got a working project, **save the file in your workspace** before moving on to the next step.

## Getting the data ready

### Download the data

Get the data of the 19th century American children's book trade directory from the University of Pennsylvania Scholarly Commons: <https://repository.upenn.edu/entities/dataset/16705c2f-023b-495e-baf4-dee805eae59f>

You should download both `0-dateaddr.xlsx` and `1-heading.xlsx`.

![download](./images/image01.png)

Take a beat to open the data in Microsoft Excel. Consider: which one of these files would you want to geocode?

### Pre-processing

Perhaps obviously, we're going to geocode the `0-dateaddr.xlsx` file, because it contains well-structured address data. But before you geocode this data, it needs a little bit of pre-processing.

There are thousands of records in this spreadsheet. Even a fraction of this will take a while to geocode, so let's focus on a smaller geography, like the state of Massachusetts. To do that we're going to filter the spreadsheet and exclude all records that aren't located in the state of Massachusetts.

1. In Microsoft Excel, open the `0-dateaddr.xlsx` file
2. In the "Home" tab, click "Filter"—you should see drop-down arrows appear next to all the fields

   ![sort](./images/image03.png)

3. Click on the drop-down arrow by the `state` field ➡️ uncheck "Select All" ➡️ scroll down to "MA" and check it
4. Open a new spreadsheet and save it as `directoryAddresses_MA`. **Make sure to save it as a `.csv`!**
5. In `0-dateaddr.xlsx`
   1. select all the data with `ctrl+A` or another selection method of your choosing 
   2. copy all the data with `ctrl+C` or right-click ➡️ "Copy"
6. In `directoryAddresses_MA.csv`, click on the cell in the most upper left part of the spreadsheet and paste the data with `ctrl+V` or right-click ➡️ "Paste"
7. Save your spreadsheet

Now we have `csv` data exclusively filtered for Massachusetts—a little more manageable for this activity.

## Geocoding children's book publishers

As we discussed in class, **geocoding**—the process of turning descriptive address information into spatial data—requires at least two points of reference:

1. A topologically sound network of vector data that ideally includes things like parcel boundaries, streets, and even buildings
2. Descriptive information associated with that topological network, e.g., a gazetteer

Thanks to OpenStreetMap, Nominatim, and MMQGIS, we have all of these things built into QGIS for free. That's why we're using this instead of ArcGIS Pro: in order to geocode addresses in ArcGIS Pro, we need to pay for it. I don't want to spend thousands of our [limited ArcGIS Online credits](https://www.esri.com/en-us/arcgis/products/credits/overview) on a learning exercise, so we're making lemons out of lemonade and also learning a new software while we geocode for free instead.

### OpenStreetMap, Nominatim, and MMQGIS

You already know what OpenStreetMap (OSM) is from the parking lot cemetery assignment: it's a free and open-source base map, the "Wikipedia of maps," because anybody can edit it. This serves as our topologically sound network of vector data as well as our descriptive information or gazetteer.

[Nominatim](https://nominatim.org/) is a free and open-source tool for geocoding with OSM data. You could geocode with Nominatim in ArcGIS Pro, but it requires writing bespoke code into the Python console.

[MMQGIS](https://plugins.qgis.org/plugins/mmqgis/) is a QGIS plugin for manipulating vector map layers in Quantum GIS: CSV input/output/join, geocoding, geometry conversion, buffering, hub analysis, simplification, column modification, and simple animation. It comes installed with QGIS in all the Data Lab computers, but if you don't see it in the toolbar at the top of your screen, it's really easy to install (`Plugins` ➡️ `Manage and install plugins` ➡️ search for `mmqgis`, click it, and click "Install").  

### Running the geocoder

To geocode the data, navigate to the menu bar at the top of the screen and click "MMQGIS" ➡️ "Geocode" ➡️ "Geocode CSV with Web Service." MMQGIS should appear on the upper right-hand side.

![geocode](./images/image04.png)

In the geocoding dialog that opens, you should see a dialog box like this:

![dialog](./images/image07.png)

**Click the little backspace arrows in the fields for "Output File Name" and "Not Found Output List."** This will make placing the output files in your workspace much easier.

Now fill out the parameters as in the image below, taking care to... 

1. Click the **backspace buttons highlighted in yellow** to remove the default file paths before you
2. Click the **ellipses highlighted in red** to select

![params](./images/image08.png)

... and before you click "Apply," **make sure that the "Web Service" parameter is set to `OpenStreetMap / Nominatim`!**

> ![imp]
>
> Before you click "Apply," note that **it's probably going to take at least 15-30 minutes to fully geocode this query**. It's not a fast tool. Only run it when you have time to let it run fully.

When you're ready, click "Apply," and wait...

![buffering](./images/image09.gif)

When it's done, your geocoding dialog should see something like this:

![done](./images/image10.png)

Wow! Pretty impressive that 100% of the records geocoded. Let's exit this dialog box and go back to the map. "Right-click" the layer in your layers list—mine is titled `directory_geocoded`—and click "Zoom to Layer(s)." You should see something like this:

![map](./images/image11.png)

Hmmm... why did a bunch of these layers end up outside of Massachusetts?

## Natural language processing "by hand"

We're not actually going to do any computational natural language processing (NLP) in this class, but if you think about it, geocoding is itself a kind of NLP: we're taking descriptive address data, "tokenizing" it into discrete parts, and passing that through an algorithm that can recognize those parts and assign them to places in the real world.

To wrap up this activity, I want you to do some natural language processing, but "by hand." By this, I mean you are going to manually look through the attribute table of the geocoded data and figure out why some things ended up in places where they weren't supposed to. **This is exactly the kind of work that NLP can automate, but for now, you're going to do a snippet of it manually.**

To accomplish this, you'll need to use the **selection** tool and the **attribute table**. Both of these should feel familiar, but in QGIS, they're just in slightly different places:

![selectattributes](./images/image12.png)

| ![q] |
| :--- |
| Pick five addresses from your geocoded layer and try to figure out why OSM couldn't match them to their expected geography in Massachusetts. Consider: does the historical address, as it's listed in the source spreadsheet, still exist? Has the address possibly changed? To figure this out, I recommend searching for the addresses as they appear in the attribute table in Google Maps. You can also try going to OSM and navigating to where you would expect that address to appear. See if you can determine why it didn't join, and for each record, explain why you think it didn't match, and how you think you might fix it. (These answers might be similar for multiple addresses.) |

## Join the `1-heading.xlsx` table to your geocoded layer

In your workspace, you should have a secondary table that you could join to the geocoded layer based on a common field.

> ![imp]
> 
> Before trying to join anything, make sure that you save the `xlsx` file as a `csv` file.
> 
> `csv` files behave better with QGIS.

Table joins in QGIS are pretty easy. Try [following this tutorial](https://www.qgistutorials.com/en/docs/3/performing_table_joins.html) to join the `1-heading.csv` layer to your geocoded data.

You should be able to identify the *common field* required for the join by comparing the **attribute table** of your geocoded layer with the `1-heading.csv` spreadsheet.

## Symbolize your data

To wrap up, try symbolizing your data. It's pretty similar in QGIS to how you'd to it in ArcGIS Pro.

1. Right-click on the geocoded layer in your layers list
2. Click on the "Symbology" tab on the left-hand side
3. Pick "Categorical"
4. Set the value to `heading_name`
5. Click the symbol and make it bigger—maybe `4.0` in size
6. Use a "Random color" ramp
7. Click "Classify" just below the ramp
8. When you're done, click "OK" in the bottom right-hand corner of the Symbology dialog

![symb](./images/image13.png)

# Activity deliverables

Before **6:30pm on Tuesday, 2/27**, you should submit to Canvas:
* A document in `pdf` or `docx` format, answering the question tagged with ![q]
* A screenshot in that document of your symbolized and geocoded data in QGIS



<!-------------------------------------[ Links ]
---------------------------------------->

[data]: https://canvas.tufts.edu/courses/54475/files/7090292/download?download_frd=1

<!---------------------------------[ Buttons ]--------------------------------->

[imp]: https://img.shields.io/badge/IMPORTANT!-red?style=plastic
[q]: https://img.shields.io/badge/Question-blue?style=plastic
[qs]: https://img.shields.io/badge/All_Questions-blue?style=plastic
[down]: https://img.shields.io/badge/Download_the_data-blue?style=for-the-badge
