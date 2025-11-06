---
title: Come integrare Adobe Acrobat Sign con AEM Forms?
description: Scopri come configurare Adobe Acrobat Sign per  [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms, Acrobat Sign
role: Admin, User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 1%

---

# Connetti [!DNL AEM Forms] as a Cloud Service con [!DNL Adobe Acrobat Sign] {#integrate-adobe-sign-with-aem-forms}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms.html#adobe-acrobat-sign-for-government) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Acrobat Sign] abilita i flussi di lavoro di firma elettronica per i flussi di lavoro Adaptive Forms e AEM. Le firme elettroniche consentono di migliorare i flussi di lavoro per l&#39;elaborazione di documenti relativi a questioni legali, vendite, retribuzioni, gestione delle risorse umane e molte altre aree.

In uno scenario tipico di [!DNL Adobe Acrobat Sign] e Forms adattivo, un utente compila un modulo adattivo da applicare a un servizio. Ad esempio, la richiesta di una carta di credito e il modulo relativo ai benefit per i cittadini. Quando un utente compila, invia e firma il modulo di richiesta, questo viene inviato al fornitore di servizi per ulteriori azioni. Il provider di servizi esamina l&#39;applicazione e utilizza [!DNL Adobe Acrobat Sign] per contrassegnarla come approvata. AEM Forms supporta sia Adobe Acrobat Sign che Adobe Acrobat Sign Solutions for Government. A seconda della licenza e dei requisiti, puoi integrare o collegare AEM Forms con una delle seguenti soluzioni:

* [Collegare AEM Forms a Adobe Acrobat Sign](#adobe-sign)
* [Collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government](#adobe-acrobat-sign-for-government)

## Collegare AEM Forms a Adobe Acrobat Sign {#adobe-sign}

Per connettere **[!DNL AEM Forms]** a **[!DNL Adobe Acrobat Sign]**, configura il software e gli account elencati nella sezione dei prerequisiti e configura Adobe Sign Cloud Service nelle istanze Forms as a Cloud Service Author e Publish:

### Prerequisiti per collegare AEM Forms a Adobe Acrobat Sign {#prerequisites-for-adobe-sign}

Per integrare [!DNL Adobe Acrobat Sign] con [!DNL AEM Forms] è necessario eseguire l&#39;installazione seguente:

1. Un account sviluppatore [Adobe Acrobat Sign attivo.](https://www.adobe.com/acrobat/business/developer-form.html)
1. Applicazione API [Adobe Acrobat Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
1. Credenziali (ID client e segreto client) dell&#39;applicazione API [!DNL Adobe Acrobat Sign].
1. (Solo per autenticazione basata su documento ufficiale) [Abilitare il metodo di autenticazione](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) per l&#39;autenticazione tramite documento ufficiale.

### Connettere le istanze di authoring e pubblicazione di AEM Forms con Adobe Acrobat Sign {#configure-adobe-sign-with-aem-forms}

Dopo aver impostato i prerequisiti, eseguire la procedura seguente per configurare [!DNL Adobe Acrobat Sign] con [!DNL AEM Forms] nelle istanze di authoring.

1. Nell&#39;istanza Autore AEM Forms, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.
1. Nella pagina **[!UICONTROL Browser configurazioni]**, selezionare **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]** e seleziona **[!UICONTROL Crea]**. Crea un contenitore di configurazione per archiviare Cloud Services. Verificare che il nome della cartella non contenga spazio.
1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Adobe Acrobat Sign]** e apri il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >Quando crei un modulo adattivo, specifica il nome del contenitore nel campo **[!UICONTROL Contenitore configurazione]**.

1. Nella pagina di configurazione, seleziona **[!UICONTROL Crea]** per creare la configurazione [!DNL Adobe Acrobat Sign] in AEM Forms.
1. Nella scheda **[!UICONTROL Generale]** della pagina **[!UICONTROL Crea configurazione Adobe Acrobat Sign]**, specifica un **[!UICONTROL Nome]** per la configurazione e seleziona **[!UICONTROL Avanti]**. Facoltativamente, puoi specificare un **[!UICONTROL Titolo]** e cercare di selezionare una **[!UICONTROL Miniatura]** per la configurazione.

1. Ora puoi **[!UICONTROL Selezionare la soluzione]** per selezionare [!DNL Adobe Acrobat Sign].

   <!--![Adobe Acrobat Sign Solutions](assets/adobe-sign-solution.png)-->
   ![Configurazione Adobe Acrobat Sign Solutions](assets/adobe-sign-solution-config.png)

<!--

[create URL](#create-a-redirect-url-for-your-aem-instance)
 -->

1. Copiare l&#39;URL presente nella finestra del browser corrente in un blocco note e rimuovere la parte `/ui#/aem` dall&#39;URL. L&#39;URL modificato è quindi necessario per configurare l&#39;applicazione [!DNL Adobe Acrobat Sign] con [!DNL AEM Forms], in un passaggio successivo. Seleziona **[!UICONTROL Avanti]**.

1. Nella scheda **[!UICONTROL Impostazioni]**,
   * il campo **[!UICONTROL URL OAuth]** contiene l&#39;URL predefinito che include la partizione del database di Adobe Sign. Il formato dell’URL è:

     `https://<shard>/public/oauth/v2`

     Ad esempio:
     `https://secure.na1.echosign.com/public/oauth/v2`

   * il campo **[!UICONTROL URL token di accesso]** contiene l&#39;URL predefinito che include la partizione del database di Adobe Sign. Il formato dell’URL è:

     `https://<shard>/oauth/v2/token`

     Ad esempio:
     `https://api.na1.echosign.com/oauth/v2/token`

   dove:

   **na1** fa riferimento alla partizione di database predefinita. È possibile modificare il valore della partizione del database. Verificare che le [!DNL  Adobe Acrobat Sign] configurazioni cloud puntino alla [partizione corretta](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   >* Mantieni aperta la pagina **Crea configurazione Adobe Acrobat Sign**. Non chiuderlo. È possibile recuperare **ID client** e **Segreto client** dopo aver configurato le impostazioni OAuth per l&#39;applicazione [!DNL Adobe Acrobat Sign] come descritto nei passaggi successivi.
   >* Dopo aver effettuato l&#39;accesso all&#39;account Adobe Sign, passa a **[!UICONTROL API Acrobat Sign]** > **[!UICONTROL Informazioni API]** > **[!UICONTROL Documentazione dei metodi REST API]** > **[!UICONTROL Token di accesso OAuth]** per accedere alle informazioni relative all&#39;URL OAuth di Adobe Sign e all&#39;URL del token di accesso.

1. Configurare le impostazioni OAuth per l&#39;applicazione [!DNL Adobe Acrobat Sign]:

   1. Apri una finestra del browser e accedi al tuo account sviluppatore [!DNL Adobe Acrobat Sign].
   1. Selezionare l&#39;applicazione configurata per [!DNL AEM Forms] e selezionare **[!UICONTROL Configura OAuth per l&#39;applicazione]**.
   1. Nella casella **[!UICONTROL URL di reindirizzamento]**, aggiungi l&#39;URL copiato in un passaggio precedente (passaggio 8) e fai clic su **[!UICONTROL Salva]**.
   1. Abilitare l&#39;ambito seguente per l&#39;applicazione [!DNL Adobe Acrobat Sign] e fare clic su **[!UICONTROL Salva]**.

   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   >[!NOTE]
   > È possibile modificare il modificatore ambiti da `self` a `account` direttamente dall&#39;interfaccia utente di AEM, come indicato nel passaggio 12.

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un&#39;applicazione [!DNL Adobe Acrobat Sign] e ottenere le chiavi, vedere [Configurare le impostazioni OAuth per la documentazione per gli sviluppatori dell&#39;applicazione](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

   ![Configurazione OAuth](/help/forms/assets/oauthconfig-new.png)

1. Tornare alla pagina **[!UICONTROL Crea configurazione Adobe Acrobat Sign]**. Nella scheda **[!UICONTROL Impostazioni]**, specifica [**[!UICONTROL ID client]** (noto anche come ID applicazione) e **[!UICONTROL Segreto client]**]. Utilizza l&#39;[ID client e segreto client dell&#39;applicazione Adobe Acrobat Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) creati nel passaggio precedente.

1. Nella sezione [!UICONTROL Ambito autorizzazione] è possibile modificare gli ambiti in &quot;account&quot; o &quot;self&quot; aggiungendo il prefisso &quot;self&quot; o &quot;account&quot; agli ambiti, in base alle esigenze.
   ![Ambito autorizzazione](/help/forms/assets/authorization-scope.png)

1. Selezionare l&#39;opzione **[!UICONTROL Abilita Adobe Acrobat Sign per gli allegati]** per aggiungere i file allegati a un modulo adattivo al documento [!DNL Adobe Acrobat Sign] corrispondente inviato per la firma.

1. Selezionare **[!UICONTROL Connetti a Adobe Acrobat Sign]**. Quando vengono richieste le credenziali, fornire **nomeutente** e **password** dell&#39;account utilizzato durante la creazione dell&#39;applicazione [!DNL Adobe Acrobat Sign]. Quando viene richiesto di confermare, accedere a `your developer account`, fare clic su **[!UICONTROL Consenti accesso]**. Se le credenziali sono corrette e si consente a [!DNL AEM Forms] di accedere all&#39;account sviluppatore [!DNL Adobe Acrobat Sign], verrà visualizzato un messaggio di operazione riuscita simile al seguente.

   ![Configurazione cloud Adobe Acrobat Sign completata](assets/adobe-sign-cloud-configuration-success.png)

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione di [!DNL Adobe Acrobat Sign].

1. Seleziona la configurazione e fai clic su **[!UICONTROL Pubblica]**, seleziona la configurazione e fai clic su **[!UICONTROL Pubblica]**. Replica la configurazione negli ambienti di pubblicazione corrispondenti.

1. Ripeti tutti i passaggi precedenti per le istanze di sviluppo, stage e produzione (qualsiasi sia rimasto) per completare la configurazione di [!DNL Adobe Acrobat Sign] con [!DNL AEM Forms] per il tuo ambiente.

Ora puoi [utilizzare l&#39;aggiunta di campi Adobe Acrobat Sign a un modulo adattivo](working-with-adobe-sign.md). Accertati di aggiungere il contenitore di configurazione utilizzato per Cloud Service a tutto il Forms adattivo abilitato per [!DNL Adobe Acrobat Sign]. È possibile specificare un contenitore di configurazione dalle proprietà di un modulo adattivo.

>[!NOTE]
>
> Per configurare la sandbox di Adobe Sign, puoi seguire gli stessi passaggi di configurazione descritti in [Adobe Sign](#adobe-sign).

#### Risoluzione di problemi {#resolve-config-error}

Quando si connette [!DNL Adobe Acrobat Sign] a [!DNL AEM Forms] e si trova un errore `Unable to authorize access because the client configuration is invalid: invalid_request`, come illustrato nell&#39;immagine seguente. Per risolvere il problema, segui questi passaggi:

![Errore di configurazione](/help/forms/assets/config_error_sign.png)

1. Copiare l&#39;URL presente nella finestra del browser corrente in un blocco note e rimuovere la parte `/ui#/aem` dall&#39;URL.
1. Apri una finestra del browser e accedi al tuo account sviluppatore [!DNL Adobe Acrobat Sign].
1. Selezionare l&#39;applicazione configurata per [!DNL AEM Forms] e selezionare **[!UICONTROL Configura OAuth per l&#39;applicazione]**.
1. Nella casella **[!UICONTROL URL di reindirizzamento]**, aggiungi l&#39;URL copiato in un passaggio precedente e fai clic su **[!UICONTROL Salva]**.

## Collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government {#adobe-acrobat-sign-for-government}

La connessione di AEM Forms ad Adobe Acrobat Sign Solutions for Government è un processo in più fasi. Comporta:

* Creazione di un URL di reindirizzamento per le istanze di AEM
* Condivisione dell’URL di reindirizzamento e degli ambiti con il team delle soluzioni Adobe Sign per la pubblica amministrazione
* Ricezione delle credenziali dal team Adobe Sign
* Utilizzo delle credenziali ricevute per collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government

![Flusso di lavoro per la pubblica amministrazione di Adobe Sign](/help/forms/assets/adobe-acrobat-sign-govt-workflow.png)


AEM Forms as a Cloud Service fornisce ambienti di sviluppo, staging e produzione. È possibile iniziare con la connessione dell’ambiente di sviluppo per con Adobe Acrobat Sign Solutions for Government e collegare successivamente l’area di visualizzazione e gli ambienti di produzione.

### Prima di iniziare {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Prima di iniziare a collegare AEM Forms con la soluzione Adobe Acrobat Sign, assicurati che sia stato eseguito il provisioning del tuo account [Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning).


### Collegare AEM Forms as a Cloud Service ad Adobe Acrobat Sign Solutions for Government {#connect-adobe-acrobat-sign-for-government}

#### Creare un URL di reindirizzamento per l’istanza di AEM

1. Nell&#39;istanza di authoring di Forms as a Cloud Service, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.
1. Nella pagina **[!UICONTROL Browser configurazioni]**, selezionare **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]** e seleziona **[!UICONTROL Crea]**. Crea un contenitore di configurazione per archiviare Cloud Services. Verificare che il nome della cartella non contenga spazio.
1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Adobe Acrobat Sign]** e apri il contenitore di configurazione creato nel passaggio precedente. Quando crei un modulo adattivo, specifica il nome del contenitore nel campo **[!UICONTROL Contenitore configurazione]**.
1. Nella pagina di configurazione, seleziona **[!UICONTROL Crea]** per creare la configurazione [!DNL Adobe Acrobat Sign] in AEM Forms.
1. Copiare l&#39;URL della finestra del browser corrente in un blocco note e rimuovere `/ui#/aem` dall&#39;URL. Questo URL è denominato `re-direct URL`.
Nella sezione successiva, condividi `re-direct URL` e `Scopes` con il team Adobe Sign e richiedi le credenziali (ID client e Segreto client).

#### Condividi l’URL di reindirizzamento e gli ambiti con il team di Adobe Sign e ricevi le credenziali

Il team Adobe Acrobat Sign for Government Solutions richiede che `re-direct URL` e gli ambiti specifici siano abilitati per l&#39;applicazione Adobe Acrobat Sign (elencata di seguito) per generare le credenziali (ID client e segreto client) che consentono di connettere AEM Forms ad Adobe Acrobat Sign Solutions for Government.

Condividi `scopes` (elencato di seguito) e `re-direct URL` creati e annotati nell&#39;ultimo passaggio della sezione precedente con il tuo rappresentante Adobe Acrobat Sign for Government Solution ([membro del team Adobe Professional Services](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password)).

**_Ambiti_**

* [!DNL aggrement_read]
* [!DNL aggrement_write]
* [!DNL aggrement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

Il rappresentante genera e condivide le credenziali con te. Nella sezione successiva utilizzi le credenziali (ID client e Segreto client) per collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government.

#### Utilizza le credenziali ricevute per collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government

1. Apri `re-direct URL` nel browser. Hai creato e annotato `re-direct URL` nell&#39;ultimo passaggio di [creazione di un URL di reindirizzamento nell&#39;istanza di AEM](#create-a-redirect-url-for-your-aem-instance).

1. Nella scheda **[!UICONTROL Generale]** della pagina **[!UICONTROL Crea configurazione Adobe Sign]**, specifica un **[!UICONTROL Nome]** per la configurazione e seleziona **[!UICONTROL Avanti]**. Facoltativamente, puoi specificare un **[!UICONTROL Titolo]** e cercare di selezionare una **[!UICONTROL Miniatura]** per la configurazione. Fai clic su **[!UICONTROL Avanti]**.

1. Nella scheda **[!UICONTROL Impostazioni]** della pagina **[!UICONTROL Crea configurazione Adobe Sign]**, per l&#39;opzione **[!UICONTROL Seleziona soluzione]**, selezionare [!DNL Adobe Acrobat Sign Solutions for Government].


   ![Adobe Acrobat Sign Solutions per enti pubblici](assets/adobe-sign-for-govt.png)

1. Nel campo **[!UICONTROL E-mail]**, specifica l&#39;indirizzo e-mail associato al tuo account Adobe Acrobat Sign Solutions for Government.

1. Nella scheda **[!UICONTROL Impostazioni]**,
   * il campo **[!UICONTROL URL OAuth]** contiene l&#39;URL predefinito che include la partizione del database di Adobe Sign. Il formato dell’URL è:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     Ad esempio:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * il campo **[!UICONTROL URL token di accesso]** contiene l&#39;URL predefinito che include la partizione del database di Adobe Sign. Il formato dell’URL è:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     Ad esempio:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   dove:

   **na1** fa riferimento alla partizione di database predefinita. È possibile modificare il valore della partizione del database. Verificare che le [!DNL  Adobe Acrobat Sign] configurazioni cloud puntino alla [partizione corretta](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   > * Dopo aver effettuato l&#39;accesso all&#39;account Adobe Sign, passa a **[!UICONTROL API Acrobat Sign]** > **[!UICONTROL Informazioni API]** > **[!UICONTROL Documentazione dei metodi REST API]** > **[!UICONTROL Token di accesso OAuth]** per accedere alle informazioni relative all&#39;URL oAuth di Adobe Sign e all&#39;URL del token di accesso.

1. Utilizza le credenziali condivise da Adobe Acrobat Sign per il rappresentante di soluzioni governative ([membro del team Adobe Professional Services]) nella sezione precedente come [**[!UICONTROL ID client]** e **[!UICONTROL Segreto client]**].

1. Selezionare l&#39;opzione **[!UICONTROL Abilita Adobe Acrobat Sign per gli allegati]** per aggiungere i file allegati a un modulo adattivo al documento [!DNL Adobe Acrobat Sign] corrispondente inviato per la firma.

1. Seleziona **[!UICONTROL Connetti ad Adobe Sign]**. Quando vengono richieste le credenziali, specificare il nome utente e la password dell&#39;account utilizzato durante la creazione dell&#39;applicazione [!DNL Adobe Acrobat Sign]. Quando viene richiesto di confermare l&#39;accesso per `your developer account`, fare clic su **[!UICONTROL Consenti accesso]**. Se le credenziali sono corrette e si consente a [!DNL AEM Forms] di accedere all&#39;account sviluppatore [!DNL Adobe Acrobat Sign], verrà visualizzato un messaggio di operazione riuscita simile al seguente.

   ![Configurazione cloud Adobe Acrobat Sign completata](assets/adobe-sign-cloud-configuration-success.png)

   <!-- 
      > When prompted for credentials, provide username and password of the account used while creating [!DNL Adobe Acrobat Sign] application. When asked to confirm access for `your developer account`, Click **[!UICONTROL Allow Access]**. 
      -->

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione.

1. Seleziona la configurazione e fai clic su **[!UICONTROL Pubblica]**, seleziona la configurazione e fai clic su **[!UICONTROL Pubblica]**. Replica la configurazione negli ambienti di pubblicazione corrispondenti.

1. Ripeti tutti i passaggi precedenti per le istanze di sviluppo, stage e produzione (qualsiasi sia rimasto) per completare la configurazione di [!DNL Adobe Acrobat Sign Solutions for Government] con [!DNL AEM Forms] per il tuo ambiente.

Ora puoi [utilizzare Aggiungi campi Adobe Acrobat Sign in un modulo adattivo](working-with-adobe-sign.md) o [flusso di lavoro AEM](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Assicurarsi di aggiungere il contenitore di configurazione utilizzato per la configurazione di Cloud Service a tutto il Forms adattivo abilitato per [!DNL Adobe Acrobat Sign]. È possibile specificare un contenitore di configurazione dalle proprietà di un modulo adattivo.

## Configura l&#39;utilità di pianificazione [!DNL Adobe Acrobat Sign] per sincronizzare lo stato di firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

AEM Forms as a Cloud Service fornisce un servizio di pianificazione che controlla lo stato dei firmatari a intervalli definiti. Gli scenari in cui si configura il servizio di pianificazione:

* Se si utilizza [Invia il modulo (dopo che ogni destinatario ha completato la cerimonia di firma)](/help/forms/working-with-adobe-sign.md#select-adobe-sign-cloud-service-and-signing-order) per firmare un documento, il modulo verrà inviato solo dopo che tutti i firmatari avranno firmato il modulo.
* Se si utilizza il [passaggio di firma in un flusso di lavoro AEM](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step) per firmare un documento, il passaggio di firma attende che tutti i firmatari firmino il documento prima di procedere al passaggio successivo del flusso di lavoro.

Per impostazione predefinita, i servizi di pianificazione [!DNL Adobe Acrobat Sign] controllano (polling) la risposta del firmatario dopo ogni 24 ore. È possibile modificare l’intervallo predefinito per l’ambiente.

Per modificare l&#39;intervallo predefinito, specificare un&#39;espressione [cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) per la proprietà **sign.status.exp** della configurazione **Servizio di configurazione di Adobe Acrobat Sign**.

Ad esempio, per eseguire il servizio di configurazione ogni giorno alle 00:00, impostare la proprietà **sign.status.exp** della configurazione **Servizio di configurazione di Adobe Acrobat Sign** per specificare `0 0 0 1/1 * ? *`. Nel seguente file JSON viene visualizzato l&#39;esempio per l&#39;esecuzione giornaliera del servizio di configurazione alle 00:00:

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

Per impostare i valori di una configurazione, [Genera configurazioni OSGi utilizzando AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [distribuisci la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) nell&#39;istanza Cloud Service.

## Domande frequenti

* **Q: posso eseguire il rendering della pagina di firma GovCloud di Adobe Sign in un iframe?**
* **A:** Sì, puoi eseguire il rendering della pagina Adobe Sign GovCloud Signature in un iframe.

>[!MORELIKETHIS]
>
>* [Firma un modulo tramite firma digitale](/help/forms/signing-forms-using-scribble.md)
>* [Best practice per l&#39;utilizzo di Adobe Acrobat Sign con Adaptive Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
