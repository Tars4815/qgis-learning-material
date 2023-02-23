# Introduction

## **What is a GIS?**

A **GIS** (*Geographic Information System*) is a computerised information system that allows the **acquisition**, **storage**, **analysis**, **visualization** and **exchange** of geographical information in the form of **geo-referenced data**.

It then allows data to be associated with their geographical position on the earth's surface and processed in order to extract information.


The most common **GIS software** are:

* ArcGIS
* QGIS
* GeoMedia
* SagaGIS
...

**Why QGIS?**

It is:

* Free and Open Source
* Constantly updated -> Every 4 months a new version is released

But it has the great advantage for those working with older versions that it can also handle projects made with newer versions.

![QGIS logo](./assets/img/QGIS-logo.png "QGIS logo")

## **Main functionalities**

* **Data visualisation**:

Vector and raster data can be displayed and superimposed in different formats and map projections.

* **Data exploration and map print layout creation**:

You can compose maps and interactively explore spatial data through an easy-to-use graphical interface.

* **Creation, editing, management, export**:

Spatial analysis of data can be performed 

* **Link to external DBs**:

You can view and query data stored on external DBs (e.g., MySQL, PostgreSQL...).

* **Publication of maps on the web**

With native and non-native plugins, QGIS allows you to define settings to make an interactive map to share on web pages.

...and much more!

## Graphic User Interface

The GUI of QGIS Desktop is mainly composed of:

1. **Menu toolbar** where you can find the main QGIS project features grouped by themes.
2. **Attributes and Vector toolbar** customizable that includes shortcuts to the most commonly used tools for data manipulation in a GIS environment.
3. **Loaded layers list** which indicates what data have been included in the project, specifying their characteristics, symbology and visibility.
4. **Map view** that is the map canvas on which the geographic and geometric component of the data can be evaluated graphically.
5. **Status bar** indicating the status of any processings initiated and any errors encountered.

![QGIS Graphic User Interface](./assets/img/GUI-en.png "QGIS GUI")

## Data management

**How QGIS handles geographic data?**

What is needed in order to work with QGIS?

* Knowing how to handle geographical data in **different geographical and/or projected coordinate systems**;
* Knowing how to manage a project;
* Knowing how to import:
    * **Vector** data (e.g. shapefile .shp, GeoJSON .geojson...)
    * **Raster** data (e.g. .tiff)
* Understanding the functionalities of **plugin**

**What is the purpose of a reference system?**

**Reference System** -> set of rules that allow us to determine the position in space in a unique way.

This geometric concept is even more important in cartography to correctly locate a point in the territory.

![Reference system](./assets/img/cartesian-sr.png "Reference system")

## Geographical reference system

The concept of geographical reference system is the best known and most comprehensive, and perhaps also one of the most powerful georeferencing systems.

**It is metric, standard, stable, unique.**

It uses a well-defined and fixed reference
based on:

* Earth's axis of rotation
* centre of mass
* Greenwich reference meridian
* Equator

[INSERIRE IMMAGINE]

Normally, different R.S. are used for planimetry and altimetry....

* **planimetry**: ellipsoid reference (spherical for small or large scales). Why it is not used for altimetry? No link with the gravity field.

![Planimetry](./assets/img/planimetria.png "Planimetry Reference Systems")

* **altimetry**: geoid reference (no simple analytical description). Why is it not used for planimetry? It is very complex to use in the treatment of observations made for planimetry (due to angles and distances conversion).

![Geoid](./assets/img/geoid.png "Geoid")


## Datum

A **datum (geodetic)**, is a geodetic reference system that allows the position of points on the Earth's surface to be defined in mathematical terms.


**Datum** -> Set of parameters defining the **shape** of the ellipsoid used and its **orientation**.


A datum is composed by 8 parameters:

* 2 for the ellipsoid shape;
* 6 for the position and the orientation:
    * latitude e longitude on the ellipsoid (2)
    * geoid height
    * 2 components of the deviation from the vertical
    * azimut of the ellipsoid

## Projections

The surface of the earth is curved but there are many reasons for representing it on a **plane**, even in numerical cartography.

* The map used to represent the results of GIS analysis is flat.
* Flat maps are scanned and used to create GIS data.
* The raster model is flat (2D)
* It is not possible to see all the land on a curved surface at once
* It is much easier to make measurements in the plane (areas, distances, directions)

For this reason, different **map projections** are also used in numerical cartography.

![Projection](./assets/img/proj.png "Projection")

Cartographic projections carry coordinates from the ellipsoid of the reference system to the map plane. **The two surfaces are not topologically equivalent, so it is not possible to move from ellipsoid to map without deformation.**

Depending on the **geometric shape** adopted, the projections are classified as:

* Planar projections;
* Cylindrical projections;
* Conic projections.

There are many types of map projections, those used in **Italy** are:

* **UTM** (Universal Trasversal Mercator), globally adopted;
* **Gauss-Boaga**, used for the Roma 40 Monte Mario datum;
* **Cassini-Soldner**, used for Nuovo Catasto dei Terreni Italiano.

Ultimately, the definition of a reference system is given by:

* *geographical coordinate systems*:

**Datum** (es. WGS84 or Roma 40 Monte Mario)

* *sistemi di coordinate proiettate*:

**Datum + projection system** (es. WGS84-UTM32N or Roma 40 Monte Mario - Gauss Boaga Fuso Ovest)

In addition, all GIS softwares use geometric parameter registers, the best known of which are the **EPSG** (European Petroleum Survey Group) codes that unambiguously define the various world reference systems.

**How does QGIS handle geographical data?**

The management of **reference systems** is always a particularly delicate element in a GIS.

In QGIS, there are 2 different reference system managements: 

* **Project R.S.**
* **Single layer R.S.**

QGIS is capable of reprojecting on the fly individual layers using the [proj4](https://proj.org/) libraries, provided that the R.S. of the individual layer is defined.

QGIS uses **EPSG** (European Petroleum Survey Group) codes to uniquely define the different global reference systems.

### RS Settings

In the settings panel (***Settings → Options → CRS tab***) it is possible to define the rules with which the layers RS can be managed.

![Reference System Settings](./assets/img/SRsettingsprj.png "Reference System Settings")

It allows you to define which SR to adopt when opening a new project or how to manage layers without information on the reference system used.

### Layer RS

The **SR of the individual layer** can be managed by right-clicking on the layer.

![Layer Reference System Settings](./assets/img/layer-sr-en-01.png "Layer Reference System Settings")

![Layer Reference System Settings](./assets/img/layer-sr-en-02.png "Layer Reference System Settings")

### Reprojection - Shapefile

You can manage the re-projection of vectors: ***Right click on the layer → Save features as…***

![Vector reprojection](./assets/img/vector-reproj.png "Vector reprojection")

## Reality modelling with QGIS

There are mainly two ways of conceptualising or modelling reality from a geographical point of view by considering objects as:

* **Discrete objects**: can be observed or described in the real world and identified by its position

![Vector model](./assets/img/vector-model.jpg "Vector model")

* **Distributed objects**:
represent a quantity whose value is a function of position and can be measured at any location

![Raster model](./assets/img/raster-model.png "Raster model")

**Vector** model: information on discrete objects is coded and stored as a set of x, y, z coordinates.

The vector model indicates a representation of geographical entities through:

* **Points**
* **Lines**
* **Polygons**

Vector model features are particularly useful for representing and storing discrete objects such as buildings, roads, particles, etc.

**In the vector model, information on discrete objects is coded and stored as a set of x,y,z coordinates.**

![Vector model primitives](./assets/img/vector-model-primitive.png "Vector model primitives")

**Raster** model: information on continuous objects, are coded using a set of grid cells, each with its relative value 

Values are cells of a grid with certain extensions and a certain resolution. 

![Raster model primitives](./assets/img/raster-model-primitive.png "Raster model primitives")

## Shapefile import

![Shapefile import](./assets/img/shapefile-import.png "Shapefile import")

![Shapefile import](./assets/img/shapefile-import-1.png "Shapefile import")

![Shapefile import](./assets/img/shapefile-import-2.png "Shapefile import")

## Shapefile properties

To change the properties of the shapefile, right-click on the layer and select properties.

![Shapefile properties](./assets/img/shapefile-properties.png "Shapefile properties")

### Stile

**Visualizzazione con singolo simbolo**

[INSERIRE IMMAGINE]

E' possibile anche impostare la trasparenza del layer che può essere utile nei casi in cui si vuole sovrappore questo ad un altro strato informativo (es. un'ortofoto).

**Visualizzazione con simbolo categorizzato** in base ai valori contenuti in un campo del layer.

[INSERIRE IMMAGINE]

L'utilizzo di questo stile permette anche di assegnare a ogni valore individuato un'etichetta da includere nella legenda. In questo modo il significato del campo scelto e dei suoi valori risulta ancora più chiaro e comprensibile.

[INSERIRE IMMAGINE]

### Etichette

Per identificare meglio i comuni è possibile inserire anche le etichette relative ad ogni unità geometrica: cliccare su **etichette** -> Selezionare ***Etichette singole*** e scegliere quale ***Valore*** far comparire.

[INSERIRE IMMAGINE]

[INSERIRE IMMAGINE]

## Dati vettoriali

### Tabella attributi

Per visualizzare la tabella con i comuni della provincia di PC, cliccare con il tasto destro sul layer nel pannello layer -> premere ***Apri tabella attributi***

### Aggiunta campo

***Tasto destro sul layer -> Apri tabella attributi -> Attiva modifiche -> Nuovo campo***

[INSERIRE IMMAGINE]

Definire i campi richiesti con particolare attenzione al **tipo di valore** che verrà inserito nel nuovo campo (numero intero, decimale, testo, data, etc.) e il **numero massimo di caratteri**.

[INSERIRE IMMAGINE]

Per finalizzare le modifiche, salvare e concludere la sessione di editing.

### Calcolatore di campi

***Tasto destro sul layer -> Apri tabella attributi -> Attiva modifiche -> Apri il calcolatore di campi***

[INSERIRE IMMAGINE]

Con il **calcolatore di campi** è possibile creare un nuovo campo con il risultato della funzione scelta oppure aggiornarne uno esistente.

[INSERIRE IMMAGINE]

### Rimuovi campo

***Tasto destro sul layer -> Apri tabella attributi -> Attiva modifiche -> Elimina campo***

[INSERIRE IMMAGINE]

Selezionare il campo di interesse e confermare la rimozione.

[INSERIRE IMMAGINE]

Per finalizzare le modifiche, salvare e concludere la sessione di editing.

## Dati raster

Che cos'è un raster?

[INSERIRE IMMAGINE]

Un dato fondamentale per le analisi GIS sono i cosiddetti **Digital Terrain Model** (DTM) ma ci sono anche **Ortofoto**, **Carte tecniche**, foto aree, immagini satellitari, mappe geologiche etc.

### Modelli digitali delle altezze

* **DEM** (Digital Elevation Model) è un file digitale con le quote della superficie del terreno a intervalli regolarmente spaziati sul piano orizzontale.

* **DTM** (Digital Terrain Model) avrebbe un significato più generico indicando oltre alla quota della superficie del terreno anche altre informazioni come pendenza ed esposizione.

* **DSM** (Digital Surface Model) rappresenta in forma digitale le quote della parte superiore del terreno comprensivo degli edifici, delle infrastrutture e degli alberi senza le procedure di filtraggio utilizzare per produrre DEM e/o DTM.

[INSERIRE IMMAGINE]

### Ortofoto

E' una mappa fotografica che combina le caratteristiche di una mappa tradizionale con quelle di un'immagine. E' georeferenziata, priva di distorsioni e con scala uniforme.

### Importare un raster

[INSERIRE IMMAGINE]

### Riproiezione

La riproiezione raster tramite le librerie GDAL:
***Raster -> Proiezioni -> Riproiezione**

[INSERIRE IMMAGINI]

### Proprietà

Per modificare le proprietà del raster, cliccare sul tasto destro e selezionare **proprietà**:

[INSERIRE IMMAGINE]

### Stile

Modificare lo **stile**:

* Banda singola grigia
* Colori banda multipla
* Valori a tavolozza
* Banda singola falso colore
* Omreggiatura

...e altre opzioni statistiche.

[INSERIRE IMMAGINE]




[IN COSTRUZIONE//]