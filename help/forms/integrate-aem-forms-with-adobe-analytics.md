---
title: Come integrare AEM Forms con Adobe Analytics?
seo-title: Learn how to integrate AEM Forms with Adobe Analytics.
exl-id: 0730432e-75b8-4b35-a377-ae4a2bee6c9f
hidefromtoc: true
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: 64a8b363cff079aa0a6f56effd77830ac797deca
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 1%

---

# Integrare AEM Forms con [!DNL Adobe Analytics] {#integrate-aem-forms-with-adobe-analytics}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

<span class="preview"> Questo documento illustra la procedura manuale per abilitare Adobe Analytics in un modulo adattivo. Tuttavia, Adobe consiglia di utilizzare [Abilitare Adobe Analytics per un modulo adattivo utilizzando Experience Cloud Setup Automation](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md). </span>

AEM Forms si integra con [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=it) per consentire di acquisire e tenere traccia delle metriche delle prestazioni per i moduli pubblicati. L’obiettivo dell’analisi di queste metriche è quello di consentire agli utenti aziendali di ottenere informazioni sul comportamento degli utenti finali e di ottimizzare l’esperienza di acquisizione dei dati. Puoi acquisire e tenere traccia del comportamento degli utenti connessi e non connessi (anonimi) tramite Adobe Analytics for Adaptive Forms.

Dopo aver eseguito le azioni indicate in questo articolo, è possibile configurare e visualizzare i report in [!DNL Adobe Analytics], come illustrato nel video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

È possibile utilizzare [!DNL Adobe Analytics] per individuare i pattern di interazione e i problemi riscontrati dagli utenti durante l’utilizzo dei moduli adattivi. [!DNL Adobe Analytics] tiene traccia e memorizza le informazioni sui seguenti eventi:

* **Rendering**: numero di volte in cui un modulo viene aperto.

* **Invia**: numero di volte in cui un modulo viene inviato.

* **Abbandono**: numero di volte in cui gli utenti se ne vanno senza completare il modulo.

* **Errore**: numero di errori riscontrati nel pannello e nei campi del pannello.

* **Guida**: numero di volte in cui un utente apre la Guida di un pannello e dei campi del pannello.

* **Visita sul campo**: numero di volte in cui un utente visita un campo nel modulo.

* **Salva**: numero di volte in cui gli utenti salvano un modulo sul portale Forms.

Oltre a questi eventi predefiniti, puoi definire eventi personalizzati nei moduli adattivi utilizzando un editor di regole e mapparli agli eventi in [!DNL Adobe Analytics]

Nella figura seguente sono illustrate le azioni da eseguire prima di visualizzare i report in [!DNL Adobe Analytics]:

![Panoramica di Analytics](assets/analytics-workflow.png)

## 1. Configurare [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Prima di configurare [!DNL Adobe Analytics], creare:

* Un Adobe ID per accedere a [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* Una [suite di rapporti](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=it).


### Installa le estensioni AEM Forms e [!DNL Adobe Analytics] {#install-extensions}

Per configurare le estensioni AEM Forms e [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=it), effettua le seguenti operazioni:

1. Accedi a Adobe Experience Cloud e seleziona un nome appropriato per l’azienda.

1. Seleziona **[!UICONTROL Launch/Data Collection]** e seleziona **[!UICONTROL Vai a Launch/Data Collection]**.

1. Selezionare **[!UICONTROL Nuova proprietà]** e specificare un nome per la configurazione.

1. Specifica un nome di dominio e seleziona **[!UICONTROL Salva]** per salvare la proprietà.

1. Seleziona il nome della configurazione disponibile nell’elenco Proprietà tag.

1. Nella sezione **[!UICONTROL Authoring]**, seleziona **[!UICONTROL Estensioni]**.

1. Seleziona **[!UICONTROL Catalogo]** e **[!UICONTROL Installa]** per l&#39;estensione **[!UICONTROL Adobe Experience Manager Forms]**. **[!UICONTROL Adobe Experience Manager Forms]** viene visualizzato nell&#39;elenco delle estensioni installate disponibili nella scheda **Installed**.

1. Seleziona **[!UICONTROL Installa]** per l&#39;estensione **[!UICONTROL Adobe Analytics]**.
1. Seleziona il nome della suite di rapporti negli elenchi a discesa **[!UICONTROL Suite di rapporti per lo sviluppo]**, **[!UICONTROL Suite di rapporti per la gestione temporanea]** e **[!UICONTROL Suite di rapporti sui prodotti]** e seleziona **[!UICONTROL Salva]** per salvare l&#39;estensione.

### Configurare gli elementi dati {#configure-data-elements}

Puoi selezionare uno qualsiasi degli elementi dati configurati in una regola creata per un evento. Quando si verifica un evento in un modulo adattivo, AEM Forms invia questi elementi dati a [!DNL Adobe Analytics].

Dopo aver installato l&#39;estensione **[!UICONTROL Adobe Experience Manager Forms]**, puoi creare i seguenti elementi dati:

<table>
 <tbody>
  <tr>
   <td>NomeCampo</th>
   <td>FieldTitle</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>NomeModulo<br /> </td>
   <td>FormTitle<br /> </td>
   <td>NomePagina</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>Titolo pannello<br /> </td>
   <td>TimeSpent</td>
  </tr>
 </tbody>
</table>

Per configurare gli elementi dati, effettua le seguenti operazioni:

1. Nella sezione **[!UICONTROL Authoring]**, seleziona **[!UICONTROL Elementi dati]**.

1. Selezionare **[!UICONTROL Crea nuovo elemento dati]**.

1. Specifica un nome per l’elemento dati. Ad esempio, Titolo modulo per il tipo di elemento dati FormTitle.

1. Specifica **[!UICONTROL Adobe Experience Manager Forms]** come nome dell&#39;estensione.

1. Selezionare **[!UICONTROL Tipo elemento dati]**.

1. Seleziona **[!UICONTROL Salva]** per salvare l&#39;elemento dati.

>[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configurare le regole {#configure-rules}

Per creare regole basate sull&#39;estensione **[!UICONTROL Adobe Experience Manager Forms]**, effettua le seguenti operazioni:

1. Nella sezione **[!UICONTROL Authoring]**, seleziona **[!UICONTROL Regole]**.

1. Seleziona **[!UICONTROL Crea nuova regola]**.

1. Specifica un nome per la regola. Ad esempio, Invio modulo per registrare gli invii dei moduli.

1. Nella sezione **[!UICONTROL Eventi]**, seleziona **[!UICONTROL Aggiungi]**.

1. Specifica **[!UICONTROL Adobe Experience Manager Forms]** come nome dell&#39;estensione.

1. Seleziona il tipo di evento. L&#39;input per il campo **[!UICONTROL Name]** viene popolato automaticamente in base al tipo di evento selezionato.

1. Seleziona **[!UICONTROL Mantieni modifiche]** per salvare l&#39;evento.

1. Nella sezione **[!UICONTROL Azioni]**, seleziona **[!UICONTROL Aggiungi]**.

1. Specifica **[!UICONTROL Adobe Analytics]** come nome dell&#39;estensione.

1. Selezionare **[!UICONTROL Imposta variabili]** come tipo di azione. Le opzioni disponibili nell’elenco a discesa includono:

   * **[!UICONTROL Imposta variabili]**: utilizzare questo tipo di azione per definire il tipo di evento per il quale gli elementi dati selezionati vengono inviati da AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Invia beacon]**: utilizza questo tipo di azione per inviare dati da AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Cancella variabili]**: utilizzare questo tipo di azione per cancellare la traccia dati in modo che l&#39;evento venga registrato una sola volta in [!DNL Adobe Analytics].

     L&#39;approccio consigliato consiste nell&#39;utilizzare il tipo di azione **[!UICONTROL Imposta variabili]** per configurare l&#39;evento e gli elementi dati, quindi utilizzare **[!UICONTROL Invia beacon]** per inviare i dati, quindi utilizzare **[!UICONTROL Cancella variabili]** per cancellare l&#39;analisi dei dati.

1. Nella sezione **[!UICONTROL Prop]**, mappa le opzioni della suite di rapporti disponibili nell&#39;elenco a discesa con gli elementi dati definiti utilizzando [Configura elementi dati](#configure-data-elements).

   Ad esempio, per inviare l&#39;elemento dati **Titolo modulo** da AEM Forms a [!DNL Adobe Analytics] quando si invia un modulo:
   1. Nella sezione **[!UICONTROL Prop]**, seleziona una proprietà per Titolo modulo disponibile nella suite di rapporti, quindi seleziona ![Icona database](assets/database-icon.svg) per mapparla al Titolo modulo creato in [Configura elementi dati](#configure-data-elements).

      ![define-props](assets/define-props.png)

   1. Seleziona **[!UICONTROL Aggiungi altro]** per aggiungere altri elementi dati all&#39;elenco.

1. Nella sezione **[!UICONTROL Eventi]**, seleziona un evento tra le opzioni disponibili nella suite di rapporti, quindi seleziona **[!UICONTROL Mantieni modifiche]**.

1. Nella sezione **[!UICONTROL Azioni]**, seleziona + e specifica **[!UICONTROL Adobe Analytics]** come nome dell&#39;estensione.

1. Selezionare **[!UICONTROL Invia beacon]** come tipo di azione. Nel riquadro di destra, selezionare **[!UICONTROL s.t()]** per inviare dati a [!DNL Adobe Analytics] e trattarli come visualizzazioni pagina oppure **[!UICONTROL s.tl()]** per inviare dati a [!DNL Adobe Analytics] e non trattarli come visualizzazioni pagina. Seleziona **[!UICONTROL Mantieni modifiche]**.

1. Nella sezione **[!UICONTROL Azioni]**, seleziona + e specifica **[!UICONTROL Adobe Analytics]** come nome dell&#39;estensione.

1. Selezionare **[!UICONTROL Cancella variabili]** come tipo di azione. Seleziona **[!UICONTROL Mantieni modifiche]**. Dopo aver eseguito questi passaggi, la sezione **[!UICONTROL Azioni]** viene visualizzata come:
   ![Configurazione azioni](assets/actions-config.png)

   Personalizza la sezione **[!UICONTROL Azioni]** in base alle tue esigenze. Ad esempio, è possibile definire due passaggi **Invia beacon** in un flusso di azioni per inviare dati a [!DNL Adobe Analytics] e trattarli come una visualizzazione di pagina in un unico passaggio e inviare dati a [!DNL Adobe Analytics] senza considerarli come visualizzazione di pagina nel secondo passaggio.

   ![Configurazione azioni](assets/actions-config-2.png)

1. Seleziona **[!UICONTROL Salva]** per salvare la regola.

   Puoi creare regole per tutti i tipi di evento, ad esempio Abbandona, Errore, Visita campo, Aiuto, Rendering, Salva e Invia.

>[!VIDEO](https://video.tv.adobe.com/v/337425)


### Flussi Publish {#publish-flow}

Dopo aver creato gli elementi dati e averli utilizzati nelle regole, pubblicare la configurazione per raccogliere i dati del modulo in [!DNL Adobe Analytics].

Per pubblicare la configurazione, effettua le seguenti operazioni:

1. Nella sezione **[!UICONTROL Pubblicazione]**, seleziona **[!UICONTROL Flusso di pubblicazione]**.

1. Selezionare **[!UICONTROL Aggiungi libreria]**, specificare un nome e selezionare l&#39;ambiente per la libreria.

1. Seleziona **[!UICONTROL Aggiungi tutte le risorse modificate]**, quindi seleziona **[!UICONTROL Salva e genera in sviluppo]**.

1. Nella sezione **[!UICONTROL Sviluppo]**, seleziona ![Altre opzioni](assets/more-options-icon.svg), quindi seleziona **[!UICONTROL Approva e Publish alla produzione]**.

1. Conferma che le modifiche e il flusso di pubblicazione verranno presto visualizzati nella sezione **[!UICONTROL Pubblicato]**.

![Flusso Publish](assets/publish-flow.png)

## 2. Configurare AEM Forms {#configure-aem-forms}

Prima di creare una configurazione di Adobe Launch, crea una [configurazione Adobe IMS utilizzando Adobe Launch come soluzione cloud](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html?lang=it).

### Crea configurazione di Adobe Launch {#create-adobe-launch-configuration}

Per creare una configurazione di Adobe Launch, effettua le seguenti operazioni:

1. Nell&#39;istanza di AEM Forms Author, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configurazioni di Adobe Launch]**.

1. Selezionare una cartella per creare la configurazione e selezionare **[!UICONTROL Crea]**.

1. Specifica un titolo per la configurazione nel campo **[!UICONTROL Titolo]**.

1. Seleziona la [configurazione Adobe IMS associata](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html?lang=it).

1. Selezionare il nome dell&#39;azienda utilizzata durante [la configurazione di Adobe Analytics](#Configure-adobe-analytics).

1. Selezionare il nome della proprietà creata durante [la configurazione di Adobe Analytics](#install-extensions).

1. Seleziona **[!UICONTROL Salva e chiudi]**.

1. Publish la configurazione.

### Abilita [!DNL Adobe Analytics] per un modulo adattivo {#enable-analytics-adaptive-form}

Per utilizzare la configurazione [!DNL Adobe Launch] in un modulo adattivo esistente:

1. Nell&#39;istanza Autore AEM Forms, passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo e seleziona **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Base]**, seleziona il [contenitore di configurazione](#create-adobe-launch-configuration) utilizzato durante la creazione della configurazione di Adobe Launch.
1. Seleziona **[!UICONTROL Salva e chiudi]**. Modulo adattivo abilitato per [!DNL Adobe Analytics].
1. Publish il modulo.

Dopo aver abilitato [!DNL Adobe Analytics] per un modulo adattivo, puoi [convalidare](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=it#validate-the-page-view-beacon) se esiste un flusso di eventi dati appropriato tra AEM Forms e [!DNL Adobe Analytics]. L’integrazione di AEM Forms con Adobe Analytics è completa. Ora puoi [configurare e visualizzare i rapporti in Adobe Analytics](#view-reports-adobe-analytics).

### Creare regole per acquisire eventi personalizzati (facoltativo) {#capture-custom-events}

Crea regole su campi specifici di un modulo adattivo utilizzando un editor di regole per inviare dati di Analytics da un modulo adattivo a [!DNL Adobe Analytics].

In un processo in due fasi, puoi definire una regola su un campo in un modulo adattivo. La regola invia un evento. Il nome dell’evento è mappato a un evento di acquisizione personalizzato in Adobe Launch.

Per creare regole utilizzando un editor di regole in un modulo adattivo:

1. Seleziona il campo e fai clic su ![Editor regole](assets/rule-editor-icon.svg) per aprire la pagina dell&#39;editor regole.
1. Definisci una condizione nella sezione [!UICONTROL When] della regola.
1. Nella sezione [!UICONTROL Then] della regola, seleziona **[!UICONTROL Dispatch Event]** dall&#39;elenco a discesa **[!UICONTROL Select Action]**.
1. Specificare il nome dell&#39;evento nel campo **[!UICONTROL Tipo Nome evento]**.

Ad esempio, se la data di nascita è precedente a una determinata data, AEM Forms invia l&#39;evento **Sicurezza**.

![Evento di invio](assets/security-event.png)

Per mappare l&#39;evento a un evento di acquisizione personalizzato in [!DNL Adobe Analytics]:

1. [Crea una regola](#configure-rules).

1. Nella sezione **[!UICONTROL Eventi]**, seleziona **[!UICONTROL Aggiungi]**.

1. Specifica **[!UICONTROL Adobe Experience Manager Forms]** come nome dell&#39;estensione.

1. Selezionare **[!UICONTROL Acquisisci evento personalizzato]** dall&#39;elenco a discesa **[!UICONTROL Tipo evento]**.

1. Specifica il nome dell&#39;evento specificato nel passaggio 4 durante la creazione di una regola utilizzando l&#39;editor di regole.

1. Selezionare **Mantieni modifiche** ed eseguire le altre azioni specificate in [Configura regole](#configure-rules).

## 3. Configurare e visualizzare i report in [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Dopo aver configurato un modulo adattivo per l&#39;invio di dati evento a [!DNL Adobe Analytics], puoi iniziare a visualizzare i rapporti in [!DNL Adobe Analytics]:

1. Selezionare ![Seleziona prodotto](assets/select-analytics.png) e **[!UICONTROL Analytics]**.

1. Seleziona **[!UICONTROL Crea progetto]** e seleziona **[!UICONTROL Progetto vuoto]**.

1. Seleziona il nome della suite di rapporti dall’elenco a discesa in alto a destra nella figura a forma libera.

1. Specifica **Titolo modulo** nel testo **[!UICONTROL Cerca elementi dimensione]** per visualizzare tutti i titoli del modulo.

1. Rilascia il titolo del modulo adattivo nella casella di testo **[!UICONTROL Rilascia qui un segmento (o qualsiasi altro componente)]**.

1. Dalla sezione **[!UICONTROL Metriche]**, rilascia gli eventi da monitorare fino a **[!UICONTROL Rilascia qui una metrica (o qualsiasi altro componente)]**.

1. Seleziona ![Visualizzazioni](assets/visualization-icon.svg) e rilascia un tipo di grafico nella sezione a forma libera. Analogamente, è possibile aggiungere più tipi di grafico alla sezione a forma libera.

1. Selezionate Ctrl + S e specificate un nome per salvare il progetto.

<!--

## Add AEM Forms and Adobe Analytics integration specific rules to Dispatcher {#forms-specific-rules-to-dispatcher}

Add AEM Forms and Adobe Analytics integration specific rules to filter the data traffic that is sent to the backend.

Perform the following steps to add AEM Forms and Adobe Analytics integration specific rules to Dispatcher for Experience Manager Forms as a Cloud Service:

1. Open your AEM Project and navigate to `\src\conf.dispatcher.d\filters`.
1. Open `filters.any` file for editing and add the following rule at the end of the file:

     ```json
     /00XX { /type "allow" /path "/content/forms/af/*" /method "POST" /selectors '(analyticsconfigparser)' /extension '(jsp|json)' }
     ```

1. Save and close the file.
1. Compile and deploy the project to your [!DNL AEM Forms] as a Cloud Service environment.



## Limitations {#limitations}

* Adobe Analytics can track form metrics only for authenticated users.

-->

>[!MORELIKETHIS]
>
>*[Abilitare Adobe Analytics in un modulo adattivo](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)