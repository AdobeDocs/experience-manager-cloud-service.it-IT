---
title: Rielaborazione di risorse digitali
description: Scopri i vari metodi di rielaborazione delle risorse digitali
role: User, Leader, Developer
exl-id: 19ca5278-929e-438b-9436-928f6c9f87d5
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 3%

---

# Rielaborazione di risorse digitali {#reprocessing-digital-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

È possibile rielaborare le risorse in una cartella che dispone già di un profilo di metadati esistente che è stato successivamente modificato. Se desiderate che il predefinito appena modificato venga riapplicato alle risorse esistenti nella cartella, dovete rielaborare la cartella. Puoi rielaborare tutte le risorse necessarie.

Rielabora le risorse in una cartella se si verifica uno dei due scenari seguenti:

* Desideri eseguire un predefinito per set di batch in una cartella di risorse esistente in cui sono già caricate risorse.
* In seguito puoi modificare un predefinito per set di batch esistente precedentemente applicato a una cartella di risorse.

## Rielabora risorse {#reprocessing-steps}

Per rielaborare le risorse in una cartella:

1. In [!DNL Assets view], dalla pagina Assets, seleziona le risorse appena aggiunte o quelle che desideri rielaborare.
Se selezioni una cartella:

   * Il flusso di lavoro considera tutti i file nella cartella selezionata in modo ricorsivo.
   * Se nella cartella principale selezionata sono presenti una o più sottocartelle con risorse, il flusso di lavoro rielabora ogni risorsa nella gerarchia delle cartelle.
   * Come best practice, evita di eseguire questo flusso di lavoro su una gerarchia di cartelle con più di 1000 risorse.

1. Selezionare **[!UICONTROL Rielabora Assets]**. Scegli tra le due opzioni:

   ![Rielaborazione delle opzioni di Assets](assets/reprocessing-options.png)

   * **[!UICONTROL Processo completo]:** Selezionare questa opzione quando si desidera eseguire il processo complessivo, inclusi il profilo predefinito, il profilo personalizzato, l&#39;elaborazione dinamica (se configurata) e i flussi di lavoro di post-elaborazione.
   * **[!UICONTROL Avanzate]:** Seleziona questa opzione per scegliere la rielaborazione avanzata.

     ![Opzioni avanzate di rielaborazione di Assets](assets/reprocessing-options-advanced.png)

     Seleziona tra le seguenti opzioni avanzate:

      * **[!UICONTROL Rappresentazioni anteprima predefinite]:** Scegliere questa opzione per rielaborare le rappresentazioni visualizzate in anteprima per impostazione predefinita.

      * **[!UICONTROL Metadati]:** Scegliere questa opzione per estrarre le informazioni sui metadati e i tag avanzati per le risorse selezionate.

      * **[!UICONTROL Elaborazione dei profili]:** Scegliere questa opzione quando si desidera rielaborare un profilo selezionato. È possibile scegliere l&#39;opzione **[!UICONTROL Processo completo]** per includere l&#39;elaborazione predefinita e il profilo personalizzato assegnato a livello di cartella.
        <!--When assets are uploaded to a folder, [!DNL Assets ~~view~~] checks the containing folder's properties for a processing profile. If none is applied, a parent folder in the hierarchy is checked for a processing profile to apply.-->

      * **[!UICONTROL Flusso di lavoro di post-elaborazione]:** Scegliere questa opzione se è necessaria un&#39;ulteriore elaborazione delle risorse che non può essere ottenuta utilizzando i profili di elaborazione. È possibile aggiungere alla configurazione ulteriori flussi di lavoro di post-elaborazione. La post-elaborazione consente di aggiungere un’elaborazione completamente personalizzata oltre a quella configurabile utilizzando i microservizi per le risorse.

Consulta [utilizzare i microservizi delle risorse e i profili di elaborazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en) per ulteriori informazioni sui profili di elaborazione e sul flusso di lavoro di post-elaborazione.

![Opzioni avanzate di rielaborazione Assets2](assets/reprocessing-options-advanced-2.png)

Dopo aver selezionato le opzioni appropriate, fare clic su **[!UICONTROL Rielabora]**. Viene visualizzato il messaggio di operazione riuscita.

## Scenari per la rielaborazione delle risorse digitali {#scenarios-reprocessing}

[!DNL Experience Manager] consente la rielaborazione delle risorse digitali per i seguenti componenti.

### Tag avanzati {#reprocessing-smart-tags}

Le organizzazioni che si occupano di risorse digitali utilizzano sempre più spesso il vocabolario controllato dalla tassonomia nei metadati delle risorse. In sostanza, include un elenco di parole chiave utilizzate comunemente da dipendenti, partner e clienti per fare riferimento e cercare risorse digitali di una particolare classe. L’assegnazione dei tag alle risorse tramite un vocabolario controllato dalla tassonomia consente di identificarle e recuperarle facilmente.

Rispetto ai vocabolari del linguaggio naturale, assegnare tag alle risorse digitali in base alla tassonomia aziendale consente di allinearle alle attività aziendali e assicura che le risorse più rilevanti vengano visualizzate nelle ricerche.

Ulteriori informazioni su [Tag avanzati per risorse video](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags-video-assets.html?lang=en).

Ulteriori informazioni su [Rielabora tag colore per immagini esistenti in DAM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en#color-tags-existing-images).

### Ritaglio avanzato {#reprocessing-smart-crop}

Ulteriori informazioni su [Ritaglio avanzato Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=en) che consente di applicare alle risorse caricate specifiche configurazioni di ritaglio (**[!UICONTROL Ritaglio avanzato]** e ritaglio pixel) e nitidezza.

### Metadati {#reprocessing-metadata}

[!DNL Adobe Experience Manager Assets] mantiene i metadati per ogni risorsa. Consente di categorizzare e organizzare più facilmente le risorse e aiuta le persone alla ricerca di una risorsa specifica. Grazie alla possibilità di estrarre i metadati dai file caricati in Experience Manager Assets, la gestione dei metadati si integra con il flusso di lavoro creativo. Grazie alla possibilità di conservare e gestire i metadati con le risorse, è possibile organizzare ed elaborare automaticamente le risorse in base ai relativi metadati.

Ulteriori informazioni su [Rielaborazione dei profili di metadati](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en).

### Rielaborare le risorse Dynamic Media in una cartella {#reprocessing-dynamic-media}

È possibile rielaborare le risorse in una cartella che dispone già di un profilo immagine Dynamic Media esistente o di un profilo video Dynamic Media modificato successivamente. Per ulteriori informazioni, visita [rielabora risorse Dynamic Media in una cartella](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/about-image-video-profiles.html?lang=en).

>[!NOTE]
>
>È necessario configurare [!DNL Dynamic Media] nell&#39;ambiente per abilitare la finestra di dialogo Dynamic Media.
>

### Flussi di lavoro

Ulteriori informazioni su [profili di elaborazione e flussi di lavoro di post-elaborazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en).
