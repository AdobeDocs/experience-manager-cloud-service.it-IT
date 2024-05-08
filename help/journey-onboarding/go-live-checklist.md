---
title: Elenco di controllo per la pubblicazione
description: Scopri tutti gli elementi che devono essere presenti per consentire una pubblicazione di successo con gli as a Cloud Service AEM
source-git-commit: 4a03e2fe3519fd9e0d8d646526ea6c9cc6637f52
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 6%

---


# Elenco di controllo per la pubblicazione {#Go-Live-Checklist}

Rivedi questo elenco di attività per assicurarti di eseguire un lancio senza intoppi e di successo.

* Esegui una pipeline di produzione end-to-end con test funzionali e dell’interfaccia utente per garantire un’ **sempre corrente** Esperienza con prodotti AEM. Consulta le risorse seguenti.
   * [Aggiornamenti della versione di AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Test funzionali personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Test dell’interfaccia utente](/help/implementing/cloud-manager/ui-testing.md)
* Se stai eseguendo la migrazione da AEM 6.5, devi migrare i contenuti alla produzione e assicurarti che un sottoinsieme rilevante sia disponibile nella staging per il test.
   * Le best practice per i DevOps per l’AEM implicano che il codice passi dallo sviluppo all’ambiente di produzione, mentre il contenuto scende dagli ambienti di produzione.
* Pianifica un periodo di blocco del codice e dei contenuti.
   * Vedi anche la sezione [Timeline di blocco del codice e dei contenuti per la migrazione](#code-content-freeze)
* Eseguire l’integrazione del contenuto finale.
* Convalida le configurazioni del dispatcher.
   * Utilizza una funzione di convalida del dispatcher locale che semplifica la configurazione, la convalida e la simulazione locale del dispatcher
      * [Configura gli strumenti del dispatcher locale.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html#prerequisites)
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
      * Configura SSL e DNS in base alla documentazione del fornitore CDN.
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
   * Esecuzione di test nell&#39;ambiente stage.  Ha le stesse dimensioni della produzione.
   * Gli ambienti di sviluppo non hanno le stesse dimensioni di stage e produzione.
* Esamina il passaggio e assicurati che il lancio effettivo venga eseguito senza alcuna nuova distribuzione o aggiornamento del contenuto.
* Creazione di Admin Console di profili di notifica utente. Consulta [Profili di notifica](/help/journey-onboarding/notification-profiles.md)
* Prendi in considerazione la configurazione delle regole del filtro del traffico per controllare quale traffico non dovrebbe essere consentito sul tuo sito web.
   * Le regole del filtro del traffico del limite di velocità possono essere uno strumento efficace contro gli attacchi DDoS. Una categoria speciale di regole del filtro del traffico, chiamate regole WAF, richiede una licenza separata.
   * Consulta la documentazione per alcuni [regole iniziali suggerite](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules).

Puoi sempre fare riferimento all’elenco nel caso in cui sia necessario ricalibrare le attività durante il lancio.