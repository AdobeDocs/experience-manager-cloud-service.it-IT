---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
translation-type: tm+mt
source-git-commit: a09377df02225e9ad58ea4a8a0671fc40bd7d703
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 5%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

Nella sezione seguente sono riportate le note generali sulla versione relative a [!DNL Experience Manager] come Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] come Cloud Service 2020.12.0 è il 17 dicembre 2020.
La seguente release (2021.1.0) sarà del 28 gennaio 2021.

## [!DNL Adobe Experience Manager Sites] come Cloud Service  {#sites}

* **[API](/help/assets/content-fragments/assets-api-content-fragments.md)** HTTP frammento di contenuto: Aggiunta la possibilità di aggiungere/aggiornare ed eliminare varianti di frammenti di contenuto mediante l&#39;API HTTP.

## [!DNL Adobe Experience Manager Assets] come  [!DNL Cloud Service] {#assets}

* L&#39;integrazione con [!DNL Adobe InDesign Server] è ora disponibile per [!DNL Experience Manager] come [!DNL Cloud Service]. Fornisce automazione per elaborare i file [!DNL Adobe InDesign] utilizzando [!DNL Adobe InDesign Server] script e consente agli utenti di utilizzare l&#39;interfaccia utente dei modelli [!DNL Assets] per creare brochure o annunci. Solo [!DNL InDesign Server] ospitato da [!DNL Adobe Managed Services] è supportato per [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] è stato migliorato per tenere traccia e visualizzare i riferimenti alle risorse quando una risorsa viene utilizzata in una  [!DNL Experience Manager Sites] distribuzione remota tramite la funzionalità Risorse collegate. Una nuova scheda [!UICONTROL Riferimenti] nella pagina [!UICONTROL Proprietà] della risorsa elenca ora i riferimenti locali e remoti della risorsa. I riferimenti consentono agli utenti DAM di tenere traccia dell’utilizzo delle risorse nelle [!DNL Sites] pagine e nelle risorse composte in [!DNL Assets]. Consulta [configurare e utilizzare le risorse connesse](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] le funzionalità sono ora accessibili tramite i componenti core basati su  [!DNL Sites] immagini. Gli autori possono configurare rapidamente i componenti per l’utilizzo dei predefiniti per immagini, del ritaglio avanzato e dei modificatori immagine durante la creazione di pagine Web. Consultate [Componenti di base 2.13.0 release](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] l&#39;app desktop consente agli utenti di caricare file e cartelle trascinandoli da Esplora risorse o dal Finder del Mac nell&#39;interfaccia dell&#39;app desktop. Consultate [aggiungere risorse tramite l&#39;app desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Sito di riferimento CIF Venia rilasciato - 2020.12.01 che include la versione più recente CIF Core Components v1.6.0. Per ulteriori informazioni, fare riferimento a [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01).

* Componenti CIF di base rilasciati v1.6.0. Per ulteriori informazioni, consultare [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0).

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio per Cloud Manager in AEM come Cloud Service 2021.1.0 è il 14 gennaio 2021.

### Correzioni di bug {#bug-fixes-cloud-manager}

* In alcuni casi, l&#39;istanza Produzione risorse può mostrare lo stato del Portale marchio nella pagina di dettaglio **Ambienti** come *In sospeso*, senza consentire all&#39;utente di eseguire alcuna azione.

* Quando si attiva la disattivazione da Cloud Manager, talvolta veniva visualizzato un messaggio di errore anche quando la disattivazione veniva avviata correttamente.

* Sono stati risolti rari casi di errori nella creazione o eliminazione dell&#39;ambiente.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità in [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Nuova versione del plugin AIO-CLI rilasciata. La versione più recente di questo plug-in include correzioni di bug per AEM Dispatcher Converter e Repository Modernizer e supporta anche una nuova utility - Index Converter. Fare riferimento a [Esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) per ulteriori informazioni su questo plug-in.

* Index Converter è un&#39;utility che può essere utilizzata per trasformare le definizioni dell&#39;indice OAK personalizzato di un cliente da AEM come definizione dell&#39;indice OAK compatibile con il Cloud Service. Per ulteriori informazioni, fare riferimento a [Convertitore indice](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter).

* Nuova funzionalità aggiunta a [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) che crea un pacchetto separato `ui.config` contenente tutte le configurazioni OSGi.

### Correzioni di bug {#crt-bug-fixes}

* Diverse correzioni di bug eseguite sugli strumenti AEM Dispatcher Converter e Repository Modernizer. Fare riferimento a [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## Strumenti di transizione verso il cloud {#code-transition-tools}

### Data di rilascio {#release-date-ctt}

La Data di rilascio per lo strumento di trasferimento dei contenuti v1.1.20 è il 08 gennaio 2021.

### Novità in [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Gli utenti possono ora sapere se il token di accesso è scaduto passando il puntatore sull&#39;icona di stato nell&#39;interfaccia utente CTT (Content Transfer Tool). Inoltre, nell’interfaccia utente dei dettagli del set di migrazione, verrà loro notificato che non sono in grado di connettersi all’istanza del Cloud Service.

### Correzioni di bug {#ctt-bug-fixes}

* Lo stato dell&#39;interfaccia utente CTT (Content Transfer Tool) per un set di migrazione non è persistente e non è stato modificato dopo un periodo di inattività. Questo è stato corretto.
* Se i registri non erano disponibili, l’opzione per visualizzare i registri era disabilitata. Questo problema è stato risolto ed è stato aggiunto un messaggio per segnalare all’utente i motivi della mancanza dei registri.
* Lo stato dell&#39;interfaccia utente dello strumento di trasferimento dei contenuti risultava NON RIUSCITO quando l&#39;utente arrestava un&#39;assimilazione. È stato risolto il problema per visualizzare *STOPPED*.

