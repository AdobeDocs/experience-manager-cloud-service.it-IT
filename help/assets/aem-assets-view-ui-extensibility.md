---
title: Abilita estensibilità interfaccia utente in [!DNL AEM Assets View]
description: Scopri la funzionalità di estensibilità dell'interfaccia utente di  [!DNL AEM Assets View]. [!DNL AEM Assets View] UI consente di aggiungere componenti dell'interfaccia utente personalizzati per soddisfare esigenze aziendali specifiche.
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Abilita estensibilità interfaccia utente in [!DNL AEM Assets View] {#AEM-Assets-View-UI-Extensibility}

[!DNL AEM Assets View] supporta l&#39;estensibilità dell&#39;interfaccia utente, che consente di aggiungere componenti personalizzati all&#39;interfaccia utente di [!DNL Assets View] per flussi di lavoro e requisiti aziendali specifici che non sono soddisfatti dalle funzionalità predefinite di [!DNL AEM Assets View]. Questa funzionalità di estensibilità dell&#39;interfaccia utente di [!DNL AEM Assets View] ne migliora la flessibilità, consentendo alle organizzazioni di adattare l&#39;interfaccia per flussi di lavoro e requisiti specifici.\
Puoi aggiungere le estensioni al livello **Risorsa**, **Cartella** e **Raccolta**. L&#39;estensione aggiunta viene visualizzata in un pannello dedicato nella pagina **Risorsa**, **Raccolta** o **Cartella** **[!UICONTROL Dettagli]**.

>[!IMPORTANT]
>
> * Estensibilità dell&#39;interfaccia utente [!DNL AEM Assets View] disponibile con [[!DNL Assets Ultimate]](/help/assets/assets-ultimate-overview.md).
> * Per accedere all&#39;estensibilità dell&#39;interfaccia utente [!DNL Assets view], [crea e invia un [!DNL Adobe] caso di assistenza clienti](https://helpx.adobe.com/it/enterprise/using/support-for-experience-cloud.html).
> * Puoi fornire feedback sulla documentazione espandendo **[!UICONTROL le opzioni di feedback dettagliate]** e facendo clic su **[!UICONTROL Segnala un problema]**.

## <a id="1"></a> Accedi alla visualizzazione Assets{#add-UI-Extensibility-in-AEM-Assets-View}

Segui i passaggi indicati nell&#39;immagine seguente per accedere a [!DNL Assets View]:
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## Visualizza estensioni interfaccia utente in [!DNL Assets View] {#ui-extensibility-panel-assets-view}

In [!DNL Assets View], passa alla pagina **[!UICONTROL Dettagli]** di una risorsa, cartella o raccolta. Nella pagina **[!UICONTROL Dettagli]** viene visualizzata l&#39;estensione dell&#39;interfaccia utente aggiunta in un pannello dedicato.
![area di lavoro personale](/help/assets/assets/my-workspace-assets-view3.png)

## Prerequisiti per l’aggiunta del componente extensibility{#assets-view-ui-extensibility}

Per iniziare ad aggiungere il componente di estensibilità in [!DNL Assets View UI], è necessario soddisfare i seguenti requisiti:

* [Accesso a [!DNL Assets View]](#1).
* Accesso a [[!DNL Adobe app builder]](https://developer.adobe.com/app-builder/docs/overview/).
* Diritto allo sviluppatore del ruolo di amministratore di sistema all’interno dell’organizzazione. Per ulteriori informazioni, consulta [questa documentazione](https://developer.adobe.com/uix/docs/guides/get-access/).
* [!DNL Adobe IO command line tool (AIO CLI)] è installato nei computer locali. Questo strumento è essenziale per la creazione e la distribuzione di progetti di estensione. Per ulteriori informazioni, vedere [Creare la prima applicazione App Builder](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app#local-environment-set-up) (richiede l&#39;autenticazione per l&#39;accesso).
* Buona conoscenza delle tecnologie [!DNL JavaScript], [!DNL Node.js] e [!DNL React].

## Aggiungi il componente di estendibilità dell&#39;interfaccia utente a [!DNL Assets View] {#ui-extensibility-in-assets-view}

1. Consulta [Guida introduttiva](https://developer.adobe.com/uix/docs/getting-started/) per informazioni essenziali sulle estensioni dell&#39;interfaccia utente e sul framework [!DNL Adobe App Builder]. Scopri come l&#39;estensibilità dell&#39;interfaccia utente consente l&#39;integrazione di logica e interfaccia utente personalizzate in [!DNL Adobe Experience Cloud services] e l&#39;architettura e il flusso di lavoro per l&#39;implementazione delle estensioni dell&#39;interfaccia utente.
1. Consulta [Guide](https://developer.adobe.com/uix/docs/guides/) per informazioni generali sull&#39;estensibilità dell&#39;interfaccia utente, tra cui configurazione dell&#39;ambiente locale, anteprima locale, pubblicazione e gestione.
1. Consulta [Concetti comuni nella creazione di estensioni](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/) per informazioni sulle nozioni di base necessarie per sviluppare un&#39;estensione dell&#39;interfaccia utente per [!DNL AEM Assets View].
1. Aggiungere pannelli laterali personalizzati all&#39;interfaccia [!DNL Assets View]. L&#39;applicazione host ([!DNL Assets View]) gestisce questi pannelli per gestire le interazioni dell&#39;interfaccia utente, ad esempio l&#39;attivazione e il collegamento profondo. Le estensioni utilizzano il punto di estensione `aem/assets/details/1` per integrare pannelli personalizzati che specificano proprietà quali ID pannello, titolo e URL contenuto. Gli sviluppatori registrano i pannelli personalizzati con il metodo `getPanels()` e creano le route per visualizzare il contenuto personalizzato. Per informazioni dettagliate sull&#39;implementazione, inclusi riferimenti API ed esempi di codice, vedere [Visualizzazione dettagli](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/).
1. Configurare l&#39;ambiente locale e creare la prima estensione dell&#39;interfaccia utente per acquisire un&#39;esperienza diretta del processo di sviluppo delle estensioni dell&#39;interfaccia utente in [!DNL Assets View]. Per ulteriori dettagli, consulta [Sviluppo dell&#39;estensione AEM Assets View](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/) passo dopo passo.
1. Configurate l&#39;applicazione utilizzando la CLI AIO per generare la struttura di estensione di base e il codice richiesto. Per informazioni dettagliate, vedere [generazione del codice per [!DNL AEM Assets View]](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/).
1. Verifica le estensioni a livello locale per assicurarti che funzionino come previsto prima della distribuzione. Eseguire l&#39;estensione in un ambiente completamente isolato o con isolamento parziale e connettere l&#39;estensione all&#39;ambiente di produzione [!DNL AEM Assets View] per il test. Per informazioni dettagliate, vedere [Risoluzione dei problemi - [!DNL AEM Assets View] estensibilità](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/).

## Personalizzare le azioni nella vista Assets {#customize-actions-assets-view}

La vista AEM Assets consente di personalizzare le seguenti azioni nella vista Sfoglia:

* Personalizza le azioni da visualizzare quando selezioni una o più risorse nella barra delle azioni.

* Personalizza le azioni visualizzate quando fai clic su Altre opzioni (...) nella scheda delle risorse.

* Personalizza le azioni disponibili nel menu Intestazione.

Per ulteriori informazioni, vedere [Sfoglia visualizzazione](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/browse-view/).

## Apri finestre di dialogo personalizzate in visualizzazione Assets {#open-custom-dialogs-assets-view}

La vista Assets consente inoltre di aprire finestre di dialogo personalizzate con il testo desiderato. È inoltre possibile aggiungere collegamenti al testo. Per ulteriori informazioni, vedere [API modale](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/#modal-api).
