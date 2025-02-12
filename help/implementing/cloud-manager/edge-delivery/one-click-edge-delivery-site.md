---
title: Creare un sito Edge Delivery in Cloud Manager con un clic
description: Scopri come creare rapidamente un sito Edge Delivery in Cloud Manager con un clic.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8034fc8454fca41c2430fa1179f80d2d2ab80563
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 7%

---


# Informazioni sulla creazione di un sito Edge Delivery in Cloud Manager con un clic {#about-one-click-edge-delivery-site}

Il servizio EDS (One Click Edge Delivery Service) è progettato per automatizzare l’onboarding e la distribuzione di siti Edge Delivery all’interno di Cloud Manager. Semplifica notevolmente il processo facendo clic su un singolo pulsante. Questo singolo clic esegue il provisioning dell’infrastruttura richiesta, si integra con GitHub per il controllo della versione e configura l’archiviazione dei documenti e delle risorse in Google Drive.

Questa automazione consente di ridurre lo sforzo manuale necessario per configurare il sito iniziale. Garantisce flussi di lavoro ottimizzati, scalabilità e prestazioni migliori per i team quando si tratta di gestire i contenuti ai margini.

## Concetti fondamentali {#key-concepts}

Concetti chiave quando si utilizza un clic per creare un sito Edge Delivery.

| Concetto chiave | Descrizione |
| --- | --- |
| Distribuzione automatizzata di Edge | <ul><li>Gli utenti possono creare e configurare siti Edge Delivery all’istante.</li><li>Riduce o elimina la necessità di processi di onboarding manuali utilizzando l’integrazione di Cloud Manager con il flusso di lavoro CI/CD.</li><li>Integrato con Cloud Manager per flussi di lavoro CI/CD ottimizzati.</li></ul> |
| Integrazione con Cloud Manager | <ul><li>Utilizza l’interfaccia utente di Cloud Manager per attivare il processo Edge Delivery con un clic.</li><li>Consente di accedere alla creazione e alla distribuzione automatizzate dell&#39;archivio.</li></ul> |
| Controllo della versione basato su GitHub | <ul><li>Crea un archivio GitHub all’interno di un’organizzazione utilizzando modelli standard predefiniti per standardizzare le distribuzioni.</li><li>Collegamenti con AEM Bot per aggiornamenti dei contenuti.</li></ul> |
| Integrazione di archiviazione di documenti e risorse | <ul><li>Genera una cartella di Google Drive per l&#39;archiviazione.<li>Installa l&#39;applicazione AEM Code Sync nell&#39;archivio, garantendo la sincronizzazione e la distribuzione senza interruzioni.</li></li><li>Consente a più collaboratori di gestire facilmente i documenti.</li></ul> |
| Sicurezza e scalabilità | <ul><li>Garantisce la conformità agli standard di sicurezza aziendali.</li><li>Supporta più siti Edge Delivery con tenant Cloud Manager diversi.</li></ul> |



## Creare un sito Edge Delivery in Cloud Manager con un clic {#one-click-edge-delivery-site}

Per creare un sito di consegna Adobe Edge con un solo clic, la tua organizzazione deve disporre di una licenza Edge Delivery Services disponibile. Questa licenza fa parte di Adobe Experience Manager (AEM) ed è necessaria per la creazione di Edge Delivery Services all’interno di Cloud Manager.

In termini di autorizzazioni, devi avere il ruolo di Proprietario business o disporre delle autorizzazioni appropriate per aggiungere o modificare programmi in Cloud Manager. Questo livello di accesso consente di gestire l’integrazione di Edge Delivery Services nei programmi.

Consulta anche [Introduzione a Edge Delivery Services in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

LE CONFIGURAZIONI BOT DI AEM APPROPRIATE DEVONO ESSERE ATTIVATE PRIMA PER GLI AGGIORNAMENTI AUTOMATICI DEI CONTENUTI? VERO? FALSE?

**Per creare un sito Edge Delivery in Cloud Manager con un clic:**

1. Accedi a Cloud Manager all’indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e seleziona il programma appropriato.
1. Nell&#39;angolo superiore sinistro della pagina fare clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu sul lato sinistro.
1. Nel menu a sinistra, sotto l&#39;intestazione **Servizi**, fare clic su ![icona Pagina Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Siti Edge Delivery**.
1. Nella finestra di dialogo **Elenco attività di Edge Delivery** della pagina Edge Delivery fare clic su **Provisioning** nella casella di gruppo **Prerequisiti completi**.
1. Nella finestra di dialogo **Provisioning sito Edge Delivery**, immetti il nome del sito nel campo di testo **Nome progetto**, quindi fai clic su **Provisioning**.
Nella parte superiore centrale dello schermo viene visualizzato un avviso popup che informa dell’avvio del provisioning del sito Edge Delivery.
Una volta completato il provisioning e convalidato il sito, il nome del sito viene visualizzato nell&#39;area **Edge Delivery sites** della pagina Edge Delivery.

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