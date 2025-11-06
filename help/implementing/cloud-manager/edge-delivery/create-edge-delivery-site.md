---
title: Creare il primo sito Edge Delivery con un clic
description: Scopri come creare rapidamente un sito Edge Delivery in Cloud Manager con il solo clic di un pulsante.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 100%

---

# Creare il primo sito Edge Delivery con un clic{#about-one-click-edge-delivery-site}

La creazione del primo sito Edge Delivery con un clic è progettata per consentirti di automatizzare l’onboarding e la distribuzione di siti Edge Delivery all’interno di Cloud Manager. Il processo è notevolmente semplificato ed è sufficiente fare clic su un singolo pulsante. Con un singolo clic, infatti, si esegue il provisioning dell’infrastruttura richiesta, l’integrazione con GitHub per il controllo della versione e la configurazione del’archiviazione di documenti e risorse in Google Drive.

Questa automazione consente di ridurre le attività manuali necessarie per configurare il sito iniziale. Garantisce flussi di lavoro ottimizzati, scalabilità e prestazioni migliori per i team che gestiscono i contenuti su server Edge.

<!-- Check out this quick 2-minute video for a step-by-step walkthrough on creating your first Edge Delivery site—no hassle, just one click.

>[!VIDEO](https://video.tv.adobe.com/v/3458975?quality=12&learn=on) -->



<!--
## Practical use cases {#use-cases}

| Use case | Description |
| --- | --- |
| Website and application deployment | <ul><li>Automate the hosting and delivery of static or dynamic sites.</li><li>Ensure fast performance through edge caching. </li></ul> |
| API gateway and content delivery | <ul><li>Optimize API responses by caching data at the edge.</li><li>Reduce backend load and improved response times. </li></ul> |
| Real-time content updates | <ul><li>Instant deployment of new content across edge locations.</li><li>Support integration with automated content pipelines. </li></ul> |
| Edge computing workloads | <ul><li>Support serverless computing to process workloads closer to users.</li><li>Reduce latency and enhance performance. </li></ul> |
| Security and governance | <ul><li>Security is provided with integrated DDoS (Distributed Denial of Service) protection and WAF (Web Application Firewall) integration.</li><li>Ensure that content is delivered securely through TLS (Transport Security Layer) encryption. </li></ul> |
-->





## Creare un sito Edge Delivery in Cloud Manager con un solo clic {#one-click-edge-delivery-site}

Per creare un sito Adobe Edge Delivery con un solo clic, l’organizzazione deve disporre di una licenza Edge Delivery Services. Questa licenza fa parte di Adobe Experience Manager (AEM) ed è necessaria per la creazione di Edge Delivery Services all’interno di Cloud Manager.

In termini di autorizzazioni, devi avere il ruolo di Proprietario business o disporre delle autorizzazioni appropriate per aggiungere o modificare programmi in Cloud Manager. Questo livello di accesso consente di gestire l’integrazione di Edge Delivery Services nei programmi.

Consulta anche [Introduzione a Edge Delivery Services in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**Per creare un sito Edge Delivery in Cloud Manager con un solo clic:**

1. Accedi a Cloud Manager all’indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nell’angolo in alto a sinistra della pagina, fai clic sull’![icona Mostra menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu a sinistra.
1. Nel menu a sinistra, sotto l’intestazione **Programma**, fai clic su **Panoramica**.
1. Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**.
1. Nella finestra di dialogo **Elenco attività di Edge Delivery** della pagina Edge Delivery, fai clic su **Crea sito ora** nella casella del gruppo **Aggiungi sito Edge Delivery**.
1. Nella finestra di dialogo **Crea sito Edge Delivery**, immetti il nome del sito nel campo di testo **Nome progetto**, quindi fai clic su **Crea sito ora**.

   Nella parte superiore centrale della schermata viene visualizzata una notifica pop-up che informa dell’avvio del provisioning del sito Edge Delivery.

Quando il provisioning e la convalida del sito vengono completati da Cloud Manager, il **Nome sito** (il nome del progetto immesso in precedenza) viene visualizzato nella casella di riepilogo **Siti Edge Delivery** nella pagina Edge Delivery. A sinistra dell’URL dell’archivio viene inoltre visualizzato un segno di spunta verde.


### Esplorare un sito Edge Delivery creato con un clic {#explore-one-click-ed-site}

1. Accedi a Cloud Manager all’indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nell’angolo in alto a sinistra della pagina, fai clic sull’![icona Mostra menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu a sinistra.
1. Nel menu a sinistra, sotto l’intestazione **Programma**, fai clic su **Panoramica**.
1. Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**.
1. Nella pagina Edge Delivery, effettua una delle seguenti operazioni:

   | Cosa esplorare | Passaggi |
   | --- | --- |
   | Archivio GitHub di un sito | <ul><li>Nella casella di riepilogo **Siti Edge Delivery**, sotto l’intestazione di colonna **Archivio**, fai clic sull’URL del sito appena creato.<br>Potrebbe essere necessario accedere a GitHub con il proprio nome utente o indirizzo e-mail e la password.</li> |
   | Pubblicare un sito | <ul><li> Nella casella di riepilogo **Siti Edge Delivery**, all’estrema destra del nome del sito, fai clic sull’![icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per aprire il menu a discesa.</li><li>Fai clic su ![icona Controllo pubblicazione](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **Pubblica sito** nel menu a discesa.<br>Viene visualizzato un messaggio pop-up che informa che la pubblicazione del sito è stata avviata correttamente.</li></ul> |
   | Visualizzare l’anteprima di un sito pubblicato | <ul><li>Nella casella di riepilogo **Siti Edge Delivery**, sotto l’intestazione della colonna **Nome sito**, fai clic sull’URL del sito appena creato e pubblicato.<br>Nella barra degli indirizzi URL del browser, l’URL del sito termina con `.page` e indica che stai visualizzando un’anteprima del sito.</li><li>Per visualizzare il sito live, modifica manualmente `.page` in `.live` nella barra degli indirizzi URL.</li></ul> |
   | Concedere agli utenti l’accesso all’archivio dei contenuti su Google Drive | <ul><li> Nella casella di riepilogo **Siti Edge Delivery**, all’estrema destra del nome del sito, fai clic sull’![icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per aprire il menu a discesa.</li><li>Fai clic su![icona Aggiunta utenti](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **Ottieni l’accesso all’archivio dei contenuti** nel menu a discesa.</li><li>Nella finestra di dialogo **Aggiungi collaboratori al sito**, immetti l’indirizzo e-mail di un collaboratore, quindi fai clic sull’![icona Segno di spunta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Continua ad aggiungere e-mail dei collaboratori, in base alle esigenze.</li><li>Al termine, fai clic su **Aggiungi collaboratori**.</li><li>Per condividere il collegamento con i collaboratori del contenuto, nella finestra di dialogo **Collaborazione aggiunta correttamente**, fai clic su **OK**.</li><li>Nella finestra di dialogo Collaborazione aggiunta correttamente, fai clic sull’![icona Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) per copiare il collegamento e condividerlo con i collaboratori.<br>Prima di condividere il collegamento, verifica che i collaboratori abbiano effettuato l’accesso con l’indirizzo e-mail associato al loro account IMS. Se il loro account e-mail IMS non è disponibile, sarà necessario utilizzare l’indirizzo e-mail aggiunto come collaboratore. In questo modo i collaboratori possono accedere al collegamento e visualizzare il contenuto da modificare o aggiornare in Google Drive.</li><li>Al termine della modifica, fai clic su **Pubblica sito** in Cloud Manager, nel modo descritto in precedenza.<br>Oppure, visualizza in anteprima le modifiche apportate, nel modo descritto in precedenza.</li></ul> |
   | Concedere agli utenti l’accesso all’archivio di base su GitHub | <ul><li> Nella casella di riepilogo **Siti Edge Delivery**, all’estrema destra del nome del sito, fai clic sull’![icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per aprire il menu a discesa.</li><li>Fai clic su ![icona Codice](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **Ottieni l’accesso all’archivio di base** nel menu a discesa.</li><li>Nella finestra di dialogo **Accedi all’archivio di base del tuo sito**, immetti il nome utente GitHub di un collaboratore, quindi fai clic sull’![icona Segno di spunta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Continua ad aggiungere i nomi utente GitHub in base alle esigenze.</li><li>Al termine, fai clic su **Aggiungi collaboratori**.</li>Per visualizzare l’archivio, gli utenti devono concedere l’accesso al proprio nome utente GitHub. |
