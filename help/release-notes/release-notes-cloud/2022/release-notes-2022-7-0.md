---
title: Note sulla versione 2022.7.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2022.7.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: b339ab48-e836-4589-a573-9c50917b9280
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 82%

---

# Note sulla versione 202278.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione 2022.7.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] (2022.7.0) è l’8 agosto 2022.

La prossima versione (2022.8.0) è prevista per il 1° settembre 2022.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di luglio 2022 per un riepilogo delle funzioni aggiunte alla versione 2022.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Sites] {#sites-features}

* La [Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console) ora supporta le [scelte rapide da tastiera](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md).

* AEM come Cloud Service [consegna di immagini ottimizzate per il web](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html?lang=it) consente di migliorare in modo significativo la velocità della pagina distribuendo formati come WebP. Questo nuovo servizio offre anche opzioni più flessibili per il ridimensionamento e la trasformazione delle immagini. Tutte le versioni di [Componente immagine core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html?lang=it) consente di utilizzare questo servizio e di distribuire immagini come WebP facendo clic su un’opzione nel criterio del componente immagine.

* Le attività di personalizzazione dell’AEM possono ora utilizzare frammenti di esperienza al posto delle offerte legacy. Questa funzione:
   * abilita un percorso di migrazione in cui il contenuto AEM promuoverebbe le offerte di Frammenti di esperienza anziché le offerte della libreria precedente, per fornire nel tempo contenuti con stili appropriati, in linea con la personalizzazione su larga scala.
   * impedisce agli autori di contenuti di inserire accidentalmente contenuti non formattati sul sito.
   * consente di convertire la modalità di targeting di qualsiasi componente in un Frammento di esperienza (sia di tipo JSON che HTML) che utilizza modelli modificabili.

>[!NOTE]
>
>Le attività di personalizzazione esistenti che utilizzano già offerte precedenti possono continuare a farlo, ma dovranno creare le nuove attività di personalizzazione come Frammenti di esperienza, in quanto questo è l’approccio consigliato in futuro.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni disponibili nel canale prerelease di [!DNL Assets] {#prerelease-features-assets}

Ora puoi configurare Adobe Experience Manager Assets in modo da [limitare il tipo di risorse che gli utenti possono caricare in base al tipo MIME](/help/assets/configure-asset-upload-restrictions.md).

![Restrizioni al caricamento delle risorse](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni in [!DNL Forms] {#forms-features}

* **[Supporto di input da tastiera per le firme scarabocchio](/help/forms/signing-forms-using-scribble.md)**: i dispositivi touch utilizzano sempre più i moduli adattivi e il supporto delle firme è un requisito comune. Firmare documenti su dispositivi touch è diventata una modalità accettata per firmare moduli. I moduli adattivi hanno il supporto nativo delle firme scarabocchio e Adobe Sign per tali casi d&#39;uso. Ora, insieme ad altre opzioni già supportate, è anche possibile utilizzare la tastiera per le firme scarabocchio in un modulo adattivo. Consente inoltre di migliorare la conformità in materia di accessibilità.

![Supporto di input da tastiera per le firme scarabocchio su iPhone](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **Utilizza l’assistente virtuale dei moduli adattivi nella lingua locale**: puoi utilizzare l’assistente virtuale nella lingua desiderata. Ora supporta tutte le lingue supportate da Adobe Experience Manager.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[Richiama DDX: un passaggio del flusso di lavoro AEM](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**: Document Description XML (DDX) è un linguaggio di markup dichiarativo i cui elementi rappresentano blocchi predefiniti di documenti. Questi blocchi predefiniti includono documenti PDF e XDP e altri elementi quali commenti, segnalibri e testo con stili. I documenti DDX sono modelli per i documenti e descrivono le caratteristiche desiderate dei documenti sorgente che dovrebbero essere visualizzate nei documenti risultanti. Un singolo DDX può essere utilizzato con una serie di documenti sorgente. È possibile utilizzare il passaggio Richiama e un flusso di lavoro AEM per eseguire varie operazioni, come assemblaggio e disassemblaggio di documenti, la creazione e la modifica di moduli Acrobat e XFA e altre operazioni descritte nella documentazione di [Riferimenti DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

* **[Converti in PDF/A: un passaggio del flusso di lavoro AEM](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**: PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, in cui sono incorporati tutti i font e il file non è compresso. Ora è possibile utilizzare il passaggio Converti in PDF/A e un flusso di lavoro AEM per convertire i documenti o i file in qualsiasi formato in formato PDF/A.


## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* L’arricchimento del catalogo dei prodotti ora supporta le pagine AEM. Questo consente agli autori di gestire l’associazione pagina - prodotto.

* Vari miglioramenti dei componenti core CIF

### Correzioni di bug {#bug-fixes-cif}

* Aggiungere token di accesso al recupero prezzi lato client

* Componente pagina errato in Data Layer

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* Il [Browser dell’archivio](/help/implementing/developing/tools/repository-browser.md) ora dispone di un campo di input del percorso che consente di passare direttamente a una cartella specifica nella gerarchia dell’archivio
* La Distribuzione dei contenuti Sling (SCD) ora supporta un’azione esplicita di &quot;annullamento della validità&quot; per annullare la validità del contenuto senza pubblicarlo. Consulta [Memorizzazione in cache in AEM as a Cloud Service](/help/implementing/dispatcher/caching.md#explicit-invalidation) per ulteriori dettagli.
* La mod_macro adesso è disponibile in AEM as a Cloud Service. Consulta [questa tabella](/help/implementing/dispatcher/disp-overview.md) per un elenco dei moduli Apache supportati.

### Miglioramenti degli strumenti di Dispatcher SDK in AEM as a Cloud Service {#dispatcher-tools-enhancements}

* Apache può essere avviato con lo script `docker_run_hot_reload.sh`, che caricherà e convaliderà automaticamente eventuali modifiche successive alla configurazione di Apache e Dispatcher, migliorando così la velocità degli sviluppatori. Supportato solo per la modalità flessibile degli strumenti del dispatcher. Per ulteriori informazioni sul ricaricamento e la convalida automatici, consulta anche [Debug della configurazione di Apache e Dispatcher](/help/implementing/dispatcher/validation-debug.md#automatic-reloading).
* La configurazione locale di Apache/Dispatcher traccerà con maggiore attenzione le modifiche negli ambienti cloud, aumentando il livello di parità tra i due ambienti.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Experience Manager] {#prerelease-features-foundation}

* AEM as a Cloud Service è ora integrato con Unified Shell per migliorare l’esperienza utente e per coerenza con tutte le altre applicazioni di Experience Cloud. Consulta [AEM as a Cloud Service su Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) per ulteriori dettagli.

## Connettori di Adobe Learning Manager {#learn-manage}

* Il nuovo Adobe Learning Manager dispone di connettori per Adobe Experience Manager Sites, Marketo Engage e Adobe Commerce. Per ulteriori informazioni, consulta: [Guida utente di Adobe Learning Manager](https://helpx.adobe.com/it/learning-manager/user-guide.html).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
