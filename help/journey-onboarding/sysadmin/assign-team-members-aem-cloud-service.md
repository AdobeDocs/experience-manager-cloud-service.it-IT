---
title: Assegnare i membri del team ai profili di prodotto di AEM as a Cloud Service
description: Segui questa pagina per scoprire come assegnare i membri del team a AEM profili di prodotto as a Cloud Service
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 5%

---

# Assegnare i membri del team ai profili di prodotto di AEM as a Cloud Service {#assign-team-members-cloud-service}

## Obiettivo {#objective}

Questo documento aiuta a comprendere i passaggi che l’amministratore di sistema deve seguire per assegnare i membri del team a AEM profili di prodotto as a Cloud Service e perché è fondamentale per consentire agli autori AEM di iniziare il proprio percorso con AEM.

Dopo aver letto questa sezione è necessario comprendere:

* Perché e come i membri del team vengono assegnati a AEM profili di prodotto as a Cloud Service.
* Come aggiungere membri del team al profilo di prodotto AEM utente.
* Come aggiungere membri del team al profilo di prodotto Amministratori AEM.


## Introduzione {#introduction}

Per poter accedere AEM utenti as a Cloud Service, è necessario appartenere a uno dei due profili di prodotto:  `AEM Users` o `AEM Administrators`. Ai membri del team devono essere concesse le autorizzazioni per l’istanza AEM, in quanto le autorizzazioni per amministrare Cloud Manager non sono sufficienti.

>[!NOTE]
>Ogni utente assegnato a AEM profilo di prodotto utente dall’amministratore di sistema avrà accesso (in sola lettura) a Cloud Manager.

## Prerequisiti {#prerequisites}

Prima di iniziare a leggere questa sezione, è necessario considerare quanto segue:

* Comprendere [AEM profili di prodotto as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)
* Acquisisci familiarità con [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)
* I profili di prodotto di Cloud Manager sono stati assegnati ai membri del team a seconda delle necessità e le risorse cloud sono state configurate
* Dettagli sul membro del team: L’amministratore di sistema deve disporre dei nomi e degli indirizzi e-mail e dei ruoli e delle responsabilità dei membri del team che avranno bisogno dell’accesso a AEM as a Cloud Service.

   >[!NOTE]
   >Ai fini dell’onboarding, è consigliabile aggiungere inizialmente utenti che parteciperanno alle attività immediate, come amministratori, sviluppatori e autori di contenuti. Puoi continuare il resto dell’onboarding senza aggiungere tutti gli utenti. Dopo aver completato l’onboarding, puoi scalare un numero maggiore di utenti in un secondo momento.


   >[!IMPORTANT]
   >Prima di iniziare a rivedere i passaggi per assegnare i membri del team a AEM profili di prodotto as a Cloud Service, assicurati di seguire questi due passaggi:
   >
   >1. Accedi a [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en). Per ulteriori informazioni, consulta Accesso ad Admin Console .
   >
   >1. Revisione [AEM profili di prodotto as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).


Per visualizzare l’elenco dei profili di Cloud Manager da Adobe Admin Console, effettua le seguenti operazioni:

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/). Da **Panoramica** pagina, seleziona **Adobe Experience Manager as a Cloud Service** dal **Prodotti e servizi** il Card.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Passa all’istanza (istanza autore dell’ambiente di sviluppo) e selezionala come illustrato di seguito.

   ![](/help/journey-onboarding/assets/cloud-profiles-1.png)


1. Verrà visualizzato l’elenco dei profili di prodotto as a Cloud Service che dovranno essere assegnati a un utente in base al suo ruolo.

   >[!NOTE]
   >Per ulteriori informazioni, consulta [AEM profili di prodotto as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/journey-onboarding/assets/cloud-profiles-2.png)


## Aggiungi membri del team a AEM profilo di prodotto utente o AEM amministratore {#add-team-members}

Per poter accedere a AEM’istanza as a Cloud Service, gli utenti devono appartenere a uno dei due profili di prodotto `AEM Users` o `AEM Administrators`.

>[!NOTE]
>È necessario disporre delle autorizzazioni per l’istanza. Le autorizzazioni per amministrare Cloud Manager non saranno sufficienti. Per saperne di più.

I passaggi seguenti devono essere seguiti da un amministratore di sistema che si trova anche nel ruolo Proprietario business.

1. Passa al programma da Cloud Manager e seleziona la **Gestisci accesso** dal contesto di interesse come mostrato di seguito.

   ![](/help/journey-onboarding/assets/add-team1.png)

1. Una nuova scheda consente di accedere a Adobe Admin Console da dove puoi accedere all’istanza di authoring dell’ambiente. Seleziona **Amministratori AEM** o **Utenti AEM** in base alle autorizzazioni che questa persona deve dare. Ulteriori informazioni [AEM profili di prodotto as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/journey-onboarding/assets/add-team2.png)

1. Seleziona `AEM Administrator` o `AEM User` e fai clic su **Aggiungi utente** come mostrato di seguito e invia i dettagli necessari per completare l’aggiunta del membro del team.

   ![](/help/journey-onboarding/assets/add-team3.png)

   L’utente aggiunto avrà ora accesso ai AEM servizi di authoring as a Cloud Service.

   >[!NOTE]
   >Se si dispone delle informazioni dei membri del team che hanno bisogno di accedere, è necessario ripetere questi passaggi per tutti gli ambienti, inclusi Sviluppo, Stage e Produzione.


## Novità {#whats-next}

Gli utenti assegnati a AEM profili di prodotto as a Cloud Service sono ora in grado di accedere a Author e di acquisire familiarità con le pagine di authoring in AEM as a Cloud Service. Seguire il percorso, rivedendo il percorso di apprendimento del documento per [Utenti AEM](/help/journey-onboarding/sysadmin/learning-path-aem-users.md) o [Sviluppatori e gestori di distribuzione](/help/journey-onboarding/sysadmin/learning-path-developers-deploymentmanagers.md).

## Risorse aggiuntive {#additional-resources}

* [Gestione dei prodotti e dell’accesso utente in Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console)
* [Configurazione dell’accesso a AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [Guida rapida all’authoring delle pagine](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)
