---
title: Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Sites]
description: Utilizzare le risorse disponibili su un sito remoto [!DNL Adobe Experience Manager Assets] distribuzione durante la creazione di pagine web su un’altra [!DNL Adobe Experience Manager Sites] distribuzione.
contentOwner: AK
mini-toc-levels: 2
feature: Asset Management,Connected Assets,Asset Distribution,User and Groups
role: Admin,User,Architect
exl-id: 2346f72d-a383-4202-849e-c5a91634617a
source-git-commit: 5da4be3ec9af6a00cce8d80b8eea7f7520754a1d
workflow-type: tm+mt
source-wordcount: '3816'
ht-degree: 16%

---


# Utilizzare la funzione Risorse collegate per condividere risorse DAM in [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html) |
| AEM as a Cloud Service | Questo articolo |

Nelle grandi aziende l’infrastruttura necessaria per la creazione di siti web può essere dislocata in luoghi diversi. A volte, le funzionalità per la creazione di siti web e le risorse digitali utilizzate per creare i siti possono trovarsi in implementazioni diverse. Uno dei motivi può essere la distribuzione geografica delle implementazioni esistenti necessarie per la collaborazione. Un altro motivo può essere costituito dalle acquisizioni che portano a infrastrutture eterogenee, tra cui diverse [!DNL Experience Manager] versioni, che la società madre desidera utilizzare insieme.

La funzionalità Risorse collegate supporta i casi d’uso precedenti tramite l’integrazione di [!DNL Experience Manager Sites] e [!DNL Experience Manager Assets]. Gli utenti possono creare pagine web in [!DNL Sites] che utilizzano le risorse digitali da un [!DNL Assets] distribuzioni.

>[!NOTE]
>
>Configurare le risorse collegate solo quando è necessario utilizzare le risorse disponibili in una distribuzione DAM remota in una distribuzione Sites separata per la creazione di pagine web.

## Panoramica della funzione Risorse collegate {#overview-of-connected-assets}

Durante la modifica delle pagine in [!UICONTROL Editor pagina] come destinazione, gli autori possono cercare, sfogliare e incorporare facilmente le risorse di un’altra [!DNL Assets] che funge da origine di risorse. Gli amministratori creano un’integrazione una tantum di una distribuzione di [!DNL Experience Manager] con [!DNL Sites] con un&#39;altra implementazione di [!DNL Experience Manager] con [!DNL Assets] funzionalità. Puoi anche utilizzare le immagini Dynamic Media nelle pagine web del sito tramite Risorse collegate e sfruttare le funzionalità di Dynamic Media, come il ritaglio avanzato e i predefiniti per immagini.

Per [!DNL Sites] autori, le risorse remote sono disponibili come risorse locali di sola lettura. Questa funzionalità supporta la ricerca e l’accesso diretti alle risorse remote nell’Editor sito. Per qualsiasi altro caso d’uso che richieda la disponibilità su Sites del corpus completo di risorse, valuta la possibilità di migrare le risorse in blocco invece di sfruttare le risorse collegate.

### Prerequisiti e implementazioni supportate {#prerequisites}

Prima di utilizzare o configurare questa funzionalità, verifica questi aspetti:

* Gli utenti fanno parte dei gruppi di utenti appropriati per ogni distribuzione.
* Per [!DNL Adobe Experience Manager] tipi di distribuzione, è soddisfatto uno dei criteri supportati. [!DNL Experience Manager] as a Cloud Service [!DNL Assets] funziona con [!DNL Experience Manager] 6.5. Per ulteriori informazioni su come funziona questa funzionalità in [!DNL Experience Manager] 6.5, cfr. [Risorse collegate in [!DNL Experience Manager] 6,5 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6,5 [!DNL Sites] su AMS | [!DNL Experience Manager] 6,5 [!DNL Sites] on-premise |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | Supportato | Supportato | Supportato |
   | **[!DNL Experience Manager]6,5 [!DNL Assets] su AMS** | Supportato | Supportato | Supportato |
   | **[!DNL Experience Manager]6,5 [!DNL Assets] on-premise** | Non supportato | Non supportato | Non supportato |

### Formati di file supportati {#mimetypes}

Gli autori cercano le immagini e i seguenti tipi di documenti in Content Finder e trascinano le risorse trovate nell’Editor pagina. I documenti vengono aggiunti al `Download` componenti e immagini per `Image` componente. Gli autori possono inoltre aggiungere le risorse remote a qualsiasi [!DNL Experience Manager] componente che estende il valore predefinito `Download` o `Image` componenti. I formati supportati sono:

* **Formati immagine**: i formati che [Componente immagine](file-format-support.md#image-formats) supporta.
* **Formati dei documenti**: consulta [formati di documento supportati](file-format-support.md#document-formats).

### Utenti e gruppi interessati {#users-and-groups-involved}

Di seguito sono descritti i vari ruoli coinvolti nella configurazione e la funzionalità e i relativi gruppi di utenti. L’ambito locale viene utilizzato per il caso d’uso in cui un autore crea una pagina web. L’ambito remoto viene utilizzato per l’implementazione DAM in cui sono ospitate le risorse necessarie. Il [!DNL Sites] l’autore recupera queste risorse remote.

| Ruolo | Ambito | Gruppo di utenti | Descrizioni |
|------|--------|-----------|----------|
| [!DNL Sites] administrator | Locale | [!DNL Experience Manager] `administrators` | Configurazione [!DNL Experience Manager] e configurare l&#39;integrazione con il [!DNL Assets] distribuzione. |
| Utente DAM | Locale | `Authors` | Utilizzato per visualizzare e duplicare le risorse recuperate in `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Locale | <ul><li>`Authors` (con accesso in lettura in DAM remoto e accesso di authoring in locale) [!DNL Sites]) </li> <li>`dam-users` su locale [!DNL Sites]</li></ul> | Gli utenti finali sono [!DNL Sites] autori che utilizzano questa integrazione per velocizzare le attività relative ai contenuti. Gli autori possono cercare e sfogliare le risorse in DAM remoto utilizzando [!UICONTROL Content Finder] e utilizzando le immagini richieste nelle pagine web locali. |
| [!DNL Assets] administrator | Remoto | [!DNL Experience Manager] `administrators` | Configurare la condivisione risorse tra le origini (CORS, Cross-Origin Resource Sharing). |
| Utente DAM | Remoto | `Authors` | Autore ruolo sul remoto [!DNL Experience Manager] distribuzione. Cercare e sfogliare le risorse in Risorse collegate utilizzando [!UICONTROL Content Finder]. |
| Distributore DAM (utente tecnico) | Remoto | <ul> <li> [!DNL Sites] `Authors`</li> <li> `connectedassets-assets-techaccts` </li> </ul> | Questo utente presente nell’implementazione remota viene utilizzato da [!DNL Experience Manager] server locale (non il [!DNL Sites] per recuperare le risorse remote, per conto di [!DNL Sites] Autore. |
| [!DNL Sites] utente tecnico | Locale | `connectedassets-sites-techaccts` | Consente [!DNL Assets] implementazione per cercare riferimenti alle risorse in [!DNL Sites] pagine web. |

### Architettura delle risorse collegate {#connected-assets-architecture}

Experience Manager consente di collegare una distribuzione DAM remota come origine a più Experienci Manager [!DNL Sites] distribuzioni. Tuttavia, è possibile collegare un [!DNL Sites] distribuzione con una sola distribuzione remota di DAM.

Valuta il numero ottimale di istanze Sites per la connessione a una distribuzione DAM remota. L’Adobe consiglia di connettere in modo incrementale le istanze Sites alla distribuzione e di verificare che non vi sia alcun impatto sulle prestazioni in DAM remoto, in quanto ogni istanza Sites connessa contribuisce al traffico dati in DAM remoto.

I seguenti diagrammi illustrano gli scenari supportati:

![Architettura delle risorse collegate](assets/connected-assets-architecture.png)

Il diagramma seguente illustra uno scenario non supportato:

![Architettura delle risorse collegate](assets/connected-assets-architecture-unsupported.png)

## Configurare una connessione tra [!DNL Sites] e [!DNL Assets] implementazioni {#configure-a-connection-between-sites-and-assets-deployments}

Un [!DNL Experience Manager] l’amministratore può creare questa integrazione. Una volta create, le autorizzazioni necessarie per utilizzarle vengono stabilite tramite gruppi di utenti. I gruppi di utenti sono definiti nel [!DNL Sites] e sull’implementazione di DAM.

Per configurare le risorse collegate e locali [!DNL Sites] connettività, segui questi passaggi:

1. Accedere a un [!DNL Sites] distribuzione. Questo [!DNL Sites] La distribuzione viene utilizzata per l’authoring delle pagine web, ad esempio all’indirizzo `https://<sites_server_fqdn>:[port]`. Quando l’authoring delle pagine avviene [!DNL Sites] distribuzione, chiamiamo il [!DNL Sites] come locale dal punto di vista dell’authoring delle pagine.

1. Accedere a un [!DNL Assets] distribuzione. Questo [!DNL Assets] L’implementazione viene utilizzata per gestire le risorse digitali, ad esempio all’indirizzo `https://[assets_servername]:port`.

1. Assicurati che gli utenti e i ruoli con l&#39;ambito appropriato siano presenti nel [!DNL Sites] distribuzione e sul [!DNL Assets] distribuzione in AMS. Creare un utente tecnico su [!DNL Assets] e aggiungi al gruppo di utenti menzionato in [utenti e gruppi interessati](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Accedi al [!DNL Sites] distribuzione in `https://[sites_servername]:port`. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Configurazione risorse collegate]** e fornisci i seguenti valori:

   1. A **[!UICONTROL Titolo]** della configurazione.
   1. **[!UICONTROL URL DAM remoto]** è l’URL del [!DNL Assets] posizione nel formato `https://[assets_servername]:[port]`.
   1. Credenziali di un distributore DAM (utente tecnico).
   1. In **[!UICONTROL Punto di montaggio]** , immettere il valore locale [!DNL Experience Manager] percorso in cui [!DNL Experience Manager] recupera le risorse. Ad esempio, la cartella `connectedassets`. Le risorse recuperate da DAM vengono memorizzate in questa cartella sul [!DNL Sites] distribuzione.
   1. **[!UICONTROL URL siti locali]** è la posizione del [!DNL Sites] distribuzione. [!DNL Assets] La distribuzione utilizza questo valore per mantenere i riferimenti alle risorse digitali recuperate da questo [!DNL Sites] distribuzione.
   1. Credenziali di [!DNL Sites] utente tecnico.
   1. Il valore di **[!UICONTROL Soglia ottimizzazione trasferimento binario originale]** specifica se le risorse originali (incluse le rappresentazioni) vengono trasferite in modo sincrono o meno. Le risorse con file di dimensioni inferiori possono essere recuperate facilmente, mentre le risorse con file di dimensioni relativamente maggiori possono essere sincronizzate in modo ottimale in modo asincrono. Il valore dipende dalle funzionalità di rete.
   1. Seleziona **[!UICONTROL Archivio dati condiviso con risorse collegate]**, se utilizzi un archivio dati per memorizzare le risorse e l’archivio dati è condiviso tra entrambe le distribuzioni. In questo caso, il limite di soglia non ha importanza in quanto i dati binari effettivi delle risorse sono disponibili nell’archivio dati e non vengono trasferiti.

   ![Configurazione tipica per la funzionalità Risorse collegate](assets/connected-assets-typical-config.png)

   *Figura: Configurazione tipica per la funzionalità Risorse collegate.*

1. Le risorse digitali esistenti su [!DNL Assets] La distribuzione è già stata elaborata e vengono generate le relative rappresentazioni. Queste rappresentazioni vengono recuperate utilizzando questa funzionalità, pertanto non è necessario rigenerarle. Disattiva i moduli di avvio dei flussi di lavoro per impedire la rigenerazione delle rappresentazioni. Regola le configurazioni del modulo di avvio in ([!DNL Sites]) per escludere il `connectedassets` cartella (le risorse vengono recuperate in questa cartella).

   1. On [!DNL Sites] distribuzione, fare clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Moduli di avvio]**.

   1. Individua i moduli di avvio con flussi di lavoro come **[!UICONTROL Aggiorna risorsa DAM]** e **[!UICONTROL Writeback di metadati DAM]**.

   1. Seleziona il modulo di avvio del flusso di lavoro e fai clic su **[!UICONTROL Proprietà]** nella barra delle azioni.

   1. In [!UICONTROL Proprietà] procedura guidata, modifica **[!UICONTROL Percorso]** come le mappature seguenti per aggiornare le espressioni regolari al fine di escludere il punto di montaggio **[!UICONTROL connectedassets]**.

   | Prima | Dopo |
   | ------ | ------------ |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Quando gli autori recuperano una risorsa, vengono recuperati tutti i rendering disponibili nell’implementazione remota. Se desideri creare più rendering per una risorsa recuperata, ignora questo passaggio di configurazione. Il [!UICONTROL Aggiorna risorsa DAM] Il flusso di lavoro viene attivato e crea più rappresentazioni. Queste rappresentazioni sono disponibili solo sul [!DNL Sites] e non nell’implementazione remota di DAM.

1. Aggiungi il [!DNL Sites] distribuzione come origine consentita nella configurazione CORS sul [!DNL Assets] distribuzione. Per ulteriori informazioni, consulta [comprendere CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. Configura [supporto per cookie dello stesso sito](/help/security/same-site-cookie-support.md).

Puoi controllare la connettività tra le [!DNL Sites] implementazioni e [!DNL Assets] distribuzione.

![Prova di connessione delle risorse collegate configurate [!DNL Sites]](assets/connected-assets-multiple-config.png)
*Figura: Prova di connessione delle risorse collegate configurate [!DNL Sites].*

<!-- TBD: Check if Launchers are to be disabled on CS instances. Is this option even available to the users on CS? -->

## Utilizzare le risorse di Dynamic Media {#dynamic-media-assets}


Con Risorse collegate, puoi utilizzare le risorse immagine elaborate da [!DNL Dynamic Media] dall’implementazione remota di DAM nelle pagine Sites e sfrutta le funzionalità di Dynamic Media, come i predefiniti per ritaglio avanzato e immagini.

Da utilizzare [!DNL Dynamic Media] con risorse collegate:

1. Configura [!DNL Dynamic Media] in un’implementazione remota di DAM con la modalità di sincronizzazione abilitata.
1. Configura [Risorse collegate](#configure-a-connection-between-sites-and-assets-deployments).
1. Configura [!DNL Dynamic Media] sull’istanza Sites con lo stesso nome società configurato in DAM remoto. Per poter funzionare con le risorse connesse, l’implementazione di Sites deve disporre dell’accesso in sola lettura all’account Dynamic Media. Pertanto, assicurati di disabilitare la modalità di sincronizzazione nella configurazione di Dynamic Media nell’istanza di Sites.

>[!CAUTION]
>
>Con risorse collegate e [!DNL Dynamic Media] , non è possibile utilizzare [!DNL Dynamic Media] per elaborare le risorse locali disponibili su [!DNL Sites] distribuzione.

## Configurare [!DNL Dynamic Media] {#configure-dynamic-media}

Per configurare [!DNL Dynamic Media] il [!DNL Assets] e [!DNL Sites] distribuzioni:

1. Crea la configurazione di Risorse collegate come descritto in precedenza, tranne quando configuri la funzionalità, seleziona **[!UICONTROL Recupera rappresentazione originale per risorse collegate a Dynamic Media]** opzione.

1. Configura [!DNL Dynamic Media] su locale [!DNL Sites] e remoto [!DNL Assets] distribuzioni. Seguire le istruzioni per [configura [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

   * Utilizza lo stesso nome società in tutte le configurazioni.
   * Su locale [!DNL Sites], in [!UICONTROL Modalità di sincronizzazione Dynamic Media], seleziona **[!UICONTROL Disabilitata per impostazione predefinita]**. Il [!DNL Sites] la distribuzione deve avere accesso in sola lettura al [!DNL Dynamic Media] account.
   * Su locale [!DNL Sites], nella **[!UICONTROL Pubblicare le risorse]** , seleziona **[!UICONTROL Pubblicazione selettiva]**. Non selezionare **[!UICONTROL Sincronizza tutto il contenuto]**.
   * In remoto [!DNL Assets] distribuzione, in [!UICONTROL Modalità di sincronizzazione Dynamic Media], seleziona **[!UICONTROL Attivato per impostazione predefinita]**.

1. Abilita [[!DNL Dynamic Media] supporto nel componente core Immagine](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). Questa funzione abilita l&#39;impostazione predefinita [Componente immagine](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html) da visualizzare [!DNL Dynamic Media] immagini quando [!DNL Dynamic Media] le immagini vengono utilizzate dagli autori nelle pagine Web in locale [!DNL Sites] distribuzione.

## Utilizzare le risorse remote {#use-remote-assets}

Gli autori del sito web utilizzano Content Finder per connettersi all’implementazione DAM. Gli autori possono sfogliare, cercare e trascinare le risorse remote in un componente. Per eseguire l’autenticazione nel DAM remoto, tieni a portata di mano le credenziali fornite dall’amministratore (se presenti).

Gli autori possono utilizzare le risorse disponibili nell’implementazione DAM locale e nell’implementazione DAM remota in un’unica pagina web. Utilizza Content Finder per passare dalla ricerca nel DAM locale alla ricerca nel DAM remoto.

Vengono recuperati solo i tag delle risorse remote con un tag corrispondente esatto insieme alla stessa gerarchia di tassonomia, disponibile nel [!DNL Sites] distribuzione. Tutti gli altri tag vengono eliminati. Gli autori possono cercare risorse remote utilizzando tutti i tag presenti sul remoto [!DNL Experience Manager] distribuzione, in quanto offre una ricerca full-text.

### Procedura dettagliata per l’utilizzo {#walk-through-of-usage}

Utilizza la configurazione precedente per provare l’esperienza di authoring e comprendere il funzionamento di questa caratteristica. Utilizza documenti o immagini di tua scelta nell’implementazione remota di DAM.

1. Accedi a [!DNL Assets] nell&#39;implementazione remota mediante l&#39;accesso **[!UICONTROL Risorse]** > **[!UICONTROL File]** da [!DNL Experience Manager] Workspace. In alternativa, puoi accedere a `https://[assets_servername_ams]:[port]/assets.html/content/dam` in un browser. Carica le risorse che hai scelto.

1. Il giorno [!DNL Sites] implementazione, nell’attivatore del profilo in alto a destra, fai clic su **[!UICONTROL Impersona]**. Specifica il nome utente, seleziona l’opzione fornita e fai clic su **[!UICONTROL OK]**.

1. Apri un [!DNL Sites] e modificare la pagina.

   Fai clic su **[!UICONTROL Attiva/Disattiva pannello laterale]** nell’angolo in alto a sinistra della pagina.

1. Apri [!UICONTROL Risorse] (Remote Content Finder) e fare clic su **[!UICONTROL Accedi alle risorse collegate]**.

1. Specifica le credenziali per accedere alle risorse collegate. Questo utente dispone di autorizzazioni di authoring sia per [!DNL Experience Manager] distribuzioni.

1. Cerca la risorsa aggiunta a DAM. Le risorse remote vengono visualizzate nel pannello a sinistra. Filtra immagini o documenti e filtra ulteriormente i tipi di documenti supportati. Trascina le immagini su un componente `Image`, e i documenti su un componente `Download`.

   Le risorse recuperate sono di sola lettura nel locale [!DNL Sites] distribuzione. Puoi continuare a utilizzare le opzioni fornite dal tuo [!DNL Sites] componenti per modificare la risorsa recuperata. La modifica per componenti non è distruttiva.

   ![Opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opzioni di filtro per tipi di documenti e immagini nella ricerca di risorse in DAM remoto.*

1. Un autore del sito riceve una notifica se l’originale di una risorsa viene recuperato in modo asincrono e se un’attività di recupero ha esito negativo. Durante l’authoring, o anche successivamente, gli autori possono visualizzare informazioni dettagliate sulle attività di recupero e sugli errori in [processi asincroni](/help/operations/asynchronous-jobs.md) dell&#39;utente.

   ![Notifica relativa al recupero asincrono delle risorse in background.](assets/assets_async_transfer_fails.png)

   *Figura: notifica relativa al recupero asincrono delle risorse in background.*

1. Quando pubblichi una pagina, [!DNL Experience Manager] visualizza un elenco completo delle risorse utilizzate nella pagina. Assicurati che le risorse remote vengano recuperate correttamente al momento della pubblicazione. Per verificare lo stato di ciascuna risorsa recuperata, vedi [processi asincroni](/help/operations/asynchronous-jobs.md) dell&#39;utente.

   >[!NOTE]
   >
   >Anche se una o più risorse remote non vengono recuperate completamente, la pagina viene pubblicata. Il [!DNL Experience Manager] nell’area di notifica viene visualizzata una notifica degli errori visualizzati nella pagina processi asincroni.

>[!CAUTION]
>
>Una volta utilizzate in una pagina web, le risorse remote recuperate possono essere cercate e utilizzate da qualsiasi utente con autorizzazioni di accesso alla cartella locale. Le risorse recuperate vengono memorizzate nella cartella locale (`connectedassets` nel passaggio precedente). Le risorse possono inoltre essere cercate e visualizzate nell’archivio locale tramite [!UICONTROL Content Finder].

Le risorse recuperate possono essere utilizzate come qualsiasi altra risorsa locale, ad eccezione del fatto che i metadati associati non possono essere modificati.

### Controllare l’utilizzo di una risorsa in più pagine web {#asset-usage-references}

[!DNL Experience Manager] consente agli utenti DAM di controllare tutti i riferimenti a una risorsa. Consente di comprendere e gestire l’utilizzo di una risorsa in remoto [!DNL Sites] e in attività composte. Molti autori di pagine web su [!DNL Experience Manager Sites] La distribuzione può utilizzare una risorsa in un DAM remoto in diverse pagine web. Per semplificare la gestione delle risorse e non causare riferimenti interrotti, è importante che gli utenti DAM controllino l’utilizzo di una risorsa nelle pagine web locali e remote. Il [!UICONTROL Riferimenti] scheda di una risorsa [!UICONTROL Proprietà] pagina elenca i riferimenti locali e remoti della risorsa.

Per visualizzare e gestire i riferimenti in [!DNL Assets] distribuzione, segui questi passaggi:

1. Selezionare una risorsa in [!DNL Assets] Console e fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti.
1. Clic **[!UICONTROL Riferimenti]** scheda. Consulta **[!UICONTROL Riferimenti locali]** per l’utilizzo della risorsa su [!DNL Assets] distribuzione. Consulta **[!UICONTROL Riferimenti remoti] per l’utilizzo della risorsa il [!DNL Sites] implementazione in cui la risorsa è stata recuperata utilizzando la funzionalità Risorse collegate.

   ![Riferimenti remoti nella pagina Proprietà della risorsa](assets/connected-assets-remote-reference.png)

1. I riferimenti per [!DNL Sites] le pagine visualizzano il conteggio totale dei riferimenti per ogni locale [!DNL Sites]. La ricerca di tutti i riferimenti e la visualizzazione del numero totale di riferimenti potrebbero richiedere del tempo.
1. L’elenco dei riferimenti è interattivo e gli utenti DAM possono fare clic su un riferimento per aprire la pagina di riferimento. Se per qualche motivo non è possibile recuperare i riferimenti remoti, viene visualizzata una notifica per informare l’utente dell’errore.
1. Gli utenti possono spostare o eliminare la risorsa. Quando si sposta o si elimina una risorsa, in una finestra di dialogo di avviso viene visualizzato il numero totale di riferimenti di tutte le risorse o cartelle selezionate. Quando si elimina una risorsa per la quale non sono ancora stati recuperati i riferimenti, viene visualizzata una finestra di dialogo di avvertenza.

   ![avviso di eliminazione forzata](assets/delete-referenced-asset.png)

### Gestire gli aggiornamenti delle risorse in DAM remoto {#handling-updates-to-remote-assets}

Dopo [configurazione di una connessione](#configure-a-connection-between-sites-and-assets-deployments) tra le implementazioni remote di DAM e Sites, le risorse in DAM remoto sono rese disponibili nell’implementazione di Sites. È quindi possibile aggiornare, eliminare, rinominare e spostare le operazioni sulle risorse o cartelle DAM remote. Gli aggiornamenti, con un certo ritardo, sono disponibili automaticamente nell’implementazione di Sites. Inoltre, se una risorsa in DAM remoto viene utilizzata in una pagina Experience Manager Sites locale, gli aggiornamenti della risorsa in DAM remoto vengono visualizzati nella pagina Sites.

Quando sposti una risorsa da una posizione a un’altra, assicurati di [regola riferimenti](manage-digital-assets.md) in modo che la risorsa venga visualizzata nella pagina Sites. Se sposti una risorsa in un percorso non accessibile dall’implementazione Sites locale, la risorsa non viene visualizzata nell’implementazione Sites.

Puoi anche aggiornare le proprietà dei metadati di una risorsa in DAM remoto e le modifiche sono disponibili nell’implementazione Sites locale.

Gli autori dei siti possono visualizzare in anteprima gli aggiornamenti disponibili nell’implementazione di Sites e quindi ripubblicare le modifiche per renderle disponibili nell’istanza di pubblicazione dell’AEM.

L’Experience Manager mostra un `expired` indicatore visivo di stato sulle risorse in Remote Assets Content Finder per impedire agli autori del sito di utilizzare la risorsa in una pagina Sites. Se utilizzi una risorsa con un `expired` in una pagina Sites, la risorsa non viene visualizzata nell’istanza Publish di Experience Manager.

## Domande frequenti {#frequently-asked-questions}

+++**Configurare Risorse collegate se è necessario utilizzare le risorse disponibili sul [!DNL Sites] distribuzione?**

In tal caso, non è necessario configurare le risorse collegate. Puoi utilizzare le risorse disponibili nella [!DNL Sites] distribuzione.

+++

+++**Quando è necessario configurare la funzione Risorse collegate?**

Configurare la funzione Risorse collegate solo quando è necessario utilizzare le risorse disponibili in una distribuzione DAM remota su un [!DNL Sites] distribuzione.

+++

+++**È possibile collegare più [!DNL Sites] distribuzioni in una distribuzione DAM remota dopo la configurazione di Risorse collegate?**

Sì, è possibile connettere più [!DNL Sites] implementazioni in una distribuzione DAM remota dopo la configurazione di Risorse collegate. Per ulteriori informazioni, consulta [Architettura delle risorse collegate](#connected-assets-architecture).

+++

+++**Quante distribuzioni DAM remote è possibile connettersi a una [!DNL Sites] dopo aver configurato le risorse collegate?**

È possibile connettere una distribuzione DAM remota a una [!DNL Sites] dopo la configurazione di Risorse collegate. Per ulteriori informazioni, consulta [Architettura delle risorse collegate](#connected-assets-architecture).

+++

+++**È possibile utilizzare le risorse di Dynamic Media dal proprio [!DNL Sites] dopo aver configurato le risorse collegate?**

Dopo aver configurato le risorse collegate, [!DNL Dynamic Media] le risorse sono disponibili su [!DNL Sites] distribuzione in modalità di sola lettura. Di conseguenza, non è possibile utilizzare [!DNL Dynamic Media] per elaborare le risorse in [!DNL Sites] distribuzione. Per ulteriori informazioni, consulta [Configurare una connessione tra le distribuzioni di Sites e Dynamic Media](#dynamic-media-assets).

+++

+++**È possibile utilizzare le risorse di tipo Immagine e Documento della distribuzione remota DAM in [!DNL Sites] dopo aver configurato le risorse collegate?**

Sì, è possibile utilizzare le risorse di tipo Immagine e Documento della distribuzione remota DAM in [!DNL Sites] dopo la configurazione di Risorse collegate.

+++

+++**È possibile utilizzare frammenti di contenuto e risorse video dall’implementazione remota di DAM in [!DNL Sites] dopo aver configurato le risorse collegate?**

No, non è possibile utilizzare frammenti di contenuto e risorse video dall’implementazione remota di DAM in [!DNL Sites] dopo la configurazione di Risorse collegate.

+++

+++**È possibile utilizzare le risorse Dynamic Media dall’implementazione remota di DAM in [!DNL Sites] dopo aver configurato le risorse collegate?**

Sì, puoi configurare e utilizzare le risorse immagine Dynamic Media dall’implementazione remota di DAM in [!DNL Sites] dopo la configurazione di Risorse collegate. Per ulteriori informazioni, consulta [Configurare una connessione tra le distribuzioni di Sites e Dynamic Media](#dynamic-media-assets).

+++

+++**Dopo aver configurato le risorse collegate, è possibile eseguire le operazioni di aggiornamento, eliminazione, ridenominazione e spostamento sulle risorse o cartelle DAM remote?**

Sì, dopo aver configurato le risorse collegate, puoi eseguire le operazioni di aggiornamento, eliminazione, ridenominazione e spostamento sulle risorse o cartelle DAM remote. Gli aggiornamenti, con un certo ritardo, sono disponibili automaticamente nell’implementazione di Sites. Per ulteriori informazioni, consulta [Gestire gli aggiornamenti delle risorse in DAM remoto](#handling-updates-to-remote-assets).

+++

+++**Dopo aver configurato le risorse collegate, puoi aggiungere o modificare le risorse sul tuo [!DNL Sites] e renderle disponibili nell’implementazione remota di DAM?**

Puoi aggiungere risorse alla sezione [!DNL Sites] Tuttavia, tali risorse non possono essere rese disponibili per l’implementazione remota di DAM.

+++


## Limitazioni e best practice {#tip-and-limitations}

* Per ottenere informazioni approfondite sull’utilizzo delle risorse, configura [Assets Insight](/help/assets/assets-insights.md) funzionalità di [!DNL Sites] dell&#39;istanza.

### Autorizzazioni e gestione delle risorse {#permissions-and-managing-assets}

* Le risorse locali sono copie in sola lettura. [!DNL Experience Manager]I componenti apportano modifiche non distruttive alle risorse. Non sono consentite altre modifiche.
* Le risorse recuperate localmente sono disponibili solo a scopo di authoring. I flussi di lavoro di aggiornamento delle risorse non possono essere applicati e i metadati non possono essere modificati.
* Quando si utilizza [!DNL Dynamic Media] in [!DNL Sites] pagine la risorsa originale non viene recuperata e memorizzata nell’implementazione locale. Il `dam:Asset` , i metadati e le rappresentazioni generati da [!DNL Assets] dell’implementazione vengono tutti recuperati nel [!DNL Sites] distribuzione.
* Sono supportati solo le immagini e i formati di documento elencati. [!DNL Content Fragments] e [!DNL Experience Fragments] non sono supportati.
* [!DNL Experience Manager] non recupera gli schemi di metadati. Ciò significa che potrebbero non essere visualizzati tutti i metadati recuperati. Se lo schema viene aggiornato separatamente nella [!DNL Sites] , vengono visualizzate tutte le proprietà dei metadati.
* Tutti [!DNL Sites] gli autori dispongono di autorizzazioni di lettura per le copie recuperate, anche se non possono accedere alla distribuzione remota di DAM.
* Nessun supporto API per personalizzare l’integrazione.
* Questa funzionalità supporta la ricerca e l’utilizzo diretti delle risorse remote. Per rendere disponibili molte risorse remote nell’implementazione locale con un’unica operazione, è consigliabile eseguire la migrazione delle risorse.
* Non è possibile utilizzare una risorsa remota come miniatura di pagina in [!UICONTROL Proprietà pagina] dell&#39;utente. È possibile impostare una miniatura di una pagina web in [!UICONTROL Proprietà pagina] interfaccia utente da [!UICONTROL Miniatura] facendo clic su [!UICONTROL Seleziona immagine].

### Configurazione e licenze {#setup-licensing}

* [!DNL Assets] distribuzione su [!DNL Adobe Managed Services] è supportato.
* [!DNL Sites] può connettersi a un singolo [!DNL Assets] alla volta.
* Una licenza di [!DNL Assets] è necessario lavorare come archivio remoto.
* Una o più licenze di [!DNL Sites] è necessario lavorare come implementazione di authoring locale.

### Utilizzo {#usage}

* Gli utenti possono cercare risorse remote e trascinarle sulla pagina locale durante l’authoring. Non sono supportate altre funzionalità.
* L’operazione di recupero si interrompe per timeout dopo 5 secondi. Gli autori possono rilevare dei problemi durante il recupero delle risorse, ad esempio in caso di problemi di rete. Gli autori possono riprovare trascinando la risorsa remota da [!UICONTROL Content Finder] a [!UICONTROL Editor pagina].
* Le risorse recuperate possono essere sottoposte a semplici modifiche non distruttive e alle modifiche supportate tramite il componente `Image` di Le risorse sono di sola lettura.
* L’unico metodo per recuperare nuovamente la risorsa è trascinarla su una pagina. Non è disponibile alcun supporto API o altri metodi per recuperare nuovamente una risorsa e aggiornarla.
* Se le risorse vengono disattivate da DAM, continuano a essere in uso il [!DNL Sites] pagine.
* Le voci di riferimento remote di una risorsa vengono recuperate in modo asincrono. I riferimenti e il conteggio totale non sono in tempo reale e potrebbe esserci una differenza se un [!DNL Sites] L’autore utilizza la risorsa mentre un utente DAM sta visualizzando il riferimento. Gli utenti DAM possono aggiornare la pagina e riprovare tra qualche minuto per ottenere il conteggio totale.

## Risoluzione dei problemi {#troubleshoot}

Per risolvere gli errori più comuni, effettuare le seguenti operazioni:

* Se non riesci a cercare le risorse remote dal [!UICONTROL Content Finder], quindi accertati che siano presenti i ruoli e le autorizzazioni richiesti.

* Una risorsa recuperata da DAM remoto potrebbe non essere pubblicata su una pagina web per uno o più motivi. Non esiste sul server remoto, la mancanza di autorizzazioni appropriate per recuperarlo o un errore di rete possono essere i motivi. Assicurati che la risorsa non venga rimossa da DAM remoto. Assicurati di disporre delle autorizzazioni appropriate e che i prerequisiti siano soddisfatti. Riprova ad aggiungere la risorsa alla pagina e ripubblica. Controlla l’[elenco dei processi asincroni](/help/operations/asynchronous-jobs.md) per verificare la presenza di errori nel recupero delle risorse.

* Se non riesci ad accedere all’implementazione remota di DAM dal server locale [!DNL Sites] , assicurati che i cookie tra siti siano consentiti e [supporto per cookie dello stesso sito](/help/security/same-site-cookie-support.md) è configurato. Se i cookie cross-site sono bloccati, le distribuzioni di [!DNL Experience Manager] non può autenticare. Ad esempio: [!DNL Google Chrome] in modalità di navigazione in incognito può bloccare i cookie di terze parti. Per consentire i cookie in [!DNL Chrome] , fare clic sull&#39;icona &#39;occhio&#39; nella barra degli indirizzi e passare a **Sito non funzionante** > **Bloccato**, seleziona l’URL DAM remoto e consenti il cookie token di accesso. In alternativa, vedere [come abilitare i cookie di terze parti](https://support.google.com/chrome/answer/95647).

   ![Errore di cookie nel browser Chrome in modalità di navigazione in incognito](assets/chrome-cookies-incognito-dialog.png)

* Se i riferimenti remoti non vengono recuperati e generano un messaggio di errore, verifica se [!DNL Sites] la distribuzione è disponibile e verifica la presenza di problemi di connettività di rete. Riprova più tardi per controllare. [!DNL Assets] l’implementazione tenta di stabilire la connessione due volte [!DNL Sites] e quindi segnala un errore.

   ![impossibile recuperare i riferimenti remoti delle risorse](assets/reference-report-failure.png)

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
