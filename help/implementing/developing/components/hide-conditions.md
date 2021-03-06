---
title: Utilizzo di Nascondi condizioni
description: È possibile utilizzare le condizioni Nascondi per determinare se è stato eseguito o meno il rendering di una risorsa componente.
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 2%

---

# Utilizzo di Nascondi condizioni {#using-hide-conditions}

È possibile utilizzare le condizioni Nascondi per determinare se è stato eseguito o meno il rendering di una risorsa componente. Un esempio è quello di un autore di modelli che configura il componente core [componente elenco](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html) in [editor modelli](/help/sites-cloud/authoring/features/templates.md) decide di disabilitare le opzioni per creare l’elenco in base alle pagine figlie. Se si disabilita questa opzione nella finestra di dialogo di progettazione, viene impostata una proprietà in modo che quando si esegue il rendering del componente elenco, venga valutata la condizione Nascondi e l’opzione per mostrare le pagine figlie non venga visualizzata.

## Panoramica {#overview}

Le finestre di dialogo possono diventare molto complesse con numerose opzioni per l&#39;utente, che possono utilizzare solo una frazione delle opzioni che sono a loro disposizione. Questo può portare a esperienze di interfaccia utente travolgenti per gli utenti.

Utilizzando le condizioni di visualizzazione, gli amministratori, gli sviluppatori e i super utenti possono nascondere le risorse in base a un set di regole. Questa funzione consente di decidere quali risorse visualizzare quando un autore modifica il contenuto.

>[!NOTE]
>
>Nascondere una risorsa basata su un&#39;espressione non sostituisce le autorizzazioni ACL. Il contenuto rimane modificabile, ma semplicemente non viene visualizzato.

## Implementazione e dettagli di utilizzo {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` è responsabile del filtraggio delle risorse in base all&#39;esistenza e al valore del `granite:hide` proprietà, situata nel campo da filtrare. L&#39;attuazione `/libs/cq/gui/components/authoring/dialog/dialog.jsp` include un&#39;istanza di `FilteringResourceWrapper.`

L&#39;implementazione utilizza la Granite [API ELResolver](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) e aggiunge un `cqDesign` variabile personalizzata tramite ExpressionCustomizer.

Di seguito sono riportati alcuni esempi di condizioni nascoste su un nodo di progettazione situato in `etc/design` o come criterio dei contenuti.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

Quando definisci l’espressione nascondi , tieni presente quanto segue:

* Per essere valido, l&#39;ambito in cui viene trovato il bene deve essere espresso (ad es. `cqDesign.myProperty`).
* I valori sono di sola lettura.
* Le funzioni (se necessarie) devono essere limitate a un determinato set fornito dal servizio.

## Esempio {#example}

Esempi di condizioni di nascondere possono essere trovati in tutto AEM e [componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) in particolare. Ad esempio, considera il [elenco dei componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html) come implementato in [Esercitazione WKND.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

[Utilizzo dell’editor modelli](/help/sites-cloud/authoring/features/templates.md), l’autore del modello può definire nella finestra di dialogo della progettazione quali opzioni del componente elenco sono disponibili per l’autore della pagina. Ad esempio, se consentire o meno che l’elenco sia un elenco statico, un elenco di pagine figlie, un elenco di pagine con tag e così via. possono essere abilitate o disabilitate.

Se un autore del modello sceglie di disabilitare l’opzione pagine figlie, viene impostata una proprietà di progettazione e viene valutata una condizione di nascondere, in modo che l’opzione non venga renderizzata per l’autore della pagina.

1. Per impostazione predefinita, l’autore della pagina può utilizzare il componente di base elenco per creare un elenco utilizzando pagine figlie, scegliendo l’opzione . **Pagine figlie**.

   ![Elenca impostazioni componente](assets/hide-conditions-list-settings.png)

1. Nella finestra di dialogo di progettazione del componente di base elenco, l’autore del modello può scegliere l’opzione **Disattiva bambini** per evitare che l’opzione generi un elenco basato su pagine figlie venga mostrata all’autore della pagina.

   ![Finestra di dialogo della progettazione di un componente elenco](assets/hide-conditions-list-design.png)

1. Un nodo di criteri viene creato in `/conf/wknd/settings/wcm/policies/wknd/components/list` con una proprietà `disableChildren` impostato su `true`.

   ![Struttura del nodo della condizione di nascondere](assets/hide-conditions-node-structure.png)

1. La condizione Nascondi è definita come valore di un `granite:hide` sul nodo della proprietà dialog `/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`

   ![Valutazione della condizione di nascondimento](assets/hide-conditions-evaluation.png)

1. Il valore di `disableChildren` viene estratto dalla configurazione di progettazione e dall’espressione `${cqDesign.disableChildren}` valuta `false`, il che significa che non viene eseguito il rendering dell’opzione come parte del componente.

1. Opzione **Pagine figlie** non viene più eseguito il rendering per l’autore della pagina quando si utilizza il componente elenco .

   ![Componente elenco con opzione figlio disabilitata](assets/hide-conditions-child-disabled.png)
