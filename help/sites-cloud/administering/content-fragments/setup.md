---
title: Frammenti di contenuto - Configurazione
description: Scopri come abilitare la funzionalità Frammento di contenuto e GraphQL per utilizzare le funzioni di consegna headless AEM.
feature: Content Fragments
role: Developer, Architect
source-git-commit: 676173813b6ea4defeafe25c95be9668d32aac38
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 37%

---


# Frammenti di contenuto - Configurazione {#content-fragments-setup}

I frammenti di contenuto as a Cloud Service all’interno di Adobe Experience Manager (AEM) consentono di preparare contenuti pronti per l’uso in più posizioni e su più canali. È ideale per la distribuzione headless e l’authoring delle pagine.

Per abilitare la tua istanza per la funzionalità Frammento di contenuto è necessario abilitare:

* **Modelli per frammenti di contenuto**: obbligatorio

  >[!CAUTION]
  >
  >Se non si abilita **Modelli per frammenti di contenuto**:
  >
  >* il **Crea** non sarà disponibile per la creazione di modelli.
  >* non potrai [selezionare la configurazione Sites per creare il relativo endpoint](/help/headless/graphql-api/graphql-endpoint.md).

* **Query GraphQL persistenti**: facoltativo

Configurazione dell’istanza completata:

* da [abilitazione della funzionalità nel browser configurazioni](#enable-content-fragment-functionality-configuration-browser)
* allora [applicazione della configurazione alle singole cartelle di Assets](#apply-the-configuration-to-your-folder)

## Abilitare la funzionalità Frammenti di contenuto nel browser configurazioni {#enable-content-fragment-functionality-configuration-browser}

Per utilizzare la funzionalità Frammento di contenuto, dei modelli di Frammento di contenuto e delle query persistenti di GraphQL, puoi **deve** per prima cosa abilitarli tramite **Browser configurazioni**:

>[!NOTE]
>
>Per ulteriori dettagli, consulta [Browser configurazioni](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>Le [Configurazioni secondarie](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (configurazioni nidificate all’interno di un’altra configurazione) sono supportate totalmente per l’utilizzo con Frammenti di contenuto, Modelli di frammenti di contenuto e query GraphQL.
>
>Fai attenzione che:
>
>* dopo la creazione di modelli in una configurazione secondaria, NON è possibile spostare o copiare il modello in un’altra configurazione secondaria.
>
>* Un endpoint GraphQL sarà (ancora) basato su una configurazione principale (root).
>
>* Le query persistenti verranno (ancora) salvate in base alla configurazione principale (root).

1. Accedi a **Strumenti**, **Generali**, quindi apri **Browser configurazioni**.

1. Utilizza **Crea** per aprire la finestra di dialogo, in cui:

   1. Specificare un **Titolo**.
   1. Al momento della creazione, il **Nome** diventa il nome del nodo nell’archivio.
È possibile immettere un nome. Se lasci vuoto il campo, questo viene generato automaticamente in base al titolo, quindi regolato in base a [Convenzioni di denominazione AEM](/help/implementing/developing/introduction/naming-conventions.md); se necessario, è possibile regolare il risultato.
   1. Per attivarne l’uso, seleziona
      * **Modelli per frammenti di contenuto**
      * **Query persistenti GraphQL**

      ![Definire la configurazione](assets/cf-setup-create-conf.png)

1. Seleziona **Crea** per salvare la definizione.

## Applicare la configurazione alla cartella {#apply-the-configuration-to-your-folder}

Quando la configurazione **globale** è abilitato per la funzionalità Frammento di contenuto, quindi si applica a qualsiasi cartella Risorse accessibile tramite **Risorse** console.

Per utilizzare altre configurazioni (escludendo quindi globali) con una cartella Risorse simile, è necessario definire la connessione. A tale scopo, seleziona il **Configurazione** nel **Cloud Service** scheda di **Proprietà cartella** della cartella appropriata.

![Applica configurazione](assets/cf-setup-apply-conf.png)
