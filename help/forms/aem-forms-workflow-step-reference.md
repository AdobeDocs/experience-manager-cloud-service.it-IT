---
title: Come assegnare un flusso di lavoro ad un altro utente, inviare e-mail, utilizzare Adobe Sign in un flusso di lavoro?
description: I flussi di lavoro incentrati su Forms consentono di creare rapidamente flussi di lavoro adattivi basati su Forms. Puoi utilizzare Adobe Sign per firmare i documenti via e-mail, creare processi aziendali basati su moduli, recuperare e inviare dati a più origini dati e inviare notifiche e-mail
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '7210'
ht-degree: 0%

---

# Flussi di lavoro AEM incentrati su Forms - Riferimento dettagliato {#forms-centric-workflow-on-osgi-step-reference}

I modelli di flusso di lavoro consentono di convertire una logica di business in un processo ripetitivo automatizzato. Un modello consente di definire ed eseguire una serie di passaggi. Puoi anche definire le proprietà del modello, ad esempio se il flusso di lavoro è transitorio o se utilizza più risorse. È possibile [includere vari passaggi del flusso di lavoro AEM in un modello per raggiungere la logica di business](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem).

## Passaggi incentrati su Forms {#forms-workflow-steps}

I passaggi del flusso di lavoro incentrati su Forms eseguono operazioni specifiche di AEM Forms in un flusso di lavoro AEM. Questi passaggi ti consentono di creare rapidamente un flusso di lavoro basato su Forms adattivo basato su Forms su OSGi. Questi flussi di lavoro possono essere utilizzati per sviluppare flussi di lavoro di base per la revisione e l’approvazione, processi aziendali interni e attraverso il firewall. Puoi inoltre utilizzare i passaggi Forms Workflow per:

* Crea processi aziendali, flussi di lavoro post-invio e flussi di lavoro di back-end per gestire i processi di iscrizione.

* Creare e assegnare attività a un utente o a un gruppo.

* Utilizzo [!DNL Adobe Sign] in un flusso di lavoro AEM per inviare un documento per la firma.

* Generare un documento di registrazione on-demand o su invio del modulo.

* Collega un modello di flusso di lavoro con varie origini dati per salvare e recuperare facilmente i dati.

* Utilizza il passaggio e-mail per inviare e-mail di notifica e altri allegati al completamento di un’azione e all’inizio o al completamento di un flusso di lavoro.

>[!NOTE]
>
>Se il modello di flusso di lavoro è contrassegnato per uno storage esterno, per tutti i passaggi del flusso di lavoro Forms è possibile selezionare solo l&#39;opzione variabile per archiviare o recuperare file di dati e allegati.


## Assegna passaggio attività {#assign-task-step}

Il passaggio dell&#39;attività di assegnazione crea un elemento di lavoro e lo assegna a un utente o a un gruppo. Oltre ad assegnare l’attività, il componente specifica anche il Modulo adattivo o il PDF non interattivo per l’attività. Il Modulo adattivo è necessario per accettare l’input degli utenti e PDF non interattivo o un Modulo adattivo di sola lettura viene utilizzato per i flussi di lavoro di revisione.

È inoltre possibile utilizzare il componente per controllare il comportamento dell’attività. Ad esempio, creazione di un documento di record automatico, assegnazione dell&#39;attività a un utente o a un gruppo specifico, specifica il percorso dei dati inviati, specifica il percorso dei dati da precompilare e specifica le azioni predefinite. Il passaggio Assegna attività ha le seguenti proprietà:

* **[!UICONTROL Titolo]**: Titolo dell’attività. Il titolo viene visualizzato in AEM casella in entrata.
* **[!UICONTROL Descrizione]**: Spiegazione delle operazioni eseguite nell&#39;attività. Queste informazioni sono utili per altri sviluppatori di processi quando lavori in un ambiente di sviluppo condiviso.

* **[!UICONTROL Percorso miniatura]**: Percorso della miniatura dell&#39;attività. Se non viene specificato alcun percorso, per una miniatura predefinita del modulo adattivo viene visualizzata un’icona predefinita per il documento di record.
* **[!UICONTROL Fase del flusso di lavoro]**: Un flusso di lavoro può avere più fasi. Queste fasi vengono visualizzate nella casella in entrata AEM. Puoi definire questi stadi nelle proprietà del modello (Barra laterale > Pagina > Proprietà pagina > Stadi).
* **[!UICONTROL Priorità]**: La priorità selezionata viene visualizzata nella casella in entrata AEM. Le opzioni disponibili sono Alta, Media e Bassa. Il valore predefinito è Medio.
* **[!UICONTROL Data di scadenza]**: Specificare il numero di giorni o ore dopo le quali l&#39;attività è contrassegnata come scaduta. Se si seleziona **[!UICONTROL Disattivato]**, quindi l&#39;attività non viene mai contrassegnata come scaduta. È inoltre possibile specificare un gestore di timeout per eseguire attività specifiche dopo la scadenza dell&#39;attività.

* **[!UICONTROL Giorni]**: Numero di giorni precedenti al completamento dell&#39;attività. Il numero di giorni conteggiati dopo l’assegnazione dell’attività a un utente. Se un&#39;attività non è completa e supera il numero di giorni specificato nel campo Giorni, se selezionato, viene attivato un gestore di timeout dopo la data di scadenza.
* **[!UICONTROL Ore]**: Numero di ore prima del completamento dell&#39;attività. Il numero di ore viene conteggiato dopo che l’attività è stata assegnata a un utente. Se un&#39;attività non è completa e supera il numero di ore specificato nel campo Ore, se selezionato, viene attivato un gestore di timeout dopo le ore di scadenza.
* **[!UICONTROL Timeout dopo la data di scadenza]**: Selezionare questa opzione per abilitare il campo di selezione Gestore timeout.
* **[!UICONTROL Gestore di timeout]**: Selezionare lo script da eseguire quando la fase dell&#39;attività di assegnazione supera la data di scadenza. Script inseriti nell’archivio CRX in [app]/fd/dashboard/scripts/timeoutHandler sono disponibili per la selezione. Il percorso specificato non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo.
* **[!UICONTROL Evidenziare l&#39;azione e il commento dall&#39;ultima attività in Dettagli attività]**: Selezionare questa opzione per visualizzare l’ultima azione eseguita e il commento ricevuto sulla sezione dei dettagli dell’attività di un’attività.
* **[!UICONTROL Tipo]**: Scegliere il tipo di documento da compilare all&#39;avvio del flusso di lavoro. È possibile scegliere un modulo adattivo, un modulo adattivo di sola lettura, un documento PDF non interattivo.

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL Usa modulo adattivo]**: Specificare il metodo per individuare il modulo adattivo di input. Questa opzione è disponibile se si seleziona Modulo adattivo o Modulo adattivo di sola lettura dall’elenco a discesa Tipo . Puoi utilizzare il Modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile di tipo String per specificare il percorso.\
   Puoi associare più Forms adattivo a un flusso di lavoro. Di conseguenza, è possibile specificare un Modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL Percorso modulo adattivo]**: Specifica il percorso del modulo adattivo. È possibile utilizzare il Modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto, oppure recuperare il Modulo adattivo da un percorso memorizzato in una variabile di tipo dati stringa.
* **[!UICONTROL Seleziona PDF di input utilizzando]**: Specifica il percorso di un documento PDF non interattivo. Il campo è disponibile quando si sceglie un documento PDF non interattivo nel campo Tipo. È possibile selezionare il PDF di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto o utilizzando una variabile del tipo di dati Documento. Ad esempio: [Payload_Directory]/Workflow/PDF/credit-card.pdf. Il percorso non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo. Per utilizzare l’opzione Percorso di PDF è necessario abilitare l’opzione Documento di record o Forms adattivo basato su modelli di modulo.
* **[!UICONTROL Per l’attività completata, eseguire il rendering del modulo adattivo come]**: Quando un’attività è contrassegnata come completa, è possibile eseguire il rendering del modulo adattivo come modulo adattivo di sola lettura o come documento PDF. Per eseguire il rendering del modulo adattivo come documento di record, è necessario abilitare l’opzione Documento di record o Forms adattivo basato su modelli di modulo.
* **[!UICONTROL Prepopolato]**: I campi seguenti elencati fungono da input per l’attività:

   * **[!UICONTROL Seleziona il file di dati di input utilizzando]**: Percorso del file di dati di input (.json, .xml, .doc o modello di dati del modulo). È possibile recuperare il file di dati di input utilizzando un percorso relativo al payload o recuperare il file memorizzato in una variabile di tipo di dati Document, XML o JSON. Ad esempio, il file contiene i dati inviati per il modulo tramite un’applicazione Casella in entrata AEM. Un esempio di percorso è [Payload_Directory]/workflow/data.
   * **[!UICONTROL Selezionare gli allegati di input utilizzando]**: Gli allegati disponibili nella posizione vengono allegati al modulo associato all&#39;attività. Il percorso può essere relativo al payload o recuperare l&#39;allegato memorizzato in una variabile di un documento. Un esempio di percorso è [Payload_Directory]/attachment/. È possibile specificare gli allegati posizionati in relazione al payload o utilizzare una variabile di tipo documento (Elenco array > Documento) per specificare un allegato di input per il modulo adattivo.

   <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL Mappatura attributi richiesta]**: Utilizza la sezione Mappatura attributi di richiesta per definire la [nome e valore dell’attributo della richiesta](work-with-form-data-model.md#bindargument). Recupera i dettagli dall’origine dati in base al nome e al valore dell’attributo specificati nella richiesta. È possibile definire un valore dell&#39;attributo della richiesta utilizzando un valore letterale o una variabile di tipo dati String.

   <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL Informazioni inviate]**: I campi seguenti elencati fungono da percorsi di output per l’attività:

   * **[!UICONTROL Salva file di dati di output utilizzando]**: Salvare il file di dati (.json, .xml, .doc o modello dati modulo). Il file di dati contiene informazioni inviate tramite il modulo associato. È possibile salvare il file di dati di output utilizzando un percorso relativo al payload o archiviarlo in una variabile di tipo di dati Document, XML o JSON. Ad esempio: [Payload_Directory]/Workflow/data, dove i dati sono un file.
   * **[!UICONTROL Salva allegati utilizzando]**: Salvare gli allegati del modulo forniti in un’attività. È possibile salvare gli allegati utilizzando un percorso relativo al payload o archiviarlo in una variabile dell&#39;elenco di matrice del tipo di dati Documento.
   * **[!UICONTROL Salva documento di record utilizzando]**: Percorso per il salvataggio di un file del documento di record. Ad esempio: [Payload_Directory]/DocumentofRecord/credit-card.pdf. È possibile salvare il documento di record utilizzando un percorso relativo al payload o archiviarlo in una variabile del tipo di dati Documento. Se si seleziona **[!UICONTROL Relativo al payload]** Se il campo percorso viene lasciato vuoto, il documento di record non viene generato. Questa opzione è disponibile solo se si seleziona Modulo adattivo dall’elenco a discesa Tipo .

   <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL Assegnatario]** > **[!UICONTROL Opzioni di assegnazione]**: Specificare il metodo per assegnare l&#39;attività a un utente. È possibile assegnare dinamicamente l&#39;attività a un utente o a un gruppo utilizzando lo script Selezione partecipanti o assegnarla a un utente o gruppo AEM specifico.
* **[!UICONTROL Selettore partecipante]**: L’opzione è disponibile quando **[!UICONTROL In modo dinamico per un utente o un gruppo]** l’opzione è selezionata nel campo Assegna opzioni . È possibile utilizzare uno script ECMAScript o un servizio per selezionare in modo dinamico un utente o un gruppo. Per ulteriori informazioni, consulta [Assegnazione dinamica di un flusso di lavoro agli utenti](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) e [Creazione di un passaggio personalizzato Adobe Experience Manager Dynamic Participant .](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **[!UICONTROL Partecipanti]**: Il campo è disponibile quando la **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** è selezionata nella **[!UICONTROL Selettore partecipante]** campo . Il campo consente di selezionare utenti o gruppi per l’opzione RandomParticipantChooser.

* **[!UICONTROL Assegnatario]**: Il campo è disponibile quando la **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** è selezionato in **[!UICONTROL Selettore partecipante]** campo . Il campo ti consente di selezionare una variabile del tipo di dati String per definire l’assegnatario.

* **[!UICONTROL Argomenti]**: Il campo è disponibile quando nel campo Selettore partecipante è selezionato uno script diverso da quello RandomParticipantChoose . Il campo consente di fornire un elenco di un argomento separato da virgole per lo script selezionato nel campo Selettore partecipante.

* **[!UICONTROL Utente o gruppo]**: L&#39;attività viene assegnata all&#39;utente o al gruppo selezionato. L’opzione è disponibile quando **[!UICONTROL Per un utente o un gruppo specifico]** è selezionato in **[!UICONTROL Opzioni di assegnazione]** campo . Il campo elenca tutti gli utenti e i gruppi del [!DNL workflow-users] gruppo.\
   La **[!UICONTROL Utente o gruppo]** nel menu a discesa sono elencati gli utenti e i gruppi a cui l&#39;utente connesso ha accesso. La visualizzazione del nome utente dipende dal se si dispone delle autorizzazioni di accesso per **[!UICONTROL utenti]** nodo in crx-repository per quel particolare utente.

* **[!UICONTROL Invia e-mail di notifica]**: Seleziona questa opzione per inviare notifiche e-mail all’assegnatario. Queste notifiche vengono inviate quando un’attività viene assegnata a un utente o a un gruppo. È possibile utilizzare **[!UICONTROL Indirizzo e-mail destinatario]** per specificare il meccanismo per recuperare l’indirizzo e-mail.

* **[!UICONTROL Indirizzo e-mail destinatario]**: È possibile memorizzare l’indirizzo e-mail in una variabile, utilizzare un valore letterale per specificare un indirizzo e-mail permanente o utilizzare l’indirizzo e-mail predefinito dell’assegnatario specificato nel profilo dell’assegnatario. Puoi utilizzare il valore letterale o una variabile per specificare l’indirizzo e-mail di un gruppo. L’opzione della variabile è utile per recuperare e utilizzare in modo dinamico un indirizzo e-mail. La **[!UICONTROL Usa indirizzo e-mail predefinito dell’assegnatario]** l&#39;opzione è disponibile solo per un singolo assegnatario. In questo caso, viene utilizzato l’indirizzo e-mail memorizzato nel profilo utente assegnatari.

* **[!UICONTROL Modello e-mail HTML]**: Seleziona il modello e-mail per l’e-mail di notifica. Per modificare un modello, modifica il file che si trova in /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt in crx-repository.
* **[!UICONTROL Consenti delega a]**: AEM casella in entrata fornisce all’utente connesso un’opzione per delegare il flusso di lavoro assegnato a un altro utente. Puoi delegare all’interno dello stesso gruppo o all’utente del flusso di lavoro di un altro gruppo. Se l’attività viene assegnata a un singolo utente e la **[!UICONTROL consentire la delega ai membri del gruppo assegnatario]** l’opzione è selezionata, quindi non è possibile delegare l’attività a un altro utente o gruppo.
* **[!UICONTROL Impostazioni condivisione]**: AEM casella in entrata fornisce opzioni per condividere con un altro utente una singola o tutte le attività presenti nella casella in entrata:
   * Quando il **[!UICONTROL Consentire agli assegnatari di condividere esplicitamente nella casella in entrata]** l’opzione è selezionata, l’utente può selezionare l’attività in AEM casella in entrata e condividerla con un altro utente AEM.
   * Quando il **[!UICONTROL Consentire agli assegnatari di condividere tramite condivisione in entrata]** l’opzione è selezionata e gli utenti condividono gli elementi della casella in entrata o consentono ad altri utenti di accedere agli elementi della casella in entrata, solo le attività con l’opzione precedentemente menzionata abilitata vengono condivise con altri utenti.
   * Quando il **[!UICONTROL Consenti agli assegnatari di delegare utilizzando le impostazioni &quot;Fuori sede&quot;]** è selezionato. L&#39;assegnatario può abilitare l&#39;opzione per delegare l&#39;attività ad altri utenti insieme ad altre opzioni Out of Office. Tutte le nuove attività assegnate all’utente fuori sede vengono automaticamente delegate (assegnate) agli utenti indicati nelle impostazioni fuori sede.

   Consente agli altri utenti di scegliere le attività assegnate mentre è fuori sede e non è in grado di lavorare sulle attività assegnate.

* **[!UICONTROL Azioni]** > **[!UICONTROL Azioni predefinite]**: Sono disponibili le azioni Invia, Salva e Ripristina predefinite. Per impostazione predefinita sono abilitate tutte le azioni predefinite.
* **[!UICONTROL Variabile di percorso]**: Nome della variabile di route. La variabile di route acquisisce le azioni personalizzate selezionate da un utente nella casella in entrata AEM.
* **[!UICONTROL Percorsi]**: Un&#39;attività può essere suddivisa in percorsi diversi. Se selezionata in AEM casella in entrata, la route restituisce un valore e i rami del flusso di lavoro in base alla route selezionata. È possibile memorizzare i percorsi in una variabile della matrice del tipo di dati String oppure selezionare **[!UICONTROL Letterale]** per aggiungere manualmente i percorsi.

* **[!UICONTROL Titolo percorso]**: Specifica il titolo della route. Viene visualizzato in AEM casella in entrata.
* **[!UICONTROL Icona Corallo]**: Specifica l&#39;attributo HTML di un&#39;icona corallo. La libreria CorelUI di Adobe fornisce un ampio set di icone touch-first. È possibile scegliere e utilizzare un&#39;icona per il percorso. Viene visualizzato insieme al titolo nella casella in entrata AEM. Se si memorizzano i percorsi in una variabile, i percorsi utilizzano un&#39;icona corallina &#39;Tags&#39; predefinita.
* **[!UICONTROL Consenti all&#39;assegnatario di aggiungere un commento]**: Selezionare questa opzione per abilitare i commenti per l&#39;attività. Al momento dell’invio dell’attività, un assegnatario può aggiungere i commenti all’interno AEM casella in entrata.
* **[!UICONTROL Salva commento nella variabile]**: Salvare il commento in una variabile di tipo dati String. Questa opzione viene visualizzata solo se si seleziona la **[!UICONTROL Consenti all&#39;assegnatario di aggiungere un commento]** casella di controllo.

* **[!UICONTROL Consenti all&#39;assegnatario di aggiungere allegati all&#39;attività]**: Selezionare questa opzione per abilitare gli allegati per l&#39;attività. Al momento dell’invio dell’attività, un assegnatario può aggiungere gli allegati dall’interno AEM casella in entrata. Puoi anche limitare la dimensione massima **[!UICONTROL (Dimensione massima del file)]** di un allegato. La dimensione predefinita è 2 MB.

* **[!UICONTROL Salva gli allegati delle attività di output utilizzando]**: Specificare il percorso della cartella dell&#39;allegato. È possibile salvare gli allegati dell&#39;attività di output utilizzando un percorso relativo al payload o in una variabile di matrice del tipo di dati del documento. Questa opzione viene visualizzata solo se si seleziona la **[!UICONTROL Consenti all&#39;assegnatario di aggiungere allegati all&#39;attività]** seleziona e seleziona **[!UICONTROL Modulo adattivo]**, **[!UICONTROL Modulo adattivo di sola lettura]** oppure **[!UICONTROL Documento PDF non interattivo]** dal **[!UICONTROL Tipo]** elenco a discesa nella **[!UICONTROL Modulo/Documento]** scheda .

* **[!UICONTROL Utilizzare i metadati personalizzati]**: Seleziona questa opzione per abilitare il campo metadati personalizzato. I metadati personalizzati vengono utilizzati nei modelli e-mail.
* **[!UICONTROL Metadati personalizzati]**: Seleziona un metadati personalizzato per i modelli e-mail. I metadati personalizzati sono disponibili in crx-repository su apps/fd/dashboard/scripts/metadataScripts. Il percorso specificato non esiste in crx-repository. Un amministratore crea il percorso prima di utilizzarlo. Puoi anche utilizzare un servizio per i metadati personalizzati. È inoltre possibile estendere `WorkitemUserMetadataService` per fornire metadati personalizzati.
* **[!UICONTROL Mostra dati dai passaggi precedenti]**: Selezionare questa opzione per consentire agli assegnatari di visualizzare gli assegnatari precedenti, le azioni già eseguite sull&#39;attività, i commenti aggiunti all&#39;attività e il documento di registrazione dell&#39;attività completata, se disponibile.
* **[!UICONTROL Mostra dati dai passaggi successivi]**: Selezionare questa opzione per consentire all&#39;assegnatario corrente di visualizzare l&#39;azione intrapresa e i commenti aggiunti all&#39;attività dagli assegnatari successivi. Consente inoltre all&#39;assegnatario corrente di visualizzare un documento di registrazione dell&#39;attività completata, se disponibile.
* **[!UICONTROL Visibilità del tipo di dati]**: Per impostazione predefinita, un assegnatario può visualizzare un documento di registrazione, gli assegnatari, le azioni intraprese e i commenti aggiunti dagli assegnatari precedenti e successivi. Utilizza l’opzione di visibilità del tipo di dati per limitare il tipo di dati visibili agli assegnatari.

>[!NOTE]
>
>Le opzioni per salvare il passaggio Assegna attività come bozza e recuperare la cronologia del passaggio Assegna attività sono disabilitate quando si configura un modello di flusso di lavoro AEM per l’archiviazione dei dati esterni. Inoltre, in Posta in arrivo, l’opzione per il salvataggio è disabilitata.

## Passaggio Converti in PDF/A {#convert-pdfa}

PDF/A è un formato di archiviazione per la conservazione a lungo termine del contenuto del documento, incorporando i font e decomprimendo il file. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. È possibile utilizzare ***Converti in PDF/A*** passa a un flusso di lavoro AEM per convertire i documenti PDF in formato PDF/A.

Il passaggio Converti in PDF/A ha le seguenti proprietà:

**[!UICONTROL Documento di input]**: Il documento di input può essere relativo al payload, avere un percorso assoluto, può essere fornito come payload o memorizzato in una variabile di tipo di dati Documento.

**[!UICONTROL Opzioni di conversione]**: Questa proprietà consente di specificare le impostazioni per la conversione dei documenti PDF in documenti PDF/A. Varie opzioni disponibili in questa scheda sono:
* **[!UICONTROL Conformità]**: Specifica lo standard a cui deve conformarsi il documento PDF/A di output. Supporta diversi standard PDF come PDF/A-1b, PDF/A-2b o PDF/A-3b.
* **[!UICONTROL Livello dei risultati]**: Specifica il livello del risultato come PassFail, Summary o Detailed, per l&#39;output di conversione.
* **[!UICONTROL Spazio colore]**: Specifica lo spazio colore predefinito come S_RGB, COATED_FOGRA27, JAPAN_COLOR_COATED o SWOP, che può essere utilizzato per i file di output PDF/A.
* **[!UICONTROL Contenuto facoltativo]**: Consenti la visualizzazione di oggetti grafici e/o annotazioni specifici nel documento PDF/A di output, solo quando viene soddisfatto un set specifico di criteri.

**[!UICONTROL Documenti di output]**: Specifica il percorso in cui salvare il file di output. Il file di output può essere salvato in una posizione relativa al payload, sovrascrive il payload, se il payload è un file o in una variabile del tipo di dati Documento.


## Invia passaggio e-mail {#send-email-step}

Utilizza il passaggio e-mail per inviare un’e-mail, ad esempio un messaggio e-mail con un documento di record, un collegamento a un modulo adattivo <!-- , link of an interactive communication-->oppure con un documento PDF allegato. Supporto dei passaggi di invio e-mail [E-mail HTML](https://en.wikipedia.org/wiki/HTML_email). Le e-mail di HTML sono reattive e si adattano al client e-mail e alle dimensioni dello schermo dei destinatari. Puoi utilizzare un modello e-mail di HTML per definire l’aspetto, lo schema colore e il comportamento dell’e-mail.

Il passaggio e-mail utilizza Day CQ Mail Service per inviare e-mail. Prima di utilizzare il passaggio e-mail, assicurati che il servizio e-mail sia configurato. Per impostazione predefinita, le e-mail supportano solo i protocolli HTTP e HTTP. [Contatta il team di supporto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email) per abilitare le porte per l’invio di e-mail e per abilitare il protocollo SMTP per l’ambiente. Questa limitazione consente di migliorare la sicurezza della piattaforma.

Il passaggio e-mail ha le seguenti proprietà:

**[!UICONTROL Titolo]**: Il titolo del passaggio ti aiuta a identificare il passaggio nell’editor del flusso di lavoro.

**[!UICONTROL Descrizione]**: La spiegazione è utile per altri sviluppatori di processi quando lavori in un ambiente di sviluppo condiviso.

**[!UICONTROL Oggetto e-mail]**: L’oggetto può essere recuperato dai metadati di un flusso di lavoro, specificati manualmente o recuperati dal valore memorizzato in una variabile. Seleziona tra le seguenti opzioni:

* **[!UICONTROL Letterale]** Specifica manualmente un oggetto.
* **[!UICONTROL Recupera dai metadati del flusso di lavoro]** - Recupera l&#39;oggetto da una proprietà di metadati.
* **[!UICONTROL Variabile]** - Recupera l&#39;oggetto dal valore memorizzato in una variabile del tipo di dati stringa.

**[!UICONTROL Modello e-mail HTML]**: Modello HTML per l’e-mail. Puoi specificare le variabili in un modello e-mail. Il Passaggio e-mail estrae e visualizza tutte le variabili incluse in un modello per gli input.

**[!UICONTROL Metadati modello e-mail]**: Il valore delle variabili del modello e-mail può essere un valore specificato dall’utente, il percorso di una risorsa sull’autore o sul server di pubblicazione, sull’immagine o su una proprietà di metadati del flusso di lavoro.

* **[!UICONTROL Letterale]**: Utilizza l’opzione quando conosci il valore esatto da specificare. Ad esempio: [example@example.com](mailto:example@example.com).

* **[!UICONTROL Metadati del flusso di lavoro]**: Utilizza l’opzione quando il valore da utilizzare viene salvato in una proprietà di metadati di un flusso di lavoro. Dopo aver selezionato l’opzione , immetti il nome della proprietà metadati nella casella di testo vuota sotto l’opzione Metadati flusso di lavoro . Ad esempio, emailAddress.

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL Immagine]**: Utilizza l’opzione per incorporare un’immagine nell’e-mail. Dopo aver selezionato l&#39;opzione , sfoglia e scegli l&#39;immagine. L’opzione immagine è disponibile solo per i tag immagine (&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />&quot;/>) disponibili nel modello e-mail.&#42;

**[!UICONTROL Indirizzo e-mail del mittente/destinatario]**: Seleziona la **[!UICONTROL Letterale]** opzione per specificare manualmente un indirizzo e-mail o selezionare **[!UICONTROL Recupera dai metadati del flusso di lavoro]** per recuperare l’indirizzo e-mail da una proprietà metadati. È inoltre possibile specificare un elenco di array di proprietà di metadati per **[!UICONTROL Recupera dai metadati del flusso di lavoro]** opzione . Seleziona la **[!UICONTROL Variabile]** per recuperare l’indirizzo e-mail dal valore memorizzato in una variabile di tipo dati stringa.

* **[!UICONTROL File allegato]**: La risorsa disponibile nel percorso specificato viene allegata all’e-mail. Il percorso della risorsa può essere relativo al payload o al percorso assoluto. Un esempio di percorso è [Payload_Directory]/attachment/.

Seleziona la **[!UICONTROL Variabile]** per recuperare l’allegato del file memorizzato in una variabile del tipo di dati Document, XML o JSON.

**[!UICONTROL Nome file]**: Nome del file allegato e-mail. Il Passaggio e-mail modifica il nome file originale dell’allegato al nome file specificato. Il nome può essere specificato manualmente o recuperato da una proprietà di metadati di un flusso di lavoro o da una variabile. Utilizza la **[!UICONTROL Letterale]** quando si conosce il valore esatto da specificare. Utilizza la **[!UICONTROL Variabile]** per recuperare il nome del file dal valore memorizzato in una variabile di tipo dati stringa. Utilizza la **[!UICONTROL Recupera da un metadati del flusso di lavoro]** quando il valore da utilizzare viene salvato in una proprietà di metadati del flusso di lavoro.

## Passaggio Genera documento di record {#generate-document-of-record-step}

Quando un modulo viene compilato o inviato, è possibile conservare un record del modulo, in formato cartaceo o documento. Questo record è denominato documento di registrazione (DoR). È possibile utilizzare il passaggio Genera documento di record per creare una versione PDF interattiva o di sola lettura di un modulo adattivo. La versione PDF contiene informazioni inserite nel modulo insieme al layout del modulo adattivo.

Il passaggio Documento di record ha le seguenti proprietà:

**[!UICONTROL Usa modulo adattivo]**: Specificare il metodo per individuare il modulo adattivo di input. Puoi utilizzare il Modulo adattivo inviato al flusso di lavoro, disponibile in un percorso assoluto o disponibile in un percorso in una variabile. È possibile utilizzare una variabile del tipo di dati String per specificare il percorso nel **[!UICONTROL Selezionare la variabile da risolvere]** campo .\
Puoi associare più Forms adattivo a un flusso di lavoro. Di conseguenza, è possibile specificare un Modulo adattivo in fase di esecuzione utilizzando i metodi di input disponibili.

**[!UICONTROL Percorso modulo adattivo]**: Specifica il percorso del modulo adattivo. Il campo è disponibile quando selezioni la **[!UICONTROL Disponibile in un percorso assoluto]** dall&#39;opzione **[!UICONTROL Usa modulo adattivo]** campo .

**[!UICONTROL Seleziona i dati di input utilizzando]**: Percorso dei dati di input per il modulo adattivo. È possibile mantenere i dati in una posizione relativa al payload, specificare un percorso assoluto dei dati o recuperare i dati memorizzati in una variabile di tipo Document, JSON o XML. I dati di input vengono uniti al modulo adattivo per creare un documento di record.

**[!UICONTROL Selezionare il percorso dell&#39;allegato di input utilizzando]**: Percorso degli allegati. Questi allegati sono inclusi nel documento di registrazione. È possibile mantenere gli allegati in una posizione relativa al payload, specificare un percorso assoluto degli allegati o recuperare gli allegati memorizzati in una variabile di tipo di dati Documento.

Se si specifica il percorso di una cartella, ad esempio gli allegati, tutti i file direttamente disponibili nella cartella vengono allegati al documento di record. Se sono disponibili file nelle cartelle direttamente disponibili nel percorso allegato specificato, i file sono inclusi nel documento di registrazione come allegati. Se sono presenti cartelle in cartelle direttamente disponibili, queste vengono ignorate.

**[!UICONTROL Salva documento di record generato utilizzando le opzioni seguenti]**: Specificare il percorso in cui conservare un file del documento di record. È possibile scegliere di sovrascrivere la cartella payload, posizionare il documento di record in una posizione all’interno della directory di payload o archiviare il documento di record in una variabile di tipo di dati Documento.

**[!UICONTROL Impostazioni internazionali]**: Specificare la lingua del documento di record. Seleziona **[!UICONTROL Letterale]** per selezionare le impostazioni internazionali da un elenco a discesa o selezionare **[!UICONTROL Variabile]** per recuperare le impostazioni internazionali dal valore memorizzato in una variabile di tipo dati stringa. È necessario definire il codice delle impostazioni internazionali quando si memorizza il valore delle impostazioni internazionali in una variabile. Ad esempio, specifica **en_US** per inglese e **fr_FR** per il francese.

## Richiama passaggio DDX {#invokeddx}

Document Description XML (DDX) è un linguaggio di markup dichiarativo i cui elementi rappresentano blocchi predefiniti di documenti. Questi blocchi predefiniti includono documenti PDF e XDP e altri elementi quali commenti, segnalibri e testo con stili. DDX definisce un set di operazioni, che può essere applicato su uno o più documenti di input per generare uno o più documenti di output.  Un singolo DDX può essere utilizzato con una serie di documenti sorgente. È possibile utilizzare ***Richiama passaggio DDX*** in un flusso di lavoro di AEM per eseguire varie operazioni, come Assembling Disassembling Documents, Creating e edit Acrobat e XFA Forms, e altre descritte in [Documentazione di riferimento DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

Richiama il passaggio DDX con le seguenti proprietà:

**[!UICONTROL Documenti di input]**: Utilizzato per impostare le proprietà di un documento di input. Varie opzioni disponibili in questa scheda sono:
* **[!UICONTROL Specifica DDX utilizzando]**: Specifica il documento di input relativo al payload, presenta un percorso assoluto, può essere fornito come payload o memorizzato in una variabile di tipo di dati Documento.
* **[!UICONTROL Crea mappa da payload]**: Aggiungi tutti i documenti sotto la cartella payload alla mappa del documento di input per l’API di chiamata in Assembler. Il nome del nodo di ciascun documento viene utilizzato come chiave nella mappa.
* **[!UICONTROL Mappa del documento di input]**: L&#39;opzione viene utilizzata per aggiungere più voci utilizzando **[!UICONTROL AGGIUNGI]** pulsante . Ogni voce rappresenta la chiave del documento nella mappa e nell’origine del documento.

**[!UICONTROL Opzioni ambiente]**: Questa opzione viene utilizzata per impostare le impostazioni di elaborazione per l’API di chiamata. Varie opzioni disponibili in questa scheda sono:
* **[!UICONTROL Convalida solo]**: Verifica la validità del documento DDX di input.
* **[!UICONTROL Errore]**: Valore booleano per indicare se il servizio API di chiamata non riesce, in caso di errore o meno. Per impostazione predefinita, il relativo valore è impostato su False.
* **[!UICONTROL Numero di Bates]**: Specifica il numero, che si auto-incrementa. Questo numero con incremento automatico viene visualizzato automaticamente su ogni pagina consecutiva.
* **[!UICONTROL Stile predefinito]**: Imposta lo stile predefinito per il file di output.

>[!NOTE]
>
>Le opzioni dell’ambiente vengono mantenute sincronizzate con le API HTTP.

**[!UICONTROL Documenti di output]**: Specifica il percorso in cui salvare il file di output. Varie opzioni disponibili in questa scheda sono:
* **[!UICONTROL Salva output nel payload]**: Salva i documenti di output sotto la cartella payload o sovrascrive il payload, nel caso in cui il payload sia un file.
* **[!UICONTROL Mappa del documento di output]**: Specifica il percorso in cui salvare esplicitamente ogni file di documento, aggiungendo una voce per documento. Ogni voce rappresenta il documento e il percorso, dove salvarlo. Se sono presenti più documenti di output, viene utilizzata questa opzione.

## Passaggio Invoca il servizio del modello dati del modulo {#invoke-form-data-model-service-step}

È possibile utilizzare [[!DNL AEM Forms] Integrazione dei dati](data-integration.md) per configurare e connettersi a origini dati diverse. Queste origini dati possono essere un servizio Web, un servizio REST, un servizio OData e una soluzione CRM. [!DNL AEM Forms] L’integrazione dei dati consente di creare un modello dati modulo che include vari servizi per eseguire operazioni di recupero, aggiunta e aggiornamento dei dati sul database configurato. È possibile utilizzare **[!UICONTROL Richiama del passaggio Servizio del modello dati]** per selezionare un modello dati modulo (FDM) e utilizzare i servizi di FDM per recuperare, aggiornare o aggiungere dati a origini dati diverse.

Per spiegare gli input per i campi del passaggio , come esempio vengono utilizzati la seguente tabella di database e il file JSON :

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

Il passaggio Invoke Form Data Model Service presenta i campi elencati di seguito per facilitare le operazioni del Form Data Model:

* **[!UICONTROL Titolo]**: Titolo del passaggio. Consente di identificare il passaggio nell’editor del flusso di lavoro.
* **[!UICONTROL Descrizione]**: Spiegazione utile per altri sviluppatori di processi quando lavori in un ambiente di sviluppo condiviso.

* **[!UICONTROL Percorso modello dati modulo]**: Individuare e selezionare un modello dati modulo presente sul server.

* **[!UICONTROL Errori e convalide]**: L’opzione ti consente di acquisire messaggi di errore e specificare le opzioni di convalida per i dati recuperati e inviati a origini dati. Con queste modifiche, è possibile garantire che i dati passati al passaggio Invoke Form Data Model Service aderiscano ai vincoli dati definiti dall’origine dati. Per ulteriori dettagli, consulta [Convalida automatizzata dei dati di input](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL Livello di convalida]**: Sono disponibili tre categorie di convalide: Base, Completo e OFF:

   * Completo: Vengono convalidati tutti i vincoli.
   * Base: Solo vincoli obbligatori e nullable
   * OFF Non viene eseguita alcuna convalida.

* **[!UICONTROL Termina flusso di lavoro in caso di errore]**: Quando un vincolo non viene convalidato, il flusso di lavoro viene interrotto.

* **[!UICONTROL Memorizza il codice di errore nella variabile]**: È possibile memorizzare un codice di errore in un [Variabile del tipo di stringa](variable-in-aem-workflows.md).

* **[!UICONTROL Archiviare il messaggio di errore nella variabile]**: È possibile memorizzare un messaggio di errore in un [Variabile del tipo di stringa](variable-in-aem-workflows.md).

* **[!UICONTROL Memorizza dettagli errore in variabile]**: È possibile memorizzare un dettaglio di errore in una [Variabile del tipo JSON](variable-in-aem-workflows.md).

* **[!UICONTROL Servizio]**: Elenco dei servizi forniti dal modello dati modulo selezionato.
* **[!UICONTROL Input per i servizi]** > **[!UICONTROL Fornire i dati di input utilizzando i metadati letterali, variabili o flussi di lavoro e un file JSON]**: Un servizio può avere più argomenti. Seleziona l’opzione per ottenere il valore degli argomenti del servizio da una proprietà dei metadati di un flusso di lavoro, un oggetto JSON, una variabile o immetti direttamente il valore nella casella di testo fornita:

   * **[!UICONTROL Letterale]**: Utilizza l’opzione quando conosci il valore esatto da specificare. Ad esempio, srose@we.info.
   * **[!UICONTROL Variabile]**: Utilizza l’opzione per recuperare il valore memorizzato in una variabile.
   * **[!UICONTROL Recupera dai metadati del flusso di lavoro]**: Utilizza l’opzione quando il valore da utilizzare viene salvato in una proprietà di metadati di un flusso di lavoro. Ad esempio, emailAddress.

   * **[!UICONTROL Relativo al payload]**: Utilizzare l&#39;opzione per recuperare l&#39;allegato salvato in un percorso relativo al payload. Selezionare l&#39;opzione e specificare il nome della cartella che include l&#39;allegato o specificare il nome dell&#39;allegato del file nella casella di testo.

      Ad esempio, se la cartella Relativo a Payload nell&#39;archivio CRX include un allegato al `attachment\attachment-folder` posizione, specificare `attachment\attachment-folder` nella casella di testo dopo aver selezionato il **[!UICONTROL Relativo al payload]** opzione .

   * **[!UICONTROL Notazione punto JSON]**: Utilizza l’opzione quando il valore da utilizzare si trova in un file JSON. Ad esempio, Insurance.customerDetails.emailAddress. L’opzione Notazione punto JSON è disponibile solo se è selezionata l’opzione Mappa campi di input dall’input JSON di input.
   * **[!UICONTROL Mappare i campi di input da JSON di input]**: Specifica il percorso di un file JSON per ottenere il valore di input di alcuni argomenti di servizio dal file JSON. Il percorso del file JSON può essere relativo al payload, a un percorso assoluto, oppure è possibile selezionare un documento JSON di input utilizzando una variabile di tipo JSON o Form Data Model.

* **[!UICONTROL Input per i servizi]** > **[!UICONTROL Fornire dati di input utilizzando una variabile o un file JSON]**: Seleziona l’opzione per ottenere i valori per tutti gli argomenti da un file JSON salvato in un percorso assoluto, in un percorso relativo al payload o in una variabile.
* **[!UICONTROL Seleziona il documento JSON di input utilizzando]**: Il file JSON contenente i valori per tutti gli argomenti del servizio. Il percorso del file JSON può essere **[!UICONTROL relativo al payload]** o **[!UICONTROL percorso assoluto]**. È inoltre possibile recuperare il documento JSON di input utilizzando una variabile di tipo JSON o Form Data Model.

* **[!UICONTROL Notazione punto JSON]**: Lascia vuoto il campo per utilizzare tutti gli oggetti del file JSON specificato come input per gli argomenti del servizio. Per leggere un oggetto JSON specifico dal file JSON specificato come input per gli argomenti del servizio, specifica la notazione del punto per l’oggetto JSON, ad esempio, se disponi di un JSON simile a quello elencato all’inizio della sezione, specifica Insurance.customerDetails per fornire tutti i dettagli di un cliente come input al servizio.
* **[!UICONTROL Uscita del servizio]** > **[!UICONTROL Mappare e scrivere i valori di output su variabili o metadati]**: Seleziona l&#39;opzione per salvare i valori di output come proprietà del nodo di metadati dell&#39;istanza del flusso di lavoro in crx-repository. Specifica il nome della proprietà metadati e seleziona l&#39;attributo di output del servizio corrispondente da mappare con la proprietà metadati, ad esempio, mappa il numero_telefono restituito dal servizio di output con la proprietà numero_telefono dei metadati del flusso di lavoro. Analogamente, è possibile memorizzare l&#39;output in una variabile di tipo Long. Quando selezioni una proprietà per la **[!UICONTROL Attributo di output del servizio da mappare]** solo le variabili in grado di memorizzare i dati della proprietà selezionata vengono compilate per **[!UICONTROL Salva l’output in]** opzione .

* **[!UICONTROL Uscita del servizio]** > **[!UICONTROL Salvare l’output su una variabile o un file JSON]**: Seleziona l’opzione per salvare i valori di output in un file JSON in un percorso assoluto, in un percorso relativo al payload o in una variabile .
* **[!UICONTROL Salva il documento JSON di output utilizzando le seguenti opzioni]**: Salva il file JSON di output. Il percorso del file JSON di output può essere relativo al payload o a un percorso assoluto. Puoi anche salvare il file JSON di output utilizzando una variabile di tipo JSON o Form Data Model.

## Passaggio Firma documento {#sign-document-step}

Il passaggio Firma documento consente di utilizzare [!DNL Adobe Sign] per firmare documenti. Quando utilizzi [!DNL Adobe Sign] Passaggio del flusso di lavoro per firmare un modulo adattivo, il modulo può essere trasmesso tra i firmatari uno dopo l’altro o può essere inviato simultaneamente a tutti i firmatari, a seconda della configurazione del passaggio del flusso di lavoro. [!DNL Adobe Sign] Adaptive Forms abilitato viene inviato a Experience Manager Forms Server solo dopo che tutti i firmatari hanno completato il processo di firma.

Per impostazione predefinita, la [!DNL Adobe Sign] I servizi di pianificazione controllano (sondaggi) la risposta del firmatario dopo ogni 24 ore. È possibile [modifica dell&#39;intervallo predefinito per l&#39;ambiente](adobe-sign-integration-adaptive-forms.md##configure-adobe-sign-scheduler-to-sync-the-signing-status).

Il passaggio Firma documento ha le seguenti proprietà:

* **[!UICONTROL Nome del contratto]**: Specifica il titolo del contratto. Il nome del contratto fa parte dell’oggetto e del corpo del messaggio e-mail inviato ai firmatari. È possibile memorizzare il nome in una variabile di tipo dati String oppure selezionare **[!UICONTROL Letterale]** per aggiungere manualmente il nome.

* **[!UICONTROL Impostazioni internazionali]**: Specifica la lingua per le opzioni di e-mail e verifica. È possibile memorizzare le impostazioni internazionali in una variabile di tipo dati String oppure selezionare **[!UICONTROL Letterale]** per scegliere le impostazioni internazionali dall’elenco delle opzioni disponibili. È necessario definire il codice delle impostazioni internazionali quando si memorizza il valore delle impostazioni internazionali in una variabile. Ad esempio, specifica **[!UICONTROL en_US]** per inglese e **[!UICONTROL fr_FR]** per il francese.

* **[!UICONTROL Configurazione di Adobe Sign Cloud]**: Scegli un [!DNL Adobe Sign] Configurazione cloud. Se non hai configurato [!DNL Adobe Sign] per [!DNL AEM Forms], vedi [Integrare Adobe Sign con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL Selezionare il documento da firmare utilizzando]**: È possibile scegliere un documento da una posizione relativa al payload, utilizzare il payload come documento, specificare un percorso assoluto del documento o recuperare il documento memorizzato in una variabile di tipo Dati documento.
* **[!UICONTROL Giorni fino alla scadenza]**: Un documento viene contrassegnato come scaduto (superato il termine) dopo che non vi è alcuna attività sull&#39;attività per il numero di giorni specificato nel **[!UICONTROL Giorni fino alla scadenza]** campo . Il numero di giorni viene conteggiato dopo che il documento è stato assegnato a un utente per la firma.
* **[!UICONTROL Frequenza e-mail promemoria]**: Puoi inviare un messaggio e-mail di promemoria a intervalli giornalieri o settimanali. La settimana viene conteggiata dal giorno in cui il documento viene assegnato a un utente per la firma.
* **[!UICONTROL Processo di firma]**: È possibile scegliere di firmare un documento in ordine sequenziale o parallelo. In ordine sequenziale, un firmatario riceve il documento alla volta per la firma. Al termine della firma del documento da parte del primo firmatario, il documento viene inviato al secondo firmatario e così via. In ordine parallelo, più firmatari possono firmare un documento alla volta.
* **[!UICONTROL URL di reindirizzamento]**: Specifica un URL di reindirizzamento. Dopo aver firmato il documento, è possibile reindirizzare l’assegnatario a un URL. Di solito, questo URL contiene un messaggio di ringraziamento o ulteriori istruzioni.
* **[!UICONTROL Fase del flusso di lavoro]**: Un flusso di lavoro può avere più fasi. Queste fasi vengono visualizzate nella casella in entrata AEM. È possibile definire queste fasi nelle proprietà del modello ( **[!UICONTROL Barra laterale]** > **[!UICONTROL Pagina]** > **[!UICONTROL Proprietà pagina]** > **[!UICONTROL Fasi]**).
* **[!UICONTROL Seleziona firmatari]**: Specificare il metodo per scegliere i firmatari per il documento. Puoi assegnare dinamicamente il flusso di lavoro a un utente o a un gruppo oppure aggiungere manualmente i dettagli di un firmatario.
* **[!UICONTROL Script o servizio per selezionare i firmatari]**: L’opzione è disponibile solo se nel campo Seleziona firmatari è selezionata l’opzione Dinamicamente . È possibile specificare uno script ECMAScript o un servizio per scegliere i firmatari e le opzioni di verifica di un documento.
* **[!UICONTROL Dettagli del firmatario]**: L’opzione è disponibile solo se l’opzione Manualmente è selezionata nel campo Seleziona firmatari . Specifica l’indirizzo e-mail e scegli un meccanismo di verifica facoltativo. Prima di selezionare un meccanismo di verifica in due fasi, assicurati che l’opzione di verifica corrispondente sia abilitata per il [!DNL Adobe Sign] conto. È possibile utilizzare una variabile del tipo di dati Stringa per definire i valori dei campi E-mail, Codice paese e Numero di telefono. I campi Codice paese e Numero di telefono vengono visualizzati solo se si seleziona Verifica telefono dall’elenco a discesa di verifica in due passaggi.

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
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.
    -->

## Genera passaggio di output stampato {#generatePrintedOutput}

Il passaggio genera un output PCL, PostScript, ZPL, IPL, TPCL o DPL in base a una struttura del modulo e a un file di dati. Il file di dati viene unito alla struttura del modulo e formattato per la stampa. L&#39;output generato da questo passaggio può essere inviato direttamente a una stampante o salvato come file. Si consiglia di utilizzare questo passaggio quando si desidera utilizzare le strutture del modulo o i dati provenienti da un&#39;applicazione. Se le strutture del modulo o le strutture del modulo si trovano in una posizione di rete, in un file system locale o in una posizione HTTP, utilizzare l&#39;operazione generaStampaOutput.

Ad esempio, l’applicazione richiede l’unione di una struttura del modulo con un file di dati. I dati contengono centinaia di record. Inoltre, richiede l&#39;invio dell&#39;output a una stampante che supporti ZPL. La struttura del modulo e i dati di input si trovano in un’applicazione. Utilizzare l&#39;operazione generatePraintOutput per unire ogni record con una struttura del modulo e inviare l&#39;output a una stampante che supporti ZPL.

Il passaggio Genera output stampato ha le seguenti proprietà:

**[!UICONTROL Proprietà di input]**

* **[!UICONTROL Seleziona il file modello utilizzando]**: Specifica il percorso del file modello. È possibile selezionare il file modello utilizzando il percorso relativo al payload, salvato in un percorso assoluto o utilizzando una variabile del tipo di dati Documento. Ad esempio: [Payload_Directory]/Workflow/data.xml. Se il percorso non esiste in crx-repository, un amministratore può creare il percorso prima di utilizzarlo. Inoltre, puoi anche accettare payload come file di dati di input.

* **[!UICONTROL Seleziona il documento dati utilizzando]**: Specifica il percorso di un file di dati di input. È possibile selezionare il file di dati di input utilizzando il percorso relativo al payload, salvato in un percorso assoluto o utilizzando una variabile del tipo di dati Documento. Ad esempio: [Payload_Directory]/Workflow/data.xml. Se il percorso non esiste in crx-repository, un amministratore può creare il percorso prima di utilizzarlo.

* **[!UICONTROL Formato stampante]**: Valore di formato di stampa che specifica il linguaggio di descrizione della pagina da utilizzare, quando non viene fornito un file XDC, per generare il flusso di output. Se si specifica un valore letterale, selezionare uno dei seguenti valori:

   * **[!UICONTROL PCL a colori]**: Utilizzare l&#39;opzione per specificare un file XDC per PCL.
   * **[!UICONTROL PostScript generico]**: Utilizzare l&#39;opzione per specificare un file XDC generico per PostScript.
   * **[!UICONTROL ZPL 300 DPI]**: Utilizzare ZPL 300 DPI. Viene utilizzato zpl300.xdc.
   * **[!UICONTROL ZPL 600 DPI]**: Utilizzare ZPL 600 DPI. Viene utilizzato il file zpl600.xdc.
   * **[!UICONTROL IPL 300 DPI]**: Utilizzare IPL 300 DPI. Viene utilizzato ipl300.xdc.
   * **[!UICONTROL IPL 400 DPI]**: Utilizzare IPL 400 DPI. Viene utilizzato il file ipl400.xdc.
   * **[!UICONTROL TPCL 600 DPI]**: Utilizzare TPCL 600 DPI. Viene utilizzato il file tpcl600.xdc.
   * **[!UICONTROL Plain PostScript]**: Utilizzare l&#39;opzione per specificare un file XDC di testo normale per PostScript.
   * **[!UICONTROL DPL300DPI]**: Utilizzare DPL 300 DPI. Viene utilizzato dpl300.xdc.
   * **[!UICONTROL DPL400DPI]**: Utilizzare DPL 400 DPI. Viene utilizzato dpl400.xdc.
   * **[!UICONTROL DPL600DPI]**: Utilizzare DPL 600 DPI. Viene utilizzato dpl600.xdc.
   * **[!UICONTROL HP_PCL_5e]**: Utilizza l’opzione per supportare più dispositivi Canon.


**[!UICONTROL Proprietà di output]**

* **[!UICONTROL Salva documento di output utilizzando]**: Specificare il percorso in cui salvare il file di output. È possibile salvare il file di output in una posizione relativa al payload, in una variabile, oppure specificare una posizione assoluta per salvare il file di output. Se il percorso non esiste in crx-repository, un amministratore può creare il percorso prima di utilizzarlo.

**[!UICONTROL Proprietà avanzate]**

* **[!UICONTROL Selezionare la posizione principale del contenuto utilizzando]**: La directory principale del contenuto è un valore stringa che specifica l’URI, il riferimento assoluto o la posizione nell’archivio per recuperare le risorse relative utilizzate dalla struttura del modulo. Ad esempio, se la struttura del modulo fa riferimento a un’immagine relativamente, ad esempio ../myImage.gif, myImage.gif deve trovarsi all’indirizzo repository://. Il valore predefinito è repository://, che punta al livello principale dell&#39;archivio.

   Quando selezioni una risorsa dall&#39;applicazione, il percorso URI della directory principale contenuto deve avere la struttura corretta. Ad esempio, se un modulo viene prelevato da un&#39;applicazione denominata SampleApp e viene posizionato in SampleApp/1.0/forms/Test.xdp, l&#39;URI della directory principale del contenuto deve essere specificato come repository://administrator@password/Applications/SampleApp/1.0/forms/ o repository:/Applications/SampleApp/1.0/forms/ (quando l&#39;autorità è null). Quando l’URI della directory principale contenuto viene specificato in questo modo, i percorsi di tutte le risorse di riferimento nel modulo verranno risolti rispetto a questo URI.

* **[!UICONTROL Seleziona il file XCI utilizzando]**: I file XCI vengono utilizzati per descrivere i font e altre proprietà utilizzati per gli elementi della struttura del modulo. È possibile mantenere un file XCI relativo al payload, in un percorso assoluto o utilizzando una variabile del tipo di dati Documento.

* **[!UICONTROL Impostazioni internazionali]**: Specifica la lingua utilizzata per generare il documento PDF. Se si specifica un valore letterale, selezionare una lingua dall’elenco o selezionare uno dei seguenti valori:
   * **[!UICONTROL Per utilizzare le impostazioni predefinite del server]**: (Impostazione predefinita) Utilizza le impostazioni internazionali configurate nella [!DNL AEM Forms] Server. Le impostazioni internazionali sono configurate mediante la console di amministrazione. (Vedi [Guida di Designer](http://www.adobe.com/go/learn_aemforms_designer_65).)

   * **[!UICONTROL Per utilizzare un valore personalizzato]**: Digitare il codice di impostazione internazionale nella casella letterale oppure selezionare una variabile di stringa contenente il codice di impostazione internazionale. Per un elenco completo dei codici locali supportati, consulta http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copie]**: Un valore intero che specifica il numero di copie da generare per l&#39;output. Il valore predefinito è 1.

* **[!UICONTROL Stampa fronte retro]**: Valore di impaginazione che specifica se utilizzare la stampa fronte/retro o fronte/retro. Le stampanti che supportano PostScript e PCL utilizzano questo valore.Se si fornisce un valore letterale, selezionare uno dei seguenti valori:
   * **[!UICONTROL Doppio lato lungo]**: Utilizzare la stampa e la stampa fronte/retro utilizzando l&#39;impaginazione a lungo termine.
   * **[!UICONTROL Bordo corto duplex]**: Utilizzare la stampa e la stampa fronte/retro utilizzando l’impaginazione a bordi brevi.
   * **[!UICONTROL Simplex]**: Utilizzare la stampa su un solo lato.

## Passaggio Genera output PDF non interattivo   {#generatePDFdocuments}

1. Trascina il flusso di lavoro Genera output PDF non interattivo nella scheda Forms Workflow nella barra laterale.
1. Fai doppio clic sul passaggio del flusso di lavoro aggiunto per modificare il componente.
1. Nella finestra di dialogo Modifica componente, configura documenti di input, documenti di output e parametri aggiuntivi e fai clic su **[!UICONTROL OK]**.

### Documenti di input {#input-documents-3}

* **File modello**: Specifica la posizione del modello XDP. È un campo obbligatorio.

* **Documento dati**: Specifica la posizione del file xml di dati da unire al modello.

### Documento di output {#output-document}

**Documento di output**: Specifica il nome del modulo PDF generato.

### Parametri aggiuntivi {#additional-parameters-1}

* **Directory principale dei contenuti**: Specifica il percorso della cartella nell&#39;archivio in cui sono archiviati i frammenti o le immagini utilizzati nel modello XDP di input.
* **Impostazioni internazionali**: Specifica le impostazioni internazionali predefinite per il modulo PDF generato.
* **Versione Acrobat**: Specifica la versione Acrobat di destinazione per il modulo PDF generato.
* **PDF lineare**: Specifica se ottimizzare il PDF generato per la visualizzazione Web.
* **PDF con tag**: Specifica se rendere accessibile il PDF generato.
* **Documento XCI**: Specifica il percorso del file XCI.
