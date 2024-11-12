---
title: Estensibilità dell’interfaccia utente di visualizzazione di AEM Assets
description: Scopri la funzionalità di estensibilità dell’interfaccia utente di AEM Assets View. L’interfaccia utente di AEM Assets View consente di aggiungere componenti personalizzati dell’interfaccia utente per soddisfare esigenze aziendali specifiche.
feature: App Builder
role: User, Developer
source-git-commit: c1446200898102881a20508031d4853c61f7c964
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 3%

---

# Estensibilità dell’interfaccia utente di visualizzazione di AEM Assets{#AEM-Assets-View-UI-Extensibility}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Media con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione di AEM Assets per sviluppatori](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

La vista AEM Assets dispone della funzionalità di estensibilità dell’interfaccia utente. Questa funzionalità consente agli utenti di aggiungere componenti personalizzati all’interfaccia utente di Assets View per soddisfare esigenze aziendali specifiche che le funzionalità predefinite della visualizzazione AEM Assets non soddisfano. Questa funzione di estensibilità migliora la flessibilità di AEM Assets View, che consente alle organizzazioni di adattare l’interfaccia per flussi di lavoro e requisiti specifici.
Puoi aggiungere le estensioni a livello di risorsa, cartella e raccolta. L’estensione aggiunta viene visualizzata in un pannello dedicato nella pagina Dettagli della risorsa, della raccolta o della cartella.

>[!IMPORTANT]
> L&#39;estensibilità dell&#39;interfaccia utente di visualizzazione di AEM Assets è disponibile con [Assets Ultimate](/help/assets/assets-ultimate-overview.md).

## <a id="1"></a> Come accedere alla vista Assets

Accedi alla vista Assets nei seguenti modi:
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## Dove viene visualizzato il componente Estensibilità dell’interfaccia utente aggiunto nell’interfaccia utente di visualizzazione di Assets? {#ui-extensibility-panel-assets-view}

Nella Vista Assets, passa alla pagina Dettagli di una risorsa, cartella o raccolta. In questa pagina Dettagli è presente un pannello dedicato che mostra l’estensione dell’interfaccia utente aggiunta.
![area di lavoro personale](/help/assets/assets/my-workspace-assets-view3.png)

>[!NOTE]
>
> L’estensibilità dell’interfaccia utente di visualizzazione di AEM Assets è disponibile nella versione di as a Beta. Puoi fornire feedback sulla documentazione espandendo le opzioni di feedback dettagliato e facendo clic su Segnala un problema.

## Prerequisiti per l’aggiunta del componente Estensibilità

* [Accesso alla visualizzazione Assets](#1).
* Adobe Accesso a [Generatore di app](https://developer.adobe.com/app-builder/docs/overview/), incluso in [Assets Ultimate](/help/assets/assets-ultimate-overview.md) per impostazione predefinita.
* Autorizzato a Sviluppatore del ruolo Amministratore di sistema all’interno dell’organizzazione. Per ulteriori informazioni, vedere [questo](https://developer.adobe.com/uix/docs/guides/get-access/).
* Lo strumento per riga di comando Adobe IO (AIO CLI) deve essere installato sui computer locali. Questo strumento è essenziale per la creazione e la distribuzione di progetti di estensione. Per ulteriori informazioni, vedere [questo](https://developer.adobe.com/app-builder/docs/getting_started/#local-environment-set-up).
* Buona conoscenza delle tecnologie JavaScript, Node.js e React.

## Aggiunta del componente Estensibilità dell’interfaccia utente nell’interfaccia di visualizzazione di Assets{#Adding-UI-Extensibility-Component-on-Assets-View}

1. Consulta [Guida introduttiva](https://developer.adobe.com/uix/docs/getting-started/) per informazioni essenziali sulle estensioni dell&#39;interfaccia utente e sul framework di Adobe App Builder. Scopri come l’estensibilità dell’interfaccia utente consente l’integrazione di logica e interfaccia utente personalizzate all’interno dei servizi Adobe Experience Cloud e l’architettura e il flusso di lavoro per l’implementazione delle estensioni dell’interfaccia utente.
1. Consulta [Guide](https://developer.adobe.com/uix/docs/guides/) per informazioni generali sull&#39;estensibilità dell&#39;interfaccia utente, tra cui configurazione dell&#39;ambiente locale, anteprima locale, pubblicazione e gestione.
1. Consulta [Concetti comuni nella sezione Creazione di estensioni](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/) per informazioni sulle nozioni di base necessarie per sviluppare un&#39;estensione dell&#39;interfaccia utente per la visualizzazione AEM Assets.
1. Aggiungi pannelli laterali personalizzati all’interfaccia di visualizzazione di Assets. L’applicazione host (Assets View) gestisce questi pannelli per gestire le interazioni dell’interfaccia utente, ad esempio l’attivazione e il collegamento profondo. Le estensioni utilizzano il punto di estensione `aem/assets/details/1` per integrare pannelli personalizzati che specificano proprietà quali ID pannello, titolo e URL contenuto. Gli sviluppatori registrano i pannelli personalizzati con il metodo `getPanels()` e creano le route per visualizzare il contenuto personalizzato. Per informazioni dettagliate sull&#39;implementazione, inclusi riferimenti API ed esempi di codice, vedere [Visualizzazione dettagli](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/).
1. Configura l&#39;ambiente locale e scopri come sviluppare estensioni dell&#39;interfaccia utente nella vista Assets creando la prima estensione dell&#39;interfaccia utente. Per ulteriori dettagli, consulta [Sviluppo dell&#39;estensione AEM Assets View](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/) passo dopo passo.
1. Configura l’app utilizzando AIO CLI per generare la struttura di estensione di base e il codice richiesto. Per informazioni dettagliate, consulta [Generazione del codice per la visualizzazione AEM Assets](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/).
1. Verifica le estensioni a livello locale per assicurarti che funzionino come previsto prima della distribuzione. Esegui l’estensione in un ambiente completamente isolato o con isolamento parziale e connetti l’estensione alla visualizzazione AEM Assets di produzione per il test. Per informazioni dettagliate, consulta [Risoluzione dei problemi - Estendibilità visualizzazione AEM Assets](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/).


