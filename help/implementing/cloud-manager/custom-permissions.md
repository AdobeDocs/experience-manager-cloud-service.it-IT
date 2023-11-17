---
title: Autorizzazioni personalizzate
description: Scopri come utilizzare le autorizzazioni personalizzate per creare nuovi profili di autorizzazioni personalizzati con autorizzazioni configurabili per limitare l’accesso a programmi, pipeline e ambienti per gli utenti di Cloud Manager.
exl-id: 167da985-7f19-45b3-90a3-884817907da2
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 2%

---

# Autorizzazioni personalizzate {#custom-permissions}

Scopri come utilizzare le autorizzazioni personalizzate per creare nuovi profili di autorizzazioni personalizzati con autorizzazioni configurabili per limitare l’accesso a programmi, pipeline e ambienti per gli utenti di Cloud Manager.

>[!NOTE]
>
>Questa funzione è disponibile solo per [il programma early adopter.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Introduzione {#introduction}

Cloud Manager dispone di un set di ruoli predefiniti che disciplinano l’accesso a varie funzioni di Cloud Manager:

* Proprietario business
* Responsabile del programma
* Responsabile della distribuzione
* Sviluppatore

Le autorizzazioni personalizzate consentono agli utenti di creare nuovi profili di autorizzazioni personalizzati con autorizzazioni configurabili per limitare l’accesso degli utenti di Cloud Manager a programmi, pipeline e ambienti.

>[!TIP]
>
>Per informazioni dettagliate sui ruoli predefiniti, consulta il documento [Profili di prodotto e team as a Cloud Service AEM.](/help/onboarding/aem-cs-team-product-profiles.md)

## Utilizzo di autorizzazioni personalizzate {#using}

Per creare e utilizzare autorizzazioni personalizzate sono necessari tre passaggi:

1. [Crea un nuovo profilo di prodotto.](#create)
1. [Assegna autorizzazioni personalizzate al nuovo profilo di prodotto.](#assign-permissions)
1. [Assegna gli utenti al nuovo profilo di prodotto.](#assign-users)

Questa sezione descrive i passaggi seguenti. Potrebbe essere utile fare riferimento alla [Termini](#terms) e [Autorizzazioni configurabili](#configurable-permissions) quando si creano autorizzazioni personalizzate.

>[!NOTE]
>
>Per poter creare nuovi profili e gestire le autorizzazioni per Cloud Manager, in Admin Console Adobe Experience Manager as a Cloud Service devi disporre dei diritti di amministratore di prodotto.

### Creare un nuovo profilo di prodotto {#create}

Devi innanzitutto creare un profilo di prodotto prima del quale assegnare autorizzazioni personalizzate.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)

1. Nella pagina di destinazione di Cloud Manager, tocca o fai clic su **Gestisci accesso** pulsante

![Pulsante Gestisci accesso](assets/manage-access.png)

1. Sei reindirizzato al **Prodotti** dell’Admin Console, in cui puoi gestire utenti e autorizzazioni per cloud manager. Nell’Admin Console, tocca o fai clic su **Nuovo profilo** pulsante.

![Pulsante Nuovo profilo](assets/admin-console-new-profile.png)

1. Fornisci i dettagli generali sul profilo.

   * **Nome del profilo di prodotto** - Nome descrittivo del profilo
   * **Nome visualizzato** - Nome abbreviato che verrà visualizzato nell’interfaccia utente (opzioni)
   * **Descrizione** - Una descrizione informativa del profilo che ne spieghi la finalità (facoltativa)
   * **Notifica agli utenti via e-mail** - Se questa opzione è selezionata, gli utenti riceveranno una notifica via e-mail quando verranno aggiunti o rimossi da questo profilo.

1. Tocca o fai clic su **Salva** al termine.

Il nuovo profilo di prodotto viene salvato ed è visibile nell’elenco dei profili di prodotto nell’Admin Console.

### Assegnare autorizzazioni personalizzate al profilo {#assign-permissions}

Ora che disponi di un nuovo profilo di prodotto, puoi assegnargli autorizzazioni personalizzate.

1. Nell’Admin Console, tocca o fai clic sul nome del [nuovo profilo di prodotto appena creato.](#create)

1. Nella finestra visualizzata, seleziona la **Autorizzazioni** per visualizzare un elenco di autorizzazioni modificabili.

   ![Autorizzazioni modificabili](assets/permissions-tab.png)

1. Tocca o fai clic su **Modifica** collegamento di un’autorizzazione per modificarlo.

1. Il **Modifica autorizzazioni** viene visualizzata la finestra.
   * L’autorizzazione selezionata nel passaggio precedente è selezionata nella colonna sinistra.
   * Gli elementi di autorizzazione disponibili per l’assegnazione dell’autorizzazione si trovano nella colonna centrale etichettata **Autorizzazioni disponibili** Elementi.
   * Gli elementi delle autorizzazioni assegnate si trovano nella colonna di destra etichettata **Elementi autorizzazione inclusi**.

   ![Modifica autorizzazioni](assets/edit-permission-items.png)

1. Tocca o fai clic sul segno più (`+`) accanto all’elemento di autorizzazione per aggiungerlo alla colonna **Elementi autorizzazione inclusi**.

   * Tocca o fai clic su `i` accanto a un elemento di autorizzazione per ulteriori informazioni.

1. Tocca o fai clic su **Aggiungi tutto** nella parte superiore della **Autorizzazioni disponibili** per aggiungere tutte le autorizzazioni.

1. Se il profilo deve sempre avere tutti gli elementi di autorizzazione, è consigliabile utilizzare **Inclusione automatica** opzione.

   * **On** - Tutti gli elementi di autorizzazione correnti e futuri verranno spostati in Elementi di autorizzazione inclusi e al salvataggio saranno applicabili di conseguenza.
   * **Disattivato** - Tutti gli elementi di autorizzazione torneranno agli elementi di autorizzazione disponibili e al momento del salvataggio saranno applicabili di conseguenza.

1. Tocca o fai clic su **Salva** al termine della definizione delle autorizzazioni per il nuovo profilo di prodotto.

Il nuovo profilo di prodotto viene ora salvato con le relative autorizzazioni personalizzate.

### Assegnare utenti alle autorizzazioni personalizzate {#assign-users}

Ora puoi assegnare gli utenti al nuovo profilo di prodotto creato con autorizzazioni personalizzate.

1. Nell’Admin Console, tocca o fai clic sul nome del [nuovo profilo di prodotto a cui hai appena assegnato autorizzazioni personalizzate.](#assign-permissions)

1. Nella finestra visualizzata, seleziona la **Utenti** scheda.

1. Tocca o fai clic su **Aggiungi utenti** e assegna gli utenti al tuo nuovo profilo di prodotto con autorizzazioni personalizzate.

Consulta la sezione **Aggiungere utenti e gruppi di utenti a un profilo di prodotto** del documento [Gestire i profili di prodotto per gli utenti aziendali](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) per ulteriori dettagli su come utilizzare l’Admin Console.

## Autorizzazioni configurabili {#configurable-permissions}

Per creare profili personalizzati sono disponibili le seguenti autorizzazioni.

| Autorizzazione | Descrizione |
|---|---|
| Creazione programma | Consenti agli utenti di creare un programma |
| Accesso al programma | Consenti agli utenti di accedere ai programmi |
| Modifica del programma | Consenti agli utenti di modificare i programmi |
| Creazione dell’ambiente | Consenti agli utenti di creare un ambiente |
| Modifica dell’ambiente | Consenti agli utenti di aggiornare e modificare gli ambienti |
| Lettura registri ambiente | Consenti agli utenti di leggere i registri dell’ambiente |
| Creare pipeline | Consenti agli utenti di creare nuove pipeline |
| Eliminazione delle pipeline | Consenti agli utenti di eliminare le pipeline |
| Modifica pipeline | Consenti agli utenti di modificare le pipeline |
| Approvazione/rifiuto delle implementazioni di produzione | Consenti agli utenti di approvare o rifiutare un passaggio di distribuzione di produzione |
| Esecuzioni pipeline annullate | Consenti agli utenti di annullare le esecuzioni della pipeline |
| Inizio esecuzioni pipeline | Consenti agli utenti di avviare una nuova esecuzione della pipeline |
| Escludere/Rifiutare Errori Di Metriche Importanti | Consenti agli utenti di ignorare/rifiutare errori metrici importanti |
| Pianificazione delle implementazioni di produzione | Consenti agli utenti di pianificare un passaggio di distribuzione nell’ambiente di produzione |
| Accesso alle informazioni dell’archivio | Consenti agli utenti di accedere alle informazioni dell’archivio e generare la password di accesso |

### Autorizzazioni a livello di organizzazione {#organization-level}

Le autorizzazioni a livello di organizzazione si riferiscono alle autorizzazioni che vengono sempre concesse in tutti i programmi di un’organizzazione.

Le autorizzazioni seguenti sono autorizzazioni a livello di organizzazione:

* **Creazione programma** - Questa autorizzazione consente agli utenti di creare un programma all’interno dell’organizzazione.
* **Accesso alle informazioni dell’archivio** Questa autorizzazione a livello di tenant/organizzazione consente agli utenti di generare nome utente, password e URL dell’archivio per accedere e contribuire al progetto del cliente.
   * Il nome utente e la password per l’accesso all’archivio saranno comuni a tutti gli archivi nell’organizzazione, tuttavia l’URL dell’archivio sarà univoco per ciascun programma.
   * Consulta il documento [Accesso agli archivi](/help/implementing/cloud-manager/managing-code/accessing-repos.md) per ulteriori informazioni.

## Termini {#terms}

I seguenti termini vengono utilizzati per creare e gestire autorizzazioni personalizzate e ruoli predefiniti.

| Termine | Descrizione |
|---|---|
| Autorizzazioni predefinite | Ruoli predefiniti come **Proprietario business**, **Responsabile dell’implementazione**, ecc. per gestire diverse funzioni di Cloud Manager. Per informazioni dettagliate sui ruoli predefiniti, consulta il documento [Profili di prodotto e team as a Cloud Service AEM.](/help/onboarding/aem-cs-team-product-profiles.md) |
| Autorizzazioni personalizzate | Funzionalità di Cloud Manager che consentono agli utenti di creare profili di autorizzazione per definire ruoli che governino le funzioni supportate di Cloud Manager |
| Profilo di prodotto | Creato in Admin Console per gestire le autorizzazioni configurabili che saranno applicabili agli utenti che fanno parte del profilo di autorizzazione |
| Autorizzazione configurabile | Autorizzazioni di Cloud Manager che possono essere configurate nel profilo di autorizzazione |
| Elemento autorizzazione | Un programma, ambiente o risorsa pipeline a cui è possibile applicare un’autorizzazione |

Gli elementi autorizzazione si riferiscono all’ambito in cui verrà applicata l’autorizzazione. In genere si tratta di uno dei seguenti.

| Tipo di elemento autorizzazione | Esempio | Descrizione |
|---|---|---|
| Organizzazione | organizzazione:societàA | Tutte le risorse applicabili di un’organizzazione. Una risorsa può essere un programma, un ambiente o una pipeline. Se l’utente aggiunge un’organizzazione per qualsiasi autorizzazione, anche tutte le nuove risorse in tale organizzazione disporranno di tale autorizzazione. |
| Programma | Programma A | Tutte le risorse applicabili di un programma |
| Ambiente | Programma A: ambiente | Applicabile in un ambiente specifico |
| Pipeline  | Programma A: pipeline | Applicabile su una pipeline specifica |

## Limitazioni {#limitations}

Quando utilizzi le autorizzazioni personalizzate, tieni presente le seguenti limitazioni.

* Nel profilo delle autorizzazioni personalizzate verranno elencati anche i programmi, gli ambienti e le pipeline di AMS durante la configurazione delle autorizzazioni.
* Risorse come programma, ambiente, pipeline, ecc. La visualizzazione del file creato in Cloud Manager nell’Admin Console per la configurazione delle autorizzazioni potrebbe richiedere due minuti.
* In rari scenari in cui il servizio di autorizzazioni personalizzate non risponde, i profili predefiniti sono ancora disponibili e gli utenti nei profili predefiniti dispongono ancora dell’accesso appropriato.

## Domande frequenti {#faq}

### Quali profili di autorizzazione sono profili di autorizzazione predefiniti?

* Proprietario business
* Responsabile del programma
* Responsabile della distribuzione
* Sviluppatore

Per informazioni dettagliate sui ruoli predefiniti, consulta il documento [Profili di prodotto e team as a Cloud Service AEM.](/help/onboarding/aem-cs-team-product-profiles.md)

### Cosa succederà ai profili di autorizzazione predefiniti con l’introduzione ai profili personalizzati?

I profili di prodotto predefiniti e i ruoli di Cloud Manager continuano a funzionare come prima.

### Posso modificare i profili di autorizzazione predefiniti?

No, i profili predefiniti non sono modificabili. Non è possibile aggiungere o rimuovere autorizzazioni al profilo di autorizzazione predefinito. Puoi aggiungere o rimuovere utenti solo dai profili predefiniti.

### È necessario eliminare i profili di autorizzazione predefiniti perché i profili personalizzati sono ora disponibili?

I profili di autorizzazione predefiniti non devono essere eliminati dall’Admin Console.

### Posso aggiungere utenti a più profili di autorizzazione?

Sì, un utente può far parte di più profili, inclusi profili di autorizzazione predefiniti e personalizzati. Quando un utente viene assegnato a più profili, le autorizzazioni combinate di tutti i profili di autorizzazione assegnati saranno disponibili per tale utente.

### Cosa succede se un utente dispone dell’autorizzazione per modificare un ambiente o una pipeline ma non ha accesso a un programma che contiene l’ambiente o la pipeline?

In questo caso, l’utente non potrà accedere all’ambiente o alla pipeline se non dispone di **Accesso al programma** autorizzazioni contenenti l’ambiente o la pipeline.
