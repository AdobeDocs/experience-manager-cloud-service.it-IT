---
title: Frammenti di contenuto - Configurazione
description: Scopri come abilitare la funzionalità Frammento di contenuto e GraphQL per l’utilizzo con le funzioni di consegna headless di AEM e l’authoring delle pagine.
feature: Content Fragments
role: Developer
exl-id: 3974d698-1e7d-4a5f-a6d5-cbf8d96b4095
solution: Experience Manager Sites
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 37%

---

# Frammenti di contenuto - Configurazione {#content-fragments-setup}

I frammenti di contenuto in Adobe Experience Manager (AEM) as a Cloud Service consentono di preparare contenuti pronti per l’uso in più posizioni e su più canali. È ideale per la distribuzione headless e l’authoring delle pagine.

Per abilitare la tua istanza per la funzionalità Frammento di contenuto è necessario abilitare:

* **Modelli per frammenti di contenuto**: obbligatorio

  >[!CAUTION]
  >
  >Se non si abilita **Modelli per frammenti di contenuto**:
  >
  >* l&#39;opzione **Crea** non sarà disponibile per la creazione di modelli.
  >* non potrai [selezionare la configurazione Sites per creare il relativo endpoint](/help/headless/graphql-api/graphql-endpoint.md).

* **Query GraphQL persistenti**: facoltativo

Configurazione dell’istanza completata:

* da [abilitazione della funzionalità nel browser configurazioni](#enable-content-fragment-functionality-configuration-browser)
* quindi [applicare la configurazione alle singole cartelle di Assets](#apply-the-configuration-to-your-folder)

## Abilitare la funzionalità Frammenti di contenuto nel browser configurazioni {#enable-content-fragment-functionality-configuration-browser}

Per utilizzare la funzionalità Frammento di contenuto dei modelli di Frammento di contenuto e delle query persistenti di GraphQL, **devi** prima abilitarli tramite il **Browser configurazioni**:

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Browser configurazioni](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

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
   1. Al momento della creazione, **Name** diventa il nome del nodo nell&#39;archivio.
È possibile immettere un nome. Se lasci vuoto il campo, viene generato automaticamente in base al titolo e poi regolato in base alle [convenzioni di denominazione di AEM](/help/implementing/developing/introduction/naming-conventions.md). Se necessario, puoi modificare il risultato.
   1. Per abilitarne l’uso, seleziona
      * **Modelli per frammenti di contenuto**
      * **Query persistenti GraphQL**

      ![Definire la configurazione](assets/cf-setup-create-conf.png)

1. Seleziona **Crea** per salvare la definizione.

## Applicare la configurazione alla cartella {#apply-the-configuration-to-your-folder}

Quando la configurazione **global** è abilitata per la funzionalità Frammento di contenuto, viene applicata a qualsiasi cartella Assets accessibile tramite la console **Assets**.

Per utilizzare altre configurazioni con una cartella Assets simile, escludendo quindi quelle globali, è necessario definire la connessione. A tale scopo, selezionare la **Configurazione** appropriata nella scheda **Servizi cloud** delle **Proprietà cartella** della cartella appropriata.

![Applica configurazione](assets/cf-setup-apply-conf.png)
