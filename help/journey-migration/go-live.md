---
title: Pubblicazione
description: Scopri come eseguire la migrazione quando il codice e il contenuto sono pronti per il cloud
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: 55ecd685afa28226974f3415b550bd2e8d05e2e6
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 2%

---

# Pubblicazione {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Preparazione Go-Live"
>abstract="Per garantire una corretta e corretta esecuzione delle AEM as a Cloud Service, è necessario pianificare i periodi di blocco del codice e del contenuto, le iterazioni di test, i riepiloghi dei contenuti, i test delle prestazioni, i test di sicurezza e altro ancora."

In questa parte del percorso, imparerai a pianificare ed eseguire la migrazione una volta che sia il codice che il contenuto saranno pronti per essere spostati in AEM as a Cloud Service. Inoltre, scoprirai quali sono le best practice e le limitazioni note durante l’esecuzione della migrazione.

## Percorso affrontato finora {#story-so-far}

Nelle fasi precedenti del percorso:

* Hai imparato a iniziare con il passaggio a AEM as a Cloud Service nel [Introduzione](/help/journey-migration/getting-started.md) pagina.
* Determinato se la distribuzione è pronta per essere spostata nel cloud leggendo il [Fase di preparazione](/help/journey-migration/readiness.md)
* Acquisisci familiarità con gli strumenti e il processo attraverso i quali puoi rendere il codice e il cloud di contenuti pronti con il [Fase di implementazione](/help/journey-migration/implementation.md).

## Obiettivo {#objective}

Questo documento illustra come eseguire la migrazione a AEM as a Cloud Service una volta acquisita familiarità con i passaggi precedenti del percorso. Scoprirai come eseguire la migrazione di produzione iniziale e le best practice da seguire per la migrazione a AEM as a Cloud Service.

## Migrazione alla produzione iniziale {#initial-migration}

Prima di eseguire la migrazione della produzione, segui i passaggi di installazione e prova della migrazione descritti in [Strategia e cronologia di migrazione dei contenuti](/help/journey-migration/implementation.md##strategy-timeline) della sezione [Fase di implementazione](/help/journey-migration/implementation.md).

* Avvia la migrazione dalla produzione in base all’esperienza acquisita durante la migrazione del passaggio as a Cloud Service AEM eseguita sui cloni:
   * Autore-autore
   * Publish-Publish

* Convalida il contenuto acquisito nei livelli di authoring e pubblicazione AEM as a Cloud Service.
* Informare il team di authoring dei contenuti per evitare lo spostamento dei contenuti sia nell’origine che nella destinazione fino al completamento dell’acquisizione
* È possibile aggiungere, modificare o eliminare nuovi contenuti, ma non spostarli. Questo vale sia per l&#39;origine che per la destinazione.
* Registrare [tempo impiegato](/help/journey-migration/implementation.md#gathering-data) per l’estrazione e l’acquisizione complete, effettua una stima dei tempi di migrazione futuri per l’integrazione.
* Crea un [pianificazione della migrazione](/help/journey-migration/implementation.md#migration-plan) sia per l’autore che per la pubblicazione.

## Incremental Top-Up {#top-up}

Dopo la migrazione iniziale dalla produzione, è necessario eseguire integrazioni incrementali per assicurarsi che il contenuto venga aggiornato sull’istanza cloud. Per questo motivo, si consiglia di seguire le seguenti best practice:

* Raccogliere dati sulla quantità di contenuto. Ad esempio: per una settimana, due settimane o un mese.
* Pianifica gli integratori in modo da evitare più di 48 ore di estrazione e acquisizione dei contenuti. Questa opzione è consigliata affinché le integrazioni dei contenuti si adattino a un intervallo di tempo del fine settimana.
* Pianifica il numero di integrazioni richieste e utilizza tali stime per pianificare la data del lancio.

## Identificare le timeline di blocco del codice e del contenuto per la migrazione {#code-content-freeze}

Come accennato in precedenza, sarà necessario pianificare un periodo di blocco del codice e del contenuto. Utilizza le seguenti domande per aiutarti a pianificare il periodo di congelamento:

* Per quanto tempo devo congelare le attività di authoring dei contenuti?
* Per quanto tempo devo chiedere al team di consegna di interrompere l’aggiunta di nuove funzioni?

Per rispondere alla prima domanda, è necessario considerare il tempo necessario per eseguire esecuzioni di prova in ambienti non di produzione. Per rispondere alla seconda domanda, è necessaria una stretta collaborazione tra il team che sta aggiungendo nuove funzionalità e il team che sta refactoring il codice. L’obiettivo deve essere quello di assicurarsi che anche tutto il codice aggiunto alla distribuzione esistente venga aggiunto, testato e distribuito al ramo cloud services. In generale, ciò significa che la quantità di congelamento del codice sarà inferiore.

Inoltre, è necessario pianificare il blocco dei contenuti quando l’integrazione del contenuto finale è pianificata.

## Best practice   {#best-practices}

Quando pianifichi o esegui la migrazione, prendi in considerazione le seguenti linee guida:

* Migrazione da Author a Author e pubblicazione a Publish
* Richiedi un clone di produzione che può essere utilizzato per:
   * Acquisire le statistiche del repository
   * Prova delle attività di migrazione
   * Preparare il piano di migrazione
   * Identificare i requisiti di blocco dei contenuti
   * Identifica eventuali esigenze di upsize sulla produzione durante la migrazione dalla produzione

**Best practice per lo strumento Content Transfer (Trasferimento contenuti)**

Assicurati di eseguire la migrazione dei contenuti in produzione al posto di un clone quando vai in onda. Un buon approccio è quello di utilizzare [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) per la migrazione iniziale, quindi esegui spesso le estrazioni di alto livello (anche quotidianamente) per estrarre blocchi più piccoli ed evitare un carico a lungo termine sul AEM sorgente.

Durante la migrazione di produzione, evita di eseguire lo strumento Content Transfer (Trasferimento contenuti) da un clone perché:

* Se un cliente richiede la migrazione delle versioni di contenuto durante le migrazioni degli integratori, l’esecuzione dello strumento Content Transfer (Trasferimento contenuti) da un clone non esegue la migrazione delle versioni. Anche se il clone viene ricreato frequentemente dall’autore live, ogni volta che viene creato un clone i punti di controllo che verranno utilizzati dallo strumento Content Transfer (Trasferimento contenuti) per calcolare i delta vengono reimpostati.
* Poiché un clone non può essere aggiornato nel suo insieme, il pacchetto ACL Query deve essere utilizzato per creare un pacchetto e installare il contenuto aggiunto o modificato dalla produzione al clone. Il problema con questo approccio è che qualsiasi contenuto eliminato sull&#39;istanza sorgente non arriverà mai al clone a meno che non venga eliminato manualmente sia dall&#39;origine che dal clone. Questo introduce la possibilità che il contenuto eliminato in produzione non venga eliminato sul clone e AEM as a Cloud Service.

**Ottimizzazione del carico sulla sorgente AEM durante l’esecuzione della migrazione dei contenuti**

Ricorda che il carico sulla sorgente AEM sarà maggiore durante la fase di estrazione. È necessario tenere presente che:

* Lo strumento Content Transfer (Trasferimento contenuti) è un processo Java esterno che utilizza un heap JVM di 4 GB
* La versione non-AzCopy scarica i file binari, li memorizza in uno spazio temporaneo sull’autore dell’AEM di origine, consuma l’I/O del disco, quindi li carica nel contenitore Azure che consuma la larghezza di banda della rete
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) trasferisce i BLOB direttamente dall’archivio BLOB al contenitore Azure, che salva l’I/O del disco e la larghezza di banda della rete. La versione AzCopy utilizza ancora il disco e la larghezza di banda di rete per estrarre e caricare i dati dall’archivio segmenti nel contenitore Azure
* Il processo dello strumento Content Transfer (Trasferimento contenuti) è più leggero sulle risorse di sistema durante la fase di acquisizione, in quanto esegue lo streaming dei registri di acquisizione e non vi è molto carico sull&#39;istanza sorgente per quanto riguarda l&#39;I/O del disco o la larghezza di banda della rete.

## Limitazioni note {#known-limitations}

Tieni presente che l’intera acquisizione non riesce se nel set di migrazione estratto sono presenti le seguenti limitazioni:

* Un nodo JCR con un nome più lungo di 150 caratteri
* Un nodo JCR più grande di 16 MB
* Qualsiasi utente/gruppo con `rep:AuthorizableID` acquisizione già presente in AEM as a Cloud Service
* Se una risorsa estratta e assimilata si sposta in un percorso diverso sia sull’origine che sulla destinazione prima della successiva iterazione della migrazione.

## Salute risorse {#asset-health}

Rispetto alla sezione precedente l’acquisizione **non** fallire a causa dei seguenti problemi di asset. Tuttavia, si consiglia vivamente di adottare le misure appropriate in questi scenari:

* Qualsiasi risorsa con rendering originale mancante
* Qualsiasi cartella che presenta una cartella mancante `jcr:content` nodo

Entrambi gli elementi di cui sopra saranno identificati e segnalati nella [Best practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) rapporto.

## Lista di controllo per la pubblicazione {#Go-Live-Checklist}

Controlla questo elenco di attività per assicurarti di eseguire una migrazione fluida e corretta.

* Esegui una pipeline di produzione end-to-end con test funzionali e dell’interfaccia utente per garantire un **sempre corrente** AEM esperienza di prodotto. Consulta le risorse seguenti.
   * [Aggiornamenti della versione di AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Test funzionali personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Test dell’interfaccia utente](/help/implementing/cloud-manager/ui-testing.md)
* Esegui la migrazione dei contenuti in produzione e assicurati che un sottoinsieme pertinente sia disponibile nella fase di staging per il test.
   * Tieni presente che le best practice DevOps per AEM implicano che il codice passi dallo sviluppo all’ambiente di produzione mentre il contenuto si sposta dagli ambienti di produzione.
* Pianifica un periodo di blocco del codice e del contenuto.
   * Vedi anche la sezione [Timeline per la migrazione a blocchi di codice e contenuti](#code-content-freeze)
* Esegui l’integrazione del contenuto finale.
* Convalida le configurazioni del dispatcher.
   * Utilizza una convalida del dispatcher locale che facilita la configurazione, la convalida e la simulazione locale del dispatcher
      * [Imposta gli strumenti del dispatcher locale.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)
   * Esamina attentamente la configurazione dell&#39;host virtuale.
      * La soluzione più semplice (e predefinita) è quella di includere `ServerAlias *` nel file host virtuale nel `/dispatcher/src/conf.d/available_vhostsfolder`.
         * In questo modo gli alias host utilizzati dai test funzionali del prodotto, dall’annullamento della validità della cache del dispatcher e dai duplicati funzioneranno.
      * Tuttavia, se `ServerAlias *` non è accettabile, almeno quanto segue `ServerAlias` oltre ai domini personalizzati, le voci devono essere consentite:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Configura CDN, SSL e DNS.
   * Se utilizzi una rete CDN personalizzata, inserisci un ticket di supporto per configurare l’indirizzamento appropriato.
      * Vedi la sezione [CDN cliente punta a AEM CDN gestito](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) nella documentazione CDN per ulteriori informazioni.
      * Sarà necessario configurare SSL e DNS in base alla documentazione del fornitore CDN.
   * Se non utilizzi un CDN aggiuntivo, gestisci SSL e DNS in base alla documentazione seguente:
      * Gestione dei certificati SSL
         * [Introduzione alla gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [Gestione del certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Gestione dei nomi di dominio personalizzati (DNS)
         * Per assicurarti che il cutover DNS non presenti problemi imprevisti, è consigliabile creare un sottodominio di prova a cui collegare l’istanza di produzione prima di iniziare il ciclo di vita e di eseguire un ciclo di test UAT. Quindi se il tuo dominio è example.com, puoi creare un sottodominio test.example.com e applicarlo alla produzione. Durante il test UAT del dominio dovrai cercare cose come il corretto reindirizzamento dei collegamenti, la memorizzazione in cache e le configurazioni del dispatcher.
         * [Introduzione ai nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Gestione del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Ricorda di convalidare il set TTL per il record DNS.
      * Il TTL è il tempo in cui un record DNS rimane in una cache prima di richiedere un aggiornamento al server.
      * Se si dispone di un TTL molto alto, gli aggiornamenti al record DNS richiederanno più tempo per propagarsi.
* Esegui test di prestazioni e sicurezza che soddisfino i requisiti e gli obiettivi aziendali.
* Effettua i passaggi e assicurati che l’effettivo live sia eseguito senza alcuna nuova distribuzione o aggiornamento del contenuto.
* Crea ad Admin Console profili di notifica utente. Vedi [Profili di notifica](/help/journey-onboarding/notification-profiles.md)

È sempre possibile fare riferimento all’elenco nel caso in cui sia necessario ricalibrare le attività durante l’esecuzione della migrazione.

## Passaggio successivo {#what-is-next}

Dopo aver compreso come eseguire la migrazione a AEM as a Cloud Service, puoi controllare la [Post-Go-Live](/help/journey-migration/post-go-live.md) per mantenere l’istanza in esecuzione senza problemi.
