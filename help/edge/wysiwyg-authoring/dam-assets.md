---
title: Pubblicazione di pagine con risorse DAM tramite Edge Delivery Services
description: Scopri quali sono le impostazioni necessarie per garantire che le risorse DAM per le pagine siano pubblicate facilmente in Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '433'
ht-degree: 100%

---

# Pubblicazione di pagine con risorse DAM tramite Edge Delivery Services {#dam-assets}

Scopri quali sono le impostazioni necessarie per garantire che le risorse DAM per le pagine siano pubblicate facilmente in Edge Delivery Services.

## Editor universale, risorse DAM ed Edge Delivery {#overview}

Durante la modifica del contenuto per l’editor universale, è ovviamente possibile selezionare le risorse da DAM. Quando pubblichi il contenuto in Edge Delivery Services, viene pubblicato anche il contenuto DAM correlato.

Per garantire questo comportamento perfetto, AEM ed Edge Delivery Services devono avere accesso corretto a DAM per poter pubblicare. Ciò include:

* [Garantire l’accessibilità alle cartelle di risorse](#accessible).
* [Assicurarsi che alla cartella delle risorse sia assegnata la configurazione corretta (come richiesto)](#configuration).

## Garantire l’accessibilità alle cartelle di risorse {#accessible}

Durante la pubblicazione di pagine da AEM ad Edge Delivery Services, viene utilizzato [un account tecnico](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md). Questo account, con un nome in formato `<hash>@techacct.adobe.com`, viene creato automaticamente come utente in AEM da Cloud Manager ogni volta che viene pubblicata una pagina creata con l’editor universale.

![Account tecnico](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

Per poter pubblicare i propri contenuti, questo account tecnico deve disporre dei diritti di accesso a tutte le cartelle DAM. Puoi:

* non utilizzare cartelle DAM private;
* concedere all’account tecnico l’accesso utente alle cartelle DAM.

## Assicurarsi che alla cartella delle risorse sia assegnata una configurazione corretta {#configuration}

In genere, garantire che l’account tecnico abbia accesso alle risorse in DAM è sufficiente per pubblicare le risorse insieme alle pagine in Edge Delivery Services.

Tuttavia, è necessaria una configurazione aggiuntiva in due casi:

* Se desideri pubblicare in Edge Delivery Services pagine con risorse non di immagine, ad esempio PDF o video.
* Se desideri pubblicare le risorse immagine in Edge Delivery Services indipendentemente dalle pagine.

Per supportare entrambi questi casi d’uso, è necessario assegnare una [configurazione](/help/implementing/developing/introduction/configurations.md) alla cartella DAM.

1. Accedi all’ambiente di authoring di AEM.
1. In **Sites** seleziona il sito su cui stai pubblicando le risorse o il sito a cui saranno associate le risorse.
1. Nella barra degli strumenti, tocca o fai clic su **Proprietà**.
1. Nella scheda **Avanzate** della finestra delle proprietà, prendi nota della configurazione nel campo **Configurazione cloud**.
   * Quando crei il sito, questa viene creata automaticamente nel formato `/conf/<site-name>`.
1. Tocca o fai clic su **Annulla** nella finestra delle proprietà, passa a **Risorse** -> **File** e seleziona la cartella DAM.
1. Nella barra degli strumenti, tocca o fai clic su **Proprietà**.
1. Nella scheda **Servizi cloud** della finestra delle proprietà, nel campo **Configurazione cloud** seleziona la stessa configurazione annotata in precedenza.
1. Tocca o fai clic su **Salva e chiudi**.
