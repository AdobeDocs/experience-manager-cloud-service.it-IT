---
title: Configurare e utilizzare i microservizi delle risorse
description: Configurate e utilizzate i microservizi delle risorse native per il cloud per elaborare le risorse su scala.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '2514'
ht-degree: 1%

---


# Utilizzare i microservizi delle risorse e i profili di elaborazione {#get-started-using-asset-microservices}

I microservizi delle risorse consentono l’elaborazione scalabile e resiliente delle risorse mediante applicazioni native per il cloud (o &quot;lavoratori&quot;).  Adobe gestisce i servizi per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione.

I microservizi delle risorse consentono di elaborare una [vasta gamma di tipi di file](/help/assets/file-format-support.md) che include più formati out-of-the-box di quanto sia possibile con le versioni precedenti di [!DNL Experience Manager]. Ad esempio, l&#39;estrazione delle miniature dei formati PSD e PSB ora è possibile che soluzioni di terze parti come ImageMagick precedentemente richieste.

L&#39;elaborazione delle risorse dipende dalla configurazione in **[!UICONTROL Profili di elaborazione]**.  Experience Manager fornisce una configurazione di base predefinita e consente agli amministratori di aggiungere una configurazione di elaborazione delle risorse più specifica. Gli amministratori creano, mantengono e modificano le configurazioni dei flussi di lavoro post-elaborazione, inclusa la personalizzazione facoltativa. La personalizzazione dei flussi di lavoro consente agli sviluppatori di ampliare l&#39;offerta predefinita.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Visualizzazione di alto livello dell’](assets/asset-microservices-flow.png "elaborazione delle risorseVisualizzazione di alto livello dell’elaborazione delle risorse")

>[!NOTE]
>
>L&#39;elaborazione delle risorse qui descritta sostituisce il modello di flusso di lavoro `DAM Update Asset` esistente nelle versioni precedenti di [!DNL Experience Manager]. La maggior parte della generazione di rappresentazioni standard e dei passaggi relativi ai metadati vengono sostituiti dall’elaborazione dei microservizi di risorse e gli eventuali passaggi rimanenti possono essere sostituiti dalla configurazione del flusso di lavoro di post-elaborazione.

## Informazioni sulle opzioni di elaborazione delle risorse {#get-started}

 Experience Manager consente i seguenti livelli di elaborazione.

| Opzione | Descrizione | Casi di utilizzo coperti |
|---|---|---|
| [Configurazione predefinita](#default-config) | È disponibile così come è e non può essere modificato. Questa configurazione fornisce funzionalità di generazione delle rappresentazioni di base. | <ul> <li>Miniature standard utilizzate dall&#39;interfaccia utente [!DNL Assets] (48, 140 e 319 pixel) </li> <li> Anteprima grande (rappresentazione Web - 1280 pixel) </li><li> Estrazione di metadati e testo.</li></ul> |
| [Configurazione personalizzata](#standard-config) | Configurato dagli amministratori tramite l&#39;interfaccia utente. Offre più opzioni per la generazione della rappresentazione, estendendo l&#39;opzione predefinita. Estendete l’opzione out-of-the-box per fornire formati e rappresentazioni diversi. | <ul><li>Rendering FPO. </li> <li>Modificare il formato file e la risoluzione delle immagini</li> <li> Applicabile in modo condizionale ai tipi di file configurati. </li> </ul> |
| [Profilo personalizzato](#custom-config) | Configurato dagli amministratori tramite l&#39;interfaccia utente per utilizzare il codice personalizzato attraverso le applicazioni personalizzate per chiamare [ Asset compute Service](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html). Supporta requisiti più complessi in un metodo scalabile e nativo per il cloud. | Vedere [casi di utilizzo consentiti](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formati di file supportati {#supported-file-formats}

I microservizi delle risorse supportano un’ampia varietà di formati di file per elaborare, generare rappresentazioni o estrarre metadati. Vedere [formati di file supportati](file-format-support.md) per l&#39;elenco completo dei tipi MIME e le funzionalità supportate per ciascun tipo.

## Configurazione predefinita {#default-config}

Alcune impostazioni predefinite sono preconfigurate per garantire la disponibilità delle rappresentazioni predefinite richieste nel  Experience Manager. La configurazione predefinita garantisce inoltre la disponibilità di operazioni di estrazione dei metadati e di estrazione del testo. Gli utenti possono iniziare a caricare o aggiornare immediatamente le risorse e per impostazione predefinita è disponibile l’elaborazione di base.

Con la configurazione predefinita, è configurato solo il profilo di elaborazione di base. Tale profilo di elaborazione non è visibile nell&#39;interfaccia utente e non è possibile modificarlo. Viene sempre eseguito per elaborare le risorse caricate. Questo profilo di elaborazione predefinito garantisce che l&#39;elaborazione di base richiesta da [!DNL Experience Manager] sia completata su tutte le risorse.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configurazione standard {#standard-config}

[!DNL Experience Manager] forniscono funzionalità per generare rappresentazioni più specifiche per i formati comuni in base alle esigenze dell&#39;utente. Un amministratore può creare [!UICONTROL Profili di elaborazione] aggiuntivi per facilitare la creazione di rappresentazioni. Gli utenti quindi assegnano uno o più dei profili disponibili a cartelle specifiche per completare l’elaborazione aggiuntiva. Ad esempio, l&#39;elaborazione aggiuntiva può generare rappresentazioni per Web, dispositivi mobili e tablet. Il seguente video illustra come creare e applicare [!UICONTROL Profili di elaborazione] e come accedere alle rappresentazioni create.

* **Larghezza e altezza** rappresentazione: Le specifiche relative a larghezza e altezza della rappresentazione forniscono le dimensioni massime dell’immagine di output generata. I microservizi risorse cercano di produrre la rappresentazione più grande possibile, che larghezza e altezza non sono maggiori rispettivamente della larghezza e dell’altezza specificate. Le proporzioni vengono mantenute, ovvero sono uguali a quelle dell’originale. Un valore vuoto indica che l&#39;elaborazione delle risorse assume la dimensione in pixel dell&#39;originale.

* **Regole** di inclusione del tipo MIME: Quando viene elaborata una risorsa con un tipo MIME specifico, il tipo MIME viene prima controllato rispetto al valore dei tipi MIME esclusi per la specifica di rappresentazione. Se corrisponde a tale elenco, questa rappresentazione specifica non viene generata per la risorsa (elenco Bloccati ). In caso contrario, il tipo MIME viene controllato rispetto al tipo MIME incluso e, se corrisponde all&#39;elenco, viene generata la rappresentazione ( elenco Consentiti).

* **Rappresentazioni** FPO speciali: Quando si inseriscono risorse di grandi dimensioni  [!DNL Experience Manager] in  [!DNL Adobe InDesign] documenti, un creativo professionista attende molto tempo dopo aver  [inserito una risorsa](https://helpx.adobe.com/indesign/using/placing-graphics.html). Nel frattempo, l&#39;utente non può utilizzare [!DNL InDesign]. Questo interrompe il flusso creativo e influisce negativamente sull&#39;esperienza dell&#39;utente.  Adobe consente di inserire temporaneamente le rappresentazioni di piccole dimensioni nei documenti [!DNL InDesign], da sostituire successivamente con risorse a risoluzione piena su richiesta. [!DNL Experience Manager] fornisce rappresentazioni utilizzate solo per il posizionamento (FPO). Tali rappresentazioni FPO hanno una dimensione file ridotta ma hanno le stesse proporzioni.

Il profilo di elaborazione può includere una rappresentazione FPO (solo per posizionamento). Per informazioni su come attivarla per il profilo di elaborazione, vedere [!DNL Adobe Asset Link] [documentazione](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html). Per ulteriori informazioni, consultate la [documentazione completa  collegamento risorse di Adobe](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html).

### Crea profilo standard {#create-standard-profile}

Per creare un profilo di elaborazione standard, effettuate le seguenti operazioni:

1. Gli amministratori accedono a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili di elaborazione]**. Fai clic su **[!UICONTROL Crea]**.
1. Specificate un nome che consenta di identificare in modo univoco il profilo quando si applica a una cartella.
1. Per generare le rappresentazioni FPO, nella scheda **[!UICONTROL Standard]** abilitare **[!UICONTROL Crea rappresentazione FPO]**. Immettete un valore **[!UICONTROL Quality]** compreso tra 1 e 100.
1. Per generare altre rappresentazioni, fate clic su **[!UICONTROL Aggiungi nuovo]** e fornite le seguenti informazioni:

   * Nome file di ogni rappresentazione.
   * Formato file (PNG, JPEG, GIF o WebP) di ciascuna rappresentazione.
   * Larghezza e altezza in pixel di ciascuna rappresentazione. Se i valori non sono specificati, viene usata la dimensione in pixel dell’immagine originale.
   * Qualità in percentuale di ciascuna rappresentazione JPEG e WebP.
   * Tipi MIME inclusi ed esclusi per definire l&#39;applicabilità di un profilo.

   ![elaborazione-profili-aggiunta](assets/processing-profiles-image.png)

1. Fai clic su **[!UICONTROL Salva]**.

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Profilo personalizzato e casi di utilizzo {#custom-config}

[!DNL Asset Compute Service] supporta una serie di casi d&#39;uso, ad esempio l&#39;elaborazione predefinita, l&#39;elaborazione  formati specifici del Adobe come i file Photoshop e l&#39;implementazione di un&#39;elaborazione personalizzata o specifica per l&#39;organizzazione. La personalizzazione del flusso di lavoro di DAM Update Asset richiesta in passato, viene gestita automaticamente o tramite la configurazione dei profili di elaborazione. Se queste opzioni di elaborazione non soddisfano le esigenze aziendali,  Adobe consiglia di sviluppare e utilizzare [!DNL Asset Compute Service] per estendere le funzionalità predefinite. Per una panoramica, vedere [comprendere l&#39;estensibilità e quando utilizzarla](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
> Adobe consiglia di utilizzare un&#39;applicazione personalizzata solo quando i requisiti aziendali non possono essere soddisfatti utilizzando le configurazioni predefinite o il profilo standard.

Può trasformare immagini, video, documenti e altri formati di file in diverse rappresentazioni, come miniature, testo estratto e metadati, nonché archivi.

Gli sviluppatori possono utilizzare [!DNL Asset Compute Service] per [creare applicazioni personalizzate](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) in grado di soddisfare i casi di utilizzo supportati. [!DNL Experience Manager] possono chiamare queste applicazioni personalizzate dall&#39;interfaccia utente utilizzando profili personalizzati che gli amministratori configurano. [!DNL Asset Compute Service] supporta i seguenti casi di utilizzo di servizi esterni:

* Utilizzate [!DNL Adobe Photoshop]&#39;s [ImageCutout API](https://github.com/AdobeDocs/photoshop-api-docs-pre-release#imagecutout) e salvate il risultato come rappresentazione.
* Chiama sistemi di terze parti per aggiornare i dati, ad esempio un sistema PIM.
* Utilizzate l&#39;API [!DNL Photoshop] per generare diverse rappresentazioni basate sul modello Photoshop.
* Utilizzate l&#39;API Lightroom [ Adobe](https://github.com/AdobeDocs/lightroom-api-docs#supported-features) per ottimizzare le risorse acquisite e salvarle come rappresentazioni.

>[!NOTE]
>
>Non potete modificare i metadati standard utilizzando le applicazioni personalizzate. Potete modificare solo i metadati personalizzati.

### Creare un profilo personalizzato {#create-custom-profile}

Per creare un profilo personalizzato, attenetevi alla procedura seguente:

1. Gli amministratori accedono a **[!UICONTROL Strumenti > Risorse > Profili di elaborazione]**. Fai clic su **[!UICONTROL Crea]**.
1. Fare clic sulla scheda **[!UICONTROL Personalizzato]**. Fare clic su **[!UICONTROL Aggiungi nuovo]**. Specificate il nome file desiderato per la rappresentazione.
1. Fornite le seguenti informazioni.

   * Nome file di ogni rappresentazione e estensione file supportata.
   * [URL punto finale di un&#39;app](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html) Firefly personalizzata. L&#39;app deve provenire dalla stessa organizzazione dell&#39;account del Experience Manager .
   * Aggiungi parametri di servizio a [trasmettere informazioni o parametri aggiuntivi all&#39;applicazione personalizzata](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend).
   * Sono inclusi ed esclusi i tipi MIME per limitare l&#39;elaborazione ad alcuni formati di file specifici.

   Fai clic su **[!UICONTROL Salva]**.

Le applicazioni personalizzate sono app [Project Firefly](https://github.com/AdobeDocs/project-firefly) senza testa. L&#39;applicazione personalizzata ottiene tutti i file forniti se sono configurati con un profilo di elaborazione. L&#39;applicazione deve filtrare i file.

>[!CAUTION]
>
>Se l&#39;app Firefly e l&#39;account [!DNL Experience Manager] non appartengono alla stessa organizzazione, l&#39;integrazione non funziona.

### Esempio di profilo personalizzato {#custom-profile-example}

Per illustrare l&#39;utilizzo del profilo personalizzato, consideriamo un caso d&#39;uso per applicare del testo personalizzato alle immagini della campagna. Potete creare un profilo di elaborazione che sfrutta l&#39;API di Photoshop per modificare le immagini.

&#39;integrazione del servizio di Asset compute consente  Experience Manager di trasmettere questi parametri all&#39;applicazione personalizzata utilizzando il campo [!UICONTROL Service Parameters]. L&#39;applicazione personalizzata chiama quindi l&#39;API Photoshop e trasmette questi valori all&#39;API. Ad esempio, potete trasmettere il nome del font, il colore del testo, lo spessore del testo e la dimensione del testo per aggiungere il testo personalizzato alle immagini della campagna.

![custom-processing-profile](assets/custom-processing-profile.png)

*Figura: Utilizzate  [!UICONTROL Service ] Parameters field per trasmettere informazioni aggiunte ai parametri predefiniti creati nell&#39;applicazione personalizzata. In questo esempio, quando le immagini della campagna vengono caricate, le immagini vengono aggiornate con il testo `Jumanji` nel font `Arial-BoldMT`.*

## Utilizzare i profili di elaborazione per elaborare le risorse{#use-profiles}

Potete creare e applicare profili di elaborazione personalizzati aggiuntivi a cartelle specifiche per  Experience Manager per elaborare le risorse caricate o aggiornate in queste cartelle. Il profilo di elaborazione standard predefinito viene sempre eseguito ma non è visibile nell&#39;interfaccia utente. Se aggiungete un profilo personalizzato, entrambi i profili vengono utilizzati per elaborare le risorse caricate.

Applicate i profili di elaborazione alle cartelle utilizzando uno dei seguenti metodi:

* Gli amministratori possono selezionare una definizione di profilo di elaborazione in **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili di elaborazione]** e utilizzare l&#39;azione **[!UICONTROL Applica profilo alle cartelle]**. Viene aperto un browser del contenuto che consente di passare a cartelle specifiche, selezionarle e confermare l’applicazione del profilo.
* Gli utenti possono selezionare una cartella nell&#39;interfaccia utente Risorse, utilizzare l&#39;azione **[!UICONTROL Proprietà]** per aprire la schermata delle proprietà della cartella, fare clic sulla scheda **[!UICONTROL Profili di elaborazione]** e, nell&#39;elenco a comparsa, selezionare il profilo di elaborazione appropriato per quella cartella. Per salvare le modifiche, fare clic su **[!UICONTROL Salva e chiudi]**.
   ![Applicazione del profilo di elaborazione a una cartella dalla scheda Proprietà risorsa](assets/folder-properties-processing-profile.png)

>[!TIP]
>
>A una cartella è possibile applicare un solo profilo di elaborazione. Per generare più rappresentazioni, aggiungi più definizioni di rappresentazione al profilo di elaborazione esistente.

Dopo aver applicato un profilo di elaborazione a una cartella, tutte le nuove risorse caricate (o aggiornate) in questa cartella o in una delle sottocartelle vengono elaborate utilizzando il profilo di elaborazione aggiuntivo configurato. Questa elaborazione si aggiunge al profilo standard predefinito.

>[!NOTE]
>
>Un profilo di elaborazione applicato a una cartella funziona per l’intera struttura ad albero, ma può essere sostituito con un altro profilo applicato a una sottocartella. Quando le risorse vengono caricate in una cartella,  Experience Manager controlla le proprietà della cartella contenitore per un profilo di elaborazione. Se non ne viene applicata alcuna, viene controllata una cartella principale nella gerarchia per verificare se è necessario applicare un profilo di elaborazione.

Per verificare che le risorse siano state elaborate, visualizzate l&#39;anteprima delle rappresentazioni generate nella vista [!UICONTROL Rappresentazioni] nella parte sinistra. Aprite l&#39;anteprima delle risorse e aprite la barra a sinistra per accedere alla vista **[!UICONTROL Rappresentazioni]**. Le rappresentazioni specifiche nel profilo di elaborazione, per le quali il tipo di risorsa specifico corrisponde alle regole di inclusione del tipo MIME, devono essere visibili e accessibili.

![rappresentazioni aggiuntive](assets/renditions-additional-renditions.png)

*Figura: Esempio di due rappresentazioni aggiuntive generate da un profilo di elaborazione applicato alla cartella principale.*

## Flussi di lavoro post-elaborazione {#post-processing-workflows}

Per situazioni in cui è necessaria un’ulteriore elaborazione delle risorse che non può essere ottenuta utilizzando i profili di elaborazione, alla configurazione possono essere aggiunti ulteriori flussi di lavoro di post-elaborazione. Questo consente di aggiungere un&#39;elaborazione completamente personalizzata al di sopra dell&#39;elaborazione configurabile tramite i microservizi delle risorse.

I flussi di lavoro post-elaborazione, se configurati, vengono eseguiti automaticamente da AEM al termine dell&#39;elaborazione dei microservizi. Non è necessario aggiungere manualmente gli avviatori del flusso di lavoro per attivarli. Gli esempi includono:

* Passaggi del flusso di lavoro personalizzati per l’elaborazione delle risorse.
* Integrazioni per aggiungere metadati o proprietà alle risorse da sistemi esterni, ad esempio informazioni su prodotti o processi.
* Elaborazione aggiuntiva eseguita da servizi esterni.

L&#39;aggiunta di una configurazione di flusso di lavoro post-elaborazione a  Experience Manager comprende i seguenti passaggi:

* Creare uno o più modelli di workflow. Nei documenti viene indicato come *modelli di flusso di lavoro post-elaborazione*, ma si tratta di modelli di flusso di lavoro  Experience Manager standard.
* A questi modelli potete aggiungere specifici passaggi del flusso di lavoro. I passaggi vengono eseguiti sulle risorse in base alla configurazione di un modello di workflow.
* Aggiungete il passaggio [!UICONTROL Flusso di lavoro aggiornamento risorse DAM Completato] alla fine. L&#39;aggiunta di questo passaggio fa sì che  Experience Manager sappia quando l&#39;elaborazione termina e la risorsa può essere contrassegnata come elaborata, ovvero *New* viene visualizzata sulla risorsa.
* Create una configurazione per il servizio Custom Workflow Runner Service che consenta di configurare l&#39;esecuzione di un modello di flusso di lavoro post-elaborazione tramite un percorso (percorso della cartella) o mediante un&#39;espressione regolare.

### Creare modelli di flusso di lavoro post-elaborazione {#create-post-processing-workflow-models}

I modelli di flusso di lavoro post-elaborazione sono modelli AEM flusso di lavoro standard. Create modelli diversi se avete bisogno di un&#39;elaborazione diversa per diverse posizioni di repository o tipi di risorse.

Le fasi di elaborazione devono essere aggiunte in base alle esigenze. Potete utilizzare tutti i passaggi supportati disponibili, nonché eventuali passaggi di flusso di lavoro implementati personalizzati.

Assicurarsi che l&#39;ultimo passaggio di ogni flusso di lavoro di post-elaborazione sia `DAM Update Asset Workflow Completed Process`. L’ultimo passaggio consente di garantire che  Experience Manager sia a conoscenza del completamento dell’elaborazione delle risorse.

### Configurare l&#39;esecuzione del flusso di lavoro post-elaborazione {#configure-post-processing-workflow-execution}

Per configurare i modelli di flusso di lavoro post-elaborazione da eseguire per le risorse caricate o aggiornate nel sistema al termine dell’elaborazione dei microservizi di risorse, è necessario configurare il servizio Custom Workflow Runner.

Il servizio Custom Workflow Runner (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) è un servizio OSGi e offre due opzioni per la configurazione:

* Flussi di lavoro di post-elaborazione per percorso (`postProcWorkflowsByPath`): È possibile elencare più modelli di workflow, basati su percorsi di repository diversi. I percorsi e i modelli devono essere separati da due punti. I percorsi dell&#39;archivio semplici sono supportati e devono essere mappati su un modello di workflow nel percorso `/var`. Esempio: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Flussi di lavoro di post-elaborazione per espressione (`postProcWorkflowsByExpression`): È possibile elencare più modelli di flusso di lavoro, in base a diverse espressioni regolari. Le espressioni e i modelli devono essere separati da due punti. L&#39;espressione regolare deve puntare direttamente al nodo Asset, e non a una delle rappresentazioni o dei file. Esempio: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>La configurazione di Custom Workflow Runner è una configurazione di un servizio OSGi. Per informazioni su come distribuire una configurazione OSGi, vedere [distribuire a  Experience Manager](/help/implementing/deploying/overview.md).
>La console Web OSGi, a differenza delle distribuzioni di AEM di servizi locali e gestiti, non è direttamente disponibile nelle distribuzioni di servizi cloud.

Per informazioni dettagliate sul passaggio del flusso di lavoro standard da utilizzare nel flusso di lavoro di post-elaborazione, consultate [passaggi del flusso di lavoro nel flusso di lavoro di post-elaborazione](developer-reference-material-apis.md#post-processing-workflows-steps) nel riferimento per lo sviluppatore.

## Best practice e limitazioni {#best-practices-limitations-tips}

* Considerate le vostre esigenze per tutti i tipi di rappresentazioni durante la progettazione di flussi di lavoro. Se non prevedete la necessità di una rappresentazione in futuro, rimuovete il passaggio di creazione dal flusso di lavoro. Le rappresentazioni non possono essere eliminate in blocco in seguito. Le rappresentazioni indesiderate possono occupare molto spazio di archiviazione dopo un uso prolungato di [!DNL Experience Manager]. Per le singole risorse, potete rimuovere manualmente i rendering dall’interfaccia utente. Per più risorse, potete personalizzare [!DNL Experience Manager] per eliminare rappresentazioni specifiche oppure eliminare le risorse e caricarle di nuovo.
* Al momento, il supporto è limitato alla generazione di rappresentazioni. La generazione di nuova risorsa non è supportata.

>[!MORELIKETHIS]
>
>* [Introduzione a  Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html).
>* [Comprendere l&#39;estensibilità e quando utilizzarla](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).
>* [Come creare applicazioni](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) personalizzate.
>* [Tipi MIME supportati per vari casi](/help/assets/file-format-support.md) di utilizzo.


<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
