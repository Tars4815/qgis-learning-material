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


[UNDER CONSTRUCTION]
