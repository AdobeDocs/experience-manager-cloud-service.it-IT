---
title: Come possiamo utilizzare Adobe Sign in un modulo adattivo?
description: Utilizza Adobe Sign in un modulo adattivo per consentire ai destinatari del modulo di firmare elettronicamente un modulo dal dispositivo e dal luogo di loro scelta.
topic-tags: develop
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: cde9523e-5409-4edd-af0f-2c2575cc22ea
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '3243'
ht-degree: 1%

---

# Usa [!DNL Adobe Sign] in un modulo adattivo {#using-adobe-sign-in-an-adaptive-form}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/working-with-adobe-sign.html) |
| AEM as a Cloud Service | Questo articolo |


[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per Adaptive Forms. Le firme elettroniche migliorano i flussi di lavoro per l&#39;elaborazione di documenti per questioni legali, vendite, retribuzioni, gestione delle risorse umane e altre aree.

In uno scenario tipico di [!DNL Adobe Sign] e Forms adattivo, un utente compila un modulo adattivo da applicare a un servizio che richiede le firme di una o più parti. Ad esempio, una richiesta di mutuo e carta di credito richiede la firma legale da parte di tutti i mutuatari e i corichiedenti. Per abilitare i flussi di lavoro di firma elettronica per scenari simili, è possibile integrare [!DNL Adobe Sign] con un modulo adattivo. Altri esempi: puoi utilizzare [!DNL Adobe Sign] per:

* Chiudere le offerte da qualsiasi dispositivo con procedure di proposta, preventivo e contratto completamente automatizzate.
* Completa i processi relativi alle risorse umane più rapidamente e offri ai tuoi dipendenti le esperienze digitali.
* Ridurre i tempi di ciclo del contratto e integrare i fornitori più rapidamente.
* Crea flussi di lavoro digitali che automatizzano i processi più comuni.

L&#39;integrazione di [!DNL Adobe Sign] con [!DNL AEM Forms] supporta:

* Flussi di lavoro di firma per utente singolo e multiplo
* Flussi di lavoro di firma sequenziali e simultanei
* Firma dei moduli come utente anonimo o connesso
* Processi di firma dinamici (integrazione con il flusso di lavoro [!DNL AEM Forms])
* Autenticazione tramite knowledge base, telefono, profili social e documento ufficiale
* Assegna ruoli a ogni destinatario del contratto. Adobe Sign per i livelli di servizio business ed enterprise può espandere i [ruoli per i destinatari del contratto](#addsignerstoanadaptiveform).

<!-- * In-form and out-of-form signing experiences -->

## Prerequisiti {#prerequisites}

Prima di utilizzare [!DNL Adobe Sign] in un modulo adattivo:

* Assicurati che [!DNL AEM Forms] as a Cloud Service sia configurato per l&#39;utilizzo di Adobe Sign. Per ulteriori dettagli, consulta [Integrare Adobe Sign con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
* Tieni pronto l’elenco dei destinatari. È necessario almeno un indirizzo e-mail per ogni destinatario.

## Configura [!DNL Adobe Sign] per un modulo adattivo {#configure-adobe-sign-for-an-adaptive-form}

Per configurare [!DNL Adobe Sign] per un modulo adattivo:

1. [Abilita  [!DNL Adobe Sign]  per un modulo adattivo](#enableadobsignforanadaptiveform)
1. [Aggiungi [!DNL Adobe Sign] campi a un modulo adattivo](#addadobesignfieldstoanadaptiveform)
1. [Seleziona [!DNL Adobe Sign] Cloud Service per un modulo adattivo](#select-adobe-sign-cloud-service-and-signing-order)

1. [Aggiungi  [!DNL Adobe Sign] destinatario a un modulo adattivo](#addsignerstoanadaptiveform)
1. [Seleziona Azione di invio per un modulo adattivo](#selectsubmitactionforanadaptiveform)

![Dettagli destinatario](assets/signer_details_new.png)

### Abilita [!DNL Adobe Sign] per un modulo adattivo  {#enableadobesign}

È possibile abilitare [!DNL Adobe Sign] per un modulo adattivo esistente o crearne uno abilitato per [!DNL Adobe Sign]. Scegliere una delle opzioni seguenti:

* [Crea un modulo adattivo abilitato per  [!DNL Adobe Sign] ](#create-an-adaptive-form-for-adobe-sign)
* [Attiva [!DNL Adobe Sign] per un modulo adattivo esistente](#editafsign).

#### Creare un modulo adattivo per Adobe Sign {#create-an-adaptive-form-for-adobe-sign}

Per creare un modulo adattivo abilitato alla firma:

1. Passa ad **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Seleziona **[!UICONTROL Crea]** e **[!UICONTROL Modulo adattivo]**. Viene visualizzato un elenco di modelli. Seleziona un modello e seleziona **[!UICONTROL Avanti]**.
1. Nella scheda **[!UICONTROL Base]**:

   1. Specifica il **[!UICONTROL Nome]** e il **[!UICONTROL Titolo]** per il modulo adattivo.

   1. Seleziona il [contenitore di configurazione](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante l&#39;[integrazione [!DNL Adobe Sign] con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

   Il contenitore di configurazione contiene i servizi cloud [!DNL Adobe Sign] configurati per l&#39;ambiente. Questi servizi sono disponibili per la selezione nel generatore di moduli adattivi.

1. Nella scheda **[!UICONTROL Modello modulo]** selezionare una delle opzioni seguenti:

   * Se si dispone di un modello di modulo personalizzato e si richiede un documento di record basato sul modello di modulo, selezionare l&#39;opzione **[!UICONTROL Associa modello di modulo come modello di documento record]** e selezionare un modello di documento record. Quando si utilizza l&#39;opzione, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   * Se non si dispone di un modello di modulo personalizzato, selezionare l&#39;opzione **[!UICONTROL Genera documento di record]**. Quando utilizzi l’opzione, nel documento inviato per la firma vengono visualizzati tutti i campi del modulo adattivo.

1. Seleziona **[!UICONTROL Crea]**. Viene creato un modulo adattivo abilitato alla firma. Puoi aggiungere i campi [!DNL Adobe Sign] al modulo e inviarlo per la firma.

#### Abilita [!DNL Adobe Sign] per un modulo adattivo {#editafsign}

Per utilizzare [!DNL Adobe Sign] in un modulo adattivo esistente:

1. Passa ad **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Seleziona il modulo adattivo e seleziona **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Base]**, seleziona il [contenitore di configurazione](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante l&#39;integrazione di [!DNL Adobe Sign] con [!DNL AEM Forms].
1. Nella scheda **[!UICONTROL Modalità modulo]** selezionare una delle opzioni seguenti:

   * Se si dispone di un modello di modulo personalizzato e si richiede un documento di record basato sul modello di modulo, selezionare l&#39;opzione **[!UICONTROL Associa modello di modulo come modello di documento record]** e selezionare un modello di documento record. Quando si utilizza l&#39;opzione, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   * Se non si dispone di un modello di modulo personalizzato, selezionare l&#39;opzione **[!UICONTROL Genera documento di record]**. Quando utilizzi l’opzione, nel documento inviato per la firma vengono visualizzati tutti i campi del modulo adattivo.

1. Seleziona **[!UICONTROL Salva e chiudi]**. Modulo adattivo abilitato per [!DNL Adobe Sign]. Ora puoi aggiungere i campi [!DNL Adobe Sign] al modulo e inviarlo per la firma.

### Aggiungi [!DNL Adobe Sign] campi a un modulo adattivo {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] contiene vari campi che possono essere inseriti in un modulo adattivo. Questi campi accettano diversi tipi di dati, ad esempio firme, iniziali, società o titoli, e consentono di raccogliere ulteriori informazioni durante la firma, insieme alle firme. È possibile utilizzare il componente di blocco [!DNL Adobe Sign] per inserire [!DNL Adobe Sign] campi in varie posizioni in un modulo adattivo.

Per aggiungere campi a un modulo adattivo e personalizzare varie opzioni relative a tali campi:

1. Trascina il componente **[!UICONTROL Adobe Sign Block]** dal browser dei componenti al modulo adattivo. Il componente di blocco [!DNL Adobe Sign] contiene tutti i campi [!DNL Adobe Sign] supportati. Per impostazione predefinita, aggiunge un campo **[!UICONTROL Firma]** al modulo adattivo.

   ![Blocco firma](assets/sign_block_new.png)

   Per impostazione predefinita, il blocco [!DNL Adobe Sign] non è visibile nel modulo adattivo pubblicato. È visibile solo nei documenti di firma. È possibile modificare la visibilità del blocco [!DNL Adobe Sign] dalle proprietà del componente di blocco [!DNL Adobe Sign].

   >[!NOTE]
   >
   > * L&#39;utilizzo del blocco [!DNL Adobe Sign] non è obbligatorio per utilizzare [!DNL Adobe Sign] in un modulo adattivo. Se non si utilizza il blocco [!DNL Adobe Sign] e non si aggiungono campi per i destinatari, nella parte inferiore dei documenti di firma verrà visualizzato il campo firma predefinito.
   > * Usa il blocco [!DNL Adobe Sign] solo per Forms adattivi che generano automaticamente documenti di record. Se utilizzi un XDP personalizzato per generare un documento di record o un modulo adattivo basato su modello di modulo, il blocco [!DNL Adobe Sign] non è supportato.


1. Seleziona il componente **[!UICONTROL Adobe Sign Block]** e l&#39;icona **[!UICONTROL Edit]** ![Edit](assets/Smock_Edit_18_N.svg). Vengono visualizzate le opzioni per aggiungere campi e formattare l&#39;aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleziona e aggiungi [!DNL Adobe Sign] campi. **B.** Espandere il blocco [!DNL Adobe Sign] in visualizzazione a schermo intero

1. Seleziona l&#39;icona **[!UICONTROL Adobe Sign]** Campo ![Adobe Sign](assets/adobesign.png). Vengono visualizzate le opzioni per selezionare e aggiungere i campi [!DNL Adobe Sign].

   Espandere il campo a discesa **[!UICONTROL Tipo]** per selezionare un campo [!DNL Adobe Sign] e selezionare l&#39;icona Fine ![Salva](assets/save_icon.svg) per aggiungere il campo selezionato al blocco [!DNL Adobe Sign]. Il campo a discesa **[!UICONTROL Tipo]** include i tipi di campo Firma, Informazioni destinatario e Dati. Integrazione di [!DNL Adobe Sign] con i campi di supporto di AEM [!DNL Forms] elencati solo nella casella a discesa [!UICONTROL Tipo]. Per informazioni dettagliate sui campi [!DNL Adobe Sign], consulta [Documentazione di Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   È obbligatorio fornire un nome univoco per un campo. Puoi anche selezionare l’opzione richiesta per contrassegnare un campo come obbligatorio. Oltre all&#39;opzione **[!UICONTROL Name]** e **[!UICONTROL Required]**, alcuni campi [!DNL Adobe Sign] contengono altre opzioni. Ad esempio, maschera e su più righe. Inoltre, specificare un nome univoco per ogni campo [!DNL Adobe Sign], indipendentemente dal fatto che i campi si trovino nello stesso blocco [!DNL Adobe Sign] o in blocchi diversi.

   Se si seleziona **[!UICONTROL Firma digitale]** dall&#39;elenco a discesa, è possibile applicare le firme digitali al modulo adattivo:

   * Online utilizzando le firme cloud per la firma con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi di attendibilità.
   * In locale, scaricando il documento con Adobe Acrobat o Reader utilizzando una smart card, un token USB o un ID digitale basato su file.

### Abilita [!DNL Adobe Sign] per un modulo adattivo {#enableadobsignforanadaptiveform}

Per impostazione predefinita, [!DNL Adobe Sign] non è abilitato per un modulo adattivo. Per abilitare questa funzione:

1. Nel browser Contenuto, selezionare **[!UICONTROL Contenitore modulo]** e l&#39;icona **[!UICONTROL Configura]** ![configura](assets/Smock_Wrench_18_N.svg). Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi il pannello a soffietto **[!UICONTROL Firma elettronica]** e seleziona l&#39;opzione **[!UICONTROL Abilita Adobe Sign]**. Abilita [!DNL Adobe Sign] per un modulo adattivo.

### Seleziona il Cloud Service [!DNL Adobe Sign] e l&#39;ordine di firma {#select-adobe-sign-cloud-service-and-signing-order}

È possibile configurare più servizi [!DNL Adobe Sign] per un&#39;istanza di AEM [!DNL Forms]. È consigliabile disporre di un insieme separato di servizi per ciascuna funzione (risorse umane, finanze e altro ancora). Semplifica il tracciamento e il reporting dei documenti firmati. Ad esempio, una banca dispone di più reparti. È possibile disporre di una configurazione separata per ciascun reparto per un migliore tracciamento dei documenti.

Un documento può avere anche più destinatari. Ad esempio, un&#39;applicazione con carta di credito può avere più richiedenti. Una banca richiede le firme di tutti i richiedenti prima di iniziare l&#39;elaborazione della domanda. Per scenari con più destinatari, è possibile scegliere di firmare il documento in ordine sequenziale o simultaneo.

Per selezionare un Cloud Service e l’ordine di firma:

![Servizio cloud](/help/forms/assets/adobe-sign-cloud-service.png)

1. Nel browser Contenuto, selezionare **[!UICONTROL Contenitore modulo]** e l&#39;icona **[!UICONTROL Configura]** ![configura](assets/Smock_Wrench_18_N.svg). Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi il pannello a soffietto **[!UICONTROL Firma elettronica]** e seleziona l&#39;opzione **[!UICONTROL Abilita Adobe Sign]**. Abilita [!DNL Adobe Sign] per un modulo adattivo.
1. Selezionare un Cloud Service dall&#39;elenco già configurato di [!DNL Adobe Sign] Cloud Services.

   Se l&#39;elenco **[!UICONTROL Adobe Sign Cloud Service]** è vuoto, seguire l&#39;articolo [Configure [!DNL Adobe Sign] with [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) per configurare il servizio.

   Nell&#39;elenco a discesa sono elencati i servizi cloud esistenti nella cartella `global` in Strumenti > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Adobe Sign]**. Nell&#39;elenco a discesa sono inoltre elencati i servizi cloud presenti nella cartella selezionata nel campo **[!UICONTROL Contenitore configurazione]** al momento della creazione di un modulo adattivo.

1. Selezionare l&#39;opzione per configurare l&#39;azione di invio utilizzando **[!UICONTROL Invia il modulo]**. È possibile selezionare una delle due opzioni seguenti:
   * **Invia il modulo (e invia il contratto per la firma)**: questa opzione invia il modulo immediatamente e quindi invia il modulo per la firma ai destinatari.
   * **Invia il modulo (dopo che ogni destinatario ha completato la firma)**: questa opzione invia Forms adattivo solo dopo che tutti i firmatari hanno completato il processo di firma. È possibile configurare l&#39;intervallo per controllare lo stato di firma per tutti i firmatari. Per ulteriori dettagli, vedere [Configure [!DNL Adobe Acrobat Sign] scheduler](/help/forms/adobe-sign-integration-adaptive-forms.md#configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status).

1. Selezionare l&#39;ordine di firma dalla finestra di dialogo **[!UICONTROL I destinatari possono completare]**. I destinatari possono firmare un modulo adattivo **[!UICONTROL in modo sequenziale]** - uno dopo l&#39;altro o **[!UICONTROL in modo simultaneo]** - in qualsiasi ordine.

   In ordine sequenziale, un destinatario riceve il contratto Adobe Sign alla volta. Dopo che il destinatario ha completato l&#39;azione assegnata, l&#39;accordo viene inviato al destinatario successivo e così via.

   In ordine simultaneo, tutti i destinatari ricevono l’accordo Adobe Sign e possono agire in parallelo tra loro.

1. Utilizzare il campo ID accordo per associare un bindref all&#39;ID accordo (agreementId). Aggiunge l’ID contratto alla sezione afBoundData dei dati di invio per i moduli basati su schema. L’ID contratto viene aggiunto anche alla sezione afSubmissionInfo nei dati inviati per tutti i moduli abilitati per Adobe Sign. È possibile utilizzare l&#39;ID accordo per tenere traccia dello stato dell&#39;accordo utilizzando un codice personalizzato (è necessaria l&#39;implementazione personalizzata).

   >[!NOTE]
   >
   > Se viene creato un modulo adattivo utilizzando un modello dati modulo (FDM), il campo ID accordo diventa visibile nella finestra di dialogo.

1. [Aggiungi i destinatari a un modulo adattivo](working-with-adobe-sign.md#addsignerstoanadaptiveform) e seleziona l&#39;icona Fine ![Salva](assets/save_icon.svg) per salvare le modifiche.

### Aggiungere destinatari a un modulo adattivo {#addsignerstoanadaptiveform}

Puoi avere uno o più destinatari per un contratto Adobe Sign. Quando aggiungi un destinatario, puoi anche configurare i dettagli di autenticazione per il destinatario e selezionare se il compilatore del modulo e il destinatario sono la stessa persona. Per aggiungere e fornire vari dettagli su un destinatario, effettua le seguenti operazioni:

1. Nel browser Contenuto, selezionare **[!UICONTROL Contenitore modulo]** e l&#39;icona **[!UICONTROL Configura]** ![configura](assets/Smock_Wrench_18_N.svg). Apre il browser delle proprietà con le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi il pannello a soffietto **[!UICONTROL Firma elettronica]** e seleziona l&#39;opzione **[!UICONTROL Abilita Adobe Sign]**. Abilita [!DNL Adobe Sign] per un modulo adattivo.
1. Seleziona **[!UICONTROL Aggiungi destinatario]**. Aggiunge un destinatario al modulo adattivo. È possibile aggiungere più destinatari a un modulo adattivo. Tutti i destinatari ricevono un accordo Adobe Sign all’invio del modulo adattivo.
   ![dettagli telefono](assets/recipient-settings.png)

1. Fai clic sull&#39;icona **[!UICONTROL Modifica]** ![Modifica](assets/Smock_Edit_18_N.svg) per specificare le seguenti informazioni sul destinatario:

   * **[!UICONTROL Titolo]:** Specificare un titolo per identificare in modo univoco un destinatario.

   * **[!UICONTROL Il destinatario e la persona che compila il modulo corrispondono?]:** Seleziona **[!UICONTROL Sì]**, se il compilatore del modulo e il primo destinatario sono la stessa persona. <!-- If the option is set to **No,** then do not use the signature step component in the Adaptive Form. If the form contains a Signature Step component, then the field is automatically set to Yes. -->

   * **[!UICONTROL Ruolo destinatario]:** Seleziona il ruolo di un destinatario. Adobe Sign per i livelli di servizio business ed enterprise ha la possibilità di espandere i [ruoli per i destinatari del contratto](https://helpx.adobe.com/sign/using/set-up-signer-approver-roles.html), oltre a **Firmatario**, per soddisfare meglio i requisiti del flusso di lavoro.

   * **[!UICONTROL Indirizzo e-mail destinatario]:** Specifica l&#39;indirizzo e-mail del destinatario. Il destinatario riceve il contratto Adobe Sign sull’indirizzo e-mail specificato. Puoi scegliere di utilizzare un indirizzo e-mail fornito in un campo del modulo, nel profilo utente di Experience Manager dell’utente connesso o immettere manualmente un indirizzo e-mail. È un passaggio obbligatorio.

     >[!NOTE]
     >
     >Verificare che l&#39;indirizzo di posta elettronica del primo destinatario o dell&#39;unico destinatario (se esiste un solo destinatario) non sia identico all&#39;account [!DNL Adobe Sign] utilizzato per configurare AEM Cloud Services.

   * **[!UICONTROL Metodo di autenticazione destinatario]:** Specificare il metodo per autenticare un destinatario prima di aprire l&#39;accordo Adobe Sign. Puoi scegliere tra telefono, knowledge base, autenticazione basata su identità social e [ID governo](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html) per [!DNL Adobe Acrobat Sign]. Per [!DNL Adobe Acrobat Sign for Government] è possibile scegliere tra l&#39;autenticazione tramite telefono e l&#39;autenticazione basata su Knowledge Base.

   >[!NOTE]
   >
   > * Per impostazione predefinita, l’autenticazione basata su identità social fornisce un’opzione per eseguire l’autenticazione tramite Facebook, Google e LinkedIn. È possibile contattare il supporto di [!DNL Adobe Sign] per abilitare altri provider di autenticazione social network.
   >

   * **[!DNL Adobe Sign]campi da compilare o firmare:** Seleziona [!DNL Adobe Sign] campi per il destinatario. Un modulo adattivo può avere più campi [!DNL Adobe Sign]. Puoi scegliere di abilitare campi specifici per un destinatario. Nel campo vengono visualizzati tutti i [!DNL Adobe Sign] blocchi disponibili. Quando selezioni un blocco, vengono selezionati tutti i campi del blocco. Puoi utilizzare l’icona X per deselezionare un campo.

   ![dettagli-destinatario](assets/signer-details.png)

   L&#39;immagine precedente contiene due blocchi di esempio [!DNL Adobe Sign]: Personal-Information e Office-details

   Seleziona l&#39;icona ![Salva](assets/save_icon.svg). Il destinatario viene aggiunto.

### Seleziona Azione di invio per un modulo adattivo {#selectsubmitactionforanadaptiveform}

Dopo aver aggiunto [!DNL Adobe Sign] campi a un modulo adattivo, abilitato [!DNL Adobe Sign] dal contenitore del modulo, selezionato [!DNL Adobe Sign] Cloud Service e aggiunto i destinatari del contratto Adobe Sign, selezionare un&#39;azione di invio appropriata per il modulo adattivo. Per informazioni dettagliate sulle azioni di invio di Adaptive Forms, vedi [Configurazione dell&#39;azione di invio](configuring-submit-actions.md).

La firma e l’invio di un modulo sono indipendenti l’uno dall’altro. L’invio di un modulo adattivo ha luogo non appena viene creato un accordo Adobe Sign dopo che un utente ha inviato un modulo. [!DNL AEM Forms] as a Cloud Service non attende che i destinatari firmino o completino altre azioni per inviare un modulo adattivo. Un modulo viene inviato non appena un utente fa clic sul pulsante Invia o quando un passaggio di riepilogo visualizza il riepilogo del modulo.

Inoltre, un modulo adattivo abilitato per [!DNL Adobe Sign] incorpora l&#39;ID contratto di Adobe Sign per inviare i dati. È possibile utilizzare l&#39;ID accordo per tenere traccia dello stato dell&#39;accordo utilizzando un codice personalizzato (è necessaria l&#39;implementazione personalizzata).

L’ID contratto di Adobe Sign (agreementId) è incluso nei dati di invio del modulo adattivo. Per impostazione predefinita, l&#39;ID contratto è presente nel nodo `afSubmissionInfo` dei dati inviati.

```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <afData>
      <afUnboundData>
         <data>
            <textbox1613455050902>ff</textbox1613455050902>
         </data>
      </afUnboundData>
      <afBoundData>
         <data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" />
      </afBoundData>
      <afSubmissionInfo>
         <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].textbox1613455050902[0]</lastFocusItem>
         <stateOverrides />
         <signers>
            <signer0>
               <email />
            </signer0>
         </signers>
         <afPath>/content/dam/formsanddocuments/testsign</afPath>
         <afSubmissionTime>20210311031009</afSubmissionTime>
         <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
      </afSubmissionInfo>
   </afData>
```

Facoltativamente, è anche possibile associare un bindref all&#39;ID contratto (agreementId). Aggiunge l&#39;ID contratto alla sezione afBoundData dei dati inviati. Ad esempio, nei seguenti dati inviati, l&#39;ID contratto è associato al nodo `<userName>`:

```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <afData>
         <afUnboundData>
            <data />
         </afUnboundData>
         <afBoundData>
            <config xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
               <userName>3AAABLblqZhC2MWu7GFauKh45j_t2ih8mAtmbdIcNSl1HgQubhMJfDaDfylyN7NQiYRam_44ISKm45enIOafHqWZrdaxShf9r</userName>
               <dateOfBirth>0001-01-01</dateOfBirth>
            </config>
         </afBoundData>
         <afSubmissionInfo>
            <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].projectDetails[0]</lastFocusItem>
            <stateOverrides />
            <signers>
               <signer0>
                  <email />
               </signer0>
            </signers>
            <afPath>/content/dam/formsanddocuments/testathon2021-1/gaurav/xsd-based</afPath>
            <afSubmissionTime>20210311095211</afSubmissionTime>
            <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
         </afSubmissionInfo>
      </afData>
```

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the Adaptive Form is stored temporarily on Forms Portal. Adobe recommends using [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

L’esperienza di firma del modulo è pronta. Puoi visualizzare in anteprima il modulo per verificare l’esperienza di firma. Nel modulo pubblicato, i campi di blocco [!DNL Adobe Sign] vengono visualizzati quando un destinatario riceve il modulo per la firma tramite un messaggio e-mail. Quando **[!UICONTROL È lo stesso destinatario e la persona che compila il modulo?L&#39;opzione]** è contrassegnata come Sì e la condizione è soddisfatta, l&#39;utente viene reindirizzato al contratto Adobe Sign dopo l&#39;invio e può firmare il documento immediatamente, invece di attendere che il contratto venga visualizzato nel messaggio di posta elettronica.

## Configurare le firme cloud per un modulo adattivo {#configure-cloud-signatures-for-an-adaptive-form}

Le firme digitali basate sul cloud o firme remote sono una nuova generazione di firme digitali che funzionano su desktop, dispositivi mobili e Web e soddisfano i massimi livelli di conformità e garanzia per l&#39;autenticazione dei destinatari. È possibile firmare un modulo adattivo con firme digitali basate su cloud.

Dopo [aver modificato le proprietà del modulo adattivo per Adobe Sign](working-with-adobe-sign.md#enableadobesign), effettua le seguenti operazioni per aggiungere il campo della firma cloud a un modulo adattivo:

1. Trascina il componente **[!UICONTROL Adobe Sign Block]** dal browser dei componenti al modulo adattivo. Il componente [!UICONTROL Adobe Sign Block] include tutti i campi [!DNL Adobe Sign] supportati. Per impostazione predefinita, aggiunge un campo **[!UICONTROL Firma]** al modulo adattivo.

   ![Blocco firma](assets/sign-block-new.png)

1. Seleziona il componente **[!UICONTROL Adobe Sign Block]** e l&#39;icona **[!UICONTROL Edit]** ![Edit](assets/Smock_Edit_18_N.svg). Vengono visualizzate le opzioni per aggiungere campi e formattare l&#39;aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleziona e aggiungi [!DNL Adobe Sign] campi. **B.** Espandere il blocco [!DNL Adobe Sign] in visualizzazione a schermo intero

1. Seleziona l&#39;icona **[!UICONTROL Campo Adobe Sign]** ![Adobe Sign](assets/adobesign.png). Vengono visualizzate le opzioni per selezionare e aggiungere i campi [!DNL Adobe Sign].

   Espandere il campo a discesa **[!UICONTROL Tipo]** per selezionare **[!UICONTROL Firma digitale]** e selezionare l&#39;icona **[!UICONTROL Fine]** per aggiungere il campo selezionato al blocco [!DNL Adobe Sign].

   ![Firme digitali](assets/digital_signatures_new.png)

   È obbligatorio fornire un nome univoco per un campo.

   Applica firme digitali al modulo adattivo utilizzando:

   * Firme cloud: accedi con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider del servizio di trust.
   * Adobe Acrobat o Reader: scarica e apri il documento con Adobe Acrobat o Reader per firmare utilizzando una smart card, un token USB o un ID digitale basato su file.

     >[!NOTE]
     >
     > La firma digitale è applicabile anche a [!DNL Adobe Acrobat Sign for Government], ma non è possibile applicarla utilizzando le firme cloud.

   Dopo aver aggiunto il campo della firma cloud al modulo adattivo, esegui i seguenti passaggi per completare il processo di configurazione:

   * [Abilitare Adobe Sign per un modulo adattivo](#enableadobsignforanadaptiveform)
   * [Seleziona Adobe Sign Cloud Service per un modulo adattivo](#selectadobesigncloudserviceforanadaptiveform)
   * [Aggiungere destinatari a un modulo adattivo](#addsignerstoanadaptiveform)
   * [Seleziona Azione di invio per un modulo adattivo](#selectsubmitactionforanadaptiveform)

### Configurare il componente per la pagina di ringraziamento o il passaggio di riepilogo {#configure-the-thank-you-page-or-summary-step-component}

Il componente **[!UICONTROL Passaggio di riepilogo]** invia automaticamente il modulo, compila le informazioni all&#39;interno della pagina di riepilogo personalizzata e visualizza il riepilogo del modulo inviato. Il componente Passaggio di riepilogo occupa l’intera larghezza disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio di riepilogo.

## Domande frequenti {#frequently-asked-questions}

**Q:** È possibile incorporare un modulo adattivo in un altro modulo adattivo. Il modulo adattivo incorporato può essere abilitato per [!DNL Adobe Sign]?
**Ans:** No, Experience Manager Forms non supporta l&#39;utilizzo di un modulo adattivo che incorpora un modulo adattivo abilitato per la firma di [!DNL Adobe Sign]

**Q:** Quando creo un modulo adattivo utilizzando il modello avanzato e lo apro per la modifica, viene visualizzato un messaggio di errore di tipo &quot;Firma elettronica o destinatari non configurati correttamente&quot;. viene visualizzato. Come si risolve il messaggio di errore?
**Ans:** il modulo adattivo creato utilizzando il modello avanzato è configurato per l&#39;utilizzo di [!DNL Adobe Sign]. Per risolvere l&#39;errore, creare e selezionare una configurazione cloud [!DNL Adobe Sign] e configurare un destinatario [!DNL Adobe Sign] per il modulo adattivo.

**Q:** posso utilizzare [!DNL Adobe Sign] tag di testo in un componente di testo statico di un modulo adattivo?
**Ans:** Sì, è possibile utilizzare i tag di testo in un componente di testo per aggiungere [!DNL Adobe Sign] campi a un modulo adattivo abilitato per il documento di record (solo per opzione Documento di record generato automaticamente). Per informazioni sulla procedura e sulle regole per creare un tag di testo, consulta [Documentazione di Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Inoltre, Adaptive Forms dispone di un supporto limitato per i tag di testo. È possibile utilizzare i tag di testo per creare solo i campi supportati da [Adobe Sign Block](working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form).

## Risoluzione dei problemi {#troubleshoot}

### [!DNL Adobe Sign] errori contratto {#adobe-sign-agreement-failures}

**Problema**
Quando il servizio [!DNL Adobe Sign] è configurato per un modulo adattivo, non riesce a creare un contratto [!DNL Adobe Sign] per il modulo adattivo sottostante.

**Risoluzione**

* Controlla la [configurazione di Adobe Sign Cloud Service](adobe-sign-integration-adaptive-forms.md) utilizzata nel modulo adattivo.
* Verificare che l&#39;applicazione API nel server [!DNL Adobe Sign] utilizzata per configurare [!DNL Adobe Sign] Cloud Service disponga delle autorizzazioni necessarie.
* Se utilizzi più servizi cloud [!DNL Adobe Sign], punta l&#39;**[!UICONTROL URL oAuth]** di tutti i servizi allo stesso **[!UICONTROL Condivisione Adobe Sign]**.

* Utilizzare indirizzi di posta elettronica distinti per configurare l&#39;account [!DNL Adobe Sign] e per il primo o il singolo destinatario. L&#39;indirizzo di posta elettronica del primo destinatario o dell&#39;unico destinatario (se è presente il singolo destinatario) non può essere identico all&#39;account [!DNL Adobe Sign] utilizzato per configurare AEM Cloud Services.

>[!MORELIKETHIS]
>
>* [Integrare [!DNL Adobe Sign] con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)
>* [Best practice per l&#39;utilizzo di [!DNL Adobe Sign] con Forms adattivo](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)


## Consulta anche {#see-also}

{{see-also}}
