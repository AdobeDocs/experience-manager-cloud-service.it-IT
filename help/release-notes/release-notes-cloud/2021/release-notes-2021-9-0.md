---
title: Note sulla versione 2021.9.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2021.9.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 21%

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

La data di rilascio di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] la versione corrente (2021.9.0) è il 6 ottobre 2021.
La seguente versione (2021.10.0) è del 4 novembre 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di settembre 2021](https://video.tv.adobe.com/v/337381) video per un riepilogo delle funzioni aggiunte.

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuova funzione in [!DNL Sites] canale prerelease {#sites-prerelease-features}

* I modelli per frammenti di contenuto ora vengono impostati automaticamente in stato di sola lettura una volta pubblicati, per evitare di interrompere in modo non intenzionale le query API live dopo la ripubblicazione di un modello modificato. Gli utenti ricevono un avviso quando tentano di modificare un modello pubblicato. La modifica è possibile dopo aver accettato l’avviso.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Ora gli utenti possono ordinare le risorse visualizzate nei risultati di ricerca nelle viste Colonna e Scheda. L’ordinamento funziona sulle colonne Nome, Creato, Modificato o Nessuno.

   ![Ordinare i risultati della ricerca in [!DNL Assets] nelle viste Colonna e Scheda](/help/assets/assets/sort-searched-assets.png)
   *Figura: Ordinare i risultati della ricerca in [!DNL Assets] nelle viste Colonna e Scheda.*

* Per richiamare in modo programmatico l’elaborazione utilizzando i microservizi per le risorse, viene introdotta una nuova API. Gli sviluppatori possono ora applicare un profilo di elaborazione a livello di cartella esistente su una o più risorse specifiche di una cartella. Il profilo di elaborazione viene applicato in base agli aggiornamenti delle proprietà dei metadati personalizzati. Consulta `AssetProcessor` nel [[!DNL Experience Manager] Riferimento API](https://www.adobe.io/experience-manager/reference-materials/). Come prima, è possibile [utilizzare i microservizi per le risorse dall’interfaccia utente](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms-sep-2021}

* **Utilizzare i ruoli di Adobe Sign in un modulo adattivo**: Adobe Sign per i livelli di servizio business ed enterprise ha la possibilità di espandere i ruoli dei destinatari del contratto, oltre a Firmatario, per soddisfare meglio i requisiti del flusso di lavoro. Ora puoi [consentire a ogni destinatario dell’accordo di configurare il proprio ruolo in un modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform), con Firmatario come ruolo predefinito.

* **Analytics per Forms adattivo**: ora puoi acquisire e tenere traccia del comportamento degli utenti finali tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni approfondite sugli utenti finali. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

* **Facile connessione di AEM Forms con Microsoft Dynamics e Salesforce**: il servizio fornisce la configurazione dell’origine dati predefinita e i modelli dati per Microsoft Dynamics e Salesforce, rendendoli [per gli sviluppatori, configurare Microsoft Dynamics e Salesforce come origini dati per un modulo adattivo in modo più semplice e veloce](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en).

* **Firma elettronica di un modulo adattivo tramite DocuSign:** È possibile utilizzare DocuSign per apporre la firma elettronica a un modulo adattivo. Il servizio fornisce un’azione di invio personalizzata per utilizzare DocuSign con un modulo adattivo. Puoi installare il pacchetto disponibile in Distribuzione di software per importare l’azione di invio.

### Funzioni beta di [!DNL Forms] {#sep-what-is-new-forms-prerelease}

* **Connettore di archiviazione unificata:** Utilizza il connettore di archiviazione unificata per esternalizzare i dati in-process negli archivi gestiti dal cliente. Ad esempio
   * Abilita la funzionalità di salvataggio e ripristino di Forms Portal e archivia le bozze di moduli adattivi in un archivio dati gestito dal cliente.
   * Archiviare dati di processo dei flussi di lavoro AEM (dati sulle variabili di flusso di lavoro AEM) contenenti dati personali sensibili (SPD) in un archivio gestito dal cliente.

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   * Generare i documenti compilando i file modello con dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   * Generare file di PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form.

Puoi scrivere a [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* La nuova scheda &quot;Contenuto e-commerce associato&quot; nell’editor di Sites aumenta l’efficienza dell’autore grazie all’accesso rapido ai contenuti dei prodotti AEM pertinenti per il contesto corrente

   ![Contenuto e-commerce associato](/help/assets/CIF/associated-commerce-content.png)

* È stata migliorata l’interfaccia utente di selezione dei prodotti per una migliore esperienza utente, maggiore efficienza e supporto per cataloghi di prodotti complessi

   ![Nuovo selettore prodotti](/help/assets/CIF/product-picker.png)

* Rispetta la proprietà &quot;include_in_menu&quot; nel componente di navigazione

### Correzioni di bug {#bug-fixes-cif}

* Lo svuotamento della cache del menu non funziona come previsto

* Errori JS durante il passaggio di distribuzione di AEM CS e quando non si utilizzano componenti lato client

* Impossibile creare la configurazione cloud CIF in cartelle che hanno un nodo sling:configs

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### Novità {#what-is-new-screens}

* Screens as a Cloud Service ora supporta il monitoraggio di base della riproduzione. Ora il lettore riporta diverse metriche di riproduzione per ciascun ping (30 secondi per impostazione predefinita). In base alle metriche, consente di rilevare vari casi limite (esperienza bloccata, schermata vuota, problemi di pianificazione, ecc.). Questa funzione consente al team di monitorare da remoto se un lettore riproduce correttamente i contenuti, migliora la reattività a schermate vuote o esperienze bloccate sul campo e diminuisce il rischio di mostrare all’utente finale un’esperienza non funzionante.
Consulta [Monitoraggio della riproduzione di base](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) per ulteriori dettagli.

* Il supporto miniature per video è ora supportato in Screens as a Cloud Service. Un autore di contenuti può definire una miniatura per video in modo che l’immagine possa essere utilizzata come segnaposto e testare correttamente la riproduzione e il targeting del contenuto, mentre il video effettivo è in fase di finalizzazione da parte del team appropriato. L’immagine può essere utilizzata anche nel caso in cui la riproduzione del video non riesca.
Consulta [Supporto miniature per video](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-screens}

* Impossibile visualizzare il contenuto dalla pagina incorporata. Il problema è stato risolto.

* Dopo aver eseguito correttamente l&#39;accesso, l&#39;accesso alla pagina predefinita (canali) si è concluso con una pagina Errore server interno.

* Le voci tag associate non sono state rimosse durante la rimozione delle playlist.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Nuove funzioni in [!DNL Experience Manager as a Cloud Service] {#foundation-features}

**Reti avanzate**

>[!INFO]
>
>La funzione di rete avanzata fa parte della versione 2021.9.0 e verrà abilitata per i clienti a metà ottobre.

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] ora offre diversi tipi di funzionalità di rete avanzate, tra cui:

* Uscita porta flessibile per far uscire il traffico da porte non standard. Ora possibile senza contattare il supporto Adobe.
* Indirizzo IP in uscita dedicato al traffico in uscita dall’AEM as a Cloud Service da un IP univoco, che ora supporta tutte le porte.
* VPN per proteggere il traffico tra l’infrastruttura e l’AEM as a Cloud Service.

Leggi le [documentazione](/help/security/configuring-advanced-networking.md) per ulteriori informazioni, tra cui come eseguire in autonomia il provisioning di reti avanzate utilizzando le API di Cloud Manager.

**Ottimizzazioni degli indici**

Per migliorare le prestazioni delle query di ricerca e dell’indicizzazione, l’indice full-text Lucene-2 non viene più utilizzato come strumento predefinito in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] da questa versione. Al fine di rimuovere questo indice full-text sugli ambienti AEM in conformità con i clienti AEM, Adobe Engineering lavora individualmente e proattivamente con i clienti per una rimozione gentile e sostenibile dell’indice full-text Lucene. Visita il sito [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [documentazione](/help/operations/indexing.md#index-optimizations) per ulteriori informazioni e in caso di domande, contatta direttamente il nostro supporto.

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.9.0 e 2021.8.0.

## Data di pubblicazione {#release-date-cm-sept}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.9.0 è il 9 settembre 2021.
La prossima versione è pianificata per il 7 ottobre 2021.

### Novità {#what-is-new-cm-sept}

* L’archetipo del progetto AEM utilizzato da Cloud Manager è stato aggiornato alla versione 30.

* Le schede del programma nella pagina di destinazione di Cloud Manager e l’esperienza associata sono state aggiornate.

* Ora il registro del passaggio della qualità del codice include informazioni di registrazione dettagliate sul processo di scansione di OakPal.

* Ora le opzioni di menu della pagina Attività includono l’opzione **Scarica registro** per le esecuzioni del generatore di codici completate. La selezione di questa opzione consente di scaricare il registro della fase di build.

* Facendo direttamente clic sulla scheda Programma, ora si accede alla pagina Panoramica di Cloud Manager.

### Correzioni di bug {#bug-fixes-sept}

* Ora l’utente visualizza un messaggio più comprensibile quando tenta di aggiungere un nuovo elenco IP consentiti in un programma nel quale è stato raggiunto il numero massimo di elenchi IP consentiti configurabili.

* Quando si selezionava l’opzione di menu Copia URL dalla schermata Archivi veniva copiato l’URL errato.

## Cloud Acceleration Manager {#cam}

### Data di pubblicazione {#release-date-october-cam}

La data di pubblicazione di Cloud Acceleration Manager è il 4 ottobre 2021.

### Novità {#what-is-new-cam}

* Cloud Acceleration Manager ora consente agli utenti di visualizzare i rapporti BPA in un’anteprima stampabile, che può essere stampata o stampata su PDF per facilitarne la condivisione. Fare riferimento ai punti 6 e 7 in [Utilizzo della scheda Analisi delle best practice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## Strumento Trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt-latest}

La data di pubblicazione dello strumento Content Transfer v1.6.0 è il 4 ottobre 2021.

### Novità {#what-is-new-ctt}

* È stata migliorata la mappatura degli utenti con un’esperienza utente semplificata, incluse le seguenti funzioni elencate di seguito. Per ulteriori informazioni, consulta [Utilizzo dello strumento di mappatura utenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=it#using-user-mapping-tool).
   * Verifica la connessione all’API User Management prima di eseguire la mappatura utente
   * Ignora gli errori e continua con l’attività Mappatura utenti
   * La mappatura degli utenti non ha più esito negativo se il token di accesso scade (dopo 24 ore). La mappatura utenti può essere rieseguita dall’ultima posizione in cui è stata interrotta.

* Per aumentare la robustezza di CTT, il contenuto può essere acquisito in un’istanza di authoring o di pubblicazione alla volta.

* Quando sono incluse le versioni, il percorso `/var/audit` è incluso automaticamente per migrare gli eventi di controllo.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa-latest}

La data di rilascio di Best Practices Analyzer v2.1.18 è il 2 settembre 2021.

### Novità {#what-is-new}

* Possibilità di rilevare e segnalare il numero totale di nodi.

* Possibilità di rilevare e segnalare il tipo e le dimensioni dell’archivio nodi.

### Correzioni di bug {#bug-fixes-bpa}

* BPA stava rilevando erroneamente la presenza di Commerce Integration Framework.
