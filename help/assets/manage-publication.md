---
title: Gestisci pubblicazione
description: Pubblicare o annullare la pubblicazione delle risorse in Experience Manager Assets, Dynamic Medie e Brand Portal
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 6%

---

# Gestire la pubblicazione in Experience Manager Assets {#manage-publication-in-aem}

Come un [!DNL Adobe Experience Manager Assets] amministratore, puoi pubblicare su risorse e cartelle contenenti risorse dall’istanza di authoring [!DNL Experience Manager Assets], [!DNL Dynamic Media], e [!DNL Brand Portal]. Inoltre, puoi pianificare la pubblicazione di una risorsa o cartella in una data o in un’ora successiva. Dopo la pubblicazione, gli utenti possono accedere e distribuire ulteriormente le risorse ad altri utenti. Per impostazione predefinita, puoi pubblicare risorse e cartelle in [!DNL Experience Manager Assets]. Tuttavia, puoi configurare [!DNL Experience Manager Assets] per abilitare la pubblicazione su [[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html) e [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

Puoi pubblicare o annullare la pubblicazione delle risorse a livello di risorsa o cartella utilizzando **[!UICONTROL Pubblicazione rapida]** o **[!UICONTROL Gestisci pubblicazione]** opzione disponibile in [!DNL Experience Manager Assets] di rete. Se apporti successive modifiche alla risorsa o alla cartella originale in [!DNL Experience Manager Assets], le modifiche non vengono applicate nell’istanza di pubblicazione fino a quando non si ripubblica da [!DNL Experience Manager Assets]. In questo modo le modifiche in corso di lavorazione non sono disponibili nell’istanza di pubblicazione. Nell’istanza di pubblicazione sono disponibili solo le modifiche approvate pubblicate da un amministratore.

* [Pubblicare le risorse tramite la pubblicazione rapida](#quick-publish)
* [Pubblicare risorse tramite Gestisci pubblicazione](#manage-publication)
* [Pubblicare le risorse in un secondo momento](#publish-assets-later)
* [Pubblicare risorse in Dynamic Medie](#publish-assets-to-dynamic-media)
* [Pubblicare risorse su Brand Portal](#publish-assets-to-brand-portal)
* [Richiedi pubblicazione](#request-publication)
* [Limitazioni e suggerimenti](#limitations-and-tips)

## Pubblicare le risorse tramite la pubblicazione rapida {#quick-publish}

La pubblicazione rapida consente di pubblicare immediatamente il contenuto nella destinazione selezionata. Dalla sezione [!DNL Experience Manager Assets] , passa alla cartella principale e seleziona tutte le risorse o cartelle da pubblicare. Clic **[!UICONTROL Pubblicazione rapida]** dalla barra degli strumenti e seleziona destinazione dall’elenco a discesa in cui desideri pubblicare le risorse.

![Pubblicazione rapida](assets/quick-publish-to-aem.png)

## Pubblicare risorse tramite Gestisci pubblicazione {#manage-publication}

Gestisci pubblicazione consente di pubblicare o annullare la pubblicazione dei contenuti da e verso la destinazione selezionata, [aggiungi contenuto](#add-content) all’elenco di pubblicazione dall’archivio DAM, [includi impostazioni cartella](#include-folder-settings) per pubblicare il contenuto delle cartelle selezionate e applicare i filtri [pubblicazione programmata](#publish-assets-later) a una data o un’ora successiva.

Dalla sezione [!DNL Experience Manager Assets] , passa alla cartella principale e seleziona tutte le risorse o cartelle da pubblicare. Clic **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti. Se non ha [!DNL Dynamic Media] e [!DNL Brand Portal] configurato nel tuo [!DNL Experience Manager Assets] pubblica risorse e cartelle solo in [!DNL Experience Manager Assets].

![Gestisci pubblicazione](assets/manage-publication-aem.png)

Le seguenti opzioni sono disponibili nel [!UICONTROL Gestisci pubblicazione] Interfaccia:

* [!UICONTROL Azioni]
   * `Publish`: pubblica risorse e cartelle nella destinazione selezionata
   * `Unpublish`: annulla la pubblicazione di risorse e cartelle dalla destinazione

* [!UICONTROL Destinazione]
   * `Publish`: pubblicazione di risorse e cartelle in [!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`: Pubblicare risorse su [!DNL Dynamic Media]
   * `Brand Portal`: pubblicazione di risorse e cartelle in [!DNL Brand Portal]

* [!UICONTROL Pianificazione]
   * `Now`: pubblica immediatamente le risorse
   * `Later`: pubblica le risorse in base a `Activation` data o ora

Per continuare, fai clic su **[!UICONTROL Successivo]**. In base alla selezione, il **[!UICONTROL Ambito]** riflettono opzioni diverse. Le opzioni per **[!UICONTROL Aggiungi contenuto]** e **[!UICONTROL Includi impostazioni cartella]** sono disponibili solo per la pubblicazione di risorse e cartelle in [!DNL Experience Manager Assets] (`Destination: Publish`).

![Ambito di Gestisci pubblicazione](assets/manage-publication-aem-scope.png)

### Aggiungi contenuto {#add-content}

Pubblicazione in [!DNL Experience Manager Assets] consente di aggiungere ulteriore contenuto (risorse e cartelle) all’elenco di pubblicazione. Puoi aggiungere più risorse o cartelle all’elenco negli archivi DAM. Clic **[!UICONTROL Aggiungi contenuto]** per aggiungere altri contenuti.

Puoi aggiungere più risorse da una cartella o più cartelle alla volta. Tuttavia, non è possibile aggiungere risorse da più cartelle alla volta.

![Aggiungi contenuto](assets/manage-publication-add-content.png)

### Impostazioni cartelle da includere {#include-folder-settings}

Per impostazione predefinita, la pubblicazione di una cartella in [!DNL Experience Manager Assets] pubblica tutte le risorse, le sottocartelle e i relativi riferimenti.

Per filtrare il contenuto della cartella da pubblicare, fai clic su **[!UICONTROL Includi impostazioni cartella]**:

* `Include folder contents`

   * Abilitato: vengono pubblicate tutte le risorse della cartella selezionata, delle sottocartelle (comprese tutte le risorse delle sottocartelle) e dei riferimenti.
   * Disabilitato: vengono pubblicati solo la cartella selezionata (vuota) e i riferimenti. Le risorse della cartella selezionata non vengono pubblicate.

* `Include folder contents` e `Include only immediate folder contents`

  Se sono selezionate entrambe le opzioni, vengono pubblicate tutte le risorse della cartella selezionata, delle sottocartelle (vuote) e dei riferimenti. Le risorse delle sottocartelle non vengono pubblicate.

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![Impostazioni cartelle da includere](assets/manage-publication-include-folder-settings.png)

Dopo aver applicato i filtri, fai clic su **[!UICONTROL OK]** e quindi fare clic su **[!UICONTROL Pubblica]**. Facendo clic sul pulsante Publish, viene visualizzato un messaggio di conferma `Resource(s) have been scheduled for publication` viene visualizzato. E le risorse e/o cartelle selezionate vengono pubblicate nella destinazione definita in base alla pianificazione (`Now` o `Later`). Accedi all’istanza di pubblicazione per verificare che le risorse e/o le cartelle siano state pubblicate correttamente.

![Pubblica in AEM](assets/manage-publication-publish-aem.png)

Nell’illustrazione precedente, puoi vedere valori diversi per **[!UICONTROL Destinazione pubblicazione]** attributo. Ricordiamo che hai scelto di pubblicare su [!DNL Experience Manager Assets] (`Destination: Publish`). Quindi, perché mostra che solo una cartella e una risorsa sono pubblicate in `AEM`e le altre due risorse vengono pubblicate in entrambi `AEM` e `Dynamic Media`?

In questo caso, è necessario comprendere il ruolo delle proprietà della cartella. Di una cartella **[!UICONTROL Modalità di pubblicazione Dynamic Medie]** La proprietà svolge un ruolo importante nella pubblicazione. Per visualizzare le proprietà di una cartella, selezionala e fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti. Per una risorsa, vedi le proprietà della relativa cartella principale.

La tabella seguente spiega come si verifica la pubblicazione in base al **[!UICONTROL Destinazione]** e **[!UICONTROL Modalità di pubblicazione Dynamic Medie]**:

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
>Se si seleziona una cartella (`Selective Publish`) e scegliere il [!DNL Dynamic Media] destinazione, il [!UICONTROL Destinazione pubblicazione] riflessi attributo `None`.


Cambiiamo ora il **[!UICONTROL Destinazione]** nel caso d’uso precedente, per **[!UICONTROL Dynamic Medie]** e verificare i risultati. In questo modo, solo la risorsa di `Selective Publish` la cartella è pubblicata in [!DNL Dynamic Media]. Le risorse di `Immediate` e `Upon Activation` cartelle non sono pubblicate e riflette `None`.

![Pubblica in Dynamic Media](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>Se [!DNL Dynamic Media] non è configurato sul tuo [!DNL Experience Manager Assets] e **[!UICONTROL Destinazione]** è **[!UICONTROL Pubblica]**, le risorse e le cartelle vengono sempre pubblicate in `AEM`.
>
>Pubblicazione in [!DNL Brand Portal] è indipendente dalle proprietà della cartella. Tutte le risorse, le cartelle e le raccolte possono essere pubblicate in Brand Portal. Consulta [pubblicare risorse in Brand Portal](#publish-assets-to-brand-portal).

>[!NOTE]
>
>Se hai personalizzato [!DNL Manage Publication] , la personalizzazione continua a funzionare con le funzionalità esistenti.
>
>Tuttavia, puoi rimuovere la personalizzazione esistente per utilizzare il nuovo [!DNL Manager Publication] funzioni.

## Pubblicare le risorse in un secondo momento {#publish-assets-later}

Per pianificare il flusso di lavoro di pubblicazione delle risorse in una data o in un’ora successiva:

1. Dalla sezione [!UICONTROL Experience Manager Assets] , passa alla cartella principale e seleziona tutte le risorse o cartelle che desideri pianificare per la pubblicazione.
1. Clic **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti.
1. Clic **[!UICONTROL Pubblica]** da **[!UICONTROL Azione]**, quindi selezionare **[!UICONTROL Destinazione]** dove desideri pubblicare il contenuto.
1. Seleziona **[!UICONTROL Più tardi]** in **[!UICONTROL Pianificazione]**.
1. Seleziona un **[!UICONTROL Data di attivazione]** e specifica la data e l’ora. Fai clic su **[!UICONTROL Avanti]**.

   ![Flusso di lavoro Gestisci pubblicazione](assets/manage-publication-workflow.png)

1. In **[!UICONTROL Ambito]** scheda, **[!UICONTROL Aggiungi contenuto]** se necessario. Fai clic su **[!UICONTROL Avanti]**.
1. In **[!UICONTROL Flussi di lavoro]** , specifica un titolo del flusso di lavoro. Fai clic su **[!UICONTROL Pubblica più tardi]**.

   ![Titolo flusso di lavoro](assets/manage-publication-workflow-title.png)

   Accedi all’istanza di destinazione per verificare le risorse pubblicate (a seconda della data o dell’ora pianificata).

## Pubblicare risorse in Dynamic Medie {#publish-assets-to-dynamic-media}

Solo le risorse vengono pubblicate in [!DNL Dynamic Media]. Tuttavia, il comportamento di pubblicazione varia in base alle proprietà della cartella. Una cartella può avere **[!UICONTROL Modalità di pubblicazione Dynamic Medie]** configurate per la pubblicazione selettiva che può essere una delle seguenti:

* `Selective Publish`
* `Immediate`
* `Upon Activation`

Il processo di pubblicazione per **[!UICONTROL Immediato]** e **[!UICONTROL All&#39;attivazione]** è coerente, tuttavia è diversa per **[!UICONTROL Pubblicazione selettiva]**. Consulta [configurare la pubblicazione selettiva a livello di cartella in Dynamic Medie](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html). Dopo aver configurato la pubblicazione selettiva in una cartella, puoi effettuare una delle seguenti operazioni:

* [Pubblicare selettivamente le risorse in Dynamic Medie o Experience Manager tramite Gestisci pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [Annullare la pubblicazione selettiva di risorse da Dynamic Medie o Experience Manager tramite Gestisci pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [Pubblicare risorse in Dynamic Medie o Experience Manager tramite Pubblicazione rapida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [Pubblicare o annullare la pubblicazione selettiva delle risorse tramite i risultati della ricerca](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## Pubblicare risorse su Brand Portal {#publish-assets-to-brand-portal}

Puoi pubblicare risorse, cartelle e raccolte in [!DNL Experience Manager Assets Brand Portal] dell&#39;istanza.

* [Pubblicare risorse su Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [Pubblicare cartelle su Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [Pubblicare raccolte su Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## Richiedi pubblicazione {#request-publication}

Il `Request Publication` consente di autenticare il flusso di lavoro delle risorse prima di pubblicarle in [!DNL AEM] Ambiente risorse. [!DNL AEM] fornisce un diverso livello di autorizzazioni a vari utenti. Puoi essere un *collaboratore* che sta caricando le risorse, ma non può pubblicarle finché non vengono verificati i caricamenti. Inoltre, essendo un *Amministratore* puoi gestire la lettura e la scrittura dei flussi di lavoro di Assets.

L’opzione Richiedi pubblicazione è disponibile per i seguenti utenti:

* **Collaboratore:** Se sei un utente che può contribuire a [!DNL AEM] Assets, quindi hai accesso limitato al [!DNL AEM] Flusso di lavoro delle risorse. `Manage publication` Il pulsante è nascosto per te. In qualità di collaboratore, puoi contribuire solo aggiungendo risorse, ma non puoi pubblicarle o avere accesso in lettura al flusso di lavoro.

* **Utente flusso di lavoro:** Questo utente non può pubblicare le risorse, ma ha accesso in lettura al flusso di lavoro. In qualità di utente del flusso di lavoro, puoi:
   * richiedi pubblicazione
   * visualizza `Manage publication` pulsante
   * pianificare il flusso di lavoro e visualizzare le opzioni `schedule now` e `schedule later`

* **Amministratore:** In qualità di utente amministratore, puoi gestire i passaggi generali del flusso di lavoro per Assets. `Manage publication` è visibile. Se la destinazione `publish` , puoi pianificare una risorsa in un secondo momento per il passaggio del flusso di lavoro.

>[!NOTE]
>
>Se [!DNL Dynamic Media] è selezionato come destinazione, quindi il passaggio del flusso di lavoro è disabilitato per **utente del flusso di lavoro** e **admin** utenti.
>

## Limitazioni e suggerimenti {#limitations-and-tips}

* `Manage publication` è disponibile per gli utenti che dispongono almeno delle autorizzazioni di lettura per il flusso di lavoro.
* Le cartelle vuote non vengono pubblicate.
* Se pubblichi una risorsa in fase di elaborazione, viene pubblicato solo il contenuto originale. Mancano le rappresentazioni. Attendi il completamento dell’elaborazione, quindi pubblica o ripubblica la risorsa al termine dell’elaborazione.
* Durante l’annullamento della pubblicazione di una risorsa complessa, annulla solo la pubblicazione della risorsa. Evita di annullare la pubblicazione dei riferimenti, poiché altre risorse pubblicate potrebbero farvi riferimento.
