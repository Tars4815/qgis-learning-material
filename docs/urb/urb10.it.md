---
tags:
  - QGIS
  - Urbanistica
  - Raster
  - Vettoriali
  - Clip
  - Raster calculator
---

# Analisi con raster e vettoriali

## Scopo dell’esercizio

Utilizzare dati raster in ambiente GIS; convertire dati da vettoriali a raster; realizzare una carta delle aree a bosco in Alta Valtellina e calcolare la superficie di bosco di conifere esboscabile.

## Dati

### Vettoriali

* *Comunita_montane_2016* (File shapefile dei confini amministrativi delle comunità montane della provincia di Sondrio - Fonte: [Geoportale Lombardia](https://www.geoportale.regione.lombardia.it/en-GB/metadati?p_p_id=detailSheetMetadata_WAR_gptmetadataportlet&p_p_lifecycle=0&p_p_state=normal&p_p_mode=view&_detailSheetMetadata_WAR_gptmetadataportlet_identifier=r_lombar:0e3f85ec-6494-407b-a6d4-66ff9ea74bd4))

* *Strade_statali* (File shapefile dei tratti stradali di rilevanza statale per la Provincia di Sondrio - Fonte: [Geoportale Lombardia](https://www.geoportale.regione.lombardia.it/en-GB/metadati?p_p_id=detailSheetMetadata_WAR_gptmetadataportlet&p_p_lifecycle=0&p_p_state=normal&p_p_mode=view&_detailSheetMetadata_WAR_gptmetadataportlet_identifier=r_lombar%3A3417cfea-5192-467e-a388-947bdd7a85f2&_jsfBridgeRedirect=true))

* *Strade_provinciali* (File shapefile dei tratti stradali di rilevanza provinciale per la Provincia di Sondrio – Fonte: [Geoportale Lombardia](https://www.geoportale.regione.lombardia.it/en-GB/metadati?p_p_id=detailSheetMetadata_WAR_gptmetadataportlet&p_p_lifecycle=0&p_p_state=normal&p_p_mode=view&_detailSheetMetadata_WAR_gptmetadataportlet_identifier=r_lombar%3A3417cfea-5192-467e-a388-947bdd7a85f2&_jsfBridgeRedirect=true))

### Raster

* *class_bosco* (Raster tiff con la classificazione delle aree boschive della Valtellina - Fonte: Geoportale Lombardia)

* *orto3* (Raster tiff con ortofoto dell’Alta Valtellina - Fonte: Geoportale Lombardia)

## Istruzioni per l'esecuzione

### Preparazione dati

Definire le unità di misura e il percorso relativo: *Project > Properties > General Tab > Save paths > Relative*. Impostare il sistema di riferimento con codice EPSG: 32632 – WGS84 – UTM Zone 32 N.

Caricare nella mappa i layer vettoriali delle strade statali e provinciali della provincia di Sondrio, il layer vettoriale con i confini delle comunità montane della Lombardia, il raster con la classificazione delle aree boschive della provincia di Sondrio, l’ortofoto dell’Alta Valtellina. Controllarne informazioni e caratteristiche per verificarne la consistenza con i requisiti di progetto.

Eseguire una query per attributo sul layer vettoriale delle comunità montane per selezionare la comunità montana denominata “ALTA VALTELLINA” ed esportarla in un nuovo layer vettoriale.
Ritagliare i 2 layer vettoriali delle strade statali e provinciali con il poligono della comunità montana dell’Alta Valtellina appena esportato.

### Classificazione delle tipologie boschive

Ritagliare il raster con la classificazione delle aree boschive *class_bosco.tif* con il poligono della comunità montana dell’Alta Valtellina. Ridefinire la simbologia per il raster appena ritagliato (*class_bosco_Alta_Valtellina.tif* secondo estensione della comunità montana in analisi) utilizzando la legenda fornita.

| Valore pixel   | Significato    | 
| ------ | ----- | 
| 1 | No info |
| 2 | Conifere | 
| 3 | Latifoglie | 
| 4 | Boschi misti |

### Filtro buffer delle strade

Fare un merge fra i due layer vettoriali delle strade, creando un nuovo layer vettoriale che contiene tutti i tratti stradali dei due layer di partenza: *Vector > Geoprocessing Tools > Union.*

Creare un buffer di 400 m attorno al layer delle strade unito, appena creato.

Aggiungere un attributo (campo numerico) nella TA del layer vettoriale con il buffer appena creato ed inserire il valore 1 in quella cella con il Field calculator.

Convertire il layer vettoriale (di poligoni) con i buffer delle strade in un raster di risoluzione 50x50 metri.

### Individuazione delle aree di diboscamento

Con l’aiuto del *Raster calculator*, creare una maschera booleana (raster in cui i pixel possono assumere solo valori 0 o 1) , in cui il valore 1 sarà attribuito ai pixel classificati come boschi di conifere: “classraster = 2”.

Moltiplicare la maschera booleana appena creata per il raster creato a partire dal buffer attorno alle strade, utilizzando ancora il *Raster Calculator*. Ripetere le operazioni del punto precedente.

Calcolare la superficie di conifere esboscabile comprese nel buffer di 400 m attorno alle strade con gli strumenti di *Raster analysis*.

## Per saperne di più

Dalla documentazione ufficiale:

* // UNDER CONSTRUCTION //
