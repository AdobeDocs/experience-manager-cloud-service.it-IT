---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 1c27b66bcd0536ec10a878b39b9ec76073634c06
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2022.7.0) è l’8 agosto 2022.

La prossima versione (2022.8.0) è prevista per il 1° settembre 2022.

## Video sulla versione {#release-video}

Guarda il video Panoramica sulla versione di luglio 2022 per un riepilogo delle funzioni aggiunte nella versione 2022.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Sites] {#sites-features}

* La [Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) ora supporta [scelte rapide da tastiera](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md).

* AEM come Cloud Service [distribuzione di immagini ottimizzate per il web](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) consente di migliorare in modo significativo la velocità della pagina distribuendo formati come WebP. Questo nuovo servizio offre anche opzioni più flessibili per il ridimensionamento e la trasformazione delle immagini. Tutte le versioni di [Componente immagine core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=it) consente di sfruttare questo servizio e di distribuire immagini come WebP facendo clic su un&#39;opzione nel criterio del componente immagine.

* AEM le attività di personalizzazione possono ora sfruttare i frammenti di esperienza al posto delle nostre offerte legacy. Questa funzione:
   * abilita un percorso di migrazione in cui AEM contenuto promuoverebbe le offerte di frammenti di esperienza anziché le offerte della libreria precedente, per fornire contenuti con stili appropriati in linea con la personalizzazione su larga scala.
   * impedisce agli autori di contenuti di servire accidentalmente contenuti non formattati sul sito.
   * consente di convertire la modalità di targeting di qualsiasi componente in un frammento di esperienza (sia di tipo JSON che HTML) che utilizza modelli modificabili.

>[!NOTE]
>
>Le attività di personalizzazione esistenti che utilizzano già offerte legacy possono continuare a farlo, ma è necessario creare nuove attività di personalizzazione come frammenti di esperienza, in quanto questo è l’approccio consigliato in futuro.

## [!DNL Experience Manager Assets] come [!DNL Cloud Service] {#assets}

### Nuove funzioni disponibili nel canale prerelease di [!DNL Assets] {#prerelease-features-assets}

Ora puoi configurare Adobe Experience Manager Assets in [limita il tipo di risorse che gli utenti possono caricare in base al tipo MIME](/help/assets/configure-asset-upload-restrictions.md).

![Restrizioni al caricamento delle risorse](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Nuove funzioni in [!DNL Forms] {#forms-features}

* **[Supporto di input da tastiera per le firme di script](/help/forms/signing-forms-using-scribble.md)**: I dispositivi touch utilizzano sempre più l’Adaptive Forms e un requisito comune è il supporto delle firme. La firma di documenti su dispositivi touch è diventato un modo accettato di firmare moduli. Adaptive Forms supporta il supporto nativo per le firme digitali e Adobe Sign per tali casi d&#39;uso. Ora, insieme ad altre opzioni già supportate, è anche possibile utilizzare la tastiera per scorrere le firme in un modulo adattivo. Consente inoltre di migliorare la conformità in materia di accessibilità.

![Supporto di input da tastiera per le firme scorrevoli su iphone](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **Utilizza la procedura guidata Adattivo di Forms nella lingua locale**: Puoi utilizzare la procedura guidata nella lingua desiderata. Ora supporta tutte le lingue supportate da Adobe Experience Manager.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[Richiama DDX - Un passaggio del flusso di lavoro AEM](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**: Document Description XML (DDX) è un linguaggio di markup dichiarativo i cui elementi rappresentano blocchi predefiniti di documenti. Questi blocchi predefiniti includono documenti PDF e XDP e altri elementi quali commenti, segnalibri e testo con stili. I documenti DDX sono modelli per i documenti e descrivono le caratteristiche desiderate dei documenti di origine che dovrebbero essere visualizzate nei documenti risultanti. Un singolo DDX può essere utilizzato con una serie di documenti sorgente. È possibile utilizzare la fase Invoke e un flusso di lavoro AEM per eseguire varie operazioni, come l&#39;assemblaggio dei documenti di smontaggio, la creazione e la modifica di Acrobat e XFA Forms e altre operazioni descritte in [Riferimento DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) documentazione.

* **[Converti in PDF/A - Un passaggio del flusso di lavoro AEM](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**: PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, tutti i font sono incorporati e il file non è compresso. Ora è possibile utilizzare il passaggio Converti in PDF/A e un flusso di lavoro AEM per convertire i documenti o i file in qualsiasi formato in formato PDF/A.


## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* L’arricchimento del catalogo dei prodotti ora supporta AEM pagine. Questo consente agli autori di gestire l’associazione pagina - prodotto.

* Vari miglioramenti dei componenti core CIF

### Correzioni di bug {#bug-fixes-cif}

* Aggiungi token di accesso al recupero prezzi lato client

* Componente pagina errato nel livello dati

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* La [Browser del repository](/help/implementing/developing/tools/repository-browser.md) ora dispone di un campo di input del percorso, che consente di passare direttamente a una cartella specifica nella gerarchia del repository
* Sling Content Distribution (SCD) ora supporta un’azione esplicita di &quot;annullamento della validità&quot; per annullare la validità del contenuto senza la pubblicazione di tale contenuto. Fai riferimento a [Memorizzazione in cache in AEM as a Cloud Service](/help/implementing/dispatcher/caching.md#explicit-invalidation) per ulteriori dettagli.
* mod_macro è ora disponibile in AEM as a Cloud Service. Fai riferimento a [questa tabella](/help/implementing/dispatcher/disp-overview.md) per un elenco dei moduli Apache supportati.

### Miglioramenti AEM strumenti SDK Dispatcher as a Cloud Service {#dispatcher-tools-enhancements}

* Apache può iniziare con `docker_run_hot_reload.sh` , che caricherà e convalida automaticamente eventuali modifiche successive alla configurazione di apache e dispatcher, migliorando in tal modo la velocità degli sviluppatori. Supportato solo per la modalità flessibile degli strumenti del dispatcher. Vedi anche [Debug della configurazione di Apache e Dispatcher](/help/implementing/dispatcher/validation-debug.md#automatic-reloading) per ulteriori informazioni sul ricaricamento e la convalida automatici.
* La configurazione locale di apache/dispatcher seguirà più da vicino le modifiche negli ambienti cloud, aumentando la parità tra i due ambienti.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service è ora integrato con Unified Shell per migliorare l’esperienza utente e per coerenza con tutte le altre applicazioni di Experience Cloud. Per ulteriori dettagli, consulta [AEM as a Cloud Service su Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md).

## Connettori di Adobe Learning Manager {#learn-manage}

* Il nuovo Adobe Learning Manager dispone di connettori per Adobe Experience Manager Sites, Marketi Engage e Adobe Commerce. Per ulteriori informazioni, consulta: [Guida utente di Adobe Learning Manager](https://helpx.adobe.com/learning-manager/user-guide.html).


## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
