---
title: Distribuisci [!DNL Content Hub]
description: Scopri come distribuire e attivare Content Hub, fornire accesso agli utenti con diversi tipi di privilegi (caricare risorse, Adobi Express di utenti) e fornire privilegi di amministratore agli utenti.
role: Admin
source-git-commit: 7224cca950e61bea298f246245bdb221fd8fa22e
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 0%

---


# Distribuire l’hub di contenuti {#deploy-content-hub}

![Distribuire Content Hub](assets/deploy-content-hub.png)

Content Hub è disponibile come parte di Experience Manager Assets as a Cloud Service per la democratizzazione dell’accesso ai contenuti sul marchio per le organizzazioni e i loro partner commerciali.

Le risorse contrassegnate come Approvate in Experience Manager Assets as a Cloud Service sono disponibili per la distribuzione delle risorse in Content Hub.

Questo articolo fornisce un flusso di lavoro end-to-end per fornire agli utenti l’accesso a Content Hub, comprese le varianti di privilegi in base alle loro esigenze.

Le varianti di privilegi su Content Hub includono:

* [Utenti Content Hub](#onboard-content-hub-users): accedi alle risorse approvate dal marchio sul portale Content Hub.

* [Amministratori Content Hub](#onboard-content-hub-administrator): accesso al [Interfaccia utente di configurazione](/help/assets/configure-content-hub-ui-options.md) su Content Hub, oltre ad accedere alle risorse approvate dal marchio, caricare le risorse su Content Hub, integrazioni Adobe Express per la modifica delle immagini (se disponi di diritti Adobi Express).

* [Utenti Content Hub con diritti per aggiungere risorse](#onboard-content-hub-users-add-assets): possibilità di [caricare risorse in Content Hub](/help/assets/upload-brand-approved-assets.md) oltre ad accedere alle risorse approvate dal marchio sul portale Content Hub.

* [Utenti Content Hub con diritti per il remix delle risorse in nuove varianti](#onboard-content-hub-users-remix-assets): [Integrazione Adobe Express](/help/assets/edit-images-content-hub.md) (se disponi di diritti di Adobe Express) oltre ad accedere alle risorse approvate dal marchio sul portale Content Hub.

* [Utenti Experience Manager Assets](#experience-manager-assets-users): possibilità di approvare le risorse su Experience Manager Assets as a Cloud Service per renderle disponibili su Content Hub.

## Passaggio 1: abilitare Content Hub per Experience Manager Assets tramite Cloud Manager {#enable-content-hub}

Per accedere al portale Content Hub, gli amministratori devono innanzitutto abilitare Content Hub per Experience Manager Assets as a Cloud Service utilizzando Cloud Manager. Esegui i passaggi seguenti:

1. Accedere a Cloud Manager. Assicurati di selezionare l’organizzazione adatta durante l’accesso. In Cloud Manager sono elencati tutti i programmi.

1. Passa a Experience Manager Assets as a Cloud Service, fai clic sull’icona Altre opzioni (...) e seleziona **[!UICONTROL Modifica programma]**.

   ![Modifica programma in Cloud Manager](assets/edit-program-cloud-manager.png)

1. Il giorno [!UICONTROL Modifica programma] , seleziona la **[!UICONTROL Soluzioni e componenti aggiuntivi]** scheda.

1. Espandi **[!UICONTROL Assets]** e seleziona **[!UICONTROL Content Hub]**.
   ![Seleziona Content Hub in Cloud Manager](assets/edit-program-cloud-manager-content-hub.png)

   >[!NOTE]
   >
   >Se **[!UICONTROL Aggiorna]** non è abilitato dopo aver selezionato Content Hub, accertati di aver specificato le impostazioni di pubblicazione per il programma.

1. Fai clic su **[!UICONTROL Aggiorna]**.

Content Hub è ora abilitato per Experience Manager Assets as a Cloud Service.

>[!NOTE]
>
>Puoi accedere a Content Hub e utilizzarlo con un massimo di 250 utenti Content Hub. Per ulteriori domande, contatta il rappresentante del tuo Adobe.


Se hai poca esperienza con Experience Manager Assets, fai clic su **[!UICONTROL Aggiungi programma]** e quindi fornire i dettagli del programma (Nome del programma, configurato per la produzione) e fare clic su **[!UICONTROL Continua]**. A questo punto puoi selezionare **[!UICONTROL Assets]** e **[!UICONTROL Content Hub]** nel **[!UICONTROL Soluzioni e componenti aggiuntivi]** scheda.

### Istanza di Content Hub e profilo di prodotto in Admin Console{#content-hub-instance-product-profile}

Dopo [abilitazione di Content Hub per Assets as a Cloud Service con Cloud Manager](#enable-content-hub), viene creata una nuova istanza all’interno di AEM Assets as a Cloud Service, ad Admin Console con `contenthub` come suffisso:

![Nuova istanza per Content Hub](assets/new-instance-content-hub.png)

Tieni presente che non è presente `author` o `publish` nel nome dell’istanza di Content Hub.

Fai clic sul nome dell’istanza per visualizzare il profilo di prodotto Content Hub.

![Profilo prodotto Content Hub](assets/content-hub-product-profile.png)

## Passaggio 2: onboarding di Content Hub administrator {#onboard-content-hub-administrator}

Gli amministratori di Content Hub possono accedere a [Interfaccia utente di configurazione](/help/assets/configure-content-hub-ui-options.md) su Content Hub, oltre ad accedere alle risorse approvate dal marchio, caricare le risorse su Content Hub, integrazioni Adobe Express per la modifica delle immagini (se disponi di diritti Adobi Express).

Per integrare l’amministratore di Content Hub:

1. [Accedi e fai clic sul profilo di prodotto utente di Content Hub](#content-hub-instance-product-profile).

1. Clic **[!UICONTROL Aggiungi utenti]** per aggiungere utenti o gruppi di utenti al profilo di prodotto.

1. Clic **[!UICONTROL Salva]** per salvare le modifiche.

1. Dopo aver aggiunto l’utente al profilo di prodotto di Content Hub, accedi ai profili di prodotto di Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell’elenco di prodotti di Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   In Admin Console vengono visualizzati due profili di prodotto per AEM as a Cloud Service: Amministratori e Utenti.
1. Fai clic sul profilo di prodotto Amministratori e fai clic su **[!UICONTROL Aggiungi utenti]** per aggiungere l’utente al profilo di prodotto.
   ![Profilo di prodotto Amministratore](assets/aem-cs-admin-product-profile.png)

1. Clic **[!UICONTROL Salva]** per salvare le modifiche.

## Passaggio 3: integrare gli utenti di Content Hub {#onboard-content-hub-users}

Gli utenti di Content Hub possono accedere alle risorse disponibili nel portale, ma non possono aggiungere nuove risorse o modificare quelle esistenti.

Per integrare gli utenti di Content Hub:

1. [Accedi e fai clic sul profilo di prodotto utente di Content Hub](#content-hub-instance-product-profile).

1. Clic **[!UICONTROL Aggiungi utenti]** per aggiungere utenti o gruppi di utenti al profilo di prodotto.

1. Clic **[!UICONTROL Salva]** per salvare le modifiche.

Questi utenti possono ora accedere alle risorse disponibili sul portale Content Hub.

>[!NOTE]
>
>Puoi utilizzare tutte le funzioni aziendali avanzate, ad esempio la sincronizzazione con provider di identità esterni.

### Come accedere a Content Hub? {#access-content-hub}

È possibile accedere a Content Hub nei modi seguenti:

* Accedi a Content Hub utilizzando il seguente collegamento:

  `https://experience.adobe.com/#/assets/contenthub`

* Accedi a `experience.adobe com` e fai clic su **[!UICONTROL Experience Manager Assets Content Hub]** disponibile in **[!UICONTROL Accesso rapido]** sezione:
  ![Accesso a Content Hub](assets/access-content-hub.png)

* Accedi a `experience.adobe com` e fai clic su **[!UICONTROL Experience Manager Assets Content Hub]** disponibile nel commutatore del prodotto:
  ![Metodo di accesso Content Hub 3](assets/access-content-hub-alternate.png)

### Disattiva le notifiche e-mail agli utenti {#disable-email-notifications}

Se gli amministratori devono disabilitare le notifiche e-mail inviate agli utenti quando vengono aggiunte al profilo di prodotto Content Hub:

Fai clic sull’icona di ricerca accanto al nome del profilo di prodotto e disattiva l’opzione **[!UICONTROL Notifica agli utenti via e-mail]** attivare/disattivare.

![Disattiva notifiche e-mail](assets/disable-email-notifications.png)


## Passaggio 4: integrare gli utenti di Content Hub con i diritti per aggiungere risorse (facoltativo) {#onboard-content-hub-users-add-assets}

Gli utenti di Content Hub con diritti per l’aggiunta di risorse possono [caricare nuove risorse approvate dal marchio in Content Hub](/help/assets/upload-brand-approved-assets.md).

Per integrare gli utenti di Content Hub con i diritti per l’aggiunta di utenti:

1. [Dopo l’aggiunta dell’utente al profilo di prodotto Content Hub](#onboard-content-hub-users), accedi ai profili di prodotto di Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell’elenco dei prodotti su Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   In Admin Console vengono visualizzati due profili di prodotto per AEM as a Cloud Service: Amministratori e Utenti.
1. Fai clic sul profilo di prodotto Utenti e fai clic su **[!UICONTROL Aggiungi utenti]** per aggiungere l’utente al profilo di prodotto.
   ![Profilo prodotto utente](assets/aem-cs-user-product-profile.png)

1. Clic **[!UICONTROL Salva]** per salvare le modifiche.

## Passaggio 4: integrare gli utenti di Content Hub con diritti per il remix delle risorse in nuove varianti (facoltativo) {#onboard-content-hub-users-remix-assets}

Gli utenti di Content Hub con diritti per il remix delle risorse in nuove varianti possono [modifica le risorse esistenti utilizzando Adobe Express e salva la risorsa nell’archivio](/help/assets/edit-images-content-hub.md). La modifica delle risorse tramite Adobe Express è disponibile solo se l’utente dispone di diritti Adobi Express.

Per integrare gli utenti di Content Hub con diritti per il remix delle risorse in nuove varianti:

1. [Dopo l’aggiunta dell’utente al profilo di prodotto Content Hub](#onboard-content-hub-users), accedi ai profili di prodotto di Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell’elenco dei prodotti su Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   In Admin Console vengono visualizzati due profili di prodotto per AEM as a Cloud Service: Amministratori e Utenti.
1. Fai clic sul profilo di prodotto Utenti e fai clic su **[!UICONTROL Aggiungi utenti]** per aggiungere l’utente al profilo di prodotto.
   ![Profilo prodotto utente](assets/aem-cs-user-product-profile.png)

1. Clic **[!UICONTROL Salva]** per salvare le modifiche.

## Utenti Experience Manager Assets {#experience-manager-assets-users}

Gli utenti di Experience Manager Assets possono approvare le risorse su AEM as a Cloud Service in modo che siano disponibili su Content Hub.

Per configurare gli utenti di Experience Manager Assets:

1. Accedi ai profili di prodotto di Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell’elenco dei prodotti di Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   In Admin Console vengono visualizzati due profili di prodotto per AEM as a Cloud Service: Amministratori e Utenti.
1. Fai clic sul profilo di prodotto Utenti e fai clic su **[!UICONTROL Aggiungi utenti]** per aggiungere l’utente al profilo di prodotto.
   ![Profilo prodotto utente](assets/aem-cs-user-product-profile.png)

1. Clic **[!UICONTROL Salva]** per salvare le modifiche.

   >[!NOTE]
   >
   > Non è necessario aggiungerlo al [Profilo prodotto Content Hub](#onboard-content-hub-users) per gli utenti di Experience Manager Assets.



