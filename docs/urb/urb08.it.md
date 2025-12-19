---
tags:
  - QGIS
  - Urbanistica
  - Vettoriali
  - Interpolazione
  - Inverse Distance Weighting
  - Spline
---

# Interpolazione e aree di influenza

## Scopo dell’esercizio

Applicare algoritmi di interpolazione in ambiente GIS; stabilire le zone di rischio rumore sulla base dei dati misurati nel Comune di Modena.

## Dati

Vettoriali:
* *zonizzacu* (Layer shapefile della zonizzazione acustica del comune di Modena)

Tabelle:
* *RUMORE_MIS* (File txt dati di rumore misurato in posizioni puntuali)

## Preparazione del progetto

Definire le unità di misura e il percorso relativo: *Project > Properties > General Tab > Save paths > Relative*. Impostare il sistema di riferimento con codice EPSG: 25832 – ETRS89 – UTM Zone 32 N.

Caricare i dati di rumore misurato in posizioni puntuali con modalità equivalenti a quelle dei file csv.

Cambiare la simbologia del layer con le misure di rumore in una visualizzazione graduata.

## Calcolo modelli di interpolazione

Ricavare una mappa interpolata del rumore nel Comune di Modena a partire dai valori puntuali misurati, usando diverse tecniche:
1.	**Inverse Distance Weighting** (*Interpolation > IDW Interpolation*)
2.	**Triangulated Irregular Network** (*Interpolation > TIN Interpolation*)

### Inverse Distance Weighting

Da *Processing Toolbox > Interpolation > IDW Interpolation*. Definire come layer da interpolare quello delle misure puntuali di rumore e scegliere come campo da considerare per l’operazione (Interpolation attribute) *RUM_DB*. Confermare queste impostazioni cliccando sull’icona +.

Scegliere come *Distance coefficient p* il valore 2 (potenza applicata alla distanza inversa), definire come *Extent* quella del layer della zonizzazione acustica e come Pixel size 25 metri. Lanciare il processamento e ripeterlo con diverse combinazioni di potenze (e.g. 0.5, 4…) e pixel (e.g. 10, 50 metri…). Come cambia il raster risultante?

### Triangulated Irregular Network

Da *Processing Toolbox > Interpolation > TIN Interpolation*. Definire come layer da interpolare quello delle misure puntuali di rumore e scegliere come campo da considerare per l’operazione (Interpolation attribute) *RUM_DB*. Confermare queste impostazioni cliccando sull’icona +.

Scegliere come Interpolation method il valore Linear, definire come *Extent* quella del layer della zonizzazione acustica e come *Pixel size* 25 metri. Lanciare il processamento e ripeterlo con diverse combinazioni di metodi (Linear o Cubic) e pixel (e.g. 10, 50 metri…). Come cambia il raster risultante?

## Validazione modello e calcolo errore di modello

Per valutare la qualità del modello interpolato, ho necessità di avere un campione di dati di validazione: dalla *Processing Toolbox > Vector selection > Random selection*. Selezionare come input layer lo shapefile delle misure puntuali. Come *Method*, definire *Percentage of selected features* e definire come Percentage 70%. Salvare in un nuovo layer “training” i record selezionati. Invertire la selezione e salvare il subset complementare come layer “validation”.

Ripetere la procedura di interpolazione con IDW e TIN usando unicamente il campione dei dati di “training”.

In corrispondenza dei punti del campione di validazione, estrarre il valore stimato dai modelli interpolati: *Processing Toolbox > Raster analysis > Sample raster values*. Scegliere come input il layer di validazione, come raster uno dei raster interpolati e definire il nome del nuovo campo (*Output column prefix*) per salvare il valore nel pixel del raster in cui ricade ciascun punto (e.g. IDW_val, TIN_val in base al raster su cui si sta effettuando il campionamento). Ripetere il procedimento per entrambi i raster interpolati.

Nel layer di validazione contenente i valori campionati derivati dalle due interpolazioni eseguite, accedere al *Field calculator* e calcolare le differenze tra i valori stimati con i due metodi e il valore osservato in corrispondenza di ciascun punto, creando di conseguenza due nuovi campi. Dei due nuovi campi ottenuti, calcolarne le statistiche (*Processing Toolbox > Vector analysis > Basic statistics for fields*).

## Analisi misurazioni suono a Modena

Confrontare il rumore effettivamente misurato con quello considerato massimo accettabile in modo da individuare le zone caratterizzate da disagio acustico.

Convertire lo shapefile zonizacc in raster per renderlo confrontabile con i risultati delle interpolazioni: *Processing toolbox > GDAL > Vector conversion > Rasterize (Vector to raster)*. *Input layer*: zonizacc; *Field to use for a burn-in value*: maxdBa; *Output raster size*: Georeferenced units > Definire di seguito la dimensione coerente con quella scelta per i raster delle interpolazioni. Avviare la procedura.

Determinare le zone di disagio acustico sulla base del raster ottenuto con interpolazione tramite IDW o TIN. *Menù Raster > Raster calculator*. Output layer: definire nome e cartella di salvataggio; nel box *Raster calculator* expression definire la formula della differenza tra *(rumore misurato [raster interpolato]) – (rumore max accettabile [raster della zonizzazione])*.

Ancora con il Raster Calculator: (risultato del calcolo prec.) > 10 dBa. Si ottiene così il raster del disagio acustico (considerare una tolleranza di 5 dBa oppure 10 dBa).

Calcolare la percentuale del comune di Modena interessata dal disagio acustico. Ricavare il numero di celle con disagio: *Processing toolbox > Raster analysis > Raster layer unique values*. Scegliere come input l’ultimo raster calcolato. L’html risultante conterrà sia per le aree che rispettano che quelle che non rispettano la tolleranza (1 o 0) il totale calcolato per la superficie. Calcolare quindi la percentuale di quelle che non rispettano i limiti di tolleranza.
