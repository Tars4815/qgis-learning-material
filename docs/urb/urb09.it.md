---
tags:
  - QGIS
  - Urbanistica
  - Raster
  - Modelli digitali del terreno
  - DTM
---

# Elaborazioni di routine su Digital Terrain Models

## Scopo dell’esercizio

Calcolare le caratteristiche morfologiche dei comuni montani della Provincia di Piacenza e visualizzarne l’andamento del terreno in modalità 2.5D.

## Dati

### Vettoriali

* Shapefile dei confini amministrativi dei comuni della Provincia di Piacenza – Fonte: [Geoportale Emilia-Romagna](https://geoportale.regione.emilia-romagna.it/download/dati-e-prodotti-cartografici-preconfezionati/confini-amministrativi/ambiti-amministrativi-2021): scaricare il formato di interesse e isolare con selezioni appropriate i comuni della provincia in studio.

### Raster

* Raster tiff del Modello Digitale del Terreno della Provincia di Piacenza – Fonte: [Geoportale Emilia-Romagna](https://geoportale.regione.emilia-romagna.it/download/download-data?type=raster) > Altimetria > DTM 5x5 metri: selezionare la Provincia di Piacenza, selezionare tutti i tasselli di interesse e avviare la procedura di download.

## Istruzioni per l'esecuzione

### Preparazione dati

Definire le unità di misura e il percorso relativo: *Project > Properties > General Tab > Save paths > Relative*. Impostare il sistema di riferimento con codice EPSG: 25832 – ETRS89 – UTM Zone 32 N.

Caricare i file raster del DTM della provincia di Piacenza. Controllarne le caratteristiche e l’estensione.

Realizzare un unico file raster per tutti i DTM: *Raster > Miscellaneous > Merge*. Per *Input layer*, cliccare sul pulsante *...*, selezionare tutti i tasselli raster DTM caricati nel progetto e infine confermare con *OK*. L'obiettivo dell'operazione è realizzare un unico raster con singola banda per l'intera dell'estensione della Provincia. Scegliere la cartella di output ed eseguire l'operazione.

??? note
    
    Nel caso in cui avessimo lavorato, per esempio, con immagini satellitari su bande distinte e avessimo voluto creare un'immagine "true color" RGB avremmo potuto eseguire la stessa operazione di *Merge* con i raster per le bande R (rosso), G (verde) e B (blu) e avremmo spuntato l'opzione *Please each input file into a separate band*.

Sottocampionare il raster DTM, a 25 metri: *Tasto dx sul layer > Export > Save As*. Nel box *Resolution* definire 25 come valore *Horizontal* e *Vertical*. Salvare con un nome appropriato il nuovo file.

Caricare il layer vettoriale dei confini amministrativi dei comuni della Provincia di Piacenza.

Ritagliare quindi il raster DTM sfruttando i poligoni dei comuni come maschera: *Raster > Extraction > Clip Raster By Mask Layer*. Definire il raster da ritagliare come *Input layer* e il vettoriale dei comuni come *Mask layer*. Definire il sistema di riferimento appropriato. Eseguire l’operazione di Clip.

Definire la trasparenza delle zone no data (rappresentate in nero) nel layer ritagliato. Tasto dx > *Properties > Transparency*. Nella sezione *Custom Transparency Options*, attivare il pulsante *Add values from display*, cliccare quindi su un pixel dell’area da nascondere alla visualizzazione: comparirà una nuova riga nella tabella sottostante con il valore contenuto nel pixel cliccato e la percentuale di trasparenza che verrà applicata in visualizzazione per pixel con tale valore. Applicare e confermare le impostazioni definite.

## Simbologia

Modificare la simbologia del raster: tasto dx > *Properties > Symbology.*

Per uno stile di visualizzazione continuo, selezionare *Render type: Singleband Pseudocolor*:

* *Interpolation*: Linear
* *Color ramp*: Spectral
* *Mode*: Continuous
* *Min/Max Value Settings*: selezione su Min/Max
* Cliccare *Classify* e poi su *Apply*

Per uno stile di visualizzazione discreto, selezionare *Render type: Singleband Pseudocolor*:

* *Interpolation*: Discrete
* *Mode*: Equal interval
* *Classes number*: 5
* Cliccare *Classify* e poi *Apply*

## Calcolo di statistiche e curve di livello

Calcolare le statistiche descrittive del layer DTM: *Processing Toolbox > Raster analysis > Raster layer statistics*. Nel file html in uscita dal processamento è possibile valutare alcune statistiche utili.

Estrarre le curve di livello dal raster: *Raster > Extraction > Contour*. Scegliere come input il raster DTM, *Interval between contour lines*: 50 metri, *Attribute name*: ELEV. Eseguire l’operazione.

Calcolare ora la quota media di ciascun comune: *Processing Toobox > Raster Analysis > Zonal Statistics*. *Input layer*: shapefile comuni, *Raster layer*: DTM. Eseguire l’elaborazione. Valutare la tabella attributi del layer shapefile risultante, graduarne la simbologia secondo la media delle quote per tre zone (Pianura, Collina e Montagna) e estrarre solo i comuni categorizzati come Montagna. Ritagliare la porzione di raster DTM corrispondente a questi comuni: solo questa verrù utilizzata per le prossime elaborazioni.

Estrarre un profilo di andamento di quote a partire dal DTM: *View > Elevation profile*. Cliccare sull’icona di tracciamento di un profilo *Capture curve* e tracciare il profilo di interesse in modalità analoghe a quelle per la vettorializzazione di elementi lineari. Una volta terminato il tracciamento, premere il tasto destro del mouse: nella sezione del grafico del profilo verrà visualizzato l’andamento della sezione a partire dai valori campionati sul raster DTM.

## Calcolo di ombreggiatura, pendenza e esposizione

Realizzare un’elaborazione di calcolo delle ombreggiature: *Raster > Analysis > Hillshade*. *Input*: raster DTM, *Azimuth of the light*: 315 (senso orario), *Altitude of the light*: 45. Eseguire l’operazione.

Realizzare un’elaborazione di calcolo delle pendenze: *Raster > Analysis > Slope*. *Input*: raster DTM, spuntare *Slope expressed as percent instead of degrees* se si vuole il calcolo in percentuali. Eseguire l’operazione.

Realizzare un’elaborazione di calcolo delle esposizioni dei versanti: *Raster > Analysis > Aspect*. *Input*: raster DTM, spuntare l’opzione *Return 0 for flat*. Eseguire l’operazione. Il layer risultante avrà valori in gradi compresi tra 0 e 360, in cui 0-45 = Nord, 45-135 = Est, 135-225 = Sud, 225-315 = Ovest (315-360 Nord). Adottare una simbologia raster adeguata per l’interpretazione del risultato.

Calcolare la superficie esposta a Sud: *Raster > Raster calculator*. Espressione: *“Aspect_Raster” > 135 AND “Aspect_Raster” <=225*

L’output sarà un file raster binario in cui il valore sarà:

* 1 nei pixel che soddisfano la condizione dell’espressione (“Aree che si affacciano a Sud”)
* 0 nei pixel che non soddisfano la condizione dell’espressione (“Aree che NON si affacciano a Sud”)

Calcolare il valore di superficie delle aree esposte a sud: *Processing Toolbox > Raster Layer Unique Values Report*.

### Visualizzazione e rendering 2.5D

Attualmente esistono due modalità di visualizzazione interattiva per i DTM (raster) in 2.5D:
* visualizzatore nativo con livello di interazione base
* visualizzatore con plugin QGIS2ThreeJS con livello di interazione avanzato e possibilità di esportazione della scena per ambiente web (documentazione: https://qgis2threejs.readthedocs.io/en/docs/).

Aprire il viewer 3D nativo di QGIS: *View > 3D Map Views > New 3D Map View*. Cliccare il pulsante *Configure…* per accedere alle impostazioni per la configurazione. Nella tab *Terrain*, flaggare la sezione *Terrain* e impostare come *Type*: DEM (Raster Layer), in *Elevation* scegliere quindi il raster di interesse. Modificando il valore del parametro *Vertical Scale* è possibile “enfatizzare” o “smussare” la scala delle quote nella rappresentazione 2.5D.

In alternativa, installare il plugin QGIS2Three: *Plugins > Manage and install plugins > Cercare Qgis2threejs > Installa*

Aprire l’interfaccia del plugin: *Web > Qgis2threejs > Qgis2threejs Exporter*

Abilitare la visualizzazione del DTM di interesse flaggando il raster associato nel box Layers.

Modificare la visualizzazione “enfatizzando” la componente z (senza esagerare): *Scene > Scene settings > Z exaggeration* = 5

Navigare nell’interfaccia di visualizzazione 3D: Tasto destro > Traslazione, Tasto sinistro > Rotazione, Rotella mouse > Zoom

Creare un’animazione video a partire da keyframe di interesse:

* Posizionarsi in una vista di interesse nella visualizzazione 3D
* Premere + nel menù del box Animation per aggiungere il keyframe
* Ripetere i due punti precedenti fino ad ottenere un numero di keyframe soddisfacente (>4)
* Premere l’icona Play (Perform the checked animations in parallel) per visualizzare il video creato a partire dai keyframes salvati

!!! note
    
    L’utilizzo di questo plugin potrebbe risultare nella comparsa di messaggi di warning o errore a schermo per alcuni utenti, limitandone quindi l’utilizzo. Seguire le indicazioni relative alla visualizzazione mappa 3D nativa di QGIS per poter eseguire comunque un layout con scena 2.5D.

## Per saperne di più

Dalla documentazione ufficiale:

* Operazioni di [**Clip** e **Merge**](https://docs.qgis.org/3.40/en/docs/training_manual/processing/cutting_merging.html) per raster.
* Operazioni di [**Terrain analysis**](https://docs.qgis.org/3.40/en/docs/training_manual/rasters/terrain_analysis.html) per raster DTM.