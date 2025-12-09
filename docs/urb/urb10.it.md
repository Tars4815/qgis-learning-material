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
