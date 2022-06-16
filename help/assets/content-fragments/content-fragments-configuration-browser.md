---
title: Frammenti di contenuto - Browser di configurazione
description: Scopri come abilitare alcune funzionalità dei frammenti di contenuto nel browser di configurazione per sfruttare AEM potenti funzionalità di distribuzione headless.
feature: Content Fragments
role: User
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: 78448aafa1b397f9131c12ab2afd74b05ae53e66
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 18%

---

# Frammenti di contenuto - Browser di configurazione{#content-fragments-configuration-browser}

Scopri come abilitare alcune funzionalità dei frammenti di contenuto nel browser di configurazione per sfruttare AEM potenti funzionalità di distribuzione headless.

## Abilita funzionalità frammento di contenuto per la tua istanza {#enable-content-fragment-functionality-instance}

Prima di utilizzare i frammenti di contenuto, è necessario utilizzare la funzione **Browser di configurazione** per abilitare:

* **Modelli per frammenti di contenuto** - obbligatorio
* **Query persistenti GraphQL** - opzionale

>[!CAUTION]
>
>Se non si abilita **Modelli per frammenti di contenuto**:
>
>* la **Crea** non sarà disponibile per la creazione di nuovi modelli.
>* non sarà in grado di [seleziona la configurazione Sites per creare il relativo punto finale](/help/headless/graphql-api/graphql-endpoint.md).


Per abilitare la funzionalità dei frammenti di contenuto è necessario:

* Abilita l’utilizzo della funzionalità dei frammenti di contenuto tramite il browser di configurazione
* Applica la configurazione alla cartella Assets

### Abilitare la funzionalità dei frammenti di contenuto nel browser di configurazione {#enable-content-fragment-functionality-in-configuration-browser}

A [utilizzare alcune funzionalità dei frammenti di contenuto](#creating-a-content-fragment-model) voi **deve** per prima cosa attivarli tramite **Browser di configurazione**:

>[!NOTE]
>
>Per maggiori dettagli vedi anche [Browser di configurazione:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Sottoconfigurazioni](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (una configurazione nidificata all’interno di un’altra configurazione) è completamente supportata per l’utilizzo con Frammenti di contenuto, Modelli di frammenti di contenuto e query GraphQL.
>
>Solo per notare che:
>
>
>* Dopo aver creato i modelli in una configurazione secondaria, NON è possibile spostare o copiare il modello in un&#39;altra configurazione secondaria.
>
>* Un endpoint GraphQL sarà (ancora) basato su una configurazione padre (root).
>
>* Le query persistenti verranno (comunque) salvate in base alla configurazione padre (root).



1. Accedi a **Strumenti**, **Generali**, quindi apri **Browser configurazioni**.

1. Utilizzo **Crea** per aprire la finestra di dialogo, in cui:

   1. Specifica una **Titolo**.
   1. Per attivarne l&#39;uso, seleziona
      * **Modelli per frammenti di contenuto**
      * **Query GraphQL persistenti**

      ![Definire la configurazione](assets/cfm-conf-01.png)


1. Seleziona **Crea** per salvare la definizione.

<!-- 1. Select the location appropriate to your website. -->

### Applica la configurazione alla cartella delle risorse {#apply-the-configuration-to-your-assets-folder}

Quando la configurazione **globale** è abilitato per la funzionalità frammento di contenuto, quindi si applica a qualsiasi cartella Assets.

Per utilizzare altre configurazioni con una cartella Risorse simile, ovvero escludendo il formato globale, è necessario definire la connessione. Questa operazione viene eseguita selezionando l’appropriata **Configurazione** nella scheda **Cloud Services** della finestra **Proprietà cartella** della cartella specifica.

![Applica configurazione](assets/cfm-conf-02.png)
