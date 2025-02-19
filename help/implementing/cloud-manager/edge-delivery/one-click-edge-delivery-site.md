---
title: Creare un sito Edge Delivery in Cloud Manager con un clic
description: Scopri come creare rapidamente un sito Edge Delivery in Cloud Manager con il clic di un pulsante.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8034fc8454fca41c2430fa1179f80d2d2ab80563
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 71%

---


# Informazioni sulla creazione di un sito Edge Delivery in Cloud Manager con un clic {#about-one-click-edge-delivery-site}

Il servizio One Click Edge Delivery Service (EDS) è progettato per automatizzare l’onboarding e la distribuzione di siti Edge Delivery all’interno di Cloud Manager. Il processo è notevolmente semplificato ed è sufficiente fare clic su un singolo pulsante. Con un singolo clic, infatti, si esegue il provisioning dell’infrastruttura richiesta, l’integrazione con GitHub per il controllo della versione e la configurazione del’archiviazione di documenti e risorse in Google Drive.

Questa automazione consente di ridurre le attività manuali necessarie per configurare il sito iniziale. Garantisce flussi di lavoro ottimizzati, scalabilità e prestazioni migliori per i team che gestiscono i contenuti su server Edge.

## Concetti fondamentali {#key-concepts}

Concetti chiave quando si utilizza un clic per creare un sito Edge Delivery.

| Concetto chiave | Descrizione |
| --- | --- |
| Implementazione Edge automatizzata | <ul><li>Gli utenti possono creare e configurare siti Edge Delivery all’istante.</li><li>Riduce o elimina la necessità di processi di onboarding manuali utilizzando l’integrazione di Cloud Manager con il flusso di lavoro CI/CD.</li><li>Integrato con Cloud Manager per flussi di lavoro CI/CD ottimizzati.</li></ul> |
| Integrazione con Cloud Manager | <ul><li>Per attivare il processo Edge Delivery con un clic viene utilizzata l’interfaccia utente di Cloud Manager.</li><li>Questo consente di accedere alla creazione e all’implementazione automatizzate dell’archivio.</li></ul> |
| Controllo delle versioni basato su GitHub | <ul><li>Un archivio GitHub viene creato all’interno di un’organizzazione utilizzando modelli standard predefiniti per garantire implementazioni standardizzate.</li><li>Si collega con il Bot di AEM per l’aggiornamento dei contenuti.</li></ul> |
| Integrazione con archiviazione di documenti e risorse | <ul><li>Per l’archiviazione viene generata una cartella Google Drive.<li>Nell’archivio viene installata l’app AEM Code Synch, che garantisce un processo diretto di sincronizzazione e implementazione.</li></li><li>Più collaboratori possono gestire facilmente i documenti.</li></ul> |
| Sicurezza e scalabilità | <ul><li>Viene garantita la conformità agli standard di sicurezza aziendali.</li><li>Sono supportati più siti Edge Delivery con tenant Cloud Manager diversi.</li></ul> |



## Creare un sito Edge Delivery in Cloud Manager con un clic {#one-click-edge-delivery-site}

Per creare un sito di consegna Adobe Edge con un solo clic, la tua organizzazione deve disporre di una licenza Edge Delivery Services disponibile. Questa licenza fa parte di Adobe Experience Manager (AEM) ed è necessaria per la creazione di Edge Delivery Services all’interno di Cloud Manager.

In termini di autorizzazioni, devi avere il ruolo di Proprietario business o disporre delle autorizzazioni appropriate per aggiungere o modificare programmi in Cloud Manager. Questo livello di accesso consente di gestire l’integrazione di Edge Delivery Services nei programmi.

Consulta anche [Introduzione a Edge Delivery Services in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

LE CONFIGURAZIONI DI BOT DI AEM APPROPRIATE DEVONO ESSERE GIÀ ATTIVATE PER GLI AGGIORNAMENTI AUTOMATICI DEI CONTENUTI? VERO? FALSO?

**Per creare un sito Edge Delivery in Cloud Manager con un clic:**

1. Accedi a Cloud Manager all’indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nell’angolo in alto a sinistra della pagina, fai clic sull’![icona Mostra menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu a sinistra.
1. Nel menu a sinistra, nella sezione **Servizi**, fai clic su ![icona Pagina web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Siti Edge Delivery**.
1. Nella finestra di dialogo **Elenco attività di Edge Delivery** della pagina Edge Delivery fai clic su **Provisioning** nella casella del gruppo **Completa i prerequisiti**.
1. Nella finestra di dialogo **Provisioning del sito Edge Delivery**, immetti il nome del sito nel campo di testo **Nome progetto**, quindi fai clic su **Provisioning**.
Nella parte superiore centrale della schermata viene visualizzato una notifica che informa dell’avvio del provisioning del sito Edge Delivery.
Una volta completato il provisioning e convalidato il sito, il nome del sito viene visualizzato nell’area **Siti Edge Delivery** della pagina Edge Delivery.

### Esplora un nuovo sito Edge Delivery creato


1. Fai clic sul collegamento Archivio Git a destra del nome del sito.

Pubblica.

Fare clic su Nome sito,

apporta alcune modifiche, quindi pubblica

Visualizza la pagina in Anteprima, quindi modifica l’URL per visualizzare la versione Live.

Aggiungi collaboratori.


## Visualizzare l’anteprima di un sito Edge Delivery con un clic

## Pubblicare un sito Edge Delivery con un solo clic





## Aggiungere collaboratori a un sito Edge Delivery con un solo clic


































Questi miglioramenti mirano ad aumentare l’automazione, semplificare i processi di configurazione e valorizzare la collaborazione degli utenti di Edge Delivery Services. <!-- CMGR-59362 -->

![Crea un sito Edge Delivery con un clic](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

![Finestra di dialogo Provisioning del sito Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)