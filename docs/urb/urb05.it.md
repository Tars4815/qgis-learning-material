---
tags:
  - QGIS
  - Urbanistica
  - Vettoriali
  - Georeferenziazione
  - Vettorializzazione
---

# Georeferenziazione e vettorializzazione

## Scopo dell’esercizio

Georeferenziare una mappa del masterplan di MIND (Ex Area Expo 2015) e vettorializzare in formato shapefile le strade e gli edifici.

## Dati

Raster:

* *MIND_Masterplan* (progetto quartiere MIND ex Area EXPO Milano – Fonte: https://www.mindmilano.it/il-distretto/)
* *Legenda_masterplan* (codifica delle destinazione delle aree/edifici del quartiere MIND - Fonte: https://www.mindmilano.it/il-distretto/)

## Configurare la georeferenziazione

Definire le unità di misura e il percorso relativo: *Project > Properties > General Tab > Save paths > Relative*. Impostare il sistema di riferimento con codice EPSG: 32632 – WGS84 – UTM Zone 32 N.

Aggiungere la basemap di OpenStreetMap con il plugin **QuickMapServices** e zoommare sull’area [MIND in zona Rho Fiera](https://www.openstreetmap.org/node/11285728979).

Attivare la procedura di georeferenziazione in QGIS: *Layer > Georeferencer*. Nella nuova finestra è possibile selezionare il file della mappa scansionata che si vuole georiferire e definire le modalità di esecuzione dell’operazione:

* *File > Open Raster*: selezionare l’immagine del Masterplan.
* *Settings > Configure Georeferencer*: Spuntare sia l’opzione **Show IDs** per associare delle etichette identificative a vari punti omologhi che verranno inseriti, che la voce **Use map units if possible** per poter interpretare i valori di stima di errore nell’anteprima del plugin (avendo selezionato l’EPSG: 32632 saranno quindi metri). Flaggare anche **Show georeferencer window docked** se si vuole mantenere sempre visibile la finestra del Georeferencer all’interno della GUI di QGIS.
*	*Settings > Transformation settings*: in questa finestra vengono definite le modalità di trasformazione e associazione di coordinate al file in ingresso. È quindi estremamente importante assicurarsi di impostare un sistema di coordinate cartografiche adeguato e coerente a quello scelto per il progetto. Resampling method: *Nearest Neighbour*; Target SRS: EPSG:32632 – WGS84 / UTM Zone 32N, spuntare save GCPs points e scegliere le cartelle in cui salvare i file di reportistica sulla qualità dell’operazione.
* Alla voce *Transformation type*, per questo caso applicativo, selezionare l’opzione Polynomial 1.

### Le possibili trasformazioni

Nella tabella di seguito sono elencate con il loro significato le possibili trasformazioni da applicare in QGIS.

| Trasformazione   | Nome in QGIS    | Parametri       | Min # GCPs |
| ------ | ----- | ------- | -----|
|  | Linear | 2: due traslazioni (non applica una “trasformazione”, ma una semplice traslazione dell’immagine) | 2 |
| Affine conforme | Helmert  | 4: rotazione, due traslazioni, variazione di scala | 2 (ma è opportuno che siano almeno 3) |
| Affine generale | Polynomial 1 | 6: rotazione, due traslazioni, due variazioni di scala, “sbandamento” | 3 |
| Polinomiale di secondo ordine | Polynomial 2 | 12 parametri (non hanno un “significato geometrico”) | 6 |
| Omografia | Projective | 8: rotazione, due traslazioni, due variabili di scala, “sbandamento”, due “convergenze” | 4 |
| Rubber sheeting | Thin Plate Spline | 12 per ogni porzione della mappa (adattati localmente) | 10 (ma è opportuno che siano in numero maggiore) |

## Selezione dei punti omologhi

Prima di procedere, controllare nuovamente che il sistema di riferimento del progetto in QGIS sia quello scelto per la Lombardia.

L’obiettivo della procedura è identificare coppie di punti omologhi (Ground Control Points, GCPs) su entrambe le mappe e consentire la trasformazione che “posizionerà” la mappa del masterplan nel sistema di riferimento scelto. Elementi utili per la selezione dei GCPs sono solitamente rappresentati da spigoli di edifici, intersezioni di strade o angoli acuti su entità ben distinguibili su entrambe le mappe su cui si stanno “catturando” i punti omologhi. Attivare quindi la modalità di selezione dei punti:

* Dalla barra menù del georeferencer selezionare *Add point* > Cliccare con il tasto sinistro sul punto omologo individuato sul masterplan > Selezionare l’opzione *From Map Canvas* > Cliccare con il tasto sinistro nuovamente sul punto corrispondente individuato sulla basemap di OSM. Dopo aver completato questa operazione, un nuovo record associato al punto omologo inserito viene incluso nella tabella del georeferencer.
* Ripetere la procedura aggiungendo almeno 3 punti. Nel caso in cui si rilevino errori elevati nella tabella oppure errori grossolani dovuti all’individuazione errata di un punto, utilizzare i comandi *Delete point* o *Move GCP Point* presenti nel menù.
* Termina la procedura di selezione di punti omologhi, cliccare *Start georeferencer*.

## Vettorializzazione

Avviare la procedura di digitalizzazione delle strade visibili nella mappa creando un nuovo layer vettoriale:
* *Layer > Create Layer > New Shapefile Layer > File name:* “strade” > *Geometry type*: LineString > *SR*: EPSG:32632 – WGS 84 / UTM zone 32N
* Aggiungere nuovo campo > *Name*: “NOME” > *Type*: Text data > *Length*: 250 > *Add to Fields List*

Attivare modalità di editing e aggiungere nuovi elementi al vettore “strade”:
* Tasto destro sul layer “strade” > *Toggle editing*
* Attivare visualizzazione della barra del menù editing: *View > Toolbars > Flag su Digitizing Toolbar*
* Nella barra degli strumenti di digitalizzazione cliccare *Add Line Features*
*	Cliccare con il tasto sinistro sulla mappa in corrispondenza dei nodi della linea che si vuole digitalizzare come strada. Cliccare il tasto destro al termine della procedura. Nella finestra di pop up inserire le informazioni relative all’id numerico e al nome della strada e premere OK.
*	Al termine della vettorializzazione degli elementi di interesse, cliccare su *Salva Modifiche Vettore* nella Barra degli Strumenti di Digitalizzazione e disattivare il pulsante *Save Layer Edits*.

Mostrare modalità di editing vettoriale avanzato per agganciare elementi stradali in modo consistente:

* Attivare visualizzazione della barra del menù editing avanzato: *View > Toolbars > Flag su Snapping Toolbar*
*	Nella snapping toolbar, premere *Enable snapping* (Calamita), cliccare su *Vertex* e *Segment* nel menù a tendina da cui scegliere gli elementi a cui agganciarsi e definire una tolleranza di aggancio di 5 metri. In questo modo, ogni nuovo nodo aggiunto in editing che ricade a meno 5 metri da un nodo o un segmento già esistente verrà “agganciato” automaticamente all’elemento esistente.

Ripetere la vettorializzazione degli edifici e delle aree in modo analogo creando un apposito attributo che permetta di categorizzare gli elementi secondo la loro destinazione.
