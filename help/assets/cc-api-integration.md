---
title: Automazione dei contenuti per l'integrazione con Creative Cloud
description: Generare varianti di risorse utilizzando l’integrazione con Creative Cloud
contentOwner: AG
feature: Upload,Asset Processing,Publishing,Asset Compute Microservices,Workflow
role: User,Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 3%

---

# Genera varianti di risorse utilizzando [!DNL Adobe Creative Cloud] integrazione {#content-automation}

Il componente aggiuntivo per l’automazione dei contenuti si integra [!DNL Adobe Experience Manager Assets] come [!DNL Cloud Service] e [!DNL Adobe Creative Cloud] API per elaborare in modo creativo le risorse su larga scala. [!DNL Experience Manager] utilizza basato su cloud [microservizi per le risorse](/help/assets/asset-microservices-overview.md) per utilizzare [!DNL Adobe Creative Cloud] e automatizza la creazione delle risorse e la gestione dei contenuti multimediali.

Per modificare le risorse in [!DNL Adobe Photoshop] e [!DNL Adobe Lightroom], non è necessario scaricare risorse da [!DNL Experience Manager Assets], modificali e caricali di nuovo. Puoi creare e configurare un profilo di elaborazione in [!DNL Experience Manager], applica il profilo a una cartella e carica le risorse nella cartella . Le risorse caricate vengono rielaborate in base ai profili di elaborazione e ottieni varianti di tali risorse. L&#39;elaborazione di massa continua e semplice consente di risparmiare lavoro manuale e di aumentare la velocità dei contenuti, anche senza la necessità di competenze creative eccezionali. Inoltre, gli sviluppatori e i partner possono estendere i microservizi per le risorse con accesso diretto a queste API e includere logica personalizzata.

Gli utenti possono creare profili di elaborazione per automatizzare le seguenti operazioni creative sulle risorse:

* **Tonalità automatica**: Utilizza l&#39;intelligenza artificiale per analizzare il contenuto dell&#39;immagine e apporta in modo intelligente correzioni di luce e colore in base agli attributi unici dell&#39;immagine.

* **Automatico verticale**: Utilizza l&#39;intelligenza artificiale per analizzare il contenuto dell&#39;immagine e correggere la prospettiva distorta nelle immagini. Ad esempio, per creare orizzonti di livello.

   ![tono automatico](/help/assets/assets/content-automation-autotone.png)

   *Figura: L&#39;ottimizzazione automatica delle tonalità e la raddrizzatura automatica possono migliorare le immagini distorte.*

* **Predefiniti Lightroom**: Applica un aspetto definito dall’utente alle immagini per ottenere un aspetto uniforme utilizzando i predefiniti personalizzati.

   ![Predefinito Lightroom](/help/assets/assets/content-automation-lrpresets.png)

   *Figura: Predefinito Adobe Lightroom per migliorare la qualità delle immagini in modo coerente per molte immagini.*

* **Ritaglio immagine**: Utilizza l&#39;intelligenza artificiale per creare una selezione intorno agli oggetti principali e rimuovere lo sfondo con un singolo comando.

   ![Rimuovere lo sfondo e ritagliare un&#39;immagine da una foto](/help/assets/assets/content-automation-backgroundremove.png)

* **Maschera immagine**: Utilizza l&#39;intelligenza artificiale per creare una maschera intorno agli oggetti più importanti con un singolo comando.

   ![Maschera un’immagine utilizzando l’intelligenza artificiale](/help/assets/assets/content-automation-mask.png)

* **Azioni Photoshop**: Applica una serie di [!DNL Adobe Photoshop] attività a un file o a un batch di file.

   ![Azioni Photoshop](/help/assets/assets/content-automation-psactions.png)

* **Sostituzione di oggetti avanzati**: Esegue la personalizzazione su scala consentendo di scambiare le immagini mantenendo tutti gli effetti e le regolazioni applicati all’interno di un file PSD.

   ![Sostituire gli oggetti in modo intelligente](/help/assets/assets/content-automation-objectreplace.png)

## Abilita automazione dei contenuti per AEM programma as a Cloud Service {#enable-content-automation}

Per abilitare il componente aggiuntivo di automazione dei contenuti per AEM programma as a Cloud Service tramite Cloud Manager:

1. Contatta il rappresentante commerciale di riferimento per richiedere la licenza del componente aggiuntivo Content Automation.
1. Accedi a Cloud Manager e passa alla tua organizzazione utilizzando il selettore dell’organizzazione.
1. Fai clic su **[!UICONTROL Aggiungi programma]** e specificare un nome di programma.
1. Fai clic su **[!UICONTROL Continua]**.
1. Espandi **[!UICONTROL Risorse]** e seleziona **[!UICONTROL Automazione dei contenuti]**.
1. Fai clic su **[!UICONTROL Crea]**.
1. Esegui la pipeline in [distribuire le modifiche a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

Se devi aggiungere il componente aggiuntivo per l’automazione dei contenuti a un programma as a Cloud Service AEM esistente in Cloud Manager:

1. Fai clic su ... sulla scheda del programma.

1. Seleziona **[!UICONTROL Modifica programma]** quindi seleziona **[!UICONTROL Soluzioni e componenti aggiuntivi]** scheda .

1. Espandi **[!UICONTROL Risorse]** e seleziona **[!UICONTROL Automazione dei contenuti]**.
1. Fai clic su **[!UICONTROL Aggiorna]**.
1. Esegui la pipeline in [distribuire le modifiche a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## Utilizzare un profilo di elaborazione per modificare in blocco le risorse creative {#process-assets}

Per utilizzare i profili di elaborazione per creare automaticamente le varianti, effettua le seguenti operazioni:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili di elaborazione]**.

1. Seleziona **[!UICONTROL Crea]** e specifica un **[!UICONTROL Nome]**.

1. Seleziona la **[!UICONTROL Creativo]** , specifica la cartella di output, seleziona **[!UICONTROL Aggiungi nuovo]** per aggiungere una configurazione creativa.

1. Fornire **[!UICONTROL Nome rappresentazione]** (o nome di uscita), **[!UICONTROL Estensione]** (o tipo di file), selezionare **[!UICONTROL Qualità]** (o parametri di output), seleziona **[!UICONTROL Include]** e **[!UICONTROL Escludi]** Il tipo MIME elenca (o filtro risorse di input) e seleziona l’operazione creativa richiesta.

   ![[!UICONTROL Creativo] scheda in [!UICONTROL Profilo di elaborazione]](assets/creative-processing-profile.png)

1. Alcune operazioni richiedono parametri aggiuntivi (risorsa). Se necessario, fornisci valori per questi parametri aggiuntivi.

1. Aggiungi più operazioni creative come parte dello stesso profilo di elaborazione o Salva il profilo.

1. Applica il profilo di elaborazione a una cartella. In una cartella **[!UICONTROL Proprietà]** pagina, seleziona **[!UICONTROL Elaborazione delle risorse]**, quindi seleziona il profilo di elaborazione da applicare.

Dopo aver applicato il profilo di elaborazione a una cartella DAM, tutte le risorse caricate o aggiornate in questa cartella eseguono le operazioni definite in aggiunta all’elaborazione standard. Le sottocartelle ereditano gli stessi profili applicati alle cartelle principali. Gli utenti possono ignorare questa ereditarietà.

Per elaborare le risorse esistenti, selezionale **[!UICONTROL Rielaborazione]** , quindi seleziona il profilo di elaborazione richiesto.

## Suggerimenti e limitazioni {#limitations-best-practices}

* [!DNL Experience Manager] limita l’elaborazione delle risorse a 300 richieste al minuto per ambiente e a 700 richieste al minuto per organizzazione.
* La dimensione del file è limitata a 4 GB per [!DNL Adobe Photoshop] Operazioni API e 1 GB per [!DNL Adobe Lightroom] operazioni.

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
>* [Configurare e utilizzare i microservizi per le risorse tramite i profili di elaborazione](/help/assets/asset-microservices-configure-and-use.md).
>* [ [!DNL Experience Manager] Integrare con [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [Acquisizione ed elaborazione delle risorse con i microservizi per le risorse: Panoramica](/help/assets/asset-microservices-overview.md).

