---
title: Console Componenti
description: La console Componenti consente di sfogliare tutti i componenti definiti per l’istanza
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Console Componenti {#components-console}

La console Componenti consente di sfogliare tutti i componenti definiti per l’istanza e visualizzare le informazioni chiave per ciascun componente.

It can be accessed from **Tools ->** **General ->** **Components**. Poiché non esiste una struttura ad albero per i componenti, è disponibile solo la vista a elenco.

![Console Componenti](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>La console Componenti mostra tutti i componenti del sistema. Il [browser Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) mostra i componenti disponibili agli autori e nasconde eventuali gruppi di componenti che iniziano con un punto ( `.`).

## Ricerca {#search-field}

L’icona **Solo contenuto** (in alto a sinistra) permette di aprire il pannello **Ricerca** per cercare e/o filtrare i componenti:

![Ricerca nella console Componenti](/help/sites-cloud/authoring/assets/components-console-search.png)

### Dettagli componente {#component-details}

Per visualizzare i dettagli relativi a un componente specifico, tocca/fai clic sulla risorsa desiderata. Sono disponibili tre schede:

* **Proprietà**

   ![Proprietà della console Componenti](/help/sites-cloud/authoring/assets/components-console-properties.png)

   Nella scheda Proprietà puoi:

   * Visualizzare le proprietà generali del componente.
      * Visualizzare come è stata definita l’icona o l’abbreviazione per il componente. <!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * Facendo clic sull’origine dell’icona passerai al relativo componente.
   * Visualizzare il **tipo di risorsa** e il **Super Type della risorsa** (se definito) per il componente.
      * Facendo clic su Super Type della risorsa passerai al relativo componente.
   >[!NOTE]
   >
   >Because `/apps` is not editable at runtime, the Components Console is read-only.

* **Criteri**

   ![Criteri della console dei componenti](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **Utilizzo live**

   ![Utilizzo live dei componenti](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

   >[!CAUTION]
   >
   >A causa della natura delle informazioni raccolte, può essere necessario qualche momento per combinarle e visualizzarle.

* **Documentazione**

   Se lo sviluppatore ha fornito la documentazione per il componente, questa viene visualizzata nella scheda **Documentazione**. Se non è presente documentazione, la scheda **Documentazione** non verrà visualizzata. <!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

   ![Documentazione dei componenti](/help/sites-cloud/authoring/assets/components-console-documentation.png)
