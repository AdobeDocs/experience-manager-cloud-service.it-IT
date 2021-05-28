---
title: Esportatore JSON per Content Services
description: AEM Content Services è progettato per generalizzare la descrizione e la distribuzione dei contenuti in/da AEM oltre l’attenzione sulle pagine web. Forniscono contenuti a canali che non sono pagine web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente.
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 5%

---

# Esportatore JSON per Content Services {#json-exporter-for-content-services}

AEM Content Services è progettato per generalizzare la descrizione e la distribuzione dei contenuti in/da AEM oltre lo scopo delle pagine web.

Forniscono contenuti a canali che non sono pagine web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* Applicazioni a pagina singola
* Applicazioni mobile native
* Altri canali e punti di contatto esterni a AEM

Con i frammenti di contenuto che utilizzano contenuti strutturati, puoi fornire servizi di contenuto utilizzando l’esportatore JSON per distribuire il contenuto di una pagina (y) AEM in formato modello dati JSON. Questo può quindi essere utilizzato dalle tue applicazioni.

## Esportazione JSON con componenti core per frammenti di contenuto {#json-exporter-with-content-fragment-core-components}

Utilizzando la funzione di esportazione JSON AEM puoi fornire il contenuto di una pagina (y) AEM nel formato del modello di dati JSON. Questo può quindi essere utilizzato dalle tue applicazioni.

All’interno di AEM la consegna viene ottenuta utilizzando il selettore `model` e l’estensione `.json`.

`.model.json`

1. Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. Fornirà contenuti quali:

   ![Modello JSON per contenuti WKND](assets/json-model-wknd.png)

In alternativa, puoi distribuire il contenuto di un frammento di contenuto strutturato specificandone il targeting.

Questa operazione viene eseguita utilizzando l’intero percorso del frammento (tramite `jcr:content`); ad esempio con un suffisso come .

`.../jcr:content/root/container/container/contentfragment.model.json`

La pagina può contenere un singolo frammento di contenuto o più componenti di vari tipi. È inoltre possibile utilizzare meccanismi quali i componenti elenco per cercare automaticamente i contenuti rilevanti.

* Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* Fornirà contenuti quali:

   ![Modello JSON del frammento di contenuto WKND](assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >Puoi [adattare i tuoi componenti](enabling-json-exporter.md) per accedere e utilizzare questi dati.

   >[!NOTE]
   >
   >Sebbene non sia un&#39;implementazione standard, [sono supportati più selettori,](enabling-json-exporter.md#multiple-selectors) ma `model` deve essere il primo.

### Ulteriori informazioni {#further-information}

Consulta anche:

* API HTTP di Assets
   * [API HTTP di Assets](/help/assets/developer-reference-material-apis.md)
* Modelli Sling:
   * [Sling Models - Associazione di una classe di modello a un tipo di risorsa a partire dal 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM con JSON:
   * [Abilitazione dell’esportazione JSON per un componente](enabling-json-exporter.md)

## Documentazione correlata {#related-documentation}

Per maggiori dettagli vedi:

* [Frammenti di contenuto nella guida utente Assets](/help/assets/content-fragments/content-fragments.md)
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componenti core ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e componente Frammento di  [contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)
