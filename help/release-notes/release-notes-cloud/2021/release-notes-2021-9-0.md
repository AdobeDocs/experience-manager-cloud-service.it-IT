---
title: Note sulla versione 2021.9.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2021.9.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 12%

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

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2021.9.0) è il 6 ottobre 2021.
La versione seguente (2021.10.0) è del 4 novembre 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di settembre 2021](https://video.tv.adobe.com/v/337381) video per un riepilogo delle funzioni aggiunte.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuova funzione nel [!DNL Sites] canale prerelease {#sites-prerelease-features}

* I modelli di frammenti di contenuto vengono ora impostati automaticamente in modalità di sola lettura dopo la pubblicazione, per evitare l’interruzione involontaria delle query API live dopo la ripubblicazione di un modello modificato. Agli utenti viene visualizzato un avviso quando si tenta di modificare un modello pubblicato. Una modifica è possibile dopo aver accettato l’avviso.

## [!DNL Experience Manager Assets] come [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Gli utenti possono ora ordinare le risorse visualizzate nei risultati della ricerca nelle viste a colonne e a schede. L’ordinamento viene eseguito sulle colonne Nome, Creato, Modificato o Nessuno.

   ![Ordina i risultati della ricerca in [!DNL Assets] nelle viste a colonne e a schede](/help/assets/assets/sort-searched-assets.png)
   *Figura: Ordina i risultati della ricerca in [!DNL Assets] nelle viste a colonne e a schede.*

* Per richiamare l’elaborazione a livello di programmazione tramite i microservizi per le risorse, viene introdotta una nuova API. Gli sviluppatori possono ora applicare un profilo di elaborazione a livello di cartella esistente a una o più risorse specifiche di una cartella. Il profilo di elaborazione viene applicato in base agli aggiornamenti delle proprietà dei metadati personalizzati. Vedi `AssetProcessor` in [[!DNL Experience Manager] Riferimento API](https://www.adobe.io/experience-manager/reference-materials/). Come prima, è possibile [utilizzare i microservizi delle risorse dall’interfaccia utente](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms-sep-2021}

* **Utilizzare i ruoli Adobe Sign in un modulo adattivo**: Adobe Sign per i livelli di servizio aziendali e aziendali ha la possibilità di espandere i ruoli per i destinatari del contratto, oltre al solo firmatario, in modo da soddisfare meglio i requisiti del flusso di lavoro. Ora puoi [abilitare ogni destinatario dell&#39;accordo a configurare il proprio ruolo in un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform), con il ruolo predefinito Firma .

* **Analytics per Forms adattivo**: È ora possibile acquisire e tenere traccia del comportamento dell’utente finale tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni sull’utente finale. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

* **Facile connessione di AEM Forms con Microsoft Dynamics e Salesforce**: Il servizio fornisce la configurazione e i modelli di dati preconfigurati dell’origine dati per Microsoft Dynamics e Salesforce, che lo rendono [più rapido e semplice per gli sviluppatori per configurare Microsoft Dynamics e Salesforce come origini dati per un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en).

* **Firma elettronica di un modulo adattivo utilizzando DocuSign:** È possibile utilizzare DocuSign per apporre la firma elettronica a un modulo adattivo. Il servizio fornisce un’azione di invio personalizzata per utilizzare DocuSign con un modulo adattivo. È possibile installare il pacchetto disponibile in Distribuzione di software per importare l’azione di invio.

### Funzioni beta di [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **Connettore di archiviazione unificata:** Utilizzare Unified Storage Connector per esternalizzare i dati in-process negli archivi gestiti dai clienti. Ad esempio
   * Abilita la funzionalità di salvataggio e ripresa di Forms Portal e archivia le bozze dei moduli adattivi in un archivio dati gestito dal cliente.
   * Archiviare i dati dei flussi di lavoro AEM in-process (AEM dati variabili di flusso di lavoro) contenenti dati personali sensibili (SPD) in un archivio gestito dal cliente.

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   * Generare i documenti compilando i file modello con dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   * Generare file PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form.

Puoi scrivere in [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* La nuova scheda &quot;contenuti commerce associati&quot; nell’editor Sites aumenta l’efficienza dell’autore grazie all’accesso rapido ai contenuti di prodotti AEM pertinenti per il contesto corrente

   ![Contenuto di e-commerce associato](/help/assets/CIF/associated-commerce-content.png)

* Interfaccia utente del selettore prodotti migliorata per una migliore esperienza utente, una maggiore efficienza e il supporto per cataloghi di prodotti complessi

   ![Nuovo selettore prodotti](/help/assets/CIF/product-picker.png)

* Rispetta la proprietà &quot;include_in_menu&quot; nel componente di navigazione

### Correzioni di bug {#bug-fixes-cif}

* Lo scaricamento della cache del menu non funziona come previsto

* Errori JS durante AEM passaggio di distribuzione CS e quando non si utilizzano componenti lato client

* Impossibile creare la configurazione cloud CIF nelle cartelle con un nodo sling:configs

## [!DNL Experience Manager Screens] come [!DNL Cloud Service] {#screens}

### Novità {#what-is-new-screens}

* Screens as a Cloud Service ora supporta il monitoraggio di base della riproduzione. Ora il lettore riporta diverse metriche di riproduzione per ciascun ping (per impostazione predefinita, 30 secondi). In base alle metriche, fornisce la possibilità di rilevare vari casi edge (esperienza bloccata, schermo vuoto, problemi di pianificazione, ecc.). Questa funzione consente al team di monitorare da remoto se un lettore riproduce correttamente i contenuti, migliora la reattività a schermi vuoti o esperienze interrotte sul campo e diminuisce il rischio di mostrare un’esperienza non funzionante all’utente finale.
Vedi [Monitoraggio della riproduzione di base](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) per ulteriori dettagli.

* Supporto delle miniature per i video in ora supportato in Screens as a Cloud Service. Un autore di contenuti può definire una miniatura per i video in modo che l’immagine possa essere utilizzata come segnaposto e possa testare correttamente la riproduzione e il targeting del contenuto, mentre il video effettivo viene finalizzato dal team appropriato. L&#39;immagine può anche essere utilizzata, nel caso in cui la riproduzione del video non riesca.
Vedi [Supporto delle miniature per video](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-screens}

* Impossibile visualizzare il contenuto dalla pagina incorporata. Il problema è stato risolto.

* Dopo l&#39;accesso, passare alla pagina (canali) predefinita è finita in una pagina di errore del server interno.

* Le voci di tag associate non sono state rimosse durante la rimozione delle playlist.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Nuove funzioni in [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**Rete avanzata**

>[!INFO]
>
>La funzionalità di rete avanzata fa parte della versione 2021.9.0 e sarà abilitata per i clienti a metà ottobre.

[!DNL Adobe Experience Manager] come [!DNL Cloud Service] offre diversi tipi di funzionalità di rete avanzate, tra cui:

* Accesso a porte flessibili per il traffico in uscita da porte non standard. Ora è possibile senza contattare il supporto Adobe.
* Indirizzo IP di uscita dedicato per il traffico in uscita da AEM as a Cloud Service da un IP univoco, che ora supporta tutte le porte.
* VPN per proteggere il traffico tra l’infrastruttura e AEM as a Cloud Service.

Leggi la sezione [documentazione](/help/security/configuring-advanced-networking.md) per ulteriori informazioni, tra cui come self service provider di servizi di rete avanzati utilizzando le API di Cloud Manager.

**Ottimizzazioni indice**

Per migliorare le prestazioni delle query di ricerca e l’indicizzazione, l’indice full-text lucene-2 non viene più utilizzato come predefinito in [!DNL Adobe Experience Manager] come [!DNL Cloud Service] da questa versione. Al fine di rimuovere questo indice full-text sugli ambienti AEM in conformità con AEM clienti, Adobe Engineering lavora individualmente e proattivamente con i clienti per una rimozione dolce e sostenibile dell&#39;indice full-text Lucene. Visita [!DNL Adobe Experience Manager] come [!DNL Cloud Service] [documentazione](/help/operations/indexing.md#index-optimizations) per ulteriori informazioni e per qualsiasi domanda, contatta direttamente il nostro supporto.

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione per Cloud Manager in AEM 2021.9.0 e 2021.8.0.

## Data di pubblicazione {#release-date-cm-sept}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.9.0 è il 9 settembre 2021.
La prossima versione è prevista per il 7 ottobre 2021.

### Novità {#what-is-new-cm-sept}

* La versione dell’Archetipo di progetto AEM utilizzato da Cloud Manager è stata aggiornata alla versione 30.

* Le schede del programma nella pagina di destinazione di Cloud Manager e l’esperienza associata sono state aggiornate.

* Il registro dettagliato dei passaggi della qualità del codice ora include informazioni di registrazione dettagliate sul processo di scansione di OakPal.

* Le opzioni del menu della pagina Attività ora includono un’opzione per **Registro di download** per le esecuzioni di Code Generator completate. Selezionando questa opzione, il registro del passaggio di compilazione verrà scaricato.

* Facendo clic direttamente sulla scheda Programma, passa alla pagina Panoramica di Cloud Manager.

### Correzioni di bug {#bug-fixes-sept}

* L’utente vedrà ora un messaggio più comprensibile quando tenta di aggiungere un nuovo Elenco consentiti IP in un programma che ha raggiunto il numero massimo consentito di Elenchi consentiti IP configurabili.

* L&#39;URL errato è stato copiato quando si seleziona l&#39;opzione di menu Copia URL dalla schermata Repository.

## Cloud Acceleration Manager {#cam}

### Data di pubblicazione {#release-date-october-cam}

La data di rilascio di Cloud Acceleration Manager è il 4 ottobre 2021.

### Novità {#what-is-new-cam}

* Cloud Acceleration Manager offre agli utenti la possibilità di visualizzare i rapporti BPA in un&#39;anteprima stampabile, consentendo di stampare o stampare facilmente i rapporti in PDF per facilitarne la condivisione. Fai riferimento ai passaggi 6 e 7 in [Utilizzo della scheda di analisi delle best practice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## Strumento Trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt-latest}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.6.0 è il 4 ottobre 2021.

### Novità {#what-is-new-ctt}

* È stata migliorata la mappatura degli utenti con un’esperienza utente semplificata, incluse le seguenti funzioni elencate di seguito. Per ulteriori informazioni, consulta [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).
   * Verificare la connessione all&#39;API User Management prima di eseguire User Mapping
   * Salta con attenzione gli errori e continua con l’attività Mappatura utente
   * La mappatura utente non genera più errori se il token di accesso scade (dopo 24 ore). La mappatura utente può essere rieseguita dal punto in cui è stata arrestata per ultima.

* Per aumentare la robustezza del CTT, il contenuto può essere acquisito sia nell’istanza Author che nell’istanza Publish alla volta.

* Quando sono incluse le versioni, il percorso `/var/audit` è incluso automaticamente per la migrazione degli eventi di controllo.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa-latest}

La data di rilascio di Best Practices Analyzer v2.1.18 è il 2 settembre 2021.

### Novità {#what-is-new}

* Possibilità di rilevare e segnalare il conteggio totale dei nodi.

* Possibilità di rilevare e segnalare il tipo e la dimensione dell&#39;archivio nodi.

### Correzioni di bug {#bug-fixes-bpa}

* BPA rilevava falsamente la presenza di Commerce Integration Framework.
