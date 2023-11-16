---
title: Concedere l’accesso allo sviluppatore front-end
description: Inserisci gli sviluppatori front-end in Cloud Manager in modo che abbiano accesso all'archivio git del sito AEM e alla pipeline.
exl-id: 58e95c92-b859-4bb9-aa62-7766510486fd
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 97%

---

# Concedere l’accesso allo sviluppatore front-end {#grant-fed-access}

Inserisci gli sviluppatori front-end in Cloud Manager in modo che abbiano accesso all&#39;archivio git del sito AEM e alla pipeline.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di Creazione Rapida dei Siti AEM, [Imposta La Pipeline,](pipeline-setup.md) hai imparato a creare una pipeline front-end per gestire la personalizzazione del tema sito e ora dovresti:

* Comprendere cos’è una pipeline front-end.
* Scoprire come impostare una pipeline front-end in Cloud Manager.

Ora devi concedere allo sviluppatore front-end l&#39;accesso a Cloud Manager attraverso il processo di onboarding, in modo che lo possa accedere all&#39;archivio git di AEM e alla pipeline creata.

## Obiettivo {#objective}

Il processo di concessione dell&#39;accesso a Cloud Manager e di assegnazione dei ruoli agli utenti si chiama onboarding. Questo documento fornisce una panoramica dei passaggi più importanti per l&#39;onboarding di uno sviluppatore front-end e dopo la lettura saprai:

* Come aggiungere uno sviluppatore front-end come utente.
* Come assegnare i ruoli richiesti allo sviluppatore front-end.

>[!TIP]
>
>È disponibile un intero percorso di documentazione dedicato all&#39;onboarding del team su AEM as a Cloud service, collegato alla [sezzione Risorse aggiuntive](#additional-resources) di questo documento, se necessiti di ulteriori dettagli sul processo.

## Ruolo responsabile {#responsible-role}

Questa parte del percorso si applica all’amministratore di Cloud Manager.

## Requisiti  {#requirements}

* Devi essere membro col ruolo di **Proprietario dell&#39;azienda** in Cloud Manager.
* Devi essere un **Amministratore di sistema** in Cloud Manager.
* Devi avere accesso all&#39;Admin Console.

## Aggiungere uno sviluppatore front-end come utente {#add-fed-user}

Innanzitutto devi aggiungere lo sviluppatore front-end come utente utilizzando l’Admin Console.

1. Accedi all’Admin Console in [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).

1. Una volta effettuato l’accesso, viene visualizzata una pagina di panoramica simile a quella riportata di seguito.

   ![Panoramica di Admin Console](assets/admin-console.png)

1. Accertati di essere nell’organizzazione appropriata, controllandone il nome nell’angolo in alto a destra dello schermo.

   ![Controlla il nome dell&#39;organizzazione](assets/correct-org.png)

1. Seleziona **Adobe Experience Manager as a Cloud Service** dalla scheda **Prodotti e servizi**.

   ![Seleziona AEMaaCS](assets/select-aemaacs.png)

1. Vedrai l’elenco dei profili di prodotto Cloud Manager preconfigurati. Se questi profili non sono visualizzati, contatta l’amministratore di Cloud Manager in quanto potresti non disporre delle autorizzazioni corrette nell’organizzazione.

   ![Profili di prodotto](assets/product-profiles.png)

1. Per assegnare lo sviluppatore front-end ai profili corretti, tocca o fai clic sul pulsante **Utenti** e quindi la scheda **Aggiungi utente** pulsante.

   ![Aggiungi utente](assets/add-user.png)

1. Nella finestra di dialogo **Aggiungi utenti al tuo team** digita l&#39;ID e-mail dell&#39;utente che desideri aggiungere. Per Tipo ID, seleziona Adobe ID se il Federated ID per i membri del team non è ancora stato configurato.

   ![Aggiungi utente al team](assets/add-to-team.png)

1. Nella selezione **Prodotto**, tocca o fai clic sul segno più, quindi seleziona **Adobe Experience Manager come servizio cloud** e assegna all&#39;utente i profili di prodotto **Gestione distribuzione** e **Sviluppatore**.

   ![Assegnare profili team](assets/assign-team.png)

1. Tocca o fai clic su **Salva** e un messaggio e-mail di benvenuto viene inviato allo sviluppatore front-end aggiunto come utente.

Lo sviluppatore front-end invitato può accedere a Cloud Manager facendo clic sul collegamento nell’e-mail di benvenuto e accedendo utilizzando il proprio Adobe ID.

## Consegna allo sviluppatore Front-End {#handover}

Con un invito e-mail a Cloud Manager per lo sviluppatore front-end, tu e l’amministratore AEM potete fornirgli le informazioni necessarie rimanenti per iniziare la personalizzazione.

* Un [percorso del contenuto tipico](#example-page)
* Il sorgente del tema che [hai scaricato](#download-theme)
* Le [credenziali utente proxy](#proxy-user)
* Il nome del programma o l&#39;URL a esso associato [copiato da Cloud Manager](pipeline-setup.md#login)
* Requisiti di progettazione front-end

## Novità {#what-is-next}

Dopo aver completato questa parte del percorso di Creazione Rapida dei Siti AEM, dovresti conoscere:

* Come aggiungere uno sviluppatore front-end come utente.
* Come assegnare i ruoli richiesti allo sviluppatore front-end.

Approfondisci questo argomento e continua il percorso di Creazione Rapida dei Siti AEM consultando il documento [Recuperare le informazioni di accesso all’archivio Git,](retrieve-access.md) che descrive la prospettiva dello sviluppatore front-end e spiega come utilizzare Cloud Manager per accedere alle informazioni dell’archivio git.

## Risorse aggiuntive {#additional-resources}

Sebbene sia consigliabile passare alla parte successiva del percorso di Creazione Rapida dei Siti consultando il documento [Recupero delle credenziali dello sviluppatore Front-End,](retrieve-access.md) le seguenti sono alcune risorse aggiuntive e opzionali che approfondiscono alcuni concetti menzionati in questo documento, ma non sono necessarie per continuare il percorso.

* [Percorso di onboarding](/help/journey-onboarding/overview.md): questa guida funge da punto di partenza per garantire che i team siano configurati e abbiano accesso a AEM as a Cloud Service.
