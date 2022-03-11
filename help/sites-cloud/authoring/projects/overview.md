---
title: Progetti
description: I progetti consentono di raggruppare le risorse in un’entità con ambiente comune e condiviso, che semplifica la gestione dei progetti
exl-id: c5f3331e-637f-4816-be83-faf2df59bd5f
source-git-commit: 8ea043b4b6424d6922c41c143ca74fd25ac60cf8
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 74%

---

# Progetti {#projects}

La funzione Progetti consente di raggruppare le risorse in una singola entità. Si ottiene così un ambiente comune e condiviso che semplifica la gestione dei progetti. I tipi di risorse che puoi associare a un progetto in AEM vengono definiti porzioni. Le porzioni possono includere informazioni sul progetto e sul team, risorse, flussi di lavoro e altri tipi di informazioni, come descritto in dettaglio in [Porzioni progetto.](#project-tiles)

>[!CAUTION]
>
>Affinché gli utenti dei progetti possano vedere altri utenti/gruppi utilizzando le funzionalità Progetti come la creazione di progetti, la creazione di attività/flussi di lavoro, la visualizzazione e la gestione del team, questi utenti devono avere accesso in lettura a `/home/users` e `/home/groups`. Il modo più semplice per implementarlo è quello di fornire **utenti dei progetti** accesso in lettura di gruppo a `/home/users` e `/home/groups`.

Come utente, puoi effettuare le seguenti operazioni:

* Creare progetti
* Assegnare contenuti e cartelle di attività a un progetto
* Eliminare progetti
* Rimuovere i collegamenti a contenuti dal progetto

Consulta i seguenti argomenti aggiuntivi:

* [Gestione dei progetti](/help/sites-cloud/authoring/projects/managing.md)
* [Utilizzo delle attività](/help/sites-cloud/authoring/projects/tasks.md)
* [Utilizzo dei flussi di lavoro per i progetti](/help/sites-cloud/authoring/projects/workflows.md)

## Console Progetti {#projects-console}

Dalla console dei progetti è possibile accedere ai tuoi progetti e gestirli in AEM.

![Console Progetti](/help/sites-cloud/authoring/assets/projects-console.png)

* Seleziona **Timeline** quindi un progetto per visualizzarne la relativa timeline.
* Tocca o fai clic su **Seleziona** per entrare nella modalità di selezione.
* Fai clic su **Crea** per aggiungere i progetti.
* **Mostra/Nascondi progetti attivi** consente di passare da tutti i progetti a solo quelli che sono attivi.
* **Mostra vista statistiche** consente di visualizzare le statistiche del progetto in relazione alle attività completate.

## Porzioni del progetto {#project-tiles}

Da Progetti, è possibile associare diversi tipi di informazioni ai progetti. Questi elementi vengono definiti **Porzioni**. In questa sezione, sono descritte le porzioni e il tipo di informazioni che contengono.

È possibile associare le seguenti porzioni al progetto. Le sezioni seguenti descrivono ogni porzione:

* Risorse e raccolte di risorse
* Esperienze
* Collegamenti
* Informazioni sul progetto
* Team
* Pagine di destinazione
* E-mail
* Flussi di lavoro
* Lanci
* Attività

### Assets {#assets}

Nella sezione **Risorse**, puoi raccogliere tutte le risorse usate per un particolare progetto.

![Riquadro risorse](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

Puoi caricare le risorse direttamente nella porzione. Inoltre, puoi creare set di immagini, set 360 gradi o set di file multimediali diversi se possiedi il componente aggiuntivo Elemento multimediale dinamico.

![Set di immagini](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### Raccolte di risorse {#asset-collections}

Come per le risorse, puoi aggiungere [raccolte di risorse](/help/assets/manage-collections.md) direttamente al tuo progetto. Puoi definire le raccolte in Risorse.

![Raccolta risorse](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

Per aggiungere una raccolta, fai clic su **Aggiungi raccolta** e seleziona la raccolta appropriata dall’elenco.

### Esperienze {#experiences}

La sezione **Esperienze** consente di aggiungere un’applicazione per dispositivi mobili, un sito web o una pubblicazione al progetto.

![Esperienze](/help/sites-cloud/authoring/assets/project-experiences.png)

Le icone indicano quale tipo di esperienza è rappresentata: sito web, app mobile o pubblicazione. Aggiungi le esperienze toccando o facendo clic sulla freccia giù e toccando **Aggiungi esperienza** e selezionando il tipo di esperienza.

![Aggiungi un’esperienza](/help/sites-cloud/authoring/assets/projects-add-experience.png)

Seleziona il percorso per le miniature, se applicabile, modifica la miniatura per l&#39;esperienza. Le esperienze sono raggruppate nel gruppo **Esperienze** piastrelle.

### Collegamenti {#links}

La sezione Collegamenti consente di associare collegamenti esterni al progetto.

![Collegamenti](/help/sites-cloud/authoring/assets/project-links.png)

Puoi denominare il collegamento con un nome facile da riconoscere, nonché modificare la miniatura.

![Aggiungi collegamento](/help/sites-cloud/authoring/assets/projects-add-link.png)

### Informazioni progetto {#project-info}

La porzione Informazioni progetto fornisce informazioni generali sul progetto, tra cui una descrizione, lo stato del progetto (attivo o inattivo), una scadenza e gli iscritti. Inoltre, puoi aggiungere una miniatura del progetto, che viene visualizzata nella pagina principale Progetti.

![Informazioni sul progetto](/help/sites-cloud/authoring/assets/project-info.png)

I membri del team possono essere assegnati a questa porzione ed eliminati (oppure è possibile modificare i ruoli), lo stesso vale per la porzione Team.

![Aggiungi membri del team al progetto](/help/sites-cloud/authoring/assets/projects-add-team.png)

### Processo di traduzione {#translation-job}

Dalla porzione Processo di traduzione puoi iniziare una traduzione e visualizzare lo stato delle traduzioni. Per configurare la traduzione, consulta [Creazione di progetti di traduzione](/help/assets/translate-assets.md).

![Processo di traduzione](/help/sites-cloud/authoring/assets/projects-translation-job.png)

Fai clic sull&#39;ellissi nella parte inferiore della **Processo di traduzione** per visualizzare le risorse nel flusso di lavoro di traduzione. Nell’elenco dei processi di traduzione vengono visualizzate anche le voci per i metadati risorsa e i tag. Queste voci indicano che anche i metadati e i tag per le risorse vengono tradotti.

![Dettaglio del lavoro di traduzione](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### Team {#team}

In questa porzione, è possibile specificare i membri del team del progetto. Durante la modifica, è possibile immettere il nome del membro del team e assegnare un ruolo all’utente.

![Riquadro del team](/help/sites-cloud/authoring/assets/projects-team-tile.png)

Puoi aggiungere ed eliminare membri dal team. Inoltre, puoi modificare il [ruolo utente](#user-roles-in-a-project) assegnato al membro del team.

![Aggiungi team dall&#39;elenco](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### Flussi di lavoro {#workflows}

Puoi assegnare il progetto in modo da seguire alcuni flussi di lavoro. Se i flussi di lavoro sono in esecuzione, il loro stato viene visualizzato nella porzione **Flussi di lavoro** in Progetti.

![Flussi di lavoro](/help/sites-cloud/authoring/assets/project-workflows.png)

Puoi assegnare il progetto in modo da seguire alcuni flussi di lavoro. A seconda del progetto scelto sono disponibili diversi flussi di lavoro.

I diversi flussi di lavoro sono descritti in [Utilizzo dei flussi di lavoro del progetto.](/help/sites-cloud/authoring/projects/workflows.md)

### Lanci {#launches}

La porzione Lanci mostra tutti i lanci richiesti con un [Flusso di lavoro di richiesta lancio.](/help/sites-cloud/authoring/projects/workflows.md) 

![Lanci](/help/sites-cloud/authoring/assets/project-launches.png)

### Attività {#tasks}

Le attività consentono di controllare lo stato di tutte le attività relative al progetto, tra cui i flussi di lavoro. I compiti sono trattati in dettaglio all&#39;indirizzo [Utilizzo delle attività](/help/sites-cloud/authoring/projects/tasks.md).

![Attività](/help/sites-cloud/authoring/assets/projects-tasks.png)

## Modelli di progetto {#project-templates}

AEM viene fornito con tre modelli diversi:

* Un progetto semplice: un esempio di riferimento per tutti i progetti che non rientrano in altre categorie (un catch-all). Comprende tre ruoli di base (Proprietari, Editor e Osservatori) e quattro flussi di lavoro (Approvazione progetto, Richiedi lancio, Richiedi pagina di destinazione e Richiedi e-mail).
* Un progetto multimediale: un progetto di esempio di riferimento per attività correlate ai contenuti multimediali. Include diversi ruoli di progetto relativi ai file multimediali (fotografi, editor, copywriter, designer, proprietari e osservatori). Richiede anche il flusso di lavoro Copia per richiedere e rivedere il testo.
* A [progetto di traduzione](/help/sites-cloud/administering/translation/overview.md) - Un esempio di riferimento per la gestione delle attività relative alla traduzione. Comprende tre ruoli di base (Proprietari, Editor e Osservatori). Include due flussi di lavoro a cui è possibile accedere nell’interfaccia utente Flussi di lavoro.

In base al modello selezionato, sono disponibili diverse opzioni, in particolare riguardo ai ruoli dell’utente e ai flussi di lavoro.

## Ruoli utente in un progetto {#user-roles-in-a-project}

I diversi ruoli dell’utente vengono impostati in un Modello di progetto e vengono utilizzati per due motivi principali:

1. Autorizzazioni. I ruoli dell’utente rientrano in una delle tre categorie elencate: Osservatore, Editor, Proprietario. Ad esempio, un fotografo o un copywriter avrà gli stessi privilegi di un editor. Le autorizzazioni determinano le azioni di un utente in relazione ai contenuti di un progetto.
1. Flussi di lavoro. I flussi di lavoro determinano a chi vengono assegnate le attività in un progetto. Le attività possono essere associate a un ruolo del progetto. Ad esempio, un’attività può essere assegnata ai fotografi così, tutti i membri del team che hanno il ruolo di fotografo, riceveranno l&#39;attività.

Tutti i progetti supportano i seguenti ruoli predefiniti per consentire all’utente di amministrare le autorizzazioni di controllo e protezione:

| Ruolo | Descrizione | Autorizzazioni | Iscrizione al gruppo |
|---|---|---|---|
| Osservatore | Un utente con questo ruolo può visualizzare le informazioni di progetto, tra cui lo stato del progetto. | Autorizzazioni di sola lettura per un progetto | `workflow-users` gruppo |
| Editor | Un utente con questo ruolo può caricare e modificare il contenuto di un progetto. | Accesso in lettura e scrittura a un progetto, ai metadati associati e alle risorse correlate; privilegi per caricare un elenco di foto e rivedere e approvare le risorse; autorizzazione scritta su /etc/commerce; modificare le autorizzazioni per un progetto specifico | gruppo degli utenti del flusso di lavoro |
| Proprietario | Un utente con questo ruolo può avviare un progetto. Un proprietario può creare un progetto, avviare il lavoro in un progetto e spostare anche le risorse approvate nella cartella Produzione. Il proprietario può visualizzare ed eseguire anche tutte le altre attività del progetto. | Autorizzazioni di scrittura su `/etc/commerce` | `dam-users` gruppo (per poter creare un progetto) amministratori di progetto (per poter creare un progetto e spostare risorse) |

>[!NOTE]
>
>Quando crei il progetto e aggiungi utenti ai vari ruoli, i gruppi associati al progetto vengono creati automaticamente per gestire le autorizzazioni associate. Ad esempio, un progetto denominato Mioprogetto avrebbe tre gruppi: **Proprietari mioprogetto**, **Editor mioprogetto**, **Osservatori mioprogetto**. Tuttavia, se il progetto viene eliminato, tali gruppi non vengono rimossi automaticamente. Un amministratore deve eliminare manualmente i gruppi da **Strumenti** > **Protezione** > **Gruppi**.
