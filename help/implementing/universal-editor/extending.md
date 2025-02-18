---
title: Estensione dell’editor universale
description: Scopri le diverse opzioni per estendere le funzionalità di Universal Editor e supportare le esigenze degli autori di contenuti.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0cab4a807be4aa402667feddb6a948f0d2db371f
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# Estensione dell’editor universale {#extending}

Scopri le diverse opzioni per estendere le funzionalità di Universal Editor e supportare le esigenze degli autori di contenuti.

>[!TIP]
>
>L&#39;editor universale offre anche diverse [opzioni di personalizzazione](/help/implementing/universal-editor/customizing.md) che consentono di soddisfare meglio le esigenze del progetto.

## Estensioni {#extensions}

In qualità di servizio di Adobe Experience Cloud, l’interfaccia utente dell’editor universale può essere estesa utilizzando App Builder e Experience Manager. Adobe offre molte estensioni pronte che puoi utilizzare per il tuo progetto.

* **[Selettore prodotti AEM per Universal Editor](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/ue-product-picker/)**: integra i dati di Adobe Commerce selezionando o rimuovendo i dati di prodotto dall&#39;editor.
* **[Bozze di contenuto dell&#39;Editor universale](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/universal-editor-content-drafts/)**: crea, modifica e gestisci più bozze di contenuto.
* **[Selettore risorse configurabile](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/)**: abilita la selezione delle risorse dai repository diversi da quello utilizzato dalla pagina modificata.
* **Editor regole Forms**: aggiungi un comportamento dinamico ai campi di AEM Forms visivamente, senza codificare.
* **[Esporta frammenti di contenuto in Adobe Target](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/exporting-content-fragment-to-adobe-target/)**: esporta frammenti di contenuto creati in Adobe Experience Manager as a Cloud Service in Adobe Target da utilizzare come offerte nelle attività di Target, per testare e personalizzare le esperienze su larga scala.
* **[Flussi di lavoro per frammenti di contenuto](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/content-fragments-workflows/)**: avvia un flusso di lavoro AEM per i frammenti di contenuto selezionati.

## Estensione dell’interfaccia utente {#extending-ui}

Le estensioni dell’interfaccia utente di Universal Editor sono applicazioni JavaScript create con Adobe App Builder. Utilizzando questi stessi strumenti, puoi anche aggiungere pulsanti e azioni personalizzati al menu e al pannello delle proprietà dell’intestazione e creare eventi personalizzati per Universal Editor.

Se desideri esplorare le possibilità di creazione di estensioni personalizzate, consulta le seguenti risorse:

1. [Estensibilità interfaccia utente](https://developer.adobe.com/uix/docs/) - Questa è la documentazione per gli sviluppatori per l&#39;estensione dell&#39;interfaccia utente.
1. [Guide all&#39;estendibilità dell&#39;interfaccia utente](https://developer.adobe.com/uix/docs/guides/): istruzioni dettagliate su come sviluppare un&#39;estensione personalizzata
1. [Punti di estensione dell&#39;interfaccia utente di Universal Editor](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - Documentazione del punto di estensione specifica di Universal Editor

>[!TIP]
>
>Se preferisci imparare da esempio, consulta l&#39;[esercitazione sull&#39;estensibilità dell&#39;interfaccia utente di AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview). Anche se si concentra sull’estensione della console Frammenti di contenuto, i concetti per l’implementazione di un’estensione dell’interfaccia utente nell’Editor universale sono gli stessi.

[Utilizzando Extension Manager in AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/), puoi abilitare o disabilitare le estensioni per singole istanze, accedere alle estensioni di prime parti di Adobe, incluse quelle per Universal Editor, e molto altro.

## Punti di estensione {#extension-points}

Oltre all’estensibilità dell’interfaccia utente, Universal Editor offre molti altri punti di estensione flessibili per consentire l’integrazione perfetta di requisiti aziendali personalizzati.

* **[Blocchi](/help/edge/developer/block-collection.md)**: in formato JSON semplice, i progetti possono regolare i blocchi e utilizzare le funzioni disponibili per la creazione di contenuti.
* **[Interfaccia utente personalizzata](#extending-ui)**: le estensioni possono visualizzare l&#39;interfaccia utente necessaria nei pannelli laterali o nelle finestre di dialogo modali.
* **[Eventi](/help/implementing/universal-editor/events.md)**: le estensioni ricevono eventi sulle azioni dell&#39;autore e sulle selezioni effettuate nella pagina per rispondere in modo appropriato.
