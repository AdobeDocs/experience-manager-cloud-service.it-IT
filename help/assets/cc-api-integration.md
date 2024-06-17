---
title: Automazione dei contenuti per l'integrazione Creative Cloud
description: Genera varianti di risorse tramite l’integrazione Creative Cloud
contentOwner: AG
feature: Upload, Asset Processing, Publishing, Asset Compute Microservices
role: User, Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 5%

---

# Genera varianti di risorse tramite [!DNL Adobe Creative Cloud] integrazione {#content-automation}

Il componente aggiuntivo di automazione dei contenuti si integra [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] e [!DNL Adobe Creative Cloud] API per elaborare in modo creativo le risorse su larga scala. [!DNL Experience Manager] utilizza basate su cloud [microservizi per risorse](/help/assets/asset-microservices-overview.md) per utilizzare [!DNL Adobe Creative Cloud] funzioni e automatizza la creazione delle risorse e la gestione dei supporti.

Per modificare le risorse in [!DNL Adobe Photoshop] e [!DNL Adobe Lightroom], non è necessario scaricare risorse da [!DNL Experience Manager Assets], modificali e caricali di nuovo. Puoi creare e configurare un profilo di elaborazione in [!DNL Experience Manager], applica il profilo a una cartella e carica le risorse nella cartella. Le risorse caricate vengono rielaborate in base ai profili di elaborazione e si ottengono varianti di tali risorse. L’elaborazione in blocco coerente e semplice consente di risparmiare sforzi manuali e di velocizzare la creazione dei contenuti, anche senza la necessità di competenze creative superiori. Inoltre, gli sviluppatori e i partner possono estendere i microservizi delle risorse con accesso diretto a queste API e includere una logica personalizzata.

Gli utenti possono creare profili di elaborazione per automatizzare le seguenti operazioni creative sulle loro risorse:

* **Tono automatico**: utilizza l’intelligenza artificiale per analizzare i contenuti dell’immagine e corregge in modo intelligente la luce e i colori in base agli attributi univoci dell’immagine.

* **Verticale automatico**: utilizza l’intelligenza artificiale per analizzare il contenuto dell’immagine e correggere la prospettiva distorta nelle immagini. Ad esempio, per creare orizzonti di livello.

  ![tono automatico](/help/assets/assets/content-automation-autotone.png)

  *Figura: Le funzioni di tono automatico e raddrizzamento automatico contribuiscono a migliorare le immagini distorte.*

* **Predefiniti Lightroom**: applica un aspetto definito dall’utente alle immagini per ottenere un aspetto coerente utilizzando predefiniti personalizzati.

  ![Predefinito Lightroom](/help/assets/assets/content-automation-lrpresets.png)

  *Figura: Predefinito di Adobe Lightroom per migliorare la qualità delle immagini in modo coerente per molte immagini.*

* **Ritaglio immagine**: utilizza l’intelligenza artificiale per creare una selezione intorno a oggetti salienti e rimuovere lo sfondo con un singolo comando.

  ![Rimuovere lo sfondo e tagliare un&#39;immagine da una foto](/help/assets/assets/content-automation-backgroundremove.png)

* **Maschera immagine**: utilizza l’intelligenza artificiale per creare una maschera intorno a oggetti salienti con un singolo comando.

  ![Mascherare un’immagine tramite AI](/help/assets/assets/content-automation-mask.png)

* **Azioni Photoshop**: applica una serie di [!DNL Adobe Photoshop] attività a un file o a un batch di file.

  ![Azioni Photoshop](/help/assets/assets/content-automation-psactions.png)

* **Sostituzione Oggetto Avanzata**: personalizza su larga scala consentendo di scambiare le immagini mantenendo tutti gli effetti e le regolazioni applicati all’interno di un file PSD.

  ![Sostituire gli oggetti in modo intelligente](/help/assets/assets/content-automation-objectreplace.png)

## Abilita l’automazione dei contenuti per il programma as a Cloud Service AEM {#enable-content-automation}

Per abilitare il componente aggiuntivo Automazione dei contenuti per il programma as a Cloud Service per l’AEM utilizzando Cloud Manager:

1. Contatta il rappresentante del tuo account per concedere in licenza il componente aggiuntivo di automazione dei contenuti.
1. Accedi a Cloud Manager e passa alla tua organizzazione utilizzando il selettore organizzazione.
1. Clic **[!UICONTROL Aggiungi programma]** e specificare il nome di un programma.
1. Fai clic su **[!UICONTROL Continua]**.
1. Espandi **[!UICONTROL Risorse]** e seleziona **[!UICONTROL Automazione dei contenuti]**.
1. Fai clic su **[!UICONTROL Crea]**.
1. Esegui la pipeline per [distribuire le modifiche in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

Se devi aggiungere il componente aggiuntivo Automazione dei contenuti a un programma AEM as a Cloud Service esistente in Cloud Manager:

1. Fai clic su ... nella scheda del programma.

1. Seleziona **[!UICONTROL Modifica programma]** e quindi seleziona **[!UICONTROL Soluzioni e componenti aggiuntivi]** scheda.

1. Espandi **[!UICONTROL Risorse]** e seleziona **[!UICONTROL Automazione dei contenuti]**.
1. Fai clic su **[!UICONTROL Aggiorna]**.
1. Esegui la pipeline per [distribuire le modifiche in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## Utilizzare un profilo di elaborazione per modificare in blocco le risorse creative {#process-assets}

Per utilizzare i profili di elaborazione per creare automaticamente le varianti, effettua le seguenti operazioni:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili elaborazione]**.

1. Seleziona **[!UICONTROL Crea]**, e specificare un **[!UICONTROL Nome]**.

1. Seleziona la **[!UICONTROL Creativo]** , specificare la cartella di output, selezionare **[!UICONTROL Aggiungi nuovo]** per aggiungere una configurazione creativa.

1. Fornire **[!UICONTROL Nome rappresentazione]** (o nome dell’output), **[!UICONTROL Estensione]** (o tipo di file), seleziona **[!UICONTROL Qualità]** (o parametri di output), seleziona **[!UICONTROL Include]** e **[!UICONTROL Esclusioni]** Elenchi di tipi MIME (o filtro risorse di input) e seleziona l’operazione creativa richiesta.

   ![[!UICONTROL Creativo] scheda in [!UICONTROL Profilo di elaborazione]](assets/creative-processing-profile.png)

1. Alcune operazioni richiedono parametri aggiuntivi (risorsa). Se necessario, fornisci i valori per questi parametri aggiuntivi.

1. Aggiungi più operazioni creative come parte dello stesso profilo di elaborazione o Salva il profilo.

1. Applica il profilo di elaborazione a una cartella. Su una cartella **[!UICONTROL Proprietà]** pagina, seleziona **[!UICONTROL Elaborazione risorse]** e seleziona il profilo di elaborazione da applicare.

Dopo aver applicato il profilo di elaborazione a una cartella DAM, tutte le risorse caricate o aggiornate in questa cartella eseguono le operazioni definite in aggiunta all’elaborazione standard. Le sottocartelle ereditano gli stessi profili applicati alle cartelle principali. Gli utenti possono ignorare questa ereditarietà.

Per elaborare le risorse esistenti, selezionale, seleziona **[!UICONTROL Rielabora]** e quindi selezionare il profilo di elaborazione richiesto.

## Suggerimenti e limitazioni {#limitations-best-practices}

* [!DNL Experience Manager] limita l’elaborazione delle risorse a 300 richieste al minuto per ambiente e a 700 richieste al minuto per organizzazione.
* Dimensione del file limitata a 4 GB per [!DNL Adobe Photoshop] operazioni API e 1 GB per [!DNL Adobe Lightroom] operazioni.

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
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Configurare e utilizzare i microservizi per le risorse tramite profili di elaborazione](/help/assets/asset-microservices-configure-and-use.md).
>* [Integrare [!DNL Experience Manager] con [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [Acquisizione ed elaborazione delle risorse con i microservizi per le risorse: panoramica](/help/assets/asset-microservices-overview.md).
