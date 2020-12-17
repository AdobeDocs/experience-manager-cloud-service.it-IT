---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
translation-type: tm+mt
source-git-commit: 984914c6147d0ee96575c93496cbdfc4bb9bc094
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 5%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

Nella sezione seguente sono riportate le note generali sulla versione relative a [!DNL Experience Manager] come Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] come Cloud Service 2020.12.0 è il 17 dicembre 2020.
La seguente release (2021.1.0) sarà del 28 gennaio 2020.

## [!DNL Adobe Experience Manager Assets] come  [!DNL Cloud Service] {#assets}

* L&#39;integrazione con [!DNL Adobe InDesign Server] è ora disponibile per [!DNL Experience Manager] come [!DNL Cloud Service]. Fornisce automazione per elaborare i file [!DNL Adobe InDesign] utilizzando [!DNL Adobe InDesign Server] script e consente agli utenti di utilizzare l&#39;interfaccia utente dei modelli [!DNL Assets] per creare brochure o annunci. Solo [!DNL InDesign Server] ospitato da [!DNL Adobe Managed Services] è supportato per [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] è stato migliorato per tenere traccia e visualizzare i riferimenti alle risorse quando una risorsa viene utilizzata in una  [!DNL Experience Manager Sites] distribuzione remota tramite la funzionalità Risorse collegate. Una nuova scheda [!UICONTROL Riferimenti] nella pagina [!UICONTROL Proprietà] della risorsa elenca ora i riferimenti locali e remoti della risorsa. I riferimenti consentono agli utenti DAM di tenere traccia dell’utilizzo delle risorse nelle [!DNL Sites] pagine e nelle risorse composte in [!DNL Assets]. Consulta [configurare e utilizzare le risorse connesse](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] le funzionalità sono ora accessibili tramite i componenti core basati su  [!DNL Sites] immagini. Gli autori possono configurare rapidamente i componenti per l’utilizzo dei predefiniti per immagini, del ritaglio avanzato e dei modificatori immagine durante la creazione di pagine Web. Consultate [Componenti di base 2.13.0 release](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] l&#39;app desktop consente agli utenti di caricare file e cartelle trascinandoli da Esplora risorse o dal Finder del Mac nell&#39;interfaccia dell&#39;app desktop. Consultate [aggiungere risorse tramite l&#39;app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Sito di riferimento CIF Venia rilasciato - 2020.12.01 che include l&#39;ultima versione CIF Core Components v1.6.0. Per ulteriori informazioni, fare riferimento a [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01).

* Componenti CIF di base rilasciati v1.6.0. Per ulteriori informazioni, consultare [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0).

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio per Cloud Manager in AEM come Cloud Service 2020.12.0 è il 10 dicembre 2020.

### Novità in [!DNL Cloud Manager] {#what-is-new-cm}

* Gestione self-service di [certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) e [nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Gestione self-service di [Elenchi consentiti  IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* La pagina dei dettagli **Environment** aggiornata ora consente agli utenti di gestire i nomi di dominio e i Elenchi consentiti di  IP personalizzati nei propri ambienti.

### Correzioni di bug {#bug-fixes-cloud-manager}

* Alcune occorrenze di errori nella fase di scansione del codice senza fornire risultati risolti.

* La scheda ambiente non visualizzava in modo uniforme il pulsante **Aggiungi**.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità in [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Nuova versione del plugin AIO-CLI rilasciata. La versione più recente di questo plug-in include correzioni di bug per AEM Dispatcher Converter e Repository Modernizer e supporta anche una nuova utility - Index Converter. Fare riferimento a [Esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) per ulteriori informazioni su questo plug-in.

* Index Converter è un&#39;utility che può essere utilizzata per trasformare le definizioni dell&#39;indice OAK personalizzato di un cliente da AEM come definizione dell&#39;indice OAK compatibile con il Cloud Service. Per ulteriori informazioni, fare riferimento a [Convertitore indice](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter).

* Nuova funzionalità aggiunta a [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) che crea un pacchetto separato `ui.config` contenente tutte le configurazioni OSGi.

### Correzioni di bug {#crt-bug-fixes}

* Diverse correzioni di bug eseguite sugli strumenti AEM Dispatcher Converter e Repository Modernizer. Fare riferimento a [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).
