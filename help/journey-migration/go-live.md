---
title: Pubblicazione
description: Scopri come eseguire la migrazione una volta che il codice e il contenuto sono pronti per il cloud
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: 7f43e09c411b0402701b5c65639ca988702ab75e
workflow-type: tm+mt
source-wordcount: '1729'
ht-degree: 2%

---

# Pubblicazione {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Preparazione Go-Live"
>abstract="Per garantire una pubblicazione corretta e senza problemi su AEM as a Cloud Service, è necessario pianificare periodi di blocco del codice e dei contenuti, iterazioni di test, integrazioni di contenuti, test delle prestazioni, test di sicurezza e altro ancora."

In questa sezione del percorso imparerai a pianificare ed eseguire la migrazione una volta che il codice e il contenuto saranno pronti per essere trasferiti a AEM as a Cloud Service. Inoltre, scoprirai quali sono le best practice e le limitazioni note durante l’esecuzione della migrazione.

## Percorso affrontato finora {#story-so-far}

Nelle fasi precedenti del percorso:

* Hai imparato come iniziare il passaggio all’AEM as a Cloud Service nel [Guida introduttiva](/help/journey-migration/getting-started.md) pagina.
* Determinato se la distribuzione è pronta per essere spostata nel cloud leggendo il [Fase di preparazione](/help/journey-migration/readiness.md)
* Acquisisci familiarità con gli strumenti e i processi attraverso i quali puoi preparare il codice e il cloud di contenuti con [Fase di implementazione](/help/journey-migration/implementation.md).

## Obiettivo {#objective}

Questo documento ti aiuterà a capire come eseguire la migrazione a AEM as a Cloud Service una volta acquisite familiarità con i passaggi precedenti del percorso. Scoprirai come eseguire la migrazione di produzione iniziale e le best practice da seguire per la migrazione a AEM as a Cloud Service.

## Migrazione iniziale alla produzione {#initial-migration}

Prima di eseguire la migrazione di produzione, segui i passaggi di installazione e verifica della migrazione descritti in [Strategia e tempistica di migrazione dei contenuti](/help/journey-migration/implementation.md##strategy-timeline) sezione del [Fase di implementazione](/help/journey-migration/implementation.md).

* Avvia la migrazione dalla produzione in base all’esperienza acquisita durante la fase di migrazione AEM as a Cloud Service eseguita sui cloni:
   * Autore-Autore
   * Publish-Publish

* Convalida i contenuti acquisiti sia nel livello di authoring che in quello di pubblicazione as a Cloud Service dall’AEM.
* Chiedi al team di authoring dei contenuti di evitare di spostare i contenuti sia sull’origine che sulla destinazione fino al completamento dell’acquisizione
* È possibile aggiungere, modificare o eliminare nuovi contenuti, ma non spostarli. Questo vale sia per l’origine che per la destinazione.
* Registra il [tempo impiegato](/help/journey-migration/implementation.md#gathering-data) per l’estrazione e l’acquisizione complete, avere una stima dei futuri tempi di migrazione di integrazione.
* Creare un [pianificazione della migrazione](/help/journey-migration/implementation.md#migration-plan) sia per Author che per Publish.

## Top-up incrementali {#top-up}

Dopo la migrazione iniziale dalla produzione, è necessario eseguire integrazioni incrementali per assicurarsi che i contenuti vengano aggiornati nell’istanza cloud. Per questo motivo, si consiglia di seguire le seguenti best practice:

* Raccogliere dati sulla quantità di contenuto. Ad esempio: una settimana, due settimane o un mese.
* Assicurati di pianificare le integrazioni in modo da evitare più di 48 ore di estrazione e acquisizione dei contenuti. Questa opzione è consigliata in modo che i contenuti aggiuntivi rientrino in un intervallo di tempo del fine settimana.
* Pianifica il numero di integrazioni necessarie e utilizza tali stime per pianificare la data di lancio.

## Identificare i tempi di blocco del codice e del contenuto per la migrazione {#code-content-freeze}

Come accennato in precedenza, dovrai pianificare un periodo di blocco del codice e dei contenuti. Utilizza le seguenti domande per pianificare il periodo di blocco:

* Quanto tempo è necessario per bloccare le attività di authoring dei contenuti?
* Per quanto tempo devo chiedere al mio team di consegna di interrompere l’aggiunta di nuove funzioni?

Per rispondere alla prima domanda, è necessario considerare il tempo necessario per eseguire le esecuzioni di prova in ambienti non di produzione. Per rispondere alla seconda domanda, è necessaria una stretta collaborazione tra il team che aggiunge nuove funzionalità e il team che refactoring del codice. L’obiettivo dovrebbe essere garantire che tutto il codice aggiunto alla distribuzione esistente venga aggiunto, testato e distribuito anche nel ramo dei servizi cloud. In generale, ciò significa che la quantità di codice bloccato sarà inferiore.

Inoltre, è necessario pianificare un blocco dei contenuti quando è pianificato l’aggiornamento finale dei contenuti.

## Best practice   {#best-practices}

Quando pianifichi o esegui la migrazione, prendi in considerazione le seguenti linee guida:

* Migrare da Author a Author e Publish a Publish
* Richiedi un clone di produzione che può essere utilizzato per:
   * Acquisire le statistiche dell’archivio
   * Prova delle attività di migrazione
   * Preparare il piano di migrazione
   * Identificazione dei requisiti di blocco dei contenuti
   * Identifica eventuali esigenze di upsize sulla produzione durante la migrazione dalla produzione

**Best practice per lo strumento Content Transfer (Trasferimento contenuti)**

Assicurati di eseguire la migrazione dei contenuti in produzione invece di clonare quando vai live. Un buon approccio è quello di utilizzare [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) per la migrazione iniziale e quindi eseguire frequentemente estrazioni integrative (anche quotidianamente) per estrarre blocchi più piccoli ed evitare un carico a lungo termine sull’AEM di origine.

Durante l’esecuzione della migrazione di produzione, è necessario evitare di eseguire lo strumento Content Transfer (Trasferimento contenuti) da un clone perché:

* Se un cliente richiede la migrazione delle versioni dei contenuti durante le migrazioni integrative, l’esecuzione dello strumento Content Transfer (Trasferimento contenuti) da un clone non esegue la migrazione delle versioni. Anche se il clone viene ricreato frequentemente dall’autore live, ogni volta che viene creato un clone vengono ripristinati i punti di controllo che verranno utilizzati dallo strumento Content Transfer (Trasferimento contenuti) per calcolare i delta.
* Poiché un clone non può essere aggiornato nel suo insieme, il pacchetto di query ACL deve essere utilizzato per creare un pacchetto e installare il contenuto aggiunto o modificato dalla produzione al clone. Il problema di questo approccio è che qualsiasi contenuto eliminato nell’istanza sorgente non arriverà mai al clone a meno che non venga eliminato manualmente sia dall’origine che dal clone. Questo introduce la possibilità che i contenuti eliminati in produzione non vengano eliminati sul clone e sull’AEM as a Cloud Service.

**Ottimizzazione del carico sull’origine AEM durante l’esecuzione della migrazione dei contenuti**

Ricorda che il carico sulla sorgente dell’AEM sarà maggiore durante la fase di estrazione. Tieni presente che:

* Lo strumento Content Transfer (Trasferimento contenuti) è un processo Java esterno che utilizza un heap JVM di 4 GB
* La versione non AzCopy scarica i file binari, li memorizza in uno spazio temporaneo nell’autore AEM di origine, consumando I/O del disco, quindi carica nel contenitore Azure che consuma la larghezza di banda della rete
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) trasferisce i BLOB direttamente dall’archivio BLOB al contenitore Azure, consentendo di salvare l’I/O del disco e la larghezza di banda della rete. La versione di AzCopy utilizza ancora la larghezza di banda del disco e della rete per estrarre e caricare i dati dall’archivio segmenti nel contenitore di Azure
* Il processo dello strumento Content Transfer (Trasferimento contenuti) è più leggero per le risorse di sistema durante la fase di acquisizione, in quanto esegue lo streaming dei registri di acquisizione e l’istanza sorgente non ha un carico elevato per quanto riguarda l’I/O del disco o la larghezza di banda della rete.

## Limitazioni note {#known-limitations}

Tieni presente che l’intera acquisizione non riesce se una qualsiasi delle seguenti limitazioni viene trovata come parte del set di migrazione estratto:

* Un nodo JCR con un nome che supera i 150 caratteri
* Un nodo JCR di dimensioni superiori a 16 MB
* Qualsiasi utente/gruppo con `rep:AuthorizableID` in fase di acquisizione, già presente nell’AEM as a Cloud Service
* Se una risorsa estratta e acquisita viene spostata in un percorso diverso nell’origine o nella destinazione prima della successiva iterazione della migrazione.

## Integrità risorsa {#asset-health}

Rispetto alla sezione precedente l’acquisizione **non** non riesce a causa dei seguenti problemi relativi alle risorse. Tuttavia, si consiglia vivamente di adottare le misure appropriate in questi scenari:

* Qualsiasi risorsa con la rappresentazione originale mancante
* Qualsiasi cartella con un `jcr:content` nodo

Entrambi gli elementi di cui sopra saranno identificati e segnalati nella [Best Practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) rapporto.

## Elenco di controllo per la pubblicazione {#Go-Live-Checklist}

Rivedi questo elenco di attività per assicurarti di eseguire una migrazione fluida e corretta.

* Esegui una pipeline di produzione end-to-end con test funzionali e dell’interfaccia utente per garantire un’ **sempre corrente** Esperienza con prodotti AEM. Consulta le risorse seguenti.
   * [Aggiornamenti della versione di AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Test funzionali personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Test dell’interfaccia utente](/help/implementing/cloud-manager/ui-testing.md)
* Migra i contenuti alla produzione e assicurati che un sottoinsieme rilevante sia disponibile nell’area di staging per il test.
   * Tieni presente che le best practice per DevOps per AEM implicano che il codice passi dallo sviluppo all’ambiente di produzione, mentre il contenuto si sposta dagli ambienti di produzione.
* Pianifica un periodo di blocco del codice e dei contenuti.
   * Vedi anche la sezione [Timeline di blocco del codice e dei contenuti per la migrazione](#code-content-freeze)
* Eseguire l’integrazione del contenuto finale.
* Convalida le configurazioni del dispatcher.
   * Utilizza una funzione di convalida del dispatcher locale che semplifica la configurazione, la convalida e la simulazione locale del dispatcher
      * [Configura gli strumenti del dispatcher locale.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)
   * Esaminare attentamente la configurazione dell&#39;host virtuale.
      * La soluzione più semplice (e predefinita) consiste nell’includere `ServerAlias *` nel file host virtuale in `/dispatcher/src/conf.d/available_vhostsfolder`.
         * In questo modo, gli alias host utilizzati dai test funzionali del prodotto, l’invalidazione della cache del dispatcher e i cloni funzioneranno.
      * Tuttavia, se `ServerAlias *` non è accettabile, almeno quanto segue `ServerAlias` le voci devono essere consentite in aggiunta ai domini personalizzati:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Configurare CDN, SSL e DNS.
   * Se utilizzi una tua rete CDN, inserisci un ticket di supporto per configurare il routing appropriato.
      * Consulta la sezione [La rete CDN del cliente punta alla rete CDN gestita dall’AEM](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) nella documentazione della rete CDN per ulteriori dettagli.
      * Dovrai configurare SSL e DNS in base alla documentazione del fornitore CDN.
   * Se non utilizzi una rete CDN aggiuntiva, gestisci SSL e DNS come descritto nella seguente documentazione:
      * Gestione dei certificati SSL
         * [Introduzione alla gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [Gestione del certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Gestione dei nomi di dominio personalizzati (DNS)
         * Per evitare che il cutover DNS introduca problemi imprevisti, è consigliabile creare un sottodominio di test a cui connettere l’istanza di produzione prima di andare &quot;live&quot; ed eseguire un ciclo di test UAT. Pertanto, se il tuo dominio è example.com, puoi creare un sottodominio test.example.com e applicarlo alla produzione. Durante il test UAT del dominio, dovrai cercare elementi come il reindirizzamento corretto dei collegamenti, la memorizzazione in cache e le configurazioni del dispatcher.
         * [Introduzione ai nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Gestione del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Ricorda di convalidare il TTL impostato per il record DNS.
      * Il TTL è il periodo di tempo in cui un record DNS rimane nella cache prima di richiedere un aggiornamento al server.
      * Se il TTL è molto alto, la propagazione degli aggiornamenti al record DNS richiederà più tempo.
* Eseguire test di prestazioni e sicurezza che soddisfino i requisiti e gli obiettivi aziendali.
* Esamina il passaggio e assicurati che il lancio effettivo venga eseguito senza alcuna nuova distribuzione o aggiornamento del contenuto.
* Creazione di gruppi di notifica per utenti Admin Console. Consulta [Gruppi di utenti per le notifiche](/help/journey-onboarding/user-groups.md)

Puoi sempre fare riferimento all’elenco nel caso in cui sia necessario ricalibrare le attività durante l’esecuzione della migrazione.

## Passaggio successivo {#what-is-next}

Una volta compreso come eseguire la migrazione a AEM as a Cloud Service, puoi controllare il [Post-pubblicazione](/help/journey-migration/post-go-live.md) per garantire il corretto funzionamento dell’istanza.
