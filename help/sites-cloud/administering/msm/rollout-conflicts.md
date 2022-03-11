---
title: Conflitti di rollout
description: Scopri come gestire e risolvere i conflitti di rollout di Multi Site Manager.
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 3%

---

# Conflitti di rollout {#msm-rollout-conflicts}

Possono verificarsi conflitti se nuove pagine con lo stesso nome di pagina vengono create sia nel ramo blueprint che in un ramo Live Copy dipendente. Tali conflitti devono essere gestiti e risolti al momento del rollout.

## Gestione dei conflitti {#conflict-handling}

Quando esistono delle pagine in conflitto (nei rami blueprint e Live Copy), MSM ti consente di definire come (o anche se) devono essere gestite.

Per garantire che il rollout non sia bloccato, le definizioni possibili possono includere:

* Quale pagina (blueprint o Live Copy) avrà priorità durante il rollout
* Quali pagine verranno rinominate (e come)
* Come questo influenzerà eventuali contenuti pubblicati

Il comportamento predefinito di AEM è che il contenuto pubblicato non sarà interessato. Quindi, se una pagina creata manualmente nel ramo Live Copy è stata pubblicata, il contenuto verrà comunque pubblicato dopo la gestione e il rollout dei conflitti.

Oltre alla funzionalità standard, è possibile aggiungere gestori di conflitti personalizzati per implementare regole diverse. Questi possono anche consentire la pubblicazione di azioni come un singolo processo.

### Esempio di scenario {#example-scenario}

Nelle sezioni seguenti viene utilizzato l’esempio di una nuova pagina `b`, creato sia nella blueprint che nel ramo Live Copy (creato manualmente), per illustrare i vari metodi di risoluzione dei conflitti:

* blueprint: `/b`

   Una pagina master con 1 pagina figlio, `bp-level-1`

* Live Copy: `/b`

   Una pagina creata manualmente nel ramo Live Copy con una pagina figlia, `lc-level-1`

   * Attivato al momento della pubblicazione come `/b`, insieme alla pagina figlio

#### Prima del rollout {#before-rollout}

|  | Blueprint prima del rollout | Live Copy prima del rollout | Pubblica prima del rollout |
|---|---|---|---|
| Valore | `b` | `b` | `b` |
| Commento | Creato nel ramo blueprint, pronto per il rollout | Creazione manuale nel ramo Live Copy | Contiene il contenuto della pagina `b` creato manualmente nel ramo Live Copy |
| Valore | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Commento |  | Creazione manuale nel ramo Live Copy | contiene il contenuto della pagina `child-level-1` creato manualmente nel ramo Live Copy |

## Gestione rollout e gestione dei conflitti {#rollout-manager-and-conflict-handling}

Il rollout manager consente di attivare o disattivare la gestione dei conflitti.

Questa operazione viene eseguita utilizzando [Configurazione OSGi](/help/implementing/deploying/configuring-osgi.md) di **Day CQ WCM Rollout Manager**. Imposta il valore **Gestisci i conflitti con le pagine create manualmente** ( `rolloutmgr.conflicthandling.enabled`) su true se il gestore di rollout deve gestire i conflitti da una pagina creata in Live Copy con un nome esistente nella blueprint.

AEM [comportamento predefinito quando la gestione dei conflitti è stata disattivata.](#behavior-when-conflict-handling-deactivated)

## Gestori dei conflitti {#conflict-handlers}

AEM utilizza gestori di conflitti per risolvere eventuali conflitti di pagina esistenti durante il rollout del contenuto da una blueprint a una Live Copy. La ridenominazione delle pagine è il metodo consueto (non solo) per risolvere tali conflitti. Per consentire la selezione di diversi comportamenti, è possibile utilizzare più gestori di conflitti.

AEM fornisce:

* La [gestore di conflitti predefinito](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* La possibilità di attuare un [handler personalizzato](#customized-handlers)
* Meccanismo di classificazione del servizio che consente di impostare la priorità di ogni singolo gestore
   * Viene utilizzato il servizio con la classificazione più alta.

### Gestore dei conflitti predefinito {#default-conflict-handler}

Il gestore di conflitti predefinito è `ResourceNameRolloutConflictHandler`

* Con questo gestore la pagina blueprint ha la precedenza.
* La classificazione del servizio per questo gestore è impostata su bassa, ovvero al di sotto del valore predefinito per il `service.ranking` poiché si presume che i gestori personalizzati avranno bisogno di una classificazione più elevata. Tuttavia, la classificazione non è il minimo assoluto per garantire flessibilità quando necessario.

Questo gestore di conflitti ha la precedenza sulla blueprint. Esempio precedente, la pagina Live Copy `/b` viene spostato all’interno del ramo Live Copy in `/b_msm_moved`.

* Live Copy: `/b`

   Viene spostato all’interno della Live Copy in `/b_msm_moved`. Questo funge da backup e assicura che non venga perso alcun contenuto.

   * `lc-level-1` non viene spostato.

* Blueprint: `/b`

   Viene introdotto nella pagina Live Copy `/b`.

   * `bp-level-1` viene inviato alla Live Copy.

#### Dopo il rollout {#after-rollout}

|  | Blueprint dopo il rollout | Live Copy dopo il rollout | Live Copy dopo il rollout | Pubblica dopo il rollout |
|---|---|---|---|---|
| Valore | `b` | `b` | `b_msm_moved` | `b` |
| Commento |  | Contiene il contenuto della pagina blueprint `b` è stato introdotto | Contiene il contenuto della pagina `b` creato manualmente nel ramo Live Copy | Nessuna modifica, contiene il contenuto della pagina originale `b` creato manualmente nel ramo Live Copy e ora viene chiamato `b_msm_moved` |
| Valore | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Commento |  |  | Nessuna modifica | Nessuna modifica |

### Gestori personalizzati {#customized-handlers}

I gestori di conflitti personalizzati ti consentono di implementare regole personalizzate. Utilizzando il meccanismo di classificazione del servizio è inoltre possibile definire il modo in cui interagiscono con altri gestori.

I gestori di conflitti personalizzati possono:

* Fai un nome in base alle tue esigenze.
* Sviluppa/configura in base alle tue esigenze.
   * Ad esempio, puoi sviluppare un gestore in modo che la pagina Live Copy abbia la precedenza.
* Può essere progettato per essere configurato utilizzando [Configurazione OSGi](/help/implementing/deploying/configuring-osgi.md). In particolare:
   * **Classifica dei servizi** definisce l&#39;ordine relativo ad altri gestori di conflitti ( `service.ranking`).
      * Il valore predefinito è `0`.

### Comportamento quando la gestione dei conflitti è disattivata {#behavior-when-conflict-handling-deactivated}

Se manualmente [disattivare la gestione dei conflitti,](#rollout-manager-and-conflict-handling) AEM non interviene su alcuna pagina in conflitto. Le pagine non in conflitto vengono distribuite come previsto.

>[!CAUTION]
>
>Quando la gestione dei conflitti è disattivata, AEM non fornisce alcuna indicazione che i conflitti vengano ignorati. Poiché in tali casi questo comportamento deve essere configurato esplicitamente, si presume che sia il comportamento desiderato.

In questo caso la Live Copy ha effettivamente la precedenza. La pagina blueprint `/b` non viene copiata e la pagina Live Copy `/b` è lasciato intatto.

* Blueprint: `/b`

   Non viene copiato, ma viene ignorato.

* Live Copy: `/b`

   Rimane lo stesso.

#### Dopo il rollout {#after-rollout-no-conflict}

|  | Blueprint dopo il rollout | Live Copy dopo il rollout | Pubblica dopo il rollout |
|---|---|---|---|
| Valore | `b` | `b` | `b` |
| Commento |  | Nessuna modifica, presenta il contenuto della pagina `b` creato manualmente nel ramo Live Copy | Nessuna modifica, contiene il contenuto della pagina `b` creato manualmente nel ramo Live Copy |
| Valore | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Commento |  | Nessuna modifica | Nessuna modifica |

### Classificazioni di servizio {#service-rankings}

La [OSGi](https://www.osgi.org/) la classificazione del servizio può essere utilizzata per definire la priorità dei singoli gestori di conflitti.
