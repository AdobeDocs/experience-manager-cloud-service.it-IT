---
title: Frammenti di contenuto - Browser configurazioni (Risorse - Frammenti di contenuto)
description: Scopri come abilitare la funzionalità Frammenti di contenuto nel Browser configurazioni.
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: 34574fdc7f246499bd238fef388671d2287e62bc
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 84%

---

# Frammenti di contenuto - Browser configurazioni{#content-fragments-configuration-browser}

Scopri come abilitare alcune funzionalità relative ai frammenti di contenuto nel browser configurazioni per sfruttare le potenti funzionalità di distribuzione headless dell’AEM.

## Abilita funzionalità frammento di contenuto per la tua istanza {#enable-content-fragment-functionality-instance}

Prima di utilizzare i frammenti di contenuto, è necessario utilizzare la funzione **Browser di configurazione** per abilitare:

* **Modelli per frammenti di contenuto**: obbligatorio
* **Query GraphQL persistenti**: facoltativo

>[!CAUTION]
>
>Se non si abilita **Modelli per frammenti di contenuto**:
>
>* l’opzione **Crea** non sarà disponibile per la creazione di nuovi modelli.
>* non potrai [selezionare la configurazione Sites per creare il relativo endpoint](/help/headless/graphql-api/graphql-endpoint.md).


Per abilitare la funzionalità dei frammenti di contenuto è necessario:

* Abilitare l’utilizzo della funzionalità dei frammenti di contenuto tramite il browser configurazioni
* Applicare la configurazione alla cartella Risorse

### Abilitare la funzionalità dei frammenti di contenuto nel browser configurazioni {#enable-content-fragment-functionality-in-configuration-browser}

Per [utilizzare alcune funzionalità dei frammenti di contenuto](#creating-a-content-fragment-model) **devi** per prima cosa attivarle tramite il **browser configurazioni**:

>[!NOTE]
>
>Per maggiori dettagli vedi anche [Browser configurazioni:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>Le [Configurazioni secondarie](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (configurazioni nidificate all’interno di un’altra configurazione) sono completamente supportate per l’utilizzo con Frammenti di contenuto, Modelli di frammenti di contenuto e query GraphQL.
>
>Fai attenzione che:
>
>
>* Dopo aver creato i modelli in una configurazione secondaria, NON è possibile spostare o copiare il modello in un’altra configurazione secondaria.
>
>* Un endpoint GraphQL sarà (ancora) basato su una configurazione principale (root).
>
>* Le query persistenti verranno (ancora) salvate in base alla configurazione principale (root).



1. Accedi a **Strumenti**, **Generali**, quindi apri **Browser configurazioni**.

1. Utilizza **Crea** per aprire la finestra di dialogo, in cui:

   1. Specificare un **Titolo**.
   1. Il **nome** diventerà il nome del nodo nell’archivio.
      * Viene generato automaticamente dal titolo, secondo le [convenzioni di denominazione di AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Se necessario è possibile regolarlo.
   1. Per attivarne l’uso, seleziona
      * **Modelli per frammenti di contenuto**
      * **Query persistenti GraphQL**

      ![Definire la configurazione](assets/cfm-conf-01.png)


1. Seleziona **Crea** per salvare la definizione.

<!-- 1. Select the location appropriate to your website. -->

### Applica la configurazione alla cartella Risorse {#apply-the-configuration-to-your-assets-folder}

Quando la configurazione **globale** è abilitato per la funzionalità frammento di contenuto, quindi si applica a qualsiasi cartella Risorse.

Per utilizzare altre configurazioni con una cartella Risorse simile, ovvero escludendo il formato globale, è necessario definire la connessione. Questa operazione viene eseguita selezionando l’appropriata **Configurazione** nella scheda **Servizi cloud** della finestra **Proprietà cartella** della cartella specifica.

![Applica configurazione](assets/cfm-conf-02.png)
