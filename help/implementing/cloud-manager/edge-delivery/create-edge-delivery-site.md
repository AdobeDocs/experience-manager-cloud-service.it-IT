---
title: Creare il primo sito Edge Delivery con un clic
description: Scopri come creare rapidamente un sito Edge Delivery in Cloud Manager con il solo clic di un pulsante.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: d3d956e9342fe6bb507b0efd952dfbecdda269c2
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 55%

---

# Creare il primo sito Edge Delivery con un clic{#about-one-click-edge-delivery-site}

La creazione del primo sito Edge Delivery con un clic è progettata per consentirti di automatizzare l’onboarding e la distribuzione di siti Edge Delivery all’interno di Cloud Manager. Il processo è notevolmente semplificato ed è sufficiente fare clic su un singolo pulsante. Il solo clic esegue il provisioning dell’infrastruttura richiesta, si integra con GitHub per il controllo della versione e configura l’archiviazione dei documenti e delle risorse in Google Drive.

Questa automazione consente di ridurre le attività manuali necessarie per configurare il sito iniziale. Garantisce flussi di lavoro ottimizzati, scalabilità e prestazioni migliori per i team che gestiscono i contenuti su server Edge.

>[!IMPORTANT]
>
>Il provisioning con un solo clic dei siti Edge Delivery è ottimizzato per i siti proof-of-concept e i prototipi rapidi. Per i carichi di lavoro di produzione, Adobe consiglia di migrare il sito a un’organizzazione Edge Delivery Services dedicata.

<!--
 Check out this quick 2-minute video for a step-by-step walkthrough on creating your first Edge Delivery site—no hassle, just one click.

>[!VIDEO](https://video.tv.adobe.com/v/3458975?quality=12&learn=on)
-->

## Creare un sito Edge Delivery in Cloud Manager con un solo clic {#one-click-edge-delivery-site}

Per creare un sito Adobe Edge Delivery con un solo clic, l’organizzazione deve disporre di una licenza Edge Delivery Services. Questa licenza fa parte di Adobe Experience Manager (AEM) ed è necessaria per la creazione di Edge Delivery Services all’interno di Cloud Manager.

In termini di autorizzazioni, devi avere il ruolo di Proprietario business o disporre delle autorizzazioni appropriate per aggiungere o modificare programmi in Cloud Manager. Questo livello di accesso consente di gestire l’integrazione di Edge Delivery Services nei programmi.

Consulta anche [Introduzione a Edge Delivery Services in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**Per creare un sito Edge Delivery in Cloud Manager con un solo clic:**

1. Accedi a Cloud Manager all&#39;indirizzo [experience.adobe.com](https://experience.adobe.com).
   1. Nella sezione **Accesso rapido**, fai clic su **Experience Manager**.
   1. Nel pannello laterale a sinistra, fai clic su **Cloud Manager**.
   1. Seleziona un’organizzazione.
1. Nella console **Programmi** fare clic su un programma.
1. Nell’angolo in alto a sinistra della pagina, fai clic sull’![icona Mostra menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu a sinistra.
1. Nel menu a sinistra, sotto l’intestazione **Programma**, fai clic su **Panoramica**.
1. Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**.
1. Nella finestra di dialogo **Elenco attività di Edge Delivery** della pagina Edge Delivery fare clic su **Crea sito ora** nella casella di gruppo **Aggiungi sito Edge Delivery**.
1. Nella finestra di dialogo **Crea sito Edge Delivery** immettere il nome del sito nel campo di testo **Nome progetto**.
1. In **Opzioni di creazione**, selezionare una delle opzioni seguenti:
   * **Authoring dei documenti**: creazione di contenuti in Google Drive o SharePoint. Questa opzione è predefinita e non richiede un ambiente AEM.
   * **Authoring AEM (Beta)**: creazione di contenuti in AEM tramite l&#39;editor universale. Se si sceglie questa opzione, in **Seleziona modello** selezionare un modello iniziale per il sito Edge Delivery.

   ![Finestra di dialogo Crea sito Edge Delivery con AEM Authoring selezionato.](/help/implementing/cloud-manager/edge-delivery/assets/eds-create-aem-authoring.png)

1. Nell&#39;elenco a discesa **Ambienti di authoring**, selezionare un ambiente AEM da utilizzare per l&#39;authoring. Questo ambiente deve esistere già nel programma. È richiesto solo il livello di authoring; un livello di pubblicazione non è necessario quando Edge Delivery gestisce la consegna. Consulta [Livello di pubblicazione flessibile (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).

1. Fai clic su **Crea sito ora**.

   Nella parte superiore centrale della schermata viene visualizzata una notifica pop-up che informa dell’avvio del provisioning del sito Edge Delivery.

   Quando Cloud Manager completa il provisioning e la convalida del sito, il **nome sito** (il nome del progetto immesso in precedenza) viene visualizzato nella casella di riepilogo **Edge Delivery sites** nella pagina Edge Delivery. A sinistra della colonna di stato **Verified** viene visualizzato un punto verde.

Vedi anche [Pubblicare contenuti da AEM Author ad Edge Delivery](#publish-from-aem-author).

### Esplorare un sito Edge Delivery creato con un clic {#explore-one-click-ed-site}

1. Accedi a Cloud Manager all’indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nell’angolo in alto a sinistra della pagina, fai clic sull’![icona Mostra menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu a sinistra.
1. Nel menu a sinistra, sotto l’intestazione **Programma**, fai clic su **Panoramica**.
1. Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**.
1. Nella pagina Edge Delivery, effettua una delle seguenti operazioni:

   | Cosa esplorare | Passaggi |
   | --- | --- |
   | Archivio GitHub di un sito | <ul><li>Nella casella di riepilogo **Siti Edge Delivery**, sotto l’intestazione di colonna **Archivio**, fai clic sull’URL del sito appena creato.<br>Potrebbe essere necessario accedere a GitHub con il proprio nome utente o indirizzo e-mail e la password.</li> |
   | Pubblicare un sito | <ul><li> Nella casella di riepilogo **Siti Edge Delivery**, all’estrema destra del nome del sito, fai clic sull’![icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per aprire il menu a discesa.</li><li>Fai clic sull&#39;icona ![Publish Check](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **Publish site** nel menu a discesa.<br>Viene visualizzato un messaggio che informa che la pubblicazione del sito è stata avviata correttamente.</li></ul> |
   | Visualizzare l’anteprima di un sito pubblicato | <ul><li>Nella casella di riepilogo **Siti Edge Delivery**, sotto l’intestazione della colonna **Nome sito**, fai clic sull’URL del sito appena creato e pubblicato.<br>Nella barra degli indirizzi URL del browser, l’URL del sito termina con `.page` e indica che stai visualizzando un’anteprima del sito.</li><li>Per visualizzare il sito live, modifica manualmente `.page` in `.live` nella barra degli indirizzi URL.</li></ul> |
   | Concedere agli utenti l’accesso all’archivio dei contenuti su Google Drive | <ul><li> Nella casella di riepilogo **Siti Edge Delivery**, all’estrema destra del nome del sito, fai clic sull’![icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per aprire il menu a discesa.</li><li>Fai clic su![icona Aggiunta utenti](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **Ottieni l’accesso all’archivio dei contenuti** nel menu a discesa.</li><li>Nella finestra di dialogo **`Add collaborators to your site`**, immetti l&#39;indirizzo e-mail di un collaboratore, quindi fai clic su ![Icona segno di spunta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Continua ad aggiungere e-mail dei collaboratori, in base alle esigenze.</li><li>Al termine, fai clic su **Aggiungi collaboratori**.</li><li>Per condividere il collegamento con i collaboratori del contenuto, nella finestra di dialogo **Collaborazione aggiunta correttamente**, fai clic su **OK**.</li><li>Nella finestra di dialogo Collaborazione aggiunta correttamente, fai clic sull’![icona Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) per copiare il collegamento e condividerlo con i collaboratori.<br>Prima di condividere il collegamento, verifica che i collaboratori abbiano effettuato l’accesso con l’indirizzo e-mail associato al loro account IMS. Se il loro account e-mail IMS non è disponibile, sarà necessario utilizzare l’indirizzo e-mail aggiunto come collaboratore. In questo modo i collaboratori possono accedere al collegamento e visualizzare il contenuto da modificare o aggiornare in Google Drive.</li><li>Al termine della modifica, fare clic su **Pubblica sito** in Cloud Manager, come descritto in precedenza.<br>Oppure, visualizzare in anteprima le modifiche apportate, come descritto in precedenza.</li></ul> |
   | Concedere agli utenti l’accesso all’archivio di base su GitHub | <ul><li> Nella casella di riepilogo **Siti Edge Delivery**, all’estrema destra del nome del sito, fai clic sull’![icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per aprire il menu a discesa.</li><li>Fai clic su ![icona Codice](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **Ottieni l’accesso all’archivio di base** nel menu a discesa.</li><li>Nella finestra di dialogo **Accedi all’archivio di base del tuo sito**, immetti il nome utente GitHub di un collaboratore, quindi fai clic sull’![icona Segno di spunta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Continua ad aggiungere i nomi utente GitHub in base alle esigenze.</li><li>Al termine, fai clic su **Aggiungi collaboratori**.</li>Per visualizzare l’archivio, gli utenti devono concedere l’accesso al proprio nome utente GitHub. |

## Pubblicare contenuti da AEM Author ad Edge Delivery (Beta) {#publish-from-aem-author}

>[!NOTE]
>
>La funzione di pubblicazione qui descritta è in Beta. Per partecipare a Beta, invia un&#39;e-mail a [grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com) con il tuo ID organizzazione Adobe e l&#39;ID programma.

Questa funzionalità è disponibile solo per i siti Edge Delivery creati con l’opzione Authoring di AEM.

Dopo aver creato il sito Edge Delivery e aver eseguito la **verifica** in Cloud Manager, puoi creare e pubblicare contenuti utilizzando AEM Universal Editor.

**Per accedere all&#39;editor universale da Cloud Manager:**

1. Nell’elenco Siti Edge Delivery della scheda Edge Delivery individua il tuo sito.

   ![Pubblicazione di contenuto da AEM Author ad Edge Delivery](/help/implementing/cloud-manager/edge-delivery/assets/eds-content-source-link.png)

1. Fare clic sul collegamento **Source dei contenuti** nella riga del sito. Il collegamento consente di aprire la pagina AEM Universal Editor, da cui è possibile creare e modificare il contenuto del sito.

**Per pubblicare il contenuto:**

* **Da Cloud Manager** -

   1. Nella scheda **Distribuzione pubblicazione** della pagina **Panoramica**, nella scheda **Ambienti**, fai clic sull&#39;icona ![Informazioni o Informazioni](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) evidenziata.

   1. Nel pop-up informativo, seleziona **Fai clic per attivare** per abilitare il provisioning a livello di pubblicazione nell&#39;interfaccia utente di Cloud Manager.

      ![Fare clic per attivare il provisioning del livello di pubblicazione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/click-to-activate-publish-tier-capabilities.png)

   1. Nella finestra di dialogo Attiva livello di pubblicazione fare clic su **Attiva**.

      ![Finestra di dialogo Attiva livello di pubblicazione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/activate-publish-tier.png)

      Una volta attivato, il livello di pubblicazione viene fornito automaticamente. In alternativa, è possibile eseguire automaticamente il provisioning del livello di pubblicazione se l’autore tenta di pubblicare contenuti direttamente dall’interfaccia utente di AEM.

      Dopo l&#39;attivazione e il provisioning del livello di pubblicazione, il collegamento **Fai clic per attivare** diventa inattivo/non disponibile.

* **Da AEM Author**: nell&#39;interfaccia di authoring di AEM, fai clic su **Pubblicazione rapida** per pubblicare i contenuti direttamente sul tuo sito Edge Delivery. Il livello di pubblicazione non è necessario per questa operazione quando Edge Delivery gestisce la consegna.

Dopo la pubblicazione, visualizza l&#39;anteprima del contenuto all&#39;URL `.page` del sito o in tempo reale all&#39;URL `.live`.—>

