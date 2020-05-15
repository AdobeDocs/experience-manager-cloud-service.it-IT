---
title: Configurare e utilizzare i microservizi delle risorse per l’elaborazione delle risorse
description: Scoprite come configurare e utilizzare i microservizi di risorse nativi per il cloud per elaborare le risorse su scala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 367456bfad25a83a36ffe45e2d6092367740cd92
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 3%

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

I microservizi delle risorse forniscono un’elaborazione scalabile e resiliente delle risorse mediante i servizi cloud. Adobe gestisce i servizi per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione.

L’elaborazione delle risorse dipende dalla configurazione in Profili **[!UICONTROL di]** elaborazione, che fornisce una configurazione predefinita, e consente all’amministratore di aggiungere una configurazione di elaborazione delle risorse più specifica. Gli amministratori possono creare e mantenere le configurazioni dei flussi di lavoro post-elaborazione, inclusa la personalizzazione facoltativa. La personalizzazione dei flussi di lavoro consente estensibilità e personalizzazione completa.

I microservizi delle risorse consentono di elaborare [un&#39;ampia gamma di tipi](/help/assets/file-format-support.md) di file che coprono più formati out-of-the-box di quanto sia possibile con le versioni precedenti di Experience Manager. Ad esempio, l&#39;estrazione delle miniature dei formati PSD e PSB ora è possibile che soluzioni di terze parti come ImageMagick precedentemente richieste.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Visualizzazione di alto livello dell’](assets/asset-microservices-flow.png "elaborazione delle risorseVisualizzazione di alto livello dell’elaborazione delle risorse")

>[!NOTE]
>
> L’elaborazione delle risorse qui descritta sostituisce il modello di `DAM Update Asset` flusso di lavoro esistente nelle versioni precedenti di Experience Manager. La maggior parte della generazione di rappresentazioni standard e dei passaggi relativi ai metadati vengono sostituiti dall’elaborazione dei microservizi di risorse e gli eventuali passaggi rimanenti possono essere sostituiti dalla configurazione del flusso di lavoro di post-elaborazione.

## Introduzione all’elaborazione delle risorse {#get-started}

L’elaborazione delle risorse con i microservizi delle risorse è preconfigurata con una configurazione predefinita, che garantisce la disponibilità delle rappresentazioni predefinite richieste dal sistema. Inoltre, garantisce la disponibilità di operazioni di estrazione dei metadati e di estrazione del testo. Gli utenti possono iniziare a caricare o aggiornare immediatamente le risorse e per impostazione predefinita è disponibile l’elaborazione di base.

Per specifiche esigenze di generazione di rappresentazioni o di elaborazione delle risorse, un amministratore AEM può creare ulteriori profili [!UICONTROL di]elaborazione. Gli utenti possono assegnare uno o più dei profili disponibili a cartelle specifiche per eseguire ulteriori elaborazioni. Ad esempio, per generare rappresentazioni specifiche per Web, dispositivi mobili e tablet. Il seguente video illustra come creare e applicare profili [!UICONTROL di] elaborazione e come accedere alle rappresentazioni create.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

Per modificare il profilo esistente, vedi [configurazioni per i microservizi](#configure-asset-microservices)delle risorse.
Per creare profili di elaborazione personalizzati in base alle tue esigenze, ad esempio per l&#39;integrazione con altri sistemi, consulta Flussi di lavoro [di](#post-processing-workflows)post-elaborazione.

## Configurazioni per i microservizi di risorse {#configure-asset-microservices}

Per configurare i microservizi delle risorse, gli amministratori possono utilizzare l’interfaccia utente di configurazione in **[!UICONTROL Strumenti > Risorse > Profili]** di elaborazione.

### Configurazione predefinita {#default-config}

Con la configurazione predefinita, è configurato solo il profilo di elaborazione standard. Il profilo di elaborazione standard non è visibile nell&#39;interfaccia utente e non è possibile modificarlo. Viene sempre eseguito per elaborare le risorse caricate. Un profilo di elaborazione standard garantisce che tutte le elaborazioni di base richieste da Experience Manager siano completate su tutte le risorse.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png) -->

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

* Nome rappresentazione.
* Formato di rappresentazione supportato, ad esempio JPEG, PNG o GIF.
* Larghezza e altezza della rappresentazione in pixel. Se non viene specificato, viene usata la dimensione in pixel dell’immagine originale.
* Qualità di rappresentazione JPEG in percentuale.
* Tipi MIME inclusi ed esclusi per definire l&#39;applicabilità di un profilo.

![elaborazione-profili-aggiunta](assets/processing-profiles-adding.png)

Quando create e salvate un nuovo profilo di elaborazione, questo viene aggiunto all&#39;elenco dei profili di elaborazione configurati. Potete applicare questi profili di elaborazione alle cartelle nella gerarchia delle cartelle per renderli efficaci per il caricamento delle risorse e l’elaborazione delle risorse.

<!-- Removed per cqdoc-15624 request by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) -->

#### Larghezza e altezza della rappresentazione {#rendition-width-height}

Le specifiche relative a larghezza e altezza della rappresentazione forniscono le dimensioni massime dell’immagine di output generata. Il servizio di microservizi risorse tenta di generare la rappresentazione più grande possibile, che larghezza e altezza non sono maggiori rispettivamente di larghezza e altezza specificate. Le proporzioni vengono mantenute, ovvero sono uguali a quelle dell’originale.

Un valore vuoto indica che l&#39;elaborazione delle risorse assume la dimensione in pixel dell&#39;originale.

#### Regole di inclusione del tipo MIME {#mime-type-inclusion-rules}

Quando viene elaborata una risorsa con un tipo MIME specifico, il tipo MIME viene prima controllato rispetto al valore dei tipi MIME esclusi per la specifica di rappresentazione. Se corrisponde a tale elenco, questa rappresentazione specifica non viene generata per la risorsa (&quot;blacklist&quot;).

In caso contrario, il tipo MIME viene controllato rispetto al tipo MIME incluso e, se corrisponde all&#39;elenco, il rendering viene generato (&quot;whitelist&quot;).

#### Rappresentazioni speciali FPO {#special-fpo-rendition}

Quando inserite risorse di grandi dimensioni da AEM nei documenti Adobe InDesign, un creativo professionista deve attendere molto tempo dopo aver [inserito una risorsa](https://helpx.adobe.com/indesign/using/placing-graphics.html). Nel frattempo, all&#39;utente non è consentito utilizzare InDesign. Questo interrompe il flusso creativo e influisce negativamente sull&#39;esperienza dell&#39;utente. Adobe consente di iniziare temporaneamente a inserire rappresentazioni di piccole dimensioni nei documenti InDesign, che possono essere sostituite con risorse a risoluzione piena on-demand in un secondo momento. Experience Manager fornisce rappresentazioni utilizzate solo per il posizionamento (FPO). Tali rappresentazioni FPO hanno una dimensione file ridotta ma hanno le stesse proporzioni.

Il profilo di elaborazione può includere una rappresentazione FPO (solo per posizionamento). Consulta la [documentazione](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) di Adobe Asset Link per comprendere se è necessario attivarla per il profilo di elaborazione. Per ulteriori informazioni, consulta la documentazione [completa di](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)Adobe Asset Link.

## Utilizzare i microservizi delle risorse per elaborare le risorse {#use-asset-microservices}

Create e applicate profili di elaborazione personalizzati aggiuntivi a cartelle specifiche per Experience Manager per elaborare le risorse caricate o aggiornate in queste cartelle. Il profilo di elaborazione standard predefinito viene sempre eseguito ma non è visibile nell&#39;interfaccia utente. Se aggiungete un profilo personalizzato, entrambi i profili vengono utilizzati per elaborare le risorse caricate.

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

### Creare modelli di flussi di lavoro post-elaborazione {#create-post-processing-workflow-models}

I modelli di flusso di lavoro post-elaborazione sono modelli di flusso di lavoro AEM standard. Create modelli diversi se avete bisogno di un&#39;elaborazione diversa per diverse posizioni di repository o tipi di risorse.

Le fasi di elaborazione devono essere aggiunte in base alle esigenze. Potete utilizzare tutti i passaggi supportati disponibili, nonché eventuali passaggi di flusso di lavoro implementati personalizzati.

Assicurati che l&#39;ultimo passaggio di ogni flusso di lavoro di post-elaborazione sia `DAM Update Asset Workflow Completed Process`. L’ultimo passaggio consente a Experience Manager di sapere quando l’elaborazione delle risorse è stata completata.

### Configurare l&#39;esecuzione del flusso di lavoro di post-elaborazione {#configure-post-processing-workflow-execution}

Per configurare i modelli di flusso di lavoro post-elaborazione da eseguire per le risorse caricate o aggiornate nel sistema al termine dell’elaborazione dei microservizi di risorse, è necessario configurare il servizio Custom Workflow Runner.

Il servizio Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) è un servizio OSGi e offre due opzioni di configurazione:

* Flussi di lavoro di post-elaborazione per percorso (`postProcWorkflowsByPath`): È possibile elencare più modelli di workflow, basati su percorsi di repository diversi. I percorsi e i modelli devono essere separati da due punti. I percorsi dell&#39;archivio semplici sono supportati e devono essere mappati su un modello di workflow nel `/var` percorso. Esempio: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Flussi di lavoro di post-elaborazione per espressione (`postProcWorkflowsByExpression`): È possibile elencare più modelli di flusso di lavoro, in base a diverse espressioni regolari. Le espressioni e i modelli devono essere separati da due punti. L&#39;espressione regolare deve puntare direttamente al nodo Asset, e non a una delle rappresentazioni o dei file. Esempio: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>La configurazione di Custom Workflow Runner è una configurazione di un servizio OSGi. Consultate [Implementare in Experience Manager](/help/implementing/deploying/overview.md) per informazioni su come distribuire una configurazione OSGi.
> La console Web OSGi, a differenza delle distribuzioni di servizi locali e gestiti di AEM, non è direttamente disponibile nelle distribuzioni di servizi cloud.

Per informazioni dettagliate sul passaggio del flusso di lavoro standard da utilizzare nel flusso di lavoro di post-elaborazione, consultate i passaggi del [flusso di lavoro nel flusso di lavoro](developer-reference-material-apis.md#post-processing-workflows-steps) di post-elaborazione (in riferimento allo sviluppatore).

## Best practice e limitazioni {#best-practices-limitations-tips}

* Considerate le vostre esigenze per tutti i tipi di rappresentazioni durante la progettazione di flussi di lavoro. Se non prevedete la necessità di una rappresentazione in futuro, rimuovete il passaggio di creazione dal flusso di lavoro. Le rappresentazioni non possono essere eliminate in blocco in seguito. Le rappresentazioni indesiderate possono occupare molto spazio di archiviazione dopo un uso prolungato di [!DNL Experience Manager]. Per le singole risorse, potete rimuovere manualmente i rendering dall’interfaccia utente. Per più risorse, potete personalizzare [!DNL Experience Manager] per eliminare rappresentazioni specifiche oppure eliminare le risorse e caricarle di nuovo.
