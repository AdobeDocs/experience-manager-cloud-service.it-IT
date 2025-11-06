---
title: Rileva risorse duplicate per  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Scopri come rilevare le risorse duplicate
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management, Publishing,Collaboration, Asset Processing
role: User, Developer, Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 9%

---


# Rilevare risorse duplicate {#detect-duplicate-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=en) |
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
