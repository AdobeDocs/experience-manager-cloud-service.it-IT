---
title: Abilita Assets Ultimate
description: Scopri come abilitare Assets Ultimate per i clienti nuovi ed esistenti.
feature: Asset Management
role: User, Admin
exl-id: 45cd8ccd-e5cf-42cd-aa7f-4ae59d0587f7
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 3%

---

# Abilita Ultimate di as a Cloud Service [!DNL Assets] {#enable-assets-cloud-service-ultimate}

![Passare ad Asset Cloud Service Ultimate](/help/assets/assets/upgrade-assets-cs-ultimate-package-banner.png)

Assets as a Cloud Service Ultimate consente di eseguire varie funzionalità DAM chiave, ad esempio gestione delle risorse e servizi libreria, sicurezza e gestione dei diritti, connessioni Creative e Experience Cloud, estensibilità dell’interfaccia utente, automazione basata su API, integrazioni con applicazioni Adobe e non Adobe, distribuzione di codice personalizzato e molto altro ancora. Per l&#39;elenco completo, vedere [Panoramica di Assets as a Cloud Service Ultimate](/help/assets/assets-ultimate-overview.md).

## Abilita Assets Ultimate {#enable-assets-ultimate}

I nuovi clienti di Assets as a Cloud Service devono prima abilitare Assets Ultimate creando un nuovo programma con Cloud Manager.

Esegui i passaggi seguenti:

1. Accedere a Cloud Manager come amministratore di sistema. Assicurati di selezionare l’organizzazione adatta durante l’accesso.

   >[!NOTE]
   >
   >Accertati di essere aggiunto al profilo di prodotto Cloud Manager appropriato per aggiungere un nuovo programma. Per ulteriori informazioni, vedere [Autorizzazioni basate sul ruolo in Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions).

1. [Crea un nuovo programma](/help/journey-onboarding/create-program.md) e [aggiungi ambienti](/help/journey-onboarding//create-environments.md).

   Durante la creazione del nuovo programma, nella scheda **[!UICONTROL Soluzioni e componenti aggiuntivi]**, seleziona **[!UICONTROL Assets Ultimate]**. Puoi anche espandere **[!UICONTROL Assets Ultimate]** e selezionare **[!UICONTROL Content Hub]** per abilitare [Content Hub](/help/assets/product-overview.md) per la distribuzione delle risorse.

   ![AEM Assets Ultimate](assets/aem-assets-ultimate-solutions.png)

1. Fai clic su **[!UICONTROL Crea]** per creare il programma. Assets Ultimate è ora abilitato per Experience Manager Assets as a Cloud Service.

L’amministratore di sistema ha automaticamente diritto come amministratore di AEM su Assets Ultimate e riceve un messaggio e-mail per passare ad Admin Console e gestire i profili di prodotto disponibili.

L’istanza di AEM as a Cloud Service su Admin Console include i seguenti profili di prodotto:

* AEM Administrators

* AEM Users

* [AEM Assets Collaborator Users](#onboard-collaborator-users)

* [AEM Assets Power Users](#onboard-power-users)

  ![Profili di prodotto di AEM Assets](assets/aem-assets-product-profiles.png)

Se hai abilitato Content Hub per Assets as a Cloud Service, è stata creata una nuova istanza all&#39;interno di AEM Assets as a Cloud Service su Admin Console con `delivery` come suffisso:

![Nuova istanza per Content Hub](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Se è stato eseguito il provisioning di Content Hub prima del 14 agosto 2024, la nuova istanza viene creata con `contenthub` come suffisso.

Tieni presente che il nome dell&#39;istanza per Content Hub non contiene `author` o `publish`.

Fare clic sul nome dell&#39;istanza per visualizzare il profilo di prodotto Content Hub `AEM Assets Limited Users`.

![Profilo prodotto Content Hub](assets/content-hub-product-profile.png)

Puoi iniziare ad aggiungere utenti o gruppi di utenti a questo profilo di prodotto per consentire loro di accedere a Content Hub.

>[!NOTE]
>
>Se hai eseguito il provisioning di Content Hub prima del 14 agosto 2024, il profilo di prodotto Content Hub presenta `contenthub` menzionato dopo `Limited Users` invece di `delivery`.

## Abilita Assets Ultimate per i clienti esistenti {#enable-assets-ultimate-existing-customers}

I clienti Assets as a Cloud Service esistenti possono effettuare l’aggiornamento ad Assets Ultimate eseguendo due semplici passaggi. Puoi passare al programma Assets as a Cloud Service in Cloud Manager e visualizzare lo stato dell’aggiornamento nella scheda Programma in base alla disponibilità dei crediti di Assets Ultimate. Se sono disponibili crediti sufficienti per l&#39;aggiornamento ad Assets Ultimate, è possibile visualizzare lo stato come `Assets license upgrade required`, come illustrato nell&#39;immagine seguente:

![Aggiornamento AEM Assets ad Assets Ultimate](assets/aem-assets-upgrade-status-ultimate.png)

Se un cliente esistente acquista una nuova licenza per Assets Ultimate, lo stato di aggiornamento visualizzato è `Assets license upgrade available`.

### Prerequisiti per l’aggiornamento {#prerequisites-assets-upgrade}

Tutti gli ambienti devono essere aggiornati alla versione più recente di AEM as a Cloud Service o almeno alla versione `2024.10.18175`. Se non soddisfi i requisiti minimi, contatta il rappresentante Adobe per passare alla versione di AEM release richiesta.

### Esegui l’aggiornamento ad Assets Ultimate {#upgrade-assets-ultimate}

Esegui i passaggi seguenti:

1. Dopo aver soddisfatto i requisiti minimi per la versione di AEM, fai clic sul nome del programma. Una scheda Aggiornamento viene visualizzata appena sopra la sezione **[!UICONTROL Ambienti]**, come illustrato nell&#39;immagine seguente:

   ![Aggiornamento AEM Assets ad Assets Ultimate](assets/aem-assets-upgrade-card.png)

1. Fare clic su **[!UICONTROL Aggiungi profili prodotto]**. In Cloud Manager sono visualizzate le opzioni per aggiungere nuovi profili di prodotto a tutti gli ambienti disponibili nel programma o nei singoli ambienti.

   ![Opzioni di aggiornamento di AEM Assets](assets/aem-assets-upgrade-options.png)

1. Fai clic su **[!UICONTROL Tutti gli ambienti]** per aggiungere i nuovi profili di prodotto a tutti gli ambienti nel programma oppure su **[!UICONTROL Singoli ambienti]** per aggiungere i nuovi profili di prodotto agli ambienti selezionati.

   Facendo clic su **[!UICONTROL Singoli ambienti]** viene visualizzato l&#39;elenco di tutti gli ambienti disponibili nel programma.

1. Fai clic sull&#39;icona Altre opzioni corrispondente a un ambiente e seleziona **[!UICONTROL Aggiungi profili di prodotto]** per aggiungere i nuovi profili di prodotto all&#39;ambiente selezionato.

   ![AEM Assets seleziona singoli ambienti](assets/aem-assets-individual-environments.png)

   Puoi anche aggiungere profili di prodotto agli ambienti selezionati passando alla sezione **[!UICONTROL Ambienti]**, facendo clic sull&#39;icona Altre opzioni corrispondente a un ambiente e selezionando **[!UICONTROL Aggiungi profili di prodotto]**.

   Lo stato dell&#39;ambiente visualizza `Adding Product Profiles` durante l&#39;aggiunta dei nuovi profili di prodotto e successivamente visualizza `Running` al termine del processo.

   Prima di eseguire il passaggio successivo, è necessario aggiungere profili di prodotto a tutti gli ambienti disponibili nel programma, singolarmente o in tutti gli ambienti insieme.

1. Fai clic su **[!UICONTROL Aggiorna]**. L&#39;opzione **[!UICONTROL Aggiorna]** viene visualizzata solo quando si aggiungono profili di prodotto a tutti gli ambienti disponibili.

   ![Ultimo passaggio nel processo di aggiornamento](assets/aem-assets-upgrade-button.png)

   Il processo di aggiornamento è stato completato ed è stato effettuato l’aggiornamento dell’as a Cloud Service di Assets ad Assets Ultimate. Lo stato del programma visualizza `Assets Ultimate`.

   ![Stato del programma dopo l&#39;aggiornamento](assets/program-status-post-upgrade.png)

L’istanza di AEM as a Cloud Service su Admin Console ora include i seguenti profili di prodotto:

* AEM Administrators

* AEM Users

* [AEM Assets Collaborator Users](#onboard-collaborator-users)

* [AEM Assets Power Users](#onboard-power-users)

![Profili di prodotto di AEM Assets](assets/aem-assets-product-profiles.png)

Se è necessario abilitare Content Hub, fare clic sull&#39;icona Altre opzioni (...) sul nome del programma in Cloud Manager e selezionare **[!UICONTROL Modifica programma]**. Espandi **[!UICONTROL Assets Ultimate]** e fai clic su **[!UICONTROL Content Hub]**. Questo passaggio abilita Content Hub per Assets Ultimate. È stata creata una nuova istanza all&#39;interno di AEM Assets as a Cloud Service su Admin Console con `delivery` come suffisso:

![Nuova istanza per Content Hub](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Se è stato eseguito il provisioning di Content Hub prima del 14 agosto 2024, la nuova istanza viene creata con `contenthub` come suffisso.

Tieni presente che il nome dell&#39;istanza per Content Hub non contiene `author` o `publish`.

Fare clic sul nome dell&#39;istanza per visualizzare il profilo di prodotto Content Hub `AEM Assets Limited Users`.

![Profilo prodotto Content Hub](assets/content-hub-product-profile.png)

Puoi iniziare ad aggiungere utenti o gruppi di utenti a questo profilo di prodotto per consentire loro di accedere a Content Hub.

>[!NOTE]
>
>Se hai eseguito il provisioning di Content Hub prima del 14 agosto 2024, il profilo di prodotto Content Hub presenta `contenthub` menzionato dopo `Limited Users` invece di `delivery`.

## Eseguire l’onboarding degli utenti AEM Assets Collaborator {#onboard-collaborator-users}

Gli utenti di AEM Assets Collaborator possono lavorare con le risorse di Experience Manager tramite integrazioni di Assets disponibili per la tua organizzazione in altri prodotti Adobe e in applicazioni non Adobe, creare e modificare le risorse utilizzando Adobe Express e Firefly integrati utilizzando modelli progettati professionalmente, kit per il marchio, risorse Adobe Stock e così via, nonché accedere e sfruttare le risorse approvate dalla tua organizzazione tramite il portale AEM Assets Content Hub.

Per integrare gli utenti di Collaborator:

1. Accedi ai profili di prodotto di Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell’elenco dei prodotti su Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Fare clic sul profilo di prodotto Utenti collaboratori e fare clic su **[!UICONTROL Aggiungi utenti]** per aggiungere utenti o gruppi di utenti al profilo di prodotto.
   ![Profilo prodotto utente](assets/aem-assets-collaborator-user-permissions.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

È inoltre possibile accedere ai servizi assegnati agli utenti di Collaborator e visualizzarli, come illustrato nell&#39;immagine seguente:

![Servizi per gli utenti di Collaborator](assets/aem-assets-collaborator-users.png)

I servizi `Adobe Express` e `AEM Assets Collaborator Users` sono abilitati per impostazione predefinita.

>[!NOTE]
>
>Puoi disattivare e attivare l’attivazione per abilitare o disabilitare i servizi disponibili, in base alle tue esigenze. Tuttavia, Adobe consiglia di utilizzare i servizi predefiniti abilitati per i profili di prodotto.


## Onboarding degli utenti AEM Assets Power {#onboard-power-users}

Gli utenti di AEM Assets Power possono accedere a tutte le funzionalità di AEM Assets, tra cui la gestione di risorse, autorizzazioni, metadati e la governance e l’automazione generali relative alle risorse digitali; possono lavorare con le risorse di Experience Manager tramite integrazioni di Assets disponibili per la tua organizzazione in altre applicazioni Adobe e non Adobe; possono creare e modificare le risorse utilizzando Adobe Express e Firefly integrati utilizzando modelli progettati professionalmente, kit per i brand, risorse Adobe Stock e così via; possono inoltre accedere e sfruttare le risorse approvate della tua organizzazione tramite il portale AEM Assets Content Hub.

Per integrare gli utenti esperti:

1. Accedi ai profili di prodotto di Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell’elenco dei prodotti su Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Fare clic sul profilo di prodotto Utenti avanzati e fare clic su **[!UICONTROL Aggiungi utenti]** per aggiungere utenti o gruppi di utenti al profilo di prodotto.
   ![Profilo prodotto utente](assets/aem-assets-power-user-permissions.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

È inoltre possibile accedere e visualizzare i servizi assegnati agli utenti esperti, come illustrato nell&#39;immagine seguente:

![Servizi per utenti esperti](assets/aem-assets-power-users.png)

I servizi `Adobe Express` e `AEM Assets Power Users` sono abilitati per impostazione predefinita.

>[!NOTE]
>
>Puoi disattivare e attivare l’attivazione per abilitare o disabilitare i servizi disponibili, in base alle tue esigenze. Tuttavia, Adobe consiglia di utilizzare i servizi predefiniti abilitati per i profili di prodotto.
