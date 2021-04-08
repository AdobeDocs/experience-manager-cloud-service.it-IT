---
title: Risoluzione dei problemi relativi a Dynamic Media
description: Suggerimenti per la risoluzione dei problemi durante l’utilizzo di Dynamic Media.
topic: '"Amministratore, Business Practitioner"'
role: Administrator,Business Practitioner
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 2%

---

# Risoluzione dei problemi relativi a Dynamic Media {#troubleshooting-dynamic-media-scene-mode}

L&#39;argomento seguente descrive la risoluzione dei problemi relativi a Dynamic Media.

## Nuova configurazione Dynamic Media {#new-dm-config}

Consulta [Risoluzione dei problemi relativi a una nuova configurazione Dynamic Media](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config).

## Generale (tutte le risorse) {#general-all-assets}

Di seguito sono riportati alcuni suggerimenti generali per tutte le risorse.

### Proprietà stato sincronizzazione risorse {#asset-synchronization-status-properties}

Le seguenti proprietà delle risorse possono essere esaminate in CRXDE Lite per confermare la corretta sincronizzazione della risorsa da Adobe Experience Manager a Dynamic Media:

| **Proprietà** | **Esempio** | **Descrizione** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | Indicatore generale che il nodo è collegato a Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **** Testo di PublishCompleteo di errore | Stato del caricamento della risorsa in Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Deve essere popolato per generare URL per la risorsa remota di Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **** successore  **non riuscito:`<error text>`** | Stato di sincronizzazione di set (set 360 gradi, set di immagini e così via), predefiniti immagine, predefiniti visualizzatore, aggiornamenti mappa immagine per una risorsa o immagini modificate. |

### Registrazione sincronizzazione {#synchronization-logging}

Gli errori e i problemi di sincronizzazione vengono registrati in `error.log` (directory del server Experience Manager `/crx-quickstart/logs/`). È disponibile una registrazione sufficiente per determinare la causa principale della maggior parte dei problemi, tuttavia è possibile aumentare la registrazione su DEBUG sul pacchetto `com.adobe.cq.dam.ips` tramite la console Sling ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) per raccogliere ulteriori informazioni.

### Controllo della versione {#version-control}

Quando sostituisci una risorsa Dynamic Media esistente (nome e posizione identici), puoi mantenere entrambe le risorse o sostituire/creare una versione:

* Mantenere entrambi crea una risorsa con un nome univoco per l’URL della risorsa pubblicata. Ad esempio, `image.jpg` è la risorsa originale e `image1.jpg` è la nuova risorsa caricata.

* La creazione di una versione non è supportata in Dynamic Media. La nuova versione sostituisce la risorsa esistente nella consegna.

## Immagini e set {#images-and-sets}

Se riscontri problemi con immagini e set, consulta le seguenti indicazioni per la risoluzione dei problemi.

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
       <li>Controlla se il predefinito nel JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> è definito. Questa posizione si applica se hai effettuato l’aggiornamento da Experience Manager 6.x a 6.4 e hai rinunciato alla migrazione. In caso contrario, la posizione è <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Verifica che la risorsa nel JCR sia <code>dam:scene7FileStatus</code><strong> </strong>sotto Metadati sia visualizzata come <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Aggiorna pagina/passa a un'altra pagina e torna (la barra laterale JSP deve essere ricompilata)</p> <p>Se questo non funziona:</p>
    <ul>
     <li>Pubblica la risorsa.</li>
     <li>Ricarica e pubblica la risorsa.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Il punto attivo del carosello si sposta dopo il passaggio tra le diapositive</td>
   <td><p>Verificare che tutte le diapositive abbiano le stesse dimensioni.</p> </td>
   <td><p>Utilizza solo immagini con la stessa dimensione per il carosello.</p> </td>
  </tr>
  <tr>
   <td>L’immagine non viene visualizzata in anteprima con il visualizzatore Dynamic Media</td>
   <td><p>Verifica che la risorsa contenga <code>dam:scene7File</code> nelle proprietà dei metadati (CRXDE Lite)</p> </td>
   <td><p>Verifica che tutte le risorse abbiano completato l’elaborazione.</p> </td>
  </tr>
  <tr>
   <td>La risorsa caricata non viene visualizzata nel selettore delle risorse</td>
   <td><p>Verifica che la risorsa abbia la proprietà <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Verifica che tutte le risorse abbiano completato l’elaborazione.</p> </td>
  </tr>
  <tr>
   <td>Il banner nella vista a schede mostra <strong>Nuovo</strong> quando la risorsa non ha iniziato l’elaborazione</td>
   <td>Controlla la risorsa <code>jcr:content</code> &gt; <code>dam:assetState</code> = se <code>unprocessed</code> non è stato rilevato dal flusso di lavoro.</td>
   <td>Attendi che la risorsa venga raccolta dal flusso di lavoro.</td>
  </tr>
  <tr>
   <td>Le immagini o i set non visualizzano l’URL o il codice di incorporamento del visualizzatore</td>
   <td>Controlla se il predefinito per visualizzatori è stato pubblicato.</td>
   <td><p>Vai a <strong>Strumenti</strong> &gt; <strong>Risorse</strong> &gt; <strong>Predefiniti visualizzatore</strong> e pubblica il predefinito visualizzatore.</p> </td>
  </tr>
 </tbody>
</table>

## Video {#video}

In caso di problemi con il video, consulta le seguenti indicazioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>Impossibile visualizzare in anteprima il video</td>
   <td>
    <ul>
     <li>Verifica che alla cartella sia assegnato un profilo video (se non è supportato). Se non è supportato, viene visualizzata solo un’immagine.</li>
     <li>Il profilo video deve contenere più di un predefinito di codifica per generare un set AVS (le codifiche singole vengono considerate come contenuto video per i file MP4; per i file non supportati, trattati come non elaborati).</li>
     <li>Verifica che l'elaborazione del video sia stata completata confermando <code>dam:scene7FileAvs</code> di <code>dam:scene7File</code> nei metadati.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Assegna un profilo video alla cartella.</li>
     <li>Modifica il profilo video per includere più di un predefinito di codifica.</li>
     <li>Attendere il completamento dell'elaborazione del video.</li>
     <li>Prima di ricaricare il video, assicurati che il flusso di lavoro Codifica video Dynamic Media non sia in esecuzione.<br/> </li>
     <li>Ricarica il video.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Il video non è codificato</td>
   <td>
    <ul>
     <li>Verifica se il Cloud Service Dynamic Media è configurato.</li>
     <li>Controlla se un profilo video è associato alla cartella di caricamento.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Verifica che la configurazione di Dynamic Media in Cloud Services sia configurata correttamente.</li>
     <li>Verifica che la cartella disponga di un profilo video. Inoltre, controlla il profilo video.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>L'elaborazione video richiede troppo tempo</td>
   <td><p>Per determinare se la codifica video è ancora in corso o se è stato immesso uno stato di errore:</p>
    <ul>
     <li>Controlla lo stato del video <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Rendering video mancante</td>
   <td><p>Quando il video viene caricato, ma non sono presenti rappresentazioni codificate:</p>
    <ul>
     <li>Verifica che alla cartella sia assegnato un profilo video.</li>
     <li>Verifica che l'elaborazione del video sia stata completata confermando <code>dam:scene7FileAvs</code> nei metadati.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Assegna un profilo video alla cartella.</li>
     <li>Attendere il completamento dell'elaborazione del video.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visualizzatori {#viewers}

Se riscontri problemi con i visualizzatori, consulta le seguenti indicazioni per la risoluzione dei problemi.

<table>
 <tbody>
  <tr>
   <td><strong>Problema</strong></td>
   <td><strong>Come eseguire il debug</strong></td>
   <td><strong>Soluzione</strong></td>
  </tr>
  <tr>
   <td>I predefiniti per visualizzatori non vengono pubblicati</td>
   <td><p>Passare alla pagina di diagnostica di sample manager: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Osserva i valori calcolati. Quando funziona correttamente, puoi vedere:</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Nota</strong>: La sincronizzazione delle risorse del visualizzatore può richiedere circa 10 minuti dopo la configurazione delle impostazioni cloud di Dynamic Media.</p> <p>Se le risorse non attivate rimangono, fai clic su uno dei pulsanti <strong>Elenca tutte le risorse non attivate</strong> per visualizzare i dettagli.</p> </td>
   <td>
    <ol>
     <li>Passa all’elenco dei predefiniti per visualizzatori in strumenti di amministrazione: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Seleziona tutti i predefiniti visualizzatore, quindi fai clic su <strong>Pubblica</strong>.</li>
     <li>Torna a Sample manager e osserva che il conteggio delle risorse non attivate è ora zero.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>L’immagine del predefinito per visualizzatori restituisce 404 dall’anteprima nei dettagli della risorsa o copia l’URL/codice da incorporare</td>
   <td><p>In CRXDE Lite procedi come segue:</p>
    <ol>
     <li>Passa alla cartella <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> all’interno della cartella di sincronizzazione Dynamic Media (ad esempio, <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Trova il nodo di metadati della risorsa problematica (ad esempio, <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Verifica la presenza delle proprietà <code>dam:scene7*</code> . Se la risorsa è stata sincronizzata e pubblicata correttamente, il set <code>dam:scene7FileStatus</code> è impostato su <strong>PublishComplete</strong>.</li>
     <li>Tentativo di richiedere l’immagine direttamente da Dynamic Media concatenando i valori delle seguenti proprietà e valori letterali stringa
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>Esempio: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>Se le risorse di esempio o l’immagine predefinita del visualizzatore non sono sincronizzate o pubblicate, riavvia l’intero processo di copia/sincronizzazione:</p>
    <ol>
     <li>Accedi a <code>/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code>
     </li>
     <li>Seleziona le azioni seguenti nell’ordine:
      <ol>
       <li>Elimina le cartelle di sincronizzazione.</li>
       <li>Elimina la cartella Preset (sotto <code>/conf</code>).
       <li>Attiva processo asincrono di configurazione DM.</li>
      </ol> </li>
     <li>Attendi la notifica della sincronizzazione corretta nella casella in entrata Experience Manager.
     </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
