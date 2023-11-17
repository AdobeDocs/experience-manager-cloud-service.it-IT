---
title: Configurazione della modifica in blocco delle proprietà di pagina
description: Scopri come configurare la modifica in serie per poter modificare le proprietà di più pagine contemporaneamente.
exl-id: 0d10c6b9-8643-479d-adc1-4066d227e83d
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# Configurazione della modifica in blocco delle proprietà di pagina {#configuring-bulk-editing-of-page-properties}

[Modifica in serie delle proprietà di pagina](/help/sites-cloud/authoring/fundamentals/page-properties.md#from-the-sites-console-multiple-pages) consente di modificare le proprietà di più pagine contemporaneamente.

## Considerazioni {#considerations}

Le proprietà di pagina non sono abilitate per la modifica in serie come impostazione predefinita. Devono essere attivati esplicitamente. Quando definisci le proprietà della pagina da rendere disponibili per la modifica in blocco, devi tenere in considerazione alcune implicazioni, ad esempio:

* Alcuni campi sono in genere univoci. È necessario decidere se è utile abilitare questi campi per la modifica in blocco, quando verrà applicato un valore.
   * Ad esempio, i titoli delle pagine sono quasi sempre univoci.
* Alcuni campi possono avere più valori che richiedono una rappresentazione significativa durante il rendering.
   * Ad esempio, un elenco a discesa di stato etichettato **Pronto per la pubblicazione**. Questo potrebbe avere diversi valori prima della modifica in blocco, ad esempio **pronto**, **in-review**, **in corso** e così via.

A causa della possibilità di utilizzare più valori, si consiglia di abilitare solo i seguenti tipi di campo per la modifica in serie.

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## Abilitazione di un campo {#enabling-a-field}

Questi passaggi utilizzano `/apps/core/wcm/components/page/v1/page` dal [Contenuto di esempio WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) come esempio per abilitare la modifica in blocco su un campo in un ambiente di sviluppo.

1. Utilizzando CRXDE, apri il componente pagina.
1. Passa al campo richiesto all’interno di `cq:dialog` definizione.
1. Definisci la seguente proprietà sul nodo del campo:

   * **Nome**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valore**: `true`

1. Seleziona **Salva tutto** per mantenere gli aggiornamenti.

## Limitazioni {#limitations}

La modifica in blocco delle proprietà di pagina è:

* Non disponibile per le pagine all’interno di una Live Copy.
* Disponibile solo per le pagine con lo stesso tipo di risorsa.
