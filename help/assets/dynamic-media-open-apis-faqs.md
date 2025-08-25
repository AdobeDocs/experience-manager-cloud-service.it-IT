---
title: Domande frequenti su Dynamic Media con funzionalità OpenAPI
description: Domande frequenti su Dynamic Media con funzionalità OpenAPI
role: User
exl-id: 3450e050-4b0b-4184-8e71-5e667d9ca721
source-git-commit: c3bac140c2e0b33cfc206cda7c0591fc75a47a1f
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 83%

---

# Domande frequenti su Dynamic Media con funzionalità OpenAPI {#new-dynaminc-media-apis-frequently-asked-questions}

## Sono disponibili tutte le risorse nell’archivio di Experience Manager Assets as a Cloud Service per la ricerca e la distribuzione tramite Dynamic Media con funzionalità OpenAPI? {#assets-available-for-search}

No, solo [le versioni approvate e più recenti delle risorse](/help/assets/approve-assets.md) sono disponibili per la ricerca e la consegna tramite Dynamic Media con funzionalità OpenAPI, garantendo la coerenza del brand su tutti i canali e le applicazioni.


## In che modo gli amministratori possono contrassegnare come approvate le risorse nuove ed esistenti aggiunte a una cartella? {#add-assets-to-folder-as-approved}

Lo stato di una risorsa in Experience Manager Assets è gestito dalla proprietà `jcr:content/metadata/dam:status`. I valori di questa proprietà possono essere:

* Approvato

* Rifiutato

* Modifiche richieste

Experience Manager Assets distingue lo stato Approvato utilizzando un’apposita icona disponibile nella scheda delle risorse, come illustrato nelle immagini seguenti per le visualizzazioni Amministratore e Risorse:

**Vista amministratore**

![Risorse approvate nella vista Amministratore](/help/assets/assets/approved-assets-thumbs-up.png)

**Vista risorse**

![Risorse approvate nella vista Risorse](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


Per approvare tutte le risorse in una cartella, consulta le istruzioni in [Come approvare in blocco le risorse in una cartella](/help/assets/approve-assets.md#bulk-approve-assets). È inoltre disponibile un video che illustra l’intero processo.

Dopo aver impostato una cartella per l’approvazione in blocco, tutte le nuove risorse aggiunte alla cartella vengono approvate automaticamente. Tutte le risorse esistenti vengono approvate dopo la rielaborazione. Per istruzioni su come rielaborare le risorse, consulta [Rielaborazione delle risorse digitali](/help/assets/reprocessing.md). Se si copiano o si spostano risorse non approvate da qualsiasi altra cartella, è necessario [rielaborare le risorse](/help/assets/reprocessing.md).

La risorsa è contrassegnata come `Rejected`, se l’amministratore specifica i valori `Rejected` o `Changes requested`. Experience Manager Assets distingue lo stato Rifiutato utilizzando ![Rifiuta risorse](/help/assets/assets/do-not-localize/reject-assets.svg) disponibile nella scheda delle risorse nella vista Amministratore.

Allo stesso modo, Experience Manager Assets distingue lo stato Rifiutato nella vista Assets utilizzando il seguente stato Rifiutato sulla scheda della risorsa:

![Risorse rifiutate nella vista Risorse](/help/assets/assets/rejected-assets-admin-view.png)


## Come puoi ottenere l’ID utente o gruppo di Adobe IMS (Adobe Identity Management Services) da utilizzare per impostare i ruoli nelle risorse in Experience Manager Admin View, al fine di garantire la consegna e l’esperienza di ricerca? {#set-roles-secure-delivery-search}

Gli utenti che richiedono l’accesso all’ambiente Experience Manager Author vengono gestiti come utenti di Adobe IMS in Adobe Admin Console. Per informazioni su cosa si intende per utenti di Adobe IMS, nonché come accedervi e gestirli in Admin Console, consulta [Utenti Adobe IMS](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=it).


## È possibile approvare più risorse contemporaneamente all’interno di una cartella? {#approve-multiple-assets-in-folder}

Sì, puoi approvare più risorse contemporaneamente all’interno di una cartella.

Per approvare più risorse contemporaneamente in [!DNL Experience Manager Assets Admin view] esegui la procedura seguente:

1. Seleziona la cartella e fai clic su **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Base]**, scorri verso il basso fino a **[!UICONTROL Stato revisione]**.
1. Cambia lo stato revisione in **[!UICONTROL Approvato]**.
1. Fai clic su **[!UICONTROL Salva e chiudi]**.

Allo stesso modo, per approvare più risorse contemporaneamente all’interno di una cartella nella vista Assets:

1. Seleziona le risorse e fai clic su **[!UICONTROL Modifica metadati in blocco]**.

1. Seleziona **[!UICONTROL Approvato]** nel campo **[!UICONTROL Stato]** disponibile nella sezione [!UICONTROL Proprietà] nel riquadro di destra.

1. Fai clic su **[!UICONTROL Salva]**.


## Come posso proteggere la distribuzione delle risorse e cercare Dynamic Media con OpenAPI? {#secure-asset-delivery}

La governance centrale delle risorse in Experience Manager consente agli amministratori DAM o ai Responsabili del brand di gestire l’accesso alle risorse. Queste figure possono limitare l’accesso configurando i ruoli o impostando il tempo di attivazione e disattivazione delle risorse approvate sul lato authoring, in particolare sull’istanza di authoring di AEM as a Cloud Service.

Gli utenti finali che cercano o utilizzano gli URL di consegna possono accedere alle risorse con restrizioni una volta completato il processo di autorizzazione.

Per ulteriori informazioni, consulta [Limitare l’accesso alle risorse in Experience Manager](restrict-assets-delivery.md#authoring).


## Come puoi ottenere le autorizzazioni per modificare lo stato di approvazione di una risorsa? {#permissions-edit-approval-status}

In qualità di utente DAM, potresti non disporre delle autorizzazioni necessarie per [approvare le risorse](approve-assets.md#approve-assets). Per ottenere le autorizzazioni di modifica dello stato di approvazione di una risorsa, gli amministratori possono modificare lo schema di metadati predefinito o qualsiasi altro schema applicato alla cartella delle risorse in modo da fornire le autorizzazioni di modifica al campo **[!UICONTROL Stato revisione]**. Per ulteriori informazioni, consulta [come disabilitare la modifica per il campo Stato revisione](approve-assets.md#configuration).


## Qual è la dimensione del file supportato per i video? {#supported-file-formats-videos}

Dynamic Media con funzionalità OpenAPI supporta i video a lunga durata. I video supportano fino a 50 GB e 2 ore.


## Quali sono le differenze tra Dynamic Media con funzionalità OpenAPI e la soluzione Dynamic Media? {#dynamic-media-and-dynamic-media-with-openapi-differences}

Dynamic Media con funzionalità OpenAPI e Dynamic Media rappresentano soluzioni distinte, ognuna delle quali offre le proprie caratteristiche di consegna specializzate. È fondamentale rivedere attentamente i requisiti specifici per determinare la soluzione più adatta alle tue esigenze.

Adobe consiglia di utilizzare Dynamic Media con lo stack OpenAPI per tutti i casi di utilizzo dell’integrazione (app di prima parte o di terze parti). Se esiste già un’integrazione con lo stack di Dynamic Media, si consiglia di non modificarla in quanto la struttura degli URL dello stack OpenAPI è diversa. Sfrutta lo stack OpenAPI solo per eventuali nuovi casi d’uso di integrazione. Se il caso d’uso richiede modificatori avanzati che non sono disponibili con lo stack OpenAPI, evita lo stack OpenAPI fino a quando Adobe non avrà colmato questa lacuna. Lo stack OpenAPI può essere valutato anche per la consegna nativa di base dai Servizi cloud di AEM Assets, purché il caso d’uso sia coperto dai modificatori disponibili con lo stack OpenAPI. In conclusione, Dynamic Media e Dynamic Media con stack OpenAPI possono coesistere, a seconda della natura del caso d’uso.

Di seguito sono riportate alcune delle principali differenze tra Dynamic Media con funzionalità OpenAPI e Dynamic Media:

| Dynamic Media con funzionalità OpenAPI | Dynamic Media |
|---|---|
| [Disponibile solo con Assets as a Cloud Service](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | Disponibile anche con On-Premise o Adobe Managed Services con passaggi di configurazione e provisioning aggiuntivi. |
| [Set completo di modificatori di immagini supportati, ad esempio larghezza, altezza, rotazione, capovolgimento, qualità e formato](/help/assets/deliver-assets-apis.md) | Set completo di modificatori di immagini disponibili |
| [Consegna delle risorse limitata in base a utenti, ruoli, data e ora](/help/assets/restrict-assets-delivery.md) | Le risorse pubblicate in Dynamic Media sono accessibili a tutti gli utenti |
| La maggior parte degli sviluppatori ha familiarità con le specifiche OpenAPI. L’estensibilità di AEM Assets diventa molto semplice utilizzando il [Selettore risorse micro front-end](/help/assets/overview-asset-selector.md). | Le API basate su SOAP, diventano una barriera durante lo sviluppo di personalizzazioni dell’integrazione. |
| Eventuali modifiche apportate alle risorse approvate in DAM, inclusi gli aggiornamenti della versione e le modifiche ai metadati, vengono automaticamente riportate negli URL di consegna. Con un valore TTL (Time-to-Live) breve di 10 minuti configurato per Dynamic Media con funzionalità OpenAPI tramite CDN, gli aggiornamenti diventano visibili in meno di 10 minuti su tutte le interfacce di authoring e pubblicazione. | TTL CDN consigliato di 10 ore. Puoi sovrascrivere il valore TTL utilizzando l’azione di annullamento della validità della cache. |
| Solo le risorse approvate sono disponibili per la consegna di risorse alle applicazioni a valle, consentendo l’utilizzo di risorse approvate dal brand nelle esperienze digitali. | Eventuali aggiornamenti a una risorsa Dynamic Media pubblicata vengono applicati automaticamente senza alcun flusso di lavoro di approvazione, il che non garantisce che le risorse nelle esperienze digitali siano approvate dal brand. |
| Report sull’utilizzo in base al numero di risorse consegnate. Questa funzionalità sarà presto disponibile. | I rapporti sull’utilizzo non sono disponibili. Questa funzionalità sarà presto disponibile. |
| Le risorse contrassegnate come Scadute nell’archivio Assets as a Cloud Service non sono più disponibili per le applicazioni a valle. | Nessuna scadenza risorsa intrinseca. Una risorsa rimane pubblica finché non viene eliminata dall’archivio AEM as a Cloud Service. |
| Non supporta le funzionalità di ritaglio avanzato video. | Supporta le funzionalità di ritaglio avanzato video. |
| Codifiche Dynamic Video, che garantiscono che le codifiche migliori al video di input siano basate su server. Non è richiesta alcuna configurazione per la consegna di video nativi. | Lo standard 3 effettua la codifica indipendentemente dal video di input (può influire sulle prestazioni di consegna del video). È necessario impostare manualmente codifiche diverse per bit rate video diverse. |
| Abilita URL protetti e offuscati utilizzando gli UID delle risorse senza compromettere l’SEO (Search Engine Optimization). | Offuscamento URL disponibile solo per i parametri di query URL. Gli ID risorsa (nomi di risorsa) negli URL sono riconoscibili. |


## In che modo Dynamic Media con funzionalità OpenAPI soddisfa le limitazioni della funzione Connected Assets? {#dynamic-media-openapi-addresses-connected-assets-limitations}

La tabella seguente illustra le principali differenze tra le due soluzioni:

| Dynamic Media con funzionalità OpenAPI | Risorse collegate |
|---|---|
| Le risorse su una distribuzione remota di DAM sono disponibili su AEM as a Cloud Service. | Le risorse su una distribuzione remota di DAM possono essere disponibili su AEM as a Cloud Service o Adobe Managed Services. |
| I file binari delle risorse non vengono copiati quando le risorse in una distribuzione DAM remota sono disponibili in un’istanza AEM Sites. | I file binari delle risorse vengono copiati quando le risorse in una distribuzione DAM remota sono disponibili in un’istanza AEM Sites. |
| Supporto per tutti i tipi di formato di risorse supportati da AEM Assets. | Nessun supporto per i video. |
| Puoi utilizzare Dynamic Media nell’implementazione Sites locale durante il recupero delle risorse dalla distribuzione remota di DAM. | L’implementazione di Dynamic Media su Sites locale è di sola lettura. |
| Non ci sono restrizioni sul numero di istanze AEM Sites connesse a una distribuzione DAM remota. Puoi [limitare l’accesso alle risorse nell’istanza Sites configurando i ruoli](/help/assets/restrict-assets-delivery.md) per le risorse approvate in DAM remoto. | Limitazione per la connessione di non più di 4 istanze di AEM Sites alla distribuzione remota di DAM. Un numero maggiore richiede ulteriori test. |
| Sia il Selettore risorse che Dynamic Media con funzionalità OpenAPI sono estensibili per consentire integrazioni personalizzate. | Le API di Assets connesse non sono estensibili per consentire integrazioni personalizzate. |
| Eventuali modifiche apportate alle risorse approvate disponibili nella distribuzione remota di DAM, inclusi gli aggiornamenti della versione e le modifiche ai metadati, vengono applicate automaticamente all’istanza di Sites in un breve TTL (Time-to-Live) di 10 minuti. | Gli aggiornamenti delle risorse sulla distribuzione remota di DAM vengono gestiti automaticamente tramite eventi del ciclo di vita, ma richiedono molto più tempo rispetto a Dynamic Media con funzionalità OpenAPI. |
| I metadati delle risorse in DAM remoto sono disponibili anche nell’istanza di AEM Sites. | I metadati delle risorse in DAM remoto non sono disponibili nell’istanza di AEM Sites. |

## Alcuni modificatori sono contrassegnati come Disponibilità limitata. Come posso iniziare a utilizzarli? {#use-limited-availability-modifiers}

Per abilitare l&#39;utilizzo di produzione di [modificatori in disponibilità limitata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) sul tuo account:

1. [Crea un caso di supporto Adobe utilizzando Admin Console](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).

1. Fai riferimento ai seguenti dettagli all’interno del caso di supporto Adobe:

   * Organizzazione IMS

   * Elenco di modificatori da abilitare


## Come si testano i modificatori sperimentali? {#modifiers-not-generally-available}

Puoi testare qualsiasi modificatore che non è generalmente disponibile tramite API sperimentali. Ad esempio, &lt;/adobe/experiment/advancemodifiers-expires-YYYYMMDD/assets>
Fai clic qui per ulteriori informazioni su come utilizzare le [API sperimentali](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/#experimental-apis) e l&#39;[elenco completo dei modificatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/).
