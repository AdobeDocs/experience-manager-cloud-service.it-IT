---
title: Elenco di controllo per la pubblicazione
description: Scopri tutti gli elementi che devono essere presenti per una pubblicazione di successo con AEM as a Cloud Service.
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 56%

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
* Convalidare le configurazioni Dispatcher.
   * Utilizza una convalida Dispatcher locale che semplifica la configurazione, la convalida e la simulazione locale di Dispatcher
      * [Configurare gli strumenti Dispatcher locali](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools#prerequisites).
   * Esamina attentamente la configurazione dell’host virtuale.
      * La soluzione più semplice e predefinita consiste nell&#39;includere `ServerAlias *` nel file host virtuale in `/dispatcher/src/conf.d/available_vhostsfolder`. In questo modo è possibile utilizzare gli alias host utilizzati dai test funzionali del prodotto, l&#39;annullamento della validità della cache di Dispatcher e i cloni.
      * Tuttavia, se `ServerAlias *` non è accettabile, oltre ai domini personalizzati devono essere consentite almeno le seguenti `ServerAlias` voci:
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
         * [Introduzione ai certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)
         * [Gestire i certificati SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Gestione dei nomi di dominio personalizzati (DNS)
         * Assicurati che il passaggio al DNS non introduca problemi imprevisti. Crea un sottodominio di test a cui connettere l’istanza di produzione prima di andare &quot;live&quot; ed esegui un ciclo di test UAT. Pertanto, se il tuo dominio è example.com, puoi creare un sottodominio test.example.com e applicarlo alla produzione. Durante il test UAT del dominio, cerca elementi quali il reindirizzamento corretto dei collegamenti, la memorizzazione in cache e le configurazioni di Dispatcher.
         * [Introduzione ai nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Gestire un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Ricorda di convalidare il TTL impostato per il record DNS.
      * Il TTL è il periodo di tempo in cui un record DNS rimane nella cache prima di richiedere un aggiornamento al server.
      * Se il TTL è molto alto, la propagazione degli aggiornamenti al record DNS richiede più tempo.
* Esegui test di prestazioni e sicurezza che soddisfino i requisiti e gli obiettivi aziendali.
   * Eseguire test in un ambiente stage.  Ha le stesse dimensioni della produzione.
   * Gli ambienti di sviluppo non hanno le stesse dimensioni dello staging della e produzione.
* Esamina l’ambiente e assicurati che la pubblicazione effettiva venga eseguita senza alcuna nuova distribuzione o aggiornamento del contenuto.
* Creazione di profili di notifica utente di Admin Console. Consulta [Profili di notifica](/help/journey-onboarding/notification-profiles.md)
* Prendi in considerazione la configurazione delle regole del filtro del traffico per controllare quale traffico non dovrebbe essere consentito sul tuo sito web.
   * Le regole di filtro del traffico per il limite di velocità possono essere uno strumento efficace contro gli attacchi DDoS. Una categoria speciale di regole del filtro del traffico, denominate regole di WAF (Web Application Firewall), richiede una licenza separata.
   * Consulta la documentazione per alcune [regole iniziali suggerite](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules).

Puoi sempre fare riferimento all’elenco nel caso in cui sia necessario ricalibrare le attività durante la pubblicazione.
