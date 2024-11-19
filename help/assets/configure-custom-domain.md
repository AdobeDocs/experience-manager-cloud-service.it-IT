---
title: Configurare un dominio personalizzato per il livello Publish
description: Scopri come configurare un dominio personalizzato per il livello di pubblicazione in Adobe Cloud Manager.
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 11%

---

# Configurare un dominio personalizzato per il livello di pubblicazione{#configure-custom-domain}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>La guida alle funzionalità di Dynamic Media con OpenAPI è ora disponibile in formato PDF. Scarica l’intera guida e utilizza Adobe Acrobat AI Assistant per rispondere alle tue domande.
>
>[!BADGE Guida di Dynamic Media con funzionalità OpenAPI PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

In Adobe Cloud Manager, puoi dare risalto al tuo sito web aggiungendo un dominio personalizzato. Se AEM as a Cloud Service viene fornito con un dominio predefinito, puoi personalizzarlo in base alle tue esigenze.

## Prima di iniziare

* È necessario disporre di un certificato TLS o SSL multi-SAN (Subject Alternative Name).
* Il certificato SSL deve avere SAN distinte rispetto al certificato mappato per il livello di pubblicazione all’interno dello stesso dominio.
* I criteri di certificato devono essere conformi ai criteri di convalida estesa (EV) o di convalida organizzazione (OV) e non ai criteri di convalida del dominio (DV).


## Configurare un dominio personalizzato per il livello di pubblicazione

1. Adobe Vai a **[!UICONTROL Cloud Manager]** > **[!UICONTROL Panoramica del programma]** > **[!UICONTROL Certificati SSL]** e aggiungi il tuo certificato SSL.
   ![immagine](/help/assets/assets/ssl-certificate.png)
Scopri come aggiungere il [certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) in Adobe Cloud Manager.

1. Dopo aver aggiunto il certificato SSL, aggiungi un dominio personalizzato. Fai clic su **[!UICONTROL Impostazioni dominio]** e specifica il dominio personalizzato in base all&#39;opzione **[!UICONTROL Servizio Publish]**.
Ulteriori informazioni sul [dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Aggiungi due [record CNAME](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) nel record DNS corrispondenti ai domini di pubblicazione.
L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS.

1. Segnala un caso di supporto per facilitare la configurazione del dominio personalizzato, garantendo che venga indirizzato al livello di consegna.

>[!NOTE]
>
Aggiungi il dominio personalizzato all’elenco degli URL di reindirizzamento consentiti. L’elenco si trova nel client IMS per il selettore risorse.<br>Coordinati con il rispettivo team di Adobe per eseguire questa attività fornendo la stringa di dominio personalizzata.
