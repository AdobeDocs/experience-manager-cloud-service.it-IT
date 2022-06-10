---
title: New Relic One
description: Scopri il nuovo servizio di monitoraggio delle prestazioni delle applicazioni Relic One (APM) per AEM as a Cloud Service e come accedervi.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 8ae52afc366c6607cfc806f68bec2069a2e93f94
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 1%

---


# Nuova relè uno {#user-access}

Scopri il nuovo servizio di monitoraggio delle prestazioni delle applicazioni Relic One (APM) per AEM as a Cloud Service e come accedervi.

## Introduzione {#introduction}

L&#39;Adobe pone un&#39;enfasi particolare sul monitoraggio, la disponibilità e le prestazioni dell&#39;applicazione. AEM as a Cloud Service fornisce l&#39;accesso a una suite di monitoraggio nuova relic One personalizzata come parte dell&#39;offerta di prodotto standard per garantire ai team la massima visibilità alle metriche di prestazioni del sistema e dell&#39;ambiente as a Cloud Service di AEM.

In questo documento viene descritto come gestire l&#39;accesso alle funzioni di monitoraggio delle prestazioni delle applicazioni (APM, New Relic One application monitoring) abilitate negli ambienti as a Cloud Service AEM per supportare le prestazioni e ottenere il massimo da AEM as a Cloud Service.

Quando viene creato un nuovo programma di produzione, viene creato automaticamente il nuovo account secondario Relic One associato al programma as a Cloud Service AEM.

## Funzioni {#transaction-monitoring}

Nuova Relic One APM per AEM as a Cloud Service ha molte caratteristiche.

* Accesso diretto a un nuovo account Relic One dedicato (accesso gestito dal supporto Adobe)

* Agente APM nuovo Relic One Strumentazione che mostra chiamate di metodo esatte con numeri di riga, incluse dipendenze esterne e database

* Ottimizzazione delle prestazioni olistica grazie alla combinazione di metriche chiave dal monitoraggio a livello di infrastruttura e dal monitoraggio delle applicazioni (Adobe Experience Manager)

* Esposizione di AEM Mbeans JMX as a Cloud Service e controlli di integrità direttamente all&#39;interno delle metriche New Relic Insights, che consentono un controllo approfondito delle prestazioni dello stack delle applicazioni e delle metriche di integrità.

## Gestione di nuovi utenti relé uno {#manage-users}

Segui questi passaggi per definire gli utenti del tuo nuovo account secondario Relic One associato al tuo programma as a Cloud Service AEM.

>[!NOTE]
>
>Un utente in **Proprietario business** o **Gestione distribuzione** per gestire i nuovi utenti di Relic One, è necessario accedere al ruolo.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione appropriata.

1. Fare clic sul programma per il quale si desidera gestire i nuovi utenti Relic One.

1. Nella parte inferiore del **Ambienti** nella pagina di panoramica del programma fare clic sul pulsante con i puntini di sospensione e selezionare **Gestire gli utenti**.

   ![Gestire gli utenti](assets/newrelic-manage-users.png)

   * Puoi anche accedere al **Gestire gli utenti** tramite il pulsante di sospensione nella parte superiore della **Ambienti** schermo del programma.

1. In **Gestisci nuovi utenti relé** immettere il nome e il cognome dell’utente che si desidera aggiungere e fare clic sul pulsante **Aggiungi** pulsante . Ripeti questo passaggio per tutti gli utenti che desideri aggiungere.

   ![Aggiungi utenti](assets/newrelic-add-users.png)

1. Per rimuovere un nuovo Relic One utenti, fare clic sul pulsante Elimina all&#39;estremità destra della riga che rappresenta l&#39;utente.

1. Fai clic su **Salva** per creare gli utenti.

Una volta definiti gli utenti, New Relic invia un’e-mail di conferma a ogni utente a cui hai concesso l’accesso, in modo che l’utente possa completare il processo di configurazione e accedere.

>[!NOTE]
>
>Se gestisci i nuovi utenti di One Relic One, devi anche aggiungerti come utente per avere accesso anche a . Essere **Proprietario business** o **Gestione distribuzione** non è sufficiente avere accesso a New Relic One. Devi creare te stesso come utente.

## Attiva il tuo nuovo account utente relé one {#activate-account}

Una volta creato un nuovo account utente Relic One come descritto nella sezione di anteprima [Gestione di nuovi utenti relé uno](#manage-users), New Relic invia a tali utenti un’e-mail di conferma all’indirizzo fornito. Per utilizzare tali account, gli utenti devono prima attivare i propri account con Nuova reliquia reimpostando le proprie password.

Segui questi passaggi per attivare il tuo account come nuovo utente relic.

1. Fai clic sul collegamento fornito nell’e-mail da Nuova relazione. Questo apre il browser alla pagina Nuovo accesso relic.

1. Nella pagina Nuovo accesso relic, seleziona **Hai dimenticato la password?**.

   ![Nuovo accesso a Relé](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Inserisci l’indirizzo e-mail in cui hai ricevuto l’e-mail di conferma e seleziona **Invia il collegamento di reimpostazione**.

   ![Immettere l&#39;indirizzo e-mail](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. Nuova relic ti invierà un’e-mail contenente un collegamento per confermare l’account.

Se non ricevi un&#39;e-mail di conferma da New Relic, consulta la [sezione sulla risoluzione dei problemi.](#troubshooting)

## Accesso a una nuova relazione {#accessing-new-relic}

Una volta che [ha attivato il tuo nuovo account Relic,](#activate-account) puoi accedere a New Relic One tramite Cloud Manager o direttamente.

Per accedere a New Relic One tramite Cloud Manager:

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione appropriata.

1. Fare clic sul programma per il quale si desidera accedere a Nuovo Relic One.

1. Nella parte inferiore del **Ambienti** nella pagina di panoramica del programma fare clic sul pulsante con i puntini di sospensione e selezionare **Apri nuova relè**.

   ![Gestire gli utenti](assets/newrelic-access.png)

   * È inoltre possibile accedere a Nuova Relica tramite il pulsante con i puntini di sospensione nella parte superiore della **Ambienti** schermo del programma.

1. Nella nuova scheda del browser che si apre, accedi a Nuovo Relic One.

Per accedere direttamente a Nuova Relic One:

1. Passa alla pagina di accesso di New Relic all&#39;indirizzo [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. Accedi a Nuovo Relic One.

### Verifica dell’e-mail {#verify-email}

Se ti viene chiesto di verificare l&#39;e-mail durante l&#39;accesso a New Relic One, significa che l&#39;e-mail è associata a più account. Questo ti consente di scegliere a quale account accedere.

Se non verifica il tuo indirizzo e-mail, New Relic tenterà di accedere con il record utente creato più di recente associato al tuo indirizzo e-mail. Per evitare di verificare l’e-mail durante ogni accesso, fai clic sul pulsante **Ricordami** nella schermata di accesso.

Per ulteriore assistenza, apri un ticket di supporto tramite il [AEM Support Portal](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).

## Risoluzione dei problemi relativi all&#39;accesso alla nuova Relé One {#troubleshooting}

Se sei stato aggiunto come nuovo utente Relic One come descritto nella sezione [Gestione di nuovi utenti relé uno](#manage-users) e non è possibile individuare l&#39;e-mail di conferma dell&#39;account originale seguendo questi passaggi.

1. Passa alla pagina di accesso di New Relic all&#39;indirizzo [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Seleziona **Hai dimenticato la password?**.

   ![Nuovo accesso a Relé](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Inserisci l’indirizzo e-mail utilizzato per creare l’account e seleziona **Invia il collegamento di reimpostazione**.

   ![Immettere l&#39;indirizzo e-mail](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. Nuova relic ti invierà un’e-mail contenente un collegamento per confermare l’account.

Se completi la procedura di registrazione e non riesci ad accedere al tuo account a causa di messaggi di errore e-mail o password, registra un ticket di supporto tramite il [Admin Console.](https://adminconsole.adobe.com/)

Se non ricevi un’e-mail da New Relic:

* Controlla il tuo [filtri anti-spam](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
* Se del caso, [aggiungi nuova relic al tuo elenco consentiti e-mail](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
* Se nessuno dei due suggerimenti ti aiuta, fornisci un feedback sul ticket di supporto e il team di supporto Adobe ti aiuterà ulteriormente.

## Limitazioni  {#limitations}

Le seguenti limitazioni si applicano all&#39;aggiunta di utenti a Nuova Relic One:

* È possibile aggiungere un massimo di 25 utenti. Se è stato raggiunto il numero massimo di utenti, rimuovi gli utenti per poter aggiungere nuovi utenti.
* Gli utenti aggiunti a Nuova relazione saranno di tipo **Limitato** fare riferimento a [per ulteriori informazioni, consulta la documentazione Nuova relic .](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/#:~:text=In%20general%2C%20Admins%20take%20responsibility,Restricted%20Users%20can%20use%20them.&amp;text=One%20or%20more%20Singoli%20who,change)%20any%20New%20Relic%20features.)
* AEM as a Cloud Service offre solo la nuova soluzione Relic One APM e non fornisce supporto per le integrazioni di avvisi, registrazioni o API.

Per ulteriori informazioni o ulteriori indicazioni sulle nuove offerte relative al programma as a Cloud Service AEM, apri un ticket di supporto tramite il [AEM Support Portal](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Domande frequenti sul nuovo relic one {#faqs}

### Che cosa controlla Adobe con Nuovo Relic One? {#adobe-monitor}

Adobe monitora i servizi di authoring, pubblicazione e anteprima as a Cloud Service AEM (dove disponibili) tramite il plug-in Java di New Relic One. L&#39;Adobe consente la telemetria e il monitoraggio personalizzati di un nuovo Relic One APM tra ambienti non di produzione e produzione AEM as a Cloud Service.

Il tuo nuovo account Relic One è collegato a un account gestito da un Adobe principale e contiene più applicazioni per la generazione di rapporti: tre per ambiente as a Cloud Service AEM.

* Un’applicazione per il servizio di authoring per ambiente
* Un&#39;applicazione per il servizio di pubblicazione per ambiente (inclusa la pubblicazione aurea)
* Un&#39;applicazione per il servizio di anteprima per ambiente

Nota:

* Ogni applicazione utilizza una chiave di licenza.
* AEM ambienti as a Cloud Service riferiscono a un solo nuovo account Relic One .
* Le metriche e gli eventi di monitoraggio completi per New Relic One vengono conservati per sette giorni.

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
