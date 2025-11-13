---
title: Estensione dell’editor universale
description: Scopri le diverse opzioni per estendere le funzionalità dell’editor universale e supportare le esigenze degli autori di contenuti.
feature: Developing
role: Admin, Developer
exl-id: 2f487fa5-57a7-477a-ad68-590e6cc12f4e
source-git-commit: d938abce2b46786343b19113454da1738a824ed0
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 100%

---

# Estensione dell’editor universale {#extending}

Scopri le diverse opzioni per estendere le funzionalità dell’editor universale e supportare le esigenze degli autori di contenuti.

>[!TIP]
>
>L’editor universale offre anche diverse [opzioni di personalizzazione](/help/implementing/universal-editor/customizing.md) che consentono di soddisfare meglio le esigenze del progetto.

## Estensioni {#extensions}

Come servizio di Adobe Experience Cloud, l’interfaccia utente dell’editor universale può essere estesa utilizzando App Builder e Experience Manager. Adobe offre molte estensioni già pronte disponibili tramite [Extension Manager](https://experience.adobe.com/aem/extension-manager) che puoi utilizzare per il tuo progetto.

* **[Estensione MSM (Gestione multi-sito) di AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)**: interrompi o ripristina l’ereditarietà a livello di componente
* **[Estensione Proprietà della pagina AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#page-properties)**: accedi alla finestra delle proprietà della pagina nell’editor universale.
* **[Estensione Amministratore del sito AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#sites-console)**: apri la console Sites alla posizione della pagina nell’editor universale
* **[Estensione Blocco pagina AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#locking-pages)**: visualizza e modifica lo stato di blocco della pagina dall’editor universale
* **[Estensione Flussi di lavoro AEM](/help/sites-cloud/authoring/universal-editor/authoring.md#workflows)**: avvia flussi di lavoro sulla pagina e sul contenuto della pagina dall’editor universale
* **[Generare varianti](/help/generative-ai/generate-variations-integrated-editor.md)**: utilizza l’intelligenza artificiale generativa (IA) per creare varianti per il contenuto direttamente nel pannello delle proprietà.
* **[Selettore del prodotto AEM per l’editor universale](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**: integra i dati di Adobe Commerce selezionando o rimuovendo i dati di prodotto dall’editor.
* **[Bozze di contenuto dell’editor universale](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**: crea, modifica e gestisci più bozze di contenuto.
* **[Selettore risorsa configurabile](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**: abilita la selezione delle risorse da archivi diversi da quello utilizzato dalla pagina modificata.
* **Editor regole di Forms**: aggiungi un comportamento dinamico ai campi di AEM Forms visivamente, senza codifica.
* **[Esporta frammenti di contenuto in Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**: esporta frammenti di contenuto creati in Adobe Experience Manager as a Cloud Service in Adobe Target, da utilizzare come offerte nelle attività di Target, per testare e personalizzare le esperienze su larga scala.
* **[Flussi di lavoro per frammento di contenuto](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**: avvia un flusso di lavoro AEM per i frammenti di contenuto selezionati.

Per informazioni su come abilitare queste estensioni, [consulta la documentazione di Extension Manager.](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)

## Estensione dell’interfaccia utente {#extending-ui}

Le estensioni dell’interfaccia utente dell’editor universale sono applicazioni JavaScript create con Adobe App Builder. Utilizzando questi stessi strumenti, puoi anche aggiungere pulsanti e azioni personalizzati al menu e al pannello delle proprietà dell’intestazione e creare eventi personalizzati per l’editor universale.

Se desideri esplorare le possibilità di creazione di estensioni personalizzate, consulta le seguenti risorse:

1. [Estensibilità dell’interfaccia utente](https://developer.adobe.com/uix/docs/): questa è la documentazione per gli sviluppatori relativa all’estensione dell’interfaccia utente.
1. [Guide all’estendibilità dell’interfaccia utente](https://developer.adobe.com/uix/docs/guides/): istruzioni dettagliate su come sviluppare un’estensione personalizzata
1. [Punti di estensione dell’interfaccia utente dell’editor universale](https://developer.adobe.com/uix/docs/services/aem-universal-editor/): documentazione relativa al punto di estensione specifica dell’editor universale

>[!TIP]
>
>Se preferisci imparare tramite esempio, consulta il [tutorial sull’estensibilità dell’interfaccia utente di AEM](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview). Anche se si concentra sull’estensione della console Frammenti di contenuto, i concetti per l’implementazione di un’estensione dell’interfaccia utente nell’editor universale sono gli stessi.

[Utilizzando Extension Manager in AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/), puoi abilitare o disabilitare le estensioni per singole istanze, accedere alle estensioni di prime parti di Adobe, incluse quelle per l’editor universale, e molto altro.

## Punti dell’estensione {#extension-points}

Oltre all’estensibilità dell’interfaccia utente, l’editor universale offre molti altri punti di estensione flessibili per consentire l’integrazione ottimizzata di requisiti aziendali personalizzati.

* **[Blocchi](https://www.aem.live/developer/block-collection)**: in formato JSON semplice, i progetti possono regolare i blocchi e utilizzare le funzionalità dell’editor universale disponibili per la creazione di contenuti.
* **[Interfaccia utente personalizzata](#extending-ui)**: le estensioni possono visualizzare l’interfaccia utente necessaria nei pannelli laterali o nelle finestre di dialogo modali.
* **[Eventi](/help/implementing/universal-editor/events.md)**: le estensioni ricevono eventi sulle azioni dell’autore e sulle selezioni effettuate nella pagina per rispondere in modo appropriato.
