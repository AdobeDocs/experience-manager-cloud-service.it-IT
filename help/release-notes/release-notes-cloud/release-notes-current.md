---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
translation-type: tm+mt
source-git-commit: baa9f84e8a32bbfdfa6717225fb706ea81b94e06
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 3%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] come Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] come Cloud Service.

>[!NOTE]
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Per informazioni sugli aggiornamenti della documentazione non direttamente correlati a una versione, consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) .

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] come Cloud Service 2021.3.0 è il 25 marzo 2021.
La versione seguente (2021.4.0) sarà del 29 aprile 2021.

## [!DNL Adobe Experience Manager Sites] come Cloud Service  {#sites}

* [È ora possibile abilitare a livello di progetto la versione Progressive Web App (PWA) di un ](/help/sites-cloud/authoring/features/enable-pwa.md) sito tramite una configurazione semplice.
* Estensioni del modello per frammenti di contenuto : ora è possibile definire tipi di dati di testo con più righe come elenchi a più campi.
* Miglioramenti dell’interfaccia utente dell’Editor frammenti di contenuto : i frammenti secondari nidificati vengono ora visualizzati nella breadcrumb e viene migliorata la visualizzazione delle azioni di pubblicazione, salvataggio e salvataggio/uscita

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] estende la funzionalità Risorse collegate per supportare l’utilizzo di  [!DNL Dynamic Media] immagini nei componenti core supportati. Consulta [Utilizzare le risorse collegate](/help/assets/use-assets-across-connected-assets-instances.md).
* Gli amministratori di Experience Manager possono pianificare l’inserimento di risorse in blocco in una data o un’ora specifica. Inoltre, gli amministratori possono pianificare acquisizioni ricorrenti in base a data e ora. Consulta [inserimento di risorse in blocco](/help/assets/add-assets.md#asset-bulk-ingestor).

### Correzioni di bug in [!DNL Assets] {#bug-fixes-assets}

* La pagina di copyright non viene visualizzata quando si tenta di scaricare più risorse gestite tramite diritti . (CQ-4314403)
* Quando si sceglie di modificare un file INDD, la risoluzione cambia in modo imprevisto. (CQ-4317376)
* Nella rappresentazione PDF è presente solo l’ultima pagina del modello InDesign. (CQ-4317305)
* L’apertura del selettore tag richiede molto tempo quando il selettore fa parte di uno schema di metadati complesso. (CQ-4316426)
* Quando si carica una risorsa con lo stesso nome file di una esistente, la finestra di dialogo del conflitto dei nomi non viene visualizzata per richiedere all’utente di creare una versione. (CQ-4315424)
* Le proprietà dei metadati della cartella possono essere impostate e salvate dal menu a comparsa nella pagina Proprietà di una cartella. Mentre la selezione viene salvata nell’archivio, non viene visualizzata quando le Proprietà metadati cartella vengono aperte nuovamente. (CQ-4314429)
* Le risorse con nomi file contenenti spazi o caratteri speciali vengono caricate utilizzando il browser. (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] come  [!DNL Cloud Service] {#forms}

AEM Forms ha aiutato molte organizzazioni a fornire esperienze di onboarding e registrazione straordinarie nel corso degli anni. Queste esperienze hanno aiutato le organizzazioni a convertire i lead in vendite, a elaborare i dati dei clienti acquisiti, a fornire esperienze reattive in base al profilo di pubblico e molto altro. Ora AEM Forms è disponibile come servizio cloud.

È possibile utilizzare [AEM Forms come Cloud Service](https://experienceleague.corp.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) per creare moduli digitali, collegare moduli a origini dati esistenti, integrare moduli con Adobe Sign per aggiungere firme elettroniche ai moduli, generare documenti di record (DoR) per archiviare i moduli inviati come file PDF. Il servizio può anche convertire i PDF forms esistenti in moduli digitali. Oltre alle funzioni standard di AEM Forms, il servizio offre diverse funzionalità native per il cloud, come il ridimensionamento automatico, tempi di inattività zero per gli aggiornamenti e ambiente di sviluppo nativo per il cloud. Leggi [questo post di blog](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html) per scoprire le funzionalità e le funzionalità di AEM Forms as a Cloud Service.

Puoi rivolgerti al tuo rappresentante Adobe per una demo o per iscriverti al servizio.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Supporto per Magenti 2.4.2

* Il componente dettaglio del prodotto può ora essere utilizzato e configurato in qualsiasi pagina di contenuto

* È stato rilasciato il sito di riferimento CIF Venia - 2021.03.25 che include la versione più recente dei componenti core CIF versione v1.9.0. Per ulteriori informazioni, consulta [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25) .

* È stata rilasciata la versione 1.9.0 dei componenti core CIF. Per ulteriori informazioni, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) .


## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione per Cloud Manager in AEM as a Cloud Service 2021.4.0 e 2021.3.0.

### Data di rilascio {#release-date-cm-april}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.4.0 è l’8 aprile 2021.
La prossima versione è prevista per il 6 maggio 2021.

### Novità {#what-is-new-april}

* L’interfaccia utente è aggiornata ai flussi di lavoro Aggiungi e Modifica programma per renderlo più intuitivo.

* Un utente con le autorizzazioni necessarie può ora inviare l’endpoint di e-commerce tramite l’interfaccia utente di .

* Le variabili di ambiente possono ora essere indirizzate a un servizio specifico, sia per l’authoring che per la pubblicazione. Richiede AEM versione `2021.03.5104.20210328T185548Z` o successiva.

* Il pulsante **Manage Git** viene visualizzato sulla scheda Pipelines anche quando non è stata configurata alcuna pipeline.

* La versione dell’archetipo di progetto AEM utilizzato da Cloud Manager è stata aggiornata alla versione 27.

* I progetti nella Console per sviluppatori di Adobe I/O creata da Cloud Manager non possono più essere modificati o eliminati accidentalmente.

* Quando un utente aggiunge un nuovo ambiente, viene informato che una volta creato l’ambiente non può essere spostato in un’area diversa.

* Le variabili di ambiente possono ora essere indirizzate a un servizio specifico, sia per l’authoring che per la pubblicazione. Richiede AEM versione 2021.03.5104.20210328T185548Z o superiore.

* È stato chiarito il messaggio di errore durante l’avvio di una pipeline quando un ambiente è stato eliminato.

* I bundle OSGi forniti dai progetti Eclipse ora sono esclusi dalla regola `CQBP-84--dependencies`.

### Correzioni di bug {#bug-fixes-cm-april}

* Quando modifichi la pagina di audit esperienza di una pipeline, un percorso di input che inizia con una barra `( / )` non bloccherà più il passaggio nello stato in sospeso.

* Quando viene creata una nuova pipeline di produzione, se l’utente non aggiunge alcuna sostituzione di controllo del contenuto, la pagina home predefinita non è stata sottoposta a controllo.

* I problemi relativi alla `CloudServiceIncompatibleWorkflowProcess` presentavano una gravità errata nel file CSV del problema scaricabile.

* Il controllo `Runmode` produceva falsi positivi sui nodi non presenti nelle cartelle.


### Data di rilascio {#release-date-cm-march}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.3.0 è l’11 marzo 2021.

### Novità {#what-is-new-march}

* I clienti con ambienti con configurazioni di nomi di dominio personalizzati preesistenti per [Elenchi consentiti IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn), [Certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn) e [Nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) visualizzeranno un messaggio sulle configurazioni esistenti in precedenza e saranno in grado di self-service tramite l&#39;interfaccia utente.

* Gli utenti con le autorizzazioni necessarie possono ora modificare un programma, consentendo loro di effettuare le seguenti operazioni in modalità self-service:

   * Aggiungi la soluzione Sites a un programma esistente con Assets o viceversa.
   * Rimuovi Sites o Assets da un programma esistente sia con Sites che con Assets.
   * Aggiungi il secondo diritto inutilizzato alla soluzione a un programma esistente o a un nuovo programma.

* **AEM push** Updatelabel verrà ora visualizzato sia per gli schermi  *Pipeline* Execution che per  ** Activityscreens.

* Se un ambiente è in ibernazione ma è disponibile anche un aggiornamento AEM, lo stato **Sospeso** avrà la precedenza su **Aggiorna disponibile**.

* Gli utenti possono ora visualizzare i propri ruoli di Cloud Manager selezionando l’opzione &quot;Visualizza ruoli Cloud Manager&quot; dopo aver visualizzato l’icona Profilo utente (in alto a destra) di Unified Shell.

* L&#39;etichetta **Domanda di approvazione** è stata rinominata **Approvazione produzione** per una maggiore chiarezza.

* L’etichetta **Versione** è stata rinominata **Tag Git** nella schermata di esecuzione della pipeline di produzione.

* Le etichette che definiscono il comportamento quando metriche importanti non soddisfano la soglia definita sono state rinominate per rispecchiare il loro comportamento effettivo: **Annulla immediatamente** e **Approva immediatamente**.

* Gli elenchi di elementi obsoleti di classi e metodi sono stati aggiornati in base alla versione `2021.3.4997.20210303T022849Z-210225` dell’SDK del Cloud Service AEM.

* La pipeline di produzione di Cloud Manager ora include la funzionalità [Test personalizzati dell’interfaccia utente](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) .

### Correzioni di bug {#bug-fixes-cm-march}

* Il controllo delle versioni del pacchetto è stato ignorato in alcuni casi durante AEM aggiornamento push.

* Alcuni problemi di qualità non sono stati rilevati correttamente quando i pacchetti sono stati incorporati in altri pacchetti.

* In situazioni oscure, il nome predefinito del programma generato all’apertura della finestra di dialogo Aggiungi programma potrebbe essere un duplicato di un nome di programma esistente.

* Talvolta, se l’utente si allontana dalla pagina di esecuzione della pipeline immediatamente dopo l’avvio di una pipeline, viene visualizzato un messaggio di errore che indica che l’azione non è riuscita, anche se l’esecuzione viene effettivamente avviata.

* Il passaggio di compilazione è stato riavviato inutilmente quando le build del cliente hanno generato pacchetti non validi.

* In alcuni casi, l’utente potrebbe visualizzare uno stato verde &quot;attivo&quot; accanto a un Inserire nell&#39;elenco Consentiti IP anche quando tale configurazione non è stata distribuita.

* Tutte le pipeline di produzione esistenti verranno abilitate automaticamente con il passaggio Audit esperienze .

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

### Data di rilascio {#release-date-ctt-april}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.3.8 è il 15 aprile 2021.

### Correzioni di bug {#bug-fixes-ctt-april}

* Il CTT non stava creando rappresentazioni di testo per le risorse. Quando le risorse vengono migrate al Cloud Service, sono necessarie rappresentazioni di testo per consentire la ricerca in base al contenuto di testo. Questo problema è stato risolto.

* Il CTT con wipe=true causava un indice di contatore errato nell&#39;istanza del Cloud Service di destinazione. Questo problema è stato risolto.

* La funzione di aggiornamento automatico nell’interfaccia CTT causava diversi bug. Questi problemi sono stati risolti.

* Le intestazioni di testo nell’interfaccia utente CTT si sovrapponevano. Questo problema è stato risolto.


### Data di rilascio {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.3.4 è il 19 marzo 2021.

### Correzioni di bug {#bug-fixes-ctt}

* Il CTT saltava il contenuto dalle cartelle con lo stesso nome ma con un trattino nel nome. Questo problema è stato risolto.

### Data di rilascio {#release-date-ctt-march}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.3.0 è il 4 marzo 2021.

### Novità nello strumento Content Transfer (Trasferimento contenuti) {#what-is-new-ctt-march}

* CTT ora viene installato su `/apps` invece di `/libs` I segnalibri del browser in alcune pagine potrebbero non essere più validi.
* Quando CTT è installato, l’utente dovrà navigare in un livello aggiuntivo per accedere alla pagina Content Transfer (Trasferimento contenuti). Per ulteriori informazioni, consulta [Utilizzo dello strumento Content Transfer (Trasferimento contenuti)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html) .

### Correzioni di bug {#bug-fixes-ctt-march}

* Durante la migrazione del contenuto da un percorso specifico, CTT effettuava l’estrazione di risorse non correlate. È stato corretto

## Analisi delle best practice {#best-practices-analyzer}

### Data di rilascio {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.12 è il 12 aprile 2021.

### Correzioni di bug {#bug-fixes-bpa-april}

* Sono state visualizzate righe duplicate nel BPA segnalato. Questo problema è stato risolto.
* L’interfaccia utente BPA sulla versione 6.4.2 AEM generava un errore JS che disattivava il pulsante Genera report . È stato corretto


## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità degli strumenti di refactoring del codice {#what-is-new-crt}

* Nuove funzioni e miglioramenti per Repository Modernizer. Fai riferimento a [Risorsa GitHub: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) per la versione più recente.
   * Normalizza le configurazioni OSGi (eccetto le configurazioni RepoInit) al formato .cfg.json preferito.
   * Rinomina le cartelle di configurazione OSGi nel formato specificato.
   * Genera il progetto ui.apps.structure.
   * Crea il modulo di analisi.

* Nuove funzioni e miglioramenti per Dispatcher Converter. Fai riferimento a [Risorsa GitHub: Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * Creazione di file separati per inclusioni diverse invece che nel rivestimento del contenuto.
   * Possibilità di gestire sia il percorso della cartella dei vhosts che il percorso dei file vhost.
   * Generazione di file farm con configurazioni cliente di grandi dimensioni in una gamma di 600 e più.
