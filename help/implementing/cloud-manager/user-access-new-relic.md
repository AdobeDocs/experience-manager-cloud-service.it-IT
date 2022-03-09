---
title: Nuova relè uno
description: Scopri il nuovo servizio di monitoraggio delle prestazioni delle applicazioni Relic One (APM) per AEM as a Cloud Service e come accedervi.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 1%

---


# Nuova relè uno {#user-access}

Scopri il nuovo servizio di monitoraggio delle prestazioni delle applicazioni Relic One (APM) per AEM as a Cloud Service e come accedervi.

## Introduzione {#introduction}

L&#39;Adobe pone un&#39;enfasi particolare sul monitoraggio, la disponibilità e le prestazioni dell&#39;applicazione. Per raggiungere questo obiettivo, AEM as a Cloud Service fornisce l&#39;accesso a una suite di monitoraggio personalizzata New Relic One come parte dell&#39;offerta di prodotto standard per garantire ai team la massima visibilità alle metriche di prestazioni del sistema e dell&#39;ambiente as a Cloud Service AEM.

In questo documento vengono descritte le funzioni di monitoraggio delle prestazioni delle applicazioni (APM, New Relic One Application Monitoraggio) abilitate negli ambienti as a Cloud Service AEM per supportare le prestazioni e ottenere il massimo da AEM as a Cloud Service.

## Funzioni {#transaction-monitoring}

Nuova Relic One APM per AEM as a Cloud Service ha molte caratteristiche.

* Accesso diretto a un nuovo account Relic One dedicato (accesso gestito dal supporto Adobe)

* Agente APM nuovo Relic One Strumentazione che mostra chiamate di metodo esatte con numeri di riga, incluse dipendenze esterne e database

* Ottimizzazione delle prestazioni olistica grazie alla combinazione di metriche chiave dal monitoraggio a livello di infrastruttura e dal monitoraggio delle applicazioni (Adobe Experience Manager)

* Esposizione di AEM Mbeans JMX as a Cloud Service e controlli di integrità direttamente all&#39;interno delle metriche New Relic Insights, che consentono un controllo approfondito delle prestazioni dello stack delle applicazioni e delle metriche di integrità.

## Accesso a una nuova relazione {#accessing-new-relic}

Segui questi passaggi per accedere al tuo nuovo account secondario Relic One associato al tuo programma as a Cloud Service AEM.

1. Apri una richiesta accedendo alla scheda Supporto nell’Admin Console.
1. Nella richiesta, includi i dettagli del tuo ID programma e l’elenco degli utenti che richiedono l’accesso a New Relic.
   * Devono essere forniti i nomi completi e gli indirizzi e-mail validi di tutti gli utenti.

Consulta il documento [Portale di supporto AEM per Experience Cloud](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html) per maggiori dettagli sull&#39;apertura dei biglietti.

Una volta fornito l’accesso, New Relic invia un’e-mail di conferma a ogni utente, in modo che l’utente possa completare il processo di configurazione e accedere.

Se l’utente non è in grado di individuare l’e-mail di conferma dell’account originale, effettua le seguenti operazioni.

1. Passa alla pagina di accesso di New Relic all&#39;indirizzo [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Seleziona **Hai dimenticato la password?**.

   ![Nuovo accesso a Relé](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Digita l’indirizzo e-mail dell’account e seleziona **Invia il collegamento di reimpostazione**.

   ![Immettere l&#39;indirizzo e-mail](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. Nuova relic invia all’utente un’e-mail contenente un collegamento per confermare l’account.

Se completi la procedura di registrazione e non riesci ad accedere al tuo account a causa di messaggi di errore e-mail o password, registra un ticket di supporto tramite il [Admin Console](https://adminconsole.adobe.com/).

>[!TIP]
>
>Se non ricevi un’e-mail da New Relic:
>
>* Controlla il tuo [filtri anti-spam](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
>* Se del caso, [aggiungi nuova relic al tuo elenco consentiti e-mail](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
>* Se nessuno dei due suggerimenti ti aiuta, fornisci un feedback sul ticket di supporto e il team di supporto Adobe ti aiuterà ulteriormente.


### Verifica dell’e-mail {#verify-email}

Se ti viene chiesto di verificare l’e-mail durante l’accesso, significa che l’e-mail è associata a più account. Questo ti consente di scegliere a quale account accedere.

Se non verifica il tuo indirizzo e-mail, New Relic tenterà di accedere con il record utente creato più di recente associato al tuo indirizzo e-mail. Per evitare di verificare l’e-mail durante ogni accesso, fai clic sul pulsante **Ricordami** nella schermata di accesso.

Per ulteriore assistenza, apri un ticket di supporto tramite il [AEM Support Portal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Eccezioni {#exceptions}

AEM as a Cloud Service offre solo la nuova soluzione Relic One APM e non fornisce supporto per le integrazioni di avvisi, registrazioni o API.

Per ulteriori informazioni o ulteriori indicazioni sulle nuove offerte relative al programma as a Cloud Service AEM, apri un ticket di supporto tramite il [AEM Support Portal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Domande frequenti per nuovo account relic {#faqs}

### Che cosa controlla Adobe con Nuovo Relic One? {#adobe-monitor}

Adobe monitora i servizi di authoring, pubblicazione e anteprima as a Cloud Service AEM (dove disponibili) tramite il plug-in Java di New Relic One. L&#39;Adobe consente la telemetria e il monitoraggio personalizzati di un nuovo Relic One APM tra ambienti non di produzione e produzione AEM as a Cloud Service.

Il tuo nuovo account Relic One è collegato a un account gestito da un Adobe principale e contiene più applicazioni per la generazione di rapporti: tre per ambiente as a Cloud Service AEM.

* Un’applicazione per il servizio di authoring per ambiente
* Un&#39;applicazione per il servizio di pubblicazione per ambiente (inclusa la pubblicazione aurea)
* Un&#39;applicazione per il servizio di anteprima per ambiente

Nota:

* Ogni applicazione utilizza una chiave di licenza.
* AEM ambienti as a Cloud Service riferiscono a un solo nuovo account Relic One .
* Le metriche e gli eventi di monitoraggio completi per New Relic One vengono conservati per 7 giorni.

### Chi può accedere ai dati del servizio cloud New Relic One? {#access-new-relic-cloud}

L&#39;accesso in lettura completa sarà concesso per un massimo di 10 membri del tuo team. L&#39;accesso in lettura includerà tutte le metriche APM raccolte dall&#39;agente New Relic One.

### La configurazione SSO personalizzata è supportata? {#custom-sso}

La configurazione SSO personalizzata non è supportata per il nuovo account Relic One fornito da Adobe.

### Cosa succede se dispongo già di un abbonamento on-premise a New Relic? {#new-relic-subscription}

La nuova Relic One è la nuova piattaforma di osservabilità da New Relic e consente al supporto di Adobe e ai team di osservare, monitorare e visualizzare metriche ed eventi in un’unica posizione.

Nuova relic One consente agli utenti di eseguire ricerche in tutti gli account in cui hanno accesso e visualizzano i dati di tutti i servizi e gli host in un’unica visualizzazione.

Anche se il supporto di Adobe monitorerà l&#39;applicazione as a Cloud Service AEM utilizzando nuovi strumenti interni e altri strumenti interni come parte del servizio, i team possono continuare a sfruttare la nuova relazione per i servizi in hosting e l&#39;infrastruttura locali. Saranno in grado di visualizzare i dati provenienti sia dal nuovo account Relic One di Adobe che da nuovi account Relic gestiti dai clienti.

>[!NOTE]
>
>Per visualizzare entrambi i set di dati all’interno di una nuova relazione, un utente deve disporre delle autorizzazioni necessarie e utilizzare la stessa metodologia di accesso per entrambi gli account (ad Adobe, Nuovo Relic One e gli account New Relic gestiti dal cliente).
