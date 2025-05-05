---
title: Rileva risorse duplicate per  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Scopri come rilevare le risorse duplicate
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management, Publishing,Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 14%

---


# Rilevare risorse duplicate {#detect-duplicate-assets}

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

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Se un utente DAM carica una o più risorse già esistenti nell&#39;archivio, [!DNL Experience Manager] rileva la duplicazione e invia una notifica all&#39;utente. Il rilevamento duplicati è disabilitato per impostazione predefinita in quanto può avere un impatto sulle prestazioni a seconda delle dimensioni dell’archivio e del numero di risorse caricate.

Per attivare la funzione:

1. Passa a **[!UICONTROL Strumenti > Assets > Configurazioni Assets]**.

1. Fare clic su **[!UICONTROL Rilevamento duplicazione risorse]**.

1. Nella pagina [!UICONTROL Rilevamento duplicazione risorse] fare clic su **[!UICONTROL Abilitato]**.

   Il valore `dam:sha1` per il campo Rileva metadati assicura che vengano rilevate risorse duplicate anche se i nomi dei file sono diversi.

1. Fai clic su **[!UICONTROL Salva]**.

   ![Rilevamento duplicazione risorse](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Se il rilevatore di duplicazione è stato configurato utilizzando il file di configurazione `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` (configurazione OSGi), è possibile continuare a utilizzarlo. Tuttavia, Adobe consiglia di utilizzare il nuovo metodo.


Una volta abilitata, Experience Manager invia le notifiche delle risorse duplicate alla casella in entrata di Experience Manager. È un risultato aggregato per più duplicati. Gli utenti possono scegliere di rimuovere le risorse in base ai risultati.

![Notifica casella in entrata per risorse duplicate](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Quando carichi le risorse nell’archivio, Experience Manager rileva la duplicazione e notifica le prime 100 risorse duplicate.
