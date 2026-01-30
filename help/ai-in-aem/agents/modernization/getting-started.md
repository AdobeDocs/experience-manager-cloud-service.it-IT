---
title: Guida introduttiva all’agente di modernizzazione esperienza
description: Scopri i primi passaggi per diventare rapidamente produttivi con l’agente di modernizzazione esperienza utilizzando la console di modernizzazione esperienza.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: c80ce5a9fc5f208fd910d5cef72225085248fb4d
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# Guida introduttiva all’agente di modernizzazione esperienza {#getting-started}

Scopri i primi passaggi per diventare rapidamente produttivi con l’agente di modernizzazione esperienza utilizzando la console di modernizzazione esperienza.

>[!NOTE]
>
>Se ti interessa utilizzare la console di modernizzazione esperienza, puoi richiedere l’accesso per garantire un’esperienza di onboarding fluida.

## Preparare un archivio GitHub di Edge Delivery {#prepare-repo}

1. Selezionare un repository [Edge Delivery Services](/help/edge/overview.md) da utilizzare con la console di modernizzazione delle esperienze.
   * Questo può essere un progetto Edge Delivery Services esistente oppure puoi crearne uno nuovo seguendo l&#39;[esercitazione per sviluppatori](https://www.aem.live/developer/tutorial) utilizzando l&#39;[archivio standard.](https://github.com/adobe/aem-boilerplate)
1. Verificare che l&#39;app [AEMY GitHub](https://github.com/apps/aem-aemy) sia installata nell&#39;archivio.
   * Questo consente alla console di controllare il codice.
1. Verificare che l&#39;app GitHub [AEM Code Sync](https://github.com/apps/aem-code-sync) sia installata nell&#39;archivio.
   * Questo consente a Edge Delivery Services di sincronizzare il codice.
   * Se l’archivio si basa sull’esercitazione, questo passaggio è già completo.

## Apri la console di modernizzazione esperienza {#open-console}

1. Passa a [`aemcoder.adobe.io`.](https://aemcoder.adobe.io)
1. Accedi con il tuo Adobe ID.

## Collegare l’archivio GitHub {#connect-repo}

La console richiede un repository al primo accesso.

![Prima schermata di accesso della console](assets/first-sign-on.png)

1. Fare clic su **Connetti repository**.
1. Verrà aperta l’app AEMY in una nuova scheda del browser. Fai clic su **Autorizza AEM AEMY**.
1. Nella console, seleziona **Proprietario**, **Archivio** e **Selezione ramo** e fai clic su **Estrai nell&#39;area di lavoro**.
   ![Connessione al progetto GitHub](assets/connect-to-github-project.png)
1. Quando viene richiesto di **Sostituire l&#39;area di lavoro esistente**, fare clic su **Sostituisci area di lavoro**.
   ![Sostituisci area di lavoro esistente](assets/replace-existing-workspace.png)

Il progetto GitHub ora è connesso alla console e si è nella schermata iniziale.

![Pagina principale console](assets/console-home.png)

## Avvia richiesta {#start-prompting}

Ora che la console è in grado di accedere al codice, puoi iniziare a chiedere conferma.

1. Per iniziare, puoi importare il contenuto di un sito:
   * &quot;Eseguire la migrazione della pagina `https://wknd-trendsetters.site`.&quot;
1. Questo importa il contenuto del sito.
   * La console osserva la separazione delle problematiche e gestisce il contenuto e la presentazione separatamente.
   * L&#39;importazione iniziale del contenuto di un sito può richiedere alcuni minuti.
   * La console offre un feedback continuo all’inizio del suo lavoro, inclusa una panoramica dei passaggi pianificati.
     ![Importazione contenuto](assets/content-import.png)
1. Una volta importato il sito, il pannello **Workspace** mostra le pagine. Seleziona una pagina per visualizzarne l’anteprima nel pannello di destra.
   ![Contenuto importato](assets/content-imported.png)
1. Ora che disponi di contenuto, puoi richiedere di importare gli stili dalla stessa origine.
   * &quot;Importare gli stili generali da `https://wknd-trendsetters.site`.&quot;
1. Come per l’importazione iniziale del contenuto, l’importazione potrebbe richiedere alcuni minuti e la console fornisce un feedback durante l’elaborazione della richiesta e l’importazione degli stili. Una volta completata l&#39;attività, fai clic su **Aggiorna anteprima** nel pannello di destra per visualizzare il contenuto formattato.
   ![Stili importati](assets/styles-imported.png)

Ora puoi importare sia il contenuto che gli stili nella console.

## Caricare contenuti {#upload-content}

Per caricare i contenuti in [Document Authoring](https://da.live):

1. Verifica di essere nella visualizzazione **Contenuto**, quindi fai clic sul pulsante **Carica contenuto** in alto a destra.
   * Per impostazione predefinita, quando entri nella console sei nella visualizzazione **Contenuto**.
   * La vista è indicata dall’icona evidenziata nella barra laterale lungo il lato sinistro della console.
1. Si apre la finestra di dialogo **Carica contenuto** con l&#39;organizzazione di destinazione e l&#39;archivio precompilati dal tuo `fstab.yaml`.
   * Se `fstab.yaml` non è presente nel repository connesso, sarà necessario immettere manualmente **Organization** e **Repository**.
   * Se è stata utilizzata la boilerplate, verrà fornito `fstab.yaml`.
1. Selezionare i file da caricare e fare clic su **Carica**.
   ![Finestra di dialogo Carica contenuto](assets/upload-content.png)
1. La console indica il processo di caricamento selezionando il pulsante **Carica**.
   ![Caricamento](assets/uploading.png) in corso
1. Al termine dell’operazione, nella parte inferiore della console viene visualizzata una notifica.
   ![Visualizza in AEM](assets/view-in-aem.png)

Per accedere ai contenuti caricati in Document Authoring, fai clic su **Visualizza in AEM** nella notifica al termine del caricamento oppure passa a `https://da.live/#/{organization}/{repository}`.

![Contenuto nell&#39;authoring dei documenti](assets/content-in-document-authoring.png)

Il contenuto importato è ora in Authoring documenti.

## Modifiche al codice push {#push-code-changes}

Una volta apportate le modifiche desiderate al codice, puoi inviarle all’archivio GitHub.

1. Passa alla visualizzazione **Codice** (icona `</>` nella barra laterale a sinistra) e quindi alla scheda **Modifiche Git** (icona del ramo in alto a destra).
   ![Visualizzazione codice](assets/code-view-git-changes.png)
1. Nell&#39;elenco dei file modificati, se alcuni file vengono visualizzati come non tracciati, fare clic sul pulsante `+` per visualizzarli nell&#39;area intermedia.
1. Fai clic sul pulsante **Azioni GitHub** in alto a destra, quindi seleziona **Invia** dal menu a discesa.
1. Nella finestra di dialogo **Push changes**, scegli di inviare le modifiche a una nuova PR (impostazione predefinita) o al ramo corrente, quindi fai clic su **Confirm** per inviare le modifiche.
   * In caso di dubbi, puoi inviare un messaggio push al ramo corrente per semplificare la procedura.
1. Al termine dell’operazione, nella parte inferiore della console viene visualizzata una notifica.
   ![Visualizza PR](assets/view-pr.png)

Se desideri accedere direttamente alle modifiche push in GitHub, fai clic su **Visualizza PR** nella notifica al termine del push.

![Codice in GitHub](assets/code-in-github.png)

Il codice ora è in GitHub.

## Anteprima sito {#preview-site}

Per visualizzare le modifiche nell’ambiente di anteprima:

1. Torna a Creazione documento.
   * Potrebbe essere ancora aperto in una scheda del browser aperta dopo aver fatto clic su **Visualizza in AEM** dopo aver caricato il contenuto.
   * Oppure passa a `https://da.live/#/{organization}/{repository}`
1. Apri una delle pagine caricate in precedenza in AEM.
1. Fare clic sull&#39;icona del piano carta (in alto a destra) e selezionare **Anteprima**.
   ![Pubblica in anteprima](assets/publish-to-preview.png)

Congratulazioni. I contenuti e gli stili migrati sono ora live nell’ambiente di anteprima AEM.

![Contenuto anteprima pubblicato](assets/published-preview.png)

Se il codice è stato inviato a un ramo diverso da `main`, l&#39;anteprima aperta da Authoring documenti non mostrerà gli stili. Passa al ramo aggiornando l’URL dell’anteprima per visualizzare i tuoi stili.

## Risorse aggiuntive {#additional-resources}

I seguenti documenti possono essere utili mentre continui a esplorare Experience Modernization Agent e la relativa console.

* [Console di modernizzazione esperienza](/help/ai-in-aem/agents/modernization/console.md) - Dettagli sulla console, visualizzazioni, opzioni e funzionalità
* [Esercitazione per sviluppatori di Edge Delivery Services](https://www.aem.live/developer/tutorial): utile se hai poca esperienza con i progetti AEM e Edge Delivery Services
* [Authoring dei documenti](https://da.live) - Utile se si è alle prime armi con l&#39;authoring dei documenti per la gestione dei contenuti
