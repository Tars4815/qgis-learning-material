# QGIS 01

## Vector Data

[...]

### Es01 - Project management, data format and join operation

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

### Es02 - Join, query standard e georeferenziate

*Scopo dell'esercizio*: calcolo del bacino di utenza (numero di abitanti) di un parco urbano

**Dati**

Shapefile:

- Parchi (parchi del comune di Modena)

- Censim (zone di censimento del comune di Modena)

Tabelle:

- serv97.dbf (nomi dei parchi)

- sez.dbf (informazioni su zone di censimento)

Settare le unità di misura e il percorso relativo: ***Project > Properties > General***

Caricare lo shapefile *Parchi*: ***Layer > Add Layer***

Caricare la tabella *serv97.dbf*: ***Drag and Drop***

Join tra *Parchi* e *serv97.dbf* (join 1:1) – le tabelle non vengono unite fisicamente in un unico file, ma solo logicamente all’interno del progetto: ***Tasto dx su Parchi > Properties > Joins (Codice)***

Caricare lo shapefile *Censim* e porlo in secondo piano.

Aprire tabella degli attributi associata a *Censim* e mostrare la necessità di collegare un’altra tabella (la tabella contiene solo il numero della sezione di censimento, ma non gli attributi ad essa associati, come per esempio il numero di abitanti). ***Tasto dx su Censim > Open Attribute Table***

Caricare la tabella *sez.dbf*. Join tra attributi di *Censim* e *sez.dbf* (mostrare che alcune zone di censimento non hanno dati perché la tabella *sez.dbf* è riferita alle vecchie sezioni di censimento (1991), mentre lo shapefile *Censim* descrive le nuove sezioni che sono in numero maggiore).

Campire il layer *Censim* in base al numero di abitanti (5 classi: <50, 50-100, 100-200, 200-500, >500): ***Tasto dx su Censim > Properties > Style: Graduated; Column: sez_NUMABT***

Calcolare la densità di abitanti per ogni sezione di censimento; rappresentare il layer Censim in base al nuovo campo creato.

Query su Parco Ferrari: ***Tasto dx su Parchi > Open Attribute Table > Select features using an expression (ε)***

Query georeferenziata sulle zone di censimento a 200 m dal parco Ferrari:

-	***Vector > Geoprocessing tools > Buffer***

-	***Vector > Research tools > Select by location***

Calcolare il numero di abitanti a 200 m dal parco Ferrari:

-	***Tasto dx su Censim > Open Attribute Table > Toggle editing mode (matita) > Open Field Calculator***

-	***Create a new field***

-	***Output field name:*** ABT_TOT

-	***Lista delle Funzioni > Fields and values > sez_NUMABT***

-	Clic su Matita per uscire da modalità di editing > ***Save***

(NOTA: Modificare i valori NULL in 0)

-	***Vector > Analysis Tools > Basic Statistics for Fields***

-	***Input Layer:*** Censim; ***Field to calculate statistics on:*** ABT_TOT

Creare un layout: ***Project > New print layout > Add Map, Add Legend, ecc*** (deve essere selezionata l’area sul foglio)


