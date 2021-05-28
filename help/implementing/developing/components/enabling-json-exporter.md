---
title: Abilitazione dell’esportazione JSON per un componente
description: I componenti possono essere adattati per generare l’esportazione JSON dei loro contenuti in base a un framework di modeling.
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 4%

---

# Abilitazione dell’esportazione JSON per un componente {#enabling-json-export-for-a-component}

I componenti possono essere adattati per generare l’esportazione JSON dei loro contenuti in base a un framework di modeling.

## Panoramica {#overview}

L&#39;esportazione JSON si basa su [modelli Sling](https://sling.apache.org/documentation/bundles/models.html) e sul framework [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (che si basa su [annotazioni Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Questo significa che il componente deve avere un modello Sling se deve esportare JSON. Pertanto, dovrai seguire questi due passaggi per abilitare l’esportazione JSON su qualsiasi componente.

* [Definire un modello Sling per il componente](#define-a-sling-model-for-the-component)
* [Annotare l’interfaccia del modello Sling](#annotate-the-sling-model-interface)

## Definire un modello Sling per il componente {#define-a-sling-model-for-the-component}

Innanzitutto, per il componente deve essere definito un modello Sling.

>[!NOTE]
>
>Per un esempio di utilizzo dei modelli Sling, consulta l’articolo [Sviluppo di esportatori di modelli Sling in AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

La classe di implementazione del modello Sling deve essere annotata con quanto segue:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

In questo modo il componente può essere esportato da solo utilizzando il selettore `.model` e l’ estensione `.json` .

Inoltre, questo specifica che la classe Sling Model può essere adattata all&#39;interfaccia `ComponentExporter`.

>[!NOTE]
>
>Le annotazioni Jackson non vengono solitamente specificate a livello di classe Sling Model, ma a livello di interfaccia Model. In questo modo, l’esportazione JSON viene considerata come parte dell’API del componente.

>[!NOTE]
>
>Le classi `ExporterConstants` e `ComponentExporter` provengono dal bundle `com.adobe.cq.export.json`.

### Utilizzo di più selettori {#multiple-selectors}

Sebbene non sia un caso d’uso standard, è possibile configurare più selettori in aggiunta al selettore `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

In tal caso, tuttavia, il selettore `model` deve essere il primo selettore e l’estensione deve essere `.json`.

## Annota l&#39;interfaccia del modello Sling {#annotate-the-sling-model-interface}

Per essere presi in considerazione dal framework JSON Exporter, l’interfaccia Model deve implementare l’ interfaccia `ComponentExporter` (o `ContainerExporter`, nel caso di un componente contenitore).

L&#39;interfaccia Sling Model corrispondente (`MyComponent`) viene quindi annotata utilizzando [Annotazioni Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) per definire come deve essere esportata (serializzata).

Per definire quali metodi devono essere serializzati, è necessario annotare correttamente l’interfaccia Model. Per impostazione predefinita, tutti i metodi che rispettano la convenzione di denominazione usuale per i getter verranno serializzati e deriveranno naturalmente i loro nomi di proprietà JSON dai nomi dei getter. Questo può essere impedito o ignorato utilizzando `@JsonIgnore` o `@JsonProperty` per rinominare la proprietà JSON.

## Esempio {#example}

[I ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) componenti core supportano l’esportazione JSON e possono essere utilizzati come riferimento.

Per un esempio, vedi l’implementazione del modello Sling del componente di base immagine e la relativa interfaccia annotata.

## Documentazione correlata {#related-documentation}

Per maggiori dettagli vedi:

* [Frammenti di contenuto nella guida utente Assets](/help/assets/content-fragments/content-fragments.md)
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
* [Authoring con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componenti core ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) e componente Frammento di  [contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)
