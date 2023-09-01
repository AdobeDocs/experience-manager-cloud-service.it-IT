---
title: Utilizzare flussi di lavoro AEM incentrati su moduli per automatizzare i processi aziendali
description: I flussi di lavoro incentrati su Forms consentono di creare rapidamente flussi di lavoro adattivi basati su Forms. Puoi utilizzare Adobe Sign per firmare i documenti tramite e-sign, creare processi aziendali basati su moduli, recuperare e inviare dati a più origini dati e inviare notifiche e-mail
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
source-git-commit: a635a727e431a73086a860249e4f42d297882298
workflow-type: tm+mt
source-wordcount: '7452'
ht-degree: 1%

---

# Utilizzare flussi di lavoro AEM incentrati su Forms - Riferimento alla fase per automatizzare i processi aziendali{#forms-centric-workflow-on-osgi-step-reference}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html) |
| AEM as a Cloud Service | Questo articolo |

<span class="preview"> Singer, Audit trail e opzioni di autenticazione basate su ID governativo in [Passaggio Firma documento](#sign-document-step) sono funzioni pre-release e accessibili tramite [canale preliminare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

Si utilizzano i modelli di flusso di lavoro. Un modello consente di definire ed eseguire una serie di passaggi. Puoi anche definire le proprietà del modello, ad esempio se il flusso di lavoro è transitorio o utilizza più risorse. È possibile [includere vari passaggi del flusso di lavoro AEM in un modello per raggiungere la logica di business](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem).

## Passaggi incentrati su Forms {#forms-workflow-steps}

I passaggi del flusso di lavoro incentrati su Forms eseguono operazioni specifiche per AEM Forms in un flusso di lavoro AEM. Questi passaggi consentono di creare rapidamente un flusso di lavoro adattivo basato su Forms basato su Forms su OSGi. Questi flussi di lavoro possono essere utilizzati per sviluppare flussi di lavoro di revisione e approvazione di base, interni e attraverso il firewall. È inoltre possibile utilizzare i passaggi di Forms Workflow per:

* Crea processi aziendali, flussi di lavoro successivi all’invio e flussi di lavoro back-end per gestire i processi di iscrizione.

* Crea e assegna attività a un utente o a un gruppo.

* Utilizzare [!DNL Adobe Sign] in un flusso di lavoro AEM per inviare un documento per la firma.

* Genera un documento di record su richiesta o all’invio di un modulo.

* Collega un modello di flusso di lavoro con diverse origini dati per salvare e recuperare facilmente i dati.

* Utilizza il passaggio e-mail per inviare e-mail di notifica e altri allegati al completamento di un’azione e all’inizio o al completamento di un flusso di lavoro.

>[!NOTE]
>
>Se il modello di flusso di lavoro è contrassegnato per un archivio esterno, per tutti i passaggi del Forms Workflow è possibile selezionare solo l&#39;opzione della variabile per memorizzare o recuperare file di dati e allegati.


## Assegna passaggio attività {#assign-task-step}

Il passaggio Assegna attività crea un elemento di lavoro e lo assegna a un utente o a un gruppo. Oltre all’assegnazione dell’attività, il componente specifica anche il Modulo adattivo o il PDF non interattivo per l’attività. Il modulo adattivo è necessario per accettare l’input degli utenti e dei PDF non interattivi, oppure un modulo adattivo di sola lettura viene utilizzato per i flussi di lavoro di sola revisione.

È inoltre possibile utilizzare il componente per controllare il comportamento dell&#39;attività. Ad esempio, la creazione di un documento di record automatico, l’assegnazione dell’attività a un utente o gruppo specifico, la specifica del percorso dei dati inviati, il percorso dei dati da precompilare e le azioni predefinite. Il passaggio Assegna attività presenta le seguenti proprietà:

* **[!UICONTROL Titolo]**: titolo dell’attività. Il titolo viene visualizzato nella casella in entrata AEM.
* **[!UICONTROL Descrizione]**: Spiegazione delle operazioni eseguite nell’attività. Queste informazioni sono utili per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

* **[!UICONTROL Percorso miniatura]**: percorso della miniatura dell’attività. Se non viene specificato alcun percorso, per un modulo adattivo viene visualizzata una miniatura predefinita e per il documento di record viene visualizzata un’icona predefinita.
* **[!UICONTROL Fase flusso di lavoro]**: un flusso di lavoro può avere più fasi. Questi stadi vengono visualizzati nella casella in entrata AEM. Potete definire questi stadi nelle proprietà del modello (Sidekick > Pagina > Proprietà pagina > Stadi).
* **[!UICONTROL Priorità]**: la priorità selezionata viene visualizzata nella casella in entrata AEM. Le opzioni disponibili sono Alta, Media e Bassa. Il valore predefinito è Medio.
* **[!UICONTROL Data di scadenza]**: specifica quanti giorni o ore devono trascorrere prima che l’attività venga contrassegnata come scaduta. Se si seleziona **[!UICONTROL Disattivato]**, quindi l’attività non viene mai contrassegnata come scaduta. È inoltre possibile specificare un gestore di timeout per eseguire attività specifiche dopo la scadenza dell&#39;attività.

* **[!UICONTROL Giorni]**: numero di giorni prima dei quali l’attività deve essere completata. Il numero di giorni viene conteggiato dopo l&#39;assegnazione dell&#39;attività a un utente. Se un’attività non è completa e supera il numero di giorni specificato nel campo Giorni, se selezionata, viene attivato un gestore di timeout dopo la data di scadenza.
* **[!UICONTROL Ore]**: numero di ore prima del quale l’attività deve essere completata. Il numero di ore che vengono conteggiate dopo l&#39;assegnazione dell&#39;attività a un utente. Se un’attività non è completa e supera il numero di ore specificato nel campo Ore, se selezionato viene attivato un gestore di timeout dopo le ore dovute.
* **[!UICONTROL Timeout dopo la data di scadenza]**: seleziona questa opzione per abilitare il campo di selezione Gestore di timeout.
* **[!UICONTROL Gestore timeout]**: seleziona lo script da eseguire quando il passaggio dell’attività di assegnazione oltrepassa la data di scadenza. Script inseriti nell’archivio CRX in [app]È possibile selezionare /fd/dashboard/scripts/timeoutHandler. Il percorso specificato non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo.
* **[!UICONTROL Evidenzia l&#39;azione e commenta dall&#39;ultima attività in Dettagli attività]**: seleziona questa opzione per visualizzare l’ultima azione eseguita e il commento ricevuto nella sezione dei dettagli di un’attività.
* **[!UICONTROL Tipo]**: scegli il tipo di documento da compilare all’avvio del flusso di lavoro. Puoi scegliere un modulo adattivo, un modulo adattivo di sola lettura, un documento PDF non interattivo.

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL Usa modulo adattivo]**: specifica il metodo per individuare il modulo adattivo di input. Questa opzione è disponibile se si seleziona Modulo adattivo o Modulo adattivo di sola lettura dall’elenco a discesa Tipo. Puoi utilizzare il modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile di tipo String per specificare il percorso.\
  È possibile associare più Forms adattivi a un flusso di lavoro. Di conseguenza, puoi specificare un modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL Percorso modulo adattivo]**: specifica il percorso del modulo adattivo. Puoi utilizzare il modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto, oppure recuperare il modulo adattivo da un percorso memorizzato in una variabile di tipo stringa di dati.
* **[!UICONTROL Seleziona PDF di input tramite]**: specifica il percorso di un documento PDF non interattivo. Il campo è disponibile quando si sceglie un documento PDF non interattivo nel campo Tipo. È possibile selezionare il PDF di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto oppure utilizzando una variabile di tipo dati Documento. Ad esempio: [Payload_Directory]/Workflow/PDF/credit-card.pdf. Il percorso non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo. Per utilizzare l’opzione Percorso PDF, è necessario abilitare l’opzione Documento di record o Adaptive Forms basato su modello di modulo.
* **[!UICONTROL Per l’attività completata, esegui il rendering del modulo adattivo come]**: quando un’attività è contrassegnata come completata, è possibile eseguire il rendering del modulo adattivo come modulo adattivo di sola lettura o documento PDF. Per eseguire il rendering del modulo adattivo come documento record, è necessario abilitare l’opzione Documento di record o un Forms adattivo basato su modello di modulo.
* **[!UICONTROL Prepopolato]**: i seguenti campi elencati di seguito fungono da input per l’attività:

   * **[!UICONTROL Seleziona file di dati di input tramite]**: percorso del file di dati di input (.json, .xml, .doc o modello dati modulo). Puoi recuperare il file di dati di input utilizzando un percorso relativo al payload o recuperare il file memorizzato in una variabile di tipo Documento, XML o JSON. Ad esempio, il file contiene i dati inviati per il modulo tramite un&#39;applicazione Casella in entrata AEM. Un esempio di percorso è [Payload_Directory]/workflow/data.
   * **[!UICONTROL Seleziona allegati di input tramite]**: gli allegati disponibili nel percorso vengono allegati al modulo associato all’attività. Il percorso può essere relativo al payload o recuperare l’allegato memorizzato in una variabile di un documento. Un esempio di percorso è [Payload_Directory]/attachments/. È possibile specificare gli allegati posizionati rispetto al payload o utilizzare una variabile di tipo documento (Elenco array > Documento) per specificare un allegato di input per il modulo adattivo.

  <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL Mappatura attributi richiesta]**: utilizza la sezione Mappatura attributi della richiesta per definire [nome e valore dell’attributo di richiesta](work-with-form-data-model.md#bindargument). Recupera i dettagli dall’origine dati in base al nome e al valore dell’attributo specificati nella richiesta. È possibile definire un valore di attributo della richiesta utilizzando un valore letterale o una variabile di tipo di dati String.

  <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL Informazioni inviate]**: i seguenti campi elencati di seguito fungono da posizioni di output per l’attività:

   * **[!UICONTROL Salva file di dati di output tramite]**: salva il file di dati (.json, .xml, .doc o il modello dati del modulo). Il file di dati contiene informazioni inviate tramite il modulo associato. Puoi salvare il file di dati di output utilizzando un percorso relativo al payload o memorizzarlo in una variabile di tipo Documento, XML o JSON. Ad esempio: [Payload_Directory]/Workflow/data, dove i dati sono un file.
   * **[!UICONTROL Salva allegati tramite]**: salva gli allegati del modulo forniti in un’attività. È possibile salvare gli allegati utilizzando un percorso relativo al payload o memorizzarlo in una variabile dell’elenco di matrici del tipo di dati Documento.
   * **[!UICONTROL Salva documento di record tramite]**: percorso per salvare un file del documento record. Ad esempio: [Payload_Directory]/DocumentofRecord/credit-card.pdf. Puoi salvare il documento record utilizzando un percorso relativo al payload o memorizzarlo in una variabile di tipo Dati documento. Se si seleziona la **[!UICONTROL Relativo al payload]** , il documento di record non viene generato se il campo percorso viene lasciato vuoto. Questa opzione è disponibile solo se si seleziona Modulo adattivo dall’elenco a discesa Tipo.

  <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL Assegnatario]** > **[!UICONTROL Assegna opzioni]**: specifica il metodo per assegnare l’attività a un utente. È possibile assegnare dinamicamente l&#39;attività a un utente o a un gruppo utilizzando lo script Selettore partecipanti oppure assegnare l&#39;attività a un utente o a un gruppo AEM specifico.
* **[!UICONTROL Selettore partecipanti]**: l’opzione è disponibile quando **[!UICONTROL Dinamicamente per un utente o un gruppo]** nel campo Assegna opzioni. È possibile utilizzare un codice ECMAScript o un servizio per selezionare dinamicamente un utente o un gruppo. Per ulteriori informazioni, consulta [Assegnazione dinamica di un flusso di lavoro agli utenti](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) e [Creazione di un passaggio Partecipante dinamico Adobe Experience Manager personalizzato.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **[!UICONTROL Partecipanti]**: campo disponibile quando **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** è selezionata in **[!UICONTROL Selettore partecipanti]** campo. Il campo consente di selezionare utenti o gruppi per l&#39;opzione RandomParticipantChooser.

* **[!UICONTROL Assegnatario]**: campo disponibile quando **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** è selezionato in **[!UICONTROL Selettore partecipanti]** campo. Il campo consente di selezionare una variabile di tipo String per definire l’assegnatario.

* **[!UICONTROL Argomenti]**: il campo è disponibile quando nel campo Selettore partecipante è selezionato uno script diverso da RandomParticipantChoose. Il campo consente di fornire un elenco di argomenti separati da virgole per lo script selezionato nel campo Selettore partecipanti.

* **[!UICONTROL Utente o gruppo]**: l’attività viene assegnata a un utente o a un gruppo selezionato. L’opzione è disponibile quando **[!UICONTROL A un utente o gruppo specifico, opzione]** è selezionato in **[!UICONTROL Assegna opzioni]** campo. Il campo elenca tutti gli utenti e i gruppi del [!DNL workflow-users] gruppo.\
  Il **[!UICONTROL Utente o gruppo]** Il menu a discesa elenca gli utenti e i gruppi a cui l&#39;utente connesso ha accesso. La visualizzazione del nome utente dipende dalla disponibilità delle autorizzazioni di accesso per **[!UICONTROL utenti]** nell’archivio crx per quel particolare utente.

* **[!UICONTROL Invia e-mail di notifica]**: seleziona questa opzione per inviare notifiche e-mail all’assegnatario. Queste notifiche vengono inviate quando un’attività viene assegnata a un utente o a un gruppo. È possibile utilizzare **[!UICONTROL Indirizzo e-mail destinatario]** per specificare il meccanismo di recupero dell’indirizzo e-mail.

* **[!UICONTROL Indirizzo e-mail destinatario]**: puoi memorizzare un indirizzo e-mail in una variabile, utilizzare un valore letterale per specificare un indirizzo e-mail permanente o utilizzare l’indirizzo e-mail predefinito dell’assegnatario specificato nel profilo dell’assegnatario. Puoi utilizzare il letterale o una variabile per specificare l’indirizzo e-mail di un gruppo. L’opzione della variabile è utile per recuperare e utilizzare in modo dinamico un indirizzo e-mail. Il **[!UICONTROL Usa indirizzo e-mail predefinito dell’assegnatario]** l&#39;opzione è riservata a un solo assegnatario. In questo caso, viene utilizzato l’indirizzo e-mail memorizzato nel profilo utente degli assegnatari.

* **[!UICONTROL Modello e-mail HTML]**: seleziona il modello e-mail per l’e-mail di notifica. Per modificare un modello, modifica il file che si trova in /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt in crx-repository.
* **[!UICONTROL Consenti delega a]**: la Casella in entrata AEM fornisce all’utente connesso un’opzione per delegare il flusso di lavoro assegnato a un altro utente. Puoi delegare all’interno dello stesso gruppo o all’utente del flusso di lavoro di un altro gruppo. Se l’attività è assegnata a un singolo utente e il **[!UICONTROL consenti delega a membri del gruppo assegnatario]** , non è possibile delegare l&#39;attività a un altro utente o gruppo.
* **[!UICONTROL Impostazioni di condivisione]**: la Casella in entrata AEM fornisce opzioni per condividere un’unica o tutte le attività presenti nella Casella in entrata con un altro utente:
   * Quando **[!UICONTROL Consenti all’assegnatario di condividere in modo esplicito nella casella in entrata]** è selezionata, l’utente può selezionare l’attività nella casella in entrata AEM e condividerla con un altro utente AEM.
   * Quando **[!UICONTROL Consenti all’assegnatario di condividere tramite la casella in entrata]** Se l&#39;opzione è selezionata e gli utenti condividono i propri elementi della casella in entrata o consentono ad altri utenti di accedere ai propri elementi della casella in entrata, solo le attività con l&#39;opzione precedentemente indicata sono condivise con altri utenti.
   * Quando **[!UICONTROL Consenti all’assegnatario di delegare utilizzando le impostazioni &quot;Fuori sede&quot;]** è selezionato. L’assegnatario può abilitare l’opzione per delegare l’attività ad altri utenti insieme ad altre opzioni Fuori sede. Tutte le nuove attività assegnate all&#39;utente fuori sede vengono automaticamente delegate (assegnate) agli utenti indicati nelle impostazioni fuori sede.

  Consente ad altri utenti di scegliere le attività assegnate mentre è fuori sede e non può lavorare sulle attività assegnate.

* **[!UICONTROL Azioni]** > **[!UICONTROL Azioni predefinite]**: sono disponibili le azioni Invio, Salva e Reimposta pronte all’uso. Per impostazione predefinita, sono attivate tutte le azioni predefinite.
* **[!UICONTROL Variabile percorso]**: nome della variabile di route. La variabile di route acquisisce le azioni personalizzate selezionate da un utente nella casella in entrata AEM.
* **[!UICONTROL Percorsi]**: un’attività può diramarsi in diversi percorsi. Se selezionata nella casella in entrata AEM, la route restituisce un valore e i rami del flusso di lavoro si basano sulla route selezionata. È possibile archiviare le route in una variabile di array di tipi di dati String oppure selezionare **[!UICONTROL Letterale]** per aggiungere percorsi manualmente.

* **[!UICONTROL Titolo percorso]**: specifica il titolo della route. Viene visualizzato nella casella in entrata AEM.
* **[!UICONTROL Icona rosso corallo]**: specifica un attributo HTML di un’icona corallo. La libreria CorelUI di Adobe fornisce un ampio set di icone touch-first. È possibile scegliere e utilizzare un&#39;icona per il ciclo di lavorazione. Viene visualizzato insieme al titolo nella casella in entrata AEM. Se memorizzi le route in una variabile, le route utilizzano un&#39;icona di corallo &quot;Tag&quot; predefinita.
* **[!UICONTROL Consenti all’assegnatario di aggiungere commenti]**: seleziona questa opzione per abilitare i commenti per l’attività. L’assegnatario può aggiungere i commenti dalla casella in entrata AEM al momento dell’invio dell’attività.
* **[!UICONTROL Salva commento in variabile]**: salva il commento in una variabile di tipo stringa. Questa opzione viene visualizzata solo se si seleziona **[!UICONTROL Consenti all’assegnatario di aggiungere commenti]** casella di controllo.

* **[!UICONTROL Consenti all’assegnatario di aggiungere allegati all’attività]**: selezionare questa opzione per abilitare gli allegati per l&#39;attività. L’assegnatario può aggiungere gli allegati dalla casella in entrata AEM al momento dell’invio dell’attività. Puoi anche limitare la dimensione massima **[!UICONTROL (Dimensione massima file)]** di un allegato. La dimensione predefinita è 2 MB.

* **[!UICONTROL Salva allegati attività di output tramite]**: specifica il percorso della cartella dell’allegato. È possibile salvare gli allegati delle attività di output utilizzando un percorso relativo al payload o in una variabile di un array di tipi di dati del documento. Questa opzione viene visualizzata solo se si seleziona **[!UICONTROL Consenti all’assegnatario di aggiungere allegati all’attività]** e seleziona **[!UICONTROL Modulo adattivo]**, **[!UICONTROL Modulo adattivo di sola lettura]**, o **[!UICONTROL Documento PDF non interattivo]** dal **[!UICONTROL Tipo]** elenco a discesa nella **[!UICONTROL Modulo/Documento]** scheda.

* **[!UICONTROL Utilizzare metadati personalizzati]**: seleziona questa opzione per abilitare il campo di metadati personalizzato. I metadati personalizzati vengono utilizzati nei modelli e-mail.
* **[!UICONTROL Metadati personalizzati]**: seleziona un metadati personalizzato per i modelli e-mail. I metadati personalizzati sono disponibili nel crx-repository in apps/fd/dashboard/scripts/metadataScripts. Il percorso specificato non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo. Puoi anche utilizzare un servizio per i metadati personalizzati. Puoi anche estendere `WorkitemUserMetadataService` per fornire metadati personalizzati.
* **[!UICONTROL Mostra dati da passaggi precedenti]**: seleziona questa opzione per consentire agli assegnatari di visualizzare gli assegnatari precedenti, le azioni già eseguite sull’attività, i commenti aggiunti all’attività e il documento di record dell’attività completata, se disponibile.
* **[!UICONTROL Mostra dati da passaggi successivi]**: seleziona questa opzione per consentire all’assegnatario corrente di visualizzare l’azione intrapresa e i commenti aggiunti all’attività dagli assegnatari successivi. Consente inoltre all’assegnatario corrente di visualizzare un documento di record dell’attività completata, se disponibile.
* **[!UICONTROL Visibilità del tipo di dati]**: per impostazione predefinita, l’assegnatario può visualizzare un documento di record, gli assegnatari, le azioni intraprese e i commenti aggiunti dagli assegnatari precedenti e successivi. Utilizza l’opzione visibilità del tipo di dati per limitare il tipo di dati visibile agli assegnatari.

>[!NOTE]
>
>Le opzioni per salvare il passaggio Assegna attività come bozza e per recuperare la cronologia del passaggio Assegna attività sono disabilitate quando si configura un modello di flusso di lavoro AEM per l’archiviazione di dati esterni. Inoltre, nella casella in entrata, l’opzione di salvataggio è disabilitata.

## Passaggio Converti in PDF/A {#convert-pdfa}

PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, incorporando i font e decomprimendo il file. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. È possibile utilizzare ***Converti in PDF/A*** entra in un flusso di lavoro AEM per convertire i documenti PDF in formato PDF/A.

Il passaggio Converti in PDF/A ha le seguenti proprietà:

**[!UICONTROL Documento di input]**: il documento di input può essere relativo al payload, avere un percorso assoluto, può essere fornito come payload o memorizzato in una variabile di tipo dati Documento.

**[!UICONTROL Opzioni di conversione]**: utilizzando questa proprietà, vengono specificate le impostazioni per la conversione di documenti PDF in documenti PDF/A. Le opzioni disponibili in questa scheda sono:
* **[!UICONTROL Conformità]**: specifica lo standard a cui deve conformarsi il documento PDF/A di output. Supporta diversi standard PDF come PDF/A-1b, PDF/A-2b o PDF/A-3b.
* **[!UICONTROL Livello di risultato]**: specifica il livello di risultato come PassFail, Summary o Detailed, per l&#39;output di conversione.
* **[!UICONTROL Spazio colore]**: specifica lo spazio colore predefinito come S_RGB, COATED_FOGRA27, JAPAN_COLOR_COATED o SWOP, che può essere utilizzato per i file PDF/A di output.
* **[!UICONTROL Contenuto facoltativo]**: consenti a specifici oggetti grafici e/o annotazioni di essere visibili nel documento PDF/A di output solo quando viene soddisfatto un set di criteri specificato.

**[!UICONTROL Documenti di output]**: specifica il percorso in cui salvare il file di output. Il file di output può essere salvato in una posizione relativa al payload, sovrascrive il payload, se il payload è un file o in una variabile di tipo dati Document.


## Passaggio Invia e-mail {#send-email-step}

Utilizza la fase e-mail per inviare un’e-mail, ad esempio un’e-mail con un documento Record e il collegamento di un modulo adattivo <!-- , link of an interactive communication-->o con un documento PDF allegato. Il passaggio Invia e-mail supporta [E-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Le e-mail di HTML sono dinamiche e si adattano alle dimensioni del client e-mail e dello schermo dei destinatari. Puoi utilizzare un modello di e-mail HTML per definire l’aspetto, la combinazione di colori e il comportamento dell’e-mail.

Il passaggio e-mail utilizza Day CQ Mail Service per inviare le e-mail. Prima di utilizzare il passaggio e-mail, accertati che il servizio e-mail sia configurato. Per impostazione predefinita, le e-mail supportano solo i protocolli HTTP e HTTP. [Contatta il team di supporto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en#sending-email) per abilitare le porte per l’invio di e-mail e il protocollo SMTP per il tuo ambiente. La restrizione contribuisce a migliorare la sicurezza della piattaforma.

Il passaggio e-mail presenta le seguenti proprietà:

**[!UICONTROL Titolo]**: il titolo del passaggio aiuta a identificare il passaggio nell’editor del flusso di lavoro.

**[!UICONTROL Descrizione]**: la spiegazione è utile per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

**[!UICONTROL Oggetto e-mail]**: l’oggetto può essere recuperato dai metadati di un flusso di lavoro, specificato manualmente, o recuperato dal valore memorizzato in una variabile. Selezionare una delle opzioni seguenti:

* **[!UICONTROL Letterale]** Specificare manualmente un oggetto.
* **[!UICONTROL Recupera dai metadati del flusso di lavoro]** : recupera l’oggetto da una proprietà di metadati.
* **[!UICONTROL Variabile]** : recupera l’oggetto dal valore memorizzato in una variabile di tipo dati stringa.

**[!UICONTROL Modello e-mail HTML]**: modello di HTML per l’e-mail. Puoi specificare le variabili in un modello e-mail. Il passaggio E-mail estrae e visualizza tutte le variabili incluse in un modello per gli input.

**[!UICONTROL Metadati modello e-mail]**: il valore delle variabili del modello e-mail può essere un valore specificato dall’utente, il percorso di una risorsa nell’istanza di authoring o nel server di pubblicazione, un’immagine o una proprietà di metadati del flusso di lavoro.

* **[!UICONTROL Letterale]**: utilizza l’opzione quando conosci il valore esatto da specificare. Ad esempio: [example@example.com](mailto:example@example.com).

* **[!UICONTROL Metadati flusso di lavoro]**: utilizza l’opzione quando il valore da utilizzare viene salvato in una proprietà di metadati del flusso di lavoro. Dopo aver selezionato l’opzione, immetti il nome della proprietà dei metadati nella casella di testo vuota sotto l’opzione Metadati del flusso di lavoro. Ad esempio, emailAddress.

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL Immagine]**: utilizza l’opzione per incorporare un’immagine nell’e-mail. Dopo aver selezionato l’opzione, sfoglia e scegli l’immagine. L’opzione immagine è disponibile solo per i tag immagine (&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />&quot;/>) disponibili nel modello e-mail.&#42;

**[!UICONTROL Indirizzo e-mail del mittente/destinatario]**: seleziona la **[!UICONTROL Letterale]** per specificare manualmente un indirizzo e-mail o selezionare **[!UICONTROL Recupera dai metadati del flusso di lavoro]** per recuperare l’indirizzo e-mail da una proprietà di metadati. È inoltre possibile specificare un elenco di matrici di proprietà dei metadati per **[!UICONTROL Recupera dai metadati del flusso di lavoro]** opzione. Seleziona la **[!UICONTROL Variabile]** per recuperare l&#39;indirizzo di posta elettronica dal valore memorizzato in una variabile di tipo di dati string.

* **[!UICONTROL File allegato]**: la risorsa disponibile nella posizione specificata viene allegata all’e-mail. Il percorso della risorsa può essere relativo al payload o al percorso assoluto. Un esempio di percorso è [Payload_Directory]/attachments/.

Seleziona la **[!UICONTROL Variabile]** per recuperare il file allegato memorizzato in una variabile di tipo Documento, XML o JSON.

**[!UICONTROL Nome file]**: nome del file allegato e-mail. Il passaggio E-mail modifica il nome file originale dell’allegato con il nome file specificato. Il nome può essere specificato manualmente o recuperato da una proprietà o variabile di metadati del flusso di lavoro. Utilizza il **[!UICONTROL Letterale]** quando si conosce il valore esatto da specificare. Utilizza il **[!UICONTROL Variabile]** per recuperare il nome del file dal valore memorizzato in una variabile di tipo di dati string. Utilizza il **[!UICONTROL Recuperare da un flusso di lavoro Metadati]** quando il valore da utilizzare viene salvato in una proprietà dei metadati di un flusso di lavoro.

## Passaggio Genera documento di record {#generate-document-of-record-step}

Quando un modulo viene compilato o inviato, è possibile conservarne una registrazione, in formato cartaceo o in formato documento. Questo record è denominato documento record (DoR). È possibile utilizzare il passaggio Genera documento di record per creare una versione PDF interattiva o di sola lettura di un modulo adattivo. La versione PDF contiene informazioni inserite nel modulo insieme al layout del modulo adattivo.

Il passaggio Documento record presenta le seguenti proprietà:

**[!UICONTROL Usa modulo adattivo]**: specifica il metodo per individuare il modulo adattivo di input. Puoi utilizzare il modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile del tipo di dati String per specificare il percorso in **[!UICONTROL Seleziona variabile da risolvere]** campo.\
È possibile associare più Forms adattivi a un flusso di lavoro. Di conseguenza, puoi specificare un modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

**[!UICONTROL Percorso modulo adattivo]**: specifica il percorso del modulo adattivo. Il campo è disponibile quando selezioni il **[!UICONTROL Disponibile in un percorso assoluto]** opzione dalla **[!UICONTROL Usa modulo adattivo]** campo.

**[!UICONTROL Seleziona dati di input tramite]**: percorso dei dati di input per il modulo adattivo. È possibile mantenere i dati in una posizione relativa al payload, specificare un percorso assoluto dei dati o recuperare i dati memorizzati in una variabile di tipo Documento, JSON o XML. I dati di input vengono uniti al modulo adattivo per creare un documento di record.

**[!UICONTROL Seleziona il percorso dell&#39;allegato di input tramite]**: percorso degli allegati. Questi allegati sono inclusi nel documento di record. È possibile mantenere gli allegati in una posizione relativa al payload, specificare un percorso assoluto degli allegati o recuperare gli allegati memorizzati in una variabile di matrice di tipo dati Documento.

Se si specifica il percorso di una cartella, ad esempio gli allegati, tutti i file direttamente disponibili nella cartella vengono allegati al documento di record. Se nelle cartelle sono disponibili file direttamente disponibili nel percorso di allegato specificato, tali file vengono inclusi nel documento di record come allegati. Se sono presenti cartelle in cartelle direttamente disponibili, queste vengono ignorate.

**[!UICONTROL Salva documento di record generato tramite le opzioni di seguito]**: specifica il percorso in cui mantenere un file del documento di record. Puoi scegliere di sovrascrivere la cartella del payload, collocare il documento di record in una posizione all’interno della directory del payload o archiviare il documento di record in una variabile di tipo dati Documento.

**[!UICONTROL Lingua]**: specifica la lingua del documento record. Seleziona **[!UICONTROL Letterale]** per selezionare le impostazioni locali da un elenco a discesa o selezionare **[!UICONTROL Variabile]** per recuperare le impostazioni locali dal valore memorizzato in una variabile di tipo stringa. Definisci il codice locale durante la memorizzazione del valore della lingua in una variabile. Ad esempio, specifica **en_US** per inglese e **fr_FR** per il francese.

## Richiama passaggio DDX {#invokeddx}

Document Description XML (DDX) è un linguaggio di markup dichiarativo i cui elementi rappresentano blocchi predefiniti di documenti. Questi blocchi predefiniti includono documenti PDF e XDP e altri elementi quali commenti, segnalibri e testo con stili. DDX definisce un set di operazioni che possono essere applicate a uno o più documenti di input per generare uno o più documenti di output. Un singolo DDX può essere utilizzato con una serie di documenti sorgente. È possibile utilizzare ***Richiama passaggio DDX*** in un flusso di lavoro AEM per eseguire varie operazioni, come assemblaggio e disassemblaggio di documenti, creazione e modifica di Acrobat e XFA Forms e altre descritte nella [Documentazione di riferimento DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

Il passaggio Richiama DDX ha le seguenti proprietà:

**[!UICONTROL Documenti di input]**: utilizzato per impostare le proprietà di un documento di input. Le opzioni disponibili in questa scheda sono:
* **[!UICONTROL Specifica DDX tramite]**: specifica il documento di input relativo al payload, dispone di un percorso assoluto, può essere fornito come payload o memorizzato in una variabile di tipo dati Documento.
* **[!UICONTROL Crea mappa da payload]**: aggiungi tutti i documenti nella cartella del payload alla mappa del documento di input per l’API di richiamo nell’Assembler. Il nome del nodo di ciascun documento viene utilizzato come chiave nella mappa.
* **[!UICONTROL Mappa del documento di input]**: l’opzione viene utilizzata per aggiungere più voci utilizzando **[!UICONTROL AGGIUNGI]** pulsante. Ogni voce rappresenta la chiave del documento nella mappa e l&#39;origine del documento.

**[!UICONTROL Opzioni di ambiente]**: questa opzione viene utilizzata per impostare le impostazioni di elaborazione per l’API di chiamata. Le opzioni disponibili in questa scheda sono:
* **[!UICONTROL Solo convalida]**: verifica la validità del documento DDX di input.
* **[!UICONTROL Non riuscito in caso di errore]**: valore booleano per indicare se il servizio Richiama API non riesce, in caso di errore o meno. Per impostazione predefinita, il relativo valore è impostato su False.
* **[!UICONTROL Primo numero di Bates]**: specifica il numero, con incremento automatico. Questo numero con incremento automatico viene visualizzato automaticamente su ogni pagina consecutiva.
* **[!UICONTROL Stile predefinito]**: imposta lo stile predefinito per il file di output.

>[!NOTE]
>
>Le opzioni dell’ambiente sono mantenute sincronizzate con le API HTTP.

**[!UICONTROL Documenti di output]**: specifica il percorso in cui salvare il file di output. Le opzioni disponibili in questa scheda sono:
* **[!UICONTROL Salva output nel payload]**: salva i documenti di output nella cartella del payload o sovrascrive il payload, nel caso in cui il payload sia un file.
* **[!UICONTROL Mappa del documento di output]**: specifica la posizione in cui salvare in modo esplicito ogni file di documento, aggiungendo una voce per documento. Ogni voce rappresenta il documento e la posizione in cui salvarlo. Se sono presenti più documenti di output, viene utilizzata questa opzione.

## Passaggio del servizio Richiama modello dati modulo {#invoke-form-data-model-service-step}

È possibile utilizzare [[!DNL AEM Forms] Integrazione dei dati](data-integration.md) per configurare e connettersi a diverse origini dati. Queste origini dati possono essere un servizio web, un servizio REST, un servizio OData e una soluzione CRM. [!DNL AEM Forms] L’integrazione dei dati consente di creare un modello di dati modulo che include vari servizi per eseguire operazioni di recupero, aggiunta e aggiornamento dei dati sul database configurato. È possibile utilizzare **[!UICONTROL Passaggio Richiama servizio modello dati]** per selezionare un modello di dati modulo (FDM) e utilizzare i servizi di FDM per recuperare, aggiornare o aggiungere dati per origini dati diverse.

Per spiegare gli input per i campi del passaggio, vengono utilizzati, ad esempio, la seguente tabella di database e il seguente file JSON:

**[!UICONTROL Tabella CustomerDetails di esempio]**

<table>
 <tbody> 
  <tr> 
   <td>Proprietà</td> 
   <td>Valore<br /> </td> 
  </tr> 
  <tr> 
   <td>Nome<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>Cognome</td> 
   <td>Rosa</td> 
  </tr> 
  <tr> 
   <td>ID cliente</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>Indirizzo e-mail<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**[!UICONTROL File JSON di esempio]**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

Il passaggio Richiama servizio modello dati modulo presenta i campi elencati di seguito per facilitare le operazioni del modello dati modulo:

* **[!UICONTROL Titolo]**: titolo del passaggio. Consente di identificare i passaggi nell’editor del flusso di lavoro.
* **[!UICONTROL Descrizione]**: spiegazione utile per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

* **[!UICONTROL Percorso modello dati modulo]**: sfoglia e seleziona un modello dati modulo presente sul server.

* **[!UICONTROL Errori e convalide]**: l’opzione ti consente di acquisire i messaggi di errore e specificare le opzioni di convalida per i dati recuperati e inviati alle origini dati. Con queste modifiche, puoi garantire che i dati passati al passaggio Richiama servizio modello dati modulo siano conformi ai vincoli di dati definiti dall’origine dati. Per ulteriori dettagli, consulta [Convalida automatica dei dati di input](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL Livello di convalida]**: sono disponibili tre categorie di convalide: Base, Completo e Disattivato:

   * Completo: tutti i vincoli vengono convalidati.
   * Di base: solo i vincoli obbligatori e nullable
   * OFF: non viene eseguita alcuna convalida.

* **[!UICONTROL Termina flusso di lavoro in caso di errore]**: quando un vincolo non viene convalidato, il flusso di lavoro viene interrotto.

* **[!UICONTROL Memorizza codice errore in variabile]**: puoi memorizzare un codice di errore in un [Variabile di tipo stringa](variable-in-aem-workflows.md).

* **[!UICONTROL Memorizza messaggio di errore in variabile]**: puoi memorizzare un messaggio di errore in un [Variabile di tipo stringa](variable-in-aem-workflows.md).

* **[!UICONTROL Memorizza dettagli errore in variabile]**: puoi memorizzare i dettagli di un errore in una [Variabile di tipo JSON](variable-in-aem-workflows.md).

* **[!UICONTROL Servizio]**: elenco dei servizi forniti dal modello dati modulo selezionato.
* **[!UICONTROL Input per servizi]** > **[!UICONTROL Fornisci dati di input utilizzando metadati letterali, variabili o del flusso di lavoro e un file JSON]**: un servizio può avere più argomenti. Seleziona l’opzione per ottenere il valore degli argomenti del servizio da una proprietà di metadati del flusso di lavoro, da un oggetto JSON, da una variabile o inserisci direttamente il valore nella casella di testo fornita:

   * **[!UICONTROL Letterale]**: utilizza l’opzione quando conosci il valore esatto da specificare. Ad esempio, srose@we.info.
   * **[!UICONTROL Variabile]**: utilizza l’opzione per recuperare il valore memorizzato in una variabile.
   * **[!UICONTROL Recupera dai metadati del flusso di lavoro]**: utilizza l’opzione quando il valore da utilizzare viene salvato in una proprietà di metadati del flusso di lavoro. Ad esempio, emailAddress.

   * **[!UICONTROL Relativo al payload]**: utilizza l’opzione per recuperare il file allegato salvato in un percorso relativo al payload. Selezionare l&#39;opzione e specificare il nome della cartella che include il file allegato oppure specificare il nome del file allegato nella casella di testo.

     Ad esempio, se la cartella relativa al payload nell’archivio CRX include un file allegato in corrispondenza di `attachment\attachment-folder` posizione, specificare `attachment\attachment-folder` nella casella di testo dopo aver selezionato **[!UICONTROL Relativo al payload]** opzione.

   * **[!UICONTROL Notazione in punti JSON]**: utilizza l’opzione quando il valore da utilizzare si trova in un file JSON. Ad esempio, insurance.customerDetails.emailAddress. L’opzione JSON Dot Notation è disponibile solo se è selezionata l’opzione Mappa campi di input dall’opzione JSON di input.
   * **[!UICONTROL Mappa i campi di input da JSON di input]**: specifica il percorso di un file JSON per ottenere il valore di input di alcuni argomenti del servizio dal file JSON. Il percorso del file JSON può essere relativo al payload, un percorso assoluto oppure puoi selezionare un documento JSON di input utilizzando una variabile di tipo JSON o Modello dati modulo.

* **[!UICONTROL Input per servizi]** > **[!UICONTROL Fornisci dati di input utilizzando una variabile o un file JSON]**: seleziona l’opzione per ottenere valori per tutti gli argomenti da un file JSON salvato in un percorso assoluto, in un percorso relativo al payload o in una variabile.
* **[!UICONTROL Seleziona documento JSON di input tramite]**: file JSON contenente i valori per tutti gli argomenti del servizio. Il percorso del file JSON può essere **[!UICONTROL relativo al payload]** o un **[!UICONTROL percorso assoluto]**. Puoi anche recuperare il documento JSON di input utilizzando una variabile di tipo di dati JSON o Modello dati modulo.

* **[!UICONTROL Notazione in punti JSON]**: lascia vuoto il campo per utilizzare tutti gli oggetti del file JSON specificato come input per gli argomenti del servizio. Per leggere un oggetto JSON specifico dal file JSON specificato come input per gli argomenti del servizio, specifica la notazione del punto per l’oggetto JSON. Ad esempio, se disponi di un JSON simile a quello elencato all’inizio della sezione, specifica insurance.customerDetails per fornire tutti i dettagli di un cliente come input per il servizio.
* **[!UICONTROL Produzione del servizio]** > **[!UICONTROL Associa e scrivi i valori di output in una variabile o nei metadati]**: seleziona l’opzione per salvare i valori di output come proprietà del nodo di metadati dell’istanza del flusso di lavoro in crx-repository. Specifica il nome della proprietà dei metadati e seleziona l’attributo di output del servizio corrispondente da mappare con la proprietà dei metadati. Ad esempio, mappa phone_number restituito dal servizio di output con la proprietà phone_number dei metadati del flusso di lavoro. Allo stesso modo, puoi memorizzare l’output in una variabile di tipo dati Long. Quando selezioni una proprietà per **[!UICONTROL Attributo di output del servizio da mappare]** , solo le variabili in grado di memorizzare i dati della proprietà selezionata vengono compilate per **[!UICONTROL Salva l’output in]** opzione.

* **[!UICONTROL Produzione del servizio]** > **[!UICONTROL Salva l’output in una variabile o in un file JSON]**: seleziona l’opzione per salvare i valori di output in un file JSON in un percorso assoluto, in un percorso relativo al payload o in una variabile.
* **[!UICONTROL Salva documento JSON di output tramite le opzioni di seguito]**: salva il file JSON di output. Il percorso del file JSON di output può essere relativo al payload o a un percorso assoluto. Puoi anche salvare il file JSON di output utilizzando una variabile di tipo di dati JSON o Modello dati modulo.



## Passaggio Firma documento {#sign-document-step}

<span class="preview"> I ruoli dei firmatari, la traccia di audit e le opzioni di autenticazione basata su documento ufficiale nel passaggio di Adobe Sign sono funzioni pre-release e accessibili tramite [canale preliminare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

Il passaggio Firma documento consente di utilizzare [!DNL Adobe Sign] per firmare i documenti. Quando si utilizza [!DNL Adobe Sign] Passaggio del flusso di lavoro per firmare un modulo adattivo, il modulo può essere trasmesso tra i destinatari uno dopo l’altro o può essere inviato a tutti i destinatari contemporaneamente, a seconda della configurazione del passaggio del flusso di lavoro. [!DNL Adobe Sign] Forms adattivo abilitato vengono inviati a Experience Manager Forms Server solo dopo che tutti i destinatari hanno completato il processo di firma.

Per impostazione predefinita, il [!DNL Adobe Sign] Il servizio di pianificazione controlla (esegue il polling) la risposta del destinatario ogni 24 ore. È possibile [modificare l’intervallo predefinito per l’ambiente](adobe-sign-integration-adaptive-forms.md#for-aem-workflows-only-configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status-configure-adobe-sign-scheduler-to-sync-the-signing-status).

Il passaggio Firma documento presenta le seguenti proprietà:

* **[!UICONTROL Nome contratto]**: specifica il titolo del contratto. Il nome del contratto diventa parte dell’oggetto e del corpo del testo dell’e-mail inviata ai firmatari. È possibile memorizzare il nome in una variabile di tipo di dati String oppure selezionare **[!UICONTROL Letterale]** per aggiungere manualmente il nome.

* **[!UICONTROL Lingua]**: specifica la lingua per le opzioni e-mail e verifica. È possibile archiviare le impostazioni locali in una variabile di tipo String oppure selezionare **[!UICONTROL Letterale]** per scegliere le impostazioni locali dall&#39;elenco delle opzioni disponibili. È necessario definire il codice delle impostazioni locali durante la memorizzazione del valore relativo in una variabile. Ad esempio, specifica **[!UICONTROL en_US]** per inglese e **[!UICONTROL fr_FR]** per il francese.

* **[!UICONTROL Configurazione cloud Adobe Sign]**: scegli un [!DNL Adobe Sign] Configurazione cloud. Se non hai configurato [!DNL Adobe Sign] per [!DNL AEM Forms], vedi [Integrare Adobe Sign con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL Seleziona documento da firmare tramite]**: puoi scegliere un documento da una posizione relativa al payload, utilizzare il payload come documento, specificare un percorso assoluto del documento o recuperare il documento memorizzato in una variabile di tipo dati Documento.
* **[!UICONTROL Giorni mancanti alla scadenza]**: un documento viene contrassegnato come dovuto (scadenza passata) dopo che non è presente alcuna attività sull’attività per il numero di giorni specificato in **[!UICONTROL Giorni mancanti alla scadenza]** campo. Il numero di giorni viene conteggiato dopo che la documentazione è stata assegnata a un utente per la firma.
* **[!UICONTROL Frequenza e-mail promemoria]**: puoi inviare un’e-mail di promemoria a intervalli giornalieri o settimanali. La settimana viene conteggiata dal giorno in cui la documentazione viene assegnata a un utente per la firma.
* **[!UICONTROL Processo di firma]**: puoi scegliere di firmare un documento in ordine sequenziale o parallelo. In ordine sequenziale, un firmatario riceve il documento alla volta per la firma. Dopo che il primo firmatario ha completato la firma del documento, questo viene inviato al secondo firmatario e così via. In ordine parallelo, più firmatari possono firmare un documento alla volta.
* **[!UICONTROL URL di reindirizzamento]**: specifica un URL di reindirizzamento. Dopo aver firmato il documento, puoi reindirizzare l’assegnatario a un URL. Di solito, questo URL contiene un messaggio di ringraziamento o ulteriori istruzioni.
* **[!UICONTROL Fase flusso di lavoro]**: un flusso di lavoro può avere più fasi. Questi stadi vengono visualizzati nella casella in entrata AEM. Potete definire questi stadi nelle proprietà del modello ( **[!UICONTROL Sidekick]** > **[!UICONTROL Pagina]** > **[!UICONTROL Proprietà pagina]** > **[!UICONTROL Fasi]**).
* **[!UICONTROL Seleziona destinatari]**: specifica il metodo di scelta dei destinatari del documento. Puoi assegnare dinamicamente il flusso di lavoro a un utente o a un gruppo oppure aggiungere manualmente i dettagli di un destinatario. Quando selezioni Manualmente nel menu a discesa, aggiungi i dettagli del destinatario come E-mail, Ruolo e Metodo di autenticazione.

  >[!NOTE]
  >
  >* Nella sezione Ruolo è possibile specificare il ruolo del destinatario come Firmatario, Approvatore, Accettatore, Destinatario certificato, Form Filler e Delegatore.
  >* Se si seleziona Delegante nell&#39;opzione Ruolo, il Delegante può assegnare l&#39;attività di firma a un altro destinatario.
  >* Se hai configurato un metodo di autenticazione per [!DNL Adobe Sign], in base alla configurazione, seleziona un metodo di autenticazione come l’autenticazione basata su telefono, l’autenticazione basata su identità social, l’autenticazione basata su conoscenza, l’autenticazione basata su identità governativa.

* **[!UICONTROL Script o servizio per selezionare i destinatari]**: l’opzione è disponibile solo se hai selezionato l’opzione Dinamicamente nel campo Seleziona destinatari. È possibile specificare un codice ECMAScript o un servizio per scegliere i firmatari e le opzioni di verifica per un documento.
* **[!UICONTROL Dettagli destinatario]**: l’opzione è disponibile solo se l’opzione Manualmente è selezionata nel campo Seleziona destinatari. Specifica un indirizzo e-mail e scegli un meccanismo di verifica opzionale. Prima di selezionare un meccanismo di verifica in due fasi, assicurati che l’opzione di verifica corrispondente sia abilitata per il [!DNL Adobe Sign] account. Puoi utilizzare una variabile di tipo stringa per definire i valori per i campi E-mail, Codice paese e Numero di telefono. I campi Codice paese e Numero di telefono vengono visualizzati solo se si seleziona Verifica telefono dall&#39;elenco a discesa Verifica in due passaggi.
* **[!UICONTROL Documento firmato]**: è possibile salvare lo stato del documento firmato in Variabile. Per aggiungere una traccia di controllo della firma elettronica per una maggiore sicurezza e legalità al documento firmato, è possibile includere un rapporto di controllo. È possibile salvare il documento firmato utilizzando la cartella Variabile o Payload.

  >[!NOTE]
  >
  > Il rapporto di audit viene aggiunto all&#39;ultima pagina del documento firmato.

<!--
## Document Services steps {#document-services-steps}

AEM Document services are a set of services for creating, assembling, and securing PDF Documents. [!DNL AEM Forms] provides a separate AEM Workflow step for each document service.

Similar to other [!DNL AEM Forms] workflow steps, such as Assign Task, Send Email, and Sign Document, you can use variables in all AEM Document services steps. For more information on creating and managing variables, see [Variables in AEM workflows](variable-in-aem-workflows.md).
 
### Apply Document Time Stamp step {#apply-document-time-stamp-step}

Add time stamp to a document. You provide document details such as input document path, input document name, location to store exported data. You may choose to overwrite existing payload file, choose a different file name to store data in a different file under payload folder, provide an absolute path to the data, or store data in a variable of Document data type.

### Convert to image step {#convert-to-image-step}

Converts a PDF document to list of images. Supported image formats are JPEG, JPEG2000, PNG, and TIFF. The following information applies to conversions to TIFF images:

* A multi-page TIFF file is generated.
* Some annotations are not included in TIFF images. Annotations that require Acrobat to generate their appearance are not included.

### Convert to PDF/A step {#convert-to-pdf-a-step}

Converts a PDF document to PDF/A format using the options provided. The PDF/A version of Portable Document Format (PDF) is specialized for archiving and long-term preservation of documents.

### Convert to PS step {#convert-to-ps-step}

Convert PDF documents to PostScript. When converting to PostScript, you can use the conversion operation to specify the source document and whether to convert to PostScript level 2 or 3. The PDF document you convert to a PostScript file must be non-interactive.

### Create PDF from specified type step {#create-pdf-from-specified-type-step}

Generate a PDF document from an input file. The input document can be relative to the payload, have an absolute path, can be payload itself, or stored in a variable of Document data type.

### Create PDF from URL/HTML/ZIP step {#create-pdf-from-url-html-zip-step}

Generates a PDF document from supplied URL, HTML, and ZIP file.

### Export Data step {#export-data-step}

Exports data from a PDF forms or XDP file. It requires you to enter the file path of Input Document and the Export Data Format. The options for Export Data Format are Auto, XDP and XmlData.

### Export PDF to specified type step {#export-pdf-to-specified-type-step}

Converts a PDF document to a selected format.

### Generate Non-Interactive PDF step {#generatenoninteractive}

Generate a Non-Interactive PDF. It provides various customization options.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Import Data step {#import-data-step}

Merges form data into a PDF form. You can import form data into a PDF form.

### Invoke DDX step {#invokeddx}

Executes the DDX file on the specified map of input documents and returns the manipulated PDF documents.

>[!NOTE]
>
>You can use variables to specify the DDX file for input documents. Store the DDX file in a variable of Document or XML data type.

### Optimize PDF step {#optimize-pdf-step}

Optimizes PDF files by reducing their size. The result of this conversion is PDF files that may be smaller than their original versions. This operation also converts PDF documents to the PDF version specified in the optimization parameters.

Optimization settings specify how files are optimized. Here are example settings:

* Target PDF version
* Discarding objects such as JavaScript actions and embedded page thumbnails
* Discarding user data such as comments and file attachments
* Discarding invalid or unused settings
* Compressing uncompressed data or using more efficient compression algorithms
* Removing embedded fonts
* Setting transparency values

### Render PDF Form step {#renderpdf}

Renders a form created in Form Designer (XDP) to a PDF form.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Secure Document step {#secure-document-step}

Encrypt, Sign, and certify a document. [!DNL AEM Forms] supports both password based and certificate base encryption. You can also choose between various algorithms for signing documents. For example, SHA-256 and SH-512. You can also use the workflow step to reader extend PDF documents. The workflow step provides option to enable barcode decoding, digital signatures, import and export of PDF data, and other options.

### Send to Printer step {#send-to-printer-step}

Send a document directly to a printer. It supports the following printing access mechanisms:

* **[!UICONTROL Direct accessible printer]**: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX&reg; printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server's IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.
    -->

## Genera passaggio di output stampato {#generatePrintedOutput}

Il passaggio genera un output PCL, PostScript, ZPL, IPL, TPCL o DPL in base a un progetto di modulo e a un file di dati. Il file di dati viene unito alla struttura del modulo e formattato per la stampa. L&#39;output generato da questo passaggio può essere inviato direttamente a una stampante o salvato come file. È consigliabile utilizzare questo passaggio quando si desidera utilizzare le progettazioni dei moduli o i dati di un&#39;applicazione. Se le progettazioni dei moduli si trovano in rete, nel file system locale o in una posizione HTTP, utilizzare l&#39;operazione generatePrintedOutput.

Ad esempio, l&#39;applicazione richiede l&#39;unione di una struttura di modulo con un file di dati. I dati contengono centinaia di record. Inoltre, è necessario che l&#39;output venga inviato a una stampante che supporta ZPL. La struttura del modulo e i dati di input sono inclusi in un&#39;applicazione. Utilizzare l&#39;operazione generatePrintedOutput per unire ogni record con una struttura di modulo e inviare l&#39;output a una stampante che supporta ZPL.

Il passaggio Genera output stampato ha le seguenti proprietà:

**[!UICONTROL Proprietà di input]**

* **[!UICONTROL Seleziona file modello tramite]**: specifica il percorso del file modello. Puoi selezionare il file modello utilizzando il percorso relativo al payload, salvato in un percorso assoluto oppure utilizzando una variabile di tipo dati Documento. Ad esempio: [Payload_Directory]/Workflow/data.xml. Se il percorso non esiste in crx-repository, un amministratore può crearlo prima di utilizzarlo. Inoltre, puoi anche accettare il payload come file di dati di input.

* **[!UICONTROL Seleziona documento dati tramite]**: specifica il percorso di un file di dati di input. Puoi selezionare il file di dati di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto oppure utilizzando una variabile di tipo dati Documento. Ad esempio: [Payload_Directory]/Workflow/data.xml. Se il percorso non esiste in crx-repository, un amministratore può crearlo prima di utilizzarlo.

* **[!UICONTROL Formato stampante]**: valore di Formato di stampa che specifica la lingua di descrizione della pagina da utilizzare, quando non viene fornito un file XDC, per generare il flusso di output. Se fornisci un valore letterale, seleziona uno dei seguenti valori:

   * **[!UICONTROL PCL colore]**: utilizza l’opzione per specificare un file XDC per PCL.
   * **[!UICONTROL PostScript generico]**: utilizza l’opzione per specificare un file XDC generico per PostScript.
   * **[!UICONTROL ZPL 300 DPI]**: utilizzare ZPL 300 DPI. Viene utilizzato zpl300.xdc.
   * **[!UICONTROL ZPL 600 DPI]**: utilizzare ZPL 600 DPI. Viene utilizzato il file zpl600.xdc.
   * **[!UICONTROL IPL 300 DPI]**: utilizza IPL 300 DPI. Viene utilizzato ipl300.xdc.
   * **[!UICONTROL IPL 400 DPI]**: utilizza IPL 400 DPI. Viene utilizzato il file ipl400.xdc.
   * **[!UICONTROL TPCL 600 DPI]**: utilizza TPCL 600 DPI. Viene utilizzato il file tpcl600.xdc.
   * **[!UICONTROL PostScript normale]**: utilizza l’opzione per specificare un file XDC in testo normale per PostScript.
   * **[!UICONTROL DPL300DPI]**: utilizzare DPL 300 DPI. Viene utilizzato dpl300.xdc.
   * **[!UICONTROL DPL400DPI]**: utilizzare DPL 400 DPI. Viene utilizzato dpl400.xdc.
   * **[!UICONTROL DPL600DPI]**: utilizzare DPL 600 DPI. Viene utilizzato dpl600.xdc.
   * **[!UICONTROL HP_PCL_5e]**: utilizza l’opzione per supportare più dispositivi Canon.


**[!UICONTROL Proprietà di output]**

* **[!UICONTROL Salva documento di output tramite]**: specifica il percorso in cui salvare il file di output. Puoi salvare il file di output in una posizione relativa al payload, in una variabile, oppure specificare una posizione assoluta per salvare il file di output. Se il percorso non esiste in crx-repository, un amministratore può crearlo prima di utilizzarlo.

**[!UICONTROL Proprietà avanzate]**

* **[!UICONTROL Seleziona posizione principale contenuto tramite]**: radice del contenuto è un valore stringa che specifica l’URI, il riferimento assoluto o la posizione nell’archivio per recuperare le risorse relative utilizzate dalla progettazione del modulo. Ad esempio, se la progettazione del modulo fa riferimento a un’immagine relativamente, ad esempio `../myImage.gif`, `myImage.gif` deve essere in `repository://`. Il valore predefinito è `repository://`, che punta al livello principale dell’archivio.

  Quando scegli una risorsa dall’applicazione, il percorso URI della directory principale del contenuto deve avere la struttura corretta. Ad esempio, se un modulo viene selezionato da un’applicazione denominata SampleApp e viene posizionato in `SampleApp/1.0/forms/Test.xdp`, l&#39;URI radice del contenuto deve essere specificato come `repository://administrator@password/Applications/SampleApp/1.0/forms/`, o `repository:/Applications/SampleApp/1.0/forms/` (quando l&#39;autorità è nulla). Quando l’URI della directory principale del contenuto viene specificato in questo modo, i percorsi di tutte le risorse a cui si fa riferimento nel modulo vengono risolti in base a questo URI.

* **[!UICONTROL Seleziona file XCI tramite]**: i file XCI vengono utilizzati per descrivere i font e altre proprietà utilizzati per gli elementi di progettazione dei moduli. È possibile mantenere un file XCI relativo al payload, in un percorso assoluto o utilizzando una variabile di tipo dati Documento.

* **[!UICONTROL Lingua]**: specifica la lingua utilizzata per generare il documento PDF. Se fornisci un valore letterale, seleziona una lingua dall’elenco o scegli uno dei seguenti valori:
   * **[!UICONTROL Per utilizzare il server predefinito]**: (impostazione predefinita) utilizza l’impostazione Locale configurata sul [!DNL AEM Forms] Server. L&#39;impostazione Locale viene configurata utilizzando la console di amministrazione. (vedere [Guida di Designer](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf).)

   * **[!UICONTROL Per utilizzare un valore personalizzato]**: digita il codice locale nella casella letterale o seleziona una variabile stringa contenente il codice locale. Per un elenco completo dei codici delle impostazioni internazionali supportati, vedere https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copie]**: valore intero che specifica il numero di copie da generare per l’output. Il valore predefinito è 1.

* **[!UICONTROL Stampa fronte retro]**: valore di impaginazione che specifica se utilizzare la stampa fronte/retro o fronte/retro. Le stampanti che supportano PostScript e PCL utilizzano questo valore. Se fornisci un valore letterale, seleziona uno dei seguenti valori:
   * **[!UICONTROL Bordo lungo fronte-retro]**: utilizza la stampa fronte/retro e la stampa con impaginazione a lungo termine.
   * **[!UICONTROL Bordo corto fronte-retro]**: utilizza la stampa fronte/retro e la stampa con impaginazione lato corto.
   * **[!UICONTROL Simplex]**: stampa fronte/retro.

## Genera passaggio di output PDF non interattivo   {#generatePDFdocuments}

1. Trascina il flusso di lavoro Genera output PDF non interattivo nella scheda Forms Workflow in Sidekick.
1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente configura i documenti di input, i documenti di output e i parametri aggiuntivi, quindi fai clic su **[!UICONTROL OK]**.

### Documenti di input {#input-documents-3}

* **File modello**: specifica la posizione del modello XDP. È un campo obbligatorio.

* **Documento dati**: specifica la posizione dell&#39;xml dati da unire al modello.

### Documento di output {#output-document}

**Documento di output**: specifica il nome del modulo PDF generato.

### Parametri aggiuntivi {#additional-parameters-1}

* **Directory principale contenuto**: specifica il percorso della cartella nell’archivio in cui vengono memorizzati i frammenti o le immagini utilizzati nel modello XDP di input.
* **Lingua**: specifica le impostazioni locali predefinite per il modulo PDF generato.
* **Versione Acrobat**: specifica la versione di Acrobat di destinazione per il modulo PDF generato.
* **Linearized PDF**: specifica se ottimizzare il PDF generato per la visualizzazione Web.
* **PDF con tag**: specifica se rendere accessibile il PDF generato.
* **Documento XCI**: specifica il percorso del file XCI.
