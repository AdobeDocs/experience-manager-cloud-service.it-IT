---
title: Assegnazione di membri del team ai profili di prodotto di Cloud Manager
description: Segui questa pagina per scoprire come assegnare i membri del team ai profili di prodotto di Cloud Manager
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 1%

---

# Assegnare membri del team ai profili di prodotto di Cloud Manager {#assign-team-members}

Nel passaggio precedente di questo percorso, [Guida introduttiva al processo di onboarding](/help/journey-onboarding/sysadmin/get-started-onboarding-journey.md), hai appreso l’accesso all’Admin Console e hai visualizzato i tuoi privilegi come amministratore di sistema. Ora puoi assegnare i membri del team ai profili di prodotto Cloud Manager.

## Obiettivo {#objective}

In questo documento viene riepilogato come assegnare i membri del team ai profili di prodotto di Cloud Manager da Adobe Admin Console. Una volta assegnati, questi membri possono quindi creare una risorsa cloud di accesso come descritto nel passaggio successivo di questo percorso.

Dopo aver letto questa sezione dovresti essere in grado di:

* Scopri perché e come aggiungere i membri del team.
* Scopri tre importanti profili di prodotto di Cloud Manager: **Proprietario business**, **Gestione distribuzione** e **Sviluppatore**.
* Assegna membri del team ai profili di prodotto di Cloud Manager.

>[!TIP]
>
>Ai fini dell’onboarding, Adobe ti consigliamo inizialmente di aggiungere utenti che parteciperanno alle attività immediate, come amministratori, sviluppatori e autori di contenuti. Puoi continuare il processo di onboarding senza aggiungere tutti gli utenti. Dopo aver completato l’onboarding, puoi aggiungere altri utenti.

## Prerequisiti {#prerequisites}

Prima di avviare questa sezione, è necessario soddisfare i seguenti prerequisiti. Devi:

* Sii amministratore di sistema e comprendi i profili di prodotto di Cloud Manager.
   * Torna a [Panoramica sul Percorso di onboarding](onboarding-journey-overview.md) se questi concetti non sono noti.
* Nozioni di base su Adobe Admin Console.
   * Torna a [Panoramica sul Percorso di onboarding](onboarding-journey-overview.md) se questi concetti non sono noti.
* Dispone di dettagli sui membri del team, che dovranno accedere AEM as a Cloud Service, tra cui
   * Nomi
   * Indirizzi e-mail
   * Ruoli e responsabilità

## Esamina i profili di prodotto di Cloud Manager {#review-product-profiles}

Dall’Adobe Admin Console puoi vedere l’elenco dei profili di Cloud Manager.

1. Accedi a Adobe Admin Console all&#39;indirizzo [adminconsole.adobe.com](https://adminconsole.adobe.com/) e dal **Panoramica** pagina, seleziona **Adobe Experience Manager as a Cloud Service** dal **Prodotti e servizi** il Card.

   ![AEM come prodotto](/help/journey-onboarding/assets/assign-team1.png)

1. Passa a **Cloud Manager** dall’elenco di tutte le istanze.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Verrà visualizzato l’elenco dei profili di prodotto Cloud Manager preconfigurati.

   ![Profili di prodotto](/help/journey-onboarding/assets/assign-team3.png)

## Assegnare utenti al profilo di prodotto proprietario business {#assign-users-business-owner}

Ora puoi aggiungere utenti e assegnarli al **Proprietario business** profilo di prodotto.

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto Proprietario business.

1. Accedi all&#39;Admin Console all&#39;indirizzo [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) e **Panoramica** pagina, seleziona **Adobe Experience Manager as a Cloud Service** prodotto da **Prodotti e servizi** il Card.

   ![Prodotti e servizi](/help/journey-onboarding/assets/assign-team1.png)

1. Seleziona la **Utenti** scheda dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![Aggiungi utente](/help/journey-onboarding/assets/assign-team4.png)

1. In **Aggiungi utenti al tuo team** , immetti l’ID e-mail dell’utente che desideri aggiungere.

   * Se l&#39;ID federato per i membri del team non è ancora stato impostato, seleziona **Adobe ID** per **Tipo di ID**.

   ![Aggiungi dettagli utente](/help/journey-onboarding/assets/assign-team5.png)

1. Fai clic sul pulsante più sotto il pulsante **Selezionare prodotti o gruppi di utenti** intestazione per iniziare la selezione del prodotto e selezionare **Adobe Experience Manager as a Cloud Service** e assegnare **Proprietario business** profilo di prodotto per l’utente.

   * Assegna a ogni utente almeno un profilo di prodotto in modo che l’utente possa accedere a Cloud Manager.
   * Ricordarsi di assegnarsi come amministratore di sistema al **Proprietario business** ruolo.

   ![Assegnazione degli utenti](/help/journey-onboarding/assets/assign-team6.png)

1. Fai clic su **Salva** e viene inviata un’e-mail di benvenuto all’utente aggiunto. L’utente invitato può accedere a Cloud Manager facendo clic sul collegamento presente nell’e-mail di benvenuto e accedendo utilizzando il proprio Adobe ID.

1. Ripeti questi passaggi per gli utenti del tuo team.

Il nuovo team Cloud Manager (incluso l’utente assegnato a **Proprietario business** role) è stato impostato. Nel ruolo di **Proprietario business**, ora sei a un solo passo dall’accesso a Cloud Manager e dall’abilitazione della creazione di risorse cloud.

## Assegnare utenti al profilo di prodotto di Deployment Manager {#assign-users-deployment-manager}

1. Identifica gli utenti che gestiranno i programmi Cloud Manager e li aggiungerà al profilo di prodotto di Deployment Manager.

1. Accedi all&#39;Admin Console all&#39;indirizzo [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) e **Panoramica** selezione pagina **Adobe Experience Manager as a Cloud Service** del prodotto **Prodotti e servizi** il Card.

   ![Prodotti e servizi](/help/journey-onboarding/assets/assign-team1.png)

1. Seleziona la **Utenti** scheda dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![Aggiungi utente](/help/journey-onboarding/assets/assign-team4.png)

1. In **Aggiungi utenti al tuo team** , immetti l’ID e-mail dell’utente che desideri aggiungere.

   * Se l&#39;ID federato per i membri del team non è ancora stato impostato, seleziona **Adobe ID** per **Tipo di ID**.

   ![Immetti ID](/help/journey-onboarding/assets/assign-team5.png)

1. Fai clic sul pulsante più sotto il pulsante **Selezionare prodotti o gruppi di utenti** intestazione per iniziare la selezione del prodotto e selezionare **Adobe Experience Manager as a Cloud Service** e assegnare **Gestione distribuzione** profilo di prodotto per l’utente.

   ![Assegna profilo](/help/journey-onboarding/assets/assign-team6.png).

## Assegnare utenti al profilo di prodotto per sviluppatori {#assign-users-developer}

1. Identifica gli utenti che gestiranno i programmi Cloud Manager.

1. Accedi all&#39;Admin Console all&#39;indirizzo [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) e **Panoramica** selezione pagina **Adobe Experience Manager as a Cloud Service** del prodotto **Prodotti e servizi** il Card.

   ![Prodotti e servizi](/help/journey-onboarding/assets/assign-team1.png)

1. Seleziona la **Utenti** scheda dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![Aggiungi utente](/help/journey-onboarding/assets/assign-team4.png)

1. In **Aggiungi utenti al tuo team** , immetti l’ID e-mail dell’utente che desideri aggiungere.

   * Se l&#39;ID federato per i membri del team non è ancora stato impostato, seleziona **Adobe ID** per **Tipo di ID**.

   ![Aggiungi ID utente](/help/journey-onboarding/assets/assign-team5.png)

1. Fai clic sul pulsante più sotto il pulsante **Selezionare prodotti o gruppi di utenti** intestazione per iniziare la selezione del prodotto e selezionare **Adobe Experience Manager as a Cloud Service** e assegnare **Sviluppatore** profilo di prodotto per l’utente.

   ![Assegna profilo](/help/journey-onboarding/assets/assign-team6.png).

## Novità {#whats-next}

In questa parte del percorso di onboarding hai imparato tutto sull’assegnazione dei membri del team ai ruoli nell’Admin Console. Ora dovresti:

* Scopri perché e come aggiungere i membri del team.
* Scopri tre importanti profili di prodotto di Cloud Manager: **Proprietario business**, **Gestione distribuzione** e **Sviluppatore**.
* Puoi assegnare i membri del team ai profili di prodotto di Cloud Manager.

È ora possibile continuare il percorso di onboarding passando alla revisione successiva del documento [Configurare le risorse Cloud tramite Cloud Manager](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md), dove imparerai:

1. Per gli altri proprietari business per la creazione di programmi, in qualità di amministratore di sistema assegnato a **Proprietario business** , deve prima accedere a Cloud Manager e accedervi.
1. Come un utente con **Proprietario business** Il ruolo può accedere e configurare le risorse cloud, inclusi il programma cloud e gli ambienti.
1. Come gli utenti con **Sviluppatore** e **Gestione distribuzione** I ruoli possono accedere a Cloud Manager.

## Risorse aggiuntive {#additional-resources}

È consigliabile continuare sul percorso di onboarding come descritto in precedenza. Queste sono alcune risorse aggiuntive se desideri effettuare un&#39;immersione approfondita su un particolare argomento da questo percorso.

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Panoramica su Admin Console Identity](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
