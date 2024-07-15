---
title: Assegnazione dei membri del gruppo ai profili di prodotto di Cloud Manager
description: Segui questa pagina per scoprire come assegnare i membri del gruppo ai profili di prodotto di Cloud Manager
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 100%

---


# Assegnazione dei membri del gruppo ai profili di prodotto di Cloud Manager {#assign-team-members}

In questa sezione del [percorso di onboarding](overview.md) scoprirai come assegnare i membri del gruppo ai profili di prodotto di Cloud Manager.

## Obiettivo {#objective}

Nel passaggio precedente di questo percorso, [Accesso a Admin Console,](admin-console.md) hai scoperto come accedere a Admin Console e verificare i privilegi come amministratore di sistema. Ora puoi consentire ai membri del gruppo di accedere a Cloud Manager. Per eseguire l’operazione, assegna i profili di prodotto.

Quando consenti l’accesso a una soluzione Adobe agli utenti, non devi necessariamente concedere loro l’accesso completo. Con i profili di prodotto è possibile disporre di un set personalizzato di autorizzazioni utente per ogni soluzione. Assegna i profili di prodotto con Admin Console.

Il primo passaggio consiste nel consentire agli utenti di accedere a Cloud Manager. Per supportarti, Cloud Manager offre configurazioni di sviluppo di livello Enterprise e pipeline CI/CD appositamente progettate per garantire test approfonditi e la massima qualità del codice, in modo da poter offrire esperienze eccezionali.

Dopo aver letto questo documento, dovresti:

* Sapere cosa sono i profili di prodotto.
* Sapere che cos’è Cloud Manager.
* Conoscere i tre importanti profili di prodotto di Cloud Manager: **Proprietario business**, **Responsabile dell’implementazione** e **Sviluppatore**.
* Saper assegnare i membri del gruppo ai profili di prodotto di Cloud Manager.

## Prerequisiti {#prerequisites}

Per assegnare i membri del gruppo ai profili di prodotto, devi disporre dei dettagli dei membri del gruppo che devono accedere ad AEM as a Cloud Service, tra cui:

* Nomi
* Indirizzi e-mail
* Ruoli e responsabilità

>[!TIP]
>
>Ai fini dell’onboarding, Adobe consiglia di aggiungere per primi gli utenti che parteciperanno alle attività fin da subito, come amministratori, sviluppatori e autori di contenuti.
>
>Puoi avanzare nel processo di onboarding senza aggiungere tutti gli utenti. Puoi aggiungere altri utenti dopo aver completato l’onboarding.

## Profili di prodotto {#product-profiles}

Quando consenti l’accesso a una soluzione Adobe agli utenti, non devi necessariamente concedere loro l’accesso completo. Con i profili di prodotto è possibile disporre per ogni soluzione di un set personalizzato di autorizzazioni utente che vengono impostate con Admin Console.

Ad esempio, più avanti in questo percorso utilizzerai Admin Console per consentire agli utenti di accedere alla soluzione AEM assegnando profili di prodotto a utenti amministratori e autori di AEM.

Tuttavia, il passaggio successivo consiste nell’assegnare i profili di prodotto in modo che i membri del gruppo possano anzitutto accedere a Cloud Manager.

## Cloud Manager {#cloud-manager}

In qualità di amministratore di sistema, sai bene che un progetto AEM as a Cloud Service di successo dipende non solo dalla creazione di contenuti straordinari con AEM, ma anche dallo sviluppo e dalla distribuzione del codice personalizzato e delle applicazioni utilizzati per pubblicare tali contenuti.

Cloud Manager è parte integrante di AEM as a Cloud Service e consente di gestire le pipeline CI/CD per la distribuzione del codice, la gestione degli archivi del codice e degli ambienti.

Prima che il team possa intraprendere operazioni, devi aver completato l’onboarding in Cloud Manager assegnando ai membri del team i profili di prodotto necessari. I passaggi successivi indicano dove trovare il profilo di prodotto Cloud Manager con Admin Console e come assegnarlo ai membri del gruppo.

## Revisione dei profili di prodotto di Cloud Manager {#review-product-profiles}

Tramite Admin Console è possibile visualizzare l’elenco dei profili di Cloud Manager.

1. Accedi a Adobe Admin Console all’indirizzo [adminconsole.adobe.com](https://adminconsole.adobe.com/) e, dalla pagina **Panoramica**, accedi alla scheda **Prodotti e servizi** e seleziona **Adobe Experience Manager as a Cloud Service**.

   ![Prodotto AEM as a Cloud Service](/help/journey-onboarding/assets/assign-team1.png)

1. Dall’elenco di tutte le istanze, accedi all’istanza di **Cloud Manager**.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Viene visualizzato l’elenco dei profili di prodotto preconfigurati per Cloud Manager.

   ![Profili di prodotto](/help/journey-onboarding/assets/assign-team3.png)

I profili più importanti da assegnare come parte del processo di onboarding iniziale sono:

* **Proprietario business**: questi utenti gestiscono diversi programmi.
* **Responsabile dell’implementazione**: questi utenti distribuiscono il codice dagli archivi agli ambienti AEM in esecuzione.
* **Sviluppatore**: questi utenti sviluppano le applicazioni AEM personalizzate ed eseguono il commit del codice negli archivi.

Tenendo a mente le caratteristiche di ogni ruolo e quali operazioni può svolgere, scorri l’elenco dei membri del gruppo per determinare a chi assegnare quale profilo. Tieni presente che gli utenti possono avere (e spesso hanno) più ruoli nel team, pertanto necessiteranno di più profili.

## Assegnazione del profilo di prodotto Proprietario business {#assign-business-owner}

Ora puoi aggiungere utenti e assegnarli al profilo di prodotto **Proprietario business**.

1. Identificare gli utenti che devono gestire i programmi di Cloud Manager. Questi sono i tuoi **Proprietari business**.

1. Accedi ad Admin Console dalla pagina `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` **Panoramica**, seleziona il prodotto **Adobe Experience Manager as a Cloud Service** nella scheda **Prodotti e servizi**.

   ![Prodotti e servizi](/help/journey-onboarding/assets/assign-team1.png)

1. Dalla navigazione superiore, seleziona la scheda **Utenti**, quindi **Aggiungi utente**.

   ![Aggiungi utente](/help/journey-onboarding/assets/assign-team4.png)

1. Nella finestra di dialogo **Aggiungi utenti al team**, inserisci l’ID e-mail dell’utente che desideri aggiungere.

   * Se il Federated ID dei membri del gruppo non è ancora stato configurato, come **Tipo ID** seleziona **Adobe ID**.

   ![Aggiungi dettagli utente](/help/journey-onboarding/assets/assign-team5.png)

1. Per selezionare il prodotto, fai clic sul pulsante Più sotto l’intestazione **Seleziona prodotti o gruppi di utenti**, quindi seleziona **Adobe Experience Manager as a Cloud Service** e assegna il profilo di prodotto **Proprietario business** all’utente.

   * Assegna a ogni utente almeno un profilo di prodotto in modo che possa accedere a Cloud Manager.
   * Ricordarti di assegnare te stesso o te stessa come amministratore di sistema al ruolo **Proprietario business**.

   ![Assegnazione utenti](/help/journey-onboarding/assets/assign-team6.png)

1. Fai clic su **Salva** per inviare un’e-mail di benvenuto all’utente aggiunto. L’utente invitato può accedere a Cloud Manager facendo clic sul collegamento nell’e-mail di benvenuto e accedendo con il proprio Adobe ID.

1. Ripeti questi passaggi per gli utenti del team.

Ora gli utenti sono stati assegnati al ruolo **Proprietario business** e possono accedere a Cloud Manager. Non dimenticare di assegnare anche te stesso o te stessa come amministratore di sistema al profilo **Proprietario business**.

## Assegnazione del profilo di prodotto Responsabile dell’implementazione {#assign-deployment-manager}

1. Identifica gli utenti che devono distribuire il codice.

1. Accedi a Admin Console all’indirizzo `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e, dalla pagina **Panoramica**, accedi alla scheda **Prodotti e servizi** e seleziona **Adobe Experience Manager as a Cloud Service**.

   ![Prodotti e servizi](/help/journey-onboarding/assets/assign-team1.png)

1. Dalla navigazione superiore, seleziona la scheda **Utenti**, quindi **Aggiungi utente**.

   ![Aggiungi utente](/help/journey-onboarding/assets/assign-team4.png)

1. Nella finestra di dialogo **Aggiungi utenti al team**, inserisci l’ID e-mail dell’utente che desideri aggiungere.

   * Se il Federated ID dei membri del gruppo non è ancora stato configurato, come **Tipo ID** seleziona **Adobe ID**.

   ![Inserisci ID](/help/journey-onboarding/assets/assign-team5.png)

1. Per selezionare il prodotto, fai clic sul pulsante Più sotto l’intestazione **Seleziona prodotti o gruppi di utenti**, quindi seleziona **Adobe Experience Manager as a Cloud Service** e assegna all’utente il profilo di prodotto **Responsabile dell’implementazione**.

   ![Assegna profilo](/help/journey-onboarding/assets/assign-team6.png)

Ora gli utenti sono stati assegnati ai ruoli **Responsabile dell’implementazione** e possono accedere a Cloud Manager. A seconda delle responsabilità future, potrebbe essere necessario assegnare te stesso o te stessa come amministratore di sistema anche al profilo **Responsabile dell’implementazione**.

## Assegnazione del profilo di prodotto Sviluppatore {#assign-developer}

1. Identifica gli utenti che devono sviluppare applicazioni AEM e gestire il codice.

1. Accedi a Admin Console all’indirizzo `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e, dalla pagina **Panoramica**, accedi alla scheda **Prodotti e servizi** e seleziona **Adobe Experience Manager as a Cloud Service**.

   ![Prodotti e servizi](/help/journey-onboarding/assets/assign-team1.png)

1. Dalla navigazione superiore, seleziona la scheda **Utenti**, quindi **Aggiungi utente**.

   ![Aggiungi utente](/help/journey-onboarding/assets/assign-team4.png)

1. Nella finestra di dialogo **Aggiungi utenti al team**, inserisci l’ID e-mail dell’utente che desideri aggiungere.

   * Se il Federated ID dei membri del gruppo non è ancora stato configurato, come **Tipo ID** seleziona **Adobe ID**.

   ![Aggiungi ID utente](/help/journey-onboarding/assets/assign-team5.png)

1. Per selezionare il prodotto, fai clic sul pulsante Più sotto l’intestazione **Seleziona prodotti o gruppi di utenti**, quindi seleziona **Adobe Experience Manager as a Cloud Service** e assegna all’utente il profilo di prodotto **Sviluppatore**.

   ![Assegna profilo](/help/journey-onboarding/assets/assign-team6.png).

Ora gli utenti sono stati assegnati ai ruoli **Sviluppatore** e possono accedere a Cloud Manager. A seconda delle responsabilità future, potrebbe essere necessario assegnare te stesso o te stessa come amministratore di sistema anche al profilo **Sviluppatore**.

## Passaggio successivo {#whats-next}

Congratulazioni. Il nuovo team Cloud Manager appena formato (che include il tuo utente assegnato al profilo **Proprietario business**) è stato configurato. Con il ruolo **Proprietario business**, ora sei a un passo dall’accesso a Cloud Manager e dalla creazione delle risorse cloud.

In questa parte del percorso di onboarding hai scoperto come assegnare i membri del gruppo ai profili in Admin Console. Ora dovresti:

* Sapere cosa sono i profili di prodotto.
* Sapere che cos’è Cloud Manager.
* Conoscere i tre importanti profili di prodotto di Cloud Manager: **Proprietario business**, **Responsabile dell’implementazione** e **Sviluppatore**.
* Saper assegnare i membri del gruppo ai profili di prodotto di Cloud Manager.

Ora puoi continuare il tuo percorso di onboarding passando al documento [Accesso a Cloud Manager](cloud-manager.md), dove verrà illustrato come accedere a Cloud Manager e creare le risorse del progetto.

## Risorse aggiuntive {#additional-resources}

È consigliabile continuare il percorso di onboarding nel modo descritto in precedenza. Queste sono alcune risorse aggiuntive utili se desideri approfondire un particolare argomento di questo percorso.

* [Introduzione a Cloud Manager](/help/onboarding/cloud-manager-introduction.md): informazioni su Cloud Manager, i programmi e gli ambienti di Cloud Manager.
* [Profili di prodotto di Cloud Manager](/help/onboarding/aem-cs-team-product-profiles.md): informazioni su team e profili di prodotto di AEM as a Cloud Service.
* [Tipi di identità su Adobe Admin Console](https://helpx.adobe.com/it/enterprise/admin-guide.html/enterprise/using/identity.ug.html): il sistema Identity Management di Adobe supporta gli amministratori nella creazione e nella gestione dell’accesso degli utenti ad applicazioni e servizi. Adobe offre questi tipi di identità o account per l’autenticazione e l’autorizzazione degli utenti.

