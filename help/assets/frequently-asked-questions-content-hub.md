---
title: Domande frequenti su Content Hub
description: Risposte ad alcune delle domande più frequenti su Content Hub.
source-git-commit: 1d51a1e0858e975bc354ffd9c4b32c26aa1604af
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---

# Domande frequenti su Content Hub {#content-hub-frequently-asked-questions}

![Domande frequenti su Content Hub](assets/content-hub-faqs.png)

## Cos’è Content Hub? {#what-is-content-hub}

Content Hub è una funzione di Adobe Experience Manager Assets as a Cloud Service.

Content Hub consente ai team più grandi di individuare facilmente le risorse approvate e rilevanti tramite un portale intuitivo e di adattarle rapidamente alle proprie esigenze.  Inoltre, Content Hub fornisce un meccanismo di acquisizione che consente agli utenti di self-service durante il caricamento delle risorse in DAM. In questo modo si soddisfa direttamente la necessità delle organizzazioni di velocizzare la creazione dei contenuti, preservando al contempo la coerenza del marchio e la conformità con le protezioni appropriate.

## Perché non è possibile abilitare Content Hub nel programma/ambiente Cloud Manager? {#cannot-enable-content-hub}

Content Hub è a questo punto disponibile solo sui programmi di produzione AEM Cloud Manager, che includono una licenza Assets. Quando si fa clic su [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) per abilitarlo, questo viene distribuito e associato all&#39;ambiente di produzione dell&#39;autore dell&#39;AEM in tale programma. Per informazioni dettagliate e prerequisiti, vedere [Distribuire Content Hub](/help/assets/deploy-content-hub.md).

È disponibile un programma di accesso anticipato a Content Hub su programmi sandbox/ambienti di produzione di authoring. Per ulteriori informazioni, vedere [Introduzione ai programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md). Per ulteriori informazioni sul programma di accesso anticipato, contatta il team del tuo account di Adobe.

Content Hub non è attualmente disponibile per ambienti non di produzione (stage, dev, ecc.).

## Ho abilitato Content Hub nel mio programma/ambiente di produzione, posso disattivarlo? {#can-i-disable-content-hub}

L&#39;abilitazione di Content Hub su un programma di produzione lo implementa come parte dell&#39;infrastruttura di produzione. AEM Cloud Manager non consente di rimuovere o disabilitare l’infrastruttura di produzione per ridurre al minimo i rischi di errori umani nell’utilizzo della produzione.

Se non desideri fornire Content Hub agli utenti una volta implementato, non assegnare alcun utente al profilo di prodotto Content Hub in Admin Console. Per ulteriori dettagli, vedere [Distribuire Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile).

## Come posso valutare Content Hub nella mia organizzazione dato che è disponibile solo per programmi di produzione/ambienti di authoring di produzione? {#how-can-i-evaluate-content-hub}

Content Hub è una funzione fornita e gestita da Adobe e non dispone di codice personalizzato che richiederebbe la tipica convalida tramite dev/stage/produzione. Inoltre, l’accesso a questa funzione per gli utenti è completamente controllato dall’amministratore, in modo da poterla valutare senza esporla a tutti gli utenti.

È possibile valutare Content Hub senza influire sugli utenti/contenuti di produzione gestiti in AEM as a Cloud Service Assets. Una procedura di valutazione potrebbe essere simile alla seguente:

* [Abilita Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) nell&#39;ambiente di produzione (programma Cloud Manager)
* [Aggiungere un utente amministratore AEM](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) dall&#39;autore della produzione al profilo di prodotto Content Hub.
* L&#39;amministratore AEM [configura Content Hub](/help/assets/configure-content-hub-ui-options.md)
* L&#39;amministratore AEM o un utente AEM dell&#39;autore di produzione AEM [approva una serie di risorse per Content Hub](/help/assets/approve-assets-content-hub.md). Se non si desidera modificare alcun contenuto di produzione in DAM, è possibile creare una cartella di valutazione separata nell&#39;istanza di authoring AEM e caricare/assegnare tag o copiare alcune risorse da DAM.
* L&#39;amministratore di Admin Console aggiunge [alcuni utenti selezionati](/help/assets/deploy-content-hub.md#onboard-content-hub-users) al profilo di prodotto di Content Hub, in modo che possano avviare la valutazione.
* Al termine della valutazione, gli utenti AEM nell’istanza di authoring possono rimuovere l’approvazione dalle risorse di test, approvare le risorse di produzione per Content Hub e quindi l’amministratore Admin Console può aggiungere tutti gli utenti che hanno bisogno di accedere a Content Hub e al contenuto approvato. Congratulazioni, il tuo Content Hub è live.

Adobe offre anche un programma di accesso anticipato a Content Hub negli ambienti Stage. Vedere la domanda [Perché non è possibile abilitare Content Hub nel programma/ambiente Cloud Manager?](#cannot-enable-content-hub) per i dettagli.

## Perché non vedo risorse dopo aver effettuato l’accesso a Content Hub? {#no-assets-in-content-hub}

Le risorse contrassegnate come approvate in Assets as a Cloud Service sono automaticamente disponibili in Content Hub. Se dopo aver effettuato l’accesso a Content Hub non riesci a visualizzare alcuna risorsa, approva le risorse utilizzando l’ambiente di authoring AEM as a Cloud Service per renderle disponibili in Content Hub. Per ulteriori informazioni, vedere [Approvare le risorse per Content Hub](/help/assets/approve-assets-content-hub.md).

## Perché non vedo le mie risorse caricate direttamente da Content Hub o importate dagli account di Dropbox o OneDrive con Content Hub? {#no-assets-uploaded-from-content-hub}

La visualizzazione delle risorse caricate tramite Content Hub dipende dal fatto che tu abbia abilitato l&#39;interruttore [Approvazione automatica](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub) disponibile nell&#39;interfaccia utente di configurazione:

* Se l&#39;opzione **Approvazione automatica** è abilitata, le risorse caricate tramite Content Hub saranno automaticamente disponibili.

* Se l&#39;opzione **Approvazione automatica** è disabilitata, le risorse caricate tramite Content Hub non vengono visualizzate automaticamente. Le risorse sono disponibili nella cartella `hydrated-assets` dell&#39;ambiente Assets as a Cloud Service. Passa alla cartella e [modifica in blocco](/help/assets/approve-assets-content-hub.md) lo stato di tali risorse in `Approved` per consentirne la visualizzazione in Content Hub.

## Come trovare rapidamente le risorse caricate utilizzando Content Hub nell’ambiente AEM as a Cloud Service? {#find-uploaded-assets-on-aem-cloud}

Per trovare rapidamente le risorse caricate tramite Content Hub nell’ambiente AEM as a Cloud Service:

1. Spostarsi nella cartella `hydrated-assets`.

1. Fare clic su **[!UICONTROL Filtri]** e impostare **[!UICONTROL Nessuno stato]** nel campo **[!UICONTROL Stato risorsa]**.

1. Ordinamento delle risorse tramite il campo **[!UICONTROL Data modificata]**.

## Perché non visualizzo l’opzione Modifica con Adobe Express nella scheda delle risorse per poter eseguire il remix delle risorse e creare nuove varianti? {#edit-using-express-not-available}

Per visualizzare l&#39;opzione di modifica tramite Adobe Express sulla scheda delle risorse, oltre ai privilegi per [utenti Content Hub con diritti per il remix delle risorse in nuove varianti](#onboard-content-hub-users-add-assets) è necessario disporre di diritti Adobe Express. Adobe Express deve essere distribuito nella stessa organizzazione in Adobe Admin Console, dove viene distribuito Adobe Experience Manager.

## È possibile impostare Content Hub in modo che le linee guida del marchio della mia organizzazione vengano visualizzate come collegamento nella pagina Home? {#content-hub-setup-brand-guidelines}

Puoi aggiungere collegamenti personalizzati come schede separate, oltre alle schede standard All Assets, Collections e Insights nella home page di Content Hub. Per informazioni su come configurarlo, consulta [Collegamenti personalizzati](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub).

## È prevista la migrazione dei clienti Brand Portal esistenti a Content Hub? {#migration-brand-portal}

Adobe fornisce supporto per la migrazione da Brand Portal a Content Hub che puoi utilizzare creando un ticket di supporto Adobe.

## Perché non è possibile visualizzare l’opzione Impostazioni prodotto/Configurazione in Content Hub? {#ui-configuration-option-missing}

Per accedere all&#39;[interfaccia utente di configurazione](/help/assets/configure-content-hub-ui-options.md), devi essere un [amministratore Content Hub](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator). Se sei assegnato al profilo di prodotto Amministratori AEM nell’istanza di authoring di produzione in Adobe Admin Console e non riesci ancora a visualizzare l’opzione di configurazione, assicurati che il profilo di prodotto Amministratori AEM non venga rinominato. Per ulteriori dettagli, vedi [Profili team e prodotto di AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md).


