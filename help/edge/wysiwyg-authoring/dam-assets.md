---
title: Pubblicazione di pagine con DAM Assets tramite Edge Delivery Services
description: Scopri le impostazioni necessarie per garantire che le risorse DAM per le pagine vengano pubblicate facilmente nei Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 2%

---

# Pubblicazione di pagine con DAM Assets tramite Edge Delivery Services {#dam-assets}

Scopri le impostazioni necessarie per garantire che le risorse DAM per le pagine vengano pubblicate facilmente nei Edge Delivery Services.

## Universal Editor, DAM Assets e Edge Delivery {#overview}

Durante la modifica del contenuto per l’Editor universale, è ovviamente possibile selezionare le risorse da DAM. Quando pubblichi il contenuto in Edge Delivery Services, viene pubblicato anche il contenuto DAM correlato.

Per garantire questo comportamento senza soluzione di continuità, l’AEM e i Edge Delivery Services devono avere accesso adeguato al DAM per poter pubblicare. Ciò include:

* [Verifica dell&#39;accessibilità delle cartelle di risorse](#accessible).
* [Verifica che alla cartella delle risorse sia assegnata la configurazione corretta (come richiesto)](#configuration).

## Garanzia di accessibilità delle cartelle di Assets {#accessible}

Quando si pubblicano pagine da AEM a Edge Delivery Services, viene utilizzato [un account tecnico](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md). Questo account, con un nome nel formato `<hash>@techacct.adobe.com`, viene creato automaticamente come utente in AEM da Cloud Manager ogni volta che si pubblica una pagina creata con Universal Editor.

![Account tecnico](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

Questo account tecnico deve disporre dei diritti di accesso a tutte le cartelle DAM per poter pubblicare i propri contenuti. Puoi effettuare le seguenti operazioni:

* Non utilizzare cartelle DAM private.
* Concedi all’account tecnico l’accesso utente alle cartelle DAM.

## Assicurarsi che alla cartella Assets sia assegnata una configurazione corretta {#configuration}

In genere, assicurarti che il tuo account tecnico abbia accesso alle risorse in DAM è sufficiente per pubblicare le risorse insieme alle pagine nei Edge Delivery Services.

È necessaria una configurazione aggiuntiva in due casi aggiuntivi, tuttavia:

* Se desideri pubblicare in Edge Delivery Services pagine con risorse non immagine, ad esempio PDF o video.
* Se desideri pubblicare le risorse immagine in Edge Delivery Services indipendentemente dalle pagine.

Per supportare entrambi questi casi d&#39;uso, è necessario assegnare una [configurazione](/help/implementing/developing/introduction/configurations.md) alla cartella DAM.

1. Accedi all’ambiente di authoring AEM.
1. In **Sites** seleziona il sito a cui stai pubblicando le risorse o il sito a cui le risorse saranno associate.
1. Tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Nella scheda **Avanzate** della finestra delle proprietà, prendi nota della configurazione nel campo **Configurazione cloud**.
   * Viene creato automaticamente quando si crea il sito nel formato `/conf/<site-name>`.
1. Tocca o fai clic su **Annulla** nella finestra delle proprietà, passa a **Assets** -> **File** e seleziona la cartella DAM.
1. Tocca o fai clic su **Proprietà** nella barra degli strumenti.
1. Nella scheda **Cloud Service** della finestra delle proprietà, seleziona nel campo **Configurazione cloud** la stessa configurazione indicata in precedenza.
1. Tocca o fai clic su **Salva e chiudi**.
