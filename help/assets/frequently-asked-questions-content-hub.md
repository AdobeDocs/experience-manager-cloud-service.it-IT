---
title: Domande frequenti su Content Hub
description: Ricevi risposte ad alcune delle domande più frequenti su Content Hub.
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1112'
ht-degree: 100%

---

# Domande frequenti su Content Hub {#content-hub-frequently-asked-questions}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Domande frequenti su Content Hub.](assets/content-hub-faqs.png)

>[!AVAILABILITY]
>
>La guida di Content Hub è ora disponibile in formato PDF. Scarica l’intera guida e utilizza l’Assistente IA di Adobe Acrobat per rispondere alle tue domande.
>
>[!BADGE Guida di Content Hub - PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

## Che cos’è Content Hub? {#what-is-content-hub}

Content Hub è una funzione di Adobe Experience Manager Assets as a Cloud Service.

Content Hub consente ai team più grandi di individuare facilmente le risorse approvate e rilevanti tramite un portale intuitivo e di adattarle rapidamente alle proprie esigenze.Inoltre, Content Hub fornisce un meccanismo di acquisizione che consente agli utenti un servizio self-service facile durante il caricamento delle risorse nel DAM. In questo modo si soddisfa direttamente la necessità delle organizzazioni di velocizzare la creazione dei contenuti, preservando al contempo la coerenza del brand e la conformità alle protezioni appropriate.

## Perché non è possibile abilitare Content Hub nel programma/ambiente Cloud Manager? {#cannot-enable-content-hub}

In questo momento, Content Hub è disponibile solo sui programmi di produzione AEM Cloud Manager che includono una licenza Assets (Assets Cloud Service, Assets Ultimate, Assets Prime). Quando fai clic su [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) per abilitarlo, questo viene distribuito e associato all’ambiente di produzione di authoring di AEM in tale programma. Per informazioni dettagliate e prerequisiti, consulta [Distribuire Content Hub](/help/assets/deploy-content-hub.md).

## Ho abilitato Content Hub nel mio programma/ambiente di produzione, posso disattivarlo? {#can-i-disable-content-hub}

L’abilitazione di Content Hub in un programma di produzione lo implementa come parte dell’infrastruttura di produzione. AEM Cloud Manager non consente di rimuovere o disabilitare l’infrastruttura di produzione per ridurre al minimo i rischi di errori umani nell’utilizzo della produzione.

Se non desideri fornire Content Hub agli utenti una volta implementato, non assegnare alcun utente al profilo di prodotto Content Hub in Admin Console. Per ulteriori dettagli, consulta [Distribuire Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile).

## Come posso valutare Content Hub nella mia organizzazione dato che è disponibile solo per programmi di produzione/ambienti di authoring e di produzione? {#how-can-i-evaluate-content-hub}

Content Hub è una funzione fornita e gestita da Adobe e non dispone di codice personalizzato che richiede la tipica convalida tramite sviluppo/staging/produzione. Inoltre, l’accesso a questa funzione per gli utenti è completamente controllato dall’amministratore, in modo da poterla valutare senza esporla a tutti gli utenti.

È possibile valutare Content Hub senza influire su utenti/contenuti di produzione gestiti in AEM as a Cloud Service Assets. Una procedura di valutazione potrebbe essere simile alla seguente:

* [Abilitare Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) nell’ambiente di produzione (programma Cloud Manager)
* [Aggiungere un utente amministratore AEM](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) dall’authoring di produzione al profilo di prodotto Content Hub.
* L’amministratore AEM [configura Content Hub](/help/assets/configure-content-hub-ui-options.md)
* L’amministratore AEM o un utente AEM nell’authoring di produzione AEM [approva una serie di risorse per Content Hub](/help/assets/approve-assets-content-hub.md). Se non desideri modificare alcun contenuto di produzione nel DAM, è possibile creare una cartella di valutazione separata nell’istanza di authoring AEM e caricare/assegnare tag o copiarvi alcune risorse da DAM.
* L’amministratore di Admin Console aggiunge [alcuni utenti selezionati](/help/assets/deploy-content-hub.md#onboard-content-hub-users) al profilo di prodotto di Content Hub in modo che possano avviare la valutazione.
* Al termine della valutazione, gli utenti AEM nell’istanza di authoring possono rimuovere l’approvazione dalle risorse di test, approvare le risorse di produzione per Content Hub e quindi l’amministratore di Admin Console può aggiungere tutti gli utenti che hanno bisogno di accedere a Content Hub e al contenuto approvato. Congratulazioni, il tuo Content Hub ora è disponibile.

È disponibile un programma di accesso anticipato per Content Hub su programmi sandbox e i relativi ambienti di produzione e di authoring. Per ulteriori informazioni, consulta [Introduzione ai programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Per ulteriori informazioni sul programma per l’accesso anticipato, contatta il team Adobe Account.

Content Hub non è ancora disponibile per gli ambienti di non produzione (staging e sviluppo). La disponibilità prevista per gli ambienti di staging/sviluppo per Assets Ultimate è marzo 2025.

## Perché non è visibile alcuna risorsa dopo aver effettuato l’accesso a Content Hub? {#no-assets-in-content-hub}

Le risorse contrassegnate come approvate in Assets as a Cloud Service sono automaticamente disponibili in Content Hub. Se non riesci a visualizzare alcuna risorsa dopo aver effettuato l’accesso a Content Hub, approva le risorse utilizzando l’ambiente di authoring AEM as a Cloud Service per renderle disponibili in Content Hub. Per ulteriori informazioni, consulta [Approvare le risorse per Content Hub](/help/assets/approve-assets-content-hub.md).

## Perché non sono visibili le risorse che ho caricato direttamente con Content Hub o importato da account Dropbox oppure OneDrive con Content Hub? {#no-assets-uploaded-from-content-hub}

La visualizzazione delle risorse caricate tramite Content Hub dipende se hai abilitato il pulsante di attivazione/disattivazione [Approvazione automatica](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub) disponibile nell’interfaccia utente Configurazione:

* Se il pulsante **Approvazione automatica** è attivato, le risorse caricate tramite Content Hub sono automaticamente disponibili.

* Se il pulsante **Approvazione automatica** è disattivato, le risorse caricate tramite Content Hub non vengono visualizzate automaticamente. Le risorse sono disponibili nella cartella `hydrated-assets` dell’ambiente Assets as a Cloud Service. Passa alla cartella e [modifica in blocco](/help/assets/approve-assets-content-hub.md) lo stato di tali risorse in `Approved` per consentirne la visualizzazione in Content Hub.

## Come trovare rapidamente le risorse caricate utilizzando Content Hub nell’ambiente AEM as a Cloud Service? {#find-uploaded-assets-on-aem-cloud}

Per trovare rapidamente le risorse caricate utilizzando Content Hub nell’ambiente AEM as a Cloud Service:

1. Passa alla cartella `hydrated-assets`.

1. Fai clic su **[!UICONTROL Filtri]** e seleziona **[!UICONTROL Nessuno stato]** per il campo **[!UICONTROL Stato risorsa]**.

1. Ordina le risorse tramite il campo **[!UICONTROL Data di modifica]**.

## Perché non trovo l’opzione Modifica con Adobe Express nella scheda delle risorse per poter eseguire il remix delle risorse e creare nuove varianti? {#edit-using-express-not-available}

Per visualizzare l’opzione Modifica con Adobe Express nella scheda delle risorse, è necessario disporre dei diritti necessari per utilizzare Adobe Express, oltre ai privilegi per [utenti di Content Hub autorizzati a eseguire il remix delle risorse per creare nuove varianti](#onboard-content-hub-users-add-assets). Adobe Express deve essere implementato nella stessa organizzazione in Adobe Admin Console in cui è stato implementato Adobe Experience Manager.

## È possibile impostare Content Hub in modo che le linee guida del brand della mia organizzazione vengano visualizzate come collegamento nella pagina Home? {#content-hub-setup-brand-guidelines}

Puoi aggiungere collegamenti personalizzati come schede a parte nella pagina Home di Content Hub, in aggiunta alle schede standard Tutte le Risorse, Raccolte e Insight. Per informazioni sulla configurazione, consulta [Collegamenti personalizzati](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub).

## È prevista la migrazione dei clienti Brand Portal esistenti a Content Hub? {#migration-brand-portal}

Adobe fornisce supporto per la migrazione da Brand Portal a Content Hub, che puoi richiedere creando un ticket di assistenza Adobe.

## Perché non trovo l’opzione Impostazioni/Configurazione del prodotto in Content Hub? {#ui-configuration-option-missing}

Per accedere all’[interfaccia utente per la configurazione](/help/assets/configure-content-hub-ui-options.md), devi avere il ruolo di [amministratore di Content Hub](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator). Se in Adobe Admin Console ti è stato assegnato il profilo di prodotto Amministratori AEM nell’istanza di authoring per l’ambiente di produzione e non trovi l’opzione di configurazione, assicurati che il profilo di prodotto Amministratori AEM non sia rinominato. Per ulteriori dettagli, consulta [Profili Team e Prodotto di AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md).
