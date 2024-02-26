---
title: Esportatore JSON per Content Services
description: I Content Services dell’AEM sono progettati per generalizzare la descrizione e la distribuzione dei contenuti all’interno e dall’AEM, non limitandosi alle pagine web. Forniscono contenuti a canali che non sono pagine web AEM tradizionali, utilizzando metodi standardizzati che possono essere utilizzati da qualsiasi cliente.
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
source-git-commit: 89f23a590338561b4cfeb10b54a260a135ec2f08
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 17%

---

# Esportatore JSON per Content Services {#json-exporter-for-content-services}

I Content Services dell’AEM sono progettati per generalizzare la descrizione e la distribuzione dei contenuti all’interno e dall’AEM al di là del focus delle pagine web.

Fornisce contenuti a canali diversi dalle tradizionali pagine web di AEM, utilizzando metodi standardizzati utilizzabili da qualsiasi cliente. Questi canali possono includere:

* Applicazioni a pagina singola
* Applicazioni mobile native
* Altri canali e punti di contatto esterni all’AEM

Con i frammenti di contenuto che utilizzano contenuti strutturati, puoi fornire servizi di contenuto utilizzando la funzione di esportazione JSON per distribuire i contenuti di una o y pagine AEM in formato di modello dati JSON. che possono essere utilizzati dalle applicazioni.

## Esportatore JSON con componenti core per frammenti di contenuto {#json-exporter-with-content-fragment-core-components}

Utilizzando la funzione di esportazione JSON per AEM puoi distribuire i contenuti di una pagina AEM (y) in formato di modello dati JSON. che possono essere utilizzati dalle applicazioni.

All’interno dell’AEM la consegna viene effettuata utilizzando il selettore `model` e `.json` estensione.

`.model.json`

1. Ad esempio, un URL come:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. Consegna contenuti quali:

   ![Modello JSON del contenuto WKND](assets/json-model-wknd.png)

In alternativa, puoi distribuire il contenuto di un frammento di contenuto strutturato eseguendo il targeting specifico.

Questa operazione viene eseguita utilizzando l’intero percorso del frammento (tramite `jcr:content`); ad esempio, con un suffisso come.

`.../jcr:content/root/container/container/contentfragment.model.json`

La pagina può contenere un singolo frammento di contenuto o più componenti di vari tipi. Puoi inoltre utilizzare meccanismi quali i componenti elenco per cercare automaticamente contenuti rilevanti.

* Ad esempio, un URL come:

  ```shell
  http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
  ```

* Consegna contenuti quali:

  ![Modello JSON del frammento di contenuto WKND](assets/json-model-wknd-content-fragment.png)

  >[!NOTE]
  >
  >È possibile [adattare i propri componenti](enabling-json-exporter.md) per accedere e utilizzare questi dati.

  >[!NOTE]
  >
  >Anche se non è un&#39;implementazione standard, [sono supportati più selettori,](enabling-json-exporter.md#multiple-selectors) ma `model` deve essere il primo.

### Ulteriori informazioni {#further-information}

* API HTTP di Assets
   * [API HTTP di Assets](/help/assets/developer-reference-material-apis.md)
* Modelli Sling:
   * [Modelli Sling: associazione di una classe di modelli a un tipo di risorsa dalla versione 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM con JSON:
   * [Abilitazione dell’esportazione JSON per un componente](enabling-json-exporter.md)

## Documentazione correlata {#related-documentation}

* [Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md)
* [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [Authoring con frammenti di contenuto](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [Componente Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it)
