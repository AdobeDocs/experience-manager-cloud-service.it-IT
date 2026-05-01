---
title: Controllo degli accessi basato su attributi
description: Scopri come abilitare il controllo degli accessi basato su attributi per definire regole basate su metadati per definire il livello di accesso alle risorse disponibili in Content Hub
role: Admin
badgeSaas: label="AEM Assets" type="Positive" tooltip="Si applica ad AEM Assets)."
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: b736af556c8580d005097c27cceba050b21a57c9
workflow-type: tm+mt
source-wordcount: '2139'
ht-degree: 2%

---


# Controllo degli accessi basato su attributi {#attribute-based-access-control}

Il controllo degli accessi basato su attributi (Attribute-Based Access Control - ABAC) consente agli amministratori di Content Hub di definire regole basate su metadati per controllare il livello di accesso alle risorse disponibili in Content Hub.

Gli amministratori di un’organizzazione definiscono regole per i gruppi di utenti, mappati su un ID gruppo. Le regole sono un mix di [operatori logici e di confronto](#supported-rule-constructs) e gli amministratori possono definire tutte le regole necessarie per gestire l&#39;accesso alle risorse in Content Hub.

Le regole si basano sui metadati. Se le condizioni definite in una regola corrispondono ai metadati della risorsa, la risorsa viene visualizzata al gruppo di utenti. Content Hub analizza i metadati delle risorse, inclusi i metadati personalizzati, per tutte le risorse disponibili in **All Assets** e **Collections** per visualizzare i risultati ai gruppi di utenti.

Ad esempio, CONSENTI l’accesso al gruppo di utenti con ID gruppo = 1011 quando i metadati della risorsa corrispondono a &quot;Brand = Brand X&quot; E &quot;Region = EMEA OR Americas&quot;. In Content Hub vengono visualizzate solo le risorse per il gruppo di utenti con ID = 1011, dove &quot;Marchio = Marchio X&quot; e &quot;Regione = EMEA o Americhe&quot;.

Le regole ABAC in Content Hub possono essere configurate utilizzando i seguenti approcci:

* **Configurazione self-service** con [Assistente IA in Content Hub](#configure-abac-using-ai-assistant-in-content-hub), con tecnologia AEM Governance Agent
* **Configurazione basata su foglio di calcolo** tramite [Supporto Adobe](#configure-abac-using-spreadsheet)

Con AI Assistant in Content Hub, gli amministratori possono definire e gestire le regole ABAC utilizzando metadati e linguaggio naturale. Questo consente una configurazione delle regole più rapida e riduce la dipendenza dai flussi di lavoro di supporto manuali.

Alcuni dei vantaggi principali del controllo degli accessi basato su attributi includono:

* Eliminazione della dipendenza dalla struttura di cartelle per le autorizzazioni
* Consenso agli amministratori di caricare le risorse e determinare retroattivamente le strutture delle autorizzazioni
* Riduce il numero di duplicati e migliora l’integrità delle risorse. I duplicati sono necessari nelle autorizzazioni basate su cartelle quando le stesse risorse sono condivise con gruppi diversi.
* Attiva l&#39;accesso granulare basato su regole
* Supporta la governance scalabile tra marchi e aree geografiche
* Migliora la gestione delle risorse

>[!VIDEO](https://video.tv.adobe.com/v/3475422/?captions=ita&learn=on&enablevpops){transcript=true}

## Come abilitare il controllo degli accessi basato su attributi {#enable-attribute-based-access-control}

Le regole ABAC in Content Hub possono essere configurate utilizzando i seguenti approcci:

* **Configurazione self-service tramite l&#39;Assistente all&#39;intelligenza artificiale in Content Hub (con tecnologia AEM Governance Agent)**\
  Gli amministratori possono definire e gestire le regole ABAC direttamente utilizzando il linguaggio naturale in Content Hub.

* **Configurazione basata su foglio di calcolo tramite il supporto Adobe**\
  Gli amministratori possono definire le regole ABAC in un foglio di calcolo e inviarle tramite il supporto Adobe per la configurazione.

## Configurare ABAC utilizzando l’Assistente AI in Content Hub

Con AI Assistant in Content Hub, basato su AEM Governance Agent, puoi creare e gestire le regole ABAC direttamente in Content Hub utilizzando il linguaggio naturale.

Operazioni disponibili:
* Cerca regole esistenti
* Creare le regole
* Aggiorna regole
* Elimina regole

In questo modo gli amministratori possono creare e gestire le regole di accesso senza dover ricorrere ai flussi di lavoro di supporto.

### Prima di iniziare {#before-you-begin-ai-assistant}

Prima di utilizzare l’Assistente IA in Content Hub per la configurazione delle regole ABAC, verifica quanto segue:

* Hai la licenza per AEM as a Cloud Service
* L’Assistente AI con tecnologia AEM Governance Agent è disponibile per la tua organizzazione
* Se non disponi ancora dell’accesso, contatta il rappresentante Adobe e completa i passaggi di licenza richiesti
* Non è necessario un pilota GenAI per il programma try-buy

### Passaggi per configurare le regole ABAC tramite l’Assistente AI {#steps-ai-assistant}

1. Apri Assistente IA in Content Hub.

1. Inizia con una semplice istruzione.

   Ad esempio:

   `Create a new rule in Content Hub`

   L’Assistente IA ti guida sulle informazioni necessarie per creare la regola.

1. Definisci la regola nel linguaggio naturale.

   Ad esempio:

   `Frescopa Web Marketers user group should have access to assets where product equals Frescopa`

1. Selezionare l&#39;ambiente in cui applicare la regola ABAC.

1. Rivedi la regola prima di applicarla.

   L’Assistente IA genera un’anteprima strutturata della regola. Non viene applicato nulla automaticamente. Puoi rivedere la regola generata, modificarla se necessario o annullare l’azione prima di applicarla.

1. Salva e applica la regola.

   Una volta salvata, la regola viene applicata in modo dinamico in base ai metadati.

Questo passaggio di revisione consente di garantire la precisione prima dell’applicazione della regola.

### Gestire le regole ABAC tramite prompt {#manage-abac-rules-using-prompts}

Dopo aver iniziato a utilizzare l&#39;Assistente IA, puoi gestire le regole ABAC a livello di conversazione.

**Scopri regole**

* Mostra tutte le regole ABAC di Content Hub esistenti

**Crea regole**

* Crea una regola che consenta al gruppo Marketing di prodotto di accedere a tutte le risorse
* Concedi l&#39;accesso al gruppo vendite alle risorse in cui l&#39;area geografica è uguale a EMEA

**Aggiorna regole**

* Aggiorna regola per il gruppo di marketing EMEA in modo da includere APAC

**Elimina regole**

* Elimina la regola per il gruppo Product Marketing

**Esplora metadati e gruppi**

* Mostra i gruppi disponibili e le proprietà dei metadati per impostare le regole

## Configurare ABAC utilizzando Spreadsheet

Se l&#39;Assistente AI non è abilitato per l&#39;organizzazione, è possibile configurare le regole ABAC utilizzando il flusso di lavoro basato su foglio di calcolo.

Fare clic su **Scarica foglio di calcolo** per scaricare e definire le regole in un foglio di calcolo. Crea un ticket di supporto Adobe e fornisci ad Adobe le regole definite nel foglio di calcolo.

[!BADGE Scarica il foglio di calcolo]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template.xlsx"}

Definisci le regole nel foglio di calcolo utilizzando le linee guida descritte in questo articolo.

>[!IMPORTANT]
>
>Dopo aver definito le regole, passare alla scheda **Errori di convalida** del foglio di calcolo e fare clic su **Esegui convalide ABAC**. Il messaggio **Tutte le convalide passate** conferma che puoi fornire le regole definite ad Adobe.

### Passaggi per configurare le regole ABAC tramite Foglio di calcolo {#steps-spreadsheet}

1. Scaricare il modello di foglio di calcolo ABAC.
1. Definisci le regole nel foglio di calcolo utilizzando condizioni basate su metadati.
1. Mappa ciascuna regola all’ID del gruppo IMS appropriato.
1. Acquisisci le finalità di business della regola nei commenti.
1. Invia un ticket di supporto Adobe e condividi il foglio di calcolo completato con Adobe.
1. Adobe configura le regole per la tua organizzazione.

## Esempio di utilizzo del controllo degli accessi basato su attributi {#example-metadata-based-rules}

Per supportare un rollout di marketing su larga scala, vari membri del team in aree geografiche e marchi diversi hanno bisogno di accedere alle risorse digitali. Ogni utente tipo ha un ambito specifico in base all’area geografica e al marchio. ABAC applica automaticamente queste regole utilizzando i metadati delle risorse. La tabella seguente illustra gli utenti tipo per questo caso d’uso e le regole applicate:

| Utente tipo | Ruolo | Descrizione ruolo | ID gruppo | Regola ABAC |
|---|---|---|---|---|
| John | Lead di marketing EMEA | Supervisiona l’esecuzione del marketing per tutti i brand nell’area EMEA. Deve accedere alle risorse approvate per tutte le marche destinate ai mercati EMEA. | group-emea-marketing | region = &quot;EMEA&quot; |
| Mike | Responsabile marketing APAC | Supervisiona l’esecuzione del marketing per tutti i brand in APAC. Deve accedere alle risorse approvate per tutti i marchi destinati ai mercati APAC. | group-apac-marketing | region = &quot;APAC&quot; |
| Sophie | Brand X Manager (EMEA) | Gestisce l’identità del marchio X nell’area EMEA. È necessario visualizzare solo i contenuti approvati del Brand X e personalizzati per i mercati EMEA. | group-emea-brandx | region = &quot;EMEA&quot; &amp;&amp; brand = &quot;Marchio X&quot; |
| Tom | Brand Y Manager (APAC) | Gestisce l’identità del marchio Y in APAC. Deve visualizzare solo i contenuti approvati con il marchio Y e personalizzati per i mercati APAC. | group-apac-brandy | region = &quot;APAC&quot; &amp;&amp; brand = &quot;Brand Y&quot; |

Utilizzando queste regole, gli amministratori di Content Hub dispongono di:

* **Accesso granulare basato su regole**: gli utenti visualizzano solo le risorse relative alla propria area geografica e al proprio marchio senza assegnazioni manuali delle autorizzazioni.
* **Collaborazione globale perfetta**: i team regionali e del brand lavorano in parallelo senza conflitti di accesso.
* **Autorizzazioni scalabili e a prova di futuro**: con l&#39;aggiunta di nuove aree geografiche o marchi, è possibile aggiornare le regole in base ai metadati.

### Scenari aggiuntivi in cui ABAC è utile {#additional-scenarios-abac}

ABAC può inoltre contribuire ad affrontare i seguenti scenari:

* **Accesso al marchio globale e regionale**: i team visualizzano solo le risorse rilevanti per il proprio marchio e il proprio mercato.
* **Collaborazione tra agenzie e partner**: le agenzie e i partner esterni possono accedere solo alle risorse della campagna pertinenti.
* **Accesso basato sui ruoli per i diversi team**: i team di marketing, vendite e legali possono accedere alle risorse rilevanti per la loro funzione.
* **Conformità legale specifica dell&#39;area**: gli utenti possono essere limitati alle risorse approvate per requisiti normativi o regionali specifici.

>[!IMPORTANT]
>
>Per impostazione predefinita, a tutti gli altri gruppi di utenti non specificati con regole nel [foglio di calcolo](#configure-abac-spreadsheet) viene negato l&#39;accesso. Se un utente non fa parte di alcun gruppo per il quale sono definite le regole ABAC, non può accedere ad alcuna risorsa. Se alcuni utenti devono avere accesso a tutte le risorse, ad esempio Amministratori, includi un gruppo con un ID gruppo nel foglio di calcolo e specifica che il gruppo richiede l’accesso a tutte le risorse in modo che Adobe possa configurarlo di conseguenza.

## Costrutti di regole supportati {#supported-rule-constructs}

* **Operatori logici**:
   * AND: Tutte le condizioni devono essere vere
   * OR: almeno una condizione deve essere true

* **Operatori di confronto**:
   * È uguale a (=): controlla se un utente o un attributo di risorsa corrisponde a un valore
   * Not Equals (!=): controlla se un utente o un attributo di risorsa non corrisponde a un valore

Quando i campi di metadati delle risorse contengono array, ad esempio più aree geografiche o tag, il termine &quot;uguale a&quot; fa riferimento a &quot;contiene logica&quot; e il termine &quot;diverso da&quot; fa riferimento a &quot;non contiene logica&quot;.

Questo consente di scrivere regole semplici ed espressive, come ALLOW if region = emea AND assetType != prototype AND tags != confidenziale.

## Linee guida {#guidelines-attribute-based-access-control}

Le seguenti linee guida si applicano sia alla configurazione basata su Assistente IA che a quella basata su foglio di calcolo:

* Le regole ABAC sono applicabili solo alle risorse approvate per Content Hub. Per ulteriori informazioni, vedere [Approvare Assets for Content Hub](/help/assets/approve-assets-content-hub.md).
* Non definire regole di NEGAZIONE. Converti sempre le regole DENY in regole ALLOW. Ad esempio, CONSENTI se region = utente-area DENY se assetType = prototipo AND Confidential = yes può essere convertito in CONSENTI se region = utente-area AND (assetType != prototype OR Confidential != yes).
* Le regole ABAC vengono applicate ai gruppi di utenti che utilizzano l’ID gruppo IMS, disponibile in Admin Console.
* È possibile impostare [Target di approvazione](/help/assets/approve-assets-content-hub.md#set-approval-target) per le risorse utilizzando l&#39;ambiente di authoring AEM as a Cloud Service. Le regole ABAC vengono applicate alle risorse approvate con Target di approvazione = Content Hub, in quanto Target di approvazione = Consegna è per le risorse disponibili per Consegna + Content Hub. Assets contrassegnato come Target di approvazione = La consegna è visibile a tutti in Content Hub.
* Assicurati che gli schemi di metadati utilizzati nelle regole ABAC siano correttamente definiti e disponibili in AEM. Fornisci il percorso completo dello schema di metadati o degli schemi in AEM che definiscono le proprietà a cui si fa riferimento nelle regole ABAC. Facoltativamente, puoi creare una cartella di test con risorse di esempio che soddisfino le condizioni ABAC per verificare il comportamento delle regole e valutare l’accesso in modo accurato.
* Acquisisci l’intento di business della regola nei commenti, anche se la condizione è scritta correttamente, perché l’intento consente di convalidare e correggere la logica, se necessario.
* Assicurati che i valori dei metadati utilizzati per le regole di accesso, come marchio, regione e prodotto, siano mantenuti in modo coerente tra le risorse.
* Inizia con casi d’uso chiave, ad esempio l’accesso basato su marchio o su regione.
* Utilizza i prompt di cancellazione quando definisci le regole con l’Assistente IA. Descrivi l’intento in linguaggio aziendale in modo che l’Assistente AI possa tradurlo in una regola strutturata.
* I file di licenza PDF impostati per DRM devono rimanere visibili a tutti gli utenti in modo che possano esaminare le informazioni sulla licenza durante il download della risorsa con la licenza.

## Domande frequenti {#faqs-attribute-based-access-control-content-hub}

### Cos’è il controllo degli accessi basato su attributi (Attribute-based Access Control - ABAC) in AEM Assets Content Hub?

Il controllo degli accessi basato su attributi (Attribute-Based Access Control - ABAC) in AEM Assets Content Hub consente agli amministratori di definire regole basate su metadati per controllare il livello di accesso alle risorse digitali da parte di diversi gruppi di utenti. L’accesso è determinato dalla corrispondenza dei metadati della risorsa con le condizioni specificate nelle regole, per una gestione granulare e dinamica della visibilità delle risorse.

### In che modo gli amministratori definiscono le regole di accesso utilizzando ABAC in AEM Assets Content Hub?

Gli amministratori definiscono le regole di accesso creando condizioni basate sui metadati delle risorse, ad esempio marchio o regione, e collegandole a ID di gruppi di utenti specifici. Queste regole utilizzano operatori logici e di confronto per specificare esattamente quali risorse sono visibili a quali gruppi di utenti.

### Quali sono i principali vantaggi dell’utilizzo di ABAC rispetto alle autorizzazioni tradizionali basate su cartelle in AEM Assets Content Hub?

ABAC elimina la dipendenza dalle strutture di cartelle per le autorizzazioni, consente agli amministratori di caricare le risorse e assegnare le autorizzazioni retroattivamente e riduce il numero di risorse duplicate necessarie. Ciò migliora l’integrità delle risorse e semplifica la gestione delle autorizzazioni, in particolare quando le risorse devono essere condivise con più gruppi.

### Gli amministratori possono impostare le regole ABAC direttamente nell’interfaccia Content Hub di AEM Assets?

Gli amministratori possono configurare le regole ABAC utilizzando l’Assistente IA in Content Hub, se abilitato per la propria organizzazione. Possono inoltre continuare a utilizzare il flusso di lavoro basato su fogli di calcolo tramite il supporto Adobe.

### Quali tipi di condizioni di metadati possono essere utilizzati durante la configurazione delle regole ABAC in AEM Assets Content Hub?

Le regole ABAC in AEM Assets Content Hub possono utilizzare operatori logici come AND e OR e operatori di confronto come è uguale a e non è uguale a. Le proprietà dei metadati utilizzate nelle regole devono essere definite correttamente e disponibili negli schemi di metadati di AEM e possono includere campi come area geografica, marchio, prodotto, campagna, tipo di risorsa o stato di pubblicazione.

### Perché AEM Assets Content Hub ABAC è particolarmente utile per le organizzazioni con team di grandi dimensioni e diverse esigenze di risorse?

ABAC è utile per le organizzazioni con team di grandi dimensioni perché consente un accesso granulare e basato su regole alle risorse in base a ruoli utente, aree geografiche, marchi o esigenze aziendali. Garantisce che gli utenti vedano solo le risorse rilevanti per le loro responsabilità, senza assegnazioni manuali di autorizzazioni o eccessiva duplicazione di risorse.

### In che modo gli amministratori devono preparare il foglio di calcolo ABAC per AEM Assets Content Hub prima di inviarlo al supporto Adobe?

Gli amministratori devono creare gruppi di utenti in Adobe Admin Console, annotare gli ID gruppo, definire chiaramente le autorizzazioni e le condizioni per ciascun gruppo nel foglio di calcolo, assicurarsi che tutte le proprietà dei metadati siano correttamente mappate agli schemi appropriati e utilizzare la colonna commenti per chiarire l’intento aziendale di ciascuna regola.