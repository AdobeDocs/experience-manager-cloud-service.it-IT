---
title: Note sulla versione 2021.3.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Note sulla versione as a Cloud Service per 2021.3.0."
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
source-git-commit: acd80887d71a528604d37fa2787bca3c3a48d7c4
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 41%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0 è il 25 marzo 2021.
La versione seguente (2021.4.0) sarà del 29 aprile 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* [Versione progressiva di un sito Web App (PWA)](/help/sites-cloud/authoring/features/enable-pwa.md) può ora essere abilitato a livello di progetto tramite una configurazione semplice.
* Estensioni del modello per frammenti di contenuto : ora è possibile definire tipi di dati di testo con più righe come elenchi a più campi.
* Miglioramenti dell’interfaccia utente dell’Editor frammenti di contenuto : i frammenti secondari nidificati vengono ora visualizzati nella breadcrumb e viene migliorata la visualizzazione delle azioni di pubblicazione, salvataggio e salvataggio/uscita

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] estende la funzionalità Risorse collegate per supportare l’utilizzo di [!DNL Dynamic Media] immagini nei componenti core supportati. Vedi [utilizzare Risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).
* Gli amministratori di Experience Manager possono pianificare l’inserimento di risorse in blocco in una data o un’ora specifica. Inoltre, gli amministratori possono pianificare acquisizioni ricorrenti in base a data e ora. Vedi [inserimento di risorse in massa](/help/assets/add-assets.md#asset-bulk-ingestor).

### Correzioni di bug in [!DNL Assets] {#bug-fixes-assets}

* La pagina di copyright non viene visualizzata quando si tenta di scaricare più risorse gestite tramite diritti . (CQ-4314403)
* Quando si sceglie di modificare un file INDD, la risoluzione cambia in modo imprevisto. (CQ-4317376)
* Nella rappresentazione di PDF è presente solo l’ultima pagina del modello di InDesign. (CQ-4317305)
* L’apertura del selettore tag richiede molto tempo quando il selettore fa parte di uno schema di metadati complesso. (CQ-4316426)
* Quando si carica una risorsa con lo stesso nome file di una esistente, la finestra di dialogo del conflitto dei nomi non viene visualizzata per richiedere all’utente di creare una versione. (CQ-4315424)
* Le proprietà dei metadati della cartella possono essere impostate e salvate dal menu a comparsa nella pagina Proprietà di una cartella. Mentre la selezione viene salvata nell’archivio, non viene visualizzata quando le Proprietà metadati cartella vengono aperte nuovamente. (CQ-4314429)
* Le risorse con nomi file contenenti spazi o caratteri speciali vengono caricate utilizzando il browser. (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

AEM Forms ha aiutato molte organizzazioni a fornire esperienze di onboarding e registrazione straordinarie nel corso degli anni. Queste esperienze hanno aiutato le organizzazioni a convertire i lead in vendite, a elaborare i dati dei clienti acquisiti, a fornire esperienze reattive in base al profilo di pubblico e molto altro. Ora AEM Forms è disponibile come servizio cloud.

È possibile utilizzare [AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) per creare moduli digitali, collegare i moduli a origini dati esistenti, integrare i moduli con Adobe Sign per aggiungere firme elettroniche ai moduli, generare documenti di record (DoR) per archiviare i moduli inviati come file PDF. Il servizio può anche convertire i PDF forms esistenti in moduli digitali. Oltre alle funzioni standard di AEM Forms, il servizio offre diverse funzionalità native per il cloud, come il ridimensionamento automatico, tempi di inattività zero per gli aggiornamenti e ambiente di sviluppo nativo per il cloud.

Puoi rivolgerti al tuo rappresentante Adobe per una demo o per iscriverti al servizio.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Supporto per Adobe Commerce 2.4.2

* Il componente dettaglio del prodotto può ora essere utilizzato e configurato in qualsiasi pagina di contenuto

* Sito di riferimento CIF Venia rilasciato: 2021.03.25 che include la versione più recente dei componenti core CIF versione v1.9.0. Fai riferimento a [Sito di riferimento CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25) per ulteriori dettagli.

* Componenti core CIF rilasciati v1.9.0. Fai riferimento a [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) per ulteriori dettagli.


## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.3.0.

## Data di pubblicazione {#release-date-cm-march}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.3.0 è il 11 marzo 2021.
La prossima versione è pianificata per il 08 aprile 2021.

### Novità {#what-is-new-march}

* Ora i clienti con ambienti con configurazioni preesistenti dei nomi di dominio personalizzati per [Elenchi IP consentiti](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [Certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) e [Nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) visualizzano un messaggio relativo alle precedenti configurazioni esistenti e possono intraprendere azioni in modalità self-service tramite l’interfaccia utente.

* Ora gli utenti con le autorizzazioni necessarie possono modificare un programma ed effettuare le seguenti operazioni in modalità self-service:

   * Aggiungere la soluzione Sites a un programma esistente con Assets o viceversa.
   * Rimuovere Sites o Assets da un programma esistente con entrambi Sites e Assets.
   * Aggiungere il secondo diritto inutilizzato di una soluzione a un programma esistente o nuovo.

* **Aggiornamento push AEM** verrà ora visualizzata l’etichetta per entrambi *Esecuzione della pipeline* e *Attività* schermate.

* Ora se un ambiente è in stato di sospensione ma è disponibile un aggiornamento di AEM lo stato **Sospeso** ha la precedenza su **Aggiornamento disponibile**.

* Ora gli utenti possono visualizzare i ruoli di Cloud Manager dall’icona Profilo utente (in alto a destra) di Unified Shell selezionando l’opzione “Visualizza ruoli di Cloud Manager”.

* L’etichetta **Domanda di approvazione** è stata rinominata in **Approvazione produzione** per maggiore chiarezza.

* L’etichetta **Versione** è stata rinominata in **Tag Git** nella schermata di esecuzione della pipeline di produzione.

* Le etichette che definiscono il comportamento quando delle metriche importanti non soddisfano la soglia definita sono state rinominate per rispecchiare il comportamento effettivo: **Annulla immediatamente** e **Approva immediatamente**.

* Gli elenchi di classi e metodi obsoleti sono stati aggiornati in base alla versione `2021.3.4997.20210303T022849Z-210225` dell’SDK di AEM Cloud Service.

* Ora la pipeline di produzione di Cloud Manager include la funzionalità [Test dell’interfaccia utente personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing).

### Correzioni di bug {#bug-fixes-cm-march}

* Il controllo delle versioni del pacchetto veniva ignorato in alcuni casi durante l’aggiornamento push di AEM.

* Alcuni problemi di qualità non venivano rilevati correttamente quando i pacchetti erano incorporati in altri pacchetti.

* In situazioni ignote, il nome predefinito del programma generato all’apertura della finestra di dialogo Aggiungi programma poteva essere un duplicato di un nome di programma esistente.

* A volte, se l’utente si allontanava dalla pagina di esecuzione della pipeline subito dopo aver avviato una pipeline, veniva visualizzato un messaggio di errore indicante che l’azione non era riuscita sebbene l’esecuzione venisse effettivamente avviata.

* La fase di build veniva riavviata inutilmente quando le build del cliente generavano pacchetti non validi.

* In alcuni casi, l’utente visualizzava uno stato verde “attivo” a fianco dell’elenco IP consentiti anche quando tale configurazione non era stata distribuita.

* Ora tutte le pipeline di produzione esistenti sono abilitate automaticamente con il passaggio Audit dell’esperienza.

## Strumento Trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.3.4 è il 19 marzo 2021.

### Correzioni di bug {#bug-fixes-ctt}

* Il CTT saltava il contenuto dalle cartelle con lo stesso nome ma con un trattino nel nome. Questo problema è stato risolto.

### Data di pubblicazione {#release-date-ctt-march}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.3.0 è il 4 marzo 2021.

### Novità nello strumento Content Transfer (Trasferimento contenuti) {#what-is-new-ctt-march}

* Il CTT viene ora installato in `/apps` anziché `/libs` I segnalibri del browser per determinate pagine potrebbero non essere più validi.
* Quando CTT è installato, l’utente dovrà navigare in un livello aggiuntivo per accedere alla pagina Content Transfer (Trasferimento contenuti). Vedi [Utilizzo dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=it) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-ctt-march}

* Durante la migrazione del contenuto da un percorso specifico, CTT effettuava l’estrazione di risorse non correlate. Questo problema è stato risolto.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.8 è il 22 marzo 2021.

### Novità di Best Practices Analyzer {#what-is-new-bpa}

* Possibilità di filtrare i risultati di ACS Commons dal rapporto BPA nell’interfaccia utente e dal rapporto esportato come file CSV.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità degli strumenti di refactoring del codice {#what-is-new-crt}

* Nuove funzioni e miglioramenti per Repository Modernizer. Fai riferimento a [Risorsa GitHub: Modernizzatore dell&#39;archivio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) per la versione più recente.
   * Normalizza le configurazioni OSGi (eccetto le configurazioni RepoInit) al formato .cfg.json preferito.
   * Rinomina le cartelle di configurazione OSGi nel formato specificato.
   * Genera il progetto ui.apps.structure.
   * Crea il modulo di analisi.

* Nuove funzioni e miglioramenti per Dispatcher Converter. Fai riferimento a [Risorsa GitHub: Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * Creazione di file separati per inclusioni diverse invece che nel rivestimento del contenuto.
   * Possibilità di gestire sia il percorso della cartella dei vhosts che il percorso dei file vhost.
   * Generazione di file farm con configurazioni cliente di grandi dimensioni in una gamma di 600 e più.
