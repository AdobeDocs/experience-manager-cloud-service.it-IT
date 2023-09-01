---
title: Frammenti di contenuto - Browser configurazioni
description: Scopri come abilitare le funzionalità Frammento di contenuto e GraphQL nel Browser di configurazione per sfruttare le funzionalità di distribuzione headless di AEM.
feature: Content Fragments
role: User
hide: true
index: false
hidefromtoc: true
exl-id: 55d442ae-ae06-4dfa-8e4e-b415385ccea5
source-git-commit: 5ce5746026c5683e79cdc1c9dc96804756321cdb
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 100%

---

# Frammenti di contenuto - Browser configurazioni{#content-fragments-configuration-browser}

<!--
hide: yes
index: no
hidefromtoc: yes
-->

Scopri come abilitare funzionalità specifiche per i frammenti di contenuto nel browser configurazioni.

## Abilita funzionalità frammento di contenuto per la tua istanza {#enable-content-fragment-functionality-instance}

Prima di utilizzare i frammenti di contenuto, utilizza la funzione **Browser di configurazione** per abilitare:

* **Modelli per frammenti di contenuto**: obbligatorio
* **Query GraphQL persistenti**: facoltativo

>[!CAUTION]
>
>Se non si abilita **Modelli per frammenti di contenuto**:
>
>* l’opzione **Crea** non è disponibile per la creazione di modelli.
>* non puoi [selezionare la configurazione Sites per creare il punto finale correlato](/help/headless/graphql-api/graphql-endpoint.md).

Per abilitare la funzionalità dei frammenti di contenuto, è necessario effettuare le seguenti operazioni:

* Abilitare l’utilizzo della funzionalità dei frammenti di contenuto tramite il browser configurazioni
* Applicare la configurazione alla cartella Risorse

### Abilitare la funzionalità dei frammenti di contenuto nel browser configurazioni {#enable-content-fragment-functionality-in-configuration-browser}

Per utilizzare alcune [funzionalità dei frammenti di contenuto](#creating-a-content-fragment-model), per prima cosa **devi** attivarle tramite il **Browser di configurazione**:

>[!NOTE]
>
>Per ulteriori dettagli, consulta [Browser di configurazione](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>Le [Configurazioni secondarie](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (configurazioni nidificate all’interno di un’altra configurazione) sono supportate totalmente per l’utilizzo con Frammenti di contenuto, Modelli di frammenti di contenuto e query GraphQL.
>
>Fai attenzione che:
>
>
>* dopo la creazione di modelli in una configurazione secondaria, NON è possibile spostare o copiare il modello in un’altra configurazione secondaria.
>
>* L’endpoint GraphQL si baserà (ancora) su una configurazione principale (primaria).
>
>* Le query persistenti verranno salvate (ancora) in base alla configurazione principale (primaria).


1. Accedi a **Strumenti**, **Generali**, quindi apri **Browser configurazioni**.

1. Utilizza **Crea** per aprire la finestra di dialogo, in cui:

   1. Specificare un **Titolo**.
   1. Il **nome** diventa il nome del nodo nell’archivio.
      * Viene generato automaticamente dal titolo, secondo le [convenzioni di denominazione AEM](/help/implementing/developing/introduction/naming-conventions.md).
      * Se necessario è possibile regolarlo.
   1. Per attivarne l’uso, seleziona
      * **Modelli per frammenti di contenuto**
      * **Query persistenti GraphQL**

      ![Definire la configurazione](assets/cfm-conf-01.png)

1. Seleziona **Crea** per salvare la definizione.

<!-- 1. Select the location appropriate to your website. -->

### Applicare la configurazione alla cartella {#apply-the-configuration-to-your-folder}

Quando la configurazione di formato **globale** è abilitata per la funzionalità frammento di contenuto, questa si applica a qualsiasi cartella Risorse accessibile tramite la console **Risorse**.

Per utilizzare altre configurazioni con una cartella Risorse simile, ovvero escludendo il formato globale, è necessario definire la connessione. Questa operazione viene eseguita selezionando l’appropriata **Configurazione** nella scheda **Servizi cloud** della finestra **Proprietà cartella** della cartella specifica.

![Applica configurazione](assets/cfm-conf-02.png)
