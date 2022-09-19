---
title: Creazione di newsletter di Campaign con AEM
description: Scopri come utilizzare AEM as a Cloud Service per creare newsletter che possono essere inviate con Adobe Campaign Classic.
feature: Authoring
role: User
exl-id: 60a6a9d0-f5e6-424f-b320-dd4943c55d45
source-git-commit: 6196f3fc67dbcfe03a71bb6a0796dd5d1d0f8546
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 100%

---


# Creazione di newsletter di Campaign con AEM {#creating-newsletters}

Questo documento illustra come utilizzare AEM as a Cloud Service per creare newsletter che possono essere inviate con Adobe Campaign Classic.

Sfruttando l’integrazione tra AEM as a Cloud Service e Adobe Campaign Classic, puoi creare le newsletter utilizzando i potenti strumenti di authoring di AEM. Quindi, quando sei pronto per inviare la newsletter, puoi utilizzare le funzioni di gestione e distribuzione dei destinatari di Campaign per inviarla.

## Prerequisiti {#prerequisites}

Prima di poter creare una newsletter con AEM e inviarla con Campaign, è necessario innanzitutto [integrare Adobe Campaign Classic e AEM as a Cloud Service.](/help/sites-cloud/integrating/integrating-campaign-classic.md)

## Creazione della struttura della newsletter {#create-structure}

Il contenuto della newsletter viene gestito in AEM analogamente alla gestione del contenuto di un sito. Inizia creando un “sito” che contenga il contenuto. All&#39;interno di questo “sito” è possibile raccogliere le newsletter in base al marchio.

1. Accedi all’istanza di authoring di AEM.

1. Dalla pagina di navigazione principale, apri la console **Sites**.

1. In un’installazione standard di AEM sarà disponibile una cartella **Campaign** esistente. Selezionala e fai clic sul pulsante **Crea** e quindi **Pagina**.

   ![Crea pagina](assets/create-page.png)

1. Seleziona **Marchio** come modello del sito e fai clic su **Avanti**.

   ![Crea marchio](assets/create-brand.png)

1. Inserisci un **Titolo**, fai clic su **Crea** e quindi su **Fine**.

   ![Fornire i dettagli del marchio](assets/create-brand-page.png)

Adesso disponi di una struttura di contenuto di base per creare le campagne.

![Struttura del contenuto](assets/content-structure.png)

## Creazione di una campagna {#create-campaign}

Adesso che disponi di una struttura di contenuto di base per la campagna, puoi creare la campagna stessa. La campagna verrà utilizzata per organizzare eventualmente più newsletter.

1. Utilizzando la [Vista a colonne](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) nella console Sites, seleziona il marchio creato in precedenza (in questo caso, **WKND Escapes**) e **Area master**, creata automaticamente, e quindi fai clic sul pulsante **Crea** e su **Pagina**.

   ![Creare una pagina della campagna](assets/create-campaign-page.png)

1. Seleziona **Campaign** come modello, fai clic su **Avanti** e su **Fine**.

   ![Selezionare il modello di campagna](assets/select-campaign-template.png)

1. Inserisci un **Titolo** per la campagna, quindi fai clic su **Crea** e **Fine**.

   ![Titolo campagna](assets/campaign-title.png)

Adesso è disponibile una campagna per la creazione delle newsletter.

![Struttura della campagna](assets/campaign-structure.png)

## Selezione della configurazione della campagna {#campaign-configuration}

AEM può supportare diverse configurazioni di integrazione. Per la nuova campagna, è necessario definire le configurazioni da utilizzare per inviare il contenuto della newsletter.

1. Utilizzando [Vista a colonne](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) nella console Sites, individua la campagna creata in precedenza (in questo caso, **Campagna estiva WKND Escape**), quindi selezionala utilizzando la casella di controllo e fai clic sul pulsante **Proprietà** sulla barra degli strumenti.

   ![Selezionare una campagna](assets/select-campaign.png)

1. Nella finestra **Proprietà**, seleziona **Cloud Service** per definire l’integrazione da utilizzare con questa campagna.

   * Seleziona **Adobe Campaign** dall’elenco a discesa **Configurazioni Cloud Services**.
   * Seleziona la configurazione dell’integrazione di Adobe Campaign desiderata dall’elenco a discesa **Adobe Campaign**.
   * Fai clic su **Salva e chiudi**.

   ![Proprietà di configurazione di Campaign](assets/campaign-configuration-properties.png)

La campagna adesso è collegata alla tua integrazione con Adobe Campaign. Ora puoi creare una newsletter in AEM e inviarla con Adobe Campaign.

## Creare una newsletter {#create-newsletter}

È possibile creare e gestire le newsletter nella struttura dei contenuti della campagna già creata e configurata.

1. Utilizzando [Vista a colonne](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) nella console Sites, individua la campagna configurata in precedenza (in questo caso, **Campagna estiva WKND Escape**), selezionala e fai clic sul pulsante **Crea** e quindi **Pagina**.

   ![Crea newsletter](assets/create-newsletter.png)

1. Nella procedura guidata Crea pagina, seleziona il modello **E-mail Adobe Campaign (AC 6.1)** e fai clic su **Avanti**.

   ![Selezionare il modello e-mail della campagna](assets/adobe-campaign-email-template.png)

1. Nel passaggio **Proprietà** della procedura guidata, immetti il **Titolo** per la newsletter, fai clic su **Crea** e **Apri**.

   ![Titolo della newsletter](assets/create-newsletter-wizard-properties.png)

1. Modifica la pagina della newsletter come faresti con qualsiasi altra pagina di contenuti di AEM per soddisfare le tue esigenze.

Adesso è disponibile una newsletter da inviare con Adobe Campaign.

## Pubblicazione della newsletter {#publishing-newsletter}

Devi pubblicare la newsletter per consentire ad Adobe Campaign di inviarla.

1. Utilizzando [Vista a colonne](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) nella console Sites, individua la newsletter creata in precedenza (in questo caso, **Prima newsletter per la campagna estiva WKND Escape**), selezionala e fai clic sul pulsante **Informazioni pagina** in alto a sinistra e su **Pubblica pagina**.

1. Seleziona la/le configurazione/i per cui la pagina deve essere pubblicata e fai clic su **Pubblica**.

   ![Pubblica pagina](assets/publish.png)

La pagina della newsletter viene adesso pubblicata nell’istanza di pubblicazione di AEM ed è visibile in Adobe Campaign Classic. Per poterla selezionare all’interno di Adobe Campaign, deve essere approvata.

1. Fai clic ancora una volta sul pulsante **Informazioni pagina** della newsletter e seleziona **Avvia flusso di lavoro**.

1. Seleziona **Approva per Adobe Campaign** come modello di flusso di lavoro (fornendo facoltativamente una descrizione) e fai clic sul pulsante **Avvia flusso di lavoro**.

   ![Avvia flusso di lavoro](assets/start-workflow.png)

1. Nella parte superiore dell’editor pagina per le newsletter viene visualizzato un banner che fornisce i passaggi successivi del processo di approvazione. Fai clic su **Completato**.

   ![Approva flusso di lavoro](assets/approve-workflow.png)

1. Nella finestra di dialogo **Completa elemento di lavoro**, seleziona **Revisione newsletter (amministratore)** nell’elenco a discesa **Passaggio successivo** e fai clic sul pulsante **OK**.

   ![Revisione newsletter](assets/newsletter-review.png)

1. Nel banner che appare nella parte superiore dell’editor pagina per le newsletter, fai di nuovo clic su **Completa**.

1. Nella finestra di dialogo **Completa elemento di lavoro**, seleziona **Approvazione newsletter** nell’elenco a discesa **Passaggio successivo** e fai clic sul pulsante **OK**.

   ![Approvazione newsletter](assets/newsletter-approval.png)

1. Quando la finestra di dialogo viene chiusa, il banner visualizzato nella parte superiore dell’editor pagina per le newsletter scompare perché il flusso di lavoro di approvazione è completo.

La newsletter viene adesso pubblicata in AEM e approvata per l’utilizzo in Adobe Campaign.

>[!TIP]
>
>I passaggi del flusso di lavoro qui descritti sono semplificati per illustrare il processo. In un normale flusso di lavoro, la creazione e l’approvazione di una newsletter solitamente funzionano in ruoli diversi
>
>Per ulteriori dettagli sull’utilizzo dei flussi di lavoro, consultare il documento [Utilizzo dei flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md).

## Creazione di un destinatario {#creating-recipient}

Per poter inviare la newsletter creata in AEM, devi innanzitutto definire i destinatari in Adobe Campaign Classic.

1. Accedi ad Adobe Campaign Classic utilizzando la console client.

1. Seleziona **Strumenti** -> **Esplora** dalla barra del menu.

1. In Esplora, passa al nodo **Profili e destinazioni** -> **Destinatari**.

   ![Destinatari](assets/recipients.png)

1. Nella barra degli strumenti, fai clic su **Nuovo** e fornisci i dettagli del destinatario.

   * Nome
   * Cognome
   * Indirizzo e-mail

1. Fai clic su **Salva**.

Adesso disponi di un destinatario a cui inviare la newsletter tramite Adobe Campaign Classic.

## Creazione di una consegna e-mail {#create-delivery}

L’ultimo passaggio consiste nell’inviare la newsletter creata in AEM al destinatario aggiunto in Adobe Campaign Classic.

1. Accedi ad Adobe Campaign Classic utilizzando la console client.

1. Seleziona **Strumenti** -> **Esplora** dalla barra del menu.

1. In Esplora, passa al nodo **Gestione campagne** -> **Consegne** e fai clic su **Nuova**.

   ![Consegna dei contenuti di AEM](assets/delivery-aem-content.png)

1. Nella finestra di dialogo **Consegna**, seleziona **Consegna e-mail con contenuti di AEM** come **Modello di consegna** dall’elenco a discesa e fai clic su **Continua**.

   ![Consegna dei contenuti di AEM](assets/aem-content-delivery.png)

1. Nella sezione **Parametri e-mail**, fai clic sul collegamento **Da** e inserisci le informazioni del mittente e fai clic su **OK**.

   * Indirizzo mittente
   * Campo Da

   ![Definisci dal campo](assets/delivery-from.png)

1. Nella sezione **Parametri e-mail**, fai clic sul collegamento **A** per aprire la finestra di dialogo **Seleziona destinazione** e quindi su **Aggiungi**.

   ![Seleziona destinazione](assets/select-target.png)

1. Nella finestra di dialogo **Seleziona l’elemento di destinazione**, seleziona **Un destinatario** e fai clic su **Avanti**.

   ![Seleziona l’elemento di destinazione](assets/select-target-element.png)

1. Utilizzando i filtri, seleziona il destinatario desiderato [creato in precedenza](#creating-recipient) e fai clic su **Fine**.

   ![Selezionare il destinatario](assets/select-target-element-recipient.png)

1. Tornando nella finestra di dialogo **Seleziona destinazione**, fai clic su **OK**.

1. Nella finestra di dialogo della consegna, fai clic su **Sincronizza**.

   ![Sincronizza](assets/synchronize.png)

1. Nella finestra di dialogo **Sincronizza con il contenuto di AEM**, seleziona dall’elenco la newsletter creata in precedenza, quindi fai clic su **OK**.

1. Il contenuto dell’e-mail di Adobe Campaign viene sincronizzato con il contenuto della newsletter creato in AEM.

   * Se il contenuto non viene caricato automaticamente, fai clic su **Aggiorna contenuto**.

1. Per inviare l’e-mail, fai clic su **Invia**.

1. Nella finestra di dialogo **Invia a destinazione della consegna principale**, seleziona **Consegna il prima possibile** e quindi fai clic su **Analizza**.

   ![Analisi della consegna](assets/delivery-analysis.png)

1. Il passaggio di analisi crea la consegna, combinando il contenuto con i destinatari. Una volta creata la consegna, fai clic su **Conferma consegna** per inviare l’e-mail. Fai clic su **Sì** per confermare.

1. La consegna è iniziata. Fai clic su **Chiudi**.

   ![Distribuzione](assets/delivering.png)

1. Fai clic su **Salva** per salvare la consegna.

La newsletter è stata inviata!

>[!TIP]
>
>In questo esempio viene mostrata una distribuzione semplificata dell’invio di una newsletter a un singolo destinatario. Naturalmente, una consegna normale conterrebbe molti destinatari diversi che Adobe Campaign rende semplici da gestire. Per ulteriori dettagli sulla gestione della consegna e dei destinatari, fai riferimento alla [Documentazione di Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=it).
