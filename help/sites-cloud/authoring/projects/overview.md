---
title: Progetti
description: I progetti consentono di raggruppare le risorse in un’unica entità il cui ambiente comune e condiviso ne semplifica la gestione
exl-id: c5f3331e-637f-4816-be83-faf2df59bd5f
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 96%

---

# Progetti {#projects}

La funzione Progetti consente di raggruppare le risorse in una singola entità. Si ottiene così un ambiente comune e condiviso che semplifica la gestione dei progetti. I tipi di risorse che puoi associare a un progetto in AEM vengono definiti porzioni. I riquadri possono includere informazioni sul progetto e sul team, risorse, flussi di lavoro e altri tipi di informazioni, come descritto in dettaglio in [Riquadri di progetto](#project-tiles).

>[!CAUTION]
>
>Affinché gli utenti dei progetti possano vedere altri utenti/gruppi mentre utilizzano le funzionalità, come la creazione di progetti, la creazione di attività/flussi di lavoro, la visualizzazione e la gestione del team, è necessario che tali utenti abbiano accesso in lettura a `/home/users` e `/home/groups`. Il modo più semplice per implementarlo è consentire al gruppo **utenti del progetto** l’accesso in lettura a `/home/users` e `/home/groups`.

Come utente, puoi effettuare le seguenti operazioni:

* Creare progetti
* Associare contenuto e cartelle di risorse a un progetto
* Eliminare progetti
* Rimuovere i collegamenti contenuto dal progetto

Consulta i seguenti argomenti aggiuntivi:

* [Gestione dei progetti](/help/sites-cloud/authoring/projects/managing.md)
* [Utilizzo delle attività](/help/sites-cloud/authoring/projects/tasks.md)
* [Utilizzo dei flussi di lavoro per i progetti](/help/sites-cloud/authoring/projects/workflows.md)

## Console Progetti {#projects-console}

Dalla console Progetti è possibile accedere e gestire i tuoi progetti in AEM.

![Console Progetti](/help/sites-cloud/authoring/assets/projects-console.png)

* Seleziona **Timeline** e quindi un progetto per visualizzarne la relativa timeline.
* Seleziona **Seleziona** per accedere alla modalità di selezione.
* Fai clic su **Crea** per aggiungere progetti.
* **Mostra/Nascondi progetti attivi** consente di passare da tutti i progetti a solo quelli che sono attivi.
* **Mostra vista statistiche** consente di visualizzare le statistiche del progetto relative al completamento delle attività.

## Riquadri progetto {#project-tiles}

Da Progetti è possibile associare diversi tipi di informazioni ai progetti. Questi vengono chiamati **Riquadri**. In questa sezione sono descritte tutti i riquadri e il tipo di informazioni che contengono.

È possibile associare i seguenti riquadri al progetto. Ciascuno è descritto nelle sezioni seguenti:

* Risorse e raccolte risorse
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

Nel riquadro **Risorse**, puoi raccogliere tutte le risorse utilizzate per un particolare progetto.

![Riquadro risorse](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

Le risorse vengono caricate direttamente nel riquadro. Inoltre, se disponi del componente aggiuntivo Dynamic Media, puoi creare set di immagini, set 360 gradi o set di file multimediali diversi.

![Set immagini](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### Raccolte di risorse {#asset-collections}

Come per le risorse, puoi aggiungere [raccolte di risorse](/help/assets/manage-collections.md) direttamente al progetto. Puoi definire le raccolte in Risorse.

![Raccolta risorse](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

Per aggiungere una raccolta, fai clic su **Aggiungi raccolta** e seleziona la raccolta appropriata dall’elenco.

### Esperienze {#experiences}

Il riquadro **Esperienze** consente di aggiungere un’app mobile, un sito web o una pubblicazione al progetto.

![Esperienze](/help/sites-cloud/authoring/assets/project-experiences.png)

Le icone indicano quale tipo di esperienza è rappresentata: sito web, app mobile o pubblicazione. Aggiungi le esperienze toccando o facendo clic sulla freccia giù e toccando **Aggiungi esperienza** e selezionando il tipo di esperienza.

![Aggiungi un&#39;esperienza](/help/sites-cloud/authoring/assets/projects-add-experience.png)

Seleziona il percorso per le miniature, se applicabile, modifica la miniatura per l&#39;esperienza. Le esperienze sono raggruppate insieme nel riquadro **Esperienze**.

### Collegamenti {#links}

Il riquadro Collegamenti consente di associare collegamenti esterni al progetto.

![Collegamenti](/help/sites-cloud/authoring/assets/project-links.png)

Puoi denominare il collegamento con un nome facile da riconoscere e modificare la miniatura.

![Aggiungi collegamento](/help/sites-cloud/authoring/assets/projects-add-link.png)

### Informazioni sul progetto {#project-info}

Il riquadro Informazioni sul progetto fornisce informazioni generali sul progetto, tra cui una descrizione, lo stato del progetto (attivo o inattivo), una data di scadenza e i membri. Inoltre, è possibile aggiungere una miniatura del progetto, che viene visualizzata nella pagina principale Progetti.

![Informazioni progetto](/help/sites-cloud/authoring/assets/project-info.png)

I membri del team possono essere assegnati a questo riquadro o al riquadro Team ed eliminati (oppure è possibile modificare i ruoli).

![Aggiungi membri del team al progetto](/help/sites-cloud/authoring/assets/projects-add-team.png)

### Processo di traduzione {#translation-job}

Dal riquadro Processo di traduzione puoi iniziare una traduzione e visualizzare lo stato delle traduzioni. Per impostare la traduzione, consulta [Creazione di progetti di traduzione](/help/assets/translate-assets.md).

![Lavoro di traduzione](/help/sites-cloud/authoring/assets/projects-translation-job.png)

Fai clic sull’ellissi nella parte inferiore della scheda **Lavoro di traduzione** per visualizzare le risorse nel flusso di lavoro di traduzione. Nell’elenco dei processi di traduzione vengono visualizzate anche le voci per i metadati risorsa e i tag. Queste voci indicano che anche i metadati e i tag per le risorse vengono tradotti.

![Dettaglio del lavoro di traduzione](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### Team {#team}

In questo riquadro è possibile specificare i membri del team del progetto. Durante la modifica, è possibile immettere il nome del membro del team e assegnare il ruolo utente.

![Riquadro team](/help/sites-cloud/authoring/assets/projects-team-tile.png)

Puoi aggiungere ed eliminare membri dal team. Inoltre, puoi modificare il [ruolo utente](#user-roles-in-a-project) assegnato al membro del team.

![Aggiungi team dall&#39;elenco](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### Flussi di lavoro {#workflows}

Puoi assegnare il progetto in modo da seguire determinati flussi di lavoro. Se sono in esecuzione dei flussi di lavoro, il loro stato viene visualizzato nel riquadro **Flussi di lavoro** in Progetti.

![Flussi di lavoro](/help/sites-cloud/authoring/assets/project-workflows.png)

Puoi assegnare il progetto in modo da seguire determinati flussi di lavoro. A seconda del progetto scelto, sono disponibili flussi di lavoro diversi.

Questi sono descritti in [Utilizzo dei flussi di lavoro del progetto](/help/sites-cloud/authoring/projects/workflows.md).

### Lanci {#launches}

Il riquadro Lanci mostra tutti i lanci richiesti con [Flusso di lavoro Richiesta lancio](/help/sites-cloud/authoring/projects/workflows.md).

![Lanci](/help/sites-cloud/authoring/assets/project-launches.png)

### Attività {#tasks}

Le attività consentono di monitorare lo stato di tutte le attività correlate al progetto, inclusi i flussi di lavoro. Le attività sono trattate in dettaglio in [Lavorare con le attività](/help/sites-cloud/authoring/projects/tasks.md).

![Attività](/help/sites-cloud/authoring/assets/projects-tasks.png)

## Modelli di progetto {#project-templates}

AEM viene fornito con tre modelli diversi:

* Un progetto semplice: un esempio di riferimento per tutti i progetti che non rientrano in altre categorie (onnicomprensivo). Comprende tre ruoli di base (Proprietari, Editor e Osservatori) e quattro flussi di lavoro (Approvazione progetto, Richiedi lancio, Richiedi pagina di destinazione e Richiedi e-mail).
* Un progetto multimediale: un progetto di riferimento per le attività che coinvolgono file multimediali. Include diversi ruoli di progetto relativi ai file multimediali (fotografi, editor, copywriter, designer, proprietari e osservatori). Necessita anche del flusso di lavoro Copia per richiedere e rivedere il testo.
* Un [progetto di traduzione](/help/sites-cloud/administering/translation/overview.md): un esempio di riferimento per la gestione delle attività di traduzione. Comprende tre ruoli di base (Proprietari, Editor e Osservatori). Include due flussi di lavoro a cui è possibile accedere dall’interfaccia utente Flussi di lavoro.

In base al modello selezionato, sono disponibili diverse opzioni, in particolare per i ruoli utente e i flussi di lavoro.

## Ruoli utente in un progetto {#user-roles-in-a-project}

I diversi ruoli utente vengono impostati in un modello di progetto e vengono utilizzati per due motivi principali:

1. Autorizzazioni. I ruoli utente rientrano in una delle tre categorie elencate: Osservatore, Editor, Proprietario. Ad esempio, un fotografo o un copywriter avrà gli stessi privilegi di un editor. Le autorizzazioni determinano cosa può fare un utente in relazione al contenuto di un progetto.
1. Flussi di lavoro. I flussi di lavoro determinano a chi vengono assegnate le attività di un progetto. Le attività possono essere associate a un ruolo del progetto. Ad esempio, un’attività può essere assegnata ai Fotografi in modo che tutti i membri del gruppo che hanno il ruolo di fotografo la riceveranno.

Tutti i progetti supportano i seguenti ruoli predefiniti che consentono di amministrare le autorizzazioni di protezione e controllo:

| Ruolo | Descrizione | Autorizzazioni | Iscrizione al gruppo |
|---|---|---|---|
| Osservatore | Un utente con questo ruolo può visualizzare i dettagli del progetto, compreso lo stato. | Autorizzazioni di sola lettura per un progetto | `workflow-users` gruppo |
| Editor | Un utente con questo ruolo può caricare e modificare il contenuto di un progetto. | Accesso in lettura e scrittura a un progetto, ai metadati associati e alle risorse correlate; privilegi per caricare un elenco di immagini, rivedere e approvare le risorse; permessi di scrittura su /etc/commerce; permessi di modifica su un progetto specifico. | gruppo utenti del flusso di lavoro |
| Proprietario | Un utente con questo ruolo può avviare un progetto. Un proprietario può creare un progetto, avviare il lavoro in un progetto e spostare le risorse approvate nella cartella di produzione. Il proprietario può visualizzare ed eseguire anche tutte le altre attività del progetto. | Autorizzazioni di scrittura su `/etc/commerce` | `dam-users` gruppo (per poter creare un progetto) amministratori di progetto (per poter creare un progetto e spostare risorse) |

>[!NOTE]
>
>Quando crei il progetto e aggiungi utenti ai vari ruoli, i gruppi associati al progetto vengono creati automaticamente per gestire le autorizzazioni associate. Ad esempio, un progetto denominato Mioprogetto avrebbe tre gruppi: **Proprietari mioprogetto**, **Editor mioprogetto**, **Osservatori mioprogetto**. Tuttavia, se il progetto viene eliminato, tali gruppi non vengono rimossi automaticamente. Un amministratore deve eliminare manualmente i gruppi in **Strumenti** > **Sicurezza** > **Gruppi**.
