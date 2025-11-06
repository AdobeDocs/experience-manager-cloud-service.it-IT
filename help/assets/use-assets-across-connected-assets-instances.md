---
title: Usa Assets connesso per condividere risorse DAM in [!DNL Sites]
description: Utilizza le risorse disponibili in una  [!DNL Adobe Experience Manager Assets] distribuzione remota quando crei le tue pagine Web in un'altra [!DNL Adobe Experience Manager Sites] distribuzione.
contentOwner: AK
mini-toc-levels: 2
feature: Asset Management, Connected Assets, Asset Distribution
role: Admin, User, Developer
exl-id: 2346f72d-a383-4202-849e-c5a91634617a
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3869'
ht-degree: 13%

---


# Usa Assets connesso per condividere risorse DAM in [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Nelle grandi aziende l’infrastruttura necessaria per la creazione di siti web può essere dislocata in luoghi diversi. A volte, le funzionalità per la creazione di siti web e le risorse digitali utilizzate per creare i siti possono trovarsi in implementazioni diverse. Uno dei motivi può essere la distribuzione geografica delle implementazioni esistenti necessarie per la collaborazione. Un altro motivo può essere costituito dalle acquisizioni che portano a infrastrutture eterogenee, incluse diverse versioni di [!DNL Experience Manager], che la società madre desidera utilizzare insieme.

>[!NOTE]
>
>Adobe consiglia di sfruttare Dynamic Media con funzionalità OpenAPI per collegare AEM Assets as a Cloud Service e AEM Sites. Vedi [Integrare AEM Assets remoto con AEM Sites](/help/assets/integrate-remote-approved-assets-with-sites.md).

La funzionalità connessa di Assets supporta i casi d&#39;uso precedenti integrando [!DNL Experience Manager Sites] e [!DNL Experience Manager Assets]. Gli utenti possono creare pagine Web in [!DNL Sites] che utilizzano le risorse digitali di [!DNL Assets] distribuzioni separate.

>[!NOTE]
>
>Configurare Connected Assets solo quando è necessario utilizzare le risorse disponibili in una distribuzione DAM remota in una distribuzione Sites separata per la creazione di pagine web.

## Panoramica di Connected Assets {#overview-of-connected-assets}

Quando si modificano le pagine in [!UICONTROL Editor pagina] come destinazione, gli autori possono cercare, sfogliare e incorporare senza problemi le risorse di una diversa distribuzione di [!DNL Assets] che funge da origine delle risorse. Gli amministratori creano un&#39;integrazione una tantum di una distribuzione di [!DNL Experience Manager] con funzionalità [!DNL Sites] con un&#39;altra distribuzione di [!DNL Experience Manager] con funzionalità [!DNL Assets]. Puoi anche utilizzare le immagini Dynamic Media nelle pagine web del sito tramite Connected Assets e utilizzare le funzionalità di Dynamic Media, ad esempio il ritaglio avanzato e i predefiniti per le immagini.

Per gli autori [!DNL Sites], le risorse remote sono disponibili come risorse locali di sola lettura. Questa funzionalità supporta la ricerca e l’accesso diretti alle risorse remote nell’Editor sito. Per qualsiasi altro caso d’uso che richieda la disponibilità su Sites del corpus completo di risorse, valuta la possibilità di migrare le risorse in blocco invece di utilizzare Connected Assets.

### Prerequisiti e implementazioni supportate {#prerequisites}

Prima di utilizzare o configurare questa funzionalità, verifica questi aspetti:

* Gli utenti fanno parte dei gruppi di utenti appropriati per ogni distribuzione.
* Per i tipi di distribuzione [!DNL Adobe Experience Manager], uno dei criteri supportati è soddisfatto. [!DNL Experience Manager] as a Cloud Service [!DNL Assets] funziona con [!DNL Experience Manager] 6.5. Per ulteriori informazioni sul funzionamento di questa funzionalità in [!DNL Experience Manager] 6.5, vedere [Assets connesso in [!DNL Experience Manager] 6.5 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html?lang=it).

  | | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.5 [!DNL Sites] in AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] on-premise |
  |---|---|---|---|
  | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | Supportato | Supportato | Supportato |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] in AMS** | Supportato | Supportato | Supportato |
  | **[!DNL Experience Manager]6.5 [!DNL Assets] on-premise** | Non supportato | Non supportato | Non supportato |

### Formati di file supportati {#mimetypes}

Gli autori cercano le immagini e i seguenti tipi di documenti in Content Finder e trascinano le risorse trovate nell’Editor pagina. I documenti vengono aggiunti al componente `Download` e le immagini al componente `Image`. Gli autori possono inoltre aggiungere le risorse remote a qualsiasi componente [!DNL Experience Manager] personalizzato che estenda i componenti predefiniti di `Download` o `Image`. I formati supportati sono:

* **Formati immagine**: formati supportati dal [componente immagine](file-format-support.md#image-formats).
* **Formati di documenti**: vedere i [formati di documenti supportati](file-format-support.md#document-formats).

### Utenti e gruppi interessati {#users-and-groups-involved}

Di seguito sono descritti i vari ruoli coinvolti nella configurazione e la funzionalità e i relativi gruppi di utenti. L’ambito locale viene utilizzato per il caso d’uso in cui un autore crea una pagina web. L’ambito remoto viene utilizzato per l’implementazione DAM in cui sono ospitate le risorse necessarie. L&#39;autore [!DNL Sites] recupera queste risorse remote.

| Ruolo | Ambito | Gruppo di utenti | Descrizioni |
|------|--------|-----------|----------|
| Amministratore [!DNL Sites] | Locale | [!DNL Experience Manager] `administrators` | Configurare [!DNL Experience Manager] e configurare l&#39;integrazione con la distribuzione remota di [!DNL Assets]. |
| Utente DAM | Locale | `Authors` | Utilizzato per visualizzare e duplicare le risorse recuperate in `/content/DAM/connectedassets/`. |
| Autore [!DNL Sites] | Locale | <ul><li>`Authors` (con accesso in lettura in DAM remoto e accesso di authoring in [!DNL Sites] locale) </li> <li>`dam-users` su [!DNL Sites] locale</li></ul> | Gli utenti finali sono [!DNL Sites] autori che utilizzano questa integrazione per velocizzare le attività relative ai contenuti. Gli autori possono cercare e sfogliare le risorse in DAM remoto utilizzando [!UICONTROL Content Finder] e utilizzando le immagini richieste nelle pagine Web locali. |
| Amministratore [!DNL Assets] | Remoto | [!DNL Experience Manager] `administrators` | Configurare la condivisione risorse tra le origini (CORS, Cross-Origin Resource Sharing). |
| Utente DAM | Remoto | `Authors` | Ruolo Autore nella distribuzione remota di [!DNL Experience Manager]. Cercare e sfogliare le risorse in Connected Assets utilizzando [!UICONTROL Content Finder]. |
| Distributore DAM (utente tecnico) | Remoto | <ul> <li> [!DNL Sites] `Authors`</li> <li> `connectedassets-assets-techaccts` </li> </ul> | Questo utente presente nella distribuzione remota viene utilizzato dal server locale [!DNL Experience Manager] (non il ruolo di autore [!DNL Sites]) per recuperare le risorse remote, per conto dell&#39;autore [!DNL Sites]. |
| [!DNL Sites] utente tecnico | Locale | `connectedassets-sites-techaccts` | Consente alla distribuzione [!DNL Assets] di cercare riferimenti alle risorse nelle pagine Web [!DNL Sites]. |

### Architettura di Assets connessa {#connected-assets-architecture}

Experience Manager consente di collegare una distribuzione DAM remota come origine a più distribuzioni Experience Manager [!DNL Sites]. È tuttavia possibile connettere una distribuzione [!DNL Sites] con una sola distribuzione remota di DAM.

Valuta il numero ottimale di istanze Sites per la connessione a una distribuzione DAM remota. Adobe consiglia di connettere in modo incrementale le istanze di Sites alla distribuzione e di verificare che non vi sia alcun impatto sulle prestazioni in DAM remoto, in quanto ogni istanza di Sites connessa contribuisce al traffico di dati in DAM remoto.

I seguenti diagrammi illustrano gli scenari supportati:

![Architettura Assets connessa](assets/connected-assets-architecture.png)

Il diagramma seguente illustra uno scenario non supportato:

![Architettura Assets connessa](assets/connected-assets-architecture-unsupported.png)

## Configura una connessione tra [!DNL Sites] e [!DNL Assets] distribuzioni {#configure-a-connection-between-sites-and-assets-deployments}

Un amministratore [!DNL Experience Manager] può creare questa integrazione. Una volta create, le autorizzazioni necessarie per utilizzarle vengono stabilite tramite gruppi di utenti. I gruppi di utenti sono definiti nell&#39;implementazione [!DNL Sites] e nell&#39;implementazione DAM.

Per configurare la connettività Connected Assets e la connettività locale di [!DNL Sites], eseguire la procedura seguente:

1. Accedere a una distribuzione [!DNL Sites] esistente. Questa distribuzione di [!DNL Sites] viene utilizzata per l&#39;authoring delle pagine Web, ad esempio alle `https://<sites_server_fqdn>:[port]`. Poiché l&#39;authoring delle pagine avviene nella distribuzione [!DNL Sites], chiamiamo la distribuzione [!DNL Sites] locale dal punto di vista dell&#39;authoring delle pagine.

1. Accedere a una distribuzione [!DNL Assets] esistente. Questa distribuzione di [!DNL Assets] viene utilizzata per gestire le risorse digitali, ad esempio in `https://[assets_servername]:port`.

1. Verificare che gli utenti e i ruoli con l&#39;ambito appropriato siano presenti nella distribuzione [!DNL Sites] e nella distribuzione [!DNL Assets] in AMS. Creare un utente tecnico nella distribuzione di [!DNL Assets] e aggiungerlo al gruppo di utenti menzionato in [utenti e gruppi interessati](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Accedere alla distribuzione locale di [!DNL Sites] in `https://[sites_servername]:port`. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Configurazione risorse collegate]** e fornisci i seguenti valori:

   1. Un **[!UICONTROL Titolo]** della configurazione.
   1. **[!UICONTROL URL DAM remoto]** è l&#39;URL del percorso [!DNL Assets] nel formato `https://[assets_servername]:[port]`.
   1. Credenziali di un distributore DAM (utente tecnico).
   1. Nel campo **[!UICONTROL Punto di montaggio]**, immettere il percorso [!DNL Experience Manager] locale in cui [!DNL Experience Manager] recupera le risorse. Ad esempio, `connectedassets` cartella. Le risorse recuperate da DAM sono memorizzate in questa cartella nella distribuzione di [!DNL Sites].
   1. **[!UICONTROL URL siti locali]** è il percorso della distribuzione [!DNL Sites]. La distribuzione [!DNL Assets] utilizza questo valore per mantenere i riferimenti alle risorse digitali recuperate da questa distribuzione [!DNL Sites].
   1. Credenziali di [!DNL Sites] utente tecnico.
   1. Il valore del campo **[!UICONTROL Soglia ottimizzazione trasferimento binario originale]** specifica se le risorse originali (incluse le rappresentazioni) vengono trasferite in modo sincrono o meno. Assets con file di dimensioni ridotte può essere recuperato facilmente, mentre è consigliabile sincronizzare in modo asincrono le risorse con file di dimensioni relativamente maggiori. Il valore dipende dalle funzionalità di rete.
   1. Seleziona **[!UICONTROL Archivio dati condiviso con Assets connesso]**, se utilizzi un archivio dati per archiviare le risorse e l&#39;archivio dati è condiviso tra entrambe le distribuzioni. In questo caso, il limite di soglia non ha importanza in quanto i dati binari effettivi delle risorse sono disponibili nell’archivio dati e non vengono trasferiti.

   ![Configurazione tipica per la funzionalità Connected Assets](assets/connected-assets-typical-config.png)

   *Figura: configurazione tipica per la funzionalità Connected Assets.*

1. Le risorse digitali esistenti nella distribuzione [!DNL Assets] sono già elaborate e le rappresentazioni sono generate. Queste rappresentazioni vengono recuperate utilizzando questa funzionalità, pertanto non è necessario rigenerarle. Disattiva i moduli di avvio dei flussi di lavoro per impedire la rigenerazione delle rappresentazioni. Regola le configurazioni del modulo di avvio nella distribuzione ([!DNL Sites]) per escludere la cartella `connectedassets` (le risorse vengono recuperate in questa cartella).

   1. Nella distribuzione di [!DNL Sites], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Moduli di avvio]**.

   1. Individua i moduli di avvio con flussi di lavoro come **[!UICONTROL Aggiorna risorsa DAM]** e **[!UICONTROL Writeback di metadati DAM]**.

   1. Seleziona il modulo di avvio del flusso di lavoro e fai clic su **[!UICONTROL Proprietà]** nella barra delle azioni.

   1. Nella procedura guidata [!UICONTROL Proprietà], modifica i campi **[!UICONTROL Percorso]** come i mapping seguenti per aggiornare le espressioni regolari al fine di escludere il punto di montaggio **[!UICONTROL connectedassets]**.

   | Prima | Dopo |
   | ------ | ------------ |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Quando gli autori recuperano una risorsa, vengono recuperati tutti i rendering disponibili nell’implementazione remota. Se desideri creare più rendering per una risorsa recuperata, ignora questo passaggio di configurazione. Il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] viene attivato e crea altre rappresentazioni. Queste rappresentazioni sono disponibili solo nell&#39;implementazione locale di [!DNL Sites] e non nell&#39;implementazione remota di DAM.

1. Aggiungere la distribuzione [!DNL Sites] come origine consentita nella configurazione CORS nella distribuzione [!DNL Assets]. Per ulteriori informazioni, vedere [Comprendere CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=it).

1. Configura [supporto per cookie dello stesso sito](/help/security/same-site-cookie-support.md).

È possibile verificare la connettività tra le distribuzioni [!DNL Sites] configurate e la distribuzione [!DNL Assets].

![Test di connessione di Assets connesso configurato [!DNL Sites]](assets/connected-assets-multiple-config.png)
*Figura: test di connessione di Connected Assets configurato [!DNL Sites].*

<!-- TBD: Check if Launchers are to be disabled on CS instances. Is this option even available to the users on CS? -->

## Utilizzare le risorse Dynamic Media {#dynamic-media-assets}


Con Connected Assets è possibile utilizzare le risorse immagine elaborate da [!DNL Dynamic Media] dalla distribuzione remota DAM nelle pagine Sites e utilizzare le funzionalità di Dynamic Media, ad esempio il ritaglio avanzato e i predefiniti per immagini.

Per utilizzare [!DNL Dynamic Media] con Connected Assets:

1. Configurare [!DNL Dynamic Media] nella distribuzione remota di DAM con la modalità di sincronizzazione abilitata.
1. Configura [Assets connesso](#configure-a-connection-between-sites-and-assets-deployments).
1. Configurare [!DNL Dynamic Media] nell&#39;istanza Sites con lo stesso nome società configurato in DAM remoto. Per poter funzionare con le risorse connesse, l’implementazione di Sites deve disporre di accesso in sola lettura all’account Dynamic Media. Pertanto, assicurati di disabilitare la modalità di sincronizzazione nella configurazione di Dynamic Media nell’istanza Sites.

>[!CAUTION]
>
>Con la configurazione Connected Assets e [!DNL Dynamic Media], non è possibile utilizzare [!DNL Dynamic Media] per elaborare le risorse locali disponibili nella distribuzione di [!DNL Sites].

## Configurare [!DNL Dynamic Media] {#configure-dynamic-media}

Per configurare [!DNL Dynamic Media] per le distribuzioni [!DNL Assets] e [!DNL Sites]:

1. Creare la configurazione di Connected Assets come descritto in precedenza, tranne quando si configura la funzionalità, selezionare **[!UICONTROL Recupera rappresentazione originale per l&#39;opzione Dynamic Media Connected Assets]**.

1. Configurare [!DNL Dynamic Media] nelle distribuzioni locali di [!DNL Sites] e remote di [!DNL Assets]. Segui le istruzioni per [configurare [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

   * Utilizza lo stesso nome società in tutte le configurazioni.
   * In [!DNL Sites] locale, in [!UICONTROL modalità di sincronizzazione Dynamic Media], selezionare **[!UICONTROL Disabilitato per impostazione predefinita]**. La distribuzione di [!DNL Sites] deve avere accesso in sola lettura all&#39;account [!DNL Dynamic Media].
   * In [!DNL Sites] locale, nell&#39;opzione **[!UICONTROL Pubblica Assets]**, selezionare **[!UICONTROL Pubblicazione selettiva]**. Non selezionare **[!UICONTROL Sincronizza tutto il contenuto]**.
   * Nella distribuzione remota di [!DNL Assets], in [!UICONTROL modalità di sincronizzazione Dynamic Media], selezionare **[!UICONTROL Abilitato per impostazione predefinita]**.

1. Abilitare il supporto per [[!DNL Dynamic Media] nel componente core Immagine](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=it#dynamic-media). Questa funzionalità consente al [componente immagine](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html) predefinito di visualizzare [!DNL Dynamic Media] immagini quando gli autori utilizzano [!DNL Dynamic Media] immagini nelle pagine Web nella distribuzione locale di [!DNL Sites].

## Utilizzare le risorse remote {#use-remote-assets}

Gli autori del sito web utilizzano Content Finder per connettersi all’implementazione DAM. Gli autori possono sfogliare, cercare e trascinare le risorse remote in un componente. Per eseguire l’autenticazione nel DAM remoto, tieni a portata di mano le credenziali fornite dall’amministratore (se presenti).

Gli autori possono utilizzare le risorse disponibili nell’implementazione DAM locale e nell’implementazione DAM remota in un’unica pagina web. Utilizza Content Finder per passare dalla ricerca nel DAM locale alla ricerca nel DAM remoto.

Vengono recuperati solo i tag delle risorse remote con un tag corrispondente esatto insieme alla stessa gerarchia di tassonomia, disponibile nella distribuzione locale di [!DNL Sites]. Tutti gli altri tag vengono eliminati. Gli autori possono cercare risorse remote utilizzando tutti i tag presenti nella distribuzione remota di [!DNL Experience Manager], in quanto offre una ricerca full-text.

### Procedura dettagliata per l’utilizzo {#walk-through-of-usage}

Utilizza la configurazione precedente per provare l’esperienza di authoring e comprendere il funzionamento di questa caratteristica. Utilizza documenti o immagini di tua scelta nell’implementazione remota di DAM.

1. Passare all&#39;interfaccia [!DNL Assets] nella distribuzione remota accedendo a **[!UICONTROL Assets]** > **[!UICONTROL File]** dall&#39;area di lavoro [!DNL Experience Manager]. In alternativa, puoi accedere a `https://[assets_servername_ams]:[port]/assets.html/content/dam` in un browser. Carica le risorse che hai scelto.

1. Nella distribuzione di [!DNL Sites], nell&#39;attivatore del profilo nell&#39;angolo superiore destro, fare clic su **[!UICONTROL Impersona]**. Specificare il nome utente, selezionare l&#39;opzione fornita e fare clic su **[!UICONTROL OK]**.

1. Aprire una pagina [!DNL Sites] e modificarla.

   Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell’angolo in alto a sinistra della pagina.

1. Apri la scheda [!UICONTROL Assets] (Trova contenuto remoto) e fai clic su **[!UICONTROL Accedi a Connected Assets]**.

1. Specificare le credenziali per accedere a Connected Assets. Questo utente dispone delle autorizzazioni di authoring per entrambe le distribuzioni [!DNL Experience Manager].

1. Cerca la risorsa aggiunta a DAM. Le risorse remote vengono visualizzate nel pannello a sinistra. Filtra immagini o documenti e filtra ulteriormente i tipi di documenti supportati. Trascina le immagini su un componente `Image`, e i documenti su un componente `Download`.

   Le risorse recuperate sono di sola lettura nell&#39;implementazione locale di [!DNL Sites]. Puoi comunque utilizzare le opzioni fornite dai componenti [!DNL Sites] per modificare la risorsa recuperata. La modifica per componenti non è distruttiva.

   ![Opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opzioni di filtro per tipi di documenti e immagini durante la ricerca di risorse in DAM remoto.*

1. Un autore del sito riceve una notifica se l’originale di una risorsa viene recuperato in modo asincrono e se un’attività di recupero ha esito negativo. Durante l&#39;authoring, o anche successivamente, gli autori possono visualizzare informazioni dettagliate sulle attività di recupero e sugli errori nell&#39;interfaccia utente [processi asincroni](/help/operations/asynchronous-jobs.md).

   ![Notifica relativa al recupero asincrono delle risorse in background.](assets/assets_async_transfer_fails.png)

   *Figura: notifica relativa al recupero asincrono delle risorse in background.*

1. Quando si pubblica una pagina, [!DNL Experience Manager] visualizza un elenco completo delle risorse utilizzate nella pagina. Assicurati che le risorse remote vengano recuperate correttamente al momento della pubblicazione. Per verificare lo stato di ciascuna risorsa recuperata, consulta l&#39;interfaccia utente di [processi asincroni](/help/operations/asynchronous-jobs.md).

   >[!NOTE]
   >
   >Anche se una o più risorse remote non vengono recuperate completamente, la pagina viene pubblicata. Nell&#39;area di notifica [!DNL Experience Manager] viene visualizzata una notifica per gli errori visualizzati nella pagina dei processi asincroni.

>[!CAUTION]
>
>Una volta utilizzate in una pagina web, le risorse remote recuperate possono essere cercate e utilizzate da qualsiasi utente con autorizzazioni di accesso alla cartella locale. Le risorse recuperate sono archiviate nella cartella locale (`connectedassets` nella procedura dettagliata precedente). Le risorse possono inoltre essere cercate e visualizzate nell’archivio locale tramite [!UICONTROL Content Finder].

Le risorse recuperate possono essere utilizzate come qualsiasi altra risorsa locale, ad eccezione del fatto che i metadati associati non possono essere modificati.

### Controllare l’utilizzo di una risorsa in più pagine web {#asset-usage-references}

[!DNL Experience Manager] consente agli utenti DAM di controllare tutti i riferimenti a una risorsa. Consente di comprendere e gestire l&#39;utilizzo di una risorsa in [!DNL Sites] remoto e in risorse composte. Molti autori di pagine Web nella distribuzione [!DNL Experience Manager Sites] possono utilizzare una risorsa in un DAM remoto in pagine Web diverse. Per semplificare la gestione delle risorse e non causare riferimenti interrotti, è importante che gli utenti DAM controllino l’utilizzo di una risorsa nelle pagine web locali e remote. Nella scheda [!UICONTROL Riferimenti] della pagina [!UICONTROL Proprietà] di una risorsa sono elencati i riferimenti locali e remoti della risorsa.

Per visualizzare e gestire i riferimenti nella distribuzione [!DNL Assets], eseguire la procedura seguente:

1. Selezionare una risorsa nella console [!DNL Assets] e fare clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Fai clic sulla scheda **[!UICONTROL Riferimenti]**. Vedi **[!UICONTROL Riferimenti locali]** per l&#39;utilizzo della risorsa nella distribuzione [!DNL Assets]. Vedi **[!UICONTROL Riferimenti remoti] per l&#39;utilizzo della risorsa nella distribuzione [!DNL Sites] in cui la risorsa è stata recuperata utilizzando la funzionalità Connected Assets.

   ![Riferimenti remoti nella pagina Proprietà risorsa](assets/connected-assets-remote-reference.png)

1. I riferimenti per [!DNL Sites] pagine visualizzano il conteggio totale dei riferimenti per ogni [!DNL Sites] locale. La ricerca di tutti i riferimenti e la visualizzazione del numero totale di riferimenti potrebbero richiedere del tempo.
1. L’elenco dei riferimenti è interattivo e gli utenti DAM possono fare clic su un riferimento per aprire la pagina di riferimento. Se per qualche motivo non è possibile recuperare i riferimenti remoti, viene visualizzata una notifica per informare l’utente dell’errore.
1. Gli utenti possono spostare o eliminare la risorsa. Quando si sposta o si elimina una risorsa, in una finestra di dialogo di avviso viene visualizzato il numero totale di riferimenti di tutte le risorse o cartelle selezionate. Quando si elimina una risorsa per la quale non sono ancora stati recuperati i riferimenti, viene visualizzata una finestra di dialogo di avvertenza.

   ![forza eliminazione avviso](assets/delete-referenced-asset.png)

### Gestire gli aggiornamenti delle risorse in DAM remoto {#handling-updates-to-remote-assets}

Dopo la [configurazione di una connessione](#configure-a-connection-between-sites-and-assets-deployments) tra le distribuzioni remote di DAM e Sites, le risorse in DAM remoto sono rese disponibili nell&#39;implementazione di Sites. È quindi possibile aggiornare, eliminare, rinominare e spostare le operazioni sulle risorse o cartelle DAM remote. Gli aggiornamenti, con un certo ritardo, sono disponibili automaticamente nell’implementazione di Sites. Inoltre, se una risorsa in DAM remoto viene utilizzata in una pagina Experience Manager Sites locale, gli aggiornamenti della risorsa in DAM remoto vengono visualizzati nella pagina Sites.

Quando sposti una risorsa da una posizione a un&#39;altra, assicurati di [regolare i riferimenti](manage-digital-assets.md) in modo che la risorsa venga visualizzata nella pagina Sites. Se sposti una risorsa in un percorso non accessibile dall’implementazione Sites locale, la risorsa non viene visualizzata nell’implementazione Sites.

Puoi anche aggiornare le proprietà dei metadati di una risorsa in DAM remoto e le modifiche sono disponibili nell’implementazione Sites locale.

Gli autori dei siti possono visualizzare in anteprima gli aggiornamenti disponibili nell’implementazione di Sites e quindi ripubblicare le modifiche per renderle disponibili nell’istanza di pubblicazione di AEM.

Experience Manager visualizza un indicatore visivo di stato `expired` sulle risorse in Remote Assets Content Finder per impedire agli autori del sito di utilizzare la risorsa in una pagina Sites. Se utilizzi una risorsa con lo stato `expired` in una pagina Sites, la risorsa non viene visualizzata nell&#39;istanza di pubblicazione di Experience Manager.

## Domande frequenti {#frequently-asked-questions}

+++**Configurare Connected Assets se è necessario utilizzare le risorse disponibili nella distribuzione di [!DNL Sites]?**

In tal caso non è necessario configurare Connected Assets. È possibile utilizzare le risorse disponibili nella distribuzione [!DNL Sites].

+++

+++**Quando è necessario configurare la funzionalità Connected Assets?**

Configurare la funzione Connected Assets solo quando è necessario utilizzare le risorse disponibili in una distribuzione DAM remota in una distribuzione [!DNL Sites].

+++

+++**È possibile connettere più distribuzioni di [!DNL Sites] a una distribuzione DAM remota dopo aver configurato Connected Assets?**

Sì, è possibile connettere più distribuzioni [!DNL Sites] a una distribuzione DAM remota dopo aver configurato Connected Assets. Per ulteriori informazioni, vedere [Architettura Assets connessa](#connected-assets-architecture).

+++

+++**Quante distribuzioni DAM remote è possibile connettersi a una distribuzione [!DNL Sites] dopo aver configurato Connected Assets?**

È possibile connettere una distribuzione DAM remota a una distribuzione [!DNL Sites] dopo aver configurato Connected Assets. Per ulteriori informazioni, vedere [Architettura Assets connessa](#connected-assets-architecture).

+++

+++**È possibile utilizzare le risorse Dynamic Media della distribuzione di [!DNL Sites] dopo aver configurato Connected Assets?**

Dopo aver configurato Connected Assets, le risorse [!DNL Dynamic Media] sono disponibili nella distribuzione [!DNL Sites] in modalità di sola lettura. Di conseguenza, non è possibile utilizzare [!DNL Dynamic Media] per elaborare le risorse nella distribuzione di [!DNL Sites]. Per ulteriori informazioni, vedere [Configurare una connessione tra le distribuzioni di Sites e Dynamic Media](#dynamic-media-assets).

+++

+++**È possibile utilizzare le risorse di tipo Immagine e Documento della distribuzione DAM remota nella distribuzione [!DNL Sites] dopo aver configurato Connected Assets?**

Sì, è possibile utilizzare le risorse dei tipi di formato Immagine e Documento della distribuzione DAM remota nella distribuzione [!DNL Sites] dopo aver configurato Connected Assets.

+++

+++**È possibile utilizzare frammenti di contenuto e risorse video della distribuzione DAM remota nella distribuzione [!DNL Sites] dopo aver configurato Connected Assets?**

No, non è possibile utilizzare frammenti di contenuto e risorse video dalla distribuzione remota DAM nella distribuzione [!DNL Sites] dopo la configurazione di Connected Assets.

+++

+++**È possibile utilizzare le risorse Dynamic Media della distribuzione remota DAM nella distribuzione [!DNL Sites] dopo aver configurato Connected Assets?**

Sì, è possibile configurare e utilizzare le risorse immagine di Dynamic Media dalla distribuzione remota di DAM nella distribuzione [!DNL Sites] dopo aver configurato Connected Assets. Per ulteriori informazioni, vedere [Configurare una connessione tra le distribuzioni di Sites e Dynamic Media](#dynamic-media-assets).

+++

+++**Dopo aver configurato Connected Assets, è possibile eseguire le operazioni di aggiornamento, eliminazione, ridenominazione e spostamento sulle risorse o cartelle DAM remote?**

Sì, dopo aver configurato Connected Assets, puoi eseguire le operazioni di aggiornamento, eliminazione, ridenominazione e spostamento sulle risorse o cartelle DAM remote. Gli aggiornamenti, con un certo ritardo, sono disponibili automaticamente nell’implementazione di Sites. Per ulteriori informazioni, consulta [Gestire gli aggiornamenti delle risorse in DAM remoto](#handling-updates-to-remote-assets).

+++

+++**Dopo aver configurato Connected Assets, è possibile aggiungere o modificare le risorse nella distribuzione di [!DNL Sites] e renderle disponibili nella distribuzione remota di DAM?**

È possibile aggiungere risorse alla distribuzione [!DNL Sites], tuttavia tali risorse non possono essere rese disponibili per la distribuzione remota di DAM.

+++


## Limitazioni e best practice {#tip-and-limitations}

* Per ottenere informazioni sull&#39;utilizzo delle risorse, configura la funzionalità [Assets Insight](/help/assets/assets-insights.md) nell&#39;istanza [!DNL Sites].
* L’utilizzo del browser percorsi nei componenti di authoring non è supportato nelle risorse collegate.

* Impossibile trascinare la risorsa remota nella [finestra di dialogo di configurazione del componente immagine](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=it#configure-dialog). Tuttavia, puoi trascinare la risorsa remota direttamente nel componente immagine nella pagina Sites senza fare clic su **[!UICONTROL Configura]**.

### Autorizzazioni e gestione delle risorse {#permissions-and-managing-assets}

* Le risorse locali sono copie in sola lettura. [!DNL Experience Manager] componenti apportano modifiche non distruttive alle risorse. Non sono consentite altre modifiche.
* Le risorse recuperate localmente sono disponibili solo a scopo di authoring. I flussi di lavoro di aggiornamento delle risorse non possono essere applicati e i metadati non possono essere modificati.
* Quando si utilizza [!DNL Dynamic Media] in [!DNL Sites] pagine, la risorsa originale non viene recuperata e memorizzata nella distribuzione locale. Il nodo `dam:Asset`, i metadati e le rappresentazioni generati dalla distribuzione [!DNL Assets] sono tutti recuperati nella distribuzione [!DNL Sites].
* Sono supportati solo le immagini e i formati di documento elencati. [!DNL Content Fragments] e [!DNL Experience Fragments] non sono supportati.
* [!DNL Experience Manager] non recupera gli schemi di metadati. Ciò significa che potrebbero non essere visualizzati tutti i metadati recuperati. Se lo schema viene aggiornato separatamente nella distribuzione [!DNL Sites], vengono visualizzate tutte le proprietà dei metadati.
* Tutti gli autori [!DNL Sites] dispongono di autorizzazioni di lettura per le copie recuperate, anche se gli autori non possono accedere alla distribuzione remota di DAM.
* Nessun supporto API per personalizzare l’integrazione.
* Questa funzionalità supporta la ricerca e l’utilizzo diretti delle risorse remote. Per rendere disponibili molte risorse remote nell’implementazione locale con un’unica operazione, è consigliabile eseguire la migrazione delle risorse.
* Impossibile utilizzare una risorsa remota come miniatura di pagina nell&#39;interfaccia utente [!UICONTROL Proprietà pagina]. È possibile impostare una miniatura di una pagina Web nell&#39;interfaccia utente di [!UICONTROL Proprietà pagina] dalla [!UICONTROL Miniatura] facendo clic su [!UICONTROL Seleziona immagine].

### Configurazione e licenze {#setup-licensing}

* La distribuzione di [!DNL Assets] in [!DNL Adobe Managed Services] è supportata.
* [!DNL Sites] può connettersi a una singola distribuzione di [!DNL Assets] alla volta.
* È necessaria una licenza di [!DNL Assets] che funziona come archivio remoto.
* Sono necessarie una o più licenze di [!DNL Sites] che funzionano come distribuzione di authoring locale.

### Utilizzo {#usage}

* Gli utenti possono cercare risorse remote e trascinarle sulla pagina locale durante l’authoring. Non sono supportate altre funzionalità.
* L’operazione di recupero si interrompe per timeout dopo 5 secondi. Gli autori possono rilevare dei problemi durante il recupero delle risorse, ad esempio in caso di problemi di rete. Gli autori possono riprovare trascinando la risorsa remota da [!UICONTROL Content Finder] all&#39;[!UICONTROL Page Editor].
* Le risorse recuperate possono essere sottoposte a semplici modifiche non distruttive e alle modifiche supportate tramite il componente `Image`. Le risorse sono di sola lettura.
* L’unico metodo per recuperare nuovamente la risorsa è trascinarla su una pagina. Non è disponibile alcun supporto API o altri metodi per recuperare nuovamente una risorsa e aggiornarla.
* Se le risorse vengono rimosse dal DAM, continuano a essere in uso su [!DNL Sites] pagine.
* Le voci di riferimento remote di una risorsa vengono recuperate in modo asincrono. I riferimenti e il conteggio totale non sono in tempo reale e potrebbe esserci una differenza se un autore [!DNL Sites] utilizza la risorsa mentre un utente DAM sta visualizzando il riferimento. Gli utenti DAM possono aggiornare la pagina e riprovare tra qualche minuto per ottenere il conteggio totale.

## Risoluzione dei problemi {#troubleshoot}

Per risolvere gli errori più comuni, effettuare le seguenti operazioni:

* Se non riesci a cercare risorse remote da [!UICONTROL Content Finder], assicurati che siano presenti i ruoli e le autorizzazioni richiesti.

* Una risorsa recuperata da DAM remoto potrebbe non essere pubblicata su una pagina web per uno o più motivi. Non esiste sul server remoto, la causa può essere la mancanza di autorizzazioni appropriate per recuperarlo o un errore di rete. Assicurati che la risorsa non venga rimossa da DAM remoto. Assicurati di disporre delle autorizzazioni appropriate e che i prerequisiti siano soddisfatti. Riprova ad aggiungere la risorsa alla pagina e ripubblica. Controlla l’[elenco dei processi asincroni](/help/operations/asynchronous-jobs.md) per verificare la presenza di errori nel recupero delle risorse.

* Se non riesci ad accedere alla distribuzione remota di DAM dalla distribuzione locale di [!DNL Sites], assicurati che siano consentiti i cookie intersito e che sia configurato il [supporto per i cookie dello stesso sito](/help/security/same-site-cookie-support.md). Se i cookie intersito sono bloccati, le distribuzioni di [!DNL Experience Manager] potrebbero non essere autenticate. Ad esempio, [!DNL Google Chrome] in modalità di navigazione in incognito potrebbe bloccare i cookie di terze parti. Per consentire i cookie nel browser [!DNL Chrome], fare clic sull&#39;icona &#39;occhio&#39; nella barra degli indirizzi, passare a **Sito non funzionante** > **Bloccato**, selezionare l&#39;URL DAM remoto e consentire il cookie token di accesso. In alternativa, consulta [come abilitare i cookie di terze parti](https://support.google.com/chrome/answer/95647).

  ![Errore cookie nel browser Chrome in modalità in incognito](assets/chrome-cookies-incognito-dialog.png)

* Se i riferimenti remoti non vengono recuperati e viene visualizzato un messaggio di errore, verificare se la distribuzione di [!DNL Sites] è disponibile e verificare la presenza di problemi di connettività di rete. Riprova più tardi per controllare. La distribuzione di [!DNL Assets] tenta due volte di stabilire una connessione con la distribuzione di [!DNL Sites], quindi segnala un errore.

  ![impossibile recuperare i riferimenti remoti delle risorse](assets/reference-report-failure.png)

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
