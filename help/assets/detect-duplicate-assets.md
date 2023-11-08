---
title: Consente di gestire i contenuti digitali
description: Scopri come rilevare le risorse duplicate
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
source-git-commit: bd0981b262f645653723f1b35d871808506d47ba
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---


# Rilevare risorse duplicate {#detect-duplicate-assets}

Se un utente DAM carica una o più risorse già esistenti nell’archivio, [!DNL Experience Manager] rileva la duplicazione e avvisa l’utente. Il rilevamento duplicati è disabilitato per impostazione predefinita in quanto può avere un impatto sulle prestazioni a seconda delle dimensioni dell’archivio e del numero di risorse caricate.

Per attivare la funzione:

1. Accedi a **[!UICONTROL Strumenti > Risorse > Configurazioni risorse]**.

1. Clic **[!UICONTROL Rilevamento duplicazione risorse]**.

1. Il giorno [!UICONTROL Pagina Rilevamento duplicazione risorse], fai clic su **[!UICONTROL Abilitato]**.

   `dam:sha1` Il valore del campo Rileva metadati garantisce che vengano rilevate risorse duplicate anche se i nomi dei file sono diversi.

1. Fai clic su **[!UICONTROL Salva]**.

   ![Rilevamento duplicazione risorse](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Se hai configurato il rilevatore di duplicazione utilizzando `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` file di configurazione di (configurazione OSGi), puoi continuare a utilizzarlo, tuttavia, l’Adobe consiglia di utilizzare il nuovo metodo.


Una volta abilitata, Experience Manager invia le notifiche delle risorse duplicate alla casella in entrata di Experience Manager. È un risultato aggregato per più duplicati. Gli utenti possono scegliere di rimuovere le risorse in base ai risultati.

![Notifica nella casella in entrata per le risorse duplicate](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Quando carichi le risorse nell’archivio, Experience Manager rileva la duplicazione e notifica le prime 100 risorse duplicate.

