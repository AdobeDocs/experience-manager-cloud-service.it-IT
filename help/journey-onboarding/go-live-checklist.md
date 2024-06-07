---
title: Elenco di controllo per la pubblicazione
description: Scopri tutti gli elementi che devono essere presenti per consentire una pubblicazione corretta con AEM as a Cloud Service
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: ht
source-wordcount: '575'
ht-degree: 100%

---

# Elenco di controllo per la pubblicazione {#Go-Live-Checklist}

Esamina questo elenco di attività per assicurarti di eseguire una pubblicazione fluida e corretta.

* Esegui una pipeline di produzione end-to-end con test funzionali e dell’interfaccia utente per garantire un’esperienza **sempre corrente** dei prodotti AEM. Consulta le risorse seguenti:
   * [Aggiornamenti della versione di AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Test funzionali personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Test dell’interfaccia utente](/help/implementing/cloud-manager/ui-testing.md)
* Se stai eseguendo la migrazione da AEM 6.5, devi migrare i contenuti alla produzione e assicurarti che un sottoinsieme rilevante sia disponibile nello staging per il test.
   * Le best practice dei DevOps per AEM implicano che il codice passi dallo sviluppo all’ambiente di produzione, mentre il contenuto sia trasferito dagli ambienti di produzione.
* Pianifica un periodo di blocco del codice e dei contenuti.
   * Consulta anche la sezione [Timeline di blocco del codice e dei contenuti per la migrazione](#code-content-freeze)
* Esegui l’integrazione del contenuto finale.
* Convalida le configurazioni di Dispatcher.
   * Utilizzare una funzione di convalida di Dispatcher che ne semplifica la configurazione, la convalida e la simulazione locale
      * [Configurare strumenti Dispatcher locali.](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools#prerequisites)
   * Esamina attentamente la configurazione dell’host virtuale.
      * La soluzione più semplice (e predefinita) consiste nell’includere `ServerAlias *` nel file host virtuale in `/dispatcher/src/conf.d/available_vhostsfolder`.
         * Questo consentirà di funzionare agli alias host utilizzati dai test funzionali del prodotto, all’invalidazione della cache di Dispatcher e ai cloni.
      * Tuttavia, se `ServerAlias *` non è accettabile, almeno le voci `ServerAlias` seguenti devono essere consentite in aggiunta ai domini personalizzati:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Configura CDN, SSL e DNS.
   * Se utilizzi una tua rete CDN, inserisci un ticket di supporto per configurare l’indirizzamento appropriato.
      * Per maggiori informazioni, consulta la sezione [La rete CDN del cliente punta a quella CDN gestita da AEM](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) nella documentazione della rete CDN.
      * Configura SSL e DNS in base alla documentazione del fornitore CDN.
   * Se non utilizzi una rete CDN aggiuntiva, gestisci SSL e DNS come descritto nella documentazione seguente:
      * Gestione dei certificati SSL
         * [Introduzione alla gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [Gestione dei certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Gestione dei nomi di dominio personalizzati (DNS)
         * Per evitare che il cutover DNS introduca problemi imprevisti, è consigliabile creare un sottodominio di test a cui connettere l’istanza di produzione prima della pubblicazione ed eseguire un ciclo di test UAT. Pertanto, se il tuo dominio è example.com, puoi creare un sottodominio test.example.com e applicarlo alla produzione. Durante il test UAT del dominio, dovrai cercare elementi come il reindirizzamento corretto dei collegamenti, la memorizzazione in cache e le configurazioni di Dispatcher.
         * [Introduzione ai nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Ricorda di convalidare il TTL impostato per il record DNS.
      * Il TTL è il periodo di tempo in cui un record DNS rimane nella cache prima di richiedere un aggiornamento al server.
      * Se il TTL è elevato, la propagazione degli aggiornamenti al record DNS richiederà più tempo.
* Esegui test di prestazioni e sicurezza che soddisfino i requisiti e gli obiettivi aziendali.
   * Esecuzione di test nell’ambiente staging.  Ha le stesse dimensioni della produzione.
   * Gli ambienti di sviluppo non hanno le stesse dimensioni dello staging della e produzione.
* Esamina l’ambiente e assicurati che la pubblicazione effettiva venga eseguita senza alcuna nuova distribuzione o aggiornamento del contenuto.
* Creare profili di notifica utente di Admin Console. Consulta [Profili di notifica](/help/journey-onboarding/notification-profiles.md)
* Prendi in considerazione la configurazione delle regole del filtro del traffico per controllare quale traffico non dovrebbe essere consentito sul tuo sito web.
   * Le regole del filtro del traffico del limite di frequenza possono essere uno strumento efficace contro gli attacchi DDoS. Una categoria speciale di regole del filtro del traffico, chiamate regole WAF, richiede una licenza separata.
   * Consulta la documentazione per alcune [regole iniziali suggerite](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules).

Puoi sempre fare riferimento all’elenco nel caso in cui sia necessario ricalibrare le attività durante la pubblicazione.
