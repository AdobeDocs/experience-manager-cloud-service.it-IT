---
title: Configurare e utilizzare i microservizi per le risorse
description: Configura e utilizza i microservizi per le risorse native per il cloud per elaborare le risorse su larga scala.
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Asset Processing
role: Architect,Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 3%

---

# Utilizzare i microservizi delle risorse e i profili di elaborazione {#get-started-using-asset-microservices}

I microservizi per le risorse forniscono un’elaborazione scalabile e resiliente delle risorse utilizzando applicazioni native per il cloud (denominate anche processi di lavoro). Adobe gestisce i servizi per una gestione ottimale di diversi tipi di risorse e opzioni di elaborazione.

I microservizi per le risorse consentono di elaborare una [ampia gamma di tipi di file](/help/assets/file-format-support.md) che includono più formati pronti all’uso di quanto sia possibile con le versioni precedenti di [!DNL Experience Manager]. Ad esempio, è ora possibile estrarre le miniature dai formati PSD e PSB, ma in precedenza richiedevano soluzioni di terze parti come [!DNL ImageMagick].

L’elaborazione delle risorse dipende dalla configurazione in **[!UICONTROL Profili elaborazione]**. In questo Experience Manager viene fornita una configurazione di base predefinita che consente agli amministratori di aggiungere una configurazione di elaborazione delle risorse più specifica. Gli amministratori possono creare, gestire e modificare le configurazioni dei flussi di lavoro di post-elaborazione, inclusa la personalizzazione facoltativa. La personalizzazione dei flussi di lavoro consente agli sviluppatori di estendere l’offerta predefinita.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Una visione di alto livello dell’elaborazione delle risorse](assets/asset-microservices-flow.png "Una visione di alto livello dell’elaborazione delle risorse")

>[!NOTE]
>
>L’elaborazione delle risorse qui descritta sostituisce la `DAM Update Asset` modello di workflow esistente nelle versioni precedenti di [!DNL Experience Manager]. La maggior parte dei passaggi standard relativi alla generazione di rendering e ai metadati vengono sostituiti dall’elaborazione dei microservizi per le risorse; i passaggi rimanenti, se presenti, possono essere sostituiti dalla configurazione del flusso di lavoro di post-elaborazione.

## Comprendere le opzioni di elaborazione delle risorse {#get-started}

[!DNL Experience Manager] consente i seguenti livelli di elaborazione.

| Opzione | Descrizione | Casi d’uso trattati |
|---|---|---|
| [Configurazione predefinita](#default-config) | È disponibile così com’è e non può essere modificato. Questa configurazione fornisce funzionalità di base per la generazione delle rappresentazioni. | <ul> <li>Miniature standard utilizzate da [!DNL Assets] (48, 140 e 319 pixel) </li> <li> Anteprima grande (rappresentazione web - 1280 pixel) </li><li> Estrazione di metadati e testo.</li></ul> |
| [Configurazione personalizzata](#standard-config) | Configurato dagli amministratori tramite l’interfaccia utente di. Fornisce ulteriori opzioni per la generazione della copia trasformata estendendo l&#39;opzione predefinita. Estendi l’opzione predefinita per fornire formati e rappresentazioni diversi. | <ul><li>Rendering FPO. </li> <li>Modificare il formato e la risoluzione delle immagini</li> <li> Applicabile in modo condizionale ai tipi di file configurati. </li> </ul> |
| [Profilo personalizzato](#custom-config) | Configurato dagli amministratori tramite l’interfaccia utente per utilizzare il codice personalizzato tramite applicazioni personalizzate da chiamare [Servizio Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html). Supporta requisiti più complessi in un metodo scalabile e nativo per il cloud. | Consulta [casi d’uso consentiti](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formati di file supportati {#supported-file-formats}

I microservizi per le risorse supportano un’ampia varietà di formati di file per elaborare, generare rappresentazioni o estrarre metadati. Consulta [formati di file supportati](file-format-support.md) per l’elenco completo dei tipi MIME e delle funzionalità supportate per ciascun tipo.

## Configurazione predefinita {#default-config}

Alcune impostazioni predefinite sono preconfigurate per garantire la disponibilità delle rappresentazioni predefinite richieste in Experience Manager. La configurazione predefinita garantisce anche la disponibilità delle operazioni di estrazione dei metadati e del testo. Gli utenti possono iniziare a caricare o aggiornare le risorse immediatamente e l’elaborazione di base è disponibile per impostazione predefinita.

Con la configurazione predefinita, viene configurato solo il profilo di elaborazione di base. Tale profilo di elaborazione non è visibile nell’interfaccia utente e non è possibile modificarlo. Viene sempre eseguito per elaborare le risorse caricate. Tale profilo di elaborazione predefinito garantisce che l’elaborazione di base richiesta da [!DNL Experience Manager] viene completato su tutte le risorse.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configurazione standard {#standard-config}

[!DNL Experience Manager] fornisce funzionalità per generare rappresentazioni più specifiche per i formati comuni in base alle esigenze dell’utente. Un amministratore può creare ulteriori [!UICONTROL Profili elaborazione] per facilitare la creazione di tali copie trasformate. Gli utenti assegnano quindi uno o più profili disponibili a cartelle specifiche per eseguire l’elaborazione aggiuntiva. Ad esempio, l’elaborazione aggiuntiva può generare rappresentazioni per web, dispositivi mobili e tablet. Il video seguente illustra come creare e applicare [!UICONTROL Profili elaborazione] e come accedere alle rappresentazioni create.

* **Larghezza e altezza della rappresentazione**: le specifiche di larghezza e altezza della rappresentazione forniscono le dimensioni massime dell’immagine generata. I microservizi per le risorse tentano di produrre la rappresentazione più grande possibile, con larghezza e altezza non superiori a quelle specificate, rispettivamente. Le proporzioni vengono mantenute, ovvero sono identiche a quelle dell&#39;originale. Un valore vuoto indica che l’elaborazione delle risorse assume la dimensione in pixel dell’originale.

* **Regole di inclusione del tipo MIME**: quando viene elaborata una risorsa con un tipo MIME specifico, il tipo MIME viene prima controllato rispetto al valore dei tipi MIME esclusi per la specifica della rappresentazione. Se corrisponde a tale elenco, la rappresentazione specifica non viene generata per la risorsa (elenco Bloccati). In caso contrario, il tipo MIME viene confrontato con il tipo MIME incluso e, se corrisponde all’elenco, viene generata la rappresentazione (elenco Consentiti).

* **Rendering FPO speciale**: quando si inseriscono risorse di grandi dimensioni da [!DNL Experience Manager] in [!DNL Adobe InDesign] documenti, un professionista del settore creativo attende per un periodo di tempo considerevole [inserire una risorsa](https://helpx.adobe.com/indesign/using/placing-graphics.html). Nel frattempo, l’utente non può utilizzare [!DNL InDesign]. Questo interrompe il flusso creativo e influisce negativamente sull’esperienza utente. Adobe consente di inserire temporaneamente rappresentazioni di piccole dimensioni in [!DNL InDesign] documenti iniziali, che possono essere sostituiti in seguito da risorse a risoluzione completa su richiesta. [!DNL Experience Manager] fornisce copie trasformate utilizzate solo per il posizionamento (FPO). Queste copie trasformate FPO hanno dimensioni di file ridotte ma hanno le stesse proporzioni.

Il profilo di elaborazione può includere una rappresentazione FPO (solo per posizionamento). Consulta [!DNL Adobe Asset Link] [documentazione](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) per capire se è necessario attivarlo per il profilo di elaborazione. Per ulteriori informazioni, consulta [Documentazione completa di Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html).

### Creare un profilo standard {#create-standard-profile}

Per creare un profilo di elaborazione standard, effettuare le seguenti operazioni:

1. Accesso degli amministratori **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili elaborazione]**. Fai clic su **[!UICONTROL Crea]**.
1. Specifica un nome che ti aiuti a identificare in modo univoco il profilo quando applichi a una cartella.
1. Per generare rappresentazioni FPO, nella **[!UICONTROL Immagine]** , abilita **[!UICONTROL Crea rappresentazione FPO]**. Input a **[!UICONTROL Qualità]** valore da 1 a 100.
1. Per generare altre rappresentazioni, fai clic su **[!UICONTROL Aggiungi nuovo]** e fornisci le seguenti informazioni:

   * Nome file di ciascuna rappresentazione.
   * Formato file (PNG, JPEG, GIF o WebP) di ciascuna copia trasformata.
   * Larghezza e altezza in pixel di ciascuna rappresentazione. Se i valori non sono specificati, viene utilizzata la dimensione in pixel completa dell&#39;immagine originale.
   * Qualità in percentuale di ogni rappresentazione di JPEG e WebP.
   * Tipi MIME inclusi ed esclusi per definire l’applicabilità di un profilo.

   ![processing-profiles-adding](assets/processing-profiles-image.png)

1. Fai clic su **[!UICONTROL Salva]**.

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Profilo personalizzato e casi d’uso {#custom-config}

Il [!DNL Asset Compute Service] supporta diversi casi d’uso, ad esempio elaborazione predefinita, elaborazione di formati specifici degli Adobi come i file Photoshop e implementazione di un’elaborazione personalizzata o specifica per l’organizzazione. La personalizzazione del flusso di lavoro Risorsa di aggiornamento DAM richiesta in passato viene gestita automaticamente o tramite l’elaborazione della configurazione dei profili. Se queste opzioni di elaborazione non soddisfano le esigenze aziendali, Adobe consiglia di sviluppare e utilizzare [!DNL Asset Compute Service] per estendere le funzionalità predefinite. Per una panoramica, vedi [comprendere l’estensibilità e quando utilizzarla](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
>L’Adobe consiglia di utilizzare un’applicazione personalizzata solo quando i requisiti aziendali non possono essere soddisfatti utilizzando le configurazioni predefinite o il profilo standard.

Può trasformare immagini, video, documenti e altri formati di file in diverse rappresentazioni, tra cui miniature, testo e metadati estratti e archivi.

Gli sviluppatori possono utilizzare [!DNL Asset Compute Service] a [creare applicazioni personalizzate](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) per i casi d’uso supportati. [!DNL Experience Manager] può richiamare queste applicazioni personalizzate dall’interfaccia utente utilizzando i profili personalizzati configurati dagli amministratori. [!DNL Asset Compute Service] supporta i seguenti casi d’uso per l’utilizzo di servizi esterni:

* Utilizzare [!DNL Adobe Photoshop]di [API ImageCutout](https://developer.adobe.com/photoshop/photoshop-api-docs/) e salvare il risultato come rappresentazione.
* Chiama i sistemi di terze parti per aggiornare i dati, ad esempio un sistema PIM.
* Utilizzare [!DNL Photoshop] API per generare diverse rappresentazioni basate sul modello Photoshop.
* Utilizzare [API ADOBE LIGHTROOM](https://developer.adobe.com/photoshop/photoshop-api-docs/) per ottimizzare le risorse acquisite e salvarle come rappresentazioni.

>[!NOTE]
>
>Non è possibile modificare i metadati standard utilizzando le applicazioni personalizzate. Puoi modificare solo i metadati personalizzati.

### Creare un profilo personalizzato {#create-custom-profile}

Per creare un profilo personalizzato, segui questi passaggi:

1. Accesso degli amministratori **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili elaborazione]**. Fai clic su **[!UICONTROL Crea]**.
1. Clic **[!UICONTROL Personalizzato]** scheda. Clic **[!UICONTROL Aggiungi nuovo]**. Specifica il nome file desiderato per la rappresentazione.
1. Fornisci le seguenti informazioni.

   * Nome file di ciascuna copia trasformata e estensione di file supportata.
   * [URL finale di un’app personalizzata di App Builder](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html). L’app deve appartenere alla stessa organizzazione dell’account di Experience Manager.
   * Aggiungi parametri servizio a [trasmettere informazioni o parametri aggiuntivi all’applicazione personalizzata](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend).
   * Tipi MIME inclusi ed esclusi per limitare l’elaborazione ad alcuni formati di file specifici.

   Fai clic su **[!UICONTROL Salva]**.

Le applicazioni personalizzate sono headless [Generatore di app di Project](https://developer.adobe.com/app-builder/docs/overview/) app. L’applicazione personalizzata ottiene tutti i file forniti se sono configurati con un profilo di elaborazione. L&#39;applicazione deve filtrare i file.

>[!CAUTION]
>
>Se l’app di App Builder e [!DNL Experience Manager] non appartengono alla stessa organizzazione, l’integrazione non funziona.

### Esempio di profilo personalizzato {#custom-profile-example}

Per illustrare l’utilizzo del profilo personalizzato, consideriamo un caso d’uso per applicare del testo personalizzato alle immagini della campagna. Puoi creare un profilo di elaborazione che utilizza l’API Photoshop per modificare le immagini.

L’integrazione del servizio Asset compute consente ad Experience Manager di trasmettere questi parametri all’applicazione personalizzata utilizzando [!UICONTROL Parametri del servizio] campo. L’applicazione personalizzata chiama quindi l’API di Photoshop e trasmette questi valori all’API. Ad esempio, puoi passare il nome del font, il colore del testo, lo spessore e la dimensione del testo per aggiungere il testo personalizzato alle immagini della campagna.

<!-- TBD: Check screenshot against the interface. -->

![custom-processing-profile](assets/custom-processing-profile.png)

*Figura: Uso [!UICONTROL Parametri del servizio] campo per trasmettere informazioni aggiunte ai parametri predefiniti generati nell’applicazione personalizzata. In questo esempio, quando vengono caricate le immagini della campagna, queste vengono aggiornate con `Jumanji` testo in `Arial-BoldMT` font.*

## Utilizzare i profili di elaborazione per elaborare le risorse {#use-profiles}

Crea e applica i profili di elaborazione aggiuntivi e personalizzati a cartelle specifiche, ad Experience Manager per elaborare le risorse caricate o aggiornate in queste cartelle. Il profilo di elaborazione standard predefinito viene sempre eseguito ma non è visibile nell’interfaccia utente. Se aggiungi un profilo personalizzato, entrambi i profili vengono utilizzati per elaborare le risorse caricate.

Applica i profili di elaborazione alle cartelle utilizzando uno dei metodi seguenti:

* Gli amministratori possono selezionare una definizione di profilo di elaborazione in **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili elaborazione]**, e utilizzare **[!UICONTROL Applica profilo alle cartelle]** azione. Viene aperto un browser dei contenuti che consente di passare a cartelle specifiche, selezionarle e confermare l’applicazione del profilo.
* Gli utenti possono selezionare una cartella nell’interfaccia utente di Assets, utilizzare **[!UICONTROL Proprietà]** per aprire la schermata delle proprietà della cartella, fare clic sul pulsante **[!UICONTROL Elaborazione risorse]** e nella scheda [!UICONTROL Profilo di elaborazione] selezionare il profilo di elaborazione appropriato per la cartella. Per salvare le modifiche, fai clic su **[!UICONTROL Salva e chiudi]**.
  ![Applicare il profilo di elaborazione a una cartella dalla scheda Proprietà risorsa](assets/folder-properties-processing-profile.png)

* Per applicare un profilo di elaborazione, gli utenti possono selezionare cartelle o risorse specifiche nell’interfaccia utente di Assets, quindi selezionare ![icona rielabora risorse](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL Rielabora risorse]** tra le opzioni disponibili nella parte superiore.

>[!TIP]
>
>A una cartella è possibile applicare un solo profilo di elaborazione. Per generare più rappresentazioni, aggiungi altre definizioni di rappresentazione al profilo di elaborazione esistente.

Dopo aver applicato un profilo di elaborazione a una cartella, tutte le nuove risorse caricate (o aggiornate) in questa cartella o in una delle sue sottocartelle vengono elaborate utilizzando il profilo di elaborazione aggiuntivo configurato. Questa elaborazione si aggiunge al profilo predefinito standard.

>[!NOTE]
>
>Un profilo di elaborazione applicato a una cartella funziona per l’intera struttura, ma può essere sostituito con un altro profilo applicato a una sottocartella. Quando le risorse vengono caricate in una cartella, Experience Manager controlla le proprietà della cartella contenitore per individuare un profilo di elaborazione. Se nessun profilo è applicato, viene selezionata una cartella principale nella gerarchia per un profilo di elaborazione da applicare.

Per verificare che le risorse siano elaborate, visualizza l’anteprima delle rappresentazioni generate nel [!UICONTROL Rappresentazioni] nella barra a sinistra. Apri l’anteprima della risorsa e apri la barra a sinistra per accedere al **[!UICONTROL Rappresentazioni]** visualizzazione. Le rappresentazioni specifiche nel profilo di elaborazione, per le quali il tipo di risorsa specifica corrisponde alle regole di inclusione del tipo MIME, devono essere visibili e accessibili.

![rappresentazioni aggiuntive](assets/renditions-additional-renditions.png)

*Figura: Esempio di due rappresentazioni aggiuntive generate da un profilo di elaborazione applicato alla cartella principale.*

## Workflow di post-elaborazione {#post-processing-workflows}

In una situazione in cui è necessaria un’elaborazione aggiuntiva delle risorse che non può essere ottenuta utilizzando i profili di elaborazione, è possibile aggiungere alla configurazione ulteriori flussi di lavoro di post-elaborazione. La post-elaborazione consente di aggiungere un’elaborazione completamente personalizzata oltre a quella configurabile utilizzando i microservizi per le risorse.

flussi di lavoro di post-elaborazione, oppure [Avvia flusso di lavoro automaticamente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/auto-start-workflows.html), se configurata, viene eseguita automaticamente da [!DNL Experience Manager] al termine dell’elaborazione da parte dei microservizi. Non è necessario aggiungere manualmente moduli di avvio dei flussi di lavoro per attivarli. Gli esempi includono:

* Passaggi personalizzati del flusso di lavoro per elaborare le risorse.
* Integrazioni per aggiungere metadati o proprietà alle risorse da sistemi esterni, ad esempio informazioni su prodotti o processi.
* Elaborazione aggiuntiva eseguita da servizi esterni.

Per aggiungere una configurazione del flusso di lavoro di post-elaborazione a [!DNL Experience Manager], effettua le seguenti operazioni:

* Crea uno o più modelli di flusso di lavoro. Questi modelli personalizzati sono denominati *modelli di flusso di lavoro di post-elaborazione* in questa documentazione. Questi sono regolari [!DNL Experience Manager] modelli di workflow.
* Aggiungi i passaggi del flusso di lavoro richiesti a questi modelli. Esamina i passaggi del flusso di lavoro predefinito e aggiungi tutti i passaggi predefiniti richiesti al flusso di lavoro personalizzato. I passaggi vengono eseguiti sulle risorse in base alla configurazione di un modello di flusso di lavoro. Ad esempio, se desideri che l’assegnazione tag avanzati avvenga automaticamente al caricamento delle risorse, aggiungi il passaggio al modello di flusso di lavoro di post-elaborazione personalizzato.
* Aggiungi [!UICONTROL Processo flusso di lavoro risorsa di aggiornamento DAM completato] alla fine. L’aggiunta di questo passaggio assicura che Experience Manager sappia quando termina l’elaborazione e che la risorsa possa essere contrassegnata come elaborata, ovvero *Nuovo* viene visualizzato sulla risorsa.
* Crea una configurazione per il servizio Custom Workflow Runner che consenta di configurare l’esecuzione di un modello di flusso di lavoro di post-elaborazione in base a un percorso (percorso cartella) o a un’espressione regolare.

Per informazioni dettagliate sul passaggio del flusso di lavoro standard che può essere utilizzato nel flusso di lavoro di post-elaborazione, vedi [passaggi del flusso di lavoro nella post-elaborazione del flusso di lavoro](developer-reference-material-apis.md#post-processing-workflows-steps) nella guida di riferimento per sviluppatori.

### Creare modelli di flusso di lavoro di post-elaborazione {#create-post-processing-workflow-models}

I modelli di flusso di lavoro di post-elaborazione sono regolari [!DNL Experience Manager] modelli di workflow. Se hai bisogno di un’elaborazione diversa per posizioni di archivio o tipi di risorse diversi, puoi creare modelli diversi.

I passaggi di elaborazione vengono aggiunti in base alle esigenze. Puoi utilizzare sia i passaggi supportati disponibili, sia tutti i passaggi del flusso di lavoro implementati in modo personalizzato.

Assicurati che l’ultimo passaggio di ogni flusso di lavoro di post-elaborazione sia `DAM Update Asset Workflow Completed Process`. L’ultimo passaggio consente ad Experience Manager di sapere quando è stata completata l’elaborazione delle risorse.

### Configurare l’esecuzione di un flusso di lavoro di post-elaborazione {#configure-post-processing-workflow-execution}

Una volta completata l’elaborazione delle risorse caricate, i microservizi per le risorse possono definire un flusso di lavoro di post-elaborazione per elaborare ulteriormente le risorse. Per configurare la post-elaborazione utilizzando i modelli di flusso di lavoro, effettuate una delle seguenti operazioni:

* [Applicare un modello di flusso di lavoro nelle proprietà della cartella](#apply-workflow-model-to-folder).
* [Configurare il servizio Workflow Runner personalizzato](#configure-custom-workflow-runner-service).

#### Applicare un modello di flusso di lavoro a una cartella {#apply-workflow-model-to-folder}

Per i casi di utilizzo tipici di post-elaborazione, considera l’utilizzo del metodo per applicare un flusso di lavoro a una cartella. Per applicare un modello di flusso di lavoro nella cartella [!UICONTROL Proprietà], effettua le seguenti operazioni:

1. Crea un modello di flusso di lavoro.
1. Seleziona una cartella e fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti e quindi fare clic su **[!UICONTROL Elaborazione risorse]** scheda.
1. Sotto **[!UICONTROL Avvia flusso di lavoro automaticamente]**, seleziona il flusso di lavoro richiesto, fornisci un titolo del flusso di lavoro, quindi salva le modifiche.

   ![Applicare un flusso di lavoro di post-elaborazione a una cartella nelle relative Proprietà](assets/post-processing-profile-workflow-for-folders.png)

#### Configurare il servizio Workflow Runner personalizzato {#configure-custom-workflow-runner-service}

Puoi configurare il servizio runner flusso di lavoro personalizzato per le configurazioni avanzate che non possono essere facilmente soddisfatte applicando un flusso di lavoro a una cartella. Ad esempio, un flusso di lavoro che utilizza un’espressione regolare. Esecuzione flusso di lavoro personalizzato di Adobe CQ DAM (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) è un servizio OSGi. Per la configurazione sono disponibili le due opzioni seguenti:

* Flussi di lavoro di post-elaborazione per percorso (`postProcWorkflowsByPath`): è possibile elencare più modelli di flusso di lavoro, in base a percorsi di archivio diversi. Separa i percorsi e i modelli utilizzando i due punti. Sono supportati percorsi di archivio semplici. Mappare questi a un modello di flusso di lavoro in `/var` percorso. Esempio: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Flussi di lavoro di post-elaborazione per espressione (`postProcWorkflowsByExpression`): è possibile elencare più modelli di flusso di lavoro, in base a espressioni regolari diverse. Le espressioni e i modelli devono essere separati da due punti. L’espressione regolare deve puntare direttamente al nodo Risorsa e non a uno dei rendering o dei file. Esempio: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

Per informazioni su come distribuire una configurazione OSGi, consulta [distribuisci in [!DNL Experience Manager]](/help/implementing/deploying/overview.md).

#### Disattiva esecuzione flusso di lavoro di post-elaborazione

Quando non è necessaria la post-elaborazione, crea e utilizza un modello di flusso di lavoro &quot;vuoto&quot; in __Avvia flusso di lavoro automaticamente__ selezione.

##### Creare il modello di flusso di lavoro con avvio automatico disattivato

1. Accedi a __Strumenti > Workflow > Modelli__
1. Seleziona __Crea > Crea modello__ dalla barra delle azioni superiore
1. Specifica un titolo e un nome per il nuovo modello di flusso di lavoro, ad esempio:
   * Titolo: Disabilita flusso di lavoro con avvio automatico
   * Nome: disable-auto-start-workflow
1. Seleziona __Fine__ per creare il modello di flusso di lavoro
1. __Seleziona__ e __Modifica__ il modello di flusso di lavoro creato
1. Nell’editor modello flusso di lavoro, seleziona __Passaggio 1__ dalla definizione del modello ed eliminala
1. Apri __Pannello laterale__, e seleziona __Passaggi__
1. Trascina __Flusso di lavoro Aggiorna risorsa DAM completato__ inserisci nella definizione del modello
1. Seleziona la __Informazioni pagina__ (accanto al pulsante __Pannello laterale__ ) e seleziona __Apri proprietà__
1. Sotto __Base__ , seleziona __Flusso di lavoro transitorio__
1. Seleziona __Salva e chiudi__ dalla barra delle azioni superiore
1. Seleziona __Sincronizza__ nella barra delle azioni superiore
1. Chiudi l’editor modello flusso di lavoro

##### Applicare il modello di flusso di lavoro con avvio automatico disattivato

Segui i passaggi descritti in [applicare un modello di flusso di lavoro a una cartella](#apply-workflow-model-to-folder) e imposta __Disabilita flusso di lavoro con avvio automatico__ come __Avvia flusso di lavoro automaticamente__ per le cartelle non richiedono la post-elaborazione delle risorse.

## Best practice e limitazioni {#best-practices-limitations-tips}

* Durante la progettazione dei flussi di lavoro, considera le tue esigenze per tutti i tipi di rendering. Se non prevedi la necessità di una rappresentazione in futuro, rimuovi il relativo passaggio di creazione dal flusso di lavoro. Non è possibile eliminare le rappresentazioni in blocco in un secondo momento. Le rappresentazioni indesiderate possono occupare grandi quantità di spazio di archiviazione dopo l’uso prolungato di [!DNL Experience Manager]. Per le singole risorse, puoi rimuovere manualmente le rappresentazioni dall’interfaccia utente. Per più risorse, puoi personalizzare [!DNL Experience Manager] per eliminare rappresentazioni specifiche o eliminare le risorse e caricarle nuovamente.
* Attualmente, il supporto è limitato alla generazione di rappresentazioni. La generazione di una nuova risorsa non è supportata.
* Attualmente, il limite di dimensione del file per l’estrazione dei metadati è di circa 15 GB. Quando si caricano risorse di grandi dimensioni, a volte l’estrazione dei metadati non riesce.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Introduzione al servizio Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html).
>* [Comprendere l’estensibilità e quando utilizzarla](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).
>* [Come creare applicazioni personalizzate](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html).
>* [Tipi MIME supportati per vari casi d’uso](/help/assets/file-format-support.md).

<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
