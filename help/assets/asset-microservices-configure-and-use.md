---
title: Configurare e utilizzare i microservizi per le risorse
description: Configura e utilizza i microservizi per le risorse native per il cloud per elaborare le risorse su larga scala.
contentOwner: AG
feature: Asset Compute Microservices,Workflow,Asset Processing
role: Architect,Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '2932'
ht-degree: 3%

---

# Utilizzare i microservizi delle risorse e i profili di elaborazione {#get-started-using-asset-microservices}

I microservizi per le risorse forniscono un’elaborazione scalabile e resiliente delle risorse utilizzando applicazioni native per il cloud (o processi di lavoro). Adobe gestisce i servizi per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione.

I microservizi per le risorse consentono di elaborare un [ampia gamma di tipi di file](/help/assets/file-format-support.md) con più formati pronti all&#39;uso rispetto alle versioni precedenti di [!DNL Experience Manager]. Ad esempio, l’estrazione delle miniature dei formati PSD e PSB è ora possibile, ma in precedenza era necessaria una soluzione di terze parti come [!DNL ImageMagick].

L’elaborazione delle risorse dipende dalla configurazione in **[!UICONTROL Profili di elaborazione]**. Experience Manager fornisce una configurazione predefinita di base e consente agli amministratori di aggiungere una configurazione di elaborazione delle risorse più specifica. Gli amministratori creano, gestiscono e modificano le configurazioni dei flussi di lavoro di post-elaborazione, inclusa la personalizzazione facoltativa. La personalizzazione dei flussi di lavoro consente agli sviluppatori di estendere l’offerta predefinita.

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Vista di alto livello sull’elaborazione delle risorse](assets/asset-microservices-flow.png "Vista di alto livello sull’elaborazione delle risorse")

>[!NOTE]
>
>L’elaborazione delle risorse qui descritta sostituisce la `DAM Update Asset` modello di flusso di lavoro esistente nelle versioni precedenti di [!DNL Experience Manager]. La maggior parte dei passaggi standard relativi alla generazione del rendering e ai metadati viene sostituita dall’elaborazione dei microservizi per le risorse e gli eventuali passaggi rimanenti possono essere sostituiti dalla configurazione del flusso di lavoro di post-elaborazione.

## Comprendere le opzioni di elaborazione delle risorse {#get-started}

[!DNL Experience Manager] consente i seguenti livelli di elaborazione.

| Opzione | Descrizione | Casi d&#39;uso coperti |
|---|---|---|
| [Configurazione predefinita](#default-config) | È disponibile così come è e non può essere modificata. Questa configurazione fornisce funzionalità di generazione del rendering di base. | <ul> <li>Miniature standard utilizzate da [!DNL Assets] interfaccia utente (48, 140 e 319 pixel) </li> <li> Anteprima grande (rendering web - 1280 pixel) </li><li> Estrazione di metadati e testo.</li></ul> |
| [Configurazione personalizzata](#standard-config) | Configurata dagli amministratori tramite l’interfaccia utente. Fornisce ulteriori opzioni per la generazione del rendering estendendo l&#39;opzione predefinita. Estendi l’opzione preconfigurata per fornire formati e rappresentazioni diversi. | <ul><li>Rendering FPO. </li> <li>Modificare il formato di file e la risoluzione delle immagini</li> <li> Applicabile in modo condizionale ai tipi di file configurati. </li> </ul> |
| [Profilo personalizzato](#custom-config) | Configurati dagli amministratori tramite l&#39;interfaccia utente per utilizzare il codice personalizzato tramite applicazioni personalizzate per chiamare [Servizio Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html). Supporta requisiti più complessi in un metodo cloud-nativo e scalabile. | Vedi [casi d&#39;uso consentiti](#custom-config). |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## Formati di file supportati {#supported-file-formats}

I microservizi per le risorse supportano un’ampia varietà di formati di file per elaborare, generare rappresentazioni o estrarre metadati. Vedi [formati di file supportati](file-format-support.md) per l’elenco completo dei tipi MIME e delle funzionalità supportate per ciascun tipo.

## Configurazione predefinita {#default-config}

Alcuni valori predefiniti sono preconfigurati per garantire la disponibilità dei rendering predefiniti richiesti in Experience Manager. La configurazione predefinita garantisce inoltre la disponibilità delle operazioni di estrazione dei metadati e di estrazione del testo. Gli utenti possono iniziare a caricare o aggiornare le risorse immediatamente e l’elaborazione di base è disponibile per impostazione predefinita.

Con la configurazione predefinita, viene configurato solo il profilo di elaborazione più semplice. Tale profilo di elaborazione non è visibile sull’interfaccia utente e non è possibile modificarlo. Viene sempre eseguito l’elaborazione delle risorse caricate. Tale profilo di elaborazione predefinito assicura che l&#39;elaborazione di base richiesta da [!DNL Experience Manager] viene completato per tutte le risorse.

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## Configurazione standard {#standard-config}

[!DNL Experience Manager] fornisce funzionalità per generare rappresentazioni più specifiche per i formati comuni in base alle esigenze dell&#39;utente. Un amministratore può creare [!UICONTROL Profili di elaborazione] per facilitare la creazione di copie trasformate. Gli utenti quindi assegnano uno o più profili disponibili a cartelle specifiche per eseguire l’elaborazione aggiuntiva. Ad esempio, l’elaborazione aggiuntiva può generare rappresentazioni per web, dispositivi mobili e tablet. Il video seguente illustra come creare e applicare [!UICONTROL Profili di elaborazione] e come accedere alle rappresentazioni create.

* **Larghezza e altezza del rendering**: Le specifiche relative a larghezza e altezza del rendering forniscono le dimensioni massime dell&#39;immagine di output generata. I microservizi per le risorse cercano di produrre il rendering più grande possibile, che larghezza e altezza non sono rispettivamente più grandi della larghezza e dell’altezza specificate. Il rapporto di formato viene mantenuto, ovvero lo stesso dell&#39;originale. Un valore vuoto indica che l’elaborazione delle risorse assume la dimensione in pixel dell’originale.

* **Regole di inclusione del tipo MIME**: Quando viene elaborata una risorsa con un tipo MIME specifico, il tipo MIME viene prima controllato rispetto al valore dei tipi MIME esclusi per la specifica di rendering. Se corrisponde a tale elenco, questo rendering specifico non viene generato per la risorsa (ad elenco Bloccati). In caso contrario, il tipo MIME viene controllato rispetto al tipo MIME incluso e, se corrisponde all’elenco, il rendering viene generato (elenco Consentiti).

* **Rendering FPO speciale**: Quando si inseriscono risorse di grandi dimensioni da [!DNL Experience Manager] in [!DNL Adobe InDesign] documenti, un creativo professionista attende per un tempo considerevole dopo [inserire una risorsa](https://helpx.adobe.com/indesign/using/placing-graphics.html). Nel frattempo, all&#39;utente è impedito di utilizzare [!DNL InDesign]. Questo interrompe il flusso creativo e influisce negativamente sull’esperienza utente. L’Adobe consente di inserire temporaneamente rappresentazioni di piccole dimensioni in [!DNL InDesign] i documenti con cui iniziare, che possono essere sostituiti successivamente con risorse a risoluzione completa on-demand. [!DNL Experience Manager] fornisce rappresentazioni utilizzate solo per il posizionamento (FPO). Queste rappresentazioni FPO hanno dimensioni file ridotte ma hanno le stesse proporzioni.

Il profilo di elaborazione può includere un rendering FPO (solo posizionamento). Vedi [!DNL Adobe Asset Link] [documentazione](https://helpx.adobe.com/it/enterprise/using/manage-assets-using-adobe-asset-link.html) per capire se è necessario attivarlo per il profilo di elaborazione. Per ulteriori informazioni, consulta [Documentazione completa di Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html).

### Creare un profilo standard {#create-standard-profile}

Per creare un profilo di elaborazione standard, effettua le seguenti operazioni:

1. Accesso amministratori **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili di elaborazione]**. Fai clic su **[!UICONTROL Crea]**.
1. Specifica un nome che ti aiuti a identificare in modo univoco il profilo quando lo applichi a una cartella.
1. Per generare rappresentazioni FPO, nella pagina **[!UICONTROL Immagine]** abilita **[!UICONTROL Crea rappresentazione FPO]**. Ingresso a **[!UICONTROL Qualità]** tra 1 e 100.
1. Per generare altre rappresentazioni, fai clic su **[!UICONTROL Aggiungi nuovo]** e fornire le seguenti informazioni:

   * Nome file di ogni rendering.
   * Formato di file (PNG, JPEG, GIF o WebP) di ciascun rendering.
   * Larghezza e altezza in pixel di ciascuna rappresentazione. Se i valori non sono specificati, viene utilizzata la dimensione in pixel dell&#39;immagine originale.
   * Qualità in percentuale di ogni rendering JPEG e WebP.
   * Tipi MIME inclusi ed esclusi per definire l’applicabilità di un profilo.

   ![elaborazione-profili-aggiunta](assets/processing-profiles-image.png)

1. Fai clic su **[!UICONTROL Salva]**.

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## Casi di utilizzo e di profilo personalizzati {#custom-config}

La [!DNL Asset Compute Service] supporta diversi casi d’uso, ad esempio l’elaborazione predefinita, l’elaborazione di formati specifici per Adobi come i file Photoshop e l’implementazione di un’elaborazione personalizzata o specifica per l’organizzazione. La personalizzazione del flusso di lavoro Risorsa di aggiornamento DAM richiesta in passato viene gestita automaticamente o tramite la configurazione dei profili di elaborazione. Se queste opzioni di elaborazione non soddisfano le esigenze aziendali, Adobe consiglia di sviluppare e utilizzare [!DNL Asset Compute Service] estendere le funzionalità predefinite. Per una panoramica, vedi [comprendere l’estensibilità e quando utilizzarla](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html).

>[!NOTE]
>
>Adobe consiglia di utilizzare un’applicazione personalizzata solo quando i requisiti aziendali non possono essere soddisfatti utilizzando le configurazioni predefinite o il profilo standard.

Può trasformare immagini, video, documenti e altri formati di file in diverse rappresentazioni, quali miniature, testo e metadati estratti e archivi.

Gli sviluppatori possono utilizzare [!DNL Asset Compute Service] a [creare applicazioni personalizzate](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html) per i casi d’uso supportati. [!DNL Experience Manager] può chiamare queste applicazioni personalizzate dall’interfaccia utente utilizzando profili personalizzati configurati dagli amministratori. [!DNL Asset Compute Service] supporta i seguenti casi d’uso per richiamare servizi esterni:

* Utilizzo [!DNL Adobe Photoshop]s [API ImageCutout](https://developer.adobe.com/photoshop/photoshop-api-docs/) e salvare il risultato come rendering.
* Invoca sistemi di terze parti per aggiornare i dati, ad esempio un sistema PIM.
* Utilizzo [!DNL Photoshop] API per generare diverse rappresentazioni basate su modelli Photoshop.
* Utilizzo [API Adobe Lightroom](https://developer.adobe.com/photoshop/photoshop-api-docs/) per ottimizzare le risorse acquisite e salvarle come rappresentazioni.

>[!NOTE]
>
>Non è possibile modificare i metadati standard utilizzando le applicazioni personalizzate. Puoi modificare solo i metadati personalizzati.

### Creare un profilo personalizzato {#create-custom-profile}

Per creare un profilo personalizzato, effettua le seguenti operazioni:

1. Accesso amministratori **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili di elaborazione]**. Fai clic su **[!UICONTROL Crea]**.
1. Fai clic su **[!UICONTROL Personalizzato]** scheda . Fai clic su **[!UICONTROL Aggiungi nuovo]**. Specifica il nome file desiderato per il rendering.
1. Fornisci le seguenti informazioni.

   * Nome file di ogni rendering e estensione file supportata.
   * [URL punto finale di un’app personalizzata di App Builder](https://experienceleague.adobe.com/docs/asset-compute/using/extend/deploy-custom-application.html). L&#39;app deve provenire dalla stessa organizzazione dell&#39;account Experience Manager.
   * Aggiungi parametri di servizio a [trasmettere informazioni o parametri aggiuntivi all&#39;applicazione personalizzata](https://experienceleague.adobe.com/docs/asset-compute/using/extend/develop-custom-application.html#extend).
   * Tipi MIME inclusi ed esclusi per limitare l’elaborazione ad alcuni formati di file specifici.

   Fai clic su **[!UICONTROL Salva]**.

Le applicazioni personalizzate sono headless [Generatore di app di progetto](https://developer.adobe.com/app-builder/docs/overview/) app. L&#39;applicazione personalizzata ottiene tutti i file forniti se sono configurati con un profilo di elaborazione. L&#39;applicazione deve filtrare i file.

>[!CAUTION]
>
>Se l’app Builder e [!DNL Experience Manager] l&#39;account non proviene dalla stessa organizzazione; l&#39;integrazione non funziona.

### Esempio di profilo personalizzato {#custom-profile-example}

Per illustrare l’utilizzo del profilo personalizzato, consideriamo un caso d’uso per applicare del testo personalizzato alle immagini della campagna. Puoi creare un profilo di elaborazione che sfrutta l’API Photoshop per modificare le immagini.

L’integrazione di Asset compute Service consente ad Experience Manager di trasmettere questi parametri all’applicazione personalizzata utilizzando [!UICONTROL Parametri del servizio] campo . L’applicazione personalizzata chiama quindi l’API Photoshop e trasmette questi valori all’API. Ad esempio, puoi passare il nome del font, il colore del testo, il peso del testo e le dimensioni del testo per aggiungere il testo personalizzato alle immagini della campagna.

<!-- TBD: Check screenshot against the interface. -->

![profilo di elaborazione personalizzato](assets/custom-processing-profile.png)

*Figura: Utilizzo [!UICONTROL Parametri del servizio] per passare informazioni aggiunte ai parametri predefiniti generati nell’applicazione personalizzata. In questo esempio, quando le immagini della campagna vengono caricate, le immagini vengono aggiornate con `Jumanji` testo in `Arial-BoldMT` font.*

## Utilizzare i profili di elaborazione per elaborare le risorse {#use-profiles}

Crea e applica i profili di elaborazione aggiuntivi e personalizzati a cartelle specifiche, ad Experience Manager per elaborare le risorse caricate o aggiornate in queste cartelle. Il profilo di elaborazione standard predefinito viene sempre eseguito ma non è visibile nell’interfaccia utente. Se aggiungi un profilo personalizzato, entrambi i profili vengono utilizzati per elaborare le risorse caricate.

Applica i profili di elaborazione alle cartelle utilizzando uno dei seguenti metodi:

* Gli amministratori possono selezionare una definizione di profilo di elaborazione in **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili di elaborazione]** e utilizza **[!UICONTROL Applica profilo a cartelle]** azione. Apre un browser dei contenuti che ti consente di navigare in cartelle specifiche, selezionarle e confermare l’applicazione del profilo.
* Gli utenti possono selezionare una cartella nell’interfaccia utente di Assets, utilizzando **[!UICONTROL Proprietà]** per aprire la schermata delle proprietà della cartella, fai clic sul pulsante **[!UICONTROL Elaborazione delle risorse]** e nella [!UICONTROL Profilo di elaborazione] selezionare il profilo di elaborazione appropriato per la cartella. Per salvare le modifiche, fai clic su **[!UICONTROL Salva e chiudi]**.
   ![Applicare un profilo di elaborazione a una cartella dalla scheda Proprietà risorsa](assets/folder-properties-processing-profile.png)

* Per applicare un profilo di elaborazione, gli utenti possono selezionare cartelle o risorse specifiche nell’interfaccia utente di Assets, quindi selezionare ![icona di rielaborazione delle risorse](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL Rielaborazione delle risorse]** tra le opzioni disponibili nella parte superiore.

>[!TIP]
>
>A una cartella può essere applicato un solo profilo di elaborazione. Per generare più rendering, aggiungi più definizioni di rendering al profilo di elaborazione esistente.

Dopo aver applicato un profilo di elaborazione a una cartella, tutte le nuove risorse caricate (o aggiornate) in questa cartella o in una delle relative sottocartelle vengono elaborate utilizzando il profilo di elaborazione aggiuntivo configurato. Questa elaborazione si aggiunge al profilo predefinito standard.

>[!NOTE]
>
>Un profilo di elaborazione applicato a una cartella funziona per l’intero albero, ma può essere sostituito con un altro profilo applicato a una sottocartella. Quando le risorse vengono caricate in una cartella, Experience Manager controlla le proprietà della cartella contenitore per un profilo di elaborazione. Se nessun profilo è applicato, viene selezionata una cartella principale nella gerarchia per un profilo di elaborazione da applicare.

Per verificare che le risorse siano state elaborate, visualizza in anteprima le rappresentazioni generate nel [!UICONTROL Rendering] nella barra a sinistra. Apri l’anteprima della risorsa e apri la barra a sinistra per accedere al **[!UICONTROL Rendering]** visualizza. Le rappresentazioni specifiche nel profilo di elaborazione, per le quali il tipo di risorsa specifico corrisponde alle regole di inclusione del tipo MIME, devono essere visibili e accessibili.

![rappresentazioni aggiuntive](assets/renditions-additional-renditions.png)

*Figura: Esempio di due rappresentazioni aggiuntive generate da un profilo di elaborazione applicato alla cartella principale.*

## Flussi di lavoro di post-elaborazione {#post-processing-workflows}

In una situazione in cui è necessaria un’elaborazione aggiuntiva delle risorse che non può essere ottenuta utilizzando i profili di elaborazione, è possibile aggiungere alla configurazione flussi di lavoro aggiuntivi di post-elaborazione. La post-elaborazione consente di aggiungere un’elaborazione completamente personalizzata oltre all’elaborazione configurabile tramite i microservizi per le risorse.

Flussi di lavoro di post-elaborazione, o [Flusso di lavoro con avvio automatico](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/auto-start-workflows.html), se configurati, vengono eseguiti automaticamente da [!DNL Experience Manager] al termine dell&#39;elaborazione dei microservizi. Non è necessario aggiungere manualmente i moduli di avvio del flusso di lavoro per attivare i flussi di lavoro. Gli esempi includono:

* Passaggi del flusso di lavoro personalizzati per elaborare le risorse.
* Integrazioni per aggiungere metadati o proprietà alle risorse da sistemi esterni, ad esempio informazioni su prodotti o processi.
* Elaborazione aggiuntiva eseguita da servizi esterni.

Per aggiungere una configurazione del flusso di lavoro di post-elaborazione a [!DNL Experience Manager], segui questi passaggi:

* Crea uno o più modelli di flusso di lavoro. Questi modelli personalizzati sono denominati *modelli di flusso di lavoro di post-elaborazione* in questa documentazione. Sono regolari [!DNL Experience Manager] modelli di flusso di lavoro.
* Aggiungi i passaggi del flusso di lavoro richiesti a questi modelli. Esamina i passaggi dal flusso di lavoro predefinito e aggiungi tutti i passaggi predefiniti richiesti al flusso di lavoro personalizzato. I passaggi vengono eseguiti sulle risorse in base alla configurazione di un modello di flusso di lavoro. Ad esempio, se desideri che l’assegnazione tag avanzati avvenga automaticamente al momento del caricamento delle risorse, aggiungi il passaggio al modello di flusso di lavoro di post-elaborazione personalizzato.
* Aggiungi [!UICONTROL Processo completato flusso di lavoro risorse di aggiornamento DAM] passo alla fine. L’aggiunta di questo passaggio garantisce che l’Experience Manager sappia quando termina l’elaborazione e che la risorsa possa essere contrassegnata come elaborata, ovvero *Nuovo* viene visualizzato sulla risorsa.
* Crea una configurazione per il servizio Custom Workflow Runner Service che consente di configurare l’esecuzione di un modello di flusso di lavoro post-elaborazione tramite un percorso (posizione della cartella) o tramite un’espressione regolare.

Per informazioni dettagliate su quale passaggio del flusso di lavoro standard può essere utilizzato nel flusso di lavoro di post-elaborazione, vedi [passaggi del flusso di lavoro nel flusso di lavoro di post-elaborazione](developer-reference-material-apis.md#post-processing-workflows-steps) in riferimento per gli sviluppatori.

### Creare modelli di flusso di lavoro di post-elaborazione {#create-post-processing-workflow-models}

I modelli di flusso di lavoro di post-elaborazione sono regolari [!DNL Experience Manager] modelli di flusso di lavoro. Crea modelli diversi se hai bisogno di un’elaborazione diversa per posizioni di archivio o tipi di risorse diversi.

Le fasi di elaborazione vengono aggiunte in base alle esigenze. Puoi utilizzare entrambi i passaggi supportati disponibili, nonché tutti i passaggi del flusso di lavoro implementati personalizzati.

Assicurati che l’ultimo passaggio di ogni flusso di lavoro di post-elaborazione sia `DAM Update Asset Workflow Completed Process`. L’ultimo passaggio consente ad Experience Manager di sapere quando viene completata l’elaborazione delle risorse.

### Configurare l’esecuzione del flusso di lavoro di post-elaborazione {#configure-post-processing-workflow-execution}

Al termine dell’elaborazione delle risorse caricate, i microservizi per le risorse possono definire il flusso di lavoro di post-elaborazione per elaborare ulteriormente le risorse. Per configurare la post-elaborazione utilizzando i modelli di flusso di lavoro, puoi effettuare una delle seguenti operazioni:

* [Applicare un modello di flusso di lavoro nelle proprietà della cartella](#apply-workflow-model-to-folder).
* [Configurare il servizio Workflow Runner personalizzato](#configure-custom-workflow-runner-service).

#### Applicare un modello di flusso di lavoro a una cartella {#apply-workflow-model-to-folder}

Per i casi d’uso tipici di post-elaborazione, considera l’utilizzo del metodo per applicare un flusso di lavoro a una cartella. Applicazione di un modello di flusso di lavoro nella cartella [!UICONTROL Proprietà], segui questi passaggi:

1. Crea un modello di flusso di lavoro.
1. Seleziona una cartella e fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti, quindi fare clic su **[!UICONTROL Elaborazione delle risorse]** scheda .
1. Sotto **[!UICONTROL Flusso di lavoro con avvio automatico]**, seleziona il flusso di lavoro richiesto, fornisci un titolo del flusso di lavoro, quindi salva le modifiche.

   ![Applicare un flusso di lavoro di post-elaborazione a una cartella nelle relative proprietà](assets/post-processing-profile-workflow-for-folders.png)

#### Configurare il servizio Workflow Runner personalizzato {#configure-custom-workflow-runner-service}

Puoi configurare il servizio di esecuzione dei flussi di lavoro personalizzato per le configurazioni avanzate che non possono essere facilmente soddisfatte applicando un flusso di lavoro a una cartella. Ad esempio, un flusso di lavoro che utilizza un’espressione regolare. Il Runner flusso di lavoro personalizzato Adobe CQ DAM (`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`) è un servizio OSGi. Fornisce le due opzioni seguenti per la configurazione:

* Flussi di lavoro di post-elaborazione per percorso (`postProcWorkflowsByPath`): È possibile elencare più modelli di flusso di lavoro, basati su diversi percorsi di archivio. Separa i percorsi e i modelli utilizzando due punti. Sono supportati percorsi archivio semplici. Mappatura di questi elementi su un modello di flusso di lavoro nel `/var` percorso. Esempio: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* Flussi di lavoro di post-elaborazione per espressione (`postProcWorkflowsByExpression`): È possibile elencare più modelli di flusso di lavoro, in base a diverse espressioni regolari. Le espressioni e i modelli devono essere separati da due punti. L’espressione regolare deve puntare direttamente al nodo Asset e non a una delle rappresentazioni o dei file. Esempio: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

Per informazioni su come distribuire una configurazione OSGi, vedi [distribuire [!DNL Experience Manager]](/help/implementing/deploying/overview.md).

#### Disattiva l’esecuzione del flusso di lavoro di post-elaborazione

Quando non è necessario eseguire la post-elaborazione, crea e utilizza un modello di flusso di lavoro &quot;vuoto&quot; nella sezione __Flusso di lavoro con avvio automatico__ selezione.

##### Creare il modello di flusso di lavoro con avvio automatico disattivato

1. Passa a __Strumenti > Flusso di lavoro > Modelli__
1. Seleziona __Crea > Crea modello__ dalla barra delle azioni superiore
1. Specifica un titolo e un nome per il nuovo modello di flusso di lavoro, ad esempio:
   * Titolo: Disattiva flusso di lavoro con avvio automatico
   * Nome: disable-auto-start-workflow
1. Seleziona __Fine__ per creare il modello di flusso di lavoro
1. __Seleziona__ e __Modifica__ il modello di workflow appena creato
1. Nell’editor per modelli di flusso di lavoro, seleziona __Passaggio 1__ dalla definizione del modello e eliminalo
1. Apri __Pannello laterale__, quindi seleziona __Passaggi__
1. Trascina __Flusso di lavoro della risorsa di aggiornamento DAM completato__ nella definizione del modello
1. Seleziona la __Informazioni pagina__ (accanto al pulsante __Pannello laterale__ ) e seleziona __Apri proprietà__
1. Sotto la __Base__ scheda , seleziona __Flusso di lavoro transitorio__
1. Seleziona __Salva e chiudi__ dalla barra delle azioni superiore
1. Seleziona __Sincronizzazione__ nella barra delle azioni superiore
1. Chiudi l’editor per modelli di flusso di lavoro

##### Applicare il modello di flusso di lavoro con avvio automatico disattivato

Segui i passaggi descritti in [applicare un modello di flusso di lavoro a una cartella](#apply-workflow-model-to-folder) e imposta __Disattiva flusso di lavoro con avvio automatico__ come __Flusso di lavoro con avvio automatico__ per le cartelle non è necessaria la post-elaborazione delle risorse.

## Best practice e limitazioni {#best-practices-limitations-tips}

* Considera le tue esigenze per tutti i tipi di rendering durante la progettazione dei flussi di lavoro. Se non prevedete la necessità di un rendering in futuro, rimuovete il relativo passaggio di creazione dal flusso di lavoro. Le rappresentazioni non possono essere eliminate in blocco in seguito. Le rappresentazioni indesiderate possono occupare molto spazio di archiviazione dopo un uso prolungato di [!DNL Experience Manager]. Per le singole risorse, puoi rimuovere manualmente i rendering dall’interfaccia utente. Per più risorse, puoi personalizzare [!DNL Experience Manager] per eliminare rappresentazioni specifiche o eliminare le risorse e caricarle di nuovo.
* Al momento, il supporto è limitato alla generazione di rappresentazioni. La generazione di nuove risorse non è supportata.
* Attualmente, il limite di dimensione del file per l’estrazione dei metadati è di circa 15 GB. Quando si caricano risorse di grandi dimensioni, a volte l’operazione di estrazione dei metadati non riesce.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)

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
