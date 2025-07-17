---
title: Controllo degli accessi basato su attributi
description: Scopri come abilitare il controllo degli accessi basato su attributi per definire regole basate su metadati per definire il livello di accesso alle risorse disponibili in Content Hub
role: Admin
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: ea1760a3076fa0e18dca38fe856ff0ef78b18f07
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 4%

---

# Controllo degli accessi basato su attributi {#attribute-based-access-control}

Il controllo degli accessi basato su attributi (Attribute-Based Access Control - ABAC) consente agli amministratori di Content Hub di definire regole basate su metadati per definire il livello di accesso alle risorse disponibili in Content Hub.

Gli amministratori di un’organizzazione definiscono regole per i gruppi di utenti, mappati su un ID gruppo. Le regole sono un mix di [operatori logici e di confronto](#supported-rule-constructs) e gli amministratori possono definire tutte le regole necessarie per gestire l&#39;accesso alle risorse in Content Hub.

Le regole si basano sui metadati e, se le condizioni definite nella regola corrispondono ai metadati della risorsa, la risorsa viene visualizzata al gruppo di utenti. Content Hub analizza i metadati della risorsa, inclusi i metadati personalizzati, per tutte le risorse disponibili in **Tutte le raccolte di Assets** e **Raccolte** per visualizzare i risultati ai gruppi di utenti.

Ad esempio, CONSENTI l’accesso al gruppo di utenti con ID gruppo = 1011, quando i metadati della risorsa corrispondono a &quot;Brand = Brand X&quot; E &quot;Region = EMEA OR Americas&quot;. In Content Hub vengono visualizzate solo le risorse con ID = 1011, dove Marchio = `Brand X` e Area geografica = `EMEA` o `Americas`.

Alcuni dei vantaggi principali del controllo degli accessi basato su attributi includono:

* Eliminazione della dipendenza dalla struttura di cartelle per le autorizzazioni

* Consenso agli amministratori di caricare le risorse e determinare retroattivamente le strutture delle autorizzazioni

* Riduzione del numero di duplicati, migliorando l’integrità della risorsa. I duplicati sono necessari nelle autorizzazioni basate su cartelle quando le stesse risorse sono condivise con gruppi diversi.

## Come abilitare il controllo degli accessi basato su attributi? {#enable-attribute-based-access-control}

Al momento, non è possibile creare autonomamente regole di controllo di accesso basate su attributi utilizzando l’interfaccia utente di Content Hub.

Fare clic su **Scarica foglio di calcolo** per scaricare e definire le regole in un foglio di calcolo. Crea un ticket di supporto Adobe e fornisci ad Adobe le regole definite nel foglio di calcolo.

[!BADGE Scarica il foglio di calcolo]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template_Validator.xlsx"}


Definisci le regole nel foglio di calcolo utilizzando le linee guida definite in questo articolo.

>[!IMPORTANT]
>
> Dopo aver definito le regole, passare alla scheda **Errori di convalida** del foglio di calcolo e fare clic su **Esegui convalide ABAC**. **Tutte le convalide passate** messaggio conferma che puoi fornire le regole definite ad Adobe.

## Esempio di utilizzo del controllo degli accessi basato su attributi {#example-metadata-based-rules}

Per supportare un rollout di marketing su larga scala, vari membri del team in aree geografiche e marchi diversi hanno bisogno di accedere alle risorse digitali. Ogni utente tipo ha un ambito specifico in base all’area geografica e al marchio. ABAC applica queste regole automaticamente tramite i metadati delle risorse. La tabella seguente illustra i diversi tipi di utenti tipo per questo caso d’uso e le regole applicate:

| Persona | Ruolo | Descrizione ruolo | ID gruppo | Regola ABAC |
|---------------------|----------------|-----------------|------------|------------|
| John | Lead di marketing EMEA | Supervisiona l’esecuzione del marketing per tutti i brand nell’area EMEA. Deve accedere alle risorse approvate per tutte le marche destinate ai mercati EMEA. | group-emea-marketing | region = &quot;EMEA&quot; |
| Mike | Responsabile marketing APAC | Supervisiona l’esecuzione del marketing per tutti i brand in APAC. Deve accedere alle risorse approvate per tutti i marchi destinati ai mercati APAC. | group-apac-marketing | region = &quot;APAC&quot; |
| Sophie | Brand X Manager (EMEA) | Gestisce l’identità del marchio X nell’area EMEA. È necessario visualizzare solo i contenuti approvati del Brand X e personalizzati per i mercati EMEA. | group-emea-brandx | region = &quot;EMEA&quot; &amp;&amp; brand = &quot;Marchio X&quot; |
| Tom | Brand Y Manager (APAC) | Gestisce l’identità del marchio Y in APAC. Deve visualizzare solo i contenuti approvati con il marchio Y e personalizzati per i mercati APAC. | group-apac-brandy | region = &quot;APAC&quot; &amp;&amp; brand = &quot;Brand Y&quot; |

Utilizzando queste regole, gli amministratori di Content Hub dispongono di:

* **Accesso granulare basato su regole**: gli utenti visualizzano solo le risorse rilevanti per la propria area geografica e il proprio marchio, senza assegnazioni manuali delle autorizzazioni.

* **Collaborazione globale perfetta**: i team regionali e del brand hanno lavorato in parallelo senza conflitti di accesso.

* **Autorizzazioni scalabili e a prova di futuro**: con l&#39;aggiunta di nuove aree geografiche o marchi, è possibile aggiornare le regole in base ai metadati.

>[!IMPORTANT]
>
> Per impostazione predefinita, a tutti gli altri gruppi di utenti, che non sono specificati con regole nel [foglio di calcolo](#enable-attribute-based-access-control), viene negato l&#39;accesso. Se un utente non fa parte di alcun gruppo per il quale sono definite le regole ABAC, non può accedere ad alcuna risorsa. Se hai bisogno che alcuni utenti abbiano accesso a tutte le risorse (ad esempio, Amministratori), nel foglio di calcolo deve essere menzionato un gruppo con un ID gruppo con i dettagli che questo particolare gruppo deve accedere a tutte le risorse, che Adobe configurerà automaticamente.


## Costrutti di regole supportati {#supported-rule-constructs}

* **Operatori logici**:
   * AND: Tutte le condizioni devono essere vere
   * OR: almeno una condizione deve essere true
* **Operatori di confronto**:
   * È uguale a (=): controlla se un utente o un attributo di risorsa corrisponde a un valore
   * Diverso da (!=): controlla se un utente o un attributo di risorsa non corrisponde a un valore

Quando i campi dei metadati delle risorse contengono array (ad esempio, più aree geografiche o tag), `Equals` fa riferimento alla logica `contains` e `Not Equals` alla logica `does not contain`.

Questo consente di scrivere regole semplici ed espressive, come: ALLOW if region = emea AND assetType != prototipo E tag != riservato.

## Linee guida {#guidelines-attribute-based-access-control}

* Le regole ABAC sono applicabili solo alle risorse approvate per Content Hub. Per ulteriori informazioni, vedere [Approvare Assets for Content Hub](/help/assets/approve-assets-content-hub.md).

* Non assegnare le regole DENY, ma convertire sempre la regola DENY in ALLOW. Ad esempio, `ALLOW if region = <user-region> DENY if assetType = prototype AND confidential = yes` può essere convertito in `ALLOW if region = <user-region> AND (assetType != prototype OR confidential != yes)`.

* Le regole ABAC vengono applicate ai gruppi di utenti che utilizzano l’ID gruppo IMS, disponibile in Admin Console.


* È possibile impostare [Target di approvazione](/help/assets/approve-assets-content-hub.md#set-approval-target) per le risorse utilizzando l&#39;ambiente di authoring AEM as a Cloud Service. Le regole ABAC vengono applicate alle risorse approvate con Target di approvazione = `Content Hub`, poiché Target di approvazione = `Delivery` è per le risorse disponibili per `Delivery` + `Content Hub`. Assets contrassegnato come destinazione di approvazione = `Delivery` sono visibili a tutti nell&#39;hub del contenuto.

* Assicurati che gli schemi di metadati utilizzati nelle regole ABAC siano correttamente definiti e disponibili in AEM. Fornisci il percorso completo degli schemi di metadati in AEM che definiscono le proprietà a cui si fa riferimento nelle regole ABAC. Facoltativamente, puoi creare una cartella di test con alcune risorse di esempio con valori di metadati che corrispondono alle condizioni ABAC. Questo aiuta a verificare il comportamento delle regole e a valutare con precisione l’accesso.

* Acquisisci l’intento di business della regola nel commento, indipendentemente dal fatto che la condizione sia scritta correttamente, in quanto l’intento ci aiuta a convalidare e correggere la logica, se necessario.

* I file PDF delle licenze impostati per DRM devono essere visibili a tutti, in modo che gli utenti possano visualizzarli quando scaricano la risorsa con licenza.
