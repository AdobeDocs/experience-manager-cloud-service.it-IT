---
title: Assegnazione dei profili di prodotto di AEM
description: Dopo aver configurato le risorse cloud, devi fornire al team l’accesso ad AEM tramite i profili di prodotto di AEM.
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 100%

---

# Assegnazione dei profili di prodotto di AEM {#assign-profiles-aem}

>[!CONTEXTUALHELP]
>id="assets_user_entitlements"
>title="Assegnare profili di prodotto AEM"
>abstract="Non disponi dei diritti necessari per utilizzare Experience Manager Assets. Contatta l’amministratore."

In questa sezione del [percorso di onboarding](overview.md) scoprirai come fornire al team l’accesso ad AEM con i profili di prodotto di AEM.

## Obiettivo {#objective}

Dopo aver letto il documento precedente in questo percorso di onboarding, [Creazione di ambienti,](create-environments.md) e aver configurato le risorse cloud, devi fornire al team l’accesso ad AEM con i profili di prodotto di AEM. Come amministratore di sistema, puoi eseguire l’operazione assegnando i profili di prodotto di AEM.

Dopo aver letto questo documento saprai:

* Quali sono i profili di prodotto di AEM.
* Come aggiungere membri del gruppo al profilo di prodotto Utente AEM.
* Come aggiungere membri del gruppo al profilo di prodotto Amministratori AEM.

## Profili di prodotto di AEM {#aem-product-profiles}

Per utilizzare AEM, i membri del gruppo devono essere assegnati ad almeno un profilo di prodotto AEM. Le autorizzazioni per accedere a Cloud Manager non sono sufficienti. Gli utenti devono essere stati assegnati a uno dei seguenti profili di prodotto:

* `AEM Users`: questo gruppo include gli utenti normali che eseguono attività quotidiane di authoring dei contenuti.
* `AEM Administrators`: questo gruppo include gli utenti responsabili delle funzioni avanzate o AEM.

>[!NOTE]
>
>Ogni utente assegnato a un profilo di prodotto di AEM as a Cloud Service ha accesso in sola lettura a Cloud Manager tramite il ruolo **Utente di Cloud Manager**.
>
>Gli utenti con solo il ruolo Utente di **Cloud Manager** possono accedere a Cloud Manager e passare agli ambienti di authoring di AEM (se esistono) utilizzando le opzioni del menu Programmi. Il ruolo **Utente di Cloud Manager** non è sufficiente per accedere ai dettagli dei programmi. Se tale accesso è necessario, l’amministratore di sistema deve assegnare agli utenti ruoli aggiuntivi.
>Consulta la [sezione delle risorse aggiuntive più avanti](#additional-resources) per ulteriori informazioni sui ruoli utente di Cloud Manager.

>[!CAUTION]
>
>Non modificare o eliminare i profili di prodotto denominati Amministratori AEM o Utenti AEM. La modifica di questi nomi di profilo può interrompere l’accesso all’istanza cloud AEM.

## Prerequisiti {#prerequisites}

Prima di iniziare a leggere questa sezione, è necessario disporre delle seguenti informazioni sul team che utilizzerà AEM.

* Nomi
* Indirizzi e-mail
* Ruoli e responsabilità

>[!TIP]
>
>Ai fini dell’onboarding, Adobe consiglia di aggiungere per primi gli utenti che parteciperanno alle attività fin da subito, come amministratori, sviluppatori e autori di contenuti. Puoi avanzare nel resto del processo di onboarding senza aggiungere tutti gli utenti. Potrai aggiungerne di più in un secondo momento, dopo aver completato l’onboarding.

## Visualizzazione dei profili di prodotto di AEM {#view-profiles}

Per visualizzare i profili di prodotto di AEM da Admin Console, segui la procedura riportata di seguito.

1. Accedi a Admin Console all’indirizzo [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. Dalla pagina **Panoramica**, accedi alla scheda **Prodotti e servizi** e seleziona **Adobe Experience Manager as a Cloud Service**.

   ![Scheda Prodotti e servizi](/help/journey-onboarding/assets/assign-team1.png)

1. Accedi all’istanza e selezionala.

   ![Selezione dell’istanza](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. Viene visualizzato l’elenco dei profili di prodotto di AEM as a Cloud Service che è possibile assegnare a un utente in base al ruolo.

   ![Profili di prodotto](/help/journey-onboarding/assets/cloud-profiles-2.png)

## Aggiunta dei membri del gruppo ai profili di prodotto {#add-team-members}

Ora che sai quali profili sono disponibili, puoi assegnarli ai membri del gruppo in base alle esigenze.

Per queste attività è necessario essere amministratori di sistema con il profilo di prodotto di Cloud Manager **Proprietario business**.

1. Da Cloud Manager, accedi al tuo programma e seleziona il pulsante **Gestisci accesso** dal contesto dell’ambiente di interesse.

   ![Gestisci accesso](/help/journey-onboarding/assets/add-team1.png)

1. Si apre nuova scheda di Admin Console, da cui puoi accedere all’istanza di Author dell’ambiente. Seleziona **Amministratori AEM** o **Utenti AEM** in base alle autorizzazioni da assegnare a questo utente.

   ![Assegnazione dell’accesso](/help/journey-onboarding/assets/add-team2.png)

1. Seleziona `AEM Administrator` o `AEM User` e fai clic su **Aggiungi utente** come mostrato di seguito, quindi inserisci i dettagli necessari per completare l’aggiunta del membro del team.

   ![Aggiunta di un membro del team](/help/journey-onboarding/assets/add-team3.png)

1. Se disponi delle informazioni dei membri del gruppo che necessitano dell’accesso, ripeti questi passaggi per tutti gli ambienti, inclusi quelli di sviluppo, staging e produzione.

L’utente aggiunto ora ha accesso ai servizi di Author di AEM as a Cloud Service.

## Fine del percorso? {#the-end}

Congratulazioni. Gli utenti assegnati ai profili di prodotto di AEM as a Cloud Service ora possono accedere all’ambiente di authoring di AEM e iniziare a creare contenuti con AEM as a Cloud Service. Analogamente, ora i team di sviluppo possono accedere a Cloud Manager per utilizzare Git per archiviare il codice dell’applicazione personalizzato e distribuirlo. In questo senso, il tuo percorso di onboarding è completo e gli utenti dell’organizzazione ora possono utilizzare AEMaaCS.

Tuttavia, se desideri comprendere meglio l’utilizzo del sistema dalla prospettiva dei ruoli Autore e Sviluppatore, puoi continuare con due parti facoltative di questo percorso di onboarding:

* [Attività dei ruoli Sviluppatore e Responsabile della distribuzione](developers.md): scoprirai in che modo i team di sviluppo possono accedere a Git per archiviare il codice personalizzato e distribuirlo con le pipeline di Cloud Manager.
* [Attività degli Utenti AEM](aem-users.md): scoprirai come accedere all’ambiente AEM e iniziare a creare contenuti.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate risorse aggiuntive e opzionali utili per andare oltre il contenuto del percorso di onboarding.

* [Team e profili di prodotto di AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md): scopri come usare i team e i profili di prodotto di AEM as a Cloud Service per concedere e limitare l’accesso alle soluzioni di Adobe con licenza.
* [Gestione di prodotti e accesso degli utenti in Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console): scopri come gestire l’accesso degli utenti con Admin Console.
* [Procedura guidata per la configurazione dell’accesso a AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=it): una procedura guidata semplificata per scoprire come configurare utenti Adobe IMS, gruppi di utenti e profili di prodotto in Admin Console.

