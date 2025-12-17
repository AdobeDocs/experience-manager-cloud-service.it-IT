---
title: Integra [!DNL AEM Assets] con [!DNL Figma].
description: Scopri come integrare  [!DNL AEM Assets] con [!DNL Figma] per accedere e utilizzare le risorse della tua organizzazione nel flusso di lavoro di progettazione [!DNL Figma] .
hide: false
role: User
exl-id: 530561ca-497b-4331-a014-72c561e1ca84
source-git-commit: a9c1f5472092b3b9fa7a5e5570feb92f32e9ef6c
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 1%

---


# Integra [!DNL AEM Assets] con [!DNL Figma]{#integrate-aem-assets-with-figma}

[!DNL AEM Assets] si integra in modo nativo con [!DNL Figma], consentendo ai designer di accedere direttamente alle risorse archiviate in [!DNL AEM Assets] dall&#39;interfaccia utente di [!DNL Figma]. È possibile inserire contenuto gestito in [!DNL AEM Assets] nell&#39;area di lavoro [!DNL Figma] e quindi salvare contenuto nuovo o modificato nell&#39;archivio [!DNL AEM Assets].

## Prima di iniziare{#prerequisites-for-aem-assets-and-figma-integration}

* La versione minima richiesta di AEM è `19149`.

* Per integrare [!DNL AEM Assets] con [!DNL Figma] è necessario disporre di [!DNL AEM Assets] e [!DNL Figma] licenze valide.

## Formati di file supportati {#supported-file-formats-integration-figma}


* Per importare risorse [!DNL AEM] in Figma, i formati supportati sono risorse immagine (JPEG, PNG), file video (MP4, MOV, WebM), file animati (GIF) e file vettoriali (SVG).
* Per esportare le progettazioni da [!DNL Figma] a [!DNL AEM Assets], i formati supportati sono **PNG**, **PDF**, **JPG**, **SVG**.

## Accedi a [!UICONTROL Connettore Assets di Adobe Experience Manager (AEM)]{#access-aem-assets-connector}

Eseguire i passaggi seguenti per accedere al connettore Assets di [!UICONTROL Adobe Experience Manager (AEM)]:

1. Nella home page di [!DNL Figma], fai clic su **[!UICONTROL Azioni]** nella barra degli strumenti nella parte inferiore dell&#39;area di lavoro e cerca [!DNL Adobe Experience Manager (AEM) Assets Connector] nella barra di ricerca disponibile nella finestra di dialogo.
1. Selezionare [!DNL Adobe Experience Manager (AEM) Assets Connector] per visualizzare il pannello [!DNL Adobe Experience Manager (AEM) Assets Connector]. [Importa [!DNL AEM] le risorse nell&#39;area di lavoro [!DNL Figma] ](#import-aem-assets-into-figma-workflow) tramite questo pannello.
   ![azioni](/help/assets/assets/actions-on-figma.png)
In alternativa, accedere a [[!DNL Adobe Experience Manager (AEM) Assets Connector]](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector) disponibile nella community [!DNL Figma], fare clic su **[!UICONTROL Apri in...]**, selezionare un file recente o crearne uno nuovo e fare clic su **[!UICONTROL Esegui]** per accedere al pannello [!DNL Adobe Experience Manager (AEM) Assets Connector].
   ![plugin-page-on-figma-community](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> [Contatta il supporto Adobe](https://helpx.adobe.com/contact.html) per assistenza se dopo l&#39;accesso all&#39;ambiente **[!UICONTROL ricevi un messaggio di]** errore di rete[!DNL AEM].

## Importa [!DNL AEM] risorse nell&#39;area di lavoro [!DNL Figma]{#import-aem-assets-into-figma-workflow}

[Accedi al pannello [!UICONTROL Connettore Assets di Adobe Experience Manager (AEM)]](#access-aem-assets-connector) nell&#39;interfaccia di progettazione di [!DNL Figma] ed effettua le seguenti operazioni:

1. Cerca le risorse nel pannello [!UICONTROL Connettore Assets di Adobe Experience Manager (AEM)]. Per ulteriori informazioni, consulta [utilizzo di Asset Selector](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector).

1. Trascina e rilascia la risorsa nell&#39;area di lavoro o selezionala e fai clic su **[!UICONTROL Seleziona]** per inserire la risorsa nell&#39;area di lavoro.

1. Fai clic su ![tre punti](/help/assets/assets/three-dots.svg) nel percorso della cartella per visualizzare tutte le cartelle principali e secondarie nella gerarchia corrente. Seleziona una cartella per passare a tale posizione.
   ![tre punti](/help/assets/assets/figma-v2-plugin.png)

1. [Facoltativo] Fare clic su **[!UICONTROL Verifica aggiornamenti]**. Le risorse utilizzate nel documento Figma attuale vengono confrontate con le risorse esistenti in AEM. Tutti gli aggiornamenti vengono elencati in una finestra separata. Fai clic su **[!UICONTROL Aggiorna]** per inserire la risorsa aggiornata da AEM nel documento Figma.

Quando la progettazione Figma è pronta, puoi [esportare la risorsa nell&#39;archivio AEM Assets](#export-figma-design-to-aem-assets-folder).

## Esporta risorse nell&#39;archivio [!DNL AEM Assets]{#export-figma-design-to-aem-assets-folder}

[Accedi al pannello [!UICONTROL Adobe Experience Manager (AEM) Assets Connector]](#access-aem-assets-connector) nell&#39;interfaccia di progettazione di [!DNL Figma] ed esegui i seguenti passaggi per esportare la progettazione nell&#39;archivio [!DNL AEM Assets]:

1. Passare alla cartella di destinazione in cui si desidera salvare la progettazione [!DNL Figma]. Se ti trovi già all&#39;interno di una cartella, fai clic su Altre opzioni (![tre punti](/help/assets/assets/three-dots.svg)) nel percorso della cartella per selezionare un&#39;altra cartella di destinazione.
1. Facoltativo: raggruppa le risorse nell’area di lavoro per selezionarle come una singola unità da caricare nella cartella.
1. Fai clic su ![caricamento file](/help/assets/assets/upload-icon.svg) **[!UICONTROL Caricamento]** per visualizzare la finestra di dialogo **[!UICONTROL Carica risorsa]**.
1. Nella finestra di dialogo, seleziona **[!UICONTROL Elemento selezionato]** o **[!UICONTROL Pagina]**, specifica un nome di file o di pagina, definisci una configurazione di esportazione e fai clic su **[!UICONTROL Carica]** per caricare la risorsa selezionata o l&#39;intera struttura nella cartella di destinazione.

   La configurazione di esportazione comprende il formato di file, la scala e la qualità. Se ad esempio si seleziona JPG come formato di file, è possibile definire anche la scala e la qualità dell&#39;immagine. Analogamente, se selezionate PNG come formato di file, potete anche definire la scala dell&#39;immagine.
   ![carica progettazione figma](/help/assets/assets/upload-figma-design.png)
