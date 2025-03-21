---
title: Generazione di rapporti in Dynamic Media
description: Scopri come richiedere un rapporto di errore per gli URL di consegna di Dynamic Media che hanno esito negativo.
contentOwner: Rick Brough
feature: Asset Management
role: User
hide: true
hidefromtoc: true
exl-id: 2488f813-df15-4dbb-8747-f827ee5925e1
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 6%

---

# Richiedi un report di errori per gli URL di consegna Dynamic Media che non superano il test

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

Puoi richiedere una segnalazione errori che identifichi gli URL di Dynamic Media non riusciti al momento della consegna. Il rapporto è un’aggregazione di dati fino a cinque giorni ed è disponibile in formato CSV. La segnalazione errori include le informazioni seguenti:

* URL di consegna Dynamic Media non riuscito: un URL non riuscito è un URL generato da Dynamic Media che non è in grado di produrre alcun contenuto al momento della consegna.
* URL referente: l’URL referente da cui viene chiamato l’URL di consegna non riuscito.
* Conteggio degli errori: il numero di volte in cui è stato caricato l’URL di consegna che ha provocato un errore.

Quando richiedi il rapporto di errore, il team di Adobe Dynamic Media ti invia il rapporto tramite e-mail in formato CSV. Esso copre un periodo di cinque giorni a decorrere dal giorno in cui è stata presentata la richiesta.

Puoi richiedere una segnalazione di errori una volta al mese, per una determinata azienda.

**Per richiedere un report di errori per gli URL di consegna di Dynamic Media non riusciti:**

1. [Invia un&#39;e-mail a reports-dynamic-media@adobe.com](mailto:reports-dynamic-media@adobe.com) con il nome della società associato al tuo account Dynamic Media.

   Se non conosci il nome della società, consulta la pagina [Configurazione elemento multimediale dinamico](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html?lang=it#configuring-dynamic-media-cloud-services) in **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Configurazione elemento multimediale dinamico]**. Nella pagina del Browser configurazioni Dynamic Media, fai clic su **[!UICONTROL global]**, seleziona la casella di controllo *[Dynamic_Media_folder_icon]*, quindi seleziona **[!UICONTROL Modifica]**. Per accedere alla pagina Configurazione di Dynamic Media è necessario disporre dei diritti di amministratore in AEM.

   ![Accesso alla pagina di configurazione di Dynamic Media.](/help/assets/dynamic-media/assets/reporting-accessdmconfig.png)
