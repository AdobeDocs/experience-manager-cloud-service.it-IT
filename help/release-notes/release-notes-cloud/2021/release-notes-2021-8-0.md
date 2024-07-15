---
title: Note sulla versione 2021.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2021.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 8b041934-1c4a-4670-9b03-d38f683b99e5
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 27%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti. Ad esempio, nel 2020 e nel 2021.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.8.0) è il venerdì 26 agosto 2021.
La seguente versione (2021.9.0) è del giovedì 6 ottobre 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al video Panoramica sulla versione di [agosto 2021](https://video.tv.adobe.com/v/336277) per un riepilogo delle funzioni aggiunte.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Quando condividi risorse digitali come collegamento, l’utente può copiare immediatamente l’URL negli Appunti. Questo miglioramento consente di condividere le risorse in modo più rapido e conveniente. Questa funzionalità consente una condivisione delle risorse più rapida e conveniente.

  ![Opzione Copia URL durante la condivisione di una risorsa come collegamento](/help/assets/assets/link-share-copy-URL-option.png)
  *Figura: quando condividi una risorsa come collegamento, ora puoi copiare l&#39;URL per condividerlo separatamente.*

* Quando carichi i file TXT, i microservizi per le risorse generano automaticamente una miniatura. La miniatura PNG è una rappresentazione di un file TXT che aiuta gli utenti a identificare il contenuto o i file in una certa misura, senza aprire i file. Questa funzionalità non richiede alcuna configurazione e funziona per impostazione predefinita.

  ![Una rappresentazione di un file TXT viene generata automaticamente da [!DNL Assets] in formato PNG](/help/assets/assets/thumbnail-rendition-txt-file.png)
  *Figura: viene generata automaticamente una copia trasformata di un file TXT per identificare il file senza aprirlo.*

### Nuova funzionalità nel canale prerelease [!DNL Assets] {#assets-prerelease-features}

* Ora gli utenti possono ordinare le risorse visualizzate nei risultati di ricerca nelle viste Colonna e Scheda. L’ordinamento funziona sulle colonne Nome, Creato, Modificato o Nessuno.

  ![Ordinare i risultati della ricerca in [!DNL Assets] nelle viste Colonna e Scheda](/help/assets/assets/sort-searched-assets.png)
  *Figura: Ordinare i risultati della ricerca in [!DNL Assets] nelle visualizzazioni Colonna e Scheda.*

### Bug corretti in [!DNL Assets] {#assets-bugs-fixed}

* Quando un membro del gruppo di collaboratori passa alla console [!DNL Assets], viene generata una richiesta `POST` aggiuntiva per creare una raccolta. Questa richiesta non è necessaria; non riesce a causa di problemi di autorizzazioni e crea molti errori nei registri. (CQ-4328856)
* Quando gli utenti visualizzano una risorsa e selezionano [!UICONTROL Timeline] dal menu a comparsa nel pannello a sinistra, viene visualizzato un errore. Nei registri vengono registrati molti avvisi a causa di una query non valida. (CQ-4328919)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* Il servizio di automated forms conversion può [convertire i PDF forms in lingua italiana e portoghese](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) in Forms adattivo.

* **Documento di record basato su Acroform**: AEM Forms as a Cloud Service supporta l’utilizzo di [Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=it) come modello per documento record oltre al modello di modulo basato su XFA.

* **Connettore per l&#39;archivio dati Microsoft® Azure**: è ora possibile [collegare il modello dati dei moduli al sistema di archiviazione Microsoft® Azure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html). Consente di recuperare e archiviare i dati dei moduli adattivi come BLOB nell’archiviazione di Microsoft® Azure.

### Nuove funzioni disponibili nel canale pre-release di [!DNL Forms] {#prerelease-features-forms}

* **Utilizzare i ruoli di Adobe Sign in un modulo adattivo** - Adobe Sign per i livelli di servizio business ed enterprise può facoltativamente espandere i ruoli per i destinatari del contratto, oltre al solo firmatario, per soddisfare meglio i requisiti del flusso di lavoro. Ora è possibile abilitare ogni destinatario dell’accordo a configurare il proprio ruolo in un modulo adattivo, con Firmatario come ruolo predefinito.

* **Analytics per Forms adattivo** - È ora possibile acquisire e monitorare il comportamento degli utenti finali tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni approfondite sugli utenti finali. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

* **Connetti facilmente AEM Forms con Microsoft® Dynamics e Salesforce.com** - Il servizio fornisce la configurazione dell&#39;origine dati predefinita e i modelli dati per Microsoft® Dynamics e Salesforce.com. In questo modo gli sviluppatori possono configurare Microsoft® Dynamics e Salesforce.com come origini dati per un modulo adattivo in modo più rapido e semplice.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Nuova interfaccia utente per il selettore delle categorie per migliorare l’esperienza utente, l’efficienza e il supporto per cataloghi di prodotti complessi

  ![Selezione nuova categoria](/help/assets/CIF/category-picker.png)

* Migliore supporto A11Y per i componenti core CIF

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.8.0 e 2021.7.0.

## Data di rilascio {#release-date-cm-aug}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.8.0 è il 12 agosto 2021.
La prossima versione è pianificata per il 9 settembre 2021.

### Novità {#what-is-new-aug}

* Ora chi usa Cloud Service può visualizzare i rapporti SLA (Service Level Agreement) in Cloud Manager. Questo sarà reso disponibile progressivamente nei prossimi mesi.
Consulta [Generazione rapporti SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/sla-reporting.html?lang=it).

* Il tipo e la gravità di IndexType e delle regole di qualità `IndexDamAssetLucene` sono stati modificati. Entrambi i bug sono ora di entità *bloccante*.

* Sono state introdotte nuove regole per la qualità dell’indice Oak che riguardano le configurazioni asincrone e tika.

* Il numero massimo di certificati SSL per programma è aumentato a 50.

* Funzionalità self-service per consentire agli utenti di creare e gestire più archivi tramite l’interfaccia utente di Cloud Manager.

* SonarQube leggeva inutilmente i dati della cronologia Git. Su basi di codice di grandi dimensioni, ciò poteva comportare un’immotivata riduzione delle prestazioni della build.

* Ora è disponibile un’API per rendere non valida la cache di dipendenza Maven per ogni pipeline.

* L’archetipo del progetto AEM utilizzato da Cloud Manager è stato aggiornato alla versione 29.

### Correzioni di bug {#bug-fixes-aug}

* Lo stato Aggiornamento disponibile non dovrebbe essere visualizzato quando l’ultima versione è precedente alla versione corrente.

* L’onboarding iniziale non veniva avviato correttamente per le nuove organizzazioni con nomi lunghi.

* Talvolta, quando una pipeline veniva attivata due volte per qualche motivo, si verificava un errore in una delle esecuzioni con *`cannot update pipeline execution status`*.

## Strumento Trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt-latest}

La data di pubblicazione dello strumento Content Transfer v1.5.6 è l’11 agosto 2021.

### Correzioni di bug {#bug-fixes-ctt}

* A volte, non tutti gli utenti venivano migrati all’istanza di destinazione. Per ottenere questa correzione, è necessario disporre di CTT v1.5.6 insieme a aem-ethos-tools 1.2.354 o versione successiva sull’istanza AEM as a Cloud Service di destinazione.

* Il pulsante **Interrompi acquisizione** è stato disabilitato durante l&#39;acquisizione nell&#39;istanza di Publish. Questo non è necessario perché non è presente alcun passaggio di ripristino mongo durante l’acquisizione di Publish.

* CTT non ha eseguito la pulizia della directory `/tmp` dopo un&#39;estrazione riuscita. Questo a volte causava problemi di spazio su disco.
