---
title: Console Componenti
description: La console Componenti consente di sfogliare tutti i componenti definiti per la tua istanza
exl-id: f4949331-5302-46d3-a004-b813bb95ec2f
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 68%

---

# Console Componenti {#components-console}

La console Componenti consente di sfogliare tutti i componenti definiti per l’istanza e visualizzare le informazioni chiave per ciascun componente.

È possibile accedervi da **Strumenti ->** **Generale ->** **Componenti**. Poiché non vi è alcuna struttura ad albero per i componenti, è disponibile solo la vista a elenco.

![Console Componenti](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>La console Componenti mostra tutti i componenti presenti nel sistema. Il [browser Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) mostra i componenti disponibili per gli autori e nasconde eventuali gruppi di componenti che iniziano con un punto ( `.`).

## Ricerca {#search-field}

L’icona **Solo contenuto** (in alto a sinistra) permette di aprire il pannello **Ricerca** per cercare e/o filtrare i componenti:

![Ricerca nella console Componenti](/help/sites-cloud/authoring/assets/components-console-search.png)

### Dettagli dei componenti {#component-details}

Per visualizzare i dettagli di un componente specifico, tocca o fai clic sulla risorsa richiesta. Tre schede forniscono:

* **Proprietà**

  ![Proprietà della console Componenti](/help/sites-cloud/authoring/assets/components-console-properties.png)

  Nella scheda Proprietà puoi:

   * Visualizzare le proprietà generali del componente.
      * Visualizzare come è stata definita l’icona o l’abbreviazione per il componente. <!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * Facendo clic sull’origine dell’icona si aprirà quel componente.
   * Visualizza **Tipo di risorsa** e **Super Type risorsa** (se definito) per il componente.
      * Facendo clic sul Super Type della risorsa si aprirà quel componente.

  >[!NOTE]
  >
  >Poiché `/apps` non è modificabile in fase di esecuzione, la console Componenti è disponibile in sola lettura.

* **Criteri**

  ![Criteri della console Componenti](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **Utilizzo live**

  ![Utilizzo live dei componenti](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

  >[!CAUTION]
  >
  >A causa della natura delle informazioni raccolte, può essere necessario qualche momento per combinarle e visualizzarle.

* **Documentazione**

  L’eventuale documentazione del componente fornita dallo sviluppatore viene visualizzata nella scheda **Documentazione**. Se la documentazione non è disponibile, la scheda **Documentazione** non verrà visualizzata. <!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

  ![Documentazione relativa ai componenti](/help/sites-cloud/authoring/assets/components-console-documentation.png)
