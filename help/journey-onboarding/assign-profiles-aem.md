---
title: Assegnazione di profili di prodotto AEM
description: Dopo aver configurato le risorse cloud, dovrai concedere al team l’accesso a AEM tramite i profili di prodotto AEM.
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---

# Assegnazione di profili di prodotto AEM {#assign-profiles-aem}

In questa parte del [percorso di bordo,](overview.md) imparerai come concedere al team l’accesso a AEM utilizzando AEM profili di prodotto.

## Obiettivo {#objective}

Dopo aver letto il documento precedente in questo percorso di onboarding, [Creare ambienti,](create-environments.md) e aver configurato le risorse cloud, dovrai concedere al team l’accesso a AEM stesso utilizzando AEM profili di prodotto. In qualità di amministratore di sistema, puoi farlo assegnando AEM profili di prodotto.

Dopo aver letto questo documento è necessario comprendere:

* Quali sono i profili di prodotto AEM.
* Come aggiungere membri del team al profilo di prodotto AEM utente.
* Come aggiungere membri del team al profilo di prodotto Amministratori AEM.

## Profili di prodotto AEM {#aem-product-profiles}

Per utilizzare AEM, i membri del team devono essere assegnati ad almeno un profilo di prodotto AEM. Le autorizzazioni per accedere a Cloud Manager non sono sufficienti. Gli utenti devono appartenere a uno dei due profili di prodotto:

* `AEM Users` - Questo gruppo include gli utenti normali che eseguono attività quotidiane di authoring dei contenuti.
* `AEM Administrators` - Questo gruppo include gli utenti responsabili di funzioni o AEM avanzate.

Anche ogni utente assegnato a un profilo di prodotto AEM avrà accesso in sola lettura a Cloud Manager. L’accesso in scrittura a Cloud Manager può essere concesso tramite altri profili di prodotto.

## Prerequisiti {#prerequisites}

Prima di iniziare a leggere questa sezione, è necessario disporre delle seguenti informazioni sul team che utilizzerà AEM.

* Nomi
* Indirizzi e-mail
* Ruoli e responsabilità

>[!TIP]
>
>Ai fini dell’onboarding, è consigliabile aggiungere inizialmente utenti che parteciperanno alle attività immediate, come amministratori, sviluppatori e autori di contenuti. Puoi continuare il resto dell’onboarding senza aggiungere tutti gli utenti. Dopo aver completato l’onboarding, puoi scalare un numero maggiore di utenti in un secondo momento.

## Visualizzare AEM profili di prodotto {#view-profiles}

Segui questi passaggi per visualizzare i profili di prodotto AEM dall’Admin Console.

1. Accedi all&#39;Admin Console in [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. Da **Panoramica** pagina, seleziona **Adobe Experience Manager as a Cloud Service** dal **Prodotti e servizi** il Card.

   ![Scheda prodotti e servizi](/help/journey-onboarding/assets/assign-team1.png)

1. Passa all’istanza e selezionala.

   ![Seleziona istanza](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. Verrà visualizzato l’elenco dei profili di prodotto as a Cloud Service che possono essere assegnati a un utente in base ai loro ruoli.

   ![Profili di prodotto](/help/journey-onboarding/assets/cloud-profiles-2.png)

## Aggiungi membri del team ai profili di prodotto {#add-team-members}

Ora che conosci i profili disponibili, puoi assegnarli in base alle esigenze ai membri del team.

Per queste attività è necessario essere amministratori di sistema con **Proprietario business** Profilo di prodotto di Cloud Manager.

1. Passa al programma da Cloud Manager e seleziona la **Gestisci accesso** dal contesto di interesse.

   ![Gestire l&#39;accesso](/help/journey-onboarding/assets/add-team1.png)

1. Una nuova scheda ti porta all’Admin Console da cui hai accesso all’istanza di authoring dell’ambiente. Seleziona **Amministratori AEM** o **Utenti AEM** in base alle autorizzazioni di cui questa persona deve disporre.

   ![Assegna accesso](/help/journey-onboarding/assets/add-team2.png)

1. Seleziona `AEM Administrator` o `AEM User` e fai clic su **Aggiungi utente** come mostrato di seguito e invia i dettagli necessari per completare l’aggiunta del membro del team.

   ![Aggiungi membro del team](/help/journey-onboarding/assets/add-team3.png)

1. Ripeti questi passaggi per tutti gli ambienti, inclusi quelli di sviluppo, staging e produzione, se disponi delle informazioni dei membri del team che necessitano dell’accesso disponibili.

L’utente aggiunto avrà ora accesso ai AEM servizi di authoring as a Cloud Service.

## Fine del percorso? {#the-end}

Congratulazioni! Gli utenti assegnati a AEM profili di prodotto as a Cloud Service sono ora pronti per accedere all’ambiente di authoring di AEM e iniziare a creare contenuti con AEM as a Cloud Service. Allo stesso modo, gli sviluppatori ora possono accedere a Cloud Manager per utilizzare git per memorizzare il codice dell’applicazione personalizzato e distribuirlo. In questo senso, il percorso di onboarding è completo e i tuoi utenti possono ora utilizzare AEMaaCS.

Tuttavia, se desideri comprendere meglio in che modo gli autori e gli sviluppatori utilizzano il sistema, puoi continuare con due parti facoltative di questo percorso di onboarding:

* [Attività di Developer Manager e Deployment Manager](developers.md) - Informazioni su come gli sviluppatori possono accedere a git per memorizzare il codice personalizzato e implementarlo utilizzando le pipeline di Cloud Manager.
* [Attività utente AEM](aem-users.md) - Informazioni su come accedere all’ambiente AEM e iniziare a creare contenuti.

## Risorse aggiuntive {#additional-resources}

* [Gestione di prodotti e accesso utente in Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) - Scopri come utilizzare l’Admin Console per gestire l’accesso all’utilizzo.
* [Configurazione dell’accesso a AEM procedura dettagliata](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en) - Consulta questa guida dettagliata per scoprire di più sulla configurazione di utenti Adobe IMS, gruppi di utenti e profili di prodotto nell’Admin Console.

