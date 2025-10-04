---
tags:
  - QGIS
  - Urbanistica
  - Intro
  - Vettoriali
---
# Introduzione a QGIS

## Cos'è QGIS?

**QGIS** (un tempo noto come Quantum GIS) è un *Sistema di Informazione Geografica Libero e Open Source*. Il progetto è nato nel maggio del 2002. 
QGIS è un software GIS disponibile per chiunque possieda un pc con piattaforme di uso comune come macOS, Linux, UNIX, Microsft Windows e, sperimentalmente, Android. 
QGIS è rilasciato sotto la [*GNU General Public License (GPL)*](https://github.com/qgis/QGIS?tab=GPL-2.0-1-ov-file#readme) che rende possibile modificare il codice sorgente sviluppato nel linguaggio C++ e garantisce l’accesso a un programma GIS libero e privo di costi che si può liberamente modificare, seguendo indicazioni precise. 
È molto simile nell’interfaccia utente e nelle funzioni ai pacchetti GIS commerciali equivalenti. QGIS è mantenuto da un gruppo di sviluppatori volontari di una community che pubblicano una nuova versione ogni quattro mesi circa.

## Formato dati supportati da QGIS

- **Dati Vettoriali**: QGIS supporta pienamente il formato shapefile di ArcGIS, che pur essendo un formato proprietario rappresenta uno dei formati vettoriali pià diffusi e rilasciati in Italia; 
- **Dati raster**: QGIS supporta molti tipi di formati (ArcInfo Binary Grid, ArcInfo ASCII Grid, GeoTIFF, ecc.), alcuni solo in lettura, altri in lettura e scrittura;
- Connessioni a **database**: QGIS supporta un'ampia varietà di database spaziali, tra cui PostgreSQL/PostGIS, SpatiaLite (basato su SQLite), Oracle Spatial, Microsoft SQL Server (Spatial), MySQL e GeoPackage.

... e molto altro!

## Installazione

La versione da utilizzare per le esercitazioni è l’attuale **Long Term Release** (LTS, versione più stabile) 3.40.xx da scaricare nell’apposita pagina Downloads del sito del progetto: https://qgis.org/download/.

![Logo QGIS 3.40 LTR](../assets/img/qgis340logo.png)

QGIS 3.40 è l’edizione desktop del software. Esso permettere di interrogare, editare ed effettuare analisi spaziali sui dati geografici.

L’interfaccia di QGIS Desktop contiene:

1.	**Barra dei menù**: fornisce accesso alle varie funzioni di QGIS utilizzando menù a tendina 
2.	**Barra degli strumenti**: fornisce gli strumenti necessari per interagire con la mappa 
3.	**Layer**: regola la visibilità e la disposizione degli strati cartografici: quelli più in alto sono sovrapposti a quelli più in basso 
4.	**Area di visualizzazione**: rappresenta la cartografia relativa ai livelli vettoriali e raster selezionati nel gruppo «Layer» 
5.	**Barra di stato**: mostra le coordinate relative alla posizione del mouse, la scala di visualizzazione e il sistema di riferimento utilizzato 

![Interfaccia grafica utente di QGIS](../assets/img/GUI.png)

## Personalizzazione dell’interfaccia grafica

### Lingua del software

Di default al primo accesso al software, QGIS Desktop definirà come sua lingua di visualizzazione quella impostata dal sistema operativo di utilizzo. Per facilitare le indicazioni delle esercitazioni e il supporto a eventuali problemi con il software, per le esercitazioni è richiesto l’utilizzo di QGIS in inglese. In questo modo, per qualsiasi esigenza, sarà molto più semplice consultare l’ampia documentazione online in inglese a supporto degli utenti.

Nel caso in cui la lingua di sistema non sia già l’inglese, è necessario accedere alle impostazioni del software da *Impostazioni -> Opzioni -> Tab Generale*. Nella nuova finestra, spuntare il box *Sovrascrivi la lingua del sistema*.
Alla voce Traduzione interfaccia utente, dal menù a tendina selezionare *American English*. 
Alla voce Localizzazione (formati per numeri, date e valuta), dal menù a tendina selezionare *English United Kingdom (en_GB)*.

!!! note
    Queste impostazioni sono particolarmente importanti per la gestione dei valori numerici che in ambiente QGIS verranno quindi gestiti considerando il punto come separatore decimale.

Per finalizzare tutte le modifiche definite nella tabella *Opzioni > Generale* è richiesto il riavvio del software.

![Preferenze software per linguaggio](../assets/img/settings-language.png)

### Visibilità dei pannelli

Nel corso delle esercitazioni e di eventuali progetti futuri in ambienti QGIS, potrebbe essere necessaria l’attivazione di nuovi pannelli e finestre nella GUI oltre a quelli già attivi di default descritti in precedenza. Per poter controllare in base alle proprie necessità la visibilità dei vari pannelli, è necessario accedere al menù *View* nella Barra dei menù. Da qui e possibile attivare o disattivare i pannelli e/o le toolbar.

![Visibilità panels](../assets/img/view-panels.png)

![Visibilità toolbars](../assets/img/view-toolbars.png)

## Risorse utili

- **QGIS User Guide**: documentazione ufficiale delle funzionalità di QGIS Desktop. Link: https://docs.qgis.org/3.40/en/docs/user_manual/index.html (Ultimo accesso: 14/09/2025)
- **QGIS source code**: repository ufficiale del codice di QGIS contenente numerosi link a risorse utili (tutorial, guide etc.). Link: https://github.com/qgis/QGIS (Ultimo accesso: 14/09/2025)
- **QGIS Tutorials and Tips** di Ujaval Gandhi: sito che documenta una selezione variegata di esercizi guidati su possibili applicazioni di QGIS. Link: http://www.qgistutorials.com/it/ (Ultimo accesso: 14/09/2025)
- **Canale YouTube QGIS**: canale con raccolte di video tutorial, workshop e presentazioni legate a versioni di QGIS e sue funzionalità in progetti di vari ambiti. Link: https://www.youtube.com/@qgishome/video (Ultimo accesso: 14/09/2025)
