---
title: Conflitti di rollout
description: Scopri come gestire e risolvere i conflitti di rollout di Multi Site Manager.
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 63%

---

# Conflitti di rollout {#msm-rollout-conflicts}

Possono verificarsi conflitti se nuove pagine con lo stesso nome vengono create sia nel ramo blueprint che in un ramo Live Copy dipendente. Tali conflitti devono essere gestiti e risolti al momento del rollout.

## Gestione dei conflitti {#conflict-handling}

Quando esistono delle pagine in conflitto (nei rami blueprint e Live Copy), MSM ti consente di definire come (o anche se) devono essere gestite.

Per garantire che il rollout non sia bloccato, le definizioni possibili possono includere:

* Quale pagina (blueprint o Live Copy) ha la priorità durante il rollout
* Quali pagine vengono rinominate e come
* Effetti su eventuali contenuti pubblicati

Il comportamento predefinito di Adobe Experience Manager (AEM) è che il contenuto pubblicato non è interessato. Pertanto, se una pagina creata manualmente nel ramo Live Copy è stata pubblicata, il contenuto viene comunque pubblicato dopo la gestione e il rollout dei conflitti.

Oltre alla funzionalità standard, è possibile aggiungere gestori di conflitti personalizzati per implementare regole diverse. Questi possono anche consentire la pubblicazione di azioni come un singolo processo.

### Esempio di scenario {#example-scenario}

Nelle sezioni seguenti viene utilizzato un esempio di nuova pagina `b`, creata sia nel ramo blueprint che Live Copy (creata manualmente), per illustrare i vari metodi di risoluzione dei conflitti:

* blueprint: `/b`

  Una pagina master con una pagina figlio, `bp-level-1`

* Live Copy: `/b`

  Una pagina creata manualmente nel ramo Live Copy con una pagina figlia, `lc-level-1`

   * Attivato al momento della pubblicazione come `/b`, insieme alla pagina figlio

#### Prima del rollout {#before-rollout}

|  | Blueprint prima del rollout | Live Copy prima del rollout | Pubblica prima del rollout |
|---|---|---|---|
| Valore | `b` | `b` | `b` |
| Commenti | Creato nel ramo blueprint, pronto per il rollout | Creato manualmente nel ramo Live Copy | Contiene il contenuto della pagina `b` creato manualmente nel ramo Live Copy |
| Valore | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Commenti |  | Creato manualmente nel ramo Live Copy | contiene il contenuto della pagina `child-level-1` creato manualmente nel ramo Live Copy |

## Gestione rollout e gestione dei conflitti {#rollout-manager-and-conflict-handling}

La gestione del rollout consente di attivare o disattivare la gestione dei conflitti.

Questa operazione viene eseguita utilizzando [Configurazione OSGi](/help/implementing/deploying/configuring-osgi.md) di **Day CQ WCM Rollout Manager**. Imposta il valore **Gestisci i conflitti con le pagine create manualmente** ( `rolloutmgr.conflicthandling.enabled`) su true se il gestore di rollout deve gestire i conflitti da una pagina creata in Live Copy con un nome esistente in blueprint.

AEM segue un [comportamento predefinito quando la gestione dei conflitti è stata disattivata.](#behavior-when-conflict-handling-deactivated)

## Gestori dei conflitti {#conflict-handlers}

AEM utilizza gestori di conflitti per risolvere eventuali conflitti di pagina esistenti durante il rollout del contenuto da blueprint a Live Copy. La ridenominazione delle pagine è il metodo consueto (non solo) per risolvere tali conflitti. Per consentire la selezione di diversi comportamenti, è possibile utilizzare più gestori di conflitti.

AEM fornisce:

* Il [gestore di conflitti predefinito](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* Possibilità di implementare un [gestore personalizzato](#customized-handlers)
* Meccanismo di classificazione del servizio che consente di impostare la priorità di ogni singolo gestore
   * Viene utilizzato il servizio con la classificazione più alta.

### Gestore dei conflitti predefinito {#default-conflict-handler}

Il gestore di conflitti predefinito è `ResourceNameRolloutConflictHandler`

* Con questo gestore, la pagina blueprint ha la precedenza.
* La classificazione del servizio per questo gestore è impostata su bassa. In altre parole, al di sotto del valore predefinito per la proprietà `service.ranking` perché si presume che i gestori personalizzati abbiano bisogno di una classificazione più elevata. Tuttavia, la classificazione non è il valore minimo assoluto per garantire flessibilità quando necessario.

Questo gestore di conflitti ha la precedenza sulla blueprint. Ad esempio, la pagina Live Copy `/b` viene spostata nel ramo Live Copy in `/b_msm_moved`.

* Live Copy: `/b`

  Viene spostato all’interno della Live Copy in `/b_msm_moved`. Questo funge da backup e assicura che non venga perso alcun contenuto.

   * `lc-level-1` non viene spostato.

* Blueprint: `/b`

  Viene distribuito alla pagina Live Copy `/b`.

   * `bp-level-1` viene distribuito nella Live Copy.

#### Dopo il rollout {#after-rollout}

|  | Blueprint dopo il rollout | Live Copy dopo il rollout | Live Copy dopo il rollout | Pubblica dopo il rollout |
|---|---|---|---|---|
| Valore | `b` | `b` | `b_msm_moved` | `b` |
| Commenti |  | Contiene il contenuto della pagina blueprint `b` su cui è stato eseguito il rollout | Contiene il contenuto della pagina `b` creato manualmente nel ramo Live Copy | Nessuna modifica; contiene il contenuto della pagina originale `b` creato manualmente nel ramo Live Copy e ora denominato `b_msm_moved` |
| Valore | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Commenti |  |  | Nessuna modifica | Nessuna modifica |

### Gestori personalizzati {#customized-handlers}

I gestori di conflitti personalizzati ti consentono di implementare regole personalizzate. Utilizzando il meccanismo di classificazione del servizio è inoltre possibile definire il modo in cui interagiscono con altri gestori.

I gestori di conflitti personalizzati possono:

* Essere nominati in base alle tue esigenze.
* Essere sviluppati/configurati in base alle tue esigenze.
   * Ad esempio, puoi sviluppare un gestore in modo che la pagina Live Copy abbia la precedenza.
* Può essere configurato utilizzando la [configurazione OSGi](/help/implementing/deploying/configuring-osgi.md). In particolare:
   * **Classifica dei servizi** definisce l’ordine relativo ad altri gestori di conflitti ( `service.ranking`).
      * Il valore predefinito è `0`.

### Comportamento quando la gestione dei conflitti è disattivata {#behavior-when-conflict-handling-deactivated}

Se [disattivi manualmente la gestione dei conflitti,](#rollout-manager-and-conflict-handling) AEM non interviene su alcuna pagina in conflitto. Le pagine non in conflitto sono distribuite come previsto.

>[!CAUTION]
>
>Quando la gestione dei conflitti è disattivata, AEM non fornisce alcuna indicazione che i conflitti vengano ignorati. Poiché in tali casi questo comportamento deve essere configurato esplicitamente, si presume che sia il comportamento desiderato.

In questo caso, la Live Copy ha effettivamente la precedenza. La pagina blueprint `/b` non viene copiata e la pagina Live Copy `/b` viene lasciata intatta.

* Blueprint: `/b`

  Non viene copiata, ma viene ignorata.

* Live Copy: `/b`

  Rimane lo stesso.

#### Dopo il rollout {#after-rollout-no-conflict}

|  | Blueprint dopo il rollout | Live Copy dopo il rollout | Pubblica dopo il rollout |
|---|---|---|---|
| Valore | `b` | `b` | `b` |
| Commenti |  | Nessuna modifica. Contiene il contenuto della pagina `b` creato manualmente nel ramo Live Copy | Nessuna modifica; contiene il contenuto della pagina `b` creato manualmente nel ramo Live Copy |
| Valore | `/bp-level-1,` | `/lc-level-1` | `/lc-level-1` |
| Commenti |  | Nessuna modifica | Nessuna modifica |

### Classificazioni di servizio {#service-rankings}

La classificazione del servizio [OSGi](https://www.osgi.org/) può essere utilizzata per definire la priorità dei singoli gestori di conflitti.
