---
title: Risoluzione dei problemi relativi a Dynamic Media
description: Risoluzione dei problemi relativi a Dynamic Media.
translation-type: tm+mt
source-git-commit: a0b4f04aaafbaef86728c8bd23cc026f43c72dde
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 2%

---


# Risoluzione dei problemi relativi a Dynamic Media {#troubleshooting-dynamic-media-scene-mode}

L&#39;argomento seguente descrive la risoluzione dei problemi relativi agli elementi multimediali dinamici.

## Nuova configurazione per contenuti multimediali dinamici {#new-dm-config}

Vedere [Risoluzione dei problemi relativi a una nuova configurazione per contenuti multimediali dinamici.](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config)

## Generale (tutte le risorse) {#general-all-assets}

Di seguito sono riportati alcuni suggerimenti e consigli generali per tutte le risorse.

### Proprietà stato sincronizzazione risorse {#asset-synchronization-status-properties}

Le seguenti proprietà della risorsa possono essere riviste in CRXDE Lite per confermare l’avvenuta sincronizzazione della risorsa da AEM a elemento multimediale dinamico:

| **Proprietà** | **Esempio** | **Descrizione** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicatore generale che il nodo è collegato a Contenuti multimediali dinamici. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **Testo di** PublishCompleteo di errore | Stato del caricamento di una risorsa in Contenuti multimediali dinamici. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Per generare gli URL delle risorse remote di elementi multimediali dinamici, è necessario compilarli. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **** successore  **non riuscito:`<error text>`** | Stato di sincronizzazione di set (set 360 gradi, set di immagini e così via), predefiniti per immagini, predefiniti per visualizzatori, aggiornamenti per mappe immagine per una risorsa o immagini modificate. |

### Registrazione sincronizzazione {#synchronization-logging}

Errori e problemi di sincronizzazione vengono registrati in `error.log` (AEM directory del server `/crx-quickstart/logs/`). È disponibile una registrazione sufficiente per determinare la causa principale della maggior parte dei problemi, tuttavia è possibile aumentare la registrazione in DEBUG sul pacchetto `com.adobe.cq.dam.ips` tramite Sling Console ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) per raccogliere ulteriori informazioni.

### Controllo della versione {#version-control}

Quando sostituite una risorsa multimediale dinamica esistente (nome e posizione identici), potete mantenere entrambe le risorse oppure sostituire o creare una versione:

* Entrambi gli elementi creeranno una nuova risorsa con un nome univoco per l’URL della risorsa pubblicata. Ad esempio, `image.jpg` è la risorsa originale e `image1.jpg` è la nuova risorsa caricata.

* La creazione di una versione non è supportata negli elementi multimediali dinamici. La nuova versione sostituirà la risorsa esistente in fase di distribuzione.

## Immagini e set {#images-and-sets}

In caso di problemi con immagini e set, consultate le seguenti istruzioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>Impossibile accedere al pulsante Copia URL/Incorpora nella visualizzazione dei dettagli della risorsa</td>
   <td>
    <ol>
     <li><p>Vai a CRX/DE:</p>
      <ul>
       <li>Verificate se il predefinito nel JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> è definito. Nota che questa posizione si applica se hai aggiornato da AEM 6.x a 6.4 e hai rinunciato alla migrazione. In caso contrario, il percorso è <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Verificate che la risorsa nel JCR sia <code>dam:scene7FileStatus</code><strong> </strong>in Metadati, come <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Aggiorna pagina/passa a un'altra pagina e torna (la barra laterale JSP deve essere ricompilata)</p> <p>Se questo non funziona:</p>
    <ul>
     <li>Pubblicare la risorsa.</li>
     <li>Caricate nuovamente la risorsa e pubblicatela.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Il punto di attivazione del carosello si sposta dopo il passaggio tra le diapositive</td>
   <td><p>Verificate che tutte le diapositive abbiano le stesse dimensioni.</p> </td>
   <td><p>Utilizzate solo immagini con la stessa dimensione per il carosello.</p> </td>
  </tr>
  <tr>
   <td>L’immagine non viene visualizzata in anteprima con il visualizzatore per contenuti multimediali dinamici</td>
   <td><p>Verificate che la risorsa contenga <code>dam:scene7File</code> nelle proprietà dei metadati (CRXDE Lite)</p> </td>
   <td><p>Verificate che tutte le risorse abbiano completato l'elaborazione.</p> </td>
  </tr>
  <tr>
   <td>La risorsa caricata non viene visualizzata nel selettore delle risorse</td>
   <td><p>La risorsa di controllo ha la proprietà <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Verificate che tutte le risorse abbiano completato l'elaborazione.</p> </td>
  </tr>
  <tr>
   <td>Il banner nella vista a schede mostra <strong>New</strong> quando la risorsa non ha iniziato l'elaborazione</td>
   <td>Controllare la risorsa <code>jcr:content</code> &gt; <code>dam:assetState</code> = se <code>unprocessed</code> non è stata individuata dal flusso di lavoro.</td>
   <td>Attendi che la risorsa venga scelta dal flusso di lavoro.</td>
  </tr>
  <tr>
   <td>Le immagini o i set non visualizzano l’URL del visualizzatore o il codice da incorporare</td>
   <td>Verificate che il predefinito per visualizzatori sia stato pubblicato.</td>
   <td><p>Passate a <strong>Strumenti</strong> &gt; <strong>Risorse</strong> &gt; <strong>Predefiniti visualizzatore</strong> e pubblicate il predefinito per visualizzatori.</p> </td>
  </tr>
 </tbody>
</table>

## Video {#video}

In caso di problemi con il video, consulta le seguenti istruzioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>Impossibile visualizzare l'anteprima del video</td>
   <td>
    <ul>
     <li>Verificate che alla cartella sia assegnato un profilo video (se il formato file non è supportato). Se non è supportato, viene visualizzata solo un'immagine.</li>
     <li>Il profilo video deve contenere più di un predefinito di codifica per generare un set AVS (le singole codifiche vengono trattate come contenuto video per i file MP4); per i file non supportati, trattati come non elaborati).</li>
     <li>Verificate che il video abbia terminato l'elaborazione confermando <code>dam:scene7FileAvs</code> di <code>dam:scene7File</code> nei metadati.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Assegnate un profilo video alla cartella.</li>
     <li>Modificate il profilo video per includere più di un predefinito di codifica.</li>
     <li>Attendere il completamento dell'elaborazione video.</li>
     <li>Ricaricate il video, accertatevi che il flusso di lavoro Codifica video elemento multimediale dinamico non sia in esecuzione.<br/> </li>
     <li>Caricate nuovamente il video.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Il video non è codificato</td>
   <td>
    <ul>
     <li>Verifica se il servizio Dynamic Media Cloud è configurato.</li>
     <li>Controllate se un profilo video è associato alla cartella di caricamento.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Verificate che la configurazione Dynamic Media in Cloud Services sia configurata correttamente.</li>
     <li>Verificate che la cartella disponga di un profilo video. Inoltre, controllate il profilo video.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>L'elaborazione video richiede troppo tempo</td>
   <td><p>Per determinare se la codifica video è ancora in corso o se è stato immesso un errore:</p>
    <ul>
     <li>Controllare lo stato del video <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Rendering video mancante</td>
   <td><p>Quando il video viene caricato, ma non esistono rappresentazioni codificate:</p>
    <ul>
     <li>Verificate che alla cartella sia assegnato un profilo video.</li>
     <li>Verificate che il video abbia terminato l'elaborazione confermando <code>dam:scene7FileAvs</code> nei metadati.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Assegnate un profilo video alla cartella.</li>
     <li>Attendere il completamento dell'elaborazione video.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visualizzatori {#viewers}

In caso di problemi con i visualizzatori, consultate le seguenti istruzioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>Predefiniti visualizzatore non pubblicati</td>
   <td><p>Passate alla pagina di diagnostica di esempio manager: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Osservare i valori calcolati. Quando funziona correttamente, dovresti vedere:</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Nota</strong>: Dopo la configurazione delle impostazioni di Dynamic Media Cloud, la sincronizzazione delle risorse del visualizzatore potrebbe richiedere circa 10 minuti.</p> <p>Se le risorse non attivate rimangono, fate clic su uno dei pulsanti <strong>Elenca tutte le risorse non attivate</strong> per visualizzare i dettagli.</p> </td>
   <td>
    <ol>
     <li>Passate all’elenco dei predefiniti per visualizzatori negli strumenti di amministrazione: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Selezionate tutti i predefiniti per visualizzatori, quindi fate clic su <strong>Pubblica</strong>.</li>
     <li>Tornate alla gestione degli esempi e tenete presente che il conteggio delle risorse non attivate è ora pari a zero.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>L’immagine del predefinito per visualizzatori restituisce 404 dall’anteprima nei dettagli delle risorse o dal codice URL/incorporato</td>
   <td><p>In CRXDE Lite, effettuate le seguenti operazioni:</p>
    <ol>
     <li>Andate alla cartella <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> all'interno della cartella di sincronizzazione di elementi multimediali dinamici (ad esempio, <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Individuate il nodo di metadati della risorsa problematica (ad esempio, <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Verificare la presenza delle proprietà <code>dam:scene7*</code>. Se la sincronizzazione e la pubblicazione della risorsa sono state completate correttamente, il set <code>dam:scene7FileStatus</code> è <strong>PublishComplete</strong>.</li>
     <li>Tentativo di richiedere l'immagine direttamente da Dynamic Media concatenando i valori delle seguenti proprietà e stringhe letterali
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>Esempio: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>Se le risorse di esempio o l’immagine del predefinito per visualizzatori non sono sincronizzate o pubblicate, riavviate l’intero processo di copia/sincronizzazione:</p>
    <ol>
     <li>Accedi a <code>/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code>
     </li>
     <li>Selezionate le azioni seguenti nell’ordine:
      <ol>
       <li>Eliminate le cartelle di sincronizzazione.</li>
       <li>Cartella dei predefiniti (sotto <code>/conf</code>).
       <li>Trigger DM Setup Async Job.</li>
      </ol> </li>
     <li>Attendi la notifica di sincronizzazione avvenuta nella casella in entrata AEM.
     </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

