---
title: Assegnazione di membri del team ai profili di prodotto di Cloud Manager
description: Segui questa pagina per scoprire come assegnare i membri del team ai profili di prodotto di Cloud Manager
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 2%

---


# Assegnare membri del team ai profili di prodotto di Cloud Manager {#assign-team-members}

In questa parte del [percorso di bordo,](overview.md) imparerai a assegnare i membri del team ai profili di prodotto di Cloud Manager.

## Obiettivo {#objective}

Nel passaggio precedente di questo percorso, [Accesso all’Admin Console,](admin-console.md) hai appreso l’accesso all’Admin Console e verifica i privilegi come amministratore di sistema. Ora puoi consentire ai membri del tuo team di accedere a Cloud Manager. A tale scopo, assegna profili di prodotto.

Quando si concede agli utenti l&#39;accesso a una soluzione di Adobe, non si desidera necessariamente concedere loro l&#39;accesso completo. I profili di prodotto consentono a ogni soluzione di disporre di un proprio set di autorizzazioni utente. Utilizza l’Admin Console per assegnare profili di prodotto.

Il primo passaggio consiste nel concedere agli utenti l’accesso a Cloud Manager. Cloud Manager ti supporta con le configurazioni di sviluppo aziendale e le sue pipeline CI/CD appositamente progettate, che sono dotate per garantire test approfonditi e la massima qualità del codice per fornire esperienze eccezionali.

Dopo aver letto questo documento, dovresti:

* Scopri i profili di prodotto.
* Scopri cos’è Cloud Manager.
* Scopri i tre importanti profili di prodotto di Cloud Manager: **Proprietario business**, **Gestione distribuzione** e **Sviluppatore**.
* Puoi assegnare i membri del team ai profili di prodotto di Cloud Manager.

## Prerequisiti {#prerequisites}

Per assegnare i membri del team ai profili di prodotto, dovrai disporre di dettagli sui membri del team, che dovranno accedere AEM as a Cloud Service, tra cui:

* Nomi
* Indirizzi e-mail
* Ruoli e responsabilità

>[!TIP]
>
>Ai fini dell’onboarding, Adobe consiglia di aggiungere inizialmente utenti che parteciperanno alle attività immediate, ad esempio amministratori, sviluppatori e autori di contenuti.
>
>Puoi continuare il processo di onboarding senza aggiungere tutti gli utenti. Dopo aver completato l’onboarding, puoi aggiungere altri utenti.

## Profili di prodotto {#product-profiles}

Quando si concede agli utenti l&#39;accesso a una soluzione di Adobe, non si desidera necessariamente concedere loro l&#39;accesso completo. I profili di prodotto consentono a ogni soluzione di disporre di un proprio set di autorizzazioni utente impostate utilizzando l’Admin Console .

Ad esempio, più avanti in questo percorso utilizzerai l’Admin Console per consentire agli utenti di accedere alla soluzione AEM assegnando profili di prodotto agli amministratori AEM e agli autori di AEM.

Tuttavia, il passaggio successivo consiste nel concedere i profili di prodotto in modo che i membri del team abbiano prima accesso a Cloud Manager.

## Cloud Manager {#cloud-manager}

In qualità di amministratore di sistema, sai che un progetto AEM as a Cloud Service di successo dipende non solo dalla creazione di contenuti straordinari utilizzando AEM, ma anche dallo sviluppo e dalla distribuzione di codice personalizzato e applicazioni per distribuire i contenuti AEM.

Cloud Manager è parte integrante di AEM as a Cloud Service e viene utilizzato per gestire le pipeline CI/CD per la distribuzione del codice, gestire gli archivi di codice e gli ambienti.

Prima di eseguire qualsiasi altra operazione, il team deve essere integrato in Cloud Manager concedendo loro i profili di prodotto necessari. I passaggi successivi mostrano dove trovare il profilo di prodotto Cloud Manager utilizzando l’Admin Console e come assegnarlo ai membri del team.

## Esamina i profili di prodotto di Cloud Manager {#review-product-profiles}

Utilizzando l’Admin Console puoi visualizzare l’elenco dei profili di Cloud Manager.

1. Accedi a Adobe Admin Console all&#39;indirizzo [adminconsole.adobe.com](https://adminconsole.adobe.com/) e dal **Panoramica** pagina, seleziona **Adobe Experience Manager as a Cloud Service** dal **Prodotti e servizi** il Card.

   ![AEM come prodotto](/help/journey-onboarding/assets/assign-team1.png)

1. Passa a **Cloud Manager** dall’elenco di tutte le istanze.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Verrà visualizzato l’elenco dei profili di prodotto Cloud Manager preconfigurati.

   ![Profili di prodotto](/help/journey-onboarding/assets/assign-team3.png)

I profili più importanti da assegnare come parte del processo di onboarding iniziale sono:

* **Proprietario business** - Questi utenti gestiscono programmi diversi.
* **Gestione distribuzione** - Questi utenti distribuiscono il codice dagli archivi agli ambienti AEM in esecuzione.
* **Sviluppatore** - Questi utenti sviluppano le applicazioni AEM personalizzate e eseguono il commit del codice negli archivi.

Sapendo cosa sono questi ruoli e cosa fanno, controlla l’elenco dei membri del team per determinare chi ha bisogno di quale profilo. Tieni presente che gli utenti possono avere e spesso hanno più ruoli nel tuo team e quindi hanno anche bisogno di più profili.

## Assegnare il profilo di prodotto del proprietario dell&#39;azienda {#assign-business-owner}

Ora puoi aggiungere utenti e assegnarli al **Proprietario business** profilo di prodotto.

1. Identifica gli utenti che devono gestire i programmi Cloud Manager. Questi saranno i vostri **Proprietari aziendali**.

1. Accedi all&#39;Admin Console all&#39;indirizzo `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e **Panoramica** pagina, seleziona **Adobe Experience Manager as a Cloud Service** prodotto da **Prodotti e servizi** il Card.

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

Le **Proprietario business** Sono stati assegnati e ora possono accedere a Cloud Manager. Non dimenticare di assegnarti anche come amministratore di sistema al **Proprietario business** profilo.

## Assegnare il profilo di prodotto di Deployment Manager {#assign-deployment-manager}

1. Identifica gli utenti che devono distribuire il codice.

1. Accedi all&#39;Admin Console all&#39;indirizzo `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e **Panoramica** selezione pagina **Adobe Experience Manager as a Cloud Service** del prodotto **Prodotti e servizi** il Card.

   ![Prodotti e servizi](/help/journey-onboarding/assets/assign-team1.png)

1. Seleziona la **Utenti** scheda dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![Aggiungi utente](/help/journey-onboarding/assets/assign-team4.png)

1. In **Aggiungi utenti al tuo team** , immetti l’ID e-mail dell’utente che desideri aggiungere.

   * Se l&#39;ID federato per i membri del team non è ancora stato impostato, seleziona **Adobe ID** per **Tipo di ID**.

   ![Immetti ID](/help/journey-onboarding/assets/assign-team5.png)

1. Fai clic sul pulsante più sotto il pulsante **Selezionare prodotti o gruppi di utenti** intestazione per iniziare la selezione del prodotto e selezionare **Adobe Experience Manager as a Cloud Service** e assegnare **Gestione distribuzione** profilo di prodotto per l’utente.

   ![Assegna profilo](/help/journey-onboarding/assets/assign-team6.png)

Le **Gestione distribuzione** Sono stati assegnati e ora possono accedere a Cloud Manager. A seconda delle responsabilità future, potrebbe essere necessario assegnare l&#39;amministratore di sistema anche a **Gestione distribuzione** profilo.

## Assegnare il profilo di prodotto per sviluppatori {#assign-developer}

1. Identifica gli utenti che devono sviluppare applicazioni AEM e gestire il codice.

1. Accedi all&#39;Admin Console all&#39;indirizzo `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e **Panoramica** selezione pagina **Adobe Experience Manager as a Cloud Service** del prodotto **Prodotti e servizi** il Card.

   ![Prodotti e servizi](/help/journey-onboarding/assets/assign-team1.png)

1. Seleziona la **Utenti** scheda dalla navigazione in alto, quindi seleziona **Aggiungi utente**.

   ![Aggiungi utente](/help/journey-onboarding/assets/assign-team4.png)

1. In **Aggiungi utenti al tuo team** , immetti l’ID e-mail dell’utente che desideri aggiungere.

   * Se l&#39;ID federato per i membri del team non è ancora stato impostato, seleziona **Adobe ID** per **Tipo di ID**.

   ![Aggiungi ID utente](/help/journey-onboarding/assets/assign-team5.png)

1. Fai clic sul pulsante più sotto il pulsante **Selezionare prodotti o gruppi di utenti** intestazione per iniziare la selezione del prodotto e selezionare **Adobe Experience Manager as a Cloud Service** e assegnare **Sviluppatore** profilo di prodotto per l’utente.

   ![Assegna profilo](/help/journey-onboarding/assets/assign-team6.png).

Le **Sviluppatore** Sono stati assegnati e ora possono accedere a Cloud Manager. A seconda delle responsabilità future, potrebbe essere necessario assegnare l&#39;amministratore di sistema anche a **Sviluppatore** profilo.

## Novità {#whats-next}

Congratulazioni! Il nuovo team Cloud Manager (incluso l’utente assegnato a **Proprietario business** profile) è stato impostato. Nel ruolo di **Proprietario business**, ora sei a un solo passo dall’accesso a Cloud Manager e dall’abilitazione della creazione di risorse cloud.

In questa parte del percorso di onboarding hai appreso come assegnare i membri del team ai profili nell’Admin Console. Ora dovresti:

* Scopri i profili di prodotto.
* Scopri cos’è Cloud Manager.
* Scopri i tre importanti profili di prodotto di Cloud Manager: **Proprietario business**, **Gestione distribuzione** e **Sviluppatore**.
* Puoi assegnare i membri del team ai profili di prodotto di Cloud Manager.

È ora possibile continuare il percorso di onboarding passando alla revisione successiva del documento [Access Cloud Manager,](cloud-manager.md) dove scoprirai come accedere a Cloud Manager e creare le risorse del tuo progetto.

## Risorse aggiuntive {#additional-resources}

È consigliabile continuare sul percorso di onboarding come descritto in precedenza. Queste sono alcune risorse aggiuntive se desideri effettuare un&#39;immersione approfondita su un particolare argomento da questo percorso.

* [Introduzione a Cloud Manager](/help/onboarding/cloud-manager-introduction.md) - Informazioni su Cloud Manager, i programmi e gli ambienti Cloud Manager.
* [Profili di prodotto di Cloud Manager](/help/onboarding/aem-cs-team-product-profiles.md) - Scopri AEM profili team e di prodotto as a Cloud Service.
* [Tipi di identità in Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html) - Il sistema di gestione delle identità di Adobe consente agli amministratori di creare e gestire l’accesso degli utenti alle applicazioni e ai servizi. Adobe offre questi tipi di identità o account per autenticare e autorizzare gli utenti.

