---
title: Come utilizzare [!DNL Adobe Sign] in un modulo adattivo?
description: È possibile abilitare la firma elettronica ([!DNL Adobe Sign]) flussi di lavoro per un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi a firma singola e multipla e per firmare elettronicamente i moduli dai dispositivi mobili.
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: cde9523e-5409-4edd-af0f-2c2575cc22ea
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '3072'
ht-degree: 0%

---


# Utilizzo [!DNL Adobe Sign] in un modulo adattivo {#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per Adaptive Forms. Le firme elettroniche migliorano i flussi di lavoro per elaborare i documenti per aree legali, di vendita, di retribuzione, di gestione delle risorse umane e per altre aree.

In un tipico [!DNL Adobe Sign] in uno scenario di Forms adattivo, un utente compila un modulo adattivo per richiedere un servizio che richiede la firma di una o più parti. Ad esempio, una domanda di mutuo e di carta di credito richiede firme legali da parte di tutti i mutuatari e co-richiedenti. Per abilitare i flussi di lavoro di firma elettronica per scenari simili, è possibile integrare [!DNL Adobe Sign] con un modulo adattivo. Alcuni altri esempi sono disponibili, è possibile utilizzare [!DNL Adobe Sign] a:

* Chiudi le offerte da qualsiasi dispositivo con processi di proposta, preventivo e contratto completamente automatizzati.
* Completa più velocemente i processi delle risorse umane e dai ai tuoi dipendenti le esperienze digitali.
* Taglia i tempi del ciclo di contratto e accedi più rapidamente ai tuoi fornitori.
* Crea flussi di lavoro digitali per automatizzare i processi comuni.

[!DNL Adobe Sign] integrazione con [!DNL AEM Forms] supporta:

* Flussi di lavoro di firma singoli e multipli
* Flussi di lavoro di firma sequenziali e simultanei
* Firma dei moduli come utente anonimo o connesso
* Processi di firma dinamici (integrazione con [!DNL AEM Forms] Flusso di lavoro)
* Autenticazione tramite knowledge base, telefono, profili social e ID governativo
* Assegna ruoli a ogni destinatario dell&#39;accordo. Adobe Sign per i livelli di servizio business ed enterprise ha la possibilità di espandere la [ruoli per i destinatari del contratto](#addsignerstoanadaptiveform).

<!-- * In-form and out-of-form signing experiences -->

## Prerequisiti {#prerequisites}

Prima di utilizzare [!DNL Adobe Sign] in un modulo adattivo:

* Assicurati che [!DNL AEM Forms] L’as a Cloud Service è configurato per l’utilizzo di Adobe Sign. Per maggiori dettagli, vedi [Integrare Adobe Sign con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
* Tieni pronto l’elenco dei destinatari. Richiedi almeno un indirizzo e-mail per ogni destinatario.

## Configura [!DNL Adobe Sign] per un modulo adattivo {#configure-adobe-sign-for-an-adaptive-form}

Per configurare [!DNL Adobe Sign] per un modulo adattivo:

1. [Abilita [!DNL Adobe Sign] per un modulo adattivo](#enableadobsignforanadaptiveform)
1. [Aggiungi [!DNL Adobe Sign] campi di un modulo adattivo](#addadobesignfieldstoanadaptiveform)
1. [Seleziona [!DNL Adobe Sign] Cloud Service per un modulo adattivo](#select-adobe-sign-cloud-service-and-signing-order)

1. [Aggiungi [!DNL Adobe Sign] destinatario in un modulo adattivo](#addsignerstoanadaptiveform)
1. [Selezionare un’azione di invio per un modulo adattivo](#selectsubmitactionforanadaptiveform)

![Dettagli del destinatario](assets/signer_details_new.png)

### Abilita [!DNL Adobe Sign] per un modulo adattivo  {#enableadobesign}

È possibile attivare [!DNL Adobe Sign] per un modulo adattivo esistente o per creare un [!DNL Adobe Sign] modulo adattivo abilitato. Scegliere una delle seguenti opzioni:

* [Crea un [!DNL Adobe Sign] modulo adattivo abilitato](#create-an-adaptive-form-for-adobe-sign)
* [Abilita [!DNL Adobe Sign] per un modulo adattivo esistente](#editafsign).

#### Creare un modulo adattivo per Adobe Sign {#create-an-adaptive-form-for-adobe-sign}

Per creare un modulo adattivo abilitato alla firma:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**. Viene visualizzato un elenco di modelli. Seleziona un modello e tocca **[!UICONTROL Successivo]**.
1. In **[!UICONTROL Base]** scheda:

   1. Specifica la **[!UICONTROL Nome]** e **[!UICONTROL Titolo]** per il modulo adattivo.

   1. Seleziona la [contenitore di configurazione](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato mentre [integrazione [!DNL Adobe Sign] con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   Il contenitore di configurazione contiene [!DNL Adobe Sign] Cloud Services configurati per il tuo ambiente. Questi servizi sono disponibili per la selezione nell’editor di moduli adattivi.

1. In **[!UICONTROL Modello Modulo]** seleziona una delle opzioni seguenti:

   * Se si dispone di un modello di modulo personalizzato e si richiede un documento di record basato sul modello di modulo, selezionare la **[!UICONTROL Associa modello di modulo come modello del documento di record]** e selezionare un modello Documento di record. Quando si utilizza l’opzione , i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non vengono visualizzati tutti i campi del modulo adattivo.

   * Se non si dispone di un modello di modulo personalizzato, selezionare la **[!UICONTROL Genera documento di registrazione]** opzione . Quando si utilizza l’opzione , nel documento inviato per la firma vengono visualizzati tutti i campi del modulo adattivo.

1. Tocca **[!UICONTROL Crea.]** Viene creato un modulo adattivo abilitato per la firma. Puoi aggiungere il tuo [!DNL Adobe Sign] campi al modulo e inviarlo per la firma.

#### Abilita [!DNL Adobe Sign] per un modulo adattivo {#editafsign}

Per utilizzare [!DNL Adobe Sign] in un modulo adattivo esistente:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo e tocca **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Base]** seleziona la scheda [contenitore di configurazione](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante l&#39;integrazione [!DNL Adobe Sign] con [!DNL AEM Forms].
1. In **[!UICONTROL Modalità modulo]** seleziona una delle opzioni seguenti:

   * Se si dispone di un modello di modulo personalizzato e si richiede un documento di record basato sul modello di modulo, selezionare la **[!UICONTROL Associa modello di modulo come modello del documento di record]** e selezionare un modello Documento di record. Quando si utilizza l’opzione , i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non vengono visualizzati tutti i campi del modulo adattivo.

   * Se non si dispone di un modello di modulo personalizzato, selezionare la **[!UICONTROL Genera documento di registrazione]** opzione . Quando si utilizza l’opzione , nel documento inviato per la firma vengono visualizzati tutti i campi del modulo adattivo.

1. Tocca **[!UICONTROL Salva e chiudi]**. Il modulo adattivo è abilitato per [!DNL Adobe Sign]. Ora puoi aggiungere il tuo [!DNL Adobe Sign] campi al modulo e inviarlo per la firma.

### Aggiungi [!DNL Adobe Sign] campi di un modulo adattivo {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] dispone di vari campi che possono essere inseriti in un modulo adattivo. Questi campi accettano vari tipi di dati, ad esempio firme, iniziali, aziendali o titoli, e consentono di raccogliere ulteriori informazioni durante la firma, insieme alle firme. È possibile utilizzare [!DNL Adobe Sign] Blocco del componente da posizionare [!DNL Adobe Sign] campi in varie posizioni in un modulo adattivo.

Per aggiungere campi a un modulo adattivo e personalizzare varie opzioni relative a questi campi:

1. Trascinamento della selezione **[!UICONTROL Blocco Adobe Sign]** dal browser Componenti al modulo adattivo. La [!DNL Adobe Sign] Il componente Blocco dispone di tutti i [!DNL Adobe Sign] campi. Per impostazione predefinita, aggiunge un **[!UICONTROL Firma]** al modulo adattivo.

   ![Blocco dei segni](assets/sign_block_new.png)

   Per impostazione predefinita, la [!DNL Adobe Sign] Il blocco non è visibile nel modulo adattivo pubblicato. È visibile solo nei documenti firmati. È possibile modificare la visibilità di [!DNL Adobe Sign] Blocca le proprietà del [!DNL Adobe Sign] Componente blocco.

   >[!NOTE]
   >
   >  * Utilizzo [!DNL Adobe Sign] blocco non obbligatorio da utilizzare [!DNL Adobe Sign] in un modulo adattivo. Se non utilizzi [!DNL Adobe Sign] bloccare e aggiungere campi per i destinatari, quindi il campo firma predefinito viene visualizzato nella parte inferiore dei documenti di firma.
   >  * Utilizzo [!DNL Adobe Sign] bloccare solo per i Forms adattivi che generano automaticamente il documento di record. Se si utilizza un modulo XDP personalizzato per la generazione di un documento di record o di un modulo adattivo basato su un modello di modulo, [!DNL Adobe Sign] blocco non supportato.



1. Seleziona la **[!UICONTROL Blocco Adobe Sign]** e tocca **[!UICONTROL Modifica]** ![Modifica](assets/Smock_Edit_18_N.svg) icona. Visualizza le opzioni per aggiungere campi e formattare l’aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleziona e aggiungi [!DNL Adobe Sign] campi. **B.** Espandi la [!DNL Adobe Sign] blocca a schermo intero

1. Tocca **[!UICONTROL Adobe Sign]** Campo ![Adobe Sign](assets/adobesign.png) icona. Visualizza le opzioni di selezione e aggiunta [!DNL Adobe Sign] campi.

   Espandi la **[!UICONTROL Tipo]** campo a discesa per selezionare un [!DNL Adobe Sign] e tocca Fine ![Salva](assets/save_icon.svg) icona per aggiungere il campo selezionato a [!DNL Adobe Sign] blocco. La **[!UICONTROL Tipo]** Il campo a discesa include i tipi di campo Firma, Informazioni destinatario e Dati. [!DNL Adobe Sign] integrazione con AEM [!DNL Forms] campi di supporto elencati in [!UICONTROL Tipo] solo casella a discesa. Per informazioni dettagliate su [!DNL Adobe Sign] campi, vedi [Documentazione di Adobe Sign](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   È obbligatorio fornire un nome univoco per un campo. È inoltre possibile selezionare l’opzione richiesta per contrassegnare un campo obbligatorio. Oltre al **[!UICONTROL Nome]** e **[!UICONTROL Obbligatorio]** opzione, alcuni [!DNL Adobe Sign] Il campo dispone di più opzioni. Ad esempio, maschera e linea multipla. Inoltre, specifica un nome univoco per ogni [!DNL Adobe Sign] se i campi si trovano nello stesso o in un altro [!DNL Adobe Sign] blocchi.

   Se si seleziona **[!UICONTROL Firma digitale]** dall’elenco a discesa è possibile applicare le firme digitali al modulo adattivo:

   * Online tramite firme cloud per firmare con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi attendibili.
   * Localmente scaricando il documento con Adobe Acrobat o Reader utilizzando una smart card, un token USB o un ID digitale basato su file.

### Abilita [!DNL Adobe Sign] per un modulo adattivo {#enableadobsignforanadaptiveform}

Fuori dalla scatola, [!DNL Adobe Sign] non è abilitato per un modulo adattivo. Per abilitare questa funzione:

1. Nel browser Contenuto, tocca **[!UICONTROL Contenitore modulo]** e tocca **[!UICONTROL Configura]** ![configurare](assets/Smock_Wrench_18_N.svg) icona. Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi la **[!UICONTROL Firma elettronica]** a soffietto e seleziona la **[!UICONTROL Abilita Adobe Sign]** opzione . Attiva [!DNL Adobe Sign] per un modulo adattivo.

### Seleziona [!DNL Adobe Sign] Cloud Service e ordine di firma {#select-adobe-sign-cloud-service-and-signing-order}

È possibile configurare più [!DNL Adobe Sign] servizi per un esempio di AEM [!DNL Forms]. È consigliabile disporre di un insieme separato di servizi per ciascuna funzione (risorse umane, finanze e altro ancora). Semplifica il tracciamento e il reporting dei documenti firmati. Ad esempio, una banca ha più reparti. Puoi disporre di una configurazione separata per ogni reparto per un migliore monitoraggio dei documenti.

Un documento può anche avere più destinatari. Ad esempio, una domanda con carta di credito può avere più candidati. Una banca richiede la firma di tutti i richiedenti prima di iniziare la domanda di elaborazione. Per gli scenari con più destinatari, è possibile scegliere di firmare il documento in ordine sequenziale o simultaneo.

Per selezionare un Cloud Service e un ordine di firma:

![Cloud-service](assets/cloud-service.png)

1. Nel browser Contenuto, tocca **[!UICONTROL Contenitore modulo]** e tocca **[!UICONTROL Configura]** ![configurare](assets/Smock_Wrench_18_N.svg) icona. Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi la **[!UICONTROL Firma elettronica]** a soffietto e seleziona la **[!UICONTROL Abilita Adobe Sign]** opzione . Attiva [!DNL Adobe Sign] per un modulo adattivo.
1. Seleziona un Cloud Service dall’elenco di [!DNL Adobe Sign] Cloud Services.

   Se la **[!UICONTROL Adobe Sign Cloud Service]** elenco vuoto, seguire [Configura [!DNL Adobe Sign] con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) per configurare il servizio.

   Il menu a discesa elenca i Cloud Services esistenti nel `global` cartella in Strumenti > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Inoltre, il menu a discesa elenca anche i Cloud Services presenti nella cartella selezionata nella **[!UICONTROL Contenitore di configurazione]** quando si crea un modulo adattivo.

1. Seleziona l’ordine di firma dal **[!UICONTROL I destinatari possono completare]** finestra di dialogo. I destinatari possono firmare un modulo adattivo **[!UICONTROL Sequenziale]** - uno dopo l&#39;altro destinatario, oppure **[!UICONTROL Simultaneamente]** - in qualsiasi ordine.

   In ordine sequenziale, un destinatario riceve il contratto Adobe Sign alla volta. Dopo che il destinatario completa l’azione assegnata, il contratto viene inviato al destinatario successivo e così via.

   In ordine simultaneo, tutti i destinatari ricevono il contratto Adobe Sign e possono agire in parallelo tra loro.

1. Utilizza il campo ID accordo per associare un binding all’ID contratto (agreementId). Aggiunge l’ID accordo alla sezione afBoundData di invio dei dati per i moduli basati su schema. L’ID contratto viene aggiunto anche alla sezione afSubmissionInfo nei dati inviati per tutti i moduli abilitati per Adobe Sign. Puoi utilizzare l&#39;ID contratto per tenere traccia dello stato del contratto utilizzando un codice personalizzato (richiede l&#39;implementazione personalizzata).

1. [Aggiungere destinatari a un modulo adattivo](working-with-adobe-sign.md#addsignerstoanadaptiveform) e tocca Fine ![Salva](assets/save_icon.svg) per salvare le modifiche.

### Aggiungere destinatari a un modulo adattivo {#addsignerstoanadaptiveform}

Puoi avere uno o più destinatari per un accordo Adobe Sign. Quando si aggiunge un destinatario, è anche possibile configurare i dettagli di autenticazione per il destinatario e selezionare se il compilatore e il destinatario sono la stessa persona. Esegui i seguenti passaggi per aggiungere e fornire vari dettagli su un destinatario:

1. Nel browser Contenuto, tocca **[!UICONTROL Contenitore modulo]** e tocca **[!UICONTROL Configura]** ![configurare](assets/Smock_Wrench_18_N.svg) icona. Apre il browser delle proprietà con le proprietà del contenitore Modulo adattivo.
1. Nel browser delle proprietà, espandi la **[!UICONTROL Firma elettronica]** a soffietto e seleziona la **[!UICONTROL Abilita Adobe Sign]** opzione . Attiva [!DNL Adobe Sign] per un modulo adattivo.
1. Tocca **[!UICONTROL Aggiungi destinatario]**. Aggiunge un destinatario al Modulo adattivo. È possibile aggiungere più destinatari a un modulo adattivo. Tutti i destinatari ricevono un accordo Adobe Sign sull’invio del modulo adattivo.
   ![dettagli telefonici](assets/recipient-settings.png)

1. Fai clic sul pulsante **[!UICONTROL Modifica]** ![Modifica](assets/Smock_Edit_18_N.svg) per specificare le seguenti informazioni sul destinatario:

   * **[!UICONTROL Titolo]:** Specifica un titolo per identificare in modo univoco un destinatario.

   * **[!UICONTROL Il destinatario è anche la persona che deve compilare il modulo?]:** Seleziona **[!UICONTROL Sì]**, se il compilatore e il primo destinatario sono la stessa persona. <!-- If the option is set to **No,** then do not use the signature step component in the Adaptive Form. If the form contains a Signature Step component, then the field is automatically set to Yes. -->

   * **[!UICONTROL Ruolo destinatario]:** Seleziona il ruolo di un destinatario. Adobe Sign per i livelli di servizio business ed enterprise ha la possibilità di espandere la [ruoli per i destinatari del contratto](https://helpx.adobe.com/sign/using/set-up-signer-approver-roles.html), al di là della **Firmatario**, per soddisfare meglio i requisiti del flusso di lavoro.

   * **[!UICONTROL Indirizzo e-mail destinatario]:** Specifica l’indirizzo e-mail del destinatario. Il destinatario riceve l’accordo Adobe Sign sull’indirizzo e-mail specificato. È possibile scegliere di utilizzare un indirizzo e-mail fornito in un campo modulo, nel profilo utente Experience Manager dell’utente connesso o immettere manualmente un indirizzo e-mail. Si tratta di un passo obbligatorio.

      >[!NOTE]
      >
      >Assicurati che l’indirizzo e-mail del primo destinatario o dell’unico destinatario (se esiste un singolo destinatario) non sia identico a [!DNL Adobe Sign] account utilizzato per configurare AEM Cloud Services.

   * **[!UICONTROL Metodo di autenticazione destinatario]:** Specifica il metodo per autenticare un destinatario prima di aprire il contratto Adobe Sign. Puoi scegliere tra telefono, knowledge base, autenticazione basata sull&#39;identità social e [ID governo](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html).
   >[!NOTE]
   >
   >    * Per impostazione predefinita, l’autenticazione basata sull’identità social fornisce un’opzione per l’autenticazione tramite Facebook, Google e LinkedIn. È possibile contattare [!DNL Adobe Sign] supporto per abilitare altri provider di autenticazione social.


   * **[!DNL Adobe Sign]campi da compilare o firmare:** Seleziona [!DNL Adobe Sign] campi per il destinatario. Un modulo adattivo può avere più [!DNL Adobe Sign] campi. Puoi scegliere di abilitare campi specifici per un destinatario. Nel campo vengono visualizzate tutte le opzioni disponibili [!DNL Adobe Sign] Blocchi. Quando selezioni un blocco, vengono selezionati tutti i campi del blocco. Puoi usare l’icona X per deselezionare un campo.

   ![dettagli destinatario](assets/signer-details.png)

   L&#39;immagine precedente ha due esempi [!DNL Adobe Sign] Blocchi: Informazioni personali e dettagli dell&#39;ufficio

   Tocca ![Salva](assets/save_icon.svg) icona. Il destinatario viene aggiunto.

### Selezionare un’azione di invio per un modulo adattivo {#selectsubmitactionforanadaptiveform}

Dopo di te, aggiungi [!DNL Adobe Sign] campi di un modulo adattivo, abilita [!DNL Adobe Sign] dal contenitore modulo, seleziona [!DNL Adobe Sign] Cloud Service e aggiungi i destinatari dell’accordo Adobe Sign, seleziona un’azione di invio appropriata per il modulo adattivo. Per informazioni dettagliate sulle azioni di invio di Forms adattive, consulta [Configurazione dell’azione Invia](configuring-submit-actions.md).

La firma e l’invio di un modulo sono indipendenti l’uno dall’altro. L’invio di moduli adattivi avviene non appena viene creato un accordo Adobe Sign dopo l’invio di un modulo da parte dell’utente. [!DNL AEM Forms] as a Cloud Service non attende che i destinatari firmino o completino altre azioni per inviare un modulo adattivo. Un modulo viene inviato non appena l’utente fa clic sul pulsante Invia o in un passaggio Riepilogo viene visualizzato il riepilogo del modulo.

Inoltre, un [!DNL Adobe Sign] il modulo adattivo abilitato incorpora l’ID accordo di Adobe Sign per l’invio dei dati. Puoi utilizzare l&#39;ID contratto per tenere traccia dello stato del contratto utilizzando un codice personalizzato (richiede l&#39;implementazione personalizzata).

L’ID contratto di Adobe Sign (agreementId) è incluso nei dati di invio del modulo adattivo. Per impostazione predefinita, l’ID del contratto è presente nella variabile `afSubmissionInfo` nodo dei dati inviati.

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

Facoltativamente, puoi anche associare un bindref all&#39;ID contratto (agreementId). Aggiunge l&#39;ID del contratto alla sezione afBoundData dei dati inviati. Ad esempio, nei seguenti dati inviati, l’ID contratto è associato a `<userName>` nodo:

```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <afData>
         <afUnboundData>
            <data />
         </afUnboundData>
         <afBoundData>
            <config xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
               <agreementID>3AAABLblqZhC2MWu7GFauKh45j_t2ih8mAtmbdIcNSl1HgQubhMJfDaDfylyN7NQiYRam_44ISKm45enIOafHqWZrdaxShf9r</agreementID>
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
>Data of the Adaptive Form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

L’esperienza di firma del modulo è pronta. È possibile visualizzare un’anteprima del modulo per verificare l’esperienza di firma. Sul modulo pubblicato, [!DNL Adobe Sign] I campi blocco vengono visualizzati quando un destinatario riceve il modulo per la firma tramite e-mail. Quando il **[!UICONTROL Quando sono uguali il destinatario e la persona che compila il modulo?]** l’opzione è contrassegnata come sì e la condizione è soddisfatta, l’utente viene reindirizzato al contratto Adobe Sign dopo l’invio e l’utente può firmare il documento immediatamente, invece di attendere che il contratto venga visualizzato nell’e-mail.

## Configurare le firme cloud per un modulo adattivo {#configure-cloud-signatures-for-an-adaptive-form}

Le firme digitali o le firme remote basate su cloud sono una nuova generazione di firme digitali che funzionano su desktop, dispositivi mobili e web e soddisfano i più alti livelli di conformità e garanzia per l’autenticazione dei destinatari. È possibile firmare un modulo adattivo con firme digitali basate su cloud.

Dopo [modifica delle proprietà del modulo adattivo per Adobe Sign](working-with-adobe-sign.md#enableadobesign), effettua le seguenti operazioni per aggiungere il campo firma cloud a un modulo adattivo:

1. Trascinamento della selezione **[!UICONTROL Blocco Adobe Sign]** dal browser Componenti al modulo adattivo. La [!UICONTROL Blocco Adobe Sign] il componente ha tutti i [!DNL Adobe Sign] campi. Per impostazione predefinita, aggiunge un **[!UICONTROL Firma]** al modulo adattivo.

   ![Blocco dei segni](assets/sign-block-new.png)

1. Seleziona la **[!UICONTROL Blocco Adobe Sign]** e tocca **[!UICONTROL Modifica]** ![Modifica](assets/Smock_Edit_18_N.svg) icona. Visualizza le opzioni per aggiungere campi e formattare l’aspetto di un campo.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Seleziona e aggiungi [!DNL Adobe Sign] campi. **B.** Espandi la [!DNL Adobe Sign] blocca a schermo intero

1. Tocca **[!UICONTROL Campo Adobe Sign]** ![Adobe Sign](assets/adobesign.png) icona. Visualizza le opzioni di selezione e aggiunta [!DNL Adobe Sign] campi.

   Espandi la **[!UICONTROL Tipo]** campo a discesa da selezionare **[!UICONTROL Firma digitale]** e tocca **[!UICONTROL Fine]** icona per aggiungere il campo selezionato a [!DNL Adobe Sign] blocco.

   ![Firme digitali](assets/digital_signatures_new.png)

   È obbligatorio fornire un nome univoco per un campo.

   Applicare le firme digitali al modulo adattivo utilizzando:

   * Firme cloud: Firma con un [ID digitale](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) ospitato da un provider di servizi attendibili.
   * Adobe Acrobat o Reader: Scarica e apri il documento con Adobe Acrobat o Reader per firmare utilizzando una smart card, un token USB o un ID digitale basato su file.

   Dopo aver aggiunto il campo firma cloud al modulo adattivo, esegui i seguenti passaggi per completare il processo di configurazione:

   * [Abilitare Adobe Sign per un modulo adattivo](#enableadobsignforanadaptiveform)
   * [Selezionare Adobe Sign Cloud Service per un modulo adattivo](#selectadobesigncloudserviceforanadaptiveform)
   * [Aggiungere destinatari a un modulo adattivo](#addsignerstoanadaptiveform)
   * [Selezionare un’azione di invio per un modulo adattivo](#selectsubmitactionforanadaptiveform)


### Configura la pagina di ringraziamento o il componente del passaggio di riepilogo {#configure-the-thank-you-page-or-summary-step-component}

La **[!UICONTROL Passaggio di riepilogo]** il componente invia automaticamente il modulo, compila le informazioni all’interno della pagina di riepilogo personalizzata e visualizza il riepilogo del modulo inviato. Il componente Passo di riepilogo occupa la larghezza completa disponibile per il modulo. Si consiglia di non avere nessun altro componente nella sezione contenente il componente Passaggio di riepilogo .

## Domande frequenti {#frequently-asked-questions}

**D:** È possibile incorporare un modulo adattivo in un altro modulo adattivo. Può il modulo adattivo incorporato essere [!DNL Adobe Sign] abilitato?
**Ans:** No, Experience Manager Forms non supporta l’uso di un modulo adattivo che incorpora un [!DNL Adobe Sign] modulo adattivo abilitato per la firma

**D:** Quando creo un modulo adattivo utilizzando il modello avanzato e lo apro per la modifica, viene visualizzato un messaggio di errore &quot;Firma elettronica o destinatari non configurati correttamente&quot;. appare. Come risolvere il messaggio di errore?
**Ans:** Il modulo adattivo creato utilizzando il modello avanzato è configurato per l’utilizzo [!DNL Adobe Sign]. Per risolvere l’errore, crea e seleziona un [!DNL Adobe Sign] configurazione cloud e configurazione di un [!DNL Adobe Sign] Destinatario del modulo adattivo.

**D:** Posso usare [!DNL Adobe Sign] tag di testo in un componente di testo statico di un modulo adattivo?
**Ans:** Sì, è possibile utilizzare i tag di testo in un componente di testo per aggiungere [!DNL Adobe Sign] campi in un documento di record (solo opzione per il documento di record generato automaticamente) abilitato Modulo adattivo. Per informazioni sulla procedura e le regole per creare un tag di testo, consulta [Documentazione di Adobe Sign](https://helpx.adobe.com/sign/using/text-tag.html). Inoltre, Adaptive Forms ha un supporto limitato per i tag di testo. È possibile utilizzare i tag di testo per creare solo i campi che [Blocco Adobe Sign](working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) supporta.

## Risoluzione dei problemi {#troubleshoot}

### [!DNL Adobe Sign] guasti del contratto {#adobe-sign-agreement-failures}

**Problema**
Quando [!DNL Adobe Sign] il servizio è configurato per un modulo adattivo, il servizio non riesce a creare un [!DNL Adobe Sign] accordo per la forma adattiva sottostante.

**Risoluzione**

* Controlla la [configurazione di Adobe Sign Cloud Service](adobe-sign-integration-adaptive-forms.md) utilizzato nel modulo adattivo.
* Assicurati che l’applicazione API sia attiva su [!DNL Adobe Sign] server utilizzato per configurare [!DNL Adobe Sign] Il Cloud Service dispone delle autorizzazioni necessarie.
* Se utilizzi più [!DNL Adobe Sign] Cloud Services, **[!UICONTROL URL di autenticazione]** di tutti i servizi **[!UICONTROL Adobe Sign Shard]**.

* Utilizzare indirizzi e-mail separati per la configurazione [!DNL Adobe Sign] e per il primo o singolo destinatario. L’indirizzo e-mail del primo destinatario o dell’unico destinatario (se esiste il singolo destinatario) non può essere identico a [!DNL Adobe Sign] account utilizzato per configurare AEM Cloud Services.

## Articoli correlati {#related-articles}

* [Integrare [!DNL Adobe Sign] con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)
* [Best practice per l’utilizzo [!DNL Adobe Sign] con Forms adattivo](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
