---
title: Utilizzo di Nascondi condizioni
description: È possibile utilizzare le condizioni Nascondi per determinare se una risorsa componente è sottoposta o meno a rendering.
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 7adfe0ca7fbab1f8a5bd488e524a48be62584966
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 1%

---

# Utilizzo di Nascondi condizioni {#using-hide-conditions}

È possibile utilizzare le condizioni Nascondi per determinare se una risorsa componente è sottoposta o meno a rendering. Un esempio potrebbe essere quando un autore di modelli configura il componente core [list](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html?lang=it) nell&#39;[editor modelli](/help/sites-cloud/authoring/page-editor/templates.md) e decide di disabilitare le opzioni per creare l&#39;elenco in base alle pagine figlie. La disattivazione di questa opzione nella finestra di dialogo per progettazione imposta una proprietà in modo che, quando viene eseguito il rendering del componente Elenco, venga valutata la condizione Nascondi e non venga visualizzata l’opzione per visualizzare le pagine figlie.

## Panoramica {#overview}

Le finestre di dialogo possono diventare molto complesse con numerose opzioni per l’utente, che può utilizzare solo una frazione delle opzioni a sua disposizione. Questo può portare a esperienze di interfaccia utente schiaccianti per gli utenti.

Utilizzando le condizioni di nascondi, gli amministratori, gli sviluppatori e gli utenti con privilegi avanzati possono nascondere le risorse in base a un set di regole. Questa funzione consente loro di decidere quali risorse visualizzare quando un autore modifica il contenuto.

>[!NOTE]
>
>Se si nasconde una risorsa basata su un’espressione, le autorizzazioni ACL non vengono sostituite. Il contenuto rimane modificabile ma non viene visualizzato.

## Dettagli sull’implementazione e sull’utilizzo {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` è responsabile del filtraggio delle risorse in base all&#39;esistenza e al valore della proprietà `granite:hide`, situata nel campo da filtrare. L&#39;implementazione di `/libs/cq/gui/components/authoring/dialog/dialog.jsp` include un&#39;istanza di `FilteringResourceWrapper.`

L&#39;implementazione utilizza l&#39;API Granite [ELResolver](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) e aggiunge una variabile personalizzata `cqDesign` tramite ExpressionCustomizer.

Di seguito sono riportati alcuni esempi di condizioni di Nascondi in un nodo di progettazione che si trova in `etc/design` o come criterio del contenuto.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

Quando definisci l’espressione Nascondi, tieni presente quanto segue:

* Per essere valido, l&#39;ambito in cui viene trovata la proprietà deve essere espresso (ad esempio, `cqDesign.myProperty`).
* I valori sono di sola lettura.
* Le funzioni (se necessario) devono essere limitate a un determinato insieme fornito dal servizio.

## Esempio {#example}

Esempi di condizioni di Nascondi sono disponibili in AEM e nei [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) in particolare. Consideriamo ad esempio il componente di base [list](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html?lang=it) come implementato nell&#39;[esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

[Utilizzando l&#39;editor modelli](/help/sites-cloud/authoring/page-editor/templates.md), l&#39;autore del modello può definire nella finestra di dialogo per progettazione le opzioni del componente Elenco disponibili per l&#39;autore della pagina. È possibile abilitare o disabilitare opzioni quali l’abilitazione o meno dell’elenco come elenco statico, elenco di pagine figlie, elenco di pagine con tag e così via.

Se un autore di modelli sceglie di disabilitare l’opzione pagine figlie, viene impostata una proprietà di progettazione e viene valutata una condizione di nascondi in base a essa, impedendo all’autore della pagina di eseguire il rendering dell’opzione.

1. Per impostazione predefinita, l&#39;autore della pagina può utilizzare il componente core Elenco per creare un elenco utilizzando pagine figlie scegliendo l&#39;opzione **Pagine figlie**.

   ![Impostazioni componente elenco](assets/hide-conditions-list-settings.png)

1. Nella finestra di dialogo per progettazione del componente core Elenco, l&#39;autore del modello può scegliere l&#39;opzione **Disattiva elementi figlio** per impedire che l&#39;autore della pagina visualizzi l&#39;opzione per generare un elenco basato su pagine figlie.

   ![Finestra di dialogo per progettazione del componente Elenco](assets/hide-conditions-list-design.png)

1. Un nodo criteri viene creato in `/conf/wknd/settings/wcm/policies/wknd/components/list` con una proprietà `disableChildren` impostata su `true`.

   ![Struttura del nodo della condizione Nascondi](assets/hide-conditions-node-structure.png)

1. La condizione di Nascondi è definita come il valore di una proprietà `granite:hide` nel nodo della proprietà della finestra di dialogo `/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`

   ![Valutazione della condizione Nascondi](assets/hide-conditions-evaluation.png)

1. Il valore di `disableChildren` viene estratto dalla configurazione di progettazione e l&#39;espressione `${cqDesign.disableChildren}` restituisce `false`, il che significa che l&#39;opzione non verrà rappresentata come parte del componente.

1. L&#39;opzione **Pagine secondarie** non viene più visualizzata per l&#39;autore della pagina quando si utilizza il componente Elenco.

   ![Componente elenco con opzione figlio disabilitata](assets/hide-conditions-child-disabled.png)
