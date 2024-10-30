---
title: Assets Prime
description: Ulteriori informazioni sugli aspetti chiave di Assets Prime, ad esempio i vantaggi chiave, i tipi di utenti e i relativi privilegi.
feature: Asset Management
role: User, Admin
source-git-commit: f033efd954ea7f9d27a891bfb9c0226e9d9c1432
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 2%

---

# [!DNL Assets] as a Cloud Service Prime  {#assets-prime}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Immagine banner AEM Assets Prime](/help/assets/assets/aem-assets-prime-package-banner.png)

Assets as a Cloud Service Prime include un DAM leggero che consente di eseguire varie funzionalità chiave, ad esempio:

* **Servizi di libreria e gestione risorse**&#x200B;: strumenti che consentono agli utenti di acquisire, archiviare, catalogare, controllare, gestire e gestire le risorse digitali di un brand in un archivio centralizzato

* **Ricerca, individuazione e Collaboration**: strumenti che consentono agli utenti di sfogliare, individuare, condividere e collaborare alle risorse necessarie per creare esperienze cliente avanzate.

* **Sicurezza e Rights Management**: strumenti per gestire l&#39;accesso, le autorizzazioni, i diritti e la sicurezza per garantire la conformità, la coerenza e l&#39;integrità del brand.

* **Creative Cloud connessioni**: strumenti che consentono ai team di marketing e creativi di collaborare con accesso semplificato, commento, revisione e annotazioni per aggiornare o finalizzare le risorse digitali.

* **Experience Cloud Connections**: strumenti per supportare l&#39;accesso nativo alle risorse digitali da altre applicazioni e servizi Experience Cloud.

* ****

* ****

* ****

[](/help/assets/assets-ultimate-overview.md)

Questo articolo fornisce un flusso di lavoro end-to-end per abilitare Assets as a Cloud Service Prime.

## Abilita Assets as a Cloud Service Prime{#enable-assets-prime}

Abilita Assets Prime durante la creazione di un nuovo programma tramite Cloud Manager. Esegui i passaggi seguenti:

1. Accedere a Cloud Manager come amministratore di sistema. Ensure that you select the right organization while logging in.

   >[!NOTE]
   >
   >Ensure that you are added to the appropriate Cloud Manager product profile to add a new program. [](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)

1. [Crea un nuovo programma](/help/journey-onboarding/create-program.md).

   Durante la creazione del nuovo programma, nella scheda **[!UICONTROL Soluzioni e componenti aggiuntivi]**, seleziona **[!UICONTROL Assets Prime]**. Puoi anche espandere **[!UICONTROL Assets Prime]** e selezionare **[!UICONTROL Content Hub]** per abilitare [Content Hub](/help/assets/product-overview.md) per la distribuzione delle risorse.

   ![AEM Assets Ultimate](assets/aem-assets-prime.png)


1. Fai clic su **[!UICONTROL Crea]** per creare il programma.

1. Fai clic sulla scheda del programma e fai clic su **[!UICONTROL Aggiungi ambiente]**.

1. Specifica il nome dell&#39;ambiente, definisci un&#39;area e fai clic su **[!UICONTROL Salva]** per creare l&#39;ambiente.

   ![Aggiungi ambiente ad Assets Prime](assets/aem-assets-prime-add-environment.png)

>[!NOTE]
>
>Assets Prime consente di creare solo un ambiente di produzione. L’opzione Aggiungi ambiente non è più disponibile dopo la corretta creazione dell’ambiente di produzione.

Assets Prime è ora abilitato per Experience Manager Assets as a Cloud Service.

![AEM Assets Prime è disponibile](assets/aem-assets-prime-setup-complete.png)

System administrator is automatically entitled as AEM administrator and receives an email to navigate to Admin Console to manage product profiles.


Your AEM as a Cloud Service instance on Admin Console comprises the following product profiles:

* AEM Administrators

* Utenti AEM

* [AEM Assets Collaborator Users](#onboard-collaborator-users)

* [AEM Assets Power Users](#onboard-power-users)


![Profili di prodotto di AEM Assets](assets/aem-assets-product-profiles.png)

Puoi iniziare ad aggiungere utenti o gruppi di utenti ai profili di prodotto Utenti di AEM Assets Collaborator e Utenti AEM Assets Power. Per ulteriori informazioni, vedere [Onboarding degli utenti AEM Assets Collaborator](#onboard-collaborator-users) e [onboarding degli utenti AEM Assets Power](#onboard-power-users).

`delivery`

![](assets/new-instance-content-hub.png)

>[!NOTE]
>
>`contenthub`

Tieni presente che il nome dell&#39;istanza per Content Hub non contiene `author` o `publish`.

Fare clic sul nome dell&#39;istanza per visualizzare il profilo di prodotto Content Hub `AEM Assets Limited Users`.

![Profilo prodotto Content Hub](assets/content-hub-product-profile.png)

Puoi iniziare ad aggiungere utenti o gruppi di utenti a questo profilo di prodotto per consentire loro di accedere a Content Hub.

>[!NOTE]
>
>Se hai eseguito il provisioning di Content Hub prima del 14 agosto 2024, il profilo di prodotto Content Hub presenta `contenthub` menzionato dopo `Limited Users` invece di `delivery`.

## Onboard AEM Assets Collaborator users {#onboard-collaborator-users}

AEM Assets Collaborator users can work with assets from Experience manager via integrations of Assets available to your organization in other Adobe products and non-Adobe applications, create and edit assets using built-in Adobe Express and Firefly leveraging professionally designed templates, brand kits, Adobe Stock assets, and so on, and access and leverage approved assets from your organization using AEM Assets Content Hub portal.

To onboard Collaborator users:

1. Access Experience Manager Assets product profiles by clicking the AEM as a Cloud Service product name in the list of products on Admin Console.

1. Click the production author instance for AEM as a Cloud Service:
   ![](assets/aem-cloud-service-instances.png)

1. Fare clic sul profilo di prodotto Utenti collaboratori e fare clic su **[!UICONTROL Aggiungi utenti]** per aggiungere l&#39;utente al profilo di prodotto.
   ![Profilo prodotto utente](assets/aem-assets-collaborator-user-permissions.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

È inoltre possibile accedere ai servizi assegnati agli utenti di Collaborator e visualizzarli, come illustrato nell&#39;immagine seguente:

![](assets/aem-assets-collaborator-users.png)

I servizi `Adobe Express` e `AEM Assets Collaborator Users` sono abilitati per impostazione predefinita. Puoi disattivare e attivare l’interruttore, in base alle tue esigenze, tuttavia, Adobe consiglia di utilizzare i servizi predefiniti abilitati per i profili di prodotto.

## Onboarding degli utenti AEM Assets Power {#onboard-power-users}

Gli utenti di AEM Assets Power possono accedere a tutte le funzionalità di AEM Assets, tra cui la gestione di risorse, autorizzazioni, metadati e la governance e l’automazione generali relative alle risorse digitali, lavorare con le risorse di Experience Manager tramite integrazioni di Assets disponibili per la tua organizzazione in altre applicazioni Adobe e non Adobe, creare e modificare le risorse utilizzando Adobi Express e Firefly incorporati utilizzando modelli progettati professionalmente, kit per il marchio, risorse Adobe Stock e così via, nonché accedere e sfruttare le risorse approvate dalla tua organizzazione tramite il portale AEM Assets Content Hub.

Per integrare gli utenti esperti:

1. Accedi ai profili di prodotto di Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell’elenco dei prodotti di Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Fare clic sul profilo di prodotto Utenti avanzati e fare clic su **[!UICONTROL Aggiungi utenti]** per aggiungere l&#39;utente al profilo di prodotto.
   ![Profilo prodotto utente](assets/aem-assets-power-user-permissions.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

È inoltre possibile accedere e visualizzare i servizi assegnati agli utenti esperti, come illustrato nell&#39;immagine seguente:

![](assets/aem-assets-power-users.png)

`Adobe Express``AEM Assets Power Users` You can turn the toggle off and on, as per your requirements, however, Adobe recommends to use the default services enabled for the product profiles.
