---
title: Note sulla versione 2020.12.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2020.12.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 11%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] La versione 2020.12.0 di as a Cloud Service è il 17 dicembre 2020.
La seguente versione (2021.1.0) è del 28 gennaio 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP per frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md)**: aggiungi la possibilità di aggiungere/aggiornare ed eliminare varianti di frammenti di contenuto utilizzando l’API HTTP.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* Integrazione con [!DNL Adobe InDesign Server] è ora disponibile per [!DNL Experience Manager] as a [!DNL Cloud Service]. Automatizza l&#39;elaborazione [!DNL Adobe InDesign] file che utilizzano [!DNL Adobe InDesign Server] scripting e consente agli utenti di utilizzare [!DNL Assets] modelli di interfaccia utente per creare brochure o annunci. Solo [!DNL InDesign Server] in hosting da [!DNL Adobe Managed Services] è supportato per [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] è stato migliorato per tenere traccia e visualizzare i riferimenti alle risorse quando una risorsa viene utilizzata in un [!DNL Experience Manager Sites] tramite la funzionalità Risorse collegate. Una nuova [!UICONTROL Riferimenti] nella scheda della risorsa [!UICONTROL Proprietà] Questa pagina elenca ora i riferimenti locali e remoti della risorsa. I riferimenti consentono agli utenti DAM di monitorare l’utilizzo delle risorse in [!DNL Sites] pagine e risorse composte in [!DNL Assets]. Consulta [configurare e utilizzare le risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] sono ora accessibili tramite AEM [!DNL Sites] Componenti core basati su immagini. Gli autori possono configurare rapidamente i componenti per utilizzare Predefiniti immagine, Ritaglio avanzato e Modificatori immagine durante la creazione di pagine Web. Consulta [Componenti core versione 2.13.0](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* Il [!DNL Experience Manager] L&#39;app desktop consente agli utenti di caricare file e cartelle trascinandoli da Esplora risorse o da Mac Finder nell&#39;interfaccia dell&#39;app desktop. Consulta [aggiungere risorse tramite l’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È stato rilasciato il sito di riferimento CIF Venia (2020.12.01), che include la versione più recente dei Componenti core CIF v1.6.0. Consulta [Sito di riferimento CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) per ulteriori dettagli.

* È stata rilasciata la versione 1.6.0 dei Componenti core CIF. Consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) per ulteriori dettagli.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di pubblicazione di Cloud Manager in Adobe Experience Manager (AEM) as a Cloud Service 2020.12.0 è il 10 dicembre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* Gestione in autonomia di [certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e dei [nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Gestione in autonomia di [elenchi IP consentiti ](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* Il valore aggiornato **Ambiente** La pagina dei dettagli ora consente agli utenti di gestire i nomi di dominio personalizzati e gli Elenchi consentiti IP nei loro ambienti.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Vengono risolte alcune occorrenze di errori nella fase di scansione del codice senza fornire risultati.

* La scheda ambiente non mostrava in modo coerente **Aggiungi** pulsante.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità in [!DNL Code Refactoring Tools] {#what-is-new-crt}

* È stata rilasciata la nuova versione del plug-in AIO-CLI. La versione più recente di questo plug-in include correzioni di bug per AEM Dispatcher Converter e Repository Modernizer e supporta anche una nuova utility: Index Converter. Consulta [Esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html#benefits) dove è possibile saperne di più su questo plug-in.

* Index Converter è un’utility che può essere utilizzata per trasformare le definizioni dell’indice Oak personalizzato di un cliente in definizioni dell’indice Oak compatibili con l’AEM as a Cloud Service. Consulta [Convertitore indice](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) per ulteriori dettagli.

* Nuova funzione aggiunta a [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) che crea un pacchetto separato `ui.config` per contenere tutte le configurazioni OSGi.

### Correzioni di bug {#crt-bug-fixes}

* Sono state apportate diverse correzioni di bug agli strumenti AEM Dispatcher Converter e Repository Modernizer. Consulta [Convertitore del Dispatcher per l’AEM](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Data di rilascio {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.1.20 è il 8 gennaio 2021.

### Novità in [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Ora gli utenti possono sapere se il loro token di accesso è scaduto passando il puntatore sull&#39;icona di stato nell&#39;interfaccia utente dello strumento Content Transfer (CTT). Nell’interfaccia utente Dettagli set di migrazione viene inoltre notificato che non è possibile connettersi alla propria istanza di Cloud Service.

### Correzioni di bug {#ctt-bug-fixes}

* Lo stato dell’interfaccia utente dello strumento Content Transfer (CTT) per un set di migrazione non persiste e viene modificato dopo un periodo di inattività. Questo problema è stato risolto.
* L’opzione per visualizzare i registri era disabilitata se i registri non erano disponibili. Questo problema è stato risolto ed è stato aggiunto un messaggio per informare gli utenti del motivo della mancanza dei registri.
* Stato dell&#39;interfaccia utente dello strumento Content Transfer (Trasferimento contenuti) visualizzato *NON RIUSCITO* quando l’utente ha interrotto un’acquisizione. Questo problema è stato risolto per la visualizzazione *INTERROTTO* invece.
