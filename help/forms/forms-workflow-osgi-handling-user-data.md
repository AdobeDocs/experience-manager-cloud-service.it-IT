---
title: Flussi di lavoro incentrati su Forms su OSGi | Gestione dei dati utente
description: Flussi di lavoro incentrati su Forms su OSGi | Gestione dei dati utente
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 1%

---


# Flussi di lavoro incentrati su Forms su OSGi | Gestione dei dati utente {#forms-centric-workflows-on-osgi-handling-user-data}

I flussi di lavoro AEM incentrati su Forms consentono di automatizzare i processi aziendali basati su Forms. I flussi di lavoro sono costituiti da una serie di passaggi eseguiti in un ordine specificato nel modello di flusso di lavoro associato. Ogni passaggio esegue un’azione specifica, ad esempio l’assegnazione di un’attività a un utente o l’invio di un messaggio e-mail. I flussi di lavoro possono interagire con le risorse nel repository, gli account utente e i servizi. Pertanto, i flussi di lavoro possono coordinare attività complicate che coinvolgono qualsiasi aspetto di Experience Manager.

Un flusso di lavoro incentrato sui moduli può essere attivato o avviato tramite uno dei seguenti metodi:

* Invio di una domanda dalla casella in entrata AEM
* Invio di un&#39;applicazione dall&#39;app [!DNL Forms] dell&#39;AEM
* Invio di un modulo adattivo
* Utilizzo di una cartella controllata
* Invio di una comunicazione interattiva o di una lettera

Per ulteriori informazioni sui flussi di lavoro e le funzionalità dell&#39;AEM incentrati su Forms, vedere [Flusso di lavoro incentrato su Forms in OSGi](aem-forms-workflow.md).

## Dati utente e archivi dati {#user-data-and-data-stores}

Quando viene attivato un flusso di lavoro, viene generato automaticamente un payload per l’istanza di flusso di lavoro. A ogni istanza del flusso di lavoro viene assegnato un ID istanza univoco e un ID payload associato. Il payload contiene le posizioni dell’archivio per i dati utente e del modulo associati a un’istanza del flusso di lavoro. Inoltre, le bozze e i dati storici di un’istanza del flusso di lavoro vengono memorizzati anche nell’archivio dell’AEM.

I percorsi predefiniti dell’archivio in cui risiedono il payload, le bozze e la cronologia di un’istanza del flusso di lavoro sono i seguenti:

>[!NOTE]
>
>È possibile configurare posizioni diverse per memorizzare i dati di payload, bozza e cronologia durante la creazione di un flusso di lavoro o di un’applicazione. Per identificare le posizioni in cui un flusso di lavoro o un&#39;applicazione ha memorizzato i dati, esaminare il flusso di lavoro.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><b>AEM 6.4 [!DNL Forms]</b></td>
   <td><b>AEM 6.3 [!DNL Forms]</b></td>
  </tr>
  <tr>
   <td><strong>Istanza <br /> del flusso di lavoro</strong></td>
   <td>/var/workflow/instances/[server_id]/&lt;data&gt;/[workflow-instance]/</td>
   <td>/etc/workflow/instances/[server_id]/[data]/[workflow-instance]/</td>
  </tr>
  <tr>
   <td><strong>Payload</strong></td>
   <td>/var/fd/dashboard/payload/[id_server]/[data]/<br /> [id-payload]/</td>
   <td>/etc/fd/dashboard/payload/[id_server]/[data]/<br /> [id-payload]/</td>
  </tr>
  <tr>
   <td><strong>Bozze</strong></td>
   <td>/var/fd/dashboard/instances/[id_server]/<br /> [data]/[istanza-flusso di lavoro]/draft/[elemento_lavoro]/</td>
   <td>/etc/fd/dashboard/instances/[id_server]/<br /> [data]/[istanza-flusso di lavoro]/draft/[elemento_lavoro]/</td>
  </tr>
  <tr>
   <td><strong>Cronologia</strong></td>
   <td>/var/fd/dashboard/instances/[id_server]/<br /> [data]/[istanza_flusso di lavoro]/history/</td>
   <td>/etc/fd/dashboard/instances/[id_server]/<br /> [data]/[istanza_flusso di lavoro]/history/</td>
  </tr>
 </tbody>
</table>

## Accedere ed eliminare i dati utente {#access-and-delete-user-data}

Puoi accedere ed eliminare i dati utente da un’istanza del flusso di lavoro nell’archivio. A questo scopo, è necessario conoscere l’ID istanza dell’istanza del flusso di lavoro associata all’utente. Per trovare l’ID istanza di un’istanza del flusso di lavoro, utilizza il nome utente dell’utente che ha avviato l’istanza del flusso di lavoro o che è l’assegnatario corrente dell’istanza del flusso di lavoro.

Tuttavia, non è possibile identificare o i risultati possono essere ambigui quando si identificano i flussi di lavoro associati a un iniziatore nei seguenti scenari:

* **Flusso di lavoro attivato tramite una cartella controllata**: impossibile identificare un&#39;istanza del flusso di lavoro utilizzando il relativo iniziatore se il flusso di lavoro è attivato da una cartella controllata. In questo caso, le informazioni utente vengono codificate nei dati memorizzati.
* **Flusso di lavoro avviato dall&#39;istanza AEM di pubblicazione**: tutte le istanze del flusso di lavoro vengono create utilizzando un utente del servizio quando Forms adattivo o vengono inviate lettere dall&#39;istanza di pubblicazione AEM. In questi casi, il nome utente dell’utente connesso non viene acquisito nei dati dell’istanza del flusso di lavoro.

### Accedere ai dati utente {#access}

Per identificare e accedere ai dati utente memorizzati per un’istanza del flusso di lavoro, effettua le seguenti operazioni:

1. Nell&#39;istanza dell&#39;autore AEM, vai a `https://'[server]:[port]'/crx/de` e passa a **[!UICONTROL Strumenti > Query]**.

   Selezionare **[!UICONTROL SQL2]** dal menu a discesa **[!UICONTROL Tipo]**.

1. A seconda delle informazioni disponibili, esegui una delle seguenti query:

   * Se l&#39;iniziatore del flusso di lavoro è noto, esegui le operazioni seguenti:

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * Eseguire le operazioni seguenti se l&#39;utente i cui dati si trovano è l&#39;assegnatario del flusso di lavoro corrente:

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   La query restituisce la posizione di tutte le istanze del flusso di lavoro per l&#39;iniziatore del flusso di lavoro specificato o l&#39;assegnatario del flusso di lavoro corrente.

   Ad esempio, la query seguente restituisce il percorso di due istanze del flusso di lavoro dal nodo `/var/workflow/instances` il cui iniziatore del flusso di lavoro è `srose`.

   ![workflow-instance](assets/workflow-instance.png)

1. Passa a un percorso di istanza del flusso di lavoro restituito dalla query. La proprietà status visualizza lo stato corrente dell’istanza del flusso di lavoro.

   ![stato](assets/status.png)

1. Nel nodo dell&#39;istanza del flusso di lavoro, passare a `data/payload/`. La proprietà `path` memorizza il percorso del payload per l&#39;istanza del flusso di lavoro. Puoi passare al percorso per accedere ai dati memorizzati nel payload.

   ![percorso-payload](assets/payload-path.png)

1. Passare alle posizioni per le bozze e la cronologia per l&#39;istanza del flusso di lavoro.

   Ad esempio:

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. Ripeti i passaggi da 3 a 5 per tutte le istanze del flusso di lavoro restituite dalla query al passaggio 2.

   >[!NOTE]
   >
   >L&#39;app AEM [!DNL Forms] memorizza anche i dati in modalità offline. È possibile che i dati di un&#39;istanza del flusso di lavoro siano memorizzati localmente su singoli dispositivi e vengano inviati al server [!DNL Forms] quando l&#39;app si sincronizza con il server.

### Elimina dati utente {#delete-user-data}

Per eliminare i dati utente dalle istanze del flusso di lavoro, è necessario essere un amministratore AEM ed effettuare le seguenti operazioni:

1. Segui le istruzioni in [Accedi ai dati utente](forms-workflow-osgi-handling-user-data.md#access) e prendi nota di quanto segue:

   * Percorsi delle istanze del flusso di lavoro associate all’utente
   * Stato delle istanze del flusso di lavoro
   * Percorsi verso i payload per le istanze del flusso di lavoro
   * Percorsi delle bozze e cronologia delle istanze del flusso di lavoro

1. Esegui questo passaggio per le istanze del flusso di lavoro con stato **RUNNING**, **SUSPENDED** o **STALE**:

   1. Vai a `https://'[server]:[port]'/aem/start.html` e accedi con le credenziali di amministratore.
   1. Passa a **[!UICONTROL Strumenti > Flusso di lavoro> Istanze]**.
   1. Selezionare le istanze di flusso di lavoro rilevanti per l&#39;utente e selezionare **[!UICONTROL Termina]** per terminare le istanze in esecuzione.

      Per ulteriori informazioni sull&#39;utilizzo delle istanze del flusso di lavoro, vedere [Amministrazione delle istanze del flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html#authoring).

1. Vai alla console [!DNL CRXDE Lite], passa al percorso del payload per un&#39;istanza del flusso di lavoro ed elimina il nodo `payload`.
1. Passare al percorso delle bozze per un&#39;istanza del flusso di lavoro ed eliminare il nodo `draft`.
1. Passare al percorso della cronologia per un&#39;istanza del flusso di lavoro ed eliminare il nodo `history`.
1. Passare al percorso dell&#39;istanza del flusso di lavoro per un&#39;istanza del flusso di lavoro ed eliminare il nodo `[workflow-instance-ID]` per il flusso di lavoro.

   >[!NOTE]
   >
   >Se si elimina il nodo dell’istanza del flusso di lavoro, verrà rimossa l’istanza del flusso di lavoro per tutti i partecipanti al flusso di lavoro.

1. Ripeti i passaggi da 2 a 6 per tutte le istanze del flusso di lavoro identificate per un utente.
1. Identificare ed eliminare i dati relativi alle bozze e agli invii non in linea dalla cartella Posta in uscita dell&#39;app [!DNL Forms] dell&#39;AEM dei partecipanti al flusso di lavoro per evitare l&#39;invio al server.

Puoi inoltre utilizzare le API per accedere e rimuovere nodi e proprietà. Per ulteriori informazioni, consulta i seguenti documenti.

* [Accesso a livello di programmazione al JCR per AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/access-jcr.html?lang=en#platform)
* [Rimozione di nodi e proprietà](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [Riferimento API](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/overview-summary.html)

>[!MORELIKETHIS]
>
>* [Utilizza il flusso di lavoro di AEM Forms per l&#39;automazione dei processi aziendali](/help/forms/aem-forms-workflow.md)