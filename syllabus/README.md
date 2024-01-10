# CLS0125 Introduction to Geospatial Humanities <!-- omit in toc -->

*Cross-listed with History 179, Art History (FAH) 0092-04, Archaeology (ARCH) 175*

**Spring 2024**

**Day/Time:** Tuesdays, 6:30-9pm

**Location:** Data Lab, Tisch Library

**Course Instructor:** Ian Spangler

**Office hours:**

* Ian: Tuesdays 5:30-6:30pm or by appointment on Zoom
* Max: Mondays, 12-1pm; Wednesdays, 1-2pm

**Prerequisites:** None. Students will be expected to have competence in computer use and some familiarity with Microsoft Windows environment and file management. 

### Table of contents <!-- omit in toc -->
- [Course Description](#course-description)
- [What you will learn](#what-you-will-learn)
  - [Major goals](#major-goals)
  - [Learning objectives](#learning-objectives)
- [Detailed schedule](#detailed-schedule)
  - [Part I: Fundamentals](#part-i-fundamentals)
  - [Part II: Approaches](#part-ii-approaches)
  - [Part III:](#part-iii)
- [Course Requirements and Grading](#course-requirements-and-grading)
- [Assignments](#assignments)
  - [In-class assignments](#in-class-assignments)
  - [Labs](#labs)
  - [Exercises](#exercises)
- [Final Project](#final-project)
- [Required Readings](#required-readings)
- [Style Guidelines \& Citation](#style-guidelines--citation)
- [Accommodations for Students with Disabilities](#accommodations-for-students-with-disabilities)

---

<!-- ### Schedule -->

<!-- <button>[Schedule](../schedule/README.md)</button> -->

### Course Description

The humanities are becoming spatial.  informs not only how texts, maps, and other objects are produced, but how we encounter them as readers and users. In this course, we will prod at the geospatial dimensions of the humanities, or those aspects from which we can derive structured geographic data.

This course introduces geospatial theory, methods, and technology for applications in the humanities in past and present settings. We'll often use the catch-all term "GIS" – short for **geographic information systems** – to describe these geospatial tools. GIS consists of a combination of software, data, methods, and hardware with capabilities for manipulating, analyzing, and displaying spatially referenced data.

The course gives primary emphasis to GIS data structures, data creation, geodesy, spatial analysis, and cartographic visualization. We will discuss not only how to use these tools effectively, but how to use them intentionally. Detailed labs and exercises apply concepts presented in the lectures using two geospatial softwares: ArcGIS Pro and ArcGIS StoryMaps software. Assignments concentrate on applying concepts covered in lectures and exercises and include a final project that applies GIS to each student's field of interest.

### What you will learn

Students will learn to use GIS to answer humanistically-informed spatial questions. For instance:

* A student interested in **urban history** seeks to determine those buildings built on filled-land within the City of Boston. The student acquires or creates an [historical shoreline of the City of Boston](https:•data.leventhalmap.org/#/catalog/dkircu2ol) and uses overlay operations to determine those buildings constructed outside of the original Boston shoreline. The student then further qualifies their spatial questions by construction date to identify buildings older than 1900 or by construction materials (brick, wood, concrete, etc.) or by use (residential, commercial, etc.).
* A student interested in **environmental history** wants to assess the impact of the straightening of the Mystic River in Massachusetts. Using historical maps and historical aerial photography, the student creates a GIS dataset of the historical Mystic River. Through incorporating additional historical GIS data and spatial operations, the student calculates the historical and present landcover and populations impacted by the straightening of the river.
* A student of **classical literature** is interested in approaches to distant readings of *The Odyssey*. The student extracts locations of places mentioned within the text and calculates the number of mentions of each place and by place type (settlement, water body, temple, etc.). This facilitates visualization techniques to identify significant places mentioned within the text. The student also incorporates additional data and various spatial measures to determine clustering and other possible patterns present in the text. The student also uses the data to visualize the journey of Odysseus.

#### Major goals

The major goals of this course are for the student to learn:

-   Spatial data structures, georeferencing, and geoprocessing
-   Spatial analysis methods for problem solving
-   Applications of GIS across the humanities
-   Basic concepts in spatial databases and queries
-   Principles of cartographic design

#### Learning objectives

By the end of this course students will have achieved the following learning objectives:

-   Identify data structures in spatial data (rasters or vectors)
-   Identify, locate, and acquire spatial data pertinent to projects in their field of interest, as well as pinpoint significant gaps in or problems with existing information
-   Evaluate the appropriateness of the existing data sources for use in a given application
-   Understand the data creation process and create geohistorical spatial data sets derived from historical maps, gazetteers, aerial photography, texts, etc.
-   Create spatial data from tabular information that includes a spatial reference
-   Describe, design, and use basic spatial databases (using keys, joins and queries)
-   Use appropriate spatial analysis methods for rasters and vectors as well as linking these methods together in a more complex analytical model.
-   Create high-quality maps and associated graphics/visualizations with text that clearly communicate spatial information and the results of analysis
-   Design an independent project that incorporates spatial analysis methods
-   Appraise spatial analysis in journal articles
-   Use appropriate map projection and coordinate system
-   Use ArcGIS Pro software with strong proficiency

### Detailed schedule

Our semester breaks down into three "Parts." During **Part I** (weeks 1-4), we'll pick up the fundamentals of geospatial humanities. During **Part II** (weeks 5-10), the rubber meets the road as we experiment with various technical and analytical approaches to "doing" the geospatial humanities. Lastly, in **Part III** (weeks 11-15), we'll go "beyond" GIS, examining other tools, archives, etc.

Both the schedule and its weekly themes are subject to change.

#### Part I: Fundamentals

**Week 1, January 23 • Introductions • What is our subject?**

> *Defining "geospatial humanities"; critical cartography; kinds of maps; "x" GIS; mapping with purpose; asking spatial research questions.*

* What are the "geospatial humanities?" What are its constitutive objects, and why are *you* interested in them? What defines a "humanistic" approach to geographic information systems and spatial data? How ought we approach these questions from a technical perspective?
* First day of class! Nothing due...

**Week 2, January 30 • Distortion • Squashing globes and bending lines**

> *Geographic and projected coordinate systems; scale; projecting XY data; basic web mapping; tile pyramids.*

* How do we go about displaying round earth as a flat map? What are the basic mathematical and geodetic rules associated with this process? What sacrifices do we have to make in order to "flatten" the globe, and how have those sacrifices been used strategically?
* Due before class:
  * Exercise 01: Learning ArcGIS Pro Basics
  * "[Squashing the globe](https://www.leventhalmap.org/digital-exhibitions/bending-lines/how-to-bend/projections/)," *Bending Lines: Maps and Data from Distortion to Deception*. 2020.

**Week 3, January 30 • Data • Making and mapping observations**

> *Evaluating data & sources; data classification; understanding vector & raster models; situated knowledge & strong objectivity; querying; logical operators.*

* What is spatial data and what are spatial data models? Where does spatial data come from? How should you understand data in their social context? How can we ethically represent different data cartographically?
* Due before class:
  * Activity 01: Mapping ancient places
  * Bouie, Jamelle. 2022. "[We Still Can’t See American Slavery for What It Was.](https://www.nytimes.com/2022/01/28/opinion/slavery-voyages-data-sets.html.)" *The New York Times*, January 28, 2022, sec. Opinion.
  * OPTIONAL: McKittrick, Katherine. 2014. "[Mathematics Black Life.](https://www.jstor.org/stable/10.5816/blackscholar.44.2.0016)" *The Black Scholar* 44 (2): 16–28.

**Week 4, February 6 • Design • Aesthetics and politics in mapping**

> *Basic color theory; choropleth mapping; the modifiable areal unit problem; layer blending; icons and iconography; text on maps; basemaps.*

* What are the best practices for representing spatial data and making maps? To what extent are those practices contingent on flexible cultural and social norms? When should you bend or break these rules in order to make a more effective argument? Is cartography an "art" or a "science?"
* Due before class:
  * Exercise 02: Mapping the Transatlantic Slave Trade Database: 1676-1805
  * Krygier, J B. 1995. "[Cartography as an Art and a Science](https://www.researchgate.net/publication/233697179_Cartography_as_an_art_and_a_science)?" *The Cartographic Journal* 32: 9.

#### Part II: Approaches

**Week 5, February 13 • Archives I • Contingencies of counting people**

> *Census data; table joins; *

* Why do we count people? Where does the device of a "census" come from? Who gets counted and who doesn't? How can we map those presences and absences?
* Due before class:
  * Assignment 01: Cartography assignment
  * Jacobs, Alexandra. 2022. "[Counting the Population Has Always Been Political](https://www.nytimes.com/2022/08/28/books/democracys-data-dan-bouk.html)," *The New York Times*, 2022.
  * Loftus, Eve and Joan Brunetta. 2024. "Mapping Black Cambridge," *Leventhal Map & Education Center*.


**Week 6, February 20 • Analysis I • Vector analysis**

> *Spatial joins;*

* 

**Week 7, February 27 • Archives II • Breathing new life into old maps**

* **Guiding questions**.
* **Theoretical positions**.
* **Technical skills**. Deriving data from historic maps; Georeferencing; feature extraction.

**Week 8,  • Analysis II • Raster analysis**

* **Guiding questions**.
* **Theoretical positions**.
* **Technical skills**. 

**Week 9 • Mandatory relaxation • Spring break**

*No class*

#### Part III: 

**Week 10 • xxx • xxx**

.

**Week 11 • Archives III • Maps from text**

What are the concepts and theories behind natural language processing (NLP) as method in the geospatial humanities?

**Week 12 • Analysis III • What is our subject?**



**Week 13 • Introductions • What is our subject?**

.

**Week 14 • Introductions • What is our subject?**

.

**Week 15 • Introductions • What is our subject?**

.

**Week 16 • Introductions • What is our subject?**

.

### Course Requirements and Grading

Students will develop GIS skills through a series of exercises and assignments during the semester. Each student will then complete a [final project](#final-project) of their choice. Students will be expected to attend every class and to complete all graded assignments as well as ungraded tutorials and in-class exercises. Completion of [Exercises](#exercises) and [Assignments](#assignments) will require additional computer/lab time outside of class.

You are expected to complete all 6 Exercises, but only 5 of them will be graded. It is up to you to decide which 5 you submit for a grade. If you choose to submit 6, the lowest graded Exercise will be dropped.

You must complete ***all*** Assignments.

Grading will be based on a **1000-point scale**. Graded assignments and exercises may be turned up to one week late. All late assignments will receive a -10 point deduction and all late graded exercises will receive a -5 point deduction. Details regarding the assignments and requirements for the final project can be found on the Canvas Course Schedule.

-   Several Labs (5 graded) worth a total of 250 points (50 each)
-   4 skill-building Exercises worth a total of 400 points (100 each)
-   Class participation worth 100 points
-   The Final Project poster or StoryMap worth 250 points

| Type          | Quantity | Points per activity |
| ------------- | -------- | ------------------- |
| Exercises     | 5        | 50                  |
| Assignments   | 4        | 100                 |
| Participation | n/a      | 100                 |
| Final Project | n/a      | 250                 |

### Assignments

There are three kinds of assignments in this class: **In-class assignments**, **Labs**, and **Exercises**.

#### In-class assignments

In-class assignments 

#### Labs

The course uses weekly **Labs** tailored for students to learn the topic(s) of each week. Four of the exercises must be submitted for a grade.

Each Exercise weaves together several components:

-   A specific method/concept
-   The utilization of geospatial software to execute that method/concept (most often, ArcGIS Pro)
-   The application of that method/concept to a specific area of the humanities (urban history, environmental history, literature, archaeology, art history, etc.)
-   The relevant types of data and data sources for that application
-   The relevant data, map projections, and visualization methods for specific geographic locations

Exercises are situated in different regions of the world and they vary across different geographic scales: neighborhood, city, state, country, region, continent, global.

#### Exercises

**Exercises** concentrate on applying concepts covered in lectures and exercises to each student's field of interest and build toward a final project that applies GIS to each student's field of interest.

### Final Project

The purpose of the final project is to provide additional experience in collecting, processing, analyzing, and visualizing spatial data. In addition, the students must conduct a literature review as part of their project proposal.

The project must use ArcGIS Pro to examine the spatial implications of a research problem. The final project will result in a **large-format infographic (poster) or an online interactive StoryMap** that describes the research question, data, and methods as well as the analysis and the results. Examples of similar student projects can be found at [Tufts GIS Expo Explorer](https:•expoexplorer.it.tufts.edu/).

Students who create a large-format infographic may choose to exhibit their work at Tufts' GIS Expo day for 25 points (5%) of extra credit.

### Required Readings

**There is no textbook for this class.**

Readings for the course will be primarily from the [ArcGIS Online Resources](https:•www.esri.com/en-us/arcgis/products/arcgis-desktop/resources) and the [GIS&T Body of Knowledge](https:•gistbok.ucgis.org/). Using these online materials also familiarizes the students with the vast availability of online resources.

Additional readings are available through online journal databases open to Tufts students and through public web sites.

### Style Guidelines & Citation

All **cartographic work** should adhere, when appropriate, to key principles of map design covered in week 3 of the course.

All **written work** should be consistent with the style guidelines of one of the two major style guides—the Chicago Manual of Style (MLA) or the Publication Manual of the American Psychological Association (APA). Both provide clear guidelines for referencing and citing other works.

The [Purdue Online Writing Lab](https:•owl.purdue.edu/) has extremely good guidance to both styles. I also recommend downloading [Zotero](https:•zotero.org) to manage citations. Tufts provides a [guide](https:•researchguides.library.tufts.edu/zotero) for getting started. It will make your life easier far beyond this class.

### Accommodations for Students with Disabilities

Tufts University values the diversity of our body of students, staff, and faculty and recognizes the important contribution each student makes to our unique community. Tufts is committed to providing equal access and support to all qualified students through the provision of reasonable accommodations so that each student may fully participate in the Tufts experience. If a student has a disability that requires reasonable accommodations, they should please contact the StAAR Center (formerly Student Accessibility Services) at StaarCenter\@tufts.edu or 617-627-4539 to make an appointment with an accessibility representative to determine appropriate accommodations. Please be aware that accommodations cannot be enacted retroactively, making timeliness a critical aspect for their provision.
