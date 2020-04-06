---
title: Configurare e utilizzare i microservizi delle risorse per l’elaborazione delle risorse
description: Scoprite come configurare e utilizzare i microservizi di risorse nativi per il cloud per elaborare le risorse su scala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

---


# Introduzione all’utilizzo dei microservizi per le risorse {#get-started-using-asset-microservices}

<!--

* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.

-->

I microservizi delle risorse forniscono un’elaborazione scalabile e resiliente delle risorse tramite i servizi cloud, gestiti da Adobe per la gestione ottimale di diversi tipi di risorse e opzioni di elaborazione.

L’elaborazione delle risorse viene eseguita in base alla configurazione in Profili **[!UICONTROL di]** elaborazione, che fornisce una configurazione predefinita, e consente all’amministratore di aggiungere una configurazione di elaborazione delle risorse più specifica. Per consentire l’estensibilità e la personalizzazione completa, l’elaborazione delle risorse consente una configurazione opzionale dei flussi di lavoro post-elaborazione, che vengono quindi creati e mantenuti dall’amministratore.

Di seguito viene illustrato un flusso di alto livello per l’elaborazione delle risorse in Experience Manager come servizio Cloud.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![asset-microservices-flow](assets/asset-microservices-flow.png)

>[!NOTE]
>
> Per i clienti che si aggiornano dalle versioni precedenti di Experience Manager, l’elaborazione delle risorse descritta in questa sezione sostituisce il modello di flusso di lavoro &quot;DAM Update Asset&quot; utilizzato per l’elaborazione dell’assimilazione delle risorse in precedenza. La maggior parte della generazione di rappresentazioni standard e dei passaggi relativi ai metadati vengono sostituiti dall’elaborazione dei microservizi di risorse e gli eventuali passaggi rimanenti possono essere sostituiti dalla configurazione del flusso di lavoro di post-elaborazione.

## Introduzione all’elaborazione delle risorse {#get-started}

L’elaborazione delle risorse con i microservizi delle risorse è preconfigurata con una configurazione predefinita, che garantisce la disponibilità delle rappresentazioni predefinite richieste dal sistema. Inoltre, garantisce la disponibilità di operazioni di estrazione dei metadati e di estrazione del testo. Gli utenti possono iniziare a caricare o aggiornare immediatamente le risorse e per impostazione predefinita è disponibile l’elaborazione di base.

Per specifiche esigenze di generazione di rappresentazioni o di elaborazione delle risorse, un amministratore AEM può creare ulteriori profili [!UICONTROL di]elaborazione. Gli utenti possono assegnare uno o più dei profili disponibili a cartelle specifiche per eseguire ulteriori elaborazioni. Ad esempio, per generare rappresentazioni specifiche per Web, dispositivi mobili e tablet. Il seguente video illustra come creare e applicare profili [!UICONTROL di] elaborazione e come accedere alle rappresentazioni create.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

Per modificare il profilo esistente, vedi [configurazioni per i microservizi](#configure-asset-microservices)delle risorse.
Per creare profili di elaborazione personalizzati in base alle tue esigenze, ad esempio per l&#39;integrazione con altri sistemi, consulta Flussi di lavoro [di](#post-processing-workflows)post-elaborazione.

## Configurazioni per i microservizi di risorse {#configure-asset-microservices}

Per configurare i microservizi delle risorse, gli amministratori possono utilizzare l’interfaccia utente di configurazione in **[!UICONTROL Strumenti > Risorse > Profili]** di elaborazione.

### Configurazione predefinita {#default-config}

Con la configurazione predefinita, è configurato solo il profilo di elaborazione [!UICONTROL standard] . Si tratta di un elemento incorporato e non può essere modificato. Viene sempre eseguito per garantire che tutte le elaborazioni richieste dall&#39;applicazione siano effettuate.

![processing-profile-standard](assets/processing-profiles-standard.png)

Il profilo di elaborazione standard fornisce la seguente configurazione di elaborazione:

* Miniature standard utilizzate dall’interfaccia utente di Asset (48, 140 e 319 px)
* Anteprima grande (rappresentazione Web - 1280 px)
* Estrazione di metadati
* Estrazione del testo

### Formati di file supportati {#supported-file-formats}

I microservizi delle risorse supportano un’ampia varietà di formati di file in termini di capacità di generare rappresentazioni o estrarre metadati. Consultate Formati [di file](file-format-support.md) supportati per l’elenco completo.

### Aggiunta di ulteriori profili di elaborazione {#processing-profiles}

È possibile aggiungere altri profili di elaborazione utilizzando l&#39;azione **[!UICONTROL Crea]** .

Ogni configurazione di profilo di elaborazione include un elenco di rappresentazioni. Per ogni rappresentazione, potete specificare quanto segue:

* nome rappresentazione
* formato di rappresentazione (sono supportati JPEG, PNG o GIF)
* larghezza e altezza della rappresentazione in pixel (se non specificata, si assume la dimensione in pixel dell’originale)
* qualità di rappresentazione (per JPEG) in percentuale
* I tipi MIME inclusi ed esclusi definiscono, a quali tipi di risorse si applica il profilo di elaborazione

![elaborazione-profili-aggiunta](assets/processing-profiles-adding.png)

Quando viene salvato un nuovo profilo di elaborazione, questo viene aggiunto all&#39;elenco dei profili di elaborazione configurati. Questi profili di elaborazione possono quindi essere applicati alle cartelle nella gerarchia delle cartelle per renderli efficaci per i caricamenti delle risorse e le risorse effettuate in tale cartella.

![processing-profile-list](assets/processing-profiles-list.png)

#### Larghezza e altezza della rappresentazione {#rendition-width-height}

Le specifiche relative a larghezza e altezza della rappresentazione forniscono le dimensioni massime dell’immagine di output generata. Il servizio di microservizi risorse tenta di generare la rappresentazione più grande possibile, che larghezza e altezza non sono maggiori rispettivamente di larghezza e altezza specificate. Le proporzioni vengono mantenute, ovvero sono uguali a quelle dell’originale.

Un valore vuoto indica che l&#39;elaborazione delle risorse assume la dimensione in pixel dell&#39;originale.

#### Regole di inclusione del tipo MIME {#mime-type-inclusion-rules}

Quando viene elaborata una risorsa con un tipo MIME specifico, il tipo MIME viene prima controllato rispetto al valore dei tipi MIME esclusi per la specifica di rappresentazione. Se corrisponde a tale elenco, questa rappresentazione specifica non viene generata per la risorsa (&quot;blacklist&quot;).

In caso contrario, il tipo MIME viene controllato rispetto al tipo MIME incluso e, se corrisponde all&#39;elenco, il rendering viene generato (&quot;whitelist&quot;).

#### Rappresentazioni speciali FPO {#special-fpo-rendition}

Il profilo di elaborazione può includere una speciale &quot;rappresentazione FPO&quot;, utilizzata quando si utilizza [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) con Adobe InDesign per inserire collegamenti diretti alle risorse da Experience Manager nei documenti InDesign.

Per informazioni su come attivarla per il profilo di elaborazione, consulta la [documentazione](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) di Adobe Asset Link.

## Utilizzare i microservizi delle risorse per elaborare le risorse {#use-asset-microservices}

Una volta creati ulteriori profili di elaborazione, questi devono essere applicati a cartelle specifiche affinché Experience Manager possa utilizzarli nell’elaborazione delle risorse per le risorse caricate o aggiornate in tali cartelle. Il profilo di elaborazione standard integrato viene sempre eseguito.

Esistono due modi per applicare i profili di elaborazione alle cartelle:

* Gli amministratori possono selezionare una definizione di profilo di elaborazione in **[!UICONTROL Strumenti > Risorse > Profili]** di elaborazione e utilizzare l&#39;azione **[!UICONTROL Applica profilo alle cartelle]** . Viene aperto un browser del contenuto che consente di passare a cartelle specifiche, selezionarle e confermare l’applicazione del profilo.
* Gli utenti possono selezionare una cartella nell’interfaccia utente Assets, utilizzare l’azione **[!UICONTROL Proprietà]** per aprire la schermata delle proprietà della cartella, fare clic sulla scheda **[!UICONTROL Profili di elaborazione]** e, nel menu a discesa, selezionare il profilo di elaborazione corretto per tale cartella. L’opzione viene salvata dopo l’azione **[!UICONTROL Salva e chiudi]**.

>[!NOTE]
>
>A una cartella specifica può essere applicato un solo profilo di elaborazione. Se avete bisogno di più rappresentazioni generate, potete aggiungere al profilo di elaborazione ulteriori definizioni delle rappresentazioni.

Dopo aver applicato un profilo di elaborazione a una cartella, tutte le nuove risorse caricate (o aggiornate) in questa cartella o in una delle sottocartelle vengono elaborate utilizzando il profilo di elaborazione aggiuntivo configurato. Questa ulteriore elaborazione si aggiunge al profilo standard predefinito. Se applicate più profili a una cartella, le risorse caricate o aggiornate vengono elaborate utilizzando ciascuno di questi profili.

>[!NOTE]
>
>Quando le risorse vengono caricate in una cartella, Experience Manager controlla le proprietà della cartella contenitore per un profilo di elaborazione. Se non ne viene applicata alcuna, la cartella viene visualizzata nella struttura delle cartelle finché non trova un profilo di elaborazione applicato e la utilizza per la risorsa. Ciò significa che un profilo di elaborazione applicato a una cartella funziona per l’intera struttura ad albero, ma può essere sostituito con un altro profilo applicato a una sottocartella.

Gli utenti possono verificare che l’elaborazione sia stata eseguita aprendo una risorsa appena caricata per la quale l’elaborazione è stata completata, aprendo l’anteprima della risorsa e facendo clic sulla vista **[!UICONTROL Rappresentazioni]** della barra a sinistra. Le rappresentazioni specifiche nel profilo di elaborazione, per le quali il tipo di risorsa specifico corrisponde alle regole di inclusione del tipo MIME, devono essere visibili e accessibili.

![rappresentazioni](assets/renditions-additional-renditions.png)*aggiuntive Figura: Esempio di due rappresentazioni aggiuntive generate da un profilo di elaborazione applicato alla cartella principale*

## Flussi di lavoro di post-elaborazione {#post-processing-workflows}

Per situazioni in cui è necessaria un’ulteriore elaborazione delle risorse che non può essere ottenuta utilizzando i profili di elaborazione, alla configurazione possono essere aggiunti ulteriori flussi di lavoro di post-elaborazione. Questo consente di aggiungere un&#39;elaborazione completamente personalizzata al di sopra dell&#39;elaborazione configurabile tramite i microservizi delle risorse.

I flussi di lavoro di post-elaborazione, se configurati, vengono eseguiti automaticamente da AEM al termine dell&#39;elaborazione dei microservizi. Non è necessario aggiungere manualmente gli avviatori del flusso di lavoro per attivarli.

Alcuni esempi:

* passaggi di flusso di lavoro personalizzati per l’elaborazione delle risorse, ad esempio codice Java per generare rappresentazioni da formati file proprietari.
* integrazioni per aggiungere metadati o proprietà alle risorse provenienti da sistemi esterni, ad esempio informazioni su prodotti o processi.
* elaborazione aggiuntiva eseguita da servizi esterni

L’aggiunta di una configurazione di flusso di lavoro post-elaborazione a Experience Manager comporta i seguenti passaggi:

* Creazione di uno o più modelli di workflow. Li chiameremo &quot;modelli di flusso di lavoro post-elaborazione&quot;, ma sono normali modelli di flusso di lavoro AEM.
* Aggiunta di passaggi di flusso di lavoro specifici a questi modelli. Questi passaggi verranno eseguiti sulle risorse in base alla configurazione del modello di workflow.
* L&#39;ultimo passo di tale modello deve essere il `DAM Update Asset Workflow Completed Process` passo. Questo è necessario per garantire che AEM sia a conoscenza del termine dell’elaborazione e che la risorsa possa essere contrassegnata come elaborata (&quot;Nuovo&quot;)
* Creazione di una configurazione per il servizio Custom Workflow Runner, che consente di configurare l&#39;esecuzione di un modello di flusso di lavoro post-elaborazione in base al percorso (percorso della cartella) o all&#39;espressione regolare

### Creazione di modelli di flusso di lavoro post-elaborazione

I modelli di flusso di lavoro post-elaborazione sono modelli di flusso di lavoro AEM standard. Se è necessaria un&#39;elaborazione diversa per diverse posizioni di repository o tipi di risorse, è necessario crearne di diversi.

Le fasi di elaborazione devono essere aggiunte in base alle esigenze. Potete utilizzare tutti i passaggi out-of-the-box supportati disponibili, nonché qualsiasi passaggio di flusso di lavoro implementato personalizzati.

L&#39;ultimo passaggio di ciascuno dei flussi di lavoro di post-elaborazione deve essere il `DAM Update Asset Workflow Completed Process`. In questo modo la risorsa verrà contrassegnata correttamente come &quot;elaborazione completata&quot;.

### Configurazione dell&#39;esecuzione del flusso di lavoro di post-elaborazione

Per configurare i modelli di flusso di lavoro post-elaborazione da eseguire per le risorse caricate o aggiornate nel sistema al termine dell’elaborazione dei microservizi di risorse, è necessario configurare il servizio Custom Workflow Runner.

Il servizio Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) è un servizio OSGi e offre due opzioni di configurazione:

* Flussi di lavoro di post-elaborazione per percorso (`postProcWorkflowsByPath`): È possibile elencare più modelli di workflow, basati su percorsi di repository diversi. I percorsi e i modelli devono essere separati da due punti. I percorsi dell&#39;archivio semplici sono supportati e devono essere mappati su un modello di workflow nel `/var` percorso. Esempio: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Flussi di lavoro di post-elaborazione per espressione (`postProcWorkflowsByExpression`): È possibile elencare più modelli di flusso di lavoro, in base a diverse espressioni regolari. Le espressioni e i modelli devono essere separati da due punti. L&#39;espressione regolare deve puntare direttamente al nodo Asset, e non a una delle rappresentazioni o dei file. Esempio: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>La configurazione di Custom Workflow Runner è una configurazione di un servizio OSGi. Consultate [Implementare in Experience Manager](/help/implementing/deploying/overview.md) per informazioni su come distribuire una configurazione OSGi.
> La console Web OSGi, a differenza delle distribuzioni di servizi locali e gestiti di AEM, non è direttamente disponibile nelle distribuzioni di servizi cloud.

Per informazioni dettagliate, su quale delle fasi standard del flusso di lavoro può essere utilizzata nel flusso di lavoro di post-elaborazione, consultate la procedura [Flusso di lavoro nel flusso di lavoro](developer-reference-material-apis.md#post-processing-workflows-steps) di post-elaborazione (in riferimento allo sviluppatore).
