---
title: Configurazione di ContextHub
description: Scopri come configurare Context Hub.
exl-id: 1fd7d41e-31ad-4838-8749-a5791edcfd63
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 2%

---

# Configurazione di ContextHub {#configuring-contexthub}

ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali. Per maggiori dettagli su ContextHub, consulta la sezione [Panoramica per gli sviluppatori ContextHub](contexthub.md).

Puoi configurare la barra degli strumenti di ContextHub per controllare se viene visualizzata in modalità Anteprima, per creare archivi ContextHub e aggiungere moduli di interfaccia utente.

## Mostrare e nascondere l’interfaccia utente di ContextHub {#showing-and-hiding-the-contexthub-ui}

Configura il servizio Adobe ContextHub OSGi per mostrare o nascondere il [Interfaccia utente ContextHub](/help/sites-cloud/authoring/personalization/targeted-content.md) sulle tue pagine. Il PID di questo servizio è `com.adobe.granite.contexthub.impl.ContextHubImpl.`

Per configurare il servizio è possibile utilizzare [Console web](/help/implementing/deploying/configuring-osgi.md) o utilizza un nodo JCR nell&#39;archivio:

* **Console Web:** Per visualizzare l’interfaccia utente, seleziona la proprietà Mostra interfaccia utente . Per nascondere l’interfaccia utente, deselezionare la proprietà Nascondi interfaccia utente .
* **Nodo JCR:** Per visualizzare l’interfaccia utente, imposta il valore booleano `com.adobe.granite.contexthub.show_ui` proprietà di `true`. Per nascondere l’interfaccia utente, imposta la proprietà su `false`.

Quando mostra l’interfaccia utente di ContextHub, questa viene visualizzata solo sulle pagine AEM istanze dell’autore. L’interfaccia utente non viene visualizzata sulle pagine delle istanze di pubblicazione.

## Aggiunta di modalità e moduli dell’interfaccia utente di ContextHub {#adding-contexthub-ui-modes-and-modules}

Configura le modalità e i moduli dell’interfaccia utente visualizzati nella barra degli strumenti di ContextHub in modalità Anteprima:

* Modalità interfaccia utente: Gruppi di moduli correlati
* Moduli: Widget che espongono i dati contestuali da un archivio e consentono agli autori di manipolare il contesto

Le modalità di interfaccia utente vengono visualizzate come una serie di icone sul lato sinistro della barra degli strumenti. Quando è selezionata questa opzione, i moduli di una modalità di interfaccia utente vengono visualizzati a destra.

![Barra degli strumenti di ContextHub](assets/contexthub-toolbar.png)

Le icone sono riferimenti dal [Libreria di icone dell’interfaccia utente Coral](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### Aggiunta di una modalità di interfaccia utente {#adding-a-ui-mode}

Aggiungi una modalità di interfaccia utente per raggruppare i moduli ContextHub correlati. Quando crei la modalità di interfaccia utente, fornisci il titolo e l’icona visualizzati nella barra degli strumenti di ContextHub.

1. Nella barra degli Experienci Manager, tocca o fai clic su Strumenti > Siti > Context Hub.
1. Tocca o fai clic sul contenitore di configurazione predefinito.
1. Tocca o fai clic su Configurazione Context Hub.
1. Tocca o fai clic sul pulsante Crea , quindi tocca o fai clic su Modalità interfaccia utente di Context Hub .

   ![Modalità Aggiungi interfaccia](assets/contexthub-ui-mode.png)

1. Immetti i valori per le seguenti proprietà:

   * Titolo modalità interfaccia utente: Titolo che identifica la modalità di interfaccia utente
   * Icona modalità: Il selettore per [Icona dell’interfaccia utente Coral](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) per utilizzare, ad esempio `coral-Icon--user`
   * Abilitato: Seleziona per visualizzare la modalità di interfaccia utente nella barra degli strumenti di ContextHub

1. Tocca o fai clic su Salva.

### Aggiunta di un modulo dell’interfaccia utente {#adding-a-ui-module}

Aggiungi un modulo dell’interfaccia utente ContextHub a una modalità dell’interfaccia utente in modo che venga visualizzato nella barra degli strumenti di ContextHub per visualizzare l’anteprima del contenuto della pagina. Quando aggiungi un modulo di interfaccia utente, stai creando un&#39;istanza di un tipo di modulo registrato con ContextHub. Per aggiungere un modulo di interfaccia utente, è necessario conoscere il nome del tipo di modulo associato.

AEM fornisce un tipo di modulo di interfaccia utente di base e diversi tipi di moduli di interfaccia utente di esempio su cui è possibile basare un modulo di interfaccia utente. La tabella seguente fornisce una breve descrizione di ciascuna di esse. Per informazioni sullo sviluppo di un modulo di interfaccia utente personalizzato, consulta [Creazione di moduli di interfaccia utente ContextHub](extending-contexthub.md#creating-contexthub-ui-module-types).

Le proprietà del modulo dell’interfaccia utente includono una configurazione dettagliata in cui è possibile fornire valori per proprietà specifiche del modulo. Fornisci la configurazione dei dettagli in formato JSON. La colonna Tipo di modulo nella tabella fornisce collegamenti a informazioni sul codice JSON richiesto per ciascun tipo di modulo di interfaccia utente.

| Tipo modulo | Descrizione | Store |
|---|---|---|
| [contexthub.base](sample-modules.md#contexthub-base-ui-module-type) | Un tipo di modulo di interfaccia utente generico | Configurata nelle proprietà del modulo dell’interfaccia utente |
| [contexthub.browserinfo](sample-modules.md#contexthub-browserinfo-ui-module-type) | Visualizza informazioni sul browser | `surferinfo` |
| [contexthub.datetime](sample-modules.md#contexthub-datetime-ui-module-type) | Visualizza informazioni su data e ora | `datetime` |
| [contexthub.location](sample-modules.md#contexthub-location-ui-module-type) | Visualizza la latitudine e la longitudine del client, nonché la posizione su una mappa. Consente di modificare la posizione. | `geolocation` |
| [contexthub.screen-orientation](sample-modules.md#contexthub-screen-orientation-ui-module-type) | Visualizza l’orientamento dello schermo del dispositivo (orizzontale o verticale) | `emulators` |
| [contexthub.tagcloud](sample-modules.md#contexthub-tagcloud-ui-module-type) | Visualizza statistiche sui tag pagina | `tagcloud` |
| [granite.profile](sample-modules.md#granite-profile-ui-module-type) | Visualizza le informazioni del profilo per l’utente corrente, tra cui `authorizableID`, `displayName` e `familyName`. Puoi modificare il valore di `displayName` e `familyName`. | `profile` |

1. Nella barra degli Experienci Manager, tocca o fai clic su Strumenti > Siti > ContextHub.
1. Tocca o fai clic sul contenitore di configurazione a cui desideri aggiungere un modulo di interfaccia utente.
1. Fai clic o digita la configurazione ContextHub alla quale desideri aggiungere il modulo dell’interfaccia utente.
1. Tocca o fai clic sulla modalità di interfaccia a cui stai aggiungendo il modulo di interfaccia utente.
1. Tocca o fai clic sul pulsante Crea , quindi tocca o fai clic sul modulo dell’interfaccia utente ContextHub (generico).

   ![Modulo dell’interfaccia utente ContextHub](assets/contexthub-ui-module.png)

1. Immetti i valori per le seguenti proprietà:

   * Titolo modulo interfaccia utente: Titolo che identifica il modulo dell’interfaccia utente
   * Tipo di modulo: Tipo di modulo
   * Abilitato: Seleziona per visualizzare il modulo dell’interfaccia utente nella barra degli strumenti di ContextHub

1. (Facoltativo) Per ignorare la configurazione predefinita dell’archivio, immetti un oggetto JSON per configurare il modulo dell’interfaccia utente.
1. Tocca o fai clic su Salva.

## Creazione di un archivio ContextHub {#creating-a-contexthub-store}

Crea un archivio Context Hub per mantenere i dati utente e accedervi in base alle esigenze. Gli archivi ContextHub si basano su candidati di store registrati. Quando si crea lo store, è necessario il valore dello storeType con cui è stato registrato il candidato dello store. (Vedi [Creazione di candidati store personalizzati](extending-contexthub.md#creating-custom-store-candidates).)

### Configurazione dettagliata archivio {#detailed-store-configuration}

Quando si configura un archivio, la proprietà Configurazione dettagli consente di fornire valori per proprietà specifiche dell&#39;archivio. Il valore è basato sul `config` parametro dell&#39;archivio `init` funzione . Pertanto, se è necessario fornire questo valore e il formato del valore, dipende dall&#39;archivio.

Il valore della proprietà Configurazione dettagli è un `config` in formato JSON.

### Candidati dell’archivio esempi {#sample-store-candidates}

AEM fornisce i seguenti candidati all&#39;archivio di esempio su cui è possibile basare un archivio.

| Tipo di archivio | Descrizione |
|---|---|
| [aem.segmentation](sample-stores.md#aem-segmentation-sample-store-candidate) | Memorizzazione di segmenti ContextHub risolti e non risolti. Recupera automaticamente i segmenti da ContextHub SegmentManager |
| [contexthub.geolocation](sample-stores.md#contexthub-geolocation-sample-store-candidate) | Memorizza la latitudine e la longitudine della posizione del browser. |
| [granite.emulatori](sample-stores.md#granite-emulators-sample-store-candidate) | Definisce proprietà e funzionalità per diversi dispositivi e rileva il dispositivo client corrente |
| [granite.profile](sample-stores.md#granite-profile-sample-store-candidate) | Memorizza i dati del profilo per l&#39;utente corrente |
| [contexthub.surferinfo](sample-stores.md#contexthub-surferinfo-sample-store-candidate) | Memorizza informazioni sul client, ad esempio informazioni sul dispositivo, sul tipo di browser e sull&#39;orientamento della finestra |

1. Nella barra degli Experienci Manager, tocca o fai clic su Strumenti > Siti > ContextHub.
1. Tocca o fai clic sul contenitore di configurazione predefinito.
1. Tocca o fai clic su Configurazione contexthub
1. Per aggiungere un archivio, tocca o fai clic sull’icona Crea , quindi tocca o fai clic su Configurazione archivio ContextHub.

   ![Configurazione dell’archivio ContextHub](assets/contexthub-store-configuration.png)

1. Immetti i valori per le proprietà di configurazione di base, quindi tocca o fai clic su Avanti:

   * **Titolo configurazione:** Titolo che identifica lo store
   * **Tipo archivio:** Valore della proprietà storeType del candidato store su cui basare lo store
   * **Obbligatorio:** Seleziona
   * **Abilitato:** Selezionare per abilitare lo store

1. (Facoltativo) Per ignorare la configurazione predefinita dell’archivio, immetti un oggetto JSON nella casella Configurazione dettagli (JSON) .
1. Tocca o fai clic su Salva.

## Esempio: Utilizzo di un servizio JSONP  {#example-using-a-jsonp-service}

Questo esempio illustra come configurare un archivio e visualizzare i dati in un modulo di interfaccia utente. In questo esempio, il servizio MD5 del sito jsontest.com viene utilizzato come origine dati per un archivio. Il servizio restituisce il codice hash MD5 di una stringa specificata, in formato JSON.

Un archivio contexthub.generic-jsonp è configurato in modo da memorizzare i dati per la chiamata al servizio `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. Il servizio restituisce i seguenti dati visualizzati in un modulo dell&#39;interfaccia utente:

```javascript
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### Creazione di un archivio contexthub.generic-jsonp {#creating-a-contexthub-generic-jsonp-store}

Il candidato per l’archivio di esempio contexthub.generic-jsonp ti consente di recuperare dati da un servizio JSONP o da un servizio Web che restituisce dati JSON. Per questo Store Candidato, utilizza la configurazione dello store per fornire dettagli sul servizio JSONP da utilizzare.

La [init](contexthub-api.md#init-name-config) funzione `ContextHub.Store.JSONPStore` La classe Javascript definisce un `config` oggetto che inizializza il candidato all&#39;archivio. La `config` un oggetto contiene `service` oggetto che include dettagli sul servizio JSONP. Per configurare lo store, fornisci il `service` in formato JSON come valore della proprietà Configurazione dettagli.

Per salvare i dati dal servizio MD5 del sito jsontest.com, utilizza la procedura descritta in [Creazione di un archivio ContextHub](#creating-a-contexthub-store) utilizzando le seguenti proprietà:

* **Titolo configurazione:** md5
* **Tipo archivio:** contexthub.generic-jsonp
* **Obbligatorio:** Seleziona
* **Abilitato:** Seleziona
* **Configurazione dettagli (JSON):**

   ```javascript
   {
    "service": {
    "jsonp": false,
    "timeout": 1000,
    "ttl": 1800000,
    "secure": false,
    "host": "md5.jsontest.com",
    "port": 80,
    "params":{
    "text":"text to md5"
        }
      }
    }
   ```

### Aggiunta di un modulo dell&#39;interfaccia utente per i dati md5 {#adding-a-ui-module-for-the-md-data}

Aggiungi un modulo dell’interfaccia utente alla barra degli strumenti di ContextHub per visualizzare i dati memorizzati nell’archivio md5 di esempio. In questo esempio, il modulo contexthub.base viene utilizzato per produrre il seguente modulo di interfaccia utente:

![Archivio ContextHub MD5](assets/contexthub-md5-store.png)

Utilizza la procedura in [Aggiunta di un modulo dell’interfaccia utente](#adding-a-ui-module) per aggiungere il modulo dell’interfaccia utente a una modalità dell’interfaccia utente esistente, ad esempio la modalità dell’interfaccia utente personale di esempio. Per il modulo dell’interfaccia utente, utilizza i seguenti valori di proprietà:

* **Titolo modulo interfaccia utente:** MD5
* **Tipo di modulo:** contexthub.base
* **Configurazione dettagli (JSON):**

   ```javascript
   {
    "icon": "coral-Icon--data",
    "title": "MD5 Conversion",
    "storeMapping": { "md5": "md5" },
    "template": "<p> {{md5.original}}</p>;
                 <p>{{md5.md5}}</p>"
   }
   ```

## Debug di ContextHub {#debugging-contexthub}

È possibile abilitare una modalità di debug per ContextHub per consentire la risoluzione dei problemi. La modalità di debug può essere abilitata sia tramite la configurazione ContextHub che tramite CRXDE.

### Tramite la configurazione {#via-the-configuration}

Modifica la configurazione di ContextHub e seleziona l’opzione **Debug**

1. Nella barra, tocca o fai clic su **Strumenti > Siti > ContextHub**
1. Tocca o fai clic sul valore predefinito **Contenitore di configurazione**
1. Seleziona la **Configurazione ContextHub** e tocca o fai clic su **Modifica elemento selezionato**
1. Tocca o fai clic su **Debug** e tocca o fai clic su **Salva**

### Tramite CRXDE {#via-crxde}

Utilizzare CRXDE Lite per impostare la proprietà `debug` a **true** in:

* `/conf/global/settings/cloudsettings` oppure
* `/conf/<site>/settings/cloudsettings`

### Registrazione dei messaggi di debug per ContextHub {#logging-debug-messages-for-contexthub}

Configura il servizio Adobe OSGi ContextHub Granite (PID = `com.adobe.granite.contexthub.impl.ContextHubImpl`) per registrare messaggi di debug dettagliati utili durante lo sviluppo.

Per configurare il servizio è possibile utilizzare [Console web](/help/implementing/deploying/configuring-osgi.md) o utilizza un nodo JCR nell&#39;archivio:

* Console Web: Per registrare i messaggi di debug, selezionare la proprietà Debug.
* Nodo JCR: Per registrare i messaggi di debug, imposta il valore booleano `com.adobe.granite.contexthub.debug` proprietà di `true`.

### Modalità silenziosa {#silent-mode}

La modalità silenziosa sopprime tutte le informazioni di debug. A differenza della normale opzione di debug, che può essere impostata indipendentemente per ogni configurazione ContextHub, la modalità silenziosa è un&#39;impostazione globale che ha un precedente su qualsiasi impostazione di debug a livello di configurazione ContextHub.

Questo è utile per l&#39;istanza di pubblicazione, in cui non si desidera alcuna informazione di debug. Poiché è un’impostazione globale, viene abilitata tramite OSGi.

1. Apri **Configurazione della console Web di Adobe Experience Manager** a `http://<host>:<port>/system/console/configMgr`
1. Cerca **Adobe Granite ContextHub**
1. Fai clic sulla configurazione **Adobe Granite ContextHub** per modificarne le proprietà
1. Controlla l’opzione **Modalità silenziosa** e fai clic su **Salva**

## Disabilitazione di ContextHub {#disabling-contexthub}

ContextHub può essere disabilitato per impedirgli di caricare js/css e di inizializzare. Esistono due opzioni per disabilitare ContextHub:

* Modifica la configurazione di ContextHub e seleziona l’opzione **Disattiva ContextHub**

   1. Nella barra, tocca o fai clic su **Strumenti > Siti > ContextHub**
   1. Tocca o fai clic sul valore predefinito **Contenitore di configurazione**
   1. Seleziona la **Configurazione ContextHub** e tocca o fai clic su **Modifica elemento selezionato**
   1. Tocca o fai clic su **Disattiva ContextHub** e tocca o fai clic su **Salva**

oppure

* Utilizzare CRXDE Lite per impostare la proprietà `disabled` a **true** sotto `/conf/global/settings/cloudsettings/<configName>/contexthub`
