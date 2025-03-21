---
title: Impostazione di Dynamic Media
description: Per configurare Dynamic Media, devi configurare Dynamic Media e gestire i predefiniti per immagini e visualizzatori.
contentOwner: Rick Brough
feature: Configuration,Viewer Presets,Image Presets,Dynamic Media
role: Admin,User
exl-id: 83b70b17-7ee3-41cb-be90-c92ca161660e
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 14%

---

# Impostazione di Dynamic Media {#setting-up-dynamic-media}

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

{{work-with-dynamic-media}}

[Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) consente di gestire le risorse distribuendo risorse di marketing e merchandising visivo su richiesta, scalabili automaticamente per l&#39;utilizzo su siti Web, mobili e social. Grazie a un insieme di risorse di origine primarie, Dynamic Media genera e distribuisce in tempo reale più varianti di rich content attraverso una rete globale, scalabile e ottimizzata per le prestazioni.

<!-- OBSOLETE UNTIL THE INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE

>[!NOTE]
>
>This documentation describes Dynamic Media capabilites, which are integrated directly into [!DNL Experience Manager]. If you are using Dynamic Media Classic (previously called Scene7) integrated into [!DNL Experience Manager], see [Dynamic Media Classic integration documentation](/help/sites-cloud/administering/integrating-scene7.md).
>
>See [Dual Use Scenario](/help/sites-cloud/administering/integrating-scene7.md#dual-use-scenario) for times when you may want to use [!DNL Experience Manager] integrated with Dynamic Media Classic along with Dynamic Media.

-->

Per l’amministrazione di Dynamic Media, sono interessanti i seguenti argomenti:

* [Configurare Dynamic Media](config-dm.md)
* [Gestione predefiniti immagine](managing-image-presets.md)
* [Gestisci predefiniti visualizzatore](managing-viewer-presets.md)
* [Risoluzione dei problemi di Dynamic Media](troubleshoot-dm.md)

Consulta anche i seguenti argomenti:

* [Codifica video e profili video](video-profiles.md)
* [Profili immagine](image-profiles.md)

>[!NOTE]
>
>**Se si sta aggiornando:**
>
>* Dopo aver avviato Adobe [!DNL Experience Manager], tutte le risorse caricate verranno abilitate automaticamente (a meno che non siano state esplicitamente disabilitate dall&#39;amministratore di sistema). Se ti trovi in un&#39;istanza aggiornata di [!DNL Experience Manager] e non usi Dynamic Media, probabilmente dovrai rielaborare le risorse per renderle abilitate per Dynamic Media. Vedi [Rielabora risorse in una cartella](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).
