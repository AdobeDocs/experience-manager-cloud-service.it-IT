---
title: Note sulla versione 2020.12.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2020.12.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 11%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service.

## Data di pubblicazione {#release-date}

Data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 è il 17 dicembre 2020.
La versione seguente (2021.1.0) sarà il 28 gennaio 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP per frammento di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md)**: Aggiungi la possibilità di aggiungere/aggiornare ed eliminare varianti di frammenti di contenuto utilizzando l’API HTTP.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* Integrazione con [!DNL Adobe InDesign Server] è ora disponibile per [!DNL Experience Manager] come [!DNL Cloud Service]. Fornisce automazione per il processo [!DNL Adobe InDesign] file che utilizzano [!DNL Adobe InDesign Server] e consente agli utenti di utilizzare [!DNL Assets] crea l’interfaccia utente dei modelli per la creazione di brochure o annunci. Solo [!DNL InDesign Server] ospitato da [!DNL Adobe Managed Services] è supportato per [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] viene migliorato per tenere traccia e visualizzare i riferimenti alle risorse quando una risorsa viene utilizzata in un [!DNL Experience Manager Sites] distribuzione tramite la funzionalità Risorse collegate. Nuovo [!UICONTROL Riferimenti] scheda della risorsa [!UICONTROL Proprietà] In questa pagina sono ora elencati i riferimenti locali e remoti della risorsa. I riferimenti consentono agli utenti DAM di tenere traccia dell’utilizzo delle risorse in [!DNL Sites] pagine e risorse composte in [!DNL Assets]. Vedi [configurare e utilizzare Risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] Le funzionalità sono ora accessibili tramite [!DNL Sites] Componenti core basati su immagini. Gli autori possono configurare rapidamente i componenti per utilizzare i predefiniti immagine, ritaglio avanzato e modificatori immagine durante la creazione di pagine web. Vedi [Componenti core versione 2.13.0](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] l’app desktop consente agli utenti di caricare file e cartelle trascinandoli da Esplora risorse o dal Finder di Mac sull’interfaccia dell’app desktop. Vedi [aggiungere risorse utilizzando l’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Sito di riferimento CIF Venia rilasciato: 2020.12.01 che include la versione più recente dei componenti core CIF versione v1.6.0. Fai riferimento a [Sito di riferimento CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) per ulteriori dettagli.

* È stata rilasciata la versione 1.6.0 dei componenti core CIF. Fai riferimento a [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) per ulteriori dettagli.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.12.0 è il 10 dicembre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* Gestione autonoma [Certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e [Nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Gestione autonoma [ELENCHI CONSENTITI IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* Aggiornato **Ambiente** la pagina dei dettagli ora consente agli utenti di gestire i nomi di dominio personalizzati e gli Elenchi consentiti IP nei loro ambienti.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Alcune occorrenze di errori nella fase di scansione del codice senza fornire i risultati risolti.

* La scheda ambiente non viene visualizzata in modo coerente **Aggiungi** pulsante .

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità in [!DNL Code Refactoring Tools] {#what-is-new-crt}

* È stata rilasciata la nuova versione del plug-in AIO-CLI. La versione più recente di questo plug-in include correzioni di bug per AEM Dispatcher Converter e Repository Modernizer e supporta anche una nuova utility - Index Converter. Fai riferimento a [Esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) per ulteriori informazioni su questo plug-in.

* Index Converter è un&#39;utilità che può essere utilizzata per trasformare le definizioni di indice OAK personalizzato di un cliente in definizioni di indice OAK compatibile AEM as a Cloud Service. Fai riferimento a [Convertitore indice](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) per ulteriori dettagli.

* Nuova funzione aggiunta a [Modernizzatore dell&#39;archivio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) che crea un pacchetto separato `ui.config` per contenere tutte le configurazioni OSGi.

### Correzioni di bug {#crt-bug-fixes}

* Diverse correzioni di bug eseguite sugli strumenti AEM Dispatcher Converter e Repository Modernizer . Fai riferimento a [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Modernizzatore dell&#39;archivio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Data di pubblicazione {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.1.20 è il 8 gennaio 2021.

### Novità in [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Gli utenti possono ora sapere se il token di accesso è scaduto passando il cursore sull’icona di stato nell’interfaccia utente dello strumento Content Transfer (Content Transfer Tool). Inoltre, nell’interfaccia utente dei Dettagli set di migrazione verrà notificato che non è possibile connettersi all’istanza del Cloud Service.

### Correzioni di bug {#ctt-bug-fixes}

* Lo stato dell’interfaccia utente dello strumento Content Transfer (CTT) per un set di migrazione non persisteva e veniva modificato dopo un periodo di inattività. Questo problema è stato risolto.
* Se i registri non erano disponibili, l’opzione per visualizzare i registri era disabilitata. Questo problema è stato risolto ed è stato aggiunto un messaggio per informare l’utente del motivo per cui i registri sono mancanti.
* Lo stato dell’interfaccia utente dello strumento Content Transfer (Trasferimento contenuti) mostrava *NON RIUSCITO* quando l’utente ha interrotto un’acquisizione. È stato corretto per la visualizzazione *ARRESTATO* invece.
