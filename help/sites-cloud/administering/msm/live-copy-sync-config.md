---
title: Configurazione della sincronizzazione di una Live Copy
description: Scopri le potenti opzioni di sincronizzazione Live Copy disponibili e come configurarle e personalizzarle in base alle esigenze del progetto.
feature: Multi Site Manager
role: Admin
exl-id: 0c97652c-edac-436e-9b5b-58000bccf534
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 94%

---


# Configurazione della sincronizzazione di una Live Copy {#configuring-live-copy-synchronization}

Adobe Experience Manager fornisce diverse configurazioni di sincronizzazione pronte all’uso. Prima di utilizzare le Live Copy, è necessario considerare quanto segue per definire come e quando vengono sincronizzate con il loro contenuto sorgente.

1. Decidi se le configurazioni di rollout esistenti soddisfano le tue esigenze
1. Se le configurazioni di rollout esistenti non fanno per te, decidi se crearne una tua.
1. Specifica le configurazioni di rollout da usare per le Live Copy.

## Configurazioni di rollout installate e personalizzate {#installed-and-custom-rollout-configurations}

Questa sezione fornisce informazioni sulle configurazioni di rollout installate e sulle azioni di sincronizzazione da esse utilizzate, nonché su come creare configurazioni personalizzate, se necessario.

>[!CAUTION]
>
>L’aggiornamento o la modifica di una configurazione di rollout preconfigurata **non** è consigliato. Se è necessaria un’azione live personalizzata, questa deve essere aggiunta in una configurazione di rollout personalizzata.

### Attivatori di rollout {#rollout-triggers}

Ogni configurazione di rollout utilizza un attivatore (o trigger) di rollout che determina l’esecuzione dell’implementazione. Le configurazioni di rollout possono utilizzare uno dei seguenti attivatori:

* **Al momento del rollout**: quando viene utilizzato il comando **Rollout** nella pagina blueprint oppure il comando **Sincronizza** nella pagina Live Copy.
* **In caso di modifica**: quando la pagina sorgente viene modificata.
* **Al momento dell’attivazione**: quando la pagina sorgente viene attivata.
* **Alla disattivazione**: quando la pagina sorgente viene disattivata.

>[!NOTE]
>
>L’utilizzo del trigger **Durante la modifica** può influire sulle prestazioni. Per ulteriori informazioni, consulta la sezione sulle [best practice per MSM](best-practices.md#onmodify).

### Configurazioni rollout {#rollout-configurations}

Nella tabella seguente sono elencate le configurazioni di rollout che vengono installate con AEM. La tabella contiene le azioni di attivazione e sincronizzazione per ciascuna configurazione di rollout.

Se le azioni di configurazione del rollout installate non soddisfano le tue esigenze, puoi [crea una configurazione di rollout.](#creating-a-rollout-configuration)

| Nome | Descrizione | Attivatore | [Azioni di sincronizzazione](#synchronization-actions) |
|---|---|---|---|
| Configurazione di rollout standard | Configurazione di rollout standard che consente di avviare il processo di rollout all’attivazione del rollout ed esegue le seguenti azioni: crea, aggiorna, elimina contenuto e ordina nodi figlio | Al momento del rollout | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`productUpdate`<br>`orderChildren` |
| Attiva in caso di attivazione Blueprint | Pubblica la Live Copy quando il sorgente viene pubblicato | Al momento dell’attivazione | `targetActivate` |
| Disattiva in caso di disattivazione Blueprint | Disattiva la Live Copy quando il sorgente è disattivato | Alla disattivazione | `targetDeactivate` |
| Invia dopo modifica | Invia il contenuto alla Live Copy quando il sorgente viene modificato<br>Utilizza questa configurazione di rollout con moderazione in quanto utilizza il trigger Durante la modifica. | In caso di modifica | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| Invia dopo modifica (superficiale) | Invia il contenuto alla Live Copy quando la pagina blueprint viene modificata, senza aggiornare i riferimenti (ad esempio, per le copie superficiali)<br>Utilizza questa configurazione di rollout con moderazione in quanto utilizza il trigger In caso di modifica. | In caso di modifica | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| Promuovi lancio | Configurazione di rollout standard per la promozione di pagine di lancio. | Al momento del rollout | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### Azioni di sincronizzazione {#synchronization-actions}

Nella tabella seguente sono elencate le azioni di sincronizzazione che vengono installate con AEM.

Se le azioni installate non soddisfano le tue esigenze, puoi [Crea una nuova azione di sincronizzazione.](/help/implementing/developing/extending/msm.md#creating-a-new-synchronization-action)

| Nome azione | Descrizione | Proprietà |
|---|---|---|
| `contentCopy` | Quando i nodi del sorgente non esistono nella Live Copy, copia i nodi in quest’ultima. [Configura il **servizio** CQ MSM Content Copy Action](#excluding-properties-and-node-types-from-synchronization) per specificare i tipi di nodo, gli elementi di paragrafo e le proprietà di pagina da escludere. |  |
| `contentDelete` | Questa azione elimina i nodi della Live Copy che non esistono nel sorgente. [Configura il **servizio** CQ MSM Content Delete Action](#excluding-properties-and-node-types-from-synchronization) per specificare i tipi di nodo, gli elementi di paragrafo e le proprietà di pagina da escludere. |  |
| `contentUpdate` | Questa azione aggiorna il contenuto della Live Copy con le modifiche apportate dal sorgente. [Configura il **servizio** CQ MSM Content Update Action](#excluding-properties-and-node-types-from-synchronization) per specificare i tipi di nodo, gli elementi di paragrafo e le proprietà di pagina da escludere. |  |
| `editProperties` | Questa azione modifica le proprietà della Live Copy. La proprietà `editMap` determina quali proprietà vengono modificate e il loro valore. Il valore della proprietà `editMap` deve utilizzare il formato seguente:<br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value` e `new_value` sono espressioni regolari e `n` è un numero intero incrementato.<br>Ad esempio, considera il seguente valore per `editMap`:<br>`sling:resourceType#/(contentpage`‖`homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>Questo valore modifica le proprietà dei nodi Live Copy come segue:<br>le `sling:resourceType` proprietà impostate su `contentpage` o `homepage` sono impostate su `mobilecontentpage`.<br>Le proprietà `cq:template` impostate su `contentpage` vengono impostate su `mobilecontentpage`. | `editMap: (String)` identifica la proprietà, il valore corrente e il nuovo valore. Per informazioni, consulta la descrizione. |
| `notify` | Questa azione invia un evento di pagina segnalando che è stata soggetta a rollout. Per ricevere una notifica, devi prima abbonarti agli eventi di rollout. |  |
| `orderChildren` | Questa azione ordina i nodi figli in base all’ordine della blueprint. |  |
| `referencesUpdate` | Questa azione di sincronizzazione aggiorna i riferimenti sulla Live Copy.<br>Cerca i percorsi nelle pagine Live Copy che puntano a una risorsa all’interno della blueprint. Quando viene trovato un percorso, lo aggiorna per indicare il punto in cui si trova la risorsa correlata all’interno della Live Copy. I riferimenti che hanno destinazioni esterne alla blueprint non vengono modificati. <br>[Configure il **servizio** CQ MSM References Update Action](#excluding-properties-and-node-types-from-synchronization) per specificare i tipi di nodo, gli elementi di paragrafo e le proprietà di pagina da escludere. |  |
| `targetVersion` | Crea una versione della pagina Live Copy.<br>Questa deve essere l’unica azione di sincronizzazione inclusa in una configurazione di rollout. |  |
| `targetActivate` | Questa azione attiva la Live Copy.<br>Questa deve essere l’unica azione di sincronizzazione inclusa in una configurazione di rollout. |  |
| `targetDeactivate` | Questa azione disattiva la Live Copy.<br>Questa deve essere l’unica azione di sincronizzazione inclusa in una configurazione di rollout. |  |
| `workflow` | Questa azione avvia il flusso di lavoro definito dalla proprietà target (solo per le pagine) e impiega la Live Copy come payload.<br>Il percorso di destinazione è il percorso del nodo modello. | `target: (String)` è il percorso del modello di flusso di lavoro. |
| `mandatory` | Questa azione imposta l’autorizzazione di diversi ACL nella pagina Live Copy in sola lettura per un determinato gruppo di utenti. Le seguenti ACL sono configurate:<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>utilizza questa azione solo per le pagine. | `target: (String)` è l’ID del gruppo per cui stai impostando le autorizzazioni. |
| `mandatoryContent` | Questa azione imposta l’autorizzazione di diversi ACL nella pagina Live Copy in sola lettura per un determinato gruppo di utenti. Le seguenti ACL sono configurate:<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>utilizza questa azione solo per le pagine. | `target: (String)` è l’ID del gruppo per cui stai impostando le autorizzazioni. |
| `mandatoryStructure` | Imposta l’autorizzazione dell’ACL `ActionSet.ACTION_NAME_REMOVE` nella pagina Live Copy in sola lettura per un determinato gruppo di utenti.<br>Usa questa azione solo per le pagine. | `target: (String)` è l’ID del gruppo per cui stai impostando le autorizzazioni. |
| `VersionCopyAction` | Se la pagina blueprint/sorgente è stata pubblicata almeno una volta, questa azione crea una pagina Live Copy utilizzando la versione pubblicata. Nota: questa azione è disponibile solo per la creazione di una pagina Live Copy basata su una pagina sorgente pubblicata e non per l’aggiornamento di una pagina Live Copy esistente. |  |
| `PageMoveAction` | La `PageMoveAction` si applica quando una pagina è stata spostata nella blueprint.<br>L’azione copia e non sposta la pagina Live Copy (correlata) dalla posizione prima dello spostamento a quella successiva.<br>La `PageMoveAction` non modifica la pagina Live Copy nella posizione in cui si trovava prima dello spostamento. Pertanto, per configurazioni di rollout consecutive ha lo stato di una relazione live senza blueprint.<br>[Configura il servizio **Azione di spostamento di pagine di CQ MSM**](#excluding-properties-and-node-types-from-synchronization) per specificare i tipi di nodo, gli elementi di paragrafo e le proprietà di pagina da escludere.<br>Questa deve essere l’unica azione di sincronizzazione inclusa in una configurazione di rollout. | Imposta `prop_referenceUpdate: (Boolean)` su true (predefinito) per aggiornare i riferimenti. |
| `markLiveRelationship` | Questa azione indica una relazione live per il contenuto creato da un lancio. |  |

### Creazione di una configurazione di rollout {#creating-a-rollout-configuration}

È possibile [creare una configurazione di rollout](/help/implementing/developing/extending/msm.md#creating-a-new-rollout-configuration) quando le configurazioni di rollout installate non soddisfano i requisiti dell’applicazione eseguendo i passaggi seguenti.

1. [Creare la configurazione di rollout:](/help/implementing/developing/extending/msm.md#create-the-rollout-configuration)
1. [Aggiungi azioni di sincronizzazione alla configurazione di rollout.](/help/implementing/developing/extending/msm.md#add-synchronization-actions-to-the-rollout-configuration)

La nuova configurazione di rollout è quindi disponibile quando configuri le configurazioni di rollout su una pagina blueprint o Live Copy.

### Esclusione delle proprietà e dei tipi di nodo dalla sincronizzazione {#excluding-properties-and-node-types-from-synchronization}

Puoi configurare diversi servizi OSGi che supportano le azioni di sincronizzazione corrispondenti in modo che non influiscano su proprietà e tipi di nodo specifici. Ad esempio, molte proprietà e sottonodi correlati al funzionamento interno di AEM non devono essere inclusi in una Live Copy. Deve essere copiato solo il contenuto rilevante all’utente della pagina.

Quando si lavora con AEM, sono disponibili diversi metodi di gestione delle impostazioni di configurazione per tali servizi. Per ulteriori dettagli e procedure consigliate, consulta [Configurazione di OSGi](/help/implementing/deploying/configuring-osgi.md).

Nella tabella seguente sono elencate le azioni di sincronizzazione per le quali è possibile specificare i nodi da escludere. La tabella fornisce i nomi dei servizi da configurare utilizzando la console web e il PID per la configurazione con un nodo dell’archivio.

| Azione di sincronizzazione | Nome del servizio nella console Web | Servizio PID |
|---|---|---|
| `contentCopy` | CQ MSM Content Copy Action | `com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory` |
| `contentDelete` | CQ MSM Content Delete Action | `com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory` |
| `contentUpdate` | CQ MSM Content Update Action | `com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory` |
| `PageMoveAction` | CQ MSM Page Move Action | `com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory` |
| `referencesUpdate` | CQ MSM References Update Action | `com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory` |

La tabella seguente descrive le proprietà che puoi configurare:

| Proprietà della console Web | Proprietà OSGi | Descrizione |
|---|---|---|
| Tipi di nodo esclusi | `cq.wcm.msm.action.excludednodetypes` | Un’espressione regolare che corrisponde ai tipi di nodo che devono essere esclusi dall’azione di sincronizzazione |
| Elementi di paragrafo esclusi | `cq.wcm.msm.action.excludedparagraphitems` | Un&#39;espressione regolare che corrisponde agli elementi di paragrafo da escludere dall’azione di sincronizzazione |
| Proprietà pagina escluse | `cq.wcm.msm.action.excludedprops` | Un’espressione regolare che corrisponde alle proprietà della pagina da escludere dall’azione di sincronizzazione |
| Tipi di nodi Mixin ignorati | `cq.wcm.msm.action.ignoredMixin` | Un’espressione regolare che corrisponde ai tipi di nodo mixin che devono essere esclusi dall’azione di sincronizzazione (disponibile solo per l&#39;azione `contentUpdate`) |

#### Azione di aggiornamento dei contenuti di CQ MSM - Esclusioni {#cq-msm-content-update-action-exclusions}

Per impostazione predefinita sono escluse diverse proprietà e tipi di nodo definiti nella configurazione OSGi di **Azione di aggiornamento dei contenuti di CQ MSM**, in **Proprietà pagina esclusa**.

Per impostazione predefinita le proprietà che corrispondono alle seguenti espressioni regolari sono escluse (ovvero non aggiornate) al momento del rollout:

![Regex di esclusione Live Copy](../assets/live-copy-exclude.png)

Puoi modificare le espressioni che definiscono l’elenco di esclusione secondo le tue esigenze.

Ad esempio, se desideri includere il **Titolo** della pagina nelle modifiche considerate per il rollout, rimuovi `jcr:title` dalle esclusioni. Ad esempio, con il codice regex:

`jcr:(?!(title)$).*`

### Configurazione della sincronizzazione per l’aggiornamento dei riferimenti {#configuring-synchronization-for-updating-references}

Puoi configurare diversi servizi OSGi che supportano le azioni di sincronizzazione corrispondenti, relative all’aggiornamento dei riferimenti.

Quando si lavora con AEM, sono disponibili diversi metodi di gestione delle impostazioni di configurazione per tali servizi. Per ulteriori dettagli e procedure consigliate, consulta [Configurazione di OSGi](/help/implementing/deploying/configuring-osgi.md).

Nella tabella seguente sono elencate le azioni di sincronizzazione per cui è possibile specificare l’aggiornamento dei riferimenti. La tabella fornisce i nomi dei servizi da configurare utilizzando la console web e il PID per la configurazione con un nodo dell’archivio.

| Proprietà della console Web | Proprietà OSGi | Descrizione |
|---|---|---|
| Aggiornare il riferimento tra LiveCopy nidificate | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | Seleziona questa opzione nella console web o imposta questa proprietà boolean su `true`utilizzare la configurazione dell’archivio per sostituire i riferimenti relativi a qualsiasi risorsa all’interno del ramo della Live Copy superiore. Disponibile solo per l&#39;azione `referencesUpdate`. |
| Aggiornare le pagine di riferimento | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | Seleziona questa opzione nella console web o imposta questa proprietà boolean su `true` utilizzando la configurazione dell’archivio per aggiornare eventuali riferimenti per utilizzare la pagina originale per fare riferimento invece alla pagina Live Copy. Disponibile solo per `PageMoveAction`. |

## Specifica delle configurazioni di rollout da utilizzare {#specifying-the-rollout-configurations-to-use}

MSM ti consente di specificare i set di configurazioni di rollout che vengono utilizzati generalmente e, quando è necessario, puoi eseguirne l&#39;override per specifiche Live Copy. MSM fornisce diverse posizioni per specificare le configurazioni di rollout da utilizzare. La posizione determina se la configurazione viene applicata a una Live Copy specifica.

Il seguente elenco di posizioni, in cui puoi specificare le configurazioni di rollout, descrive come MSM determina quali utilizzare per una Live Copy:

* **[Proprietà di pagina della Live Copy](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page):** quando una pagina Live Copy è configurata per l’utilizzo di una o più configurazioni di rollout, MSM utilizza tali configurazioni.
* **[Proprietà di pagina blueprint](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page):** quando una Live Copy è basata su una blueprint e la pagina Live Copy non presenta una configurazione di rollout, viene utilizzata la configurazione di rollout associata alla pagina blueprint sorgente.
* **Proprietà della pagina genitore della Live copy:** quando né la pagina Live Copy né la pagina sorgente blueprint presentano una configurazione di rollout, viene utilizzata la configurazione di rollout che si applica alla pagina genitore della Live Copy.
* **[Impostazione predefinita del sistema](live-copy-sync-config.md#setting-the-system-default-rollout-configuration):** quando la configurazione di rollout della pagina genitore della Live Copy non può essere determinata, viene utilizzata la configurazione predefinita del sistema.

Ad esempio, una blueprint utilizza il sito [WKND tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md) come contenuto sorgente. Viene creato un sito dalla blueprint. Ogni elemento nel seguente elenco descrive uno scenario diverso relativo all’utilizzo delle configurazioni di rollout:

* Nessuna delle pagine blueprint o delle Live Copy è impostata per l’utilizzo di una configurazione di rollout. MSM utilizza la configurazione di rollout predefinita del sistema per tutte le pagine Live Copy.
* La pagina root del sito di riferimento WKND ha impostate diverse configurazioni di rollout. MSM utilizza queste configurazioni di rollout per tutte le pagine Live Copy.
* La pagina root del sito di riferimento WKND ha impostate diverse configurazioni di rollout e la pagina principale del sito Live Copy presenta un diverso set di configurazioni di rollout. MSM utilizza le configurazioni di rollout che sono presenti nella pagina root del sito Live Copy.

### Impostazione delle configurazioni di rollout per una pagina Live Copy {#setting-the-rollout-configurations-for-a-live-copy-page}

Imposta una pagina Live Copy con le configurazioni di rollout da utilizzare quando la pagina sorgente è soggetta a rollout. Per impostazione predefinita, le pagine secondarie ereditano la configurazione. Quando imposti la configurazione di rollout da utilizzare, sovrascrivi di fatto la configurazione che la pagina Live Copy eredita dalla sua pagina genitore.

Puoi anche impostare le configurazioni di rollout per una pagina Live Copy quando [crei la Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page).

1. Utilizza la console **Sites** per selezionare la pagina Live Copy.
1. Seleziona **Proprietà** nella barra degli strumenti.
1. Apri la scheda **Live Copy.**

   La sezione **Configurazione** mostra le configurazioni di rollout ereditate dalla pagina.

   ![Ereditarietà Live Copy dalla pagina genitore](../assets/live-copy-inherit.png)

1. Se necessario, regola il flag **Ereditarietà Live Copy**. Se selezionato, la configurazione Live Copy ha effetto su tutte le pagine figlie.

1. Deseleziona la proprietà **Eredita configurazione di rollout dall’elemento principale**, quindi seleziona una o più configurazioni di rollout dall’elenco.

   Le configurazioni di rollout selezionate vengono visualizzate sotto l’elenco a discesa.

   ![Ignorare l’ereditarietà della configurazione di Live Copy](../assets/live-copy-inherit-override.png)

1. Seleziona **Salva e chiudi**.

### Impostazione della configurazione di rollout per una pagina blueprint {#setting-the-rollout-configuration-for-a-blueprint-page}

Configura una pagina blueprint con le configurazioni di rollout da utilizzare quando la pagina blueprint è soggetta a rollout.

Le pagine figlie della pagina blueprint ereditano la configurazione. Quando imposti la configurazione di rollout da utilizzare, potresti sovrascrivere la configurazione che la pagina eredita dalla sua pagina principale.

1. Utilizza la console **Sites** per selezionare la pagina principale della blueprint.
1. Seleziona **Proprietà** nella barra degli strumenti.
1. Apri la scheda **Blueprint.**
1. Seleziona una o più **Configurazioni di rollout** con il selettore a discesa.
1. Per confermare gli aggiornamenti, seleziona **Salva**.

### Impostazione della configurazione di rollout predefinita del sistema {#setting-the-system-default-rollout-configuration}

Per specificare una configurazione di rollout da utilizzare come predefinita del sistema, configura il seguente servizio OSGi.

* **Day CQ WCM Live Relationship Manager** con servizio PID `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Configura il servizio utilizzando la [console web](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o un [nodo di archivio](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* Nella console web, il nome della proprietà da configurare è **Default rollout config**.
* Utilizzando un nodo di archivio, il nome della proprietà da configurare è `liverelationshipmgr.relationsconfig.default`.

Imposta il valore di questa proprietà sul percorso della configurazione di rollout da utilizzare come impostazione predefinita del sistema. Il valore predefinito è `/libs/msm/wcm/rolloutconfigs/default`, che corrisponde alla **Configurazione di rollout standard**.
