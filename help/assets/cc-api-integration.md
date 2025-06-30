---
title: Integrazione di Content Automation per Creative Cloud
description: Generare varianti di risorse tramite l’integrazione Creative Cloud
contentOwner: AG
feature: Upload, Asset Processing, Publishing, Asset Compute Microservices
role: User, Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 5%

---

# Genera varianti di risorse utilizzando l&#39;integrazione [!DNL Adobe Creative Cloud] {#content-automation}

Il componente aggiuntivo di automazione dei contenuti integra [!DNL Adobe Experience Manager Assets] come API [!DNL Cloud Service] e [!DNL Adobe Creative Cloud] per elaborare in modo creativo le risorse su larga scala. [!DNL Experience Manager] utilizza i microservizi [asset](/help/assets/asset-microservices-overview.md) basati su cloud per utilizzare le funzionalità [!DNL Adobe Creative Cloud] e automatizzare la creazione delle risorse e la gestione dei supporti.

Per modificare le risorse in [!DNL Adobe Photoshop] e [!DNL Adobe Lightroom], non è necessario scaricare, modificare e caricare nuovamente le risorse da [!DNL Experience Manager Assets]. È possibile creare e configurare un profilo di elaborazione in [!DNL Experience Manager], applicarlo a una cartella e caricare le risorse nella cartella. Le risorse caricate vengono rielaborate in base ai profili di elaborazione e si ottengono varianti di tali risorse. L’elaborazione in blocco coerente e semplice consente di risparmiare sforzi manuali e di velocizzare la creazione dei contenuti, anche senza la necessità di competenze creative superiori. Inoltre, gli sviluppatori e i partner possono estendere i microservizi delle risorse con accesso diretto a queste API e includere una logica personalizzata.

Gli utenti possono creare profili di elaborazione per automatizzare le seguenti operazioni creative sulle loro risorse:

* **Tono automatico**: utilizza l&#39;intelligenza artificiale per analizzare il contenuto dell&#39;immagine e corregge in modo intelligente la luce e i colori in base agli attributi univoci dell&#39;immagine.

* **Altezza automatica**: utilizza l&#39;intelligenza artificiale per analizzare il contenuto dell&#39;immagine e correggere la prospettiva distorta nelle immagini. Ad esempio, per creare orizzonti di livello.

  ![tono automatico](/help/assets/assets/content-automation-autotone.png)

  *Figura: Toni automatici e raddrizzamento automatico possono contribuire a migliorare le immagini distorte.*

* **Predefiniti Lightroom**: applica un aspetto definito dall&#39;utente alle immagini per ottenere un aspetto coerente utilizzando predefiniti personalizzati.

  ![Predefinito Lightroom](/help/assets/assets/content-automation-lrpresets.png)

  *Figura: predefinito Adobe Lightroom per migliorare la qualità delle immagini in modo coerente per molte immagini.*

* **Ritaglio immagine**: utilizza l&#39;intelligenza artificiale per creare la selezione intorno agli oggetti salienti e rimuovere lo sfondo con un singolo comando.

  ![Rimuovere lo sfondo e tagliare un&#39;immagine da una foto](/help/assets/assets/content-automation-backgroundremove.png)

* **Maschera immagine**: utilizza l&#39;intelligenza artificiale per creare una maschera intorno a oggetti salienti con un solo comando.

  ![Mascherare un&#39;immagine utilizzando AI](/help/assets/assets/content-automation-mask.png)

* **Azioni Photoshop**: applica una serie di [!DNL Adobe Photoshop] attività a un file o a un batch di file.

  ![Azioni Photoshop](/help/assets/assets/content-automation-psactions.png)

* **Sostituzione oggetto avanzato**: personalizzazione su larga scala consentendo di scambiare le immagini mantenendo tutti gli effetti e le regolazioni applicati all&#39;interno di un file PSD.

  ![Sostituisci gli oggetti in modo intelligente](/help/assets/assets/content-automation-objectreplace.png)

## Abilitare il programma di automazione dei contenuti per AEM as a Cloud Service {#enable-content-automation}

Per abilitare il componente aggiuntivo Automazione dei contenuti per il programma AEM as a Cloud Service utilizzando Cloud Manager:

1. Contatta il rappresentante del tuo account per concedere in licenza il componente aggiuntivo di automazione dei contenuti.
1. Accedi a Cloud Manager e passa alla tua organizzazione utilizzando il selettore organizzazione.
1. Fare clic su **[!UICONTROL Aggiungi programma]** e specificare un nome di programma.
1. Fai clic su **[!UICONTROL Continua]**.
1. Espandi **[!UICONTROL Assets]** e seleziona **[!UICONTROL Automazione contenuti]**.
1. Fai clic su **[!UICONTROL Crea]**.
1. Esegui la pipeline per [distribuire le modifiche in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

Se devi aggiungere il componente aggiuntivo Automazione dei contenuti a un programma AEM as a Cloud Service esistente in Cloud Manager:

1. Fai clic su ... nella scheda del programma.

1. Seleziona **[!UICONTROL Modifica programma]**, quindi seleziona la scheda **[!UICONTROL Soluzioni e componenti aggiuntivi]**.

1. Espandi **[!UICONTROL Assets]** e seleziona **[!UICONTROL Automazione contenuti]**.
1. Fai clic su **[!UICONTROL Aggiorna]**.
1. Esegui la pipeline per [distribuire le modifiche in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## Utilizzare un profilo di elaborazione per modificare in blocco le risorse creative {#process-assets}

Per utilizzare i profili di elaborazione per creare automaticamente le varianti, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Profili di elaborazione]**.

1. Seleziona **[!UICONTROL Crea]** e specifica un **[!UICONTROL Nome]**.

1. Seleziona la scheda **[!UICONTROL Creative]**, specifica la cartella di output, seleziona **[!UICONTROL Aggiungi nuovo]** per aggiungere una configurazione creativa.

1. Fornisci **[!UICONTROL Nome rappresentazione]** (o nome output), **[!UICONTROL Estensione]** (o tipo di file), seleziona **[!UICONTROL Qualità]** (o parametri di output), seleziona **[!UICONTROL Includi]** e **[!UICONTROL Escludi]** elenchi di tipi MIME (o filtro risorse di input), quindi seleziona l&#39;operazione creativa richiesta.

   Scheda ![[!UICONTROL Creative] in [!UICONTROL Elaborazione profilo]](assets/creative-processing-profile.png)

1. Alcune operazioni richiedono parametri aggiuntivi (risorsa). Se necessario, fornisci i valori per questi parametri aggiuntivi.

1. Aggiungi più operazioni creative come parte dello stesso profilo di elaborazione o Salva il profilo.

1. Applica il profilo di elaborazione a una cartella. Nella pagina **[!UICONTROL Proprietà]** di una cartella, seleziona **[!UICONTROL Elaborazione risorse]** e quindi il profilo di elaborazione da applicare.

Dopo aver applicato il profilo di elaborazione a una cartella DAM, tutte le risorse caricate o aggiornate in questa cartella eseguono le operazioni definite in aggiunta all’elaborazione standard. Le sottocartelle ereditano gli stessi profili applicati alle cartelle principali. Gli utenti possono ignorare questa ereditarietà.

Per elaborare le risorse esistenti, selezionare le risorse, selezionare l&#39;opzione **[!UICONTROL Rielabora]**, quindi selezionare il profilo di elaborazione richiesto.

## Suggerimenti e limitazioni {#limitations-best-practices}

* [!DNL Experience Manager] limita l&#39;elaborazione delle risorse a 300 richieste al minuto per ambiente e 700 richieste al minuto per organizzazione.
* La dimensione del file è limitata a 4 GB per le operazioni API [!DNL Adobe Photoshop] e a 1 GB per le operazioni [!DNL Adobe Lightroom].
* Le rappresentazioni PDF dei documenti di Microsoft Office (&quot;.docx&quot;, &quot;.doc&quot;, &quot;.ppt&quot;, &quot;.pptx&quot;, &quot;.xls&quot;, &quot;.xlsx&quot;) sono limitate a file di dimensioni non superiori a 100 MB.
* La transcodifica video è limitata a file di input di 15 GB o meno.

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
