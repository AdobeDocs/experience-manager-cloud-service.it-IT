---
title: Gestisci pubblicazione
description: Pubblicare o annullare la pubblicazione delle risorse in Experience Manager Assets, Dynamic Media e Brand Portal
contentOwner: Vishabh Gupta
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 9%

---

# Gestire la pubblicazione in Experience Manager Assets {#manage-publication-in-aem}

Come [!DNL Adobe Experience Manager Assets] amministratore, puoi pubblicare risorse e cartelle contenenti risorse dall’istanza di authoring a [!DNL Experience Manager Assets], [!DNL Dynamic Media]e [!DNL Brand Portal]. Puoi anche pianificare il flusso di lavoro di una risorsa o di una cartella in modo che venga pubblicata in una data o in un’ora successiva. Dopo la pubblicazione, gli utenti possono accedere e distribuire ulteriormente le risorse ad altri utenti. Per impostazione predefinita, puoi pubblicare risorse e cartelle in [!DNL Experience Manager Assets]. Tuttavia, puoi configurare [!DNL Experience Manager Assets] per abilitare la pubblicazione in [[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html) e [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

Puoi pubblicare o annullare la pubblicazione delle risorse a livello di risorsa o di cartella utilizzando **[!UICONTROL Pubblicazione rapida]** o **[!UICONTROL Gestisci pubblicazione]** opzione disponibile in [!DNL Experience Manager Assets] interfaccia. Se apporti modifiche successive alla risorsa o alla cartella originale in [!DNL Experience Manager Assets], le modifiche vengono riportate nell’istanza di pubblicazione solo dopo la ripubblicazione da [!DNL Experience Manager Assets]. In questo modo le modifiche in corso di lavorazione non sono disponibili nell’istanza di pubblicazione. Nell’istanza di pubblicazione sono disponibili solo le modifiche approvate pubblicate da un amministratore.

* [Pubblicare risorse tramite Pubblicazione rapida](#quick-publish)
* [Pubblicare risorse tramite Gestisci pubblicazione](#manage-publication)
* [Pubblicare le risorse in un secondo momento](#publish-assets-later)
* [Pubblicare risorse in Dynamic Media](#publish-assets-to-dynamic-media)
* [Pubblicare risorse su Brand Portal](#publish-assets-to-brand-portal)
* [Limitazioni e suggerimenti](#limitations-and-tips)

## Pubblicare risorse tramite Pubblicazione rapida {#quick-publish}

La pubblicazione rapida consente di pubblicare immediatamente i contenuti nella destinazione selezionata. Da [!DNL Experience Manager Assets] console, passa alla cartella principale e seleziona tutte le risorse o le cartelle da pubblicare. Fai clic su **[!UICONTROL Pubblicazione rapida]** dalla barra degli strumenti e seleziona la destinazione dall’elenco a discesa in cui vuoi pubblicare le risorse.

![Pubblicazione rapida](assets/quick-publish-to-aem.png)

## Pubblicare risorse tramite Gestisci pubblicazione {#manage-publication}

Gestisci pubblicazione consente di pubblicare o annullare la pubblicazione dei contenuti da e verso la destinazione selezionata, [aggiungi contenuto](#add-content) all’elenco di pubblicazione dall’archivio DAM, [includere le impostazioni della cartella](#include-folder-settings) per pubblicare il contenuto delle cartelle selezionate e applicare i filtri, e [pianificazione della pubblicazione](#publish-assets-later) a una data o un&#39;ora successiva.

Da [!DNL Experience Manager Assets] console, passa alla cartella principale e seleziona tutte le risorse o le cartelle da pubblicare. Fai clic su **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti. Se non hai [!DNL Dynamic Media] e [!DNL Brand Portal] configurato nel [!DNL Experience Manager Assets] ad esempio, puoi pubblicare risorse e cartelle solo in [!DNL Experience Manager Assets].

![Gestisci pubblicazione](assets/manage-publication-aem.png)

Le seguenti opzioni sono disponibili nel [!UICONTROL Gestisci pubblicazione] interfaccia:

* [!UICONTROL Azioni]
   * `Publish`: Pubblicare risorse e cartelle nella destinazione selezionata
   * `Unpublish`: Annullare la pubblicazione di risorse e cartelle dalla destinazione

* [!UICONTROL Destinazione]
   * `Publish`: Pubblicare risorse e cartelle su [!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`: Pubblicare risorse su [!DNL Dynamic Media]
   * `Brand Portal`: Pubblicare risorse e cartelle su [!DNL Brand Portal]

* [!UICONTROL Pianificazione]
   * `Now`: Pubblicare immediatamente le risorse
   * `Later`: Pubblicare le risorse in base alla `Activation` data o ora

Per continuare, fai clic su **[!UICONTROL Successivo]**. In base alla selezione, il **[!UICONTROL Ambito]** La scheda riflette diverse opzioni. Le opzioni per **[!UICONTROL Aggiungi contenuto]** e **[!UICONTROL Includi impostazioni cartella]** sono disponibili solo per la pubblicazione delle risorse e delle cartelle in [!DNL Experience Manager Assets] (`Destination: Publish`).

![Ambito di Gestisci pubblicazione](assets/manage-publication-aem-scope.png)

### Aggiungi contenuto {#add-content}

Pubblicazione su [!DNL Experience Manager Assets] consente di aggiungere ulteriori contenuti (risorse e cartelle) all’elenco di pubblicazione. È possibile aggiungere ulteriori risorse o cartelle all’elenco negli archivi dam. Fai clic su **[!UICONTROL Aggiungi contenuto]** per aggiungere altro contenuto.

È possibile aggiungere più risorse da una cartella o più cartelle alla volta. Ma non è possibile aggiungere risorse da più cartelle alla volta.

![Aggiungi contenuto](assets/manage-publication-add-content.png)

### Impostazioni cartelle da includere {#include-folder-settings}

Per impostazione predefinita, quando si pubblica una cartella in [!DNL Experience Manager Assets] pubblica tutte le risorse, le sottocartelle e i relativi riferimenti.

Per filtrare il contenuto della cartella da pubblicare, fai clic su **[!UICONTROL Includi impostazioni cartella]**:

* `Include folder contents`

   * Abilitato: Vengono pubblicate tutte le risorse della cartella, delle sottocartelle (incluse tutte le risorse delle sottocartelle) e i riferimenti.
   * Disabilitata: Vengono pubblicati solo la cartella selezionata (vuota) e i riferimenti. Le risorse della cartella selezionata non vengono pubblicate.

* `Include folder contents` e `Include only immediate folder contents`

   Se sono selezionate entrambe le opzioni, vengono pubblicate tutte le risorse della cartella, delle sottocartelle (vuote) e dei riferimenti selezionati. Le risorse delle sottocartelle non vengono pubblicate.

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![Impostazioni cartelle da includere](assets/manage-publication-include-folder-settings.png)

Dopo aver applicato i filtri, fai clic su **[!UICONTROL OK]**, quindi fai clic su **[!UICONTROL Pubblica]**. Fai clic sul pulsante pubblica per visualizzare un messaggio di conferma `Resource(s) have been scheduled for publication` appare. E le risorse e (o) cartelle selezionate vengono pubblicate nella destinazione definita in base alla pianificazione (`Now` o `Later`). Accedi all’istanza di pubblicazione per verificare che le risorse e (o) le cartelle siano state pubblicate correttamente.

![Pubblica in AEM](assets/manage-publication-publish-aem.png)

Nell’illustrazione precedente, puoi vedere valori diversi per i **[!UICONTROL Pubblicare Target]** attributo. Ricordiamoci che hai scelto di pubblicare [!DNL Experience Manager Assets] (`Destination: Publish`). Quindi, perché mostra che solo una cartella e una risorsa sono pubblicate in `AEM`e le altre due risorse vengono pubblicate in entrambi `AEM` e `Dynamic Media`?

In questo caso è necessario comprendere il ruolo delle proprietà della cartella. Una cartella **[!UICONTROL Modalità di pubblicazione Dynamic Media]** la proprietà svolge un ruolo importante nella pubblicazione. Per visualizzare le proprietà di una cartella, selezionala e fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti. Per una risorsa, consulta le proprietà della relativa cartella principale.

Nella tabella seguente viene illustrato come si verifica la pubblicazione a seconda dei valori definiti **[!UICONTROL Destinazione]** e **[!UICONTROL Modalità di pubblicazione Dynamic Media]**:

| [!UICONTROL Destinazione] | [!UICONTROL Modalità di pubblicazione Dynamic Media] | [!UICONTROL Destinazione pubblicazione] | Contenuto consentito |
| --- | --- | --- | --- |
| Pubblicazione | Pubblicazione selettiva | `AEM` | Risorse e/o cartelle |
| Pubblicazione | Immediato | `AEM` e `Dynamic Media` | Risorse e/o cartelle |
| Pubblicazione | All&#39;attivazione | `AEM` e `Dynamic Media` | Risorse e/o cartelle |
| Dynamic Media | Pubblicazione selettiva | `Dynamic Media` | Risorse |
| Dynamic Media | Immediato | `None` | Impossibile pubblicare le risorse |
| Dynamic Media | All&#39;attivazione | `None` | Impossibile pubblicare le risorse |

>[!NOTE]
>
>Solo le risorse vengono pubblicate in [!DNL Dynamic Media].
>
>Pubblicazione di una cartella in [!DNL Dynamic Media] non è supportato.
>
>Se selezioni una cartella (`Selective Publish`) e scegli la [!DNL Dynamic Media] la destinazione, [!UICONTROL Pubblicare Target] riflesso dell&#39;attributo `None`.


Ora cambiamo le **[!UICONTROL Destinazione]** nel caso d&#39;uso precedente a **[!UICONTROL Dynamic Media]** e verifica i risultati. In questo modo, solo la risorsa di `Selective Publish` la cartella viene pubblicata in [!DNL Dynamic Media]. Le attività `Immediate` e `Upon Activation` le cartelle non vengono pubblicate e riflettono `None`.

![Pubblica in Dynamic Media](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>Se [!DNL Dynamic Media] non è configurato sul tuo [!DNL Experience Manager Assets] e **[!UICONTROL Destinazione]** è **[!UICONTROL Pubblica]**, le risorse e le cartelle vengono sempre pubblicate in `AEM`.
>
>Pubblicazione su [!DNL Brand Portal] è indipendente dalle proprietà della cartella. Tutte le risorse, le cartelle e le raccolte possono essere pubblicate in Brand Portal. Vedi [pubblicare risorse in Brand Portal](#publish-assets-to-brand-portal).

>[!NOTE]
>
>Se hai personalizzato la [!DNL Manage Publication] , la personalizzazione continua a funzionare con le funzionalità esistenti.
>
>Tuttavia, è possibile rimuovere la personalizzazione esistente per utilizzare il nuovo [!DNL Manager Publication] funzionalità.


## Pubblicare le risorse in un secondo momento {#publish-assets-later}

Per pianificare il flusso di lavoro di pubblicazione delle risorse in una data o un’ora successiva:

1. Da [!UICONTROL Experience Manager Assets] console, passa alla cartella principale e seleziona tutte le risorse o le cartelle da pianificare per la pubblicazione.
1. Fai clic su **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti.
1. Fai clic su **[!UICONTROL Pubblica]** da **[!UICONTROL Azione]**, quindi seleziona la **[!UICONTROL Destinazione]** dove vuoi pubblicare il contenuto.
1. Seleziona **[!UICONTROL Più tardi]** in **[!UICONTROL Pianificazione]**.
1. Seleziona un **[!UICONTROL Data di attivazione]** e specifica la data e l&#39;ora. Fai clic su **[!UICONTROL Avanti]**.

   ![Flusso di lavoro Gestisci pubblicazione](assets/manage-publication-workflow.png)

1. In **[!UICONTROL Ambito]** scheda **[!UICONTROL Aggiungi contenuto]** (se necessario). Fai clic su **[!UICONTROL Avanti]**.
1. In **[!UICONTROL Flussi di lavoro]** Specifica un titolo del flusso di lavoro. Fai clic su **[!UICONTROL Pubblica più tardi]**.

   ![Titolo flusso di lavoro](assets/manage-publication-workflow-title.png)

   Accedi all’istanza di destinazione per verificare le risorse pubblicate (a seconda della data o dell’ora pianificata).

## Pubblicare risorse in Dynamic Media {#publish-assets-to-dynamic-media}

Solo le risorse vengono pubblicate in [!DNL Dynamic Media]. Tuttavia, il comportamento di pubblicazione è diverso in base alle proprietà della cartella. Una cartella può avere **[!UICONTROL Modalità di pubblicazione Dynamic Media]** configurato per la pubblicazione selettiva che può essere uno dei seguenti:

* `Selective Publish`
* `Immediate`
* `Upon Activation`

Il processo di pubblicazione per **[!UICONTROL Immediato]** e **[!UICONTROL All&#39;attivazione]** tuttavia, la modalità è diversa per **[!UICONTROL Pubblicazione selettiva]**. Vedi [configurare la pubblicazione selettiva a livello di cartella in Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html). Dopo aver configurato la pubblicazione selettiva in una cartella, puoi effettuare una delle seguenti operazioni:

* [Pubblicare in modo selettivo le risorse in Dynamic Media o Experience Manager utilizzando Gestisci pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [Annullare selettivamente la pubblicazione delle risorse da Dynamic Media o Experience Manager tramite Gestisci pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [Pubblicare risorse in Dynamic Media o Experience Manager tramite Pubblicazione rapida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [Pubblicare o annullare selettivamente la pubblicazione delle risorse tramite i risultati della ricerca](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## Pubblicare risorse su Brand Portal {#publish-assets-to-brand-portal}

È possibile pubblicare risorse, cartelle e raccolte nel [!DNL Experience Manager Assets Brand Portal] istanza.

* [Pubblicare risorse su Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [Pubblicare cartelle su Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [Pubblicare raccolte su Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## Limitazioni e suggerimenti {#limitations-and-tips}

* L’opzione [!UICONTROL Gestisci pubblicazione] è disponibile solo per gli account utente che dispongono di autorizzazioni di replica.
* Le cartelle vuote non vengono pubblicate.
* Se pubblichi una risorsa in fase di elaborazione, viene pubblicato solo il contenuto originale. Mancano i rendering. Attendi il completamento dell’elaborazione, quindi pubblica o ripubblica la risorsa al termine dell’elaborazione.
* Quando si annulla la pubblicazione di una risorsa complessa, è necessario annullare la pubblicazione solo della risorsa. Evita di annullare la pubblicazione dei riferimenti perché potrebbero essere referenziati da altre risorse pubblicate.

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
