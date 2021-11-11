---
title: Accesso utente a nuova reliquia
description: Accesso utente a nuova reliquia
index: false
hide: true
source-git-commit: 22dc38ac4aa736ae5c676cfba16e16b0b3e44936
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---


# Nuovo monitoraggio delle prestazioni delle applicazioni reliche per AEM as a Cloud Service {#new-relic}

## Introduzione {#introduction}

L&#39;Adobe pone un&#39;enfasi particolare sul monitoraggio, la disponibilità e le prestazioni dell&#39;applicazione. Per raggiungere questo obiettivo, AEM as a Cloud Service fornisce l’accesso a una nuova suite di monitoraggio relic personalizzata come parte dell’offerta di prodotto standard per garantire ai team la massima visibilità alle metriche di prestazioni del sistema di Cloud Service Adobe Experience Manager e dell’ambiente. Questa sezione descrive le nuove funzioni di monitoraggio delle relazioni abilitate negli ambienti as a Cloud Service AEM per migliorare le prestazioni e consentire di sfruttare al meglio AEM as a Cloud Service.

## Monitoraggio delle transazioni as a Cloud Service tramite nuova relic {#transaction-monitoring}

Di seguito sono riportate le funzioni chiave nel nuovo monitoraggio delle prestazioni delle applicazioni reliche per AEM as a Cloud Service:

* Accesso diretto a un nuovo account Relic One dedicato (accesso gestito dal supporto Adobe).

* Agente APM nuovo Relic Strumentalizzato che mostra chiamate di metodo esatte con numeri di riga, incluse dipendenze esterne e database.

* Ottimizzazione delle prestazioni olistica grazie alla combinazione di metriche chiave dal monitoraggio a livello di infrastruttura e dal monitoraggio delle applicazioni (Adobe Experience Manager).

* Esposizione di AEM Mbeans e controlli di integrità JMX as a Cloud Service direttamente nelle metriche New Relic Insights, consentendo un controllo approfondito delle prestazioni dello stack delle applicazioni e delle metriche di integrità.

## Accesso al nuovo account relic AEM as a Cloud Service {#accessing-new-relic}

Il tuo nuovo account Relic dedicato verrà fornito e gestito da Adobe tramite l’assistenza clienti. L&#39;Adobe rimarrà il proprietario e l&#39;amministratore e fornirà l&#39;account per tuo conto per fornire l&#39;accesso al tuo sotto-account dedicato.

Per accedere al tuo account secondario Nuova relic associato al tuo programma as a Cloud Service di AEM:

* Apri una richiesta accedendo alla scheda Supporto nell’Admin Console.
* Accertati che il ticket includa i dettagli dell’ID programma e l’elenco di utenti a cui richiedi ai team di Adobe di aprire l’accesso alla nuova relazione.
* A tutti gli utenti devono essere forniti il nome completo e l&#39;indirizzo e-mail valido.

   >[!NOTE]
   >Per ulteriori informazioni su AEM portale di supporto, consulta Supporto per Experience Cloud.

Una volta fornito l’accesso, New Relic invia un’e-mail di conferma a ogni utente, in modo che possa completare il processo di configurazione e accedere. Se non sono in grado di individuare l’e-mail di conferma dell’account originale:

1. Vai alla pagina di accesso di New Relic all&#39;indirizzo login.newrelic.com/login.

1. Selezionare Password dimenticata.

1. Digita l&#39;indirizzo e-mail dell&#39;account e seleziona Invia la mia password.

1. Quando il sistema di New Relic restituisce un messaggio e-mail, seleziona il collegamento in esso contenuto per confermare nuovamente il tuo account.

   >[!NOTE]
   >Se non ricevi un’e-mail da New Relic:
   >Controlla i filtri anti-spam. Se applicabile, aggiungi Nuova relazione all’elenco consentiti e-mail.
   >Ti invitiamo a inviare feedback sul ticket di supporto e i nostri team ti aiuteranno a fornire ulteriori informazioni

1. Se completi la procedura di registrazione e non riesci ad accedere al tuo account a causa di messaggi di errore e-mail o password, riceverai un ticket di supporto tramite Admin Console.

Se ti viene chiesto di verificare l’e-mail durante l’accesso, significa che l’e-mail è associata a più account e avrà la possibilità di verificare l’e-mail durante l’accesso. Questo ti consentirà di scegliere a quale account accedere. Se non verifica il tuo indirizzo e-mail, New Relic tenterà di accedere con il record utente creato più di recente associato al tuo indirizzo e-mail. Per evitare di verificare l’e-mail durante ogni accesso, fai clic sulla casella di controllo Ricordami nella schermata di accesso.

Per ulteriori informazioni, apri una richiesta di supporto tramite AEM Support Portal.

## Eccezioni {#exceptions}

AEM as a Cloud Service concentra l&#39;offerta solo sulla nuova soluzione APM relativa e non fornisce supporto per le funzionalità di avvisi, registrazioni o integrazione API.

Per ulteriori informazioni o ulteriori indicazioni sulle offerte nuove relic per il programma as a Cloud Service di AEM, aprire un ticket di supporto tramite AEM Support Portal.

## Domande frequenti per nuovo account relic {#faqs}

### Che cosa controlla Adobe con New Relic? {#adobe-monitor}

Adobe monitora i servizi di authoring, pubblicazione e anteprima (se disponibili) as a Cloud Service AEM tramite il plug-in Java New Relic APM. L&#39;Adobe consente la telemetria e il monitoraggio APM nuovi e personalizzati tra ambienti non di produzione e produzione AEM as a Cloud Service. Il tuo nuovo account Relic è collegato a un account gestito da un Adobe primario e contiene più applicazioni che generano rapporti in esso.

Tre per AEM ambiente as a Cloud Service:

* Un’applicazione per il servizio Author per ambiente
* Un&#39;applicazione per il servizio Publish per ambiente (inclusa la pubblicazione aurea)
* Un&#39;applicazione per il servizio Preview per ogni ambiente Ogni applicazione utilizza una chiave di licenza, AEM gli ambienti as a Cloud Service genereranno rapporti su un solo account New Relic. Le metriche e gli eventi di monitoraggio completi per New Relic APM e Infrastructure vengono conservati per 7 giorni.

### Chi può accedere ai dati del nuovo Cloud Service relic? {#access-new-relic-cloud}

L&#39;accesso in lettura completa sarà concesso per un massimo di 10 membri del tuo team. L&#39;accesso in lettura includerà tutte le metriche APM raccolte dall&#39;agente Nuova relazione.

### È supportata la configurazione SSO personalizzata? {#custom-sso}

La configurazione SSO personalizzata non è attualmente supportata per il nuovo account relic fornito da Adobe.

### Cosa succede se disponi già di un abbonamento a un nuovo relic locale? {#new-relic-subscription}

La nuova piattaforma di osservabilità di New Relic denominata New Relic One consente ai gruppi di supporto di Adobe e ai team di osservare, monitorare e visualizzare metriche ed eventi in un’unica posizione. Nuova relic One consente agli utenti di eseguire ricerche in tutti gli account in cui hanno accesso e visualizzano i dati di tutti i servizi e gli host in un’unica visualizzazione. Mentre i team di supporto Adobe monitoreranno l’applicazione as a Cloud Service AEM utilizzando la nuova relic e altri strumenti interni come parte del servizio, i team possono continuare a sfruttare la nuova relic per i servizi in hosting e l’infrastruttura locali. Potranno visualizzare i dati provenienti sia da account Adobe che da account New Relic gestiti dai clienti.

>[!NOTE]
>L&#39;utente deve disporre delle autorizzazioni necessarie e utilizzare la stessa metodologia di accesso per entrambi gli account (ad Adobe e per l&#39;account New Relic gestito dai clienti).


