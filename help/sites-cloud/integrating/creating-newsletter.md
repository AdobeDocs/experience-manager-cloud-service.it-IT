---
title: Creazione di una newsletter Adobe Experience Manager
description: 'Creazione di una newsletter Adobe Experience Manager '
feature: Administering
role: Admin
source-git-commit: f68f5a457bbbcd76681cccabe5a3f4c92b6f8770
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 2%

---


# Creazione di una newsletter Adobe Experience Manager {#creating-newsletter}

Prima di eseguire i passaggi descritti di seguito, è necessario [integrare](/help/sites-cloud/integrating/integrating-campaign-classic.md) Adobe Campaign Classic e AEM as a Cloud Service. Dopo aver configurato sia Adobe Campaign Classic che AEM as a Cloud Service, verrà illustrato come creare una newsletter Adobe Experience Manager.

1. Dall’istanza di authoring AEM, fai clic sul logo Adobe Experience Manager in alto a sinistra della pagina e seleziona **Sites**.
1. Seleziona Campagna, fai clic su **Crea → Pagina**.
   ![creare brand](assets/create.png)
1. Seleziona Marchio e fai clic su **Successivo**.
1. Inserisci un titolo e fai clic su **Crea** e **Fine**.
1. Per creare una pagina Campaign, vai a **Campagne → AdobeDemo → Master** e fai clic su **Crea → Pagina**.
   ![pagina della campagna](assets/campaignpage.png)
1. Seleziona il modello Campagna e fai clic su **Successivo** e **Fine**.
1. Inserisci un titolo , fai clic su **Crea** e **Fine**.
1. Vai a **Campaign → Adobe Demo → Master** e seleziona la casella di controllo CampaignPage . Fai clic su **Proprietà** in alto a sinistra.
   ![proprietà della campagna](assets/propertiesedit.png)
1. Vai a **Cloud Service** scheda:
   * Seleziona Adobe Campaign dall’elenco a discesa Configurazioni Cloud Service .
   * Seleziona il nome desiderato per la configurazione di Adobe Campaign.
   * **Salva** e **Chiudi**.
1. Per creare una pagina e-mail Adobe Campaign Classic, vai a **Campaign → AdobeDemo → Master → CampaignPage** e fai clic su **Crea → Pagina**.
1. Seleziona il modello Adobe Campaign Email (ad esempio, AC 6.1) e fai clic su **Successivo**.
1. Nella pagina Crea , immetti il titolo della newsletter e fai clic su **Crea** e **Fine**.
1. Vai a **Campaign → AdobeDemo → Master → CampaignPage**, seleziona la casella di controllo di Campaign Classic e fai clic su **Modifica** in alto a sinistra per aprire la pagina e-mail.
1. Modifica la pagina della newsletter e-mail di Adobe Campaign Classic in base alle tue esigenze.
1. Fai clic sul pulsante **Informazioni pagina** in alto a sinistra e fai clic su **Pubblica pagina**.
1. Seleziona la configurazione in cui deve essere pubblicata la pagina. Fate clic su **Pubblica**. 
   ![pagina di pubblicazione](assets/publish.png)
1. La pagina della newsletter è stata pubblicata nell’istanza di pubblicazione e anche nella configurazione di Adobe Campaign Classic AEM.
   * Ora la pagina della newsletter sarà visibile in Adobe Campaign Classic
1. Fai clic sul pulsante Informazioni pagina e fai clic su **Avvia flusso di lavoro**.
1. Seleziona **Approva per Adobe Campaign** come modello di flusso di lavoro e fai clic su **Avvia flusso di lavoro** pulsante .
1. Nella parte superiore della pagina viene visualizzata una liberatoria. Fai clic su **Completa** per confermare la revisione, fai di nuovo clic su **OK**.
1. Fai clic su **Completa** e seleziona **Approvazione newsletter** nell’elenco a discesa Passaggio successivo , fai clic su **OK** pulsante .

## Creazione di un destinatario {#creating-recipient}

1. Apri il server Adobe Campaign Classic utilizzando la console client Adobe Campaign Classic.
1. Passare alla visualizzazione Esplora risorse.
1. Nella visualizzazione ad albero a sinistra, vai a Profili e destinazioni e seleziona **Destinatari**.
   ![destinatari](assets/recipients.png)
1. Compila i Dettagli del destinatario.
   * Immettere il Nome.
   * Immettere il cognome.
   * Immetti E-mail.
   * Fai clic su **Salva**.

## Creazione di una consegna e-mail in Adobe Campaign Classic {#create-delivery}

1. Apri il server Adobe Campaign Classic utilizzando la console client Adobe Campaign Classic.
1. Passare alla visualizzazione Esplora risorse.
1. Nella vista ad albero a sinistra, seleziona **Campaign Management** e seleziona **Consegne**.
1. Nell&#39;angolo in alto a destra, fai clic su **Nuovo**.
1. Seleziona **Consegna e-mail con contenuto AEM** dall’elenco a discesa Modello consegna , fai clic su **Continua**.
1. Fai clic sul collegamento Da sotto Parametri e-mail.
   * Inserire l’indirizzo del mittente.
   * Inserisci il campo Da .
   * Fai clic su **OK**.
1. Fai clic su **A** collegamento e clic **Aggiungi** nella schermata di selezione della destinazione.
1. Seleziona **Un destinatario** e fai clic su **Successivo**.
   ![tipo di destinazione](assets/publish.png)
1. Seleziona il destinatario creato [precedente](#creating-recipient) e fai clic su **Fine**.
1. Il destinatario è stato selezionato. Fai clic su **OK**.
1. Fai clic su **Sincronizza**.
1. Seleziona la pagina e-mail dall’elenco, fai clic su **OK**.
1. Il modello e-mail viene sincronizzato. Fai clic su **Aggiorna contenuto** se non è caricato.
1. Fai clic su **Invia** per inviare l’e-mail.
1. Nella schermata successiva, seleziona **Consegna quanto prima** quindi fai clic su **Analizza**.
   ![target di consegna](assets/deliverytarget.png)
1. Una volta creata la consegna, fai clic su **Conferma consegna** per iniziare a inviare l’e-mail. Fai clic su **Sì** per confermare.
   ![conferma consegna](assets/confirmdelivery.png)
1. La consegna è iniziata. Fai clic su **Chiudi**.
1. Fai clic su **Salva** per salvare la consegna.
