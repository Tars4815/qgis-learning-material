---
tags:
  - QGIS
  - Urbanistica
  - Vettoriali
  - OpenStreetMap
  - Servizi Web
  - WMS
  - WFS
---

# Risorse online: download dati OpenStreetMap, risorse e servizi web

## Scopo dell’esercizio

Individuare aree dismesse sul territorio della città di Milano, confrontare diverse fonti di dati e valutare le stazioni collocate nei pressi di tali aree.

## Dati

Vettoriali (da scaricare durante l’esercizio):
*	*Rete metropolitana ATM di Milano* (fonte: OpenStreetMap)
* *Stazioni reti metropolitana *(fonte: OpenStreetMap)
* *Aree dismesse “brownfield”, “greenfield”, “abandoned”* (fonte: OpenStreetMap)

Servizi web OGC:
* *Aree dismesse Lombardia* (Web Feature Service – Fonte: [Geoportale Regione Lombardia](https://www.geoportale.regione.lombardia.it/it/metadati?p_p_id=detailSheetMetadata_WAR_gptmetadataportlet&p_p_lifecycle=0&p_p_state=normal&p_p_mode=view&_detailSheetMetadata_WAR_gptmetadataportlet_identifier=r_lombar%3A37d5d480-ef27-44e4-acc3-9ab924786018&_jsfBridgeRedirect=true)), Link: https://www.cartografia.servizirl.it/arcgis2/services/ambiente/aree_dismesse/MapServer/WFSServer?_jsfBridgeRedirect=true
* *Aree della rigenerazione Lombardia* (Web Map Service – Fonte: [Geoportale Regione Lombardia](https://www.geoportale.regione.lombardia.it/metadati?p_p_id=detailSheetMetadata_WAR_gptmetadataportlet&p_p_lifecycle=0&p_p_state=normal&p_p_mode=view&_detailSheetMetadata_WAR_gptmetadataportlet_identifier=r_lombar%3A0ab5a341-8535-4e5a-a038-6103b4b4a194&_jsfBridgeRedirect=true)), Link: https://www.cartografia.servizirl.it/arcgish/services/ambiente/AreeDismesse_read/MapServer/WMSServer?request=GetCapabilities&service=WMS&_jsfBridgeRedirect=true


## Download dati di OpenStreetMap

Definire le unità di misura e il percorso relativo: *Project > Properties > General Tab > Save paths > Relative*. Impostare il sistema di riferimento con codice EPSG: 32632 – WGS84 – UTM Zone 32 N.

Aggiungere la basemap di OSM Standard con il plugin **QuickMapServices**. Questo tipo di layer che viene semplicemente selezionato da una serie di map provider attraverso l’estensione di QGIS è già un esempio di Web Map Service (WMS) poiché dietro all’operazione di selezione dalla lista risiede un link che permette di instaurare una connessione con il server OSM su cui sono esposti i servizi web OGC, tra cui quello della mappa di base di OpenStreetMap Standard in sola visualizzazione. Quindi, alla richiesta dell’utente in QGIS che ha definito un certo livello di zoom e una specifica estensione territoriale nel suo map canvas, viene inviata in risposta la semplice immagine dei dati di OSM come WMS su cui non è possibile eseguire le tipiche elaborazioni e analisi che si possono svolgere su dati vettoriali. Come si può quindi accedere a tali dati interrogandoli e filtrandoli direttamente dal database del servizio?

Per poter effettuare il download è necessario installare il plugin **QuickOSM**. Dopo averlo installato, avviarlo dal menù *Vector > QuickOSM > QuickOSM*. Al primo avvio sarà richiesto di accettare le condizioni legate alla licenza dei dati di OSM e alla loro attribuzione alla comunità di mappatori ([Open Data Commons Open Database License](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://opendatacommons.org/licenses/odbl/&ved=2ahUKEwjJhIPprpWQAxUlg_0HHceSIdsQFnoECB8QAQ&usg=AOvVaw0MkdT-SoLQy6cR7xDloxVh)).

Nella scheda Preset del plugin sono inclusi alcuni “pacchetti di queries” preconfezionati. Per esempio, il preset Urban include tutte le definizioni di query su dati OpenStreetMap legati alla mappatura tematica di ambienti cittadini, in particolare edifici e strade. Utilizzando la modalità di download con preset predefiniti come risultato direttamente caricato nel map canvas si avranno gli elementi geografici associati al preset presenti nel database e visualizzati con la stessa simbologia di OSM standard.

Le principali funzionalità del plugin, tuttavia, sono incluse nella sezione *Quick query* dove un’interfaccia semplificata permette di costruire a blocchi la query personalizzata al database. Nello specifico, in questa sezione è possibile elencare le combinazioni di *tag* – composti da combinazioni di *key* e *value* – che nello schema del database di OpenStreetMap definiscono le entità di nostro interesse.

Come individuare questi tags? Ogni informazione legata a tag approvati e/o adottati de facto dalla comunità di mappatori di OSM è documentata – anche in questo caso in modo collaborativo – sull’enciclopedia di [WikiOSM](https://wiki.openstreetmap.org/), dove è possibile trovare anche tutte le regole condivise sulle geometrie di OSM (*nodes*, *ways* e *relations*) che possono essere mappate con certi tag. Dopo aver definito una o più query sugli elementi di interesse, il plugin convertirà l’elenco definito nell’interfaccia in una richiesta tramite il servizio di OverpassTurbo.

Per esempio, per scaricare i dati relativi alle linee metropolitane di Milano e alle sue fermate è necessario individuare i tag appropriati per poter compilare la lista. Nello specifico, le linee vengono mappate come relations con il tag *route=subway* mentre le stazioni vengono mappate come nodes con il tag *station=subway*. Dopo aver definito la richiesta con operatore logico e definito come area di ricerca “In Milano”, cliccare *Run query*: il risultato verrà caricato in automatico nel map canvas del progetto.

Maggiori info sulla mappatura delle linee metropolitane in OSM: https://wiki.openstreetmap.org/wiki/Metro_Mapping

N.B: Nel caso in cui dovesse comparire l’errore Overpass API, controllare la stabilità della propria connessione internet oppure, nella sezione Advanced, definire un valore maggiore di 25 per il parametro timeout.

> **N.B.**: Nel caso in cui dovesse comparire l’errore Overpass API, controllare la stabilità della propria connessione internet oppure, nella sezione Advanced, definire un valore maggiore di 25 per il parametro timeout.

![Pannello Quick Query di QuickOSM](../assets/img/urb/quickosm-subway.png)


Nel layer di punti scaricati, selezionare per creare un nuovo layer solo quelli associati al tag *station=subway*. In risposta alla query, infatti, verranno scaricati anche tutti gli snodi metropolitani delle varie linee non necessariamente associati a una stazione accessibile.

Controllare quindi il sistema di riferimento in cui sono inquadrati i layer appena scaricati, proiettarli e salvarli permanentemente come file locali nella propria cartella di progetto (Attenzione: se non verranno salvati, alla chiusura del progetto verranno cancellati dalla memoria poiché tali layer vengono scaricati solo come vettori temporanei).

Categorizzare la simbologia delle linee metropolitane per denominazione (tag [ref](https://wiki.openstreetmap.org/wiki/Key:ref)). Categorizzare la simbologia delle stazioni per accessibilità (tag [wheelchair](https://wiki.openstreetmap.org/wiki/Key:wheelchair)).

Ripetere queste operazioni di ricerca per i tag associati alle aree dismesse/abbandonate/in via di riqualificazione in OpenStreetMap:
* *[landuse = brownfield](https://wiki.openstreetmap.org/wiki/Tag:landuse%3Dbrownfield)*
* *[landuse = greenfield](https://wiki.openstreetmap.org/wiki/Tag:landuse%3Dgreenfield)*
* *[landuse = construction](https://wiki.openstreetmap.org/wiki/Tag:landuse%3Dconstruction)*
* *[abandoned = yes](https://wiki.openstreetmap.org/wiki/Key:abandoned:*)*

Definire gli operatori logici come nell’immagine attivando anche l’opzione *Metadata* nella sezione *Advanced*:

![Pannello Quick Query di QuickOSM](../assets/img/urb/quickosm-landuse.png)

Aprire la tabella attributi del layer poligonale risultante e valutare le informazioni sulla data di ultimo aggiornamento dei record scaricati.

Individuare le aree dismesse strategiche a 200 metri dalle stazioni della metropolitana. Questa operazione può essere svolta sfruttando l’operazione di buffer come nell’esercitazione [QGIS03](urb04.it.md), oppure sfruttando il tool dal menù *Vector > Research Tools > Select within distance…*. Nella nuova schermata definire *Select features from:* layer delle aree dismesse di OSM, *By comparing to the features from:* layer delle stazioni della metropolitana; *Where the features are within:* 200 metri. Eseguire la selezione.

## Connessione a servizi web OGC

Come e quanto sono tuttavia affidabili i dati di OSM in merito alle aree dismesse?

Per poter valutare questo aspetto in maniera speditiva è possibile realizzare una valutazione comparativa tra il dataset OSM (di tipo Volunteered Geographic Information) con i dati ufficiali della Regione Lombardia (di tipo autoritativo).

Caricare quindi il WMS di Regione Lombardia delle aree di Rigenerazione (aggiornamento 2008-2010). Menù *Layer > Data Source Manager > Tab WMS/WMTS*. Cliccare quindi su New e definire la connessione al servizio OGC con un nome significativo a piacere e copiando nel box URL il link del servizio indicato nella scheda del WMS sul sito del geoportale. Quindi cliccare *OK* e *Connect*.

La visualizzazione del nuovo layer WMS caricato nel progetto si ricaricherà ogni volta che verrà cambiata l’estensione e lo zoom del map canvas tramite connessione internet. Si tratta di una semplice immagine statica. Gli elementi visibili, quindi, non sono né filtrabili né interrogabili. Per poter fare un confronto con il dataset con una selezione per posizione serve accedere a un servizio WFS.

Per caricare il servizio WFS delle aree dismesse (aggiornamento 2008-2010), accedere al menù *Layer > Data Source Manager > Tab WFS/OGC API Features *e creare una nuova connessione in modo analogo a quanto fatto in precedenza per il WMS.

Il layer WFS caricato, a differenza del WMS, ha una sua tabella attributi che può essere interrogata ed esplorata in modalità lettura. Non possono quindi essere realizzate direttamente sulla sorgente sul dato operazioni di scrittura ma possono solo essere generati campi “virtuali” attraverso il Field Calculator. Filtrare in visualizzazione quindi i dati relativi al solo comune di Milano: tasto destro sul layer *> Filter…*

Individuare quindi con una selezione per posizione le aree dismesse presenti sia nel dataset OSM che nel dataset di Regione Lombardia.

Salvare il progetto.

[...]