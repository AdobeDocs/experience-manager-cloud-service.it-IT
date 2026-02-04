---
title: Distribuisci [!DNL Content Hub]
description: Scopri come distribuire e attivare Content Hub, fornire accesso agli utenti con diversi tipi di privilegi (caricare risorse, utenti Adobe Express) e fornire privilegi di amministratore agli utenti.
role: Admin
exl-id: 58194858-6e1c-460b-bab3-3496176b2851
source-git-commit: 655f84593adb1199bcfc21cb54071feb3c8523c5
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 6%

---

# Implementare Content Hub {#deploy-content-hub}

Content Hub è disponibile come parte di Experience Manager Assets as a Cloud Service per la democratizzazione dell’accesso ai contenuti sul marchio per le organizzazioni e i loro partner commerciali.

Le risorse contrassegnate come Approvate in Experience Manager Assets as a Cloud Service sono disponibili per la distribuzione delle risorse in Content Hub.

Questo articolo fornisce un flusso di lavoro end-to-end per fornire agli utenti l’accesso a Content Hub, comprese le varianti di privilegi in base alle loro esigenze.

Guarda questo video per scoprire come abilitare Content Hub per Experience Manager Assets:

>[!VIDEO](https://video.tv.adobe.com/v/3472918/?learn=on){transcript=true}

Le varianti di privilegi su Content Hub includono:

* [Utenti Content Hub](#onboard-content-hub-users): accedi alle risorse approvate dal marchio nel portale Content Hub.

* [Amministratori Content Hub](#onboard-content-hub-administrator): accesso all&#39;[interfaccia utente di configurazione](/help/assets/configure-content-hub-ui-options.md) su Content Hub, accesso alle risorse approvate dal marchio, caricamento delle risorse in Content Hub, integrazione Adobe Express per la modifica delle immagini (se si dispone di diritti Adobe Express).

* [Utenti Content Hub con diritti per aggiungere risorse](#onboard-content-hub-users-add-assets): possibilità di [caricare risorse in Content Hub](/help/assets/upload-brand-approved-assets.md) oltre ad accedere alle risorse approvate dal marchio sul portale Content Hub.

* [Utenti Content Hub con diritti per il remix delle risorse in nuove varianti](#onboard-content-hub-users-remix-assets): [Integrazione Adobe Express](/help/assets/edit-images-content-hub.md) (se hai diritti Adobe Express) oltre ad accedere alle risorse approvate dal marchio sul portale Content Hub.

* [Utenti Experience Manager Assets](#experience-manager-assets-users): possibilità di approvare le risorse in Experience Manager Assets as a Cloud Service per renderle disponibili in Content Hub.

>[!NOTE]
>
>Puoi accedere a Content Hub e utilizzarlo con un massimo di 250 utenti Content Hub Limited per Assets Ultimate e 50 utenti Content Hub per Assets Prime. Per ulteriori domande, contatta il rappresentante Adobe.

Nella tabella seguente sono riepilogati i tipi di utenti Content Hub disponibili, i privilegi di cui dispongono e i profili di prodotto necessari per ottenere tali privilegi:

| Ruolo utente | Utenti Content Hub | Utenti Content Hub con diritti per aggiungere risorse | Utenti Content Hub con diritti per il remix delle risorse | Amministratori Content Hub |
|---------------|----------|----------|-------------------------|---|
| **Funzionalità** |  |  |  |  |
| Accesso alle risorse approvate dal brand sul portale Content Hub | ✓ | ✓ | ✓ | ✓ |
| Caricare risorse dal portale Content Hub | − | ✓ | ✓ | ✓ |
| Utilizzare l’integrazione di Adobe Express per modificare le immagini | − | − | ✓ | − |
| Accedere all’interfaccia utente di configurazione di Content Hub | − | − | − | ✓ |
| **L’utente deve essere in questi profili di prodotto (Admin Console)** |  |  |  |  |
| AEM > Istanza di consegna > Utenti con limitazione AEM Assets | ✓ | ✓ | ✓ | ✓ |
| AEM > Istanza Production Author > Utenti AEM | − | ✓ | ✓ | − |
| AEM > Istanza di authoring di produzione > Amministratori AEM | − | − | − | ✓ |
| Adobe Express | − | − | ✓ | − |
| **Ulteriori informazioni** | Visualizza [utenti Content Hub](#onboard-content-hub-users) | Vedi [Utenti Content Hub con diritti per aggiungere risorse](#onboard-content-hub-users-add-assets) | Consulta [Utenti Content Hub con diritti per eseguire il remix delle risorse in nuove varianti](#onboard-content-hub-users-remix-assets) | Visualizza [amministratori Content Hub](#onboard-content-hub-administrator) |

>[!NOTE]
>
>[Gli utenti di Experience Manager Assets](#experience-manager-assets-users) possono approvare risorse in un ambiente Experience Manager Assets as a Cloud Service per renderle disponibili su Content Hub. Questi utenti devono essere aggiunti a AEM > Istanza Production Author > Profilo di prodotto Utenti AEM utilizzando Admin Console.

## Passaggio 1: abilitare Content Hub per Experience Manager Assets tramite Cloud Manager {#enable-content-hub}


Per accedere al portale Content Hub, gli amministratori devono innanzitutto abilitare Content Hub per Experience Manager Assets as a Cloud Service utilizzando Cloud Manager.

### Autorizzazioni {#permissions-edit-program}

Per modificare i programmi in Cloud Manager è necessario avere il ruolo Proprietario business. Per ulteriori informazioni, vedere [Modifica programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).

Per abilitare Content Hub per Experience Manager Assets:

1. Accedere a Cloud Manager. Assicurati di selezionare l’organizzazione adatta durante l’accesso. In Cloud Manager sono elencati tutti i programmi.

1. Passa al programma Experience Manager Assets as a Cloud Service, fai clic sull&#39;icona Altre opzioni (...) e seleziona **[!UICONTROL Modifica programma]**.

   ![Modifica programma in Cloud Manager](assets/edit-program-cloud-manager.png)

1. Nella finestra di dialogo [!UICONTROL Modifica programma], seleziona la scheda **[!UICONTROL Soluzioni e componenti aggiuntivi]**.

1. Espandi **[!UICONTROL Assets]** e seleziona **[!UICONTROL Content Hub]**.
   ![Seleziona Content Hub in Cloud Manager](assets/edit-program-cloud-manager-content-hub.png)

   >[!NOTE]
   >
   >Se **[!UICONTROL Update]** non è abilitato dopo aver selezionato Content Hub, verificare di aver specificato le impostazioni di pubblicazione per il programma.

1. Fai clic su **[!UICONTROL Aggiorna]**.

Content Hub è ora abilitato per Experience Manager Assets as a Cloud Service. Dopo aver abilitato Content Hub in un ambiente di produzione, non puoi disabilitarlo in modo self-service.

Se hai poca esperienza con Experience Manager Assets, fai clic su **[!UICONTROL Aggiungi programma]**, quindi fornisci i dettagli del programma (Nome programma, configurato per la produzione) e fai clic su **[!UICONTROL Continua]**. Puoi quindi selezionare **[!UICONTROL Assets]** e **[!UICONTROL Content Hub]** nella scheda **[!UICONTROL Soluzioni e componenti aggiuntivi]**.

### Abilita Content Hub per ambienti di dimensioni inferiori {#enable-content-hub-lower-environments}

I seguenti crediti Content Hub sono disponibili in base alla licenza AEM Assets:

* Assets Ultimate: 3 crediti Content Hub

* Assets Prime: 1 credito Content Hub

* Clienti Assets as a Cloud Service esistenti: 1 credito Content Hub

Utilizza un credito per abilitare Content Hub in ogni ambiente, ad esempio Produzione, Sviluppo o Stage.

Per abilitare Content Hub per gli ambienti inferiori:

1. [Abilita Content Hub per Experience Manager Assets tramite Cloud Manager](#enable-content-hub).

1. Fai clic sulla scheda del programma per visualizzare l’elenco degli ambienti disponibili (Produzione, Sviluppo o Stage).

1. Fai clic sull’ambiente da abilitare. Nella sezione **[!UICONTROL Content Hub]** sono visualizzati `Content Hub is available for activation`.

   ![Abilita Content Hub per gli ambienti inferiori](assets/enable-content-hub-lower-environments.png)

1. Fai clic su **[!UICONTROL Fai clic per attivare]**. Fai di nuovo clic su **[!UICONTROL Attiva]** per confermare.

   Content Hub è abilitato per l’ambiente selezionato.



### Istanza di Content Hub e profilo di prodotto su Admin Console{#content-hub-instance-product-profile}

Dopo l&#39;abilitazione di [Content Hub per Assets as a Cloud Service tramite Cloud Manager](#enable-content-hub), è stata creata una nuova istanza in AEM Assets as a Cloud Service su Admin Console con `delivery` come suffisso:

![Nuova istanza per Content Hub](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Se è stato eseguito il provisioning di Content Hub prima del 14 agosto 2024, la nuova istanza viene creata con `contenthub` come suffisso.

Tieni presente che il nome dell&#39;istanza per Content Hub non contiene `author` o `publish`.

Fai clic sul nome dell’istanza per visualizzare il profilo di prodotto Content Hub.

![Profilo prodotto Content Hub](assets/content-hub-product-profile.png)

>[!NOTE]
>
>Se hai eseguito il provisioning di Content Hub prima del 14 agosto 2024, il profilo di prodotto Content Hub presenta `contenthub` menzionato dopo `Limited Users` invece di `delivery`.

## Passaggio 2: onboarding di Content Hub administrator {#onboard-content-hub-administrator}

Gli amministratori di Content Hub possono accedere all&#39;[Interfaccia utente di configurazione](/help/assets/configure-content-hub-ui-options.md) su Content Hub, oltre ad accedere alle risorse approvate dal marchio, caricare le risorse in Content Hub, integrare Adobe Express per la modifica delle immagini (se disponi di adesioni Adobe Express).

Per integrare l’amministratore di Content Hub:

1. [Accedere al profilo di prodotto dell&#39;utente di Content Hub](#content-hub-instance-product-profile) e fare clic su di esso.

1. Fai clic su **[!UICONTROL Aggiungi utenti]** per aggiungere utenti o gruppi di utenti al profilo di prodotto.

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

1. Dopo aver aggiunto l’utente al profilo di prodotto Content Hub, accedi ai profili di prodotto Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell’elenco dei prodotti su Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console mostra due profili di prodotto per AEM as a Cloud Service: Amministratori e Utenti.
1. Fai clic sul profilo di prodotto Amministratori e fai clic su **[!UICONTROL Aggiungi utenti]** per aggiungere l&#39;utente al profilo di prodotto.
   ![Profilo prodotto amministratore](assets/aem-cs-admin-product-profile.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

## Passaggio 3: integrare gli utenti di Content Hub {#onboard-content-hub-users}

Gli utenti di Content Hub possono accedere alle risorse disponibili nel portale, ma non possono aggiungere nuove risorse o modificare quelle esistenti.

Per integrare gli utenti di Content Hub:

1. [Accedere al profilo di prodotto dell&#39;utente di Content Hub](#content-hub-instance-product-profile) e fare clic su di esso.

1. Fai clic su **[!UICONTROL Aggiungi utenti]** per aggiungere utenti o gruppi di utenti al profilo di prodotto.

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

Questi utenti possono ora accedere alle risorse disponibili sul portale Content Hub.

>[!NOTE]
>
>Puoi utilizzare tutte le funzioni aziendali avanzate, ad esempio la sincronizzazione con provider di identità esterni.

### Come accedere a Content Hub? {#access-content-hub}

È possibile accedere a Content Hub nei modi seguenti:

* Accedi a Content Hub utilizzando il seguente collegamento:

  `https://experience.adobe.com/#/assets/contenthub`

* Accedi a `experience.adobe com` e fai clic su **[!UICONTROL Experience Manager Assets Content Hub]** disponibile nella sezione **[!UICONTROL Accesso rapido]**:
  ![Accedere a Content Hub](assets/access-content-hub.png)

* Accedi a `experience.adobe com` e fai clic su **[!UICONTROL Experience Manager Assets Content Hub]** disponibile nel commutatore del prodotto:
  ![Metodo 3 per accedere a Content Hub](assets/access-content-hub-alternate.png)

### Disattiva le notifiche e-mail agli utenti {#disable-email-notifications}

Se gli amministratori devono disabilitare le notifiche e-mail inviate agli utenti quando vengono aggiunte al profilo di prodotto Content Hub:

Fai clic sull&#39;icona di ricerca accanto al nome del profilo di prodotto e disabilita l&#39;interruttore **[!UICONTROL Notifica agli utenti via e-mail]**.

![Disabilita notifiche e-mail](assets/disable-email-notifications.png)


## Passaggio 4: integrare gli utenti di Content Hub con i diritti per aggiungere risorse (facoltativo) {#onboard-content-hub-users-add-assets}

Gli utenti di Content Hub con i diritti per aggiungere risorse possono [caricare nuove risorse approvate dal marchio in Content Hub](/help/assets/upload-brand-approved-assets.md).

Per integrare gli utenti di Content Hub con i diritti per l’aggiunta di utenti:

1. [Dopo aver aggiunto l&#39;utente al profilo di prodotto Content Hub](#onboard-content-hub-users), accedere ai profili di prodotto Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell&#39;elenco dei prodotti in Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console mostra due profili di prodotto per AEM as a Cloud Service: Amministratori e Utenti.
1. Fai clic sul profilo di prodotto Utenti e fai clic su **[!UICONTROL Aggiungi utenti]** per aggiungere l&#39;utente al profilo di prodotto.
   ![Profilo prodotto utente](assets/aem-cs-user-product-profile.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

## Passaggio 4: integrare gli utenti di Content Hub con diritti per il remix delle risorse in nuove varianti (facoltativo) {#onboard-content-hub-users-remix-assets}

Gli utenti di Content Hub con diritti per il remix delle risorse in nuove varianti possono [modificare le risorse esistenti utilizzando Adobe Express e salvare la risorsa nell&#39;archivio](/help/assets/edit-images-content-hub.md). La modifica delle risorse tramite Adobe Express è disponibile solo se l’utente dispone di diritti Adobe Express.

Per integrare gli utenti di Content Hub con diritti per il remix delle risorse in nuove varianti:

1. [Dopo aver aggiunto l&#39;utente al profilo di prodotto Content Hub](#onboard-content-hub-users), accedere ai profili di prodotto Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell&#39;elenco dei prodotti in Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console mostra due profili di prodotto per AEM as a Cloud Service: Amministratori e Utenti.
1. Fai clic sul profilo di prodotto Utenti e fai clic su **[!UICONTROL Aggiungi utenti]** per aggiungere l&#39;utente al profilo di prodotto.
   ![Profilo prodotto utente](assets/aem-cs-user-product-profile.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

## Utenti Experience Manager Assets {#experience-manager-assets-users}

Gli utenti di Experience Manager Assets possono approvare le risorse su AEM as a Cloud Service in modo che siano disponibili su Content Hub.

Per configurare gli utenti di Experience Manager Assets:

1. Accedi ai profili di prodotto di Experience Manager Assets facendo clic sul nome del prodotto AEM as a Cloud Service nell’elenco dei prodotti su Admin Console.

1. Fai clic sull’istanza di authoring di produzione per AEM as a Cloud Service:
   ![Profili di prodotto per AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   Admin Console mostra due profili di prodotto per AEM as a Cloud Service: Amministratori e Utenti.
1. Fai clic sul profilo di prodotto Utenti e fai clic su **[!UICONTROL Aggiungi utenti]** per aggiungere l&#39;utente al profilo di prodotto.
   ![Profilo prodotto utente](assets/aem-cs-user-product-profile.png)

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

   >[!NOTE]
   >
   > Non è necessario essere aggiunti al [profilo di prodotto Content Hub](#onboard-content-hub-users) per gli utenti di Experience Manager Assets.

## Abilita Content Hub per i clienti Assets as a Cloud Service esistenti {#enable-content-hub-exisitng-cs-customers}

I clienti Assets as a Cloud Service esistenti hanno 250 utenti Content Hub Limited inclusi nella licenza. Per abilitare Content Hub, effettua le seguenti operazioni:

1. [Abilita Content Hub per Experience Manager Assets tramite Cloud Manager](#enable-content-hub).

1. [Onboarding degli utenti con limitazioni di Content Hub](#onboard-content-hub-users). Questi utenti possono accedere alle risorse disponibili nel portale, ma non possono aggiungere nuove risorse o modificare quelle esistenti.

1. Se gli utenti devono aggiungere risorse al portale Content Hub, aggiungerle al profilo di prodotto `AEM Users`. Per ulteriori informazioni, consulta [Eseguire l&#39;onboarding degli utenti di Content Hub con i diritti per aggiungere risorse](#onboard-content-hub-users-add-assets).

1. Se gli utenti devono accedere all&#39;interfaccia utente di Content Hub Configuration, aggiungerli al profilo di prodotto `AEM Administrators`. Per ulteriori informazioni, vedere [Amministratore onboard di Content Hub](#onboard-content-hub-administrator).

Se gli utenti non ottengono i privilegi appropriati anche dopo averli aggiunti ai profili di prodotto pertinenti, contatta il rappresentante Adobe.
