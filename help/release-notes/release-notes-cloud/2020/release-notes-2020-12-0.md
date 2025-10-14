---
title: Note sulla versione 2020.12.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2020.12.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
feature: Release Information
role: Admin
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 9%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 è il 17 dicembre 2020.
La seguente versione (2021.1.0) è del 28 gennaio 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP per frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md)**: è stata aggiunta la possibilità di aggiungere/aggiornare ed eliminare varianti di frammenti di contenuto mediante API HTTP.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* L&#39;integrazione con [!DNL Adobe InDesign Server] è ora disponibile per [!DNL Experience Manager] come [!DNL Cloud Service]. Consente di automatizzare l&#39;elaborazione di [!DNL Adobe InDesign] file tramite script [!DNL Adobe InDesign Server] e di utilizzare l&#39;interfaccia utente di [!DNL Assets] modelli per creare brochure o annunci. Solo [!DNL InDesign Server] ospitato da [!DNL Adobe Managed Services] è supportato per [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] è stato migliorato per tenere traccia e visualizzare i riferimenti alle risorse quando una risorsa viene utilizzata in una distribuzione remota di [!DNL Experience Manager Sites] tramite la funzionalità Connected Assets. Una nuova scheda [!UICONTROL Riferimenti] nella pagina [!UICONTROL Proprietà] della risorsa elenca ora i riferimenti locali e remoti della risorsa. I riferimenti consentono agli utenti DAM di monitorare l&#39;utilizzo delle risorse nelle pagine [!DNL Sites] e nelle risorse composte in [!DNL Assets]. Vedere [configurare e utilizzare Connected Assets](/help/assets/use-assets-across-connected-assets-instances.md).

* Le funzionalità di [!DNL Dynamic Media] sono ora accessibili tramite i componenti core basati su immagini AEM [!DNL Sites]. Gli autori possono configurare rapidamente i componenti per utilizzare Predefiniti immagine, Ritaglio avanzato e Modificatori immagine durante la creazione di pagine Web. Consulta [Componenti core versione 2.13.0](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* L&#39;app desktop [!DNL Experience Manager] consente agli utenti di caricare file e cartelle trascinando i file da Esplora risorse o da Mac Finder nell&#39;interfaccia dell&#39;app desktop. Consulta [aggiungere risorse tramite l&#39;app desktop](https://experienceleague.adobe.com/it/docs/experience-manager-desktop-app/using/using#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È stato rilasciato il sito di riferimento CIF Venia (2020.12.01), che include la versione più recente dei Componenti core CIF v1.6.0. Per ulteriori dettagli, consulta [Sito di riferimento per CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01).

* È stata rilasciata la versione 1.6.0 dei Componenti core CIF. Per ulteriori dettagli, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0).

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di pubblicazione di Cloud Manager in Adobe Experience Manager (AEM) as a Cloud Service 2020.12.0 è il 10 dicembre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* Gestione self-service di [certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) e [introduzione ai nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Gestione in autonomia di [elenchi IP consentiti &#x200B;](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* La pagina dei dettagli **Ambiente** aggiornata ora consente agli utenti di gestire i nomi di dominio personalizzati e gli Elenchi consentiti IP nei loro ambienti.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Vengono risolte alcune occorrenze di errori nella fase di scansione del codice senza fornire risultati.

* La scheda ambiente non mostrava in modo coerente il pulsante **Aggiungi**.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità in [!DNL Code Refactoring Tools] {#what-is-new-crt}

* È stata rilasciata la nuova versione del plug-in AIO-CLI. La versione più recente di questo plug-in include correzioni di bug per AEM Dispatcher Converter e Repository Modernizer e supporta anche una nuova utility: Index Converter. Consulta [Esperienza unificata](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience#benefits) per ulteriori informazioni su questo plug-in.

* Index Converter è un’utility che può essere utilizzata per trasformare le definizioni dell’indice Oak personalizzato di un cliente in definizioni dell’indice Oak compatibili con AEM as a Cloud Service. Per ulteriori dettagli, vedere [Index Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter).

* È stata aggiunta una nuova funzionalità a [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) che crea un pacchetto separato `ui.config` contenente tutte le configurazioni OSGi.

### Correzioni di bug {#crt-bug-fixes}

* Sono state apportate diverse correzioni di bug agli strumenti AEM Dispatcher Converter e Repository Modernizer. Vedere [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.1.20 è il 8 gennaio 2021.

### Novità in [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Ora gli utenti possono sapere se il loro token di accesso è scaduto passando il puntatore sull&#39;icona di stato nell&#39;interfaccia utente dello strumento Content Transfer (CTT). Nell’interfaccia utente Dettagli set di migrazione viene inoltre notificato che non è possibile connettersi alla propria istanza di Cloud Service.

### Correzioni di bug {#ctt-bug-fixes}

* Lo stato dell’interfaccia utente dello strumento Content Transfer (CTT) per un set di migrazione non persiste e viene modificato dopo un periodo di inattività. Questo problema è ora risolto.
* L’opzione per visualizzare i registri era disabilitata se i registri non erano disponibili. Questo problema è ora risolto e sono stati aggiunti messaggi per informare gli utenti del motivo per cui mancano i registri.
* Lo stato dell&#39;interfaccia utente dello strumento Content Transfer mostrava *FAILED* quando l&#39;utente interrompeva un&#39;acquisizione. Il problema è ora risolto per visualizzare *STOPPED*.
