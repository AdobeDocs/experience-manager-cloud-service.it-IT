---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: f89fbf4e693fb1b17e8923dfcc6c9b4de92b536d
workflow-type: tm+mt
source-wordcount: '1928'
ht-degree: 2%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Vedi [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

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

* L’annotazione dei file PDF è ora supportata tramite strumenti di commento e annotazione nativi di Adobe Document Cloud. Aggiunta di testo, evidenziazioni, note adesive e disegni al contenuto di PDF direttamente nella finestra di anteprima del documento. Gli utenti possono anche passare alle pagine di interesse in PDF cliccando su commenti specifici

* Gli utenti possono ora ordinare le risorse visualizzate nei risultati della ricerca nelle viste a colonne e a schede. L’ordinamento viene eseguito sulle colonne Nome, Creato, Modificato o Nessuno.

   ![Ordina i risultati della ricerca in [!DNL Assets] nelle viste a colonne e a schede](/help/assets/assets/sort-searched-assets.png)
   *Figura: Ordina i risultati della ricerca in [!DNL Assets] nelle viste a colonne e a schede.*

### Nuova funzione nel [!DNL Assets] canale prerelease {#assets-prerelease-features}

* [!DNL Assets] ora include un connettore integrato per [!DNL Azure Media Services] per trascrizione audio e video. Una volta configurati, i file supportati vengono automaticamente trascritti e generati file WebVTT. I sottotitoli WebVTT vengono utilizzati per eseguire ricerche, sottotitoli o traduzioni più efficaci da utilizzare come sottotitoli.

<!-- TBD: 'Unpublishing' this feature as suggested by engineering.

* To programmatically invoke processing using asset microservices, a new API is introduced. Developers can now apply an existing folder-level processing profile on one or more specific assets in a folder. The processing profile gets applied based on custom metadata properties updates. See `AssetProcessor` in the [[!DNL Experience Manager] API reference](https://www.adobe.io/experience-manager/reference-materials/). As before, it is possible to [use asset microservices from the user interface](/help/assets/asset-microservices-configure-and-use.md).

-->
<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep prerelease channel.
A/V transcription feature via CQ-4303854 has moved to Oct prerelease now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità di [!DNL Forms] {#what-is-new-forms-sep-2021}

* **Utilizzare i ruoli Adobe Sign in un modulo adattivo**: Adobe Sign per i livelli di servizio aziendali e aziendali ha la possibilità di espandere i ruoli per i destinatari del contratto, oltre al solo firmatario, in modo da soddisfare meglio i requisiti del flusso di lavoro. Ora puoi [abilitare ogni destinatario dell&#39;accordo a configurare il proprio ruolo in un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform), con il ruolo predefinito Firma .

* **Analytics per Forms adattivo**: Ora puoi acquisire e [tracciamento del comportamento dell’utente finale tramite Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/integrate-aem-forms-with-adobe-analytics.html) per Adattivo Forms per raccogliere informazioni sugli utenti finali. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

* **Facile connessione di AEM Forms con Microsoft Dynamics e Salesforce**: Il servizio fornisce la configurazione e i modelli di dati preconfigurati dell’origine dati per Microsoft Dynamics e Salesforce, che lo rendono [più rapido e semplice per gli sviluppatori per configurare Microsoft Dynamics e Salesforce come origini dati per un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en).

* **Firma elettronica di un modulo adattivo utilizzando DocuSign:** [È possibile utilizzare DocuSign per apporre la firma elettronica a un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/integrate-docusign-adaptive-forms.html). Il servizio fornisce un’azione di invio personalizzata per utilizzare DocuSign con un modulo adattivo.

### Funzioni beta di [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **Connettore di archiviazione unificata:** Utilizzare Unified Storage Connector per esternalizzare i dati in-process negli archivi gestiti dai clienti. Ad esempio, è possibile archiviare i dati dei flussi di lavoro AEM in elaborazione (AEM dati variabili di flusso di lavoro) contenenti dati personali sensibili (SPD) in un archivio gestito dal cliente.

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=en) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che consentono di:
   * Genera i documenti compilando i file modello con dati XML.
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

Questa sezione illustra le note sulla versione per Cloud Manager in AEM 2021.10.0 e 2021.9.0.

## Data di pubblicazione {#release-date-cm-oct}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.10.0 è il 14 ottobre 2021.
La prossima versione è prevista per il 4 novembre 2021.

### Novità {#what-is-new-cm-oct}

* In preparazione di alcune modifiche imminenti, nell’interfaccia utente verrà fatto riferimento alle pipeline di distribuzione esistenti ed etichettarle come **Stack completo** gasdotti.

* La scheda della pipeline è stata aggiornata per visualizzare una singola faccia integrata che mostra sia le pipeline di produzione che quelle non di produzione e l’utente può selezionare Esegui/Pausa/Riprendi direttamente dal menu delle azioni associato a ciascuna pipeline.

* Un utente con il ruolo di Deployment Manager può ora eliminare la pipeline di produzione in modo self-service tramite l’interfaccia utente.

* Le esperienze di aggiunta e modifica delle pipeline sono state aggiornate per poter utilizzare modelli moderni e familiari.

* Gli utenti di Cloud Manager ora possono inviare un feedback direttamente dall’interfaccia utente tramite l’ **Feedback** in alto a destra della pagina di destinazione.

* I grafici SLA annuali possono ora essere scaricati dall’interfaccia utente di Cloud Manager.

* Le esecuzioni della pipeline di qualità del codice e non di produzione ora utilizzeranno un processo di duplicazione poco profondo più efficiente durante il passaggio di creazione, consentendo ai clienti con archivi Git di dimensioni particolarmente grandi di ottenere tempi di creazione più rapidi.

* La procedura guidata Aggiungi Elenco consentiti IP informa l’utente se è stato raggiunto il numero massimo consentito di Elenchi consentiti IP.

* La documentazione API di Cloud Manager ora include un parco giochi interattivo che consente agli utenti connessi di sperimentare l’API dal proprio browser. Vedi [Playground API di Cloud Manager](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) per ulteriori dettagli.

* La descrizione comandi nella scheda Programma sarà più descrittiva se un’opzione di selezione in &quot;Passa a&quot; è disabilitata. Ora viene visualizzato &quot;Un ambiente di produzione non esiste&quot;.

## Data di pubblicazione {#release-date-cm-sept}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.9.0 è il 9 settembre 2021.

### Correzioni di bug {#bug-fixes-cm-oct}

* In rare situazioni, quando uno staff Adobe ripristina l&#39;ambiente del cliente, il ripristino è stato considerato completo prima che l&#39;ambiente fosse completamente operativo.

* Alcune richieste interne effettuate durante la creazione dell’ambiente non sono state ritentate.

* Se si verifica un errore di distribuzione in seguito alla verifica del nome di dominio, il messaggio di errore è stato corretto per richiedere al cliente di contattare il proprio rappresentante Adobe.


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

## Strumento Content Transfer (Trasferimento contenuti)  {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt-latest}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.6.0 è il 4 ottobre 2021.

### Novità {#what-is-new-ctt}

* Strumento di mappatura utenti migliorato con un’esperienza utente semplificata, incluse le seguenti funzioni elencate di seguito. Per ulteriori informazioni, consulta [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html).
   * Verificare la connessione all&#39;API User Management prima di eseguire User Mapping
   * Salta con attenzione gli errori e continua con l’attività Mappatura utente
   * La mappatura utente non ha più esito negativo se **Token di accesso** scade dopo 24 ore. La mappatura utente può essere rieseguita dal punto in cui è stata arrestata per ultima.

* Per aumentare la robustezza dello strumento Content Transfer (Trasferimento contenuti), il contenuto può essere acquisito sia nell’istanza Author che nell’istanza Publish alla volta. Vedi [Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) per ulteriori dettagli.

* Quando sono incluse le versioni, il percorso `/var/audit` è incluso automaticamente per la migrazione degli eventi di controllo.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa-latest}

La data di rilascio di Best Practices Analyzer v2.1.20 è il 5 ottobre 2021.

### Novità {#what-is-new}

* Possibilità di rilevare e segnalare la lunghezza del nome del nodo.

* Capacità di rilevare e segnalare la dimensione totale dell&#39;indice.

* Possibilità di rilevare e segnalare le risorse per le quali manca il rendering originale.

