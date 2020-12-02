---
title: Abilitazione dell'esportazione JSON per un componente
description: I componenti possono essere adattati per generare l’esportazione JSON dei loro contenuti in base a un framework di modellazione.
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 7%

---


# Abilitazione dell&#39;esportazione JSON per un componente {#enabling-json-export-for-a-component}

I componenti possono essere adattati per generare l’esportazione JSON dei loro contenuti in base a un framework di modellazione.

## Panoramica {#overview}

L&#39;esportazione JSON si basa su [Sling Models](https://sling.apache.org/documentation/bundles/models.html) e sul framework [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (che si basa su [Jackson annotations](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Questo significa che il componente deve avere un modello Sling se deve esportare JSON. Pertanto, per abilitare l’esportazione JSON su qualsiasi componente dovrete seguire questi due passaggi.

* [Definire un modello Sling per il componente](#define-a-sling-model-for-the-component)
* [Annotazione dell&#39;interfaccia Sling Model](#annotate-the-sling-model-interface)

## Definire un modello Sling per il componente {#define-a-sling-model-for-the-component}

Per il componente deve essere definito innanzitutto un modello Sling.

>[!NOTE]
>
>Per un esempio di utilizzo di Sling Models, vedere l&#39;articolo [Developing Sling Model Exporter in AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

La classe di implementazione del modello Sling deve essere annotata con le seguenti annotazioni:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Questo garantisce che il componente possa essere esportato autonomamente, utilizzando il selettore `.model` e l&#39;estensione `.json`.

Inoltre, questo specifica che la classe Sling Model può essere adattata all&#39;interfaccia `ComponentExporter`.

>[!NOTE]
>
>Le annotazioni Jackson non vengono in genere specificate a livello di classe Sling Model, ma a livello di interfaccia Model. In questo modo, assicuratevi che l’esportazione JSON sia considerata parte dell’API del componente.

>[!NOTE]
>
>Le classi `ExporterConstants` e `ComponentExporter` provengono dal pacchetto `com.adobe.cq.export.json`.

### Utilizzo di più selettori {#multiple-selectors}

Sebbene non sia un caso d&#39;uso standard, è possibile configurare più selettori oltre al selettore `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

In tal caso, tuttavia, il selettore `model` deve essere il primo selettore e l&#39;estensione deve essere `.json`.

## Annota dell&#39;interfaccia del modello Sling {#annotate-the-sling-model-interface}

Per essere presa in considerazione dal framework JSON Exporter, l&#39;interfaccia Model deve implementare l&#39;interfaccia `ComponentExporter` (o `ContainerExporter`, nel caso di un componente contenitore).

L&#39;interfaccia del modello Sling corrispondente (`MyComponent`) verrà quindi annotata utilizzando le annotazioni di [Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) per definire come esportare (serializzato).

L&#39;interfaccia Model deve essere annotata correttamente per definire i metodi da serializzare. Per impostazione predefinita, tutti i metodi che rispettano le consuete convenzioni di denominazione per i getter saranno serializzati e deriveranno naturalmente i nomi delle loro proprietà JSON dai nomi dei getter. Questo può essere impedito o sostituito utilizzando `@JsonIgnore` o `@JsonProperty` per rinominare la proprietà JSON.

## Esempio {#example}

[Core ](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) Componentsupporta l’esportazione JSON e può essere utilizzato come riferimento.

Per un esempio, consultate Implementazione del modello Sling del componente Image Core e la relativa interfaccia annotata.

## Documentazione correlata {#related-documentation}

Per maggiori dettagli, consulta:

* [Frammenti di contenuto nella guida utente di Assets](/help/assets/content-fragments/content-fragments.md)
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componenti ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) di base e componente Frammento di  [contenuto](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)
