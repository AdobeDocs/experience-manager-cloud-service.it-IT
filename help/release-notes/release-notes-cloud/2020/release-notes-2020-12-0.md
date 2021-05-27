---
title: Note sulla versione 2020.12.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2020.12.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 7%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per [!DNL Experience Manager] come Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 è il 17 dicembre 2020.
La versione seguente (2021.1.0) sarà il 28 gennaio 2021.

## [!DNL Adobe Experience Manager Sites] come Cloud Service {#sites}

* **[API](/help/assets/content-fragments/assets-api-content-fragments.md)** HTTP per frammento di contenuto: Aggiungi la possibilità di aggiungere/aggiornare ed eliminare varianti di frammenti di contenuto utilizzando l’API HTTP.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* L&#39;integrazione con [!DNL Adobe InDesign Server] è ora disponibile per [!DNL Experience Manager] come [!DNL Cloud Service]. Fornisce automazione per elaborare i file [!DNL Adobe InDesign] utilizzando gli script [!DNL Adobe InDesign Server] e consente agli utenti di utilizzare l&#39;interfaccia utente dei modelli [!DNL Assets] per creare brochure o annunci. Per [!DNL Experience Manager as a Cloud Service] è supportato solo [!DNL InDesign Server] ospitato da [!DNL Adobe Managed Services]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] viene migliorato per tenere traccia e visualizzare i riferimenti alle risorse quando una risorsa viene utilizzata in una  [!DNL Experience Manager Sites] distribuzione remota utilizzando la funzionalità Risorse collegate. Una nuova scheda [!UICONTROL Riferimenti] nella pagina [!UICONTROL Proprietà] della risorsa elenca ora i riferimenti locali e remoti della risorsa. I riferimenti consentono agli utenti DAM di monitorare l’utilizzo delle risorse nelle pagine [!DNL Sites] e nelle risorse composite in [!DNL Assets]. Consulta [configurare e utilizzare Risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] Le funzionalità sono ora accessibili tramite i componenti core basati su  [!DNL Sites] immagini. Gli autori possono configurare rapidamente i componenti per utilizzare i predefiniti immagine, ritaglio avanzato e modificatori immagine durante la creazione di pagine web. Consulta [Versione Core Components 2.13.0](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] l’app desktop consente agli utenti di caricare file e cartelle trascinando i file da Esplora risorse o dal Finder del Mac sull’interfaccia dell’app desktop. Consulta [aggiungere risorse utilizzando l’app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È stato rilasciato il sito di riferimento CIF Venia - 2020.12.01 che include la versione più recente dei componenti core CIF versione v1.6.0. Per ulteriori informazioni, consulta [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) .

* È stata rilasciata la versione 1.6.0 dei componenti core CIF. Per ulteriori informazioni, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) .

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.12.0 è il 10 dicembre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* Gestione autonoma dei [certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e [nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Gestione self-service di [Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* La pagina dei dettagli **Ambiente** aggiornata ora consente agli utenti di gestire i nomi di dominio personalizzati e gli Elenchi consentiti IP nei loro ambienti.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Alcune occorrenze di errori nella fase di scansione del codice senza fornire i risultati risolti.

* La scheda ambiente non visualizzava in modo coerente il pulsante **Aggiungi** .

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità in [!DNL Code Refactoring Tools] {#what-is-new-crt}

* È stata rilasciata la nuova versione del plug-in AIO-CLI. La versione più recente di questo plug-in include correzioni di bug per AEM Dispatcher Converter e Repository Modernizer e supporta anche una nuova utility - Index Converter. Per ulteriori informazioni su questo plug-in, consulta [Esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) .

* Index Converter è un&#39;utilità che può essere utilizzata per trasformare le definizioni di indice OAK personalizzato di un cliente in AEM come definizioni di indici OAK compatibili con il Cloud Service. Per ulteriori informazioni, consulta [Convertitore indice](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) .

* Nuova funzionalità aggiunta a [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) che crea un pacchetto separato `ui.config` per contenere tutte le configurazioni OSGi.

### Correzioni di bug {#crt-bug-fixes}

* Diverse correzioni di bug eseguite sugli strumenti AEM Dispatcher Converter e Repository Modernizer . Fai riferimento a [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Data di rilascio {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.1.20 è il 8 gennaio 2021.

### Novità in [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Gli utenti possono ora sapere se il token di accesso è scaduto passando il cursore sull’icona di stato nell’interfaccia utente dello strumento Content Transfer (Content Transfer Tool). Inoltre, nell’interfaccia utente dei Dettagli set di migrazione verrà notificato che non è possibile connettersi all’istanza del Cloud Service.

### Correzioni di bug {#ctt-bug-fixes}

* Lo stato dell’interfaccia utente dello strumento Content Transfer (CTT) per un set di migrazione non persisteva e veniva modificato dopo un periodo di inattività. Questo problema è stato risolto.
* Se i registri non erano disponibili, l’opzione per visualizzare i registri era disabilitata. Questo problema è stato risolto ed è stato aggiunto un messaggio per informare l’utente del motivo per cui i registri sono mancanti.
* Lo stato dell’interfaccia utente dello strumento Content Transfer (Trasferimento contenuti) mostrava *FAILED* quando l’utente arrestava un’acquisizione. Questo problema è stato risolto per visualizzare *STOPPED*.
