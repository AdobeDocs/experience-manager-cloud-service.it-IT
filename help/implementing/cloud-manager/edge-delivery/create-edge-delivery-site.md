---
title: Creazione di un sito Edge Delivery in Cloud Manager
description: Scopri come creare rapidamente un sito Edge Delivery in Cloud Manager con un clic.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1e4e07d2690bcbd44ffe994a571ffc0a8ae7eb50
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 24%

---


# Informazioni sulla creazione di un sito Edge Delivery in Cloud Manager {#about-one-click-edge-delivery-site}

La funzione Crea un sito Edge Delivery è progettata per aiutarti ad automatizzare l’onboarding e la distribuzione di siti Edge Delivery all’interno di Cloud Manager. Il processo è notevolmente semplificato ed è sufficiente fare clic su un singolo pulsante. Con un singolo clic, infatti, si esegue il provisioning dell’infrastruttura richiesta, l’integrazione con GitHub per il controllo della versione e la configurazione del’archiviazione di documenti e risorse in Google Drive.

Questa automazione consente di ridurre le attività manuali necessarie per configurare il sito iniziale. Garantisce flussi di lavoro ottimizzati, scalabilità e prestazioni migliori per i team che gestiscono i contenuti su server Edge.

## Concetti fondamentali {#key-concepts}

Concetti chiave quando crei un sito Edge Delivery in Cloud Manager con un clic.

| Concetto chiave | Descrizione |
| --- | --- |
| Implementazione Edge automatizzata | <ul><li>Gli utenti possono creare e configurare siti Edge Delivery all’istante.</li><li>Grazie all&#39;integrazione di Cloud Manager con il flusso di lavoro CI/CD, riduce o elimina la necessità di processi di onboarding manuali.</li><li>Integrato con Cloud Manager per flussi di lavoro CI/CD ottimizzati.</li></ul> |
| Integrazione con Cloud Manager | <ul><li>Per attivare il processo Edge Delivery con un clic viene utilizzata l’interfaccia utente di Cloud Manager.</li><li>Fornire accesso alla creazione e alla distribuzione automatizzate dell’archivio.</li></ul> |
| Controllo delle versioni basato su GitHub | <ul><li>Un archivio GitHub viene creato all’interno di un’organizzazione utilizzando modelli standard predefiniti per garantire implementazioni standardizzate.</li><li>Si collega con il Bot di AEM per l’aggiornamento dei contenuti.</li></ul> |
| Integrazione con archiviazione di documenti e risorse | <ul><li>Per l’archiviazione viene generata una cartella Google Drive.<li>Nell’archivio viene installata l’app AEM Code Synch, che garantisce un processo diretto di sincronizzazione e implementazione.</li></li><li>I collaboratori possono gestire i documenti in modo semplice.</li></ul> |
| Sicurezza e scalabilità | <ul><li>Viene garantita la conformità agli standard di sicurezza aziendali.</li><li>Supporta più siti Edge Delivery con tenant Cloud Manager diversi.</li></ul> |

<!-- >
## Practical use cases {#use-cases}

| Use case | Description |
| --- | --- |
| Website and application deployment | <ul><li>Automate the hosting and delivery of static or dynamic sites.</li><li>Ensure fast performance through edge caching. </li></ul> |
| API gateway and content delivery | <ul><li>Optimize API responses by caching data at the edge.</li><li>Reduce backend load and improved response times. </li></ul> |
| Real-time content updates | <ul><li>Instant deployment of new content across edge locations.</li><li>Support integration with automated content pipelines. </li></ul> |
| Edge computing workloads | <ul><li>Support serverless computing to process workloads closer to users.</li><li>Reduce latency and enhance performance. </li></ul> |
| Security and governance | <ul><li>Security is provided with integrated DDoS (Distributed Denial of Service) protection and WAF (Web Application Firewall) integration.</li><li>Ensure that content is delivered securely through TLS (Transport Security Layer) encryption. </li></ul> |
-->

## Creare un sito Edge Delivery in Cloud Manager con un clic {#one-click-edge-delivery-site}

Per creare un sito di consegna Adobe Edge con un clic, la tua organizzazione deve disporre di una licenza Edge Delivery Services disponibile. Questa licenza fa parte di Adobe Experience Manager (AEM) ed è necessaria per la creazione di Edge Delivery Services all’interno di Cloud Manager.

In termini di autorizzazioni, devi avere il ruolo di Proprietario business o disporre delle autorizzazioni appropriate per aggiungere o modificare programmi in Cloud Manager. Questo livello di accesso consente di gestire l’integrazione di Edge Delivery Services nei programmi.

Consulta anche [Introduzione a Edge Delivery Services in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**Per creare un sito Edge Delivery in Cloud Manager con un clic:**

1. Accedi a Cloud Manager all’indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nell’angolo in alto a sinistra della pagina, fai clic sull’![icona Mostra menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu a sinistra.
1. Nel menu a sinistra, sotto l&#39;intestazione **Programma**, fare clic su **Panoramica**.
1. Nella pagina **Panoramica programma**, fare clic sulla scheda **Edge Delivery**.
1. Nella finestra di dialogo **Elenco attività di Edge Delivery** della pagina Edge Delivery fare clic su **Crea sito ora** nella casella di gruppo **Aggiungi sito Edge Delivery**.
1. Nella finestra di dialogo **Crea sito Edge Delivery**, immetti il nome del sito nel campo di testo **Nome progetto**, quindi fai clic su **Crea sito ora**.

   Nella parte superiore centrale dello schermo viene visualizzato un avviso popup che informa dell’avvio del provisioning del sito Edge Delivery.

Quando il provisioning e la convalida del sito vengono completati da Cloud Manager, il **Nome sito** (il nome del progetto immesso in precedenza) viene visualizzato nella casella di riepilogo **Siti Edge Delivery** nella pagina Edge Delivery. A sinistra dell’URL del repository viene inoltre visualizzato un segno di spunta verde.


### Esplora un sito Edge Delivery creato con un clic {#explore-one-click-ed-site}

1. Accedi a Cloud Manager all’indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nell’angolo in alto a sinistra della pagina, fai clic sull’![icona Mostra menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu a sinistra.
1. Nel menu a sinistra, sotto l&#39;intestazione **Programma**, fare clic su **Panoramica**.
1. Nella pagina **Panoramica programma**, fare clic sulla scheda **Edge Delivery**.
1. Nella pagina Edge Delivery, effettua una delle seguenti operazioni:

   | Cosa esplorare | Passaggi |
   | --- | --- |
   | Archivio GitHub di un sito | <ul><li>Nella casella di riepilogo **Siti Edge Delivery**, sotto l&#39;intestazione di colonna **Archivio**, fare clic sull&#39;URL del sito appena creato.<br>Potrebbe essere necessario accedere a GitHub con il proprio nome utente o indirizzo e-mail e la password.</li> |
   | Pubblicare un sito | <ul><li> Nella casella di riepilogo **Siti Edge Delivery**, all&#39;estrema destra del nome del sito, fare clic su ![Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per aprire il menu a discesa.</li><li>Fai clic sull&#39;icona ![Publish Check](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **Publish site** nel menu a discesa.<br>Viene visualizzato un messaggio che informa che la pubblicazione del sito è stata avviata correttamente.</li></ul> |
   | Anteprima di un sito pubblicato | <ul><li>Nella casella di riepilogo **Siti Edge Delivery**, sotto l&#39;intestazione della colonna **Nome sito**, fare clic sull&#39;URL del sito appena creato e pubblicato.<br>Nella barra degli indirizzi URL del browser, l&#39;URL del sito termina con `.page`, a indicare che è visualizzata un&#39;anteprima del sito.</li><li>Per visualizzare il sito in tempo reale, modificare manualmente `.page` in `.live` nella barra degli indirizzi URL.</li></ul> |
   | Concedi agli utenti l&#39;accesso all&#39;archivio dei contenuti su Google Drive | <ul><li> Nella casella di riepilogo **Siti Edge Delivery**, all&#39;estrema destra del nome del sito, fare clic su ![Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per aprire il menu a discesa.</li><li>Fai clic sull&#39;icona ![Utenti Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **Accedi all&#39;archivio dei contenuti** nel menu a discesa.</li><li>Nella finestra di dialogo **Aggiungi collaboratori al sito**, immetti l&#39;indirizzo di posta elettronica di un collaboratore, quindi fai clic su ![icona segno di spunta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Continua ad aggiungere e-mail ai collaboratori, in base alle esigenze.</li><li>Al termine, fare clic su **Aggiungi collaboratori**.</li><li>Per condividere il collegamento con i tuoi collaboratori di contenuti, nella finestra di dialogo **Collaboration aggiunto correttamente**, fai clic su **OK**.</li><li>Nella finestra di dialogo Aggiunta di Collaboration, fai clic sull&#39;icona ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) per copiare il collegamento e condividerlo con i tuoi collaboratori.<br>Prima di condividere il collegamento, verifica che i collaboratori abbiano effettuato l&#39;accesso con l&#39;indirizzo e-mail associato al loro account IMS. Se il loro account e-mail IMS non è disponibile, devono utilizzare l’indirizzo e-mail aggiunto come collaboratore. In questo modo i collaboratori possono accedere al collegamento e visualizzare il contenuto da modificare o aggiornare in Google Drive.</li><li>Al termine della modifica, fare clic su **Pubblica sito** in Cloud Manager, come descritto in precedenza.<br>Oppure, visualizzare in anteprima le modifiche apportate, come descritto in precedenza.</li></ul> |
   | Concedi agli utenti l’accesso all’archivio di base su GitHub | <ul><li> Nella casella di riepilogo **Siti Edge Delivery**, all&#39;estrema destra del nome del sito, fare clic su ![Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per aprire il menu a discesa.</li><li>Fai clic sull&#39;icona ![Codice](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **Accedi all&#39;archivio di base** nel menu a discesa.</li><li>Nella finestra di dialogo **Accedi all&#39;archivio di base per il sito**, immetti il nome utente GitHub di un collaboratore, quindi fai clic su ![Icona segno di spunta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Continua ad aggiungere i nomi utente GitHub in base alle esigenze.</li><li>Al termine, fare clic su **Aggiungi collaboratori**.</li>Per visualizzare l’archivio, gli utenti devono concedere l’accesso al proprio nome utente GitHub. |


