# QGIS 01

## Dati vettoriali

[...]

### Es01 - Gestione progetto, formato dati e join

*Scopo dell'esercizio*: visualizzare i casi COVID registrati a marzo 2020 in Italia

**Dati**

Shapefile:

- ProvCM01012019_g_WGS84 (limiti provinciali italiani ISTAT del 2019)

- Reg01012019_g_WGS84 (limiti regionali italiani ISTAT del 2019)

Tabelle:

- dpc-covid19-ita-province-20200319.csv (report casi COVID in Italia al 19 marzo 2020 a livello provinciale)

Settare le unità di misura e il percorso relativo: ***Project > Properties > General tab > Save paths > Relative***

Caricare il file *“dpc-covid19-ita-province-20200319.csv”* e visualizzare la tabella attributi (TA): ***Layer > Add layer > Add Delimited Text Layer, File Format > CSV, Geometry Definition – Point coordinates: X field > long, Y field > lat, Geometry CRS > EPSG:4326 – WGS 84***.

Esportare i dati in un nuovo shapefile: tasto destro sul layer > ***Export > Save features as***, Format: ESRI shapefile, cliccare sull’icona con … e scegliere il percorso in cui salvare il nuovo shapefile con il nome: *“prov_covid_20200319.shp”*.

Proiettare i dati nel sistema cartografico UTM, fuso 32 N: ***Vector > Data Management Tools > Reproject Layer, Target CRS: EPSG:32632 – WGS 84 / UTM Zone 32N***, Riproiettato: “prov_covid_20200319_UTM.shp”.

Settare il sistema di riferimento del progetto: ***Project > Properties > CRS > EPSG:32632 – WGS 84 / UTM Zone 32N***

Pulizia dei dati.  Controllare ed eventualmente rimuovere dallo shapefile “prov_covid_20200319_UTM” le province “In fase di definizione/aggiornamento”:

- Tasto destro sul layer > ***Zoom to layer***
- Tasto destro sul layer > ***Toggle editing***
- Nella toolbar attiva il comando ***Select Features > Selezionare l’entità punto localizzata fuori dai confini***
- Tasto destro sul layer > ***Open Attribute Table > Delete selected features***
- Salva modifiche; Disattiva pulsante “Toggle editing”

Installare il plugin **QuickMapServices** per aggiungere una basemap al progetto:

- ***Plugins > Manage and Install Plugins > Digitare e cercare il plugin di interesse > Install Plugin***
- Abilitare l’accesso ad una più ampia gamma di basemap: ***Web > QuickMapServices > Settings > More services > Get contributed packs***
- Aggiungere una basemap al progetto: ***Web > QuickMapServices > OpenStreetMap Standard***

Caricare i confini amministrativi ISTAT (*ProvCM01012019_g_WGS84.shp*, *Reg01012019_g_WGS84.shp*) e mostrare la tabella attributi.

Campire lo shapefile *Reg01012019_g_WGS84.shp* evidenziando ogni regione con un colore diverso (la visualizzazione può essere personalizzata a piacere):

- Tasto destro sul layer > ***Properties > Symbology > Categorized > Value = COD_REG > Classify***

Mostrare le etichette con il nome delle regioni (il fonte e la posizione sono personalizzabili a piacere):

- Tasto destro sul layer > ***Properties > Labels > Single Labels > Value = DEN_REG***

Join tra tabella attributi di “*ProvCM01012019_g_WGS84*” e “*prov_covid_20200319_UTM*” – Le tabelle non vengono unite “fisicamente” in unico file ma solo logicamente all’interno del progetto.

- Tasto destro su “*ProvCM01012019_g_WGS84*” > ***Properties > Joins > + > Join layer: prov_covid_20200319_UTM > Join field: codice_pro > Target field: COD_PROV***

Evidenziare query per individuare province con più di 200 casi:

- Tasto destro su “ProvCM01012019_g_WGS84” > ***Open attribute table > Select features using an expression > Inserire espressione: "prov_covid_20200319_UTM_totale_cas" > 200***

Cambiare simbologia per evidenziare situazione COVID a livello provinciale:

- Tasto destro su “ProvCM01012019_g_WGS84” > ***Symbology > Graduated > Value = prov_covid_20200319_UTM_totale_cas > Mode: Natural Breaks (Jenks) > Classify***

Creare un layout: ***Project > New print layout > Add Map, Add Legend, ecc.*** (deve essere selezionata l’area sul foglio)