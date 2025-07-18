---
title: Pubblicare risorse, cartelle e raccolte su Brand Portal
description: Pubblicare risorse, cartelle e raccolte su Brand Portal.
contentOwner: Adobe
feature: Brand Portal, Asset Distribution, Configuration
role: User
exl-id: 1cc438bc-8cad-4421-af03-c1f6d750e0a8
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 85%

---

# Pubblicare risorse in Brand Portal {#publish-assets-to-brand-portal}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/assets/brandportal/brand-portal-publish-assets) |
| AEM as a Cloud Service | Questo articolo |

In qualità di amministratore di Adobe Experience Manager (AEM) Assets, puoi pubblicare risorse, cartelle e raccolte nell’istanza di Brand Portal di AEM Assets. Puoi anche pianificare il flusso di lavoro di una risorsa o di una cartella in modo che venga pubblicata in una data o in un’ora successiva. Dopo la pubblicazione, gli utenti di Brand Portal possono accedere e distribuire ulteriormente risorse, cartelle e raccolte ad altri utenti.

Devi però prima configurare AEM Assets con Brand Portal. Per ulteriori dettagli, consulta [Configurare AEM Assets con Brand Portal](configure-aem-assets-with-brand-portal.md).

Le eventuali modifiche apportate successivamente alla risorsa, alla cartella o alla raccolta originale in AEM Assets non verranno applicate in Brand Portal finché non vengono ripubblicate da AEM Assets. Questa funzione garantisce che le modifiche in corso d’opera non siano disponibili in Brand Portal. Solo le modifiche approvate pubblicate da un amministratore sono infatti disponibili in Brand Portal.

* [Pubblicare risorse in Brand Portal](#publish-assets-to-bp)
* [Pubblicare cartelle in Brand Portal](#publish-folders-to-brand-portal)
* [Pubblicare raccolte in Brand Portal](#publish-collections-to-brand-portal)

>[!NOTE]
>
>Adobe consiglia di scaglionare la pubblicazione, eseguendola preferibilmente nelle ore non di picco, in modo che AEM Author non utilizzi troppe risorse.
>&#x200B;>Assets deve essere pubblicato in batch. Il valore consigliato per la dimensione del batch è 15K.
>&#x200B;> Per [!DNL Experience Manager Assets] come [!DNL Cloud Service], la velocità di trasferimento osservata in condizioni lab è di 1000 risorse all&#39;ora. Il tasso si osserva con una dimensione media di 10 MB di risorse.

## Pubblicare risorse in Brand Portal {#publish-assets-to-bp}

Di seguito è descritta la procedura per pubblicare risorse su Brand Portal da AEM Assets:

1. Dalla console di Assets, apri la cartella principale e seleziona tutte le risorse da pubblicare, quindi fai clic su **[!UICONTROL Pubblicazione rapida]** nella barra degli strumenti.

   ![publish2bp-2](assets/publish2bp.png)

1. Di seguito sono descritte le due opzioni per la pubblicazione di risorse:
   * [Pubblica ora](#publish-to-bp-now) (pubblica subito le risorse)
   * [Pubblica più tardi](#publish-to-bp-later) (pianifica la pubblicazione delle risorse)

### Pubblicare subito le risorse {#publish-to-bp-now}

Per pubblicare le risorse selezionate su Brand Portal, effettua una delle seguenti operazioni:

* Dalla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**. Dal menu, fai clic su **[!UICONTROL Pubblica su Brand Portal]**.

* Dalla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**.

   1. In **[!UICONTROL Azione]**, seleziona **[!UICONTROL Pubblica su Brand Portal]**.

      In **[!UICONTROL Pianificazione]**, seleziona **[!UICONTROL Ora]**.

      Fai clic su **[!UICONTROL Avanti]**.

   2. Conferma la selezione in **[!UICONTROL Ambito]** e fai clic su **[!UICONTROL Pubblica su Brand Portal]**.

Viene visualizzato un messaggio per informare che le risorse sono state accodate per la pubblicazione su Brand Portal. Per visualizzare le risorse pubblicate, accedi all’interfaccia di Brand Portal.

### Pubblicare le risorse in un secondo momento {#publish-to-bp-later}

Per pianificare la pubblicazione delle risorse su Brand Portal in una data o un’ora successiva:

1. Seleziona le risorse di cui vuoi pianificare la pubblicazione e fai clic su **[!UICONTROL Gestisci pubblicazione]** nella barra degli strumenti in alto.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione]**, seleziona **[!UICONTROL Pubblica su Brand Portal]** in **[!UICONTROL Azione]**.

   Seleziona **[!UICONTROL Più tardi]** in **[!UICONTROL Pianificazione]**.

   <!--![publishlaterbp-1](assets/publishlaterbp-1.png)-->

   ![pubblica più tardi](assets/publish-later.png)

1. Seleziona un valore per **[!UICONTROL Data di attivazione]** e specifica l’ora. Fai clic su **[!UICONTROL Avanti]**.

1. Seleziona un valore per **Data di attivazione** e specifica l’ora. Fai clic su **Avanti**.

1. Specifica un valore per **[!UICONTROL Titolo flusso di lavoro]** in **[!UICONTROL Flussi di lavoro]**. Fai clic su **[!UICONTROL Pubblica più tardi]**.

   <!--![publishworkflow](assets/publishworkflow.png)-->

   ![flusso di lavoro di pubblicazione](assets/publish-workflow.png)

>[!NOTE]
>
> * La parte utenti esistenti del gruppo DAM-Users dispone dell’accesso in lettura al percorso &quot;/conf/global/settings/cloudconfigs/mediaportal&quot;
> * I nuovi utenti (o utenti non amministratori) richiedono i seguenti diritti per la pubblicazione su Brand Portal.
>   &#x200B;> Percorsi:
>   &#x200B;> `"/conf/global/settings/cloudconfigs/mediaportal" : jcr:read `
>   &#x200B;>`/libs : jcr:read`
>   &#x200B;>`/conf : jcr:read`
>   &#x200B;>`/content : jcr:read, crx:replicate`
>   &#x200B;>`/content/dam/ : jcr:read,modify, crx:replicate`

## Pubblicare cartelle in Brand Portal {#publish-folders-to-brand-portal}

Puoi pubblicare o annullare subito la pubblicazione delle cartelle di risorse oppure pianificare la pubblicazione in una data o un’ora successiva.

### Pubblicare cartelle in Brand Portal {#publish-folders-to-bp}

1. Dalla console di Assets, seleziona le cartelle da pubblicare e fai clic su **[!UICONTROL Pubblicazione rapida]** nella barra degli strumenti.

   ![publish2bp](assets/publish2bp.png)

1. **Pubblicare subito le cartelle**

   Per pubblicare le cartelle selezionate su Brand Portal, effettua una delle seguenti operazioni:

   * Dalla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**.

     Dal menu, seleziona **[!UICONTROL Pubblica su Brand Portal]**.

   * Dalla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**.

      1. In **[!UICONTROL Azione]**, seleziona **[!UICONTROL Pubblica su Brand Portal]**.

         In **[!UICONTROL Pianificazione]**, seleziona **[!UICONTROL Ora]**.

         Fai clic su **Avanti**.

      1. Conferma la selezione in **[!UICONTROL Ambito]** e fai clic su **[!UICONTROL Pubblica su Brand Portal]**.

   Viene visualizzato un messaggio per informare che la cartella è stata accodata per la pubblicazione su Brand Portal. Per visualizzare la cartella pubblicata, accedi all’interfaccia di Brand Portal.

1. **Pubblica cartelle più tardi**
Per pianificare la pubblicazione delle cartelle di risorse in una data o in un’ora successiva:

   1. Seleziona le cartelle di cui vuoi pianificare la pubblicazione e fai clic su **[!UICONTROL Gestisci pubblicazione]** nella barra degli strumenti in alto.
   1. In **[!UICONTROL Azione]**, seleziona **[!UICONTROL Pubblica su Brand Portal]**.

      In **[!UICONTROL Pianificazione]**, seleziona **[!UICONTROL Più tardi]**.

   1. Seleziona un valore per **[!UICONTROL Data di attivazione]** e specifica l’ora. Fai clic su **[!UICONTROL Avanti]**.

      <!--![publishlaterbp](assets/publishlaterbp.png)-->

   ![pubblica cartella più recente](assets/publish-later-folder.png)

   1. Conferma la selezione in **[!UICONTROL Ambito]**. Fai clic su **[!UICONTROL Avanti]**.

   1. Specifica un titolo del flusso di lavoro in **[!UICONTROL Flussi di lavoro]**. Fai clic su **[!UICONTROL Pubblica più tardi]**.

      <!--![manageschedulepub](assets/manageschedulepub.png)-->

   ![flusso di lavoro di pubblicazione](assets/publish-workflow.png)

### Visualizza file o cartella pubblicata in Brand Portal {#view-published-file-folder}

1. Accedi all’interfaccia di Brand Portal per visualizzare le risorse pubblicate (a seconda della data o dell’ora pianificata).

   ![bp_landingpage](assets/bp_landingpage.png)

1. Passa alla vista a elenco ![Vista a elenco](assets/list-view.svg) per visualizzare lo stato di pubblicazione corrente della risorsa.

<!--2. On the [Asset Reports page](#https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/admin/asset-reports), you can see the current state of the report job, for example, Success, Failed, Queued, or Scheduled.-->

![stato report generato](assets/report-status.JPG)

### Annullare la pubblicazione di cartelle da Brand Portal {#unpublish-folders-from-brand-portal}

Per rimuovere una cartella di risorse pubblicata su Brand Portal, annullane la pubblicazione dall’istanza di AEM Assets. Dopo l’annullamento della pubblicazione della cartella originale, la relativa copia non sarà più disponibile per gli utenti di Brand Portal.

Puoi annullare subito la pubblicazione delle cartelle di risorse su Brand Portal oppure pianificare l’operazione per una data e un’ora successive.

Per annullare la pubblicazione delle cartelle di risorse su Brand Portal:

1. Dalla console di Assets, seleziona le cartelle di risorse di cui vuoi annullare la pubblicazione e fai clic su **[!UICONTROL Gestisci pubblicazione]** nella barra degli strumenti.

   ![publish2bp-1](assets/publish2bp.png)

1. **Annullare subito la pubblicazione delle cartelle di risorse**

   Per annullare immediatamente la pubblicazione della cartella di risorse selezionata su Brand Portal:

   1. Dalla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**.

   1. In **[!UICONTROL Azione]**, seleziona **[!UICONTROL Annulla pubblicazione su Brand Portal]**.

      In **[!UICONTROL Pianificazione]**, seleziona **[!UICONTROL Ora]**.

      Fai clic su **[!UICONTROL Avanti]**.

   1. Conferma la selezione in **[!UICONTROL Ambito]** e fai clic su **[!UICONTROL Annulla pubblicazione su Brand Portal]**.

      ![confirm-unpublish](assets/confirm-unpublish.png)

1. **Annullare la pubblicazione delle cartelle di risorse in un secondo momento**

   Per pianificare l’annullamento della pubblicazione di una cartella di risorse in una data e un’ora successive:

   1. Dalla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**.

   1. In **[!UICONTROL Azione]**, seleziona **[!UICONTROL Annulla pubblicazione su Brand Portal]**.

      In **[!UICONTROL Pianificazione]**, seleziona **[!UICONTROL Più tardi]**.

   1. Seleziona un valore per **[!UICONTROL Data di attivazione]** e specifica l’ora. Fai clic su **[!UICONTROL Avanti]**.

   1. Conferma la selezione in **[!UICONTROL Ambito]** e fai clic su **[!UICONTROL Avanti]**.

   1. Specifica un valore per **[!UICONTROL Titolo flusso di lavoro]** in **[!UICONTROL Flussi di lavoro]**. Fai clic su **[!UICONTROL Annulla pubblicazione più tardi]**.

      ![unpublishworkflows](assets/unpublishworkflows.png)

## Pubblicare raccolte in Brand Portal {#publish-collections-to-brand-portal}

Puoi pubblicare o annullare la pubblicazione delle raccolte dall’istanza cloud di AEM Assets.

>[!NOTE]
>
>I frammenti di contenuto non possono essere pubblicati su Brand Portal. Pertanto, se selezioni frammenti di contenuto in AEM Assets, l’azione **[!UICONTROL Pubblica su Brand Portal]** non è disponibile.
>
>Se le raccolte contenenti frammenti di contenuto vengono pubblicate da AEM Assets su Brand Portal, nell’interfaccia di Brand Portal viene replicato tutto il contenuto della cartella, tranne i frammenti di contenuto.

### Pubblicare le raccolte {#publish-collections}

Di seguito è descritta la procedura per pubblicare raccolte su Brand Portal da AEM Assets:

1. Nell’interfaccia utente di AEM Assets, fai clic sul logo AEM.

1. Dalla pagina **Navigazione**, passa a **[!UICONTROL Risorse]** > **[!UICONTROL Raccolte]**.

1. Dalla console **Raccolte**, seleziona le raccolte che vuoi pubblicare su Brand Portal.

   ![select_collection](assets/select_collection.png)

1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Pubblica su Brand Portal]**.

1. Nella finestra di dialogo di conferma, fai clic su **[!UICONTROL Pubblica]**.

1. Chiudi il messaggio di conferma.

   Accedi a Brand Portal come amministratore. La raccolta pubblicata è disponibile nella console Raccolte.

   ![raccolta pubblicata](assets/published_collection.png)

### Annullare la pubblicazione delle raccolte {#unpublish-collections}

Per rimuovere una raccolta pubblicata su Brand Portal, annullane la pubblicazione dall’istanza di AEM Assets. Dopo l’annullamento della pubblicazione della raccolta originale, la relativa copia non sarà più disponibile per gli utenti di Brand Portal.

Di seguito è descritta la procedura per annullare la pubblicazione di una raccolta:

1. Dalla console **Raccolte** dell’istanza di AEM Assets, seleziona la raccolta di cui vuoi annullare la pubblicazione.

   ![select_collection](assets/select_collection-1.png)

1. Dalla barra degli strumenti, fai clic sull’icona **[!UICONTROL Rimuovi da Brand Portal]**.
1. Nella finestra di dialogo, fai clic su **[!UICONTROL Annulla pubblicazione]**.
1. Chiudi il messaggio di conferma. La raccolta viene rimossa dall’interfaccia di Brand Portal.

Oltre a quanto sopra, è possibile pubblicare anche schemi di metadati, predefiniti per immagini, facet di ricerca e tag da AEM Assets a Brand Portal.

* [Pubblicare predefiniti, schemi e facet in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=it)
* [Pubblicare tag in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=it)


Per ulteriori informazioni, consulta la [documentazione di Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=it).


<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

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