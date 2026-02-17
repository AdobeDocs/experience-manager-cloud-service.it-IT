---
title: Impostazione di Dynamic Media
description: Per configurare Dynamic Media, devi configurare Dynamic Media e gestire i predefiniti per immagini e visualizzatori.
mini-toc-levels: 3
contentOwner: Rick Brough
feature: Configuration,Viewer Presets,Image Presets,Dynamic Media
role: Admin,User
exl-id: 83b70b17-7ee3-41cb-be90-c92ca161660e
source-git-commit: bd43f86c9d3ad017a5e963800938e3ead98b7441
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 4%

---

# Impostazione di Dynamic Media {#setting-up-dynamic-media}

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


## Aggiornamento DNS una tantum necessario per i rinnovi dei certificati Dynamic Media {#dns-update-dynamic-media-certificate-renewals}

Se il dominio utilizza un record DNS CAA (Certification Authority Authorization), è necessario autorizzare DigiCert a consentire il rinnovo continuo dei certificati TLS/SSL utilizzati dai nomi host Dynamic Media.

Aggiungi il seguente record CAA alla radice (apex) del dominio:

```
<yourdomain> CAA 0 issue "digicert.com"
```

Questo è un cambiamento unico.

È possibile verificare se esiste un record CAA utilizzando gli strumenti del provider DNS o un&#39;utilità di ricerca [CAA](https://caatest.co.uk/).

Se esiste un record CAA e DigiCert non è autorizzato, il rinnovo del certificato non riesce alla scadenza del certificato corrente, causando tempi di inattività per la consegna di immagini e video. Se non esiste alcun record CAA per il dominio, non è richiesta alcuna azione.
