---
title: Abilitazione dell’esportazione JSON per un componente
description: I componenti possono essere adattati per generare l’esportazione JSON dei contenuti in base a un framework modellatore.
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 12%

---

# Abilitazione dell’esportazione JSON per un componente {#enabling-json-export-for-a-component}

I componenti possono essere adattati per generare l’esportazione JSON dei contenuti in base a un framework modellatore.

## Panoramica {#overview}

L’esportazione JSON si basa su [Modelli Sling](https://sling.apache.org/documentation/bundles/models.html), e sul [Esportatore modello Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (che si basa su [Annotazioni Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Questo significa che il componente deve avere un modello Sling per esportare JSON. Pertanto, dovrai seguire questi due passaggi per abilitare l’esportazione JSON su qualsiasi componente.

* [Definire un modello Sling per il componente](#define-a-sling-model-for-the-component)
* [Annotare l’interfaccia del modello Sling](#annotate-the-sling-model-interface)

## Definire un modello Sling per il componente {#define-a-sling-model-for-the-component}

Innanzitutto, è necessario definire un modello Sling per il componente.

>[!NOTE]
>
>Per un esempio di utilizzo dei modelli Sling, consulta l’articolo [Sviluppo di esportatori di modelli Sling nell’AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=it).

La classe di implementazione del modello Sling deve essere annotata con le seguenti annotazioni:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

In questo modo il componente può essere esportato da solo utilizzando `.model` e il `.json` estensione.

Inoltre, questo specifica che la classe del modello Sling può essere adattata in `ComponentExporter` di rete.

>[!NOTE]
>
>Le annotazioni Jackson di solito non sono specificate a livello di classe di modello Sling, ma piuttosto a livello di interfaccia di modello. In questo modo, l’esportazione JSON deve essere considerata parte dell’API del componente.

>[!NOTE]
>
>Il `ExporterConstants` e `ComponentExporter` le classi provengono da `com.adobe.cq.export.json` pacchetto.

### Utilizzo di più selettori {#multiple-selectors}

Anche se non è un caso di utilizzo standard, è possibile configurare più selettori oltre al `model` selettore.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Tuttavia, in tal caso, `model` il selettore deve essere il primo selettore e l’estensione deve essere `.json`.

## Annotare l’interfaccia del modello Sling {#annotate-the-sling-model-interface}

Affinché il framework di esportazione JSON possa tenere conto di, l’interfaccia modello deve implementare `ComponentExporter` interfaccia (o `ContainerExporter`, nel caso di un componente contenitore).

Interfaccia corrispondente del modello Sling (`MyComponent`) verrebbe quindi annotato utilizzando [Annotazioni Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) per definire la modalità di esportazione (serializzata).

L’interfaccia del modello deve essere annotata correttamente per definire quali metodi serializzare. Per impostazione predefinita, tutti i metodi che rispettano la consueta convenzione di denominazione per i getter vengono serializzati e deriveranno i loro nomi di proprietà JSON naturalmente dai nomi dei getter. Questo può essere impedito o sovrascritto utilizzando `@JsonIgnore` o `@JsonProperty` per rinominare la proprietà JSON.

## Esempio {#example}

[Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) supporta l’esportazione JSON e può essere utilizzato come riferimento.

Ad esempio, consulta l’implementazione del modello Sling del componente core Immagine e la relativa interfaccia con annotazioni.

## Documentazione correlata {#related-documentation}

Per maggiori dettagli, cfr.:

* [Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md)
* [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [Authoring con frammenti di contenuto](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [Componente Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=it)
