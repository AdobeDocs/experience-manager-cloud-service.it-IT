---
title: Domande frequenti su Dynamic Medie con funzionalità OpenAPI
description: Domande frequenti su Dynamic Medie con funzionalità OpenAPI
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# Domande frequenti su Dynamic Medie con funzionalità OpenAPI {#new-dynaminc-media-apis-frequently-asked-questions}

+++**Tutte le risorse nell&#39;as a Cloud Service repository di Experience Manager Assets sono disponibili per la ricerca e la distribuzione tramite Dynamic Medie con funzionalità OpenAPI?**

No, solo [le risorse approvate e la versione più recente](/help/assets/approved-assets.md) sono disponibili per la ricerca e la distribuzione tramite Dynamic Medie con funzionalità OpenAPI, garantendo la coerenza del marchio su tutti i canali e le applicazioni.

+++

+++**In che modo gli amministratori possono contrassegnare come approvate le risorse nuove ed esistenti aggiunte a una cartella?**

Lo stato di una risorsa in Experience Manager Assets è gestito dalla proprietà `jcr:content/metadata/dam:status`. I valori di questa proprietà possono essere:

* Approvato

* Rifiutato

* Modifiche richieste

Experience Manager Assets distingue lo stato Approvato utilizzando ![Approva Assets](assets/thumbs-up-icon.svg) disponibile nella scheda delle risorse, come illustrato nell&#39;immagine seguente:

![Icona per risorse approvate](/help/assets/assets/approved-assets-thumbs-up.png)

Per approvare tutte le risorse in una cartella, consulta le istruzioni su [come approvare in blocco le risorse in una cartella](/help/assets/approved-assets.md#bulk-approve-assets). È inoltre disponibile un video che illustra l&#39;intero processo.

Dopo aver impostato una cartella per l’approvazione in blocco, tutte le nuove risorse aggiunte alla cartella vengono approvate automaticamente. Tutte le risorse esistenti vengono approvate dopo la rielaborazione. Per istruzioni su come rielaborare le risorse, consulta [Rielaborazione delle risorse digitali](/help/assets/reprocessing.md). Se si copiano o si spostano risorse non approvate da qualsiasi altra cartella, è necessario [rielaborare le risorse](/help/assets/reprocessing.md).

La risorsa è contrassegnata come `Rejected`, se l&#39;amministratore specifica `Rejected` o `Changes requested` valori. Experience Manager Assets distingue lo stato Rifiutato utilizzando ![Rifiuta Assets](/help/assets/assets/do-not-localize/reject-assets.svg) disponibile nella scheda delle risorse.

+++

+++**Come si ottiene l&#39;ID utente o gruppo Adobe IMS (Adobe Identity Management Services) da utilizzare per impostare i ruoli delle risorse nella visualizzazione Amministrazione di Experience Manager, al fine di proteggere la consegna e l&#39;esperienza di ricerca?**

Nell’Admin Console di Experience Manager, gli utenti che richiedono l’accesso all’ambiente di authoring di Adobe vengono gestiti come utenti Adobe IMS. Per informazioni sugli utenti Adobe IMS, su come accedervi e gestirli in Admin Console, consulta [Utenti Adobe IMS](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en).

+++

+++**È possibile approvare più risorse contemporaneamente all&#39;interno di una cartella?**

Sì, puoi approvare più risorse contemporaneamente all’interno di una cartella.

Eseguire la procedura seguente per approvare più risorse contemporaneamente in [!DNL Experience Manager Assets]:

1. Seleziona le risorse e fai clic su **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Base]**, scorri verso il basso fino a **[!UICONTROL Stato revisione]**.
1. Cambia lo stato di revisione in **[!UICONTROL Approvato]**.
1. Fai clic su **[!UICONTROL Salva e chiudi]**.

+++

+++**Come posso proteggere la consegna delle risorse e cercare le OpenAPI di Dynamic Medie?**

La governance centrale delle risorse in Experience Manager consente agli amministratori DAM o ai Brand Manager di gestire l’accesso alle risorse. Possono limitare l’accesso configurando i ruoli per le risorse approvate sul lato authoring, in particolare sull’istanza di authoring di AEM as a Cloud Service.

Gli utenti finali che cercano o utilizzano gli URL di consegna possono accedere alle risorse con restrizioni una volta completato il processo di autorizzazione.

Per ulteriori informazioni, vedere [Limitare l&#39;accesso alle risorse nell&#39;Experience Manager](restrict-assets-delivery.md#authoring).

+++

+++**Come puoi ottenere le autorizzazioni per modificare lo stato di approvazione di una risorsa?**

In qualità di utente DAM, potresti non disporre delle autorizzazioni necessarie per [approvare le risorse](approved-assets.md#approve-assets). Per ottenere le autorizzazioni di modifica dello stato di approvazione di una risorsa, gli amministratori possono modificare lo schema di metadati predefinito o qualsiasi altro schema applicato alla cartella delle risorse per fornire le autorizzazioni di modifica al campo **[!UICONTROL Stato revisione]**. Per ulteriori informazioni, vedere [come disabilitare la modifica per il campo Stato revisione](approved-assets.md#configuration).

+++

+++**Quali sono le differenze tra Dynamic Medie con funzionalità OpenAPI e la soluzione Dynamic Medie?**

Dynamic Medie con funzionalità OpenAPI e Dynamic Medie rappresentano soluzioni distinte, ognuna delle quali offre le proprie funzionalità di distribuzione specializzate. È fondamentale rivedere attentamente i requisiti specifici per determinare la soluzione più adatta alle tue esigenze.

Di seguito sono riportate alcune delle principali differenze tra Dynamic Medie con funzionalità OpenAPI e Dynamic Medie:

| Dynamic Medie con funzionalità OpenAPI | Dynamic Media |
|---|---|
| [Disponibile solo con Assets as a Cloud Service](/help/assets/new-dynamic-media-overview.md#prerequisites-new-dynaminc-media-apis) | Disponibile anche con Managed Services on-premise o Adobe con passaggi di configurazione e provisioning aggiuntivi. |
| [Set limitato di modificatori di immagini supportati, ad esempio larghezza, altezza, rotazione, capovolgimento, qualità e formato](/help/assets/deliver-assets-apis.md) | Set completo di modificatori di immagini disponibili |
| [Consegna delle risorse limitata in base a utenti e ruoli](/help/assets/restrict-assets-delivery.md) | Assets pubblicato in Dynamic Medie è accessibile a tutti gli utenti |
| Supporta il ritaglio avanzato delle immagini | Supporta il ritaglio avanzato di immagini e video |
| Stack basato sulle specifiche OpenAPI, con cui la maggior parte degli sviluppatori ha familiarità. L&#39;estensibilità di AEM Assets diventa molto semplice utilizzando [il selettore delle risorse Microsoft Front End](/help/assets/asset-selector.md). | API basate su SOAP, che diventano una barriera durante lo sviluppo di personalizzazioni dell’integrazione. |
| Eventuali modifiche apportate alle risorse approvate in DAM, inclusi gli aggiornamenti della versione e le modifiche ai metadati, vengono automaticamente riportate negli URL di consegna. Con un valore TTL (Time-to-Live) breve di 10 minuti configurato per Dynamic Medie con funzionalità OpenAPI tramite CDN, gli aggiornamenti diventano visibili in meno di 10 minuti su tutte le interfacce di authoring e pubblicazione. | TTL CDN consigliato di 10 ore. Puoi sovrascrivere il valore TTL utilizzando l’azione di annullamento della validità della cache. |
| Solo le risorse approvate sono disponibili per la distribuzione di risorse alle applicazioni a valle, consentendo l’utilizzo di risorse approvate dal marchio nelle esperienze digitali. Le risorse consegnate rispettano lo stato di scadenza delle risorse nell’istanza di authoring dell’archivio AEM as a Cloud Service. | Eventuali aggiornamenti a una risorsa pubblicata su Dynamic Medie vengono pubblicati automaticamente senza alcun flusso di lavoro di approvazione, il che non garantisce la corretta pubblicazione delle risorse approvate dal marchio nelle esperienze digitali. Nessuna scadenza risorsa intrinseca. Una risorsa rimane pubblica finché non viene eliminata dall’archivio AEM as a Cloud Service. |
| Report sull’utilizzo in base al numero di risorse consegnate. | I rapporti sull’utilizzo non sono disponibili. |

+++

+++**In che modo Dynamic Medie con funzionalità OpenAPI risolve i limiti della funzionalità Connected Assets?**

La tabella seguente illustra le principali differenze tra le due soluzioni:

| Dynamic Medie con funzionalità OpenAPI | Risorse collegate |
|---|---|
| Assets sull’implementazione remota di DAM è disponibile su AEM as a Cloud Service. | Assets sull’implementazione remota di DAM può essere disponibile su AEM as a Cloud Service o Managed Services Adobe. |
| I file binari delle risorse non vengono copiati quando le risorse in una distribuzione DAM remota sono disponibili in un’istanza AEM Sites. | I file binari delle risorse vengono copiati quando le risorse in una distribuzione DAM remota sono disponibili in un’istanza AEM Sites. |
| Supporto per tutti i tipi di formati di risorse supportati da AEM Assets. | Nessun supporto per i video. |
| Supporta il ritaglio avanzato dell’immagine. | Supporto per ritagli avanzati e predefiniti immagine di Dynamic Medie. |
| Puoi utilizzare Dynamic Medie nell’implementazione Sites locale durante il recupero delle risorse dall’implementazione remota di DAM. | L’implementazione di Dynamic Medie su Sites locale è di sola lettura. |
| Nessuna restrizione sul numero di istanze AEM Sites connesse a una distribuzione DAM remota. Puoi [limitare l&#39;accesso alle risorse nell&#39;istanza Sites configurando i ruoli](/help/assets/restrict-assets-delivery.md) per le risorse approvate in DAM remoto. | Limitazione per la connessione di non più di 4 istanze di AEM Sites all’implementazione remota di DAM. Un numero maggiore richiede ulteriori test. |
| Sia Asset Selector che Dynamic Medie con funzionalità OpenAPI sono estensibili per consentire integrazioni personalizzate. | Le API di Assets connesse non sono estensibili per consentire integrazioni personalizzate. |
| Eventuali modifiche apportate alle risorse approvate disponibili nell’implementazione remota di DAM, inclusi gli aggiornamenti della versione e le modifiche ai metadati, vengono applicate automaticamente all’istanza di Sites in un breve valore TTL (Time-to-Live) di 10 minuti. | Gli aggiornamenti delle risorse sull’implementazione remota di DAM vengono gestiti automaticamente tramite eventi del ciclo di vita, ma richiedono molto più tempo rispetto a Dynamic Medie con funzionalità OpenAPI. |
| I metadati delle risorse in DAM remoto sono disponibili anche nell’istanza di AEM Sites. | I metadati delle risorse in DAM remoto non sono disponibili nell’istanza di AEM Sites. |

+++



