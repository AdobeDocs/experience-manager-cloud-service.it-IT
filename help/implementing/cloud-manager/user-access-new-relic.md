---
title: New Relic One
description: Scopri il servizio New Relic One di monitoraggio delle prestazioni delle applicazioni (APM) per AEM as a Cloud Service e come accedervi.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 9089c66a2fdb5a05eb888e2af736862aff1b7a11
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 99%

---


# New Relic One {#user-access}

Scopri il servizio New Relic One di monitoraggio delle prestazioni delle applicazioni (APM) per AEM as a Cloud Service e come accedervi.

## Introduzione {#introduction}

Per Adobe, monitoraggio, disponibilità e prestazioni delle applicazioni sono molto importanti. AEM as a Cloud Service fornisce l’accesso a una suite di monitoraggio personalizzata New Relic One come parte dell’offerta standard del prodotto, per garantire che i team dispongano della massima visibilità sulle metriche delle prestazioni di ambienti e sistemi AEM as a Cloud Service.

Questo documento descrive come gestire l’accesso alle funzioni New Relic One di monitoraggio delle prestazioni delle applicazioni (APM) abilitate negli ambienti AEMaaCS per supportare le prestazioni e ottenere il massimo da AEM as a Cloud Service.

Quando si crea un nuovo programma di produzione, l’account secondario New Relic One associato al programma AEM as a Cloud Service viene creato automaticamente.

## Funzioni {#transaction-monitoring}

New Relic One APM per AEM as a Cloud Service presenta numerose funzioni.

* Accesso diretto a un account New Relic One dedicato

* Agente New Relic One APM instrumentato che mostra le chiamate al metodo esatto con i numeri delle righe, includendo le dipendenze e i database esterni

* Ottimizzazione olistica delle prestazioni grazie alla combinazione di metriche chiave dal monitoraggio a livello di infrastruttura e dal monitoraggio delle applicazioni (Adobe Experience Manager)

* Esposizione di JMX Mbeans e dei controlli di stato di AEM as a Cloud Service interni alle metriche Insights di New Relic che consentono un’analisi più approfondita delle prestazioni dello stack dell’applicazione e delle metriche relative allo stato.

## Gestione degli utenti di New Relic One {#manage-users}

Per definire gli utenti dell’account secondario New Relic One associato al programma di AEM as a Cloud Service, segui la procedura riportata di seguito.

>[!NOTE]
>
>Per poter gestire gli utenti di New Relic One, l’utente con il ruolo **Proprietario business** o **Responsabile dell’implementazione** deve aver effettuato l’accesso.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic sul programma per il quale desideri gestire gli utenti di New Relic One.

1. Dalla pagina Panoramica, passa alla parte inferiore della scheda **Ambienti** e fai clic sul pulsante con i puntini di sospensione, quindi seleziona **Gestisci utenti**.

   ![Gestisci utenti](assets/newrelic-manage-users.png)

   * Puoi accedere all’opzione **Gestisci utenti** anche dal pulsante con i puntini di sospensione nella parte superiore della schermata **Ambienti** del programma.

1. Nella finestra di dialogo **Gestisci utenti di New Relic**, inserisci nome e cognome dell’utente che desideri aggiungere, quindi fai clic sul pulsante **Aggiungi**. Ripeti questo passaggio per tutti gli utenti che desideri aggiungere.

   ![Aggiungi utenti](assets/newrelic-add-users.png)

1. Per rimuovere gli utenti di New Relic One, fai clic sul pulsante Elimina all’estrema destra della riga dell’utente.

1. Per creare gli utenti, fai clic su **Salva**.

Una volta definiti gli utenti, New Relic invia un’e-mail di conferma a tutti coloro a cui hai concesso l’accesso, in modo che possano completare il processo di configurazione e accedere.

>[!NOTE]
>
>Se gestisci gli utenti di New Relic One, per avere accesso devi aggiungere anche il tuo utente. Avere il ruolo di **Proprietario business** o **Responsabile dell’implementazione** non è sufficiente per avere accesso a New Relic One. Devi creare un utente anche per te stesso o stessa.

## Attivazione dell’account utente di New Relic One {#activate-account}

Dopo aver creato un account utente di New Relic One come descritto nella sezione precedente, [Gestione degli utenti di New Relic One](#manage-users), New Relic invia a tali utenti un’e-mail di conferma all’indirizzo fornito. Per utilizzare gli account, gli utenti devono prima attivarli con New Relic reimpostando la password.

Per attivare l’account come utente di New Relic, segui la procedura riportata di seguito.

1. Fai clic sul collegamento fornito nell’e-mail da New Relic. Ti reindirizza alla pagina di accesso a New Relic nel browser.

1. Nella pagina di accesso di New Relic, seleziona il collegamento **per il ripristino della password**.

   ![Accesso a New Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Inserisci l’indirizzo e-mail su cui hai ricevuto l’e-mail di conferma, quindi **conferma di voler ricevere il collegamento per reimpostare la password**.

   ![Inserimento dell’indirizzo e-mail](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. Riceverai un’e-mail da New Relic contente il collegamento per confermare l’account.

Se non ricevi un’e-mail di conferma da New Relic, consulta la [sezione Risoluzione dei problemi.](#troubshooting)

## Accesso a New Relic One {#accessing-new-relic}

Dopo aver [attivato l’account di New Relic,](#activate-account) puoi accedere a New Relic One direttamente o tramite Cloud Manager.

Per accedere a New Relic One tramite Cloud Manager:

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic sul programma per il quale desideri accedere a New Relic One.

1. Dalla pagina Panoramica, passa alla parte inferiore della scheda **Ambienti** e fai clic sul pulsante con i puntini di sospensione, quindi seleziona **Apri New Relic**.

   ![Gestisci utenti](assets/newrelic-access.png)

   * Puoi accedere a New Relic anche dal pulsante con i puntini di sospensione nella parte superiore della schermata **Ambienti** del programma.

1. Dalla nuova scheda del browser che viene visualizzata, accedi a New Relic One.

Per accedere direttamente a New Relic One:

1. Accedi alla pagina di accesso di New Relic all’indirizzo [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. Accedi a New Relic One.

### Verifica dell’e-mail {#verify-email}

Se ti viene chiesto di verificare l’e-mail durante l’accesso a New Relic One, significa che l’e-mail è associata a più account. Scegli a quale account accedere.

Se non verifichi il tuo indirizzo e-mail, New Relic tenterà di accedere con il più recente record utente creato e associato al tuo indirizzo e-mail. Per evitare la verifica dell’e-mail durante ogni tentativo di accesso, seleziona la casella di controllo per **ricordare le tue credenziali** nella schermata di accesso.

Per ulteriore assistenza, apri un ticket di supporto tramite il [portale AEM dedicato all’assistenza](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).

## Risoluzione dei problemi di accesso a New Relic One {#troubleshooting}

Se sei stato aggiunto o aggiunta come utente di New Relic One come descritto nella sezione [Gestione degli utenti di New Relic One](#manage-users) e non riesci a trovare l’e-mail di conferma dell’account originale, segui la procedura riportata di seguito.

1. Accedi alla pagina di accesso di New Relic all’indirizzo [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Seleziona il **collegamento per il ripristino della password**.

   ![Accesso a New Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Inserisci l’indirizzo e-mail utilizzato per creare l’account, quindi seleziona il **collegamento per reimpostare la password**.

   ![Inserimento dell’indirizzo e-mail](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. Riceverai un’e-mail da New Relic contente il collegamento per confermare l’account.

Se dopo aver completato la procedura di accesso non riesci ad accedere al tuo account per dei messaggi di errore relativi all’e-mail o alla password, invia un ticket di supporto tramite [Admin Console.](https://adminconsole.adobe.com/)

Se non ricevi un’e-mail da New Relic:

* Controlla i [filtri anti-spam](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
* Se possibile, [aggiungi New Relic all’elenco Consentiti della tua e-mail](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
* Se nessuna delle due soluzioni è utile, invia un feedback tramite ticket di supporto per ricevere ulteriore assistenza dal Team Adobe.

## Limitazioni {#limitations}

L’aggiunta di utenti a New Relic One prevede le seguenti limitazioni:

* È possibile aggiungere fino a un massimo di 25 utenti. Se è stato raggiunto il numero massimo di utenti, rimuovine alcuni per poterne aggiungere di nuovi.
* Gli utenti aggiunti a New Relic saranno di tipo **Limitato**. Per ulteriori informazioni, consulta la [documentazione di New Relic.](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/#:~:text=In%20general%2C%20Admins%20take%20responsibility,Restricted%20Users%20can%20use%20them.&amp;text=One%20or%20more%20individuals%20who,change)%20any%20New%20Relic%20features.)
* AEM as a Cloud Service offre unicamente la soluzione New Relic One APM e non fornisce supporto per avvisi, registrazione o integrazioni API.

Per ulteriore assistenza o informazioni sulle offerte di New Relic One per i programmi AEM as a Cloud Service, apri un ticket di supporto tramite il [portale AEM dedicato all’assistenza](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Domande frequenti su New Relic One {#faqs}

### Quali aspetti monitora Adobe con New Relic One? {#adobe-monitor}

Adobe monitora i servizi Author, Publish e Anteprima di AEM as a Cloud Service (quando disponibili) tramite il plug-in Java di New Relic One. Adobe supporta la telemetria e il monitoraggio personalizzati di New Relic One APM in ambienti di AEM as a Cloud Service di produzione e non di produzione.

L’account New Relic One è collegato a un account principale gestito da Adobe e integra diverse funzioni di reporting per le applicazioni: tre per ogni ambiente di AEM as a Cloud Service.

* Un’applicazione per il servizio Author per ogni ambiente
* Un’applicazione per il servizio Publish per ogni ambiente (inclusa la pubblicazione Golden)
* Un’applicazione per il servizio Anteprima per ogni ambiente

Nota:

* ogni applicazione utilizza una sola chiave di licenza.
* Gli ambienti di AEM as a Cloud Service fanno riferimento solamente a un account di New Relic One.
* Tutte le metriche di monitoraggio e gli eventi di New Relic One vengono conservati per sette giorni.

### Chi può accedere ai dati del servizio cloud di New Relic One? {#access-new-relic-cloud}

L’accesso in lettura completo è concesso a un massimo di 10 membri del team. L’accesso in lettura include tutte le metriche APM raccolte dall’agente di New Relic One.

### La configurazione SSO personalizzata è supportata? {#custom-sso}

La configurazione SSO personalizzata non è supportata per l’account New Relic One fornito da Adobe.

### Cosa succede se dispongo già di un abbonamento on-premise a New Relic? {#new-relic-subscription}

New Relic One è la nuova piattaforma di osservabilità di New Relic abilitata al supporto Adobe, che consente ai team di osservare, monitorare e visualizzare metriche ed eventi da un’unica posizione.

New Relic One mette a disposizione degli utenti la possibilità di effettuare ricerche in tutti gli account a cui hanno accesso e di visualizzare i dati di tutti i servizi e gli host in un’unica vista.

Sebbene il supporto Adobe monitori l’applicazione AEM as a Cloud Service con New Relic One e altri strumenti interni parte del servizio, i team possono continuare a sfruttare New Relic per infrastrutture e servizi ospitati on-premise. Possono visualizzare sia i dati dell’account Adobe New Relic One sia quelli degli account di New Relic gestiti dal cliente.

>[!NOTE]
>
>Per visualizzare entrambi i set di dati in New Relic One, l’utente deve disporre delle adeguate autorizzazioni e utilizzare la stessa metodologia di accesso per entrambi gli account (Adobe New Relic One e gli account di New Relic gestiti dal cliente).
