---
title: Come integrare Adobe Sign con AEM Forms?
description: Scopri come configurare Adobe Sign per [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 7b233d95e27325a7edb22948669f6c0d96e1f380
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 1%

---

# Integrare [!DNL Adobe Sign] con [!DNL AEM Forms] as a Cloud Service  {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per Adaptive Forms. Le firme elettroniche consentono di migliorare i flussi di lavoro per l&#39;elaborazione di documenti relativi a questioni legali, vendite, retribuzioni, gestione delle risorse umane e molte altre aree.

In un tipico [!DNL Adobe Sign] e nello scenario Forms adattivo, un utente compila un modulo adattivo da applicare a un servizio. Ad esempio, la richiesta di una carta di credito e il modulo relativo ai benefit per i cittadini. Quando un utente compila, invia e firma il modulo di richiesta, questo viene inviato al fornitore di servizi per ulteriori azioni. Il provider di servizi esamina l&#39;applicazione e utilizza [!DNL Adobe Sign] per contrassegnare la domanda approvata. Per abilitare flussi di lavoro di firma elettronica simili, puoi integrare [!DNL Adobe Sign] con [!DNL AEM Forms].

Da utilizzare [!DNL Adobe Sign] con [!DNL AEM Forms], configura [!DNL Adobe Sign] in AEM Cloud Services:

## Prerequisiti {#prerequisites}

Per integrare è necessario quanto segue [!DNL Adobe Sign] con [!DNL AEM Forms]:

* Un elemento attivo [account sviluppatore Adobe Sign](https://acrobat.adobe.com/us/en/sign/developer-form.html).
* Un [Applicazione API Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenziali (ID client e segreto client) di [!DNL Adobe Sign] applicazione API.
* Utilizzare [chiave di crittografia identica](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#make-sure-you-properly-replicate-encryption-keys-when-needed) per le istanze di authoring e pubblicazione.
* (Solo per autenticazione basata su documento ufficiale) [Abilita il metodo di autenticazione](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) per l’autenticazione tramite documento ufficiale.

## Configurare [!DNL Adobe Sign] con [!DNL AEM Forms] {#configure-adobe-sign-with-aem-forms}

Dopo aver impostato i prerequisiti, effettua le seguenti operazioni per configurare [!DNL Adobe Sign] con [!DNL AEM Forms] sulle istanze Autore.

1. Nell’istanza di authoring di AEM Forms, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.
1. Il giorno **[!UICONTROL Browser configurazioni]** pagina, tocca **[!UICONTROL Crea]**.
1. In **[!UICONTROL Crea configurazione]** , specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]**, e tocca **[!UICONTROL Crea]**. Crea un contenitore di configurazione per archiviare i Cloud Services. Verificare che il nome della cartella non contenga spazio.
1. Accedi a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e apri il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >Quando crei un modulo adattivo, specifica il nome del contenitore in **[!UICONTROL Contenitore configurazione]** campo.

1. Nella pagina di configurazione, tocca **[!UICONTROL Crea]** per creare [!DNL Adobe Sign] in AEM Forms.
1. In **[!UICONTROL Generale]** scheda di **[!UICONTROL Crea configurazione Adobe Sign]** , specificare un **[!UICONTROL Nome]** per la configurazione, quindi tocca **[!UICONTROL Successivo]**. Facoltativamente, puoi specificare un valore **[!UICONTROL Titolo]** e sfoglia per selezionare un **[!UICONTROL Miniatura]** per la configurazione.

1. Copiare l&#39;URL nella finestra del browser corrente in un blocco note. L’URL è necessario per configurare [!DNL Adobe Sign] applicazione con [!DNL AEM Forms] in un passaggio successivo. Tocca **[!UICONTROL Successivo]**.

1. In **[!UICONTROL Impostazioni]** , la scheda **[!UICONTROL URL OAuth]** contiene l’URL predefinito. Il formato dell’URL è:

   `https://<shard>/public/oAuth/v2`

   Esempio:
   `https://secure.na1.echosign.com/public/oauth/v2`

   Dove:

   **na1** fa riferimento alla partizione di database predefinita. È possibile modificare il valore della partizione del database. Assicurati che [!DNL  Adobe Sign] Le configurazioni cloud puntano al [partitura corretta](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   Se ne crei un altro [!DNL Adobe Sign] per una funzione o un componente di Adobe Experience Manager, assicurati che tutte le [!DNL Adobe Sign] Le configurazioni cloud puntano alla stessa partizione.

   >[!NOTE]
   >
   > Mantieni **Crea configurazione Adobe Sign** pagina aperta. Non chiuderlo. Puoi recuperare **ID client** e **Segreto client** dopo aver configurato le impostazioni OAuth per [!DNL Adobe Sign] come descritto nei passaggi successivi.


1. Configurare le impostazioni OAuth per [!DNL Adobe Sign] applicazione:

   1. Apri una finestra del browser e accedi al tuo [!DNL Adobe Sign] account sviluppatore.
   1. Seleziona l’applicazione configurata per [!DNL AEM Forms], e tocca **[!UICONTROL Configurare OAuth per l’applicazione]**.
   1. In **[!UICONTROL URL di reindirizzamento]** , aggiungere l&#39;URL copiato in un passaggio precedente (passaggio 7) e fare clic su **[!UICONTROL Salva]**.
   1. Abilita il seguente ambito per [!DNL Adobe Sign] e fare clic su **[!UICONTROL Salva]**.
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un [!DNL Adobe Sign] e ottenere le chiavi, consulta [Configurare le impostazioni OAuth per l&#39;applicazione](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) documentazione per gli sviluppatori.

   ![Configurazione OAuth](assets/oauthconfig_new.png)

1. Torna a **[!UICONTROL Crea configurazione Adobe Sign]** pagina. In **[!UICONTROL Impostazioni]** , specificare il [**[!UICONTROL ID client]** (indicato anche come ID applicazione) e **[!UICONTROL Segreto client]**]. Utilizza il [ID client e segreto client dell’applicazione Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) creato nel passaggio precedente.

1. Seleziona la **[!UICONTROL Abilita Adobe Sign per gli allegati]** opzione per aggiungere i file allegati a un modulo adattivo al [!DNL Adobe Sign] documento inviato per la firma.

1. Tocca **[!UICONTROL Connettersi ad Adobe Sign]**. Quando vengono richieste le credenziali, specifica il nome utente e la password dell’account utilizzato durante la creazione [!DNL Adobe Sign] applicazione. Quando ti viene richiesto di confermare l’accesso per `your developer account`, fai clic su **[!UICONTROL Consenti accesso]**. Se le credenziali sono corrette e si consente [!DNL AEM Forms] per accedere al [!DNL Adobe Sign] per gli sviluppatori, viene visualizzato un messaggio di successo simile al seguente.

   ![Configurazione cloud Adobe Sign completata](assets/adobe-sign-cloud-configuration-success.png)

1. Tocca **[!UICONTROL Crea]** per creare [!DNL Adobe Sign] configurazione.

1. Seleziona la configurazione e fai clic su **[!UICONTROL Pubblica]**, seleziona la configurazione e fai clic su **[!UICONTROL Pubblica]**. Replica la configurazione negli ambienti di pubblicazione corrispondenti.

1. Ripeti tutti i passaggi precedenti sulle istanze di sviluppo, staging e produzione (a seconda di quale sia il passaggio rimasto) per completare la configurazione [!DNL Adobe Sign] con [!DNL AEM Forms] per il tuo ambiente.

Ora puoi [utilizzare aggiungere campi Adobe Sign a un modulo adattivo](working-with-adobe-sign.md). Accertati di aggiungere il contenitore di configurazione utilizzato per il Cloud Service a tutti i Forms adattivi abilitati per [!DNL Adobe Sign]. È possibile specificare un contenitore di configurazione dalle proprietà di un modulo adattivo.

## (Solo per flussi di lavoro AEM) Configura [!DNL Adobe Sign] per sincronizzare lo stato della firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Quando si utilizza [!DNL Adobe Sign] Passaggio del flusso di lavoro per firmare un modulo adattivo, il modulo può essere trasmesso tra i firmatari uno dopo l’altro o può essere inviato a tutti i firmatari contemporaneamente, a seconda della configurazione del passaggio del flusso di lavoro. [!DNL Adobe Sign] Forms adattivo abilitato vengono inviati a Experience Manager Forms Server solo dopo che tutti i firmatari hanno completato il processo di firma.

Per impostazione predefinita, il [!DNL Adobe Sign] I servizi di pianificazione controllano (polling) la risposta del firmatario dopo ogni 24 ore. È possibile modificare l’intervallo predefinito per l’ambiente.

Per modificare l&#39;intervallo predefinito, specificare un [espressione cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) per **sign.status.exp** proprietà del **Servizio di configurazione Adobe Sign** configurazione.

Ad esempio, per eseguire il servizio di configurazione ogni giorno alle 00:00, impostare **sign.status.exp** proprietà del **Servizio di configurazione Adobe Sign** configurazione da specificare `0 0 0 1/1 * ? *`. Il seguente file JSON mostra l’esempio per eseguire il servizio di configurazione ogni giorno alle 00:00:

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

Per impostare i valori di una configurazione: [Generare configurazioni OSGi utilizzando l’SDK per AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart), e [distribuire la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) all’istanza di Cloud Service.

<!-- , perform the following steps:

1. Log in to [!DNL AEM Forms] Server with admin credentials and navigate to **[!UICONTROL Tools]** &gt;**[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   You can also open the following URL in a browser window:
   `https://server/system/console/configMgr`

1. Locate and open the **[!UICONTROL Adobe Sign Configuration Service]** option. Specify a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) in the **Status Update Scheduler Expression** field and click **Save**. For example, to run the configuration service daily at 00:00 am, specify `0 0 0 1/1 * ? *` in the **Status Update Scheduler Expression** field.

Default interval to sync status of [!DNL Adobe Sign] is now changed. -->

## Articoli correlati {#related-articles}

* [Utilizzo di Adobe Sign in un modulo adattivo](working-with-adobe-sign.md)

* [Best practice per l’utilizzo di Adobe Sign con Adaptive Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
