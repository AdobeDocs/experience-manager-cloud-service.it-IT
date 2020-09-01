---
title: Esportatore JSON per Content Services
description: AEM Content Services è progettato per rendere più generalizzata la descrizione e la distribuzione dei contenuti in/da AEM oltre l'attenzione sulle pagine Web. Forniscono contenuti a canali che non sono pagine Web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente.
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 7%

---


# Esportatore JSON per Content Services {#json-exporter-for-content-services}

AEM Content Services è progettato per rendere più generalizzata la descrizione e la distribuzione dei contenuti in/da AEM oltre il centro delle pagine Web.

Forniscono contenuti a canali che non sono pagine Web AEM tradizionali, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* Applicazioni a pagina singola
* Applicazioni mobili native
* Altri canali e punti di contatto esterni a AEM

Con frammenti di contenuto che utilizzano contenuto strutturato, puoi fornire servizi di contenuto utilizzando JSON Export per distribuire il contenuto di una pagina AEM (y) nel formato modello dati JSON. Questo può essere utilizzato dalle vostre applicazioni.

## Esportatore JSON con componenti di base frammento di contenuto {#json-exporter-with-content-fragment-core-components}

Utilizzando il modulo di esportazione JSON AEM potete distribuire il contenuto di una pagina AEM (y) nel formato del modello di dati JSON. Questo può essere utilizzato dalle vostre applicazioni.

All&#39;interno AEM la consegna viene ottenuta utilizzando il selettore `model` e l&#39; `.json` estensione.

`.model.json`

1. Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. Fornirà contenuti quali:

   ![Modello JSON del contenuto WKND](assets/json-model-wknd.png)

In alternativa, è possibile distribuire i contenuti di un frammento di contenuto strutturato specificandone il targeting.

Questo avviene utilizzando l&#39;intero percorso del frammento (tramite il `jcr:content`); ad esempio con un suffisso come

`.../jcr:content/root/container/container/contentfragment.model.json`

La pagina può contenere un singolo frammento di contenuto o più componenti di vari tipi. È inoltre possibile utilizzare meccanismi come i componenti elenco per cercare automaticamente i contenuti rilevanti.

* Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* Fornirà contenuti quali:

   ![Modello JSON di frammento di contenuto WKND](assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >È possibile [adattare i propri componenti](enabling-json-exporter.md) per accedere e utilizzare questi dati.

   >[!NOTE]
   >
   >Sebbene non sia un&#39;implementazione standard, [più selettori sono supportati,](enabling-json-exporter.md#multiple-selectors) ma `model` devono essere i primi.

### Ulteriori informazioni {#further-information}

Consulta anche:

* API HTTP di Assets
   * [API HTTP di Assets](/help/assets/developer-reference-material-apis.md)
* Modelli Sling:
   * [Sling Models - Associazione di una classe di modelli a un tipo di risorsa dal 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM con JSON:
   * [Abilitazione dell&#39;esportazione JSON per un componente](enabling-json-exporter.md)

## Related Documentation {#related-documentation}

Per maggiori dettagli, consulta:

* [Frammenti di contenuto nella guida utente di Assets](/help/assets/content-fragments/content-fragments.md)
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componenti](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) di base e componente Frammento di [contenuto](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)
