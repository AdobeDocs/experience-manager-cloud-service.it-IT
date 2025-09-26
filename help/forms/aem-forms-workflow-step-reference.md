---
title: Quali passaggi del flusso di lavoro sono disponibili in AEM Forms Cloud Service per la creazione di un flusso di lavoro o per l’automazione dei processi aziendali (BPM, Business Process Automation)?
description: I flussi di lavoro incentrati su Forms consentono di creare rapidamente flussi di lavoro adattivi basati su Forms. Puoi utilizzare Adobe Sign per firmare documenti tramite e-sign, creare processi aziendali basati su moduli, recuperare e inviare dati a più origini dati e inviare notifiche e-mail
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
keywords: 'Utilizza i flussi di lavoro di AEM: assegna passaggi di un’attività, converti in un passaggio PDF/A, Genera un documento del passaggio registrato, Utilizza flussi di lavoro, Firma il passaggio del documento, Genera un passaggio di output stampato, Genera un output PDF non interattivo'
feature: Adaptive Forms, Workflow
role: Admin, User
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '7409'
ht-degree: 0%

---


# Utilizzare flussi di lavoro AEM incentrati su Forms: riferimento ai passaggi per automatizzare i processi aziendali {#forms-centric-workflow-on-osgi-step-reference}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Si utilizzano i modelli di flusso di lavoro. Un modello consente di definire ed eseguire una serie di passaggi. Puoi anche definire le proprietà del modello, ad esempio se il flusso di lavoro è transitorio o utilizza più risorse. Puoi [includere vari passaggi del flusso di lavoro di AEM in un modello per ottenere la regola business](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=it#extending-aem).

## Passaggi incentrati su Forms {#forms-workflow-steps}

I passaggi del flusso di lavoro incentrati su Forms eseguono operazioni specifiche per AEM Forms in un flusso di lavoro AEM. Questi passaggi consentono di creare rapidamente un flusso di lavoro adattivo basato su Forms basato su Forms su OSGi. Questi flussi di lavoro possono essere utilizzati per sviluppare flussi di lavoro di revisione e approvazione di base, interni e attraverso il firewall. Puoi anche utilizzare i passaggi di Forms Workflow per:

* Crea processi aziendali, flussi di lavoro successivi all’invio e flussi di lavoro back-end per gestire i processi di iscrizione.

* Crea e assegna attività a un utente o a un gruppo.

* Utilizza [!DNL Adobe Sign] in un flusso di lavoro AEM per inviare un documento per la firma.

* Genera un documento di record su richiesta o all’invio di un modulo.

* Collega un modello di flusso di lavoro con diverse origini dati per salvare e recuperare facilmente i dati.

* Utilizza il passaggio e-mail per inviare e-mail di notifica e altri allegati al completamento di un’azione e all’inizio o al completamento di un flusso di lavoro.

>[!NOTE]
>
>Se il modello di flusso di lavoro è contrassegnato per un archivio esterno, per tutti i passaggi di Forms Workflow è possibile selezionare solo l&#39;opzione della variabile per memorizzare o recuperare file di dati e allegati.

## Assegna passaggio attività {#assign-task-step}

Il passaggio Assegna attività crea un elemento di lavoro e lo assegna a un utente o a un gruppo. Oltre all’assegnazione dell’attività, il componente specifica anche il Modulo adattivo o il PDF non interattivo per l’attività. Il modulo adattivo è necessario per accettare l’input degli utenti e PDF non interattivo oppure un modulo adattivo di sola lettura viene utilizzato per i flussi di lavoro di sola revisione.

È inoltre possibile utilizzare il componente per controllare il comportamento dell&#39;attività. Ad esempio, la creazione di un documento di record automatico, l’assegnazione dell’attività a un utente o gruppo specifico, la specifica del percorso dei dati inviati, il percorso dei dati da precompilare e le azioni predefinite. Il passaggio Assegna attività presenta le seguenti proprietà:

* **[!UICONTROL Titolo]**: titolo dell&#39;attività. Il titolo viene visualizzato nella casella in entrata di AEM.
* **[!UICONTROL Descrizione]**: spiegazione delle operazioni eseguite nell&#39;attività. Queste informazioni sono utili per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

* **[!UICONTROL Percorso miniatura]**: percorso della miniatura dell&#39;attività. Se non viene specificato alcun percorso, per un modulo adattivo viene visualizzata una miniatura predefinita e per il documento di record viene visualizzata un’icona predefinita.
* **[!UICONTROL Fase flusso di lavoro]**: un flusso di lavoro può avere più fasi. Questi stadi vengono visualizzati nella casella in entrata di AEM. Potete definire questi stadi nelle proprietà del modello (Sidekick > Pagina > Proprietà pagina > Stadi).
* **[!UICONTROL Priorità]**: la priorità selezionata viene visualizzata nella cartella Posta in arrivo di AEM. Le opzioni disponibili sono Alta, Medium e Bassa. Il valore predefinito è Medium.
* **[!UICONTROL Data di scadenza]**: specificare il numero di giorni o di ore dopo le quali l&#39;attività viene contrassegnata come scaduta. Se selezioni **[!UICONTROL Disattivato]**, l&#39;attività non verrà mai contrassegnata come scaduta. È inoltre possibile specificare un gestore di timeout per eseguire attività specifiche dopo la scadenza dell&#39;attività.

* **[!UICONTROL Giorni]**: il numero di giorni prima dei quali l&#39;attività deve essere completata. Il numero di giorni viene conteggiato dopo l&#39;assegnazione dell&#39;attività a un utente. Se un’attività non è completa e supera il numero di giorni specificato nel campo Giorni, se è selezionata viene attivato un gestore di timeout dopo la data di scadenza.
* **[!UICONTROL Ore]**: il numero di ore prima delle quali l&#39;attività deve essere completata. Il numero di ore che vengono conteggiate dopo l&#39;assegnazione dell&#39;attività a un utente. Se un’attività non è completa e supera il numero di ore specificato nel campo Ore, se è selezionata, viene attivato un gestore di timeout dopo le ore dovute.
* **[!UICONTROL Timeout dopo la data di scadenza]**: selezionare questa opzione per abilitare il campo di selezione del gestore di timeout.
* **[!UICONTROL Gestore timeout]**: selezionare lo script da eseguire quando il passaggio dell&#39;attività di assegnazione supera la data di scadenza. Gli script inseriti nell&#39;archivio CRX in [apps]/fd/dashboard/scripts/timeoutHandler sono disponibili per la selezione. Il percorso specificato non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo.
* **[!UICONTROL Evidenzia l&#39;azione e il commento dall&#39;ultima attività in Dettagli attività]**: selezionare questa opzione per visualizzare l&#39;ultima azione eseguita e il commento ricevuto nella sezione dei dettagli dell&#39;attività di un&#39;attività.
* **[!UICONTROL Tipo]**: scegliere il tipo di documento da compilare all&#39;avvio del flusso di lavoro. Puoi scegliere un modulo adattivo, un modulo adattivo di sola lettura, un documento non interattivo di PDF.

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
* **[!UICONTROL Seleziona PDF di input tramite]**: specifica il percorso di un documento PDF non interattivo. Il campo è disponibile quando si sceglie un documento non interattivo di PDF nel campo Tipo. Puoi selezionare il PDF di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto oppure utilizzando una variabile di tipo dati Documento. Ad esempio, [Directory_Payload]/Workflow/PDF/credit-card.pdf. Il percorso non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo. Per utilizzare l’opzione Percorso PDF è necessario che sia abilitata l’opzione Documento di record o che sia abilitato l’opzione Adaptive Forms basato su modello di modulo.
* **[!UICONTROL Per l&#39;attività completata, esegui il rendering del modulo adattivo come]**: quando un&#39;attività è contrassegnata come completata, puoi eseguire il rendering del modulo adattivo come modulo adattivo di sola lettura o documento PDF. Per eseguire il rendering del modulo adattivo come documento record, è necessario abilitare l’opzione Documento di record o un Forms adattivo basato su modello di modulo.
* **[!UICONTROL Precompilati]**: i seguenti campi elencati di seguito fungono da input per l&#39;attività:

   * **[!UICONTROL Selezionare il file di dati di input utilizzando]**: percorso del file di dati di input (.json, .xml, .doc o modello dati modulo (FDM)). Puoi recuperare il file di dati di input utilizzando un percorso relativo al payload o recuperare il file memorizzato in una variabile di tipo Documento, XML o JSON. Il file contiene ad esempio i dati inviati per il modulo tramite un&#39;applicazione Casella in entrata AEM. Il percorso di esempio è [Payload_Directory]/workflow/data.
   * **[!UICONTROL Seleziona allegati di input tramite]**: gli allegati disponibili nel percorso sono allegati al modulo associato all&#39;attività. Il percorso può essere relativo al payload o recuperare l’allegato memorizzato in una variabile di un documento. Il percorso di esempio è [Payload_Directory]/allegati/. È possibile specificare gli allegati posizionati rispetto al payload o utilizzare una variabile di tipo documento (Elenco array > Documento) per specificare un allegato di input per il modulo adattivo.

  <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL Mappatura attributo richiesta]**: utilizzare la sezione Mappatura attributo richiesta per definire il [nome e il valore dell&#39;attributo richiesta](work-with-form-data-model.md#bindargument). Recupera i dettagli dall’origine dati in base al nome e al valore dell’attributo specificati nella richiesta. È possibile definire un valore di attributo della richiesta utilizzando un valore letterale o una variabile di tipo di dati String.

  <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL Informazioni inviate]**: i campi elencati di seguito fungono da percorsi di output per l&#39;attività:

   * **[!UICONTROL Salva file di dati di output tramite]**: salva il file di dati (.json, .xml, .doc o modello dati modulo (FDM)). Il file di dati contiene informazioni inviate tramite il modulo associato. Puoi salvare il file di dati di output utilizzando un percorso relativo al payload o memorizzarlo in una variabile di tipo Documento, XML o JSON. Ad esempio, [Payload_Directory]/Workflow/data, dove i dati sono un file.
   * **[!UICONTROL Salva allegati tramite]**: salva gli allegati del modulo forniti in un&#39;attività. È possibile salvare gli allegati utilizzando un percorso relativo al payload o memorizzarlo in una variabile dell’elenco di matrici del tipo di dati Documento.
   * **[!UICONTROL Salva documento di record tramite]**: percorso per salvare un file del documento di record. Ad esempio, [Directory_Payload]/DocumentofRecord/credit-card.pdf. Puoi salvare il documento record utilizzando un percorso relativo al payload o memorizzarlo in una variabile di tipo Dati documento. Se si seleziona l&#39;opzione **[!UICONTROL Relativo al payload]**, il documento di record non viene generato se il campo percorso viene lasciato vuoto. Questa opzione è disponibile solo se si seleziona Modulo adattivo dall’elenco a discesa Tipo.

  <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL Assegnatario]** > **[!UICONTROL Assegna opzioni]**: specifica il metodo per assegnare l&#39;attività a un utente. È possibile assegnare dinamicamente l&#39;attività a un utente o a un gruppo utilizzando lo script Selettore partecipanti oppure assegnare l&#39;attività a un utente o a un gruppo AEM specifico.
* **[!UICONTROL Selettore partecipanti]**: l&#39;opzione è disponibile quando l&#39;opzione **[!UICONTROL Assegna dinamicamente a un utente o a un gruppo]** è selezionata nel campo Assegna opzioni. È possibile utilizzare un codice ECMAScript o un servizio per selezionare dinamicamente un utente o un gruppo. Per ulteriori informazioni, vedere [Creazione di un passaggio Partecipante dinamico Adobe Experience Manager personalizzato](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it&CID=RedirectAEMCommunityKautuk).

* **[!UICONTROL Partecipanti]**: il campo è disponibile quando l&#39;opzione **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** è selezionata nel campo **[!UICONTROL Selettore partecipanti]**. Il campo consente di selezionare utenti o gruppi per l&#39;opzione RandomParticipantChooser.

* **[!UICONTROL Assegnatario]**: il campo è disponibile quando **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** è selezionato nel campo **[!UICONTROL Selettore partecipanti]**. Il campo consente di selezionare una variabile di tipo String per definire l’assegnatario.

* **[!UICONTROL Argomenti]**: il campo è disponibile quando nel campo Selettore partecipanti è selezionato uno script diverso da RandomParticipantChoose. Il campo consente di fornire un elenco di argomenti separati da virgole per lo script selezionato nel campo Selettore partecipanti.

* **[!UICONTROL Utente o gruppo]**: l&#39;attività è assegnata a un utente o gruppo selezionato. L&#39;opzione è disponibile quando l&#39;opzione **[!UICONTROL A un utente o gruppo specifico]** è selezionata nel campo **[!UICONTROL Assegna opzioni]**. Nel campo sono elencati tutti gli utenti e i gruppi del gruppo [!DNL workflow-users].\
  Il menu a discesa **[!UICONTROL Utente o Gruppo]** elenca gli utenti e i gruppi a cui l&#39;utente connesso ha accesso. La visualizzazione del nome utente dipende dalla disponibilità delle autorizzazioni di accesso per il nodo **[!UICONTROL users]** nell&#39;archivio crx per un determinato utente.

* **[!UICONTROL Invia e-mail di notifica]**: selezionare questa opzione per inviare notifiche e-mail all&#39;assegnatario. Queste notifiche vengono inviate quando un’attività viene assegnata a un utente o a un gruppo. È possibile utilizzare l&#39;opzione **[!UICONTROL Indirizzo e-mail destinatario]** per specificare il meccanismo di recupero dell&#39;indirizzo e-mail.

* **[!UICONTROL Indirizzo e-mail destinatario]**: è possibile memorizzare un indirizzo e-mail in una variabile, utilizzare un valore letterale per specificare un indirizzo e-mail permanente o utilizzare l&#39;indirizzo e-mail predefinito dell&#39;assegnatario specificato nel profilo dell&#39;assegnatario. Puoi utilizzare il letterale o una variabile per specificare l’indirizzo e-mail di un gruppo. L’opzione della variabile è utile per recuperare e utilizzare in modo dinamico un indirizzo e-mail. L&#39;opzione **[!UICONTROL Usa indirizzo e-mail predefinito dell&#39;assegnatario]** è riservata a un solo assegnatario. In questo caso, viene utilizzato l’indirizzo e-mail memorizzato nel profilo utente degli assegnatari.

* **[!UICONTROL Modello e-mail HTML]**: selezionare il modello e-mail per l&#39;e-mail di notifica. Per modificare un modello, modifica il file che si trova in /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt in crx-repository.
* **[!UICONTROL Consenti delega a]**: la Casella in entrata di AEM fornisce un&#39;opzione all&#39;utente connesso per delegare il flusso di lavoro assegnato a un altro utente. Puoi delegare all’interno dello stesso gruppo o all’utente del flusso di lavoro di un altro gruppo. Se l&#39;attività è assegnata a un singolo utente e l&#39;opzione **[!UICONTROL consenti delega ai membri del gruppo assegnatario]** è selezionata, non è possibile delegare l&#39;attività a un altro utente o gruppo.
* **[!UICONTROL Impostazioni condivisione]**: la casella in entrata di AEM fornisce le opzioni per condividere una o tutte le attività della casella in entrata con un altro utente:
   * Quando l&#39;opzione **[!UICONTROL Consenti all&#39;assegnatario di condividere in modo esplicito la cartella Posta in arrivo]** è selezionata, l&#39;utente può selezionare l&#39;attività nella cartella Posta in arrivo di AEM e condividerla con un altro utente di AEM.
   * Quando l&#39;opzione **[!UICONTROL Consenti all&#39;assegnatario di condividere tramite la condivisione della casella in entrata]** è selezionata e gli utenti condividono i propri elementi della casella in entrata o consentono ad altri utenti di accedere ai propri elementi della casella in entrata, solo le attività con l&#39;opzione precedentemente indicata abilitata vengono condivise con altri utenti.
   * Quando è selezionato **[!UICONTROL Consenti all&#39;assegnatario di delegare utilizzando le impostazioni &#39;Fuori sede&#39;]**. L’assegnatario può abilitare l’opzione per delegare l’attività ad altri utenti insieme ad altre opzioni Fuori sede. Tutte le nuove attività assegnate all&#39;utente fuori sede vengono automaticamente delegate (assegnate) agli utenti indicati nelle impostazioni fuori sede.

  Consente ad altri utenti di scegliere le attività assegnate mentre è fuori sede e non può lavorare sulle attività assegnate.

* **[!UICONTROL Azioni]** > **[!UICONTROL Azioni predefinite]**: sono disponibili le azioni Invia, Salva e Reimposta. Per impostazione predefinita, sono attivate tutte le azioni predefinite.
* **[!UICONTROL Variabile route]**: nome della variabile route. La variabile di route acquisisce le azioni personalizzate selezionate dall&#39;utente nella casella in entrata di AEM.
* **[!UICONTROL Route]**: un&#39;attività può diramarsi in route diverse. Quando è selezionata nella casella in entrata di AEM, la route restituisce un valore e i rami del flusso di lavoro si basano sulla route selezionata. È possibile archiviare le route in una variabile di matrice di tipi di dati String oppure selezionare **[!UICONTROL Letterale]** per aggiungere le route manualmente.

* **[!UICONTROL Titolo route]**: specificare il titolo della route. Viene visualizzata nella casella in entrata di AEM.
* **[!UICONTROL Icona rosso corallo]**: specificare un attributo HTML di un&#39;icona rosso corallo. La libreria CorelUI di Adobe fornisce un ampio set di icone touch-first. È possibile scegliere e utilizzare un&#39;icona per il ciclo di lavorazione. Viene visualizzato insieme al titolo nella Casella in entrata AEM. Se memorizzi le route in una variabile, le route utilizzano un&#39;icona di corallo &quot;Tag&quot; predefinita.
* **[!UICONTROL Consenti all&#39;assegnatario di aggiungere commenti]**: selezionare questa opzione per abilitare i commenti per l&#39;attività. L’assegnatario può aggiungere i commenti dalla casella in entrata di AEM al momento dell’invio dell’attività.
* **[!UICONTROL Salva commento nella variabile]**: salva il commento in una variabile di tipo dati String. Questa opzione viene visualizzata solo se si seleziona la casella di controllo **[!UICONTROL Consenti all&#39;assegnatario di aggiungere commenti]**.

* **[!UICONTROL Consenti all&#39;assegnatario di aggiungere allegati all&#39;attività]**: selezionare questa opzione per abilitare gli allegati per l&#39;attività. L’assegnatario può aggiungere gli allegati dalla casella in entrata di AEM al momento dell’invio dell’attività. È inoltre possibile limitare la dimensione massima **[!UICONTROL (Dimensione massima file)]** di un allegato. La dimensione predefinita è 2 MB.

* **[!UICONTROL Salva allegati attività di output tramite]**: specificare il percorso della cartella degli allegati. È possibile salvare gli allegati delle attività di output utilizzando un percorso relativo al payload o in una variabile di un array di tipi di dati del documento. Questa opzione viene visualizzata solo se si seleziona la casella di controllo **[!UICONTROL Consenti all&#39;assegnatario di aggiungere allegati all&#39;attività]** e si seleziona **[!UICONTROL Modulo adattivo]**, **[!UICONTROL Modulo adattivo di sola lettura]** o **[!UICONTROL Documento PDF non interattivo]** dall&#39;elenco a discesa **[!UICONTROL Tipo]** nella scheda **[!UICONTROL Modulo/Documento]**.

* **[!UICONTROL Usa metadati personalizzati]**: selezionare questa opzione per abilitare il campo metadati personalizzato. I metadati personalizzati vengono utilizzati nei modelli e-mail.
* **[!UICONTROL Metadati personalizzati]**: selezionare metadati personalizzati per i modelli di posta elettronica. I metadati personalizzati sono disponibili nel crx-repository in apps/fd/dashboard/scripts/metadataScripts. Il percorso specificato non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo. Puoi anche utilizzare un servizio per i metadati personalizzati. È inoltre possibile estendere l&#39;interfaccia `WorkitemUserMetadataService` per fornire metadati personalizzati.
* **[!UICONTROL Mostra dati da passaggi precedenti]**: selezionare questa opzione per consentire agli assegnatari di visualizzare gli assegnatari precedenti, le azioni già eseguite sull&#39;attività, i commenti aggiunti all&#39;attività e il documento di record dell&#39;attività completata, se disponibile.
* **[!UICONTROL Mostra dati da passaggi successivi]**: selezionare questa opzione per consentire all&#39;assegnatario corrente di visualizzare l&#39;azione eseguita e i commenti aggiunti all&#39;attività dagli assegnatari successivi. Consente inoltre all’assegnatario corrente di visualizzare un documento di record dell’attività completata, se disponibile.
* **[!UICONTROL Visibilità del tipo di dati]**: per impostazione predefinita, l&#39;assegnatario può visualizzare un documento di record, gli assegnatari, le azioni intraprese e i commenti aggiunti dagli assegnatari precedenti e successivi. Utilizza l’opzione visibilità del tipo di dati per limitare il tipo di dati visibile agli assegnatari.

>[!NOTE]
>
>Le opzioni per salvare il passaggio Assegna attività come bozza e per recuperare la cronologia del passaggio Assegna attività sono disabilitate quando configuri un modello di flusso di lavoro AEM per l’archiviazione di dati esterni. Inoltre, nella casella in entrata, l’opzione di salvataggio è disabilitata.

## Passaggio Converti in PDF/A {#convert-pdfa}

PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, incorporando i font e decomprimendo il file. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. È possibile utilizzare il passaggio ***Converti in PDF/A*** in un flusso di lavoro AEM per convertire i documenti PDF in formato PDF/A.

Il passaggio Converti in PDF/A ha le seguenti proprietà:

**[!UICONTROL Documento di input]**: il documento di input può essere relativo al payload, avere un percorso assoluto, può essere fornito come payload o memorizzato in una variabile di tipo dati Documento.

**[!UICONTROL Opzioni di conversione]**: utilizzando questa proprietà, vengono specificate le impostazioni per la conversione di documenti PDF in documenti PDF/A. Le opzioni disponibili in questa scheda sono:
* **[!UICONTROL Conformità]**: specifica lo standard a cui deve conformarsi il documento PDF/A di output. Supporta diversi standard PDF come PDF/A-1b, PDF/A-2b o PDF/A-3b.
* **[!UICONTROL Livello risultati]**: specifica il livello dei risultati come PassFail, Summary o Detailed per l&#39;output di conversione.
* **[!UICONTROL Spazio colore]**: specifica lo spazio colore predefinito come S_RGB, COATED_FOGRA27, JAPAN_COLOR_COATED o SWOP, che può essere utilizzato per i file PDF/A di output.
* **[!UICONTROL Contenuto facoltativo]**: consenti la visualizzazione di specifici oggetti grafici e/o annotazioni nel documento PDF/A di output solo quando viene soddisfatto un insieme di criteri specificato.

**[!UICONTROL Documenti di output]**: specifica il percorso in cui salvare il file di output. Il file di output può essere salvato in una posizione relativa al payload, sovrascrive il payload, se il payload è un file o in una variabile di tipo dati Document.


## Passaggio Invia e-mail {#send-email-step}

Utilizzare il passaggio e-mail per inviare un messaggio e-mail, ad esempio un messaggio e-mail con un documento Record, un collegamento di un modulo adattivo <!-- , link of an interactive communication--> o un documento PDF allegato. Il passaggio Invia e-mail supporta [e-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Le e-mail di HTML sono dinamiche e si adattano alle dimensioni del client e-mail e dello schermo dei destinatari. Puoi utilizzare un modello e-mail di HTML per definire l’aspetto, la combinazione di colori e il comportamento dell’e-mail.

Il passaggio e-mail utilizza Day CQ Mail Service per inviare le e-mail. Prima di utilizzare il passaggio e-mail, accertati che il servizio e-mail sia configurato. Per impostazione predefinita, le e-mail supportano solo i protocolli HTTP e HTTP. [Contatta il team di supporto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=it#sending-email) per abilitare le porte per l&#39;invio di e-mail e l&#39;abilitazione del protocollo SMTP per l&#39;ambiente. La restrizione contribuisce a migliorare la sicurezza della piattaforma.

Il passaggio e-mail presenta le seguenti proprietà:

**[!UICONTROL Titolo]**: il titolo del passaggio consente di identificare il passaggio nell&#39;editor del flusso di lavoro.

**[!UICONTROL Descrizione]**: la spiegazione è utile per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

**[!UICONTROL Oggetto e-mail]**: l&#39;oggetto può essere recuperato dai metadati di un flusso di lavoro, specificato manualmente o recuperato dal valore archiviato in una variabile. Selezionare una delle opzioni seguenti:

* **[!UICONTROL Letterale]** Specificare manualmente un oggetto.
* **[!UICONTROL Recupera dai metadati del flusso di lavoro]** - Recupera l&#39;oggetto da una proprietà dei metadati.
* **[!UICONTROL Variabile]** - Recupera l&#39;oggetto dal valore memorizzato in una variabile di tipo dati stringa.

**[!UICONTROL Modello e-mail HTML]**: modello HTML per l&#39;e-mail. Puoi specificare le variabili in un modello e-mail. Il passaggio E-mail estrae e visualizza tutte le variabili incluse in un modello per gli input.

**[!UICONTROL Metadati modello e-mail]**: il valore delle variabili del modello e-mail può essere un valore specificato dall&#39;utente, il percorso di una risorsa nell&#39;autore o nel server di pubblicazione, un&#39;immagine o una proprietà dei metadati del flusso di lavoro.

* **[!UICONTROL Letterale]**: utilizzare l&#39;opzione quando si conosce il valore esatto da specificare. Ad esempio, [example@example.com](mailto:example@example.com).

* **[!UICONTROL Metadati flusso di lavoro]**: utilizzare l&#39;opzione quando il valore da utilizzare viene salvato in una proprietà dei metadati del flusso di lavoro. Dopo aver selezionato l’opzione, immetti il nome della proprietà dei metadati nella casella di testo vuota sotto l’opzione Metadati del flusso di lavoro. Ad esempio, emailAddress.

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL Immagine]**: utilizza l&#39;opzione per incorporare un&#39;immagine nell&#39;e-mail. Dopo aver selezionato l’opzione, sfoglia e scegli l’immagine. L&#39;opzione immagine è disponibile solo per i tag immagine (&lt;img src=&quot;&#42;&quot;/>) disponibili nel modello e-mail.

**[!UICONTROL Indirizzo e-mail del mittente/destinatario]**: selezionare l&#39;opzione **[!UICONTROL Letterale]** per specificare manualmente un indirizzo e-mail oppure selezionare l&#39;opzione **[!UICONTROL Recupera dai metadati del flusso di lavoro]** per recuperare l&#39;indirizzo e-mail da una proprietà dei metadati. È inoltre possibile specificare un elenco di matrici di proprietà dei metadati per l&#39;opzione **[!UICONTROL Recupera dai metadati del flusso di lavoro]**. Selezionare l&#39;opzione **[!UICONTROL Variabile]** per recuperare l&#39;indirizzo di posta elettronica dal valore memorizzato in una variabile di tipo di dati stringa.

* **[!UICONTROL File allegato]**: la risorsa disponibile nel percorso specificato è allegata all&#39;e-mail. Il percorso della risorsa può essere relativo al payload o al percorso assoluto. Il percorso di esempio è [Payload_Directory]/allegati/.

Selezionare l&#39;opzione **[!UICONTROL Variabile]** per recuperare l&#39;allegato archiviato in una variabile di tipo Documento, XML o JSON.

**[!UICONTROL Nome file]**: nome del file allegato e-mail. Il passaggio E-mail modifica il nome file originale dell’allegato con il nome file specificato. Il nome può essere specificato manualmente o recuperato da una proprietà o variabile di metadati del flusso di lavoro. Utilizza l&#39;opzione **[!UICONTROL Letterale]** quando conosci il valore esatto da specificare. Utilizzare l&#39;opzione **[!UICONTROL Variabile]** per recuperare il nome del file dal valore memorizzato in una variabile di tipo di dati stringa. Utilizzare l&#39;opzione **[!UICONTROL Recupera da un flusso di lavoro metadati]** quando il valore da utilizzare viene salvato in una proprietà dei metadati del flusso di lavoro.

## Passaggio Genera documento di record {#generate-document-of-record-step}

Quando un modulo viene compilato o inviato, è possibile conservarne una registrazione, in formato cartaceo o in formato documento. Questo record è denominato documento record (DoR). È possibile utilizzare il passaggio Genera documento di record per creare una versione di PDF di sola lettura o interattiva di un modulo adattivo. La versione PDF contiene informazioni inserite nel modulo insieme al layout del modulo adattivo.

Il passaggio Documento record presenta le seguenti proprietà:

**[!UICONTROL Usa modulo adattivo]**: specifica il metodo per individuare il modulo adattivo di input. Puoi utilizzare il modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile di tipo String per specificare il percorso nel campo **[!UICONTROL Seleziona variabile per risolvere]**.\
È possibile associare più Forms adattivi a un flusso di lavoro. Di conseguenza, puoi specificare un modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

**[!UICONTROL Percorso modulo adattivo]**: specifica il percorso del modulo adattivo. Il campo è disponibile quando si seleziona l&#39;opzione **[!UICONTROL Disponibile in un percorso assoluto]** dal campo **[!UICONTROL Usa modulo adattivo]**.

**[!UICONTROL Seleziona dati di input tramite]**: percorso dei dati di input per il modulo adattivo. È possibile mantenere i dati in una posizione relativa al payload, specificare un percorso assoluto dei dati o recuperare i dati memorizzati in una variabile di tipo Documento, JSON o XML. I dati di input vengono uniti al modulo adattivo per creare un documento di record.

**[!UICONTROL Selezionare il percorso dell&#39;allegato di input utilizzando]**: Percorso degli allegati. Questi allegati sono inclusi nel documento di record. È possibile mantenere gli allegati in una posizione relativa al payload, specificare un percorso assoluto degli allegati o recuperare gli allegati memorizzati in una variabile di matrice di tipo dati Documento.

Se si specifica il percorso di una cartella, ad esempio gli allegati, tutti i file direttamente disponibili nella cartella vengono allegati al documento di record. Se nelle cartelle sono disponibili file direttamente disponibili nel percorso di allegato specificato, tali file vengono inclusi nel documento di record come allegati. Se sono presenti cartelle in cartelle direttamente disponibili, queste vengono ignorate.

**[!UICONTROL Salva documento di record generato utilizzando le opzioni di seguito]**: specificare il percorso in cui conservare un file del documento di record. Puoi scegliere di sovrascrivere la cartella del payload, collocare il documento di record in una posizione all’interno della directory del payload o archiviare il documento di record in una variabile di tipo dati Documento.

**[!UICONTROL Impostazioni locali]**: specificare la lingua del documento di record. Selezionare **[!UICONTROL Letterale]** per selezionare le impostazioni locali da un elenco a discesa oppure selezionare **[!UICONTROL Variabile]** per recuperare le impostazioni locali dal valore memorizzato in una variabile di tipo di dati stringa. Definisci il codice locale durante la memorizzazione del valore della lingua in una variabile. Ad esempio, specifica **en_US** per l&#39;inglese e **fr_FR** per il francese.

## Richiama passaggio DDX {#invokeddx}

Document Description XML (DDX) è un linguaggio di markup dichiarativo i cui elementi rappresentano blocchi predefiniti di documenti. Questi blocchi predefiniti includono documenti PDF e XDP e altri elementi quali commenti, segnalibri e testo con stili. DDX definisce un set di operazioni che possono essere applicate a uno o più documenti di input per generare uno o più documenti di output. Un singolo DDX può essere utilizzato con una serie di documenti sorgente. È possibile utilizzare ***Richiama il passaggio DDX*** in un flusso di lavoro AEM per eseguire varie operazioni, come assemblaggio e disassemblaggio di documenti, creazione e modifica di Acrobat e XFA Forms e altre descritte nella [documentazione di riferimento DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

Il passaggio Richiama DDX ha le seguenti proprietà:

**[!UICONTROL Documenti di input]**: utilizzato per impostare le proprietà di un documento di input. Le opzioni disponibili in questa scheda sono:
* **[!UICONTROL Specificare DDX utilizzando]**: specifica il documento di input relativo al payload, dispone di un percorso assoluto, può essere fornito come payload o memorizzato in una variabile di tipo di dati Document.
* **[!UICONTROL Crea mappa da payload]**: aggiungi tutti i documenti nella cartella del payload alla mappa del documento di input per l&#39;API di richiamo in Assembler. Il nome del nodo di ciascun documento viene utilizzato come chiave nella mappa.
* **[!UICONTROL Mappa del documento di input]**: l&#39;opzione viene utilizzata per aggiungere più voci utilizzando il pulsante **[!UICONTROL AGGIUNGI]**. Ogni voce rappresenta la chiave del documento nella mappa e l&#39;origine del documento.

**[!UICONTROL Opzioni ambiente]**: questa opzione viene utilizzata per impostare le impostazioni di elaborazione per richiamare l&#39;API. Le opzioni disponibili in questa scheda sono:
* **[!UICONTROL Solo convalida]**: verifica la validità del documento DDX di input.
* **[!UICONTROL Errore]**: valore booleano per indicare se il servizio API di richiamo non riesce, in caso di errore o meno. Per impostazione predefinita, il relativo valore è impostato su False.
* **[!UICONTROL Primo numero Bates]**: specifica il numero, che è auto-incrementante. Questo numero con incremento automatico viene visualizzato automaticamente su ogni pagina consecutiva.
* **[!UICONTROL Stile predefinito]**: imposta lo stile predefinito per il file di output.

>[!NOTE]
>
>Le opzioni dell’ambiente sono mantenute sincronizzate con le API HTTP.

**[!UICONTROL Documenti di output]**: specifica il percorso in cui salvare il file di output. Le opzioni disponibili in questa scheda sono:
* **[!UICONTROL Salva output nel payload]**: salva i documenti di output nella cartella del payload o sovrascrive il payload, se il payload è un file.
* **[!UICONTROL Mappa documento di output]**: specifica il percorso in cui salvare in modo esplicito ogni file di documento, aggiungendo una voce per documento. Ogni voce rappresenta il documento e la posizione in cui salvarlo. Se sono presenti più documenti di output, viene utilizzata questa opzione.

## Passaggio del servizio Richiama modello dati modulo (FDM) {#invoke-form-data-model-service-step}

È possibile utilizzare [[!DNL AEM Forms] Integrazione dati](data-integration.md) per configurare e connettersi a diverse origini dati. Queste origini dati possono essere un servizio web, un servizio REST, un servizio OData e una soluzione CRM. L&#39;integrazione dei dati di [!DNL AEM Forms] consente di creare un modello di dati modulo (FDM) che include vari servizi per eseguire operazioni di recupero, aggiunta e aggiornamento dei dati nel database configurato. È possibile utilizzare il passaggio **[!UICONTROL Richiama servizio modello dati]** per selezionare un modello dati modulo (FDM) e utilizzare i servizi di FDM per recuperare, aggiornare o aggiungere dati a origini dati diverse.

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

Il passaggio del servizio Richiama modello dati modulo dispone dei campi elencati di seguito per facilitare le operazioni del modello dati modulo:

* **[!UICONTROL Titolo]**: titolo del passaggio. Consente di identificare i passaggi nell’editor del flusso di lavoro.
* **[!UICONTROL Descrizione]**: spiegazione utile per altri sviluppatori di processi quando si lavora in un ambiente di sviluppo condiviso.

* **[!UICONTROL Percorso modello dati modulo]**: sfogliare e selezionare un modello dati modulo (FDM) presente nel server.

* **[!UICONTROL Errori e convalide]**: questa opzione consente di acquisire i messaggi di errore e specificare le opzioni di convalida per i dati recuperati e inviati alle origini dati. Con queste modifiche, puoi garantire che i dati passati al passaggio di servizio Richiama modello dati modulo (FDM) siano conformi ai vincoli di dati definiti dall’origine dati. Per ulteriori dettagli, vedere [Convalida automatica dei dati di input](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL Livello di convalida]**: sono disponibili tre categorie di convalide: Base, Completo e Disattivato:

   * Completo: tutti i vincoli vengono convalidati.
   * Di base: solo i vincoli obbligatori e nullable
   * OFF: non viene eseguita alcuna convalida.

* **[!UICONTROL Termina flusso di lavoro in caso di errore]**: quando un vincolo non riesce a eseguire la convalida, il flusso di lavoro viene interrotto.

* **[!UICONTROL Memorizza codice errore nella variabile]**: è possibile memorizzare un codice di errore in una [variabile di tipo stringa](variable-in-aem-workflows.md).

* **[!UICONTROL Memorizza messaggio di errore nella variabile]**: è possibile memorizzare un messaggio di errore in una [variabile di tipo stringa](variable-in-aem-workflows.md).

* **[!UICONTROL Memorizza dettagli errore nella variabile]**: è possibile memorizzare un dettaglio errore in una [variabile di tipo JSON](variable-in-aem-workflows.md).

* **[!UICONTROL Servizio]**: elenco dei servizi forniti dal modello dati modulo (FDM) selezionato.
* **[!UICONTROL Input per servizi]** > **[!UICONTROL Fornire dati di input utilizzando metadati letterali, variabili o del flusso di lavoro e un file JSON]**: un servizio può avere più argomenti. Seleziona l’opzione per ottenere il valore degli argomenti del servizio da una proprietà di metadati del flusso di lavoro, da un oggetto JSON, da una variabile o inserisci direttamente il valore nella casella di testo fornita:

   * **[!UICONTROL Letterale]**: utilizzare l&#39;opzione quando si conosce il valore esatto da specificare. Ad esempio, srose@we.info.
   * **[!UICONTROL Variabile]**: utilizzare l&#39;opzione per recuperare il valore archiviato in una variabile.
   * **[!UICONTROL Recupera dai metadati del flusso di lavoro]**: utilizza l&#39;opzione quando il valore da utilizzare viene salvato in una proprietà dei metadati del flusso di lavoro. Ad esempio, emailAddress.

   * **[!UICONTROL Relativo al payload]**: utilizzare l&#39;opzione per recuperare l&#39;allegato salvato in un percorso relativo al payload. Selezionare l&#39;opzione e specificare il nome della cartella che include il file allegato oppure specificare il nome del file allegato nella casella di testo.

     >[!NOTE]
     >
     > Il passaggio del flusso di lavoro **Richiama modello dati modulo** supporta i metadati lato flusso di lavoro per gli array di allegati con codifica Base64 in [Modelli dati modulo basati su elenco SharePoint](/help/forms/connect-forms-to-sharepoint-list.md) e consente ai flussi di lavoro di passare, archiviare e recuperare metadati quali nome file, tipo MIME o proprietà personalizzate per gli allegati.
     > ![Allegati elenco SP](/help/edge/docs/forms/assets/workflow-sp-list.png)
     >
     > La cartella relativa al payload include un file allegato nel percorso `attachment`. Specificare `attachment` nella casella di testo dopo aver selezionato l&#39;opzione **[!UICONTROL relativa al payload]**.

   * **[!UICONTROL Notazione con punti JSON]**: utilizza l&#39;opzione quando il valore da utilizzare si trova in un file JSON. Ad esempio, insurance.customerDetails.emailAddress. L’opzione JSON Dot Notation è disponibile solo se è selezionata l’opzione Mappa campi di input dall’opzione JSON di input.
   * **[!UICONTROL Mappa i campi di input da JSON di input]**: specifica il percorso di un file JSON per ottenere il valore di input di alcuni argomenti del servizio dal file JSON. Il percorso del file JSON può essere relativo al payload, un percorso assoluto oppure puoi selezionare un documento JSON di input utilizzando una variabile di tipo JSON o Form Data Model (FDM).

* **[!UICONTROL Input per i servizi]** > **[!UICONTROL Fornisci dati di input utilizzando una variabile o un file JSON]**: seleziona l&#39;opzione per ottenere valori per tutti gli argomenti da un file JSON salvato in un percorso assoluto, in un percorso relativo al payload o in una variabile.
* **[!UICONTROL Selezionare il documento JSON di input utilizzando]**: il file JSON contenente i valori per tutti gli argomenti del servizio. Il percorso del file JSON può essere **[!UICONTROL relativo al payload]** o **[!UICONTROL percorso assoluto]**. Puoi anche recuperare il documento JSON di input utilizzando una variabile di JSON o il tipo di dati Form Data Model (FDM).

* **[!UICONTROL Notazione con punti JSON]**: lascia vuoto il campo per utilizzare tutti gli oggetti del file JSON specificato come input per gli argomenti del servizio. Per leggere un oggetto JSON specifico dal file JSON specificato come input per gli argomenti del servizio, specifica la notazione del punto per l’oggetto JSON. Ad esempio, se disponi di un JSON simile a quello elencato all’inizio della sezione, specifica insurance.customerDetails per fornire tutti i dettagli di un cliente come input per il servizio.
* **[!UICONTROL Output del servizio]** > **[!UICONTROL Mappa e scrivi i valori di output in una variabile o nei metadati]**: selezionare l&#39;opzione per salvare i valori di output come proprietà del nodo dei metadati dell&#39;istanza del flusso di lavoro in crx-repository. Specifica il nome della proprietà dei metadati e seleziona l’attributo di output del servizio corrispondente da mappare con la proprietà dei metadati. Ad esempio, mappa phone_number restituito dal servizio di output con la proprietà phone_number dei metadati del flusso di lavoro. Allo stesso modo, puoi memorizzare l’output in una variabile di tipo dati Long. Quando si seleziona una proprietà per l&#39;opzione **[!UICONTROL Attributo di output del servizio da mappare]**, vengono compilate solo le variabili in grado di memorizzare i dati della proprietà selezionata per l&#39;opzione **[!UICONTROL Salva output in]**.

* **[!UICONTROL Output del servizio]** > **[!UICONTROL Salva l&#39;output in una variabile o in un file JSON]**: selezionare l&#39;opzione per salvare i valori di output in un file JSON in un percorso assoluto, in un percorso relativo al payload o in una variabile.
* **[!UICONTROL Salva documento JSON di output tramite le opzioni di seguito]**: salva il file JSON di output. Il percorso del file JSON di output può essere relativo al payload o a un percorso assoluto. Puoi anche salvare il file JSON di output utilizzando una variabile di JSON o il tipo di dati Form Data Model (FDM).



## Passaggio Firma documento {#sign-document-step}

Il passaggio Firma documento consente di utilizzare [!DNL Adobe Sign] per firmare i documenti. Quando utilizzi il passaggio del flusso di lavoro [!DNL Adobe Sign] per firmare un modulo adattivo, il modulo può essere trasmesso tra i destinatari uno dopo l&#39;altro o può essere inviato a tutti i destinatari contemporaneamente, a seconda della configurazione del passaggio del flusso di lavoro. I Forms adattivi abilitati per [!DNL Adobe Sign] vengono inviati a Experience Manager Forms Server solo dopo che tutti i destinatari hanno completato il processo di firma.

Per impostazione predefinita, il servizio di pianificazione [!DNL Adobe Sign] controlla (esegue il polling) la risposta del destinatario ogni 24 ore. È possibile [modificare l&#39;intervallo predefinito per l&#39;ambiente](adobe-sign-integration-adaptive-forms.md#for-aem-workflows-only-configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status-configure-adobe-sign-scheduler-to-sync-the-signing-status).

Il passaggio Firma documento presenta le seguenti proprietà:

* **[!UICONTROL Nome contratto]**: specificare il titolo del contratto. Il nome del contratto diventa parte dell’oggetto e del corpo del testo dell’e-mail inviata ai firmatari. È possibile archiviare il nome in una variabile di tipo di dati String oppure selezionare **[!UICONTROL Letterale]** per aggiungere il nome manualmente.

* **[!UICONTROL Impostazioni locali]**: specificare la lingua per le opzioni di posta elettronica e verifica. È possibile archiviare le impostazioni locali in una variabile di tipo di dati String oppure selezionare **[!UICONTROL Letterale]** per scegliere le impostazioni locali dall&#39;elenco delle opzioni disponibili. È necessario definire il codice delle impostazioni locali durante la memorizzazione del valore relativo in una variabile. Ad esempio, specifica **[!UICONTROL en_US]** per l&#39;inglese e **[!UICONTROL fr_FR]** per il francese.

* **[!UICONTROL Configurazione Adobe Sign Cloud]**: scegli una configurazione cloud [!DNL Adobe Sign]. Se non hai configurato [!DNL Adobe Sign] per [!DNL AEM Forms], consulta [Integrare Adobe Sign con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL Selezionare il documento da firmare utilizzando]**: è possibile scegliere un documento da una posizione relativa al payload, utilizzare il payload come documento, specificare un percorso assoluto del documento o recuperare il documento archiviato in una variabile di tipo dati Documento.
* **[!UICONTROL Giorni fino alla scadenza]**: un documento è contrassegnato come scadenza (scadenza passata) dopo che non è presente alcuna attività per il numero di giorni specificato nel campo **[!UICONTROL Giorni fino alla scadenza]**. Il numero di giorni viene conteggiato dopo che la documentazione è stata assegnata a un utente per la firma.
* **[!UICONTROL Frequenza e-mail promemoria]**: è possibile inviare un messaggio e-mail di promemoria a intervalli giornalieri o settimanali. La settimana viene conteggiata dal giorno in cui la documentazione viene assegnata a un utente per la firma.
* **[!UICONTROL Processo di firma]**: è possibile scegliere di firmare un documento in ordine sequenziale o parallelo. In ordine sequenziale, un firmatario riceve il documento alla volta per la firma. Dopo che il primo firmatario ha completato la firma del documento, questo viene inviato al secondo firmatario e così via. In ordine parallelo, più firmatari possono firmare un documento alla volta.
* **[!UICONTROL URL di reindirizzamento]**: specificare un URL di reindirizzamento. Dopo aver firmato il documento, puoi reindirizzare l’assegnatario a un URL. Di solito, questo URL contiene un messaggio di ringraziamento o ulteriori istruzioni.
* **[!UICONTROL Fase flusso di lavoro]**: un flusso di lavoro può avere più fasi. Questi stadi vengono visualizzati nella casella in entrata di AEM. Puoi definire questi stadi nelle proprietà del modello ( **[!UICONTROL Sidekick]** > **[!UICONTROL Pagina]** > **[!UICONTROL Proprietà pagina]** > **[!UICONTROL Stadi]**).
* **[!UICONTROL Seleziona destinatari]**: specificare il metodo di selezione dei destinatari del documento. Puoi assegnare dinamicamente il flusso di lavoro a un utente o a un gruppo oppure aggiungere manualmente i dettagli di un destinatario. Quando selezioni Manualmente nell’elenco a discesa, aggiungi i dettagli del destinatario come E-mail, Ruolo e Metodo di autenticazione.

  >[!NOTE]
  >
  >* Nella sezione Ruolo è possibile specificare il ruolo del destinatario come Firmatario, Approvatore, Accettatore, Destinatario certificato, Form Filler e Delegatore.
  >* Se si seleziona Delegante nell&#39;opzione Ruolo, il Delegante può assegnare l&#39;attività di firma a un altro destinatario.
  >* Se è stato configurato un metodo di autenticazione per [!DNL Adobe Sign], in base alla configurazione selezionata verrà selezionato un metodo di autenticazione, ad esempio l&#39;autenticazione basata su telefono, l&#39;autenticazione basata su identità social, l&#39;autenticazione basata su Knowledge, l&#39;autenticazione basata su identità pubblica.

* **[!UICONTROL Script o servizio per selezionare i destinatari]**: l&#39;opzione è disponibile solo se si seleziona l&#39;opzione Dinamicamente nel campo Seleziona destinatari. È possibile specificare un codice ECMAScript o un servizio per scegliere i firmatari e le opzioni di verifica per un documento.
* **[!UICONTROL Dettagli destinatario]**: l&#39;opzione è disponibile solo se nel campo Seleziona destinatari è selezionata l&#39;opzione Manualmente. Specifica un indirizzo e-mail e scegli un meccanismo di verifica opzionale. Prima di selezionare un meccanismo di verifica in due fasi, verificare che l&#39;opzione di verifica corrispondente sia abilitata per l&#39;account [!DNL Adobe Sign] configurato. Puoi utilizzare una variabile di tipo stringa per definire i valori per i campi E-mail, Codice paese e Numero di telefono. I campi Codice paese e Numero di telefono vengono visualizzati solo se si seleziona Verifica telefono dall&#39;elenco a discesa Verifica in due passaggi.
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

**[!UICONTROL Proprietà input]**

* **[!UICONTROL Selezionare il file modello utilizzando]**: specificare il percorso del file modello. Puoi selezionare il file modello utilizzando il percorso relativo al payload, salvato in un percorso assoluto oppure utilizzando una variabile di tipo dati Documento. Ad esempio, [Directory_Payload]/Workflow/data.xml. Se il percorso non esiste in crx-repository, un amministratore può crearlo prima di utilizzarlo. Inoltre, puoi anche accettare il payload come file di dati di input.

* **[!UICONTROL Seleziona documento dati tramite]**: specifica il percorso di un file di dati di input. Puoi selezionare il file di dati di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto oppure utilizzando una variabile di tipo dati Documento. Ad esempio, [Directory_Payload]/Workflow/data.xml. Se il percorso non esiste in crx-repository, un amministratore può crearlo prima di utilizzarlo.

* **[!UICONTROL Formato stampante]**: valore Formato di stampa che specifica il linguaggio di descrizione della pagina da utilizzare quando non viene fornito un file XDC per generare il flusso di output. Se fornisci un valore letterale, seleziona uno dei seguenti valori:

   * **[!UICONTROL color PCL]**: utilizzare l&#39;opzione per specificare un file XDC per PCL.
   * **[!UICONTROL PostScript generico]**: utilizzare l&#39;opzione per specificare un file XDC generico per PostScript.
   * **[!UICONTROL ZPL 300 DPI]**: utilizzare ZPL 300 DPI. Viene utilizzato zpl300.xdc.
   * **[!UICONTROL ZPL 600 DPI]**: utilizzare ZPL 600 DPI. Viene utilizzato il file zpl600.xdc.
   * **[!UICONTROL IPL 300 DPI]**: utilizzare IPL 300 DPI. Viene utilizzato ipl300.xdc.
   * **[!UICONTROL IPL 400 DPI]**: utilizzare IPL 400 DPI. Viene utilizzato il file ipl400.xdc.
   * **[!UICONTROL TPCL 600 DPI]**: utilizzare TPCL 600 DPI. Viene utilizzato il file tpcl600.xdc.
   * **[!UICONTROL PostScript Plain]**: utilizzare l&#39;opzione per specificare un file XDC in testo normale per PostScript.
   * **[!UICONTROL DPL300DPI]**: utilizzare DPL 300 DPI. Viene utilizzato dpl300.xdc.
   * **[!UICONTROL DPL400DPI]**: utilizzare DPL 400 DPI. Viene utilizzato dpl400.xdc.
   * **[!UICONTROL DPL600DPI]**: utilizzare DPL 600 DPI. Viene utilizzato dpl600.xdc.
   * **[!UICONTROL HP_PCL_5e]**: utilizzare l&#39;opzione per supportare più dispositivi Canon.


**[!UICONTROL Proprietà output]**

* **[!UICONTROL Salva documento di output tramite]**: specificare il percorso in cui salvare il file di output. Puoi salvare il file di output in una posizione relativa al payload, in una variabile, oppure specificare una posizione assoluta per salvare il file di output. Se il percorso non esiste in crx-repository, un amministratore può crearlo prima di utilizzarlo.

**[!UICONTROL Proprietà avanzate]**

* **[!UICONTROL Selezionare il percorso della directory principale del contenuto utilizzando]**: la directory principale del contenuto è un valore stringa che specifica l&#39;URI, il riferimento assoluto o il percorso nel repository per recuperare le risorse relative utilizzate dalla progettazione del modulo. Ad esempio, se la struttura del modulo fa riferimento a un&#39;immagine relativamente, ad esempio `../myImage.gif`, `myImage.gif` deve trovarsi in `repository://`. Il valore predefinito è `repository://`, che punta al livello principale dell&#39;archivio.

  Quando scegli una risorsa dall’applicazione, il percorso URI della directory principale del contenuto deve avere la struttura corretta. Ad esempio, se un modulo viene selezionato da un&#39;applicazione denominata SampleApp e si trova in `SampleApp/1.0/forms/Test.xdp`, l&#39;URI radice contenuto deve essere specificato come `repository://administrator@password/Applications/SampleApp/1.0/forms/` o `repository:/Applications/SampleApp/1.0/forms/` (quando l&#39;autorità è null). Quando l’URI della directory principale del contenuto viene specificato in questo modo, i percorsi di tutte le risorse a cui si fa riferimento nel modulo vengono risolti rispetto a questo URI.

* **[!UICONTROL Seleziona file XCI tramite]**: i file XCI vengono utilizzati per descrivere i font e altre proprietà utilizzati per gli elementi di progettazione dei moduli. È possibile mantenere un file XCI relativo al payload, in un percorso assoluto o utilizzando una variabile di tipo dati Documento.

* **[!UICONTROL Impostazioni locali]**: specifica la lingua utilizzata per generare il documento PDF. Se fornisci un valore letterale, seleziona una lingua dall’elenco o scegli uno dei seguenti valori:
   * **[!UICONTROL Per utilizzare il server predefinito]**:
Impostazione predefinita. Utilizzare l&#39;impostazione Locale configurata sul server [!DNL AEM Forms]. L&#39;impostazione Locale viene configurata utilizzando la console di amministrazione. (Vedi [Guida di Designer](https://helpx.adobe.com/content/dam/help/it/experience-manager/6-5/forms/pdf/using-designer.pdf).)

   * **[!UICONTROL Per utilizzare un valore personalizzato]**:
Digita il codice locale nella casella letterale o seleziona una variabile stringa contenente il codice locale. Per un elenco completo dei codici delle impostazioni internazionali supportati, vedere https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copie]**: valore intero che specifica il numero di copie da generare per l&#39;output. Il valore predefinito è 1.

* **[!UICONTROL Stampa fronte retro]**: valore di paginazione che specifica se utilizzare la stampa fronte/retro o fronte/retro. Le stampanti che supportano PostScript e PCL utilizzano questo valore. Se fornisci un valore letterale, seleziona uno dei seguenti valori:
   * **[!UICONTROL Edge lungo fronte-retro]**: utilizzare la stampa fronte-retro e la stampa utilizzando la paginazione a lato lungo.
   * **[!UICONTROL Edge corto fronte-retro]**: utilizzare la stampa fronte-retro e la stampa utilizzando la paginazione lato-corto.
   * **[!UICONTROL Simplex]**: utilizzare la stampa fronte/retro.

## Passaggio Genera output PDF non interattivo   {#generatePDFdocuments}

1. Trascina il flusso di lavoro Genera output PDF non interattivo nella scheda Forms Workflow di Sidekick.
1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente configurare documenti di input, documenti di output e parametri aggiuntivi e fare clic su **[!UICONTROL OK]**.

### Documenti di input {#input-documents-3}

* **File modello**: specifica il percorso del modello XDP. È un campo obbligatorio.

* **Documento dati**: specifica il percorso dell&#39;XML dati da unire al modello.

### Documento di output {#output-document}

**Documento di output**: specifica il nome del modulo PDF generato.

### Parametri aggiuntivi {#additional-parameters-1}

* **Directory principale contenuto**: specifica il percorso della cartella nell&#39;archivio in cui sono archiviati i frammenti o le immagini utilizzati nel modello XDP di input.
* **Impostazioni locali**: specifica le impostazioni locali predefinite per il modulo PDF generato.
* **Acrobat versione**: specifica la versione di Acrobat di destinazione per il modulo PDF generato.
* **PDF linearizzato**: specifica se ottimizzare il PDF generato per la visualizzazione Web.
* **PDF con tag**: specifica se rendere accessibile il PDF generato.
* **Documento XCI**: specifica il percorso del file XCI.

## Consulta anche {#see-also}

* [Variabili nei flussi di lavoro AEM incentrati su Forms](/help/forms/variable-in-aem-workflows.md)
* [Configura impostazione Fuori sede](/help/forms/configure-out-of-office-settings.md)

<!--

>[!MORELIKETHIS]
>
>* [Forms-centric workflow on OSGi](/help/forms/aem-forms-workflow.md)
>* [Use AEM translation workflow to localize Adaptive Forms and Document of Record](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms.md)

-->