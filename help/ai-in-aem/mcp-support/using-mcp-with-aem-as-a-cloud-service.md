---
title: Utilizzo di MCP con AEM as a Cloud Service
description: Scopri come utilizzare Model Context Protocol con AEM as a Cloud Service
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 03ce511a28cf0fbbdd6e49d63736107720ef017b
workflow-type: tm+mt
source-wordcount: '2034'
ht-degree: 0%

---


# Utilizzo di MCP con AEM as a Cloud Service {#using-mcp-with-aem-as-a-cloud-service}

## Introduzione {#introduction}

Molti team di AEM ora lavorano in IDE e applicazioni basate su chat come Cursor, ChatGPT, Anthropic Claude e Microsoft Copilot Studio. Queste applicazioni supportano il protocollo MCP (Model Context Protocol), che consente alle applicazioni di esporre gli strumenti back-end a modelli LLM (Large Language Model) in modo standardizzato.

Con l’integrazione MCP di AEM, utenti tipo diversi possono collaborare intorno allo stesso contenuto:

* **Gli sviluppatori** possono orchestrare operazioni e flussi di lavoro per contenuti dalla loro applicazione IDE o chat
* **I professionisti** e gli architetti di contenuti possono gestire siti, frammenti di contenuto e risorse con assistenza AI, pur rimanendo nel modello di autorizzazioni esistente di AEM.

>[!IMPORTANT]
>
> Per gli scenari che modificano o eliminano il contenuto, i professionisti devono utilizzare l’interfaccia di AI Assistant anziché richiamare direttamente gli strumenti MCP, perché gli agenti AEM eseguiti da AI Assistant includono protezioni integrate.
>

Questo articolo spiega cosa fornisce la funzionalità MCP di AEM, quali applicazioni MCP sono supportate, come configurarla e come utilizzarla nella pratica.

## Perché MCP è utile per i clienti AEM {#why-mcp-is-useful-for-aem-customers}

Le moderne applicazioni IDE e chat utilizzano MCP come metodo per consentire a un LLM di richiamare gli strumenti esposti dietro i server MCP. Invece di scrivere codice in base alle specifiche API di basso livello, i clienti possono descrivere il proprio intento in linguaggio naturale (*&quot;aggiornare il banner principale per questa campagna in tutte le pagine&quot;*) e consentire al LLM di richiamare gli strumenti MCP appropriati, che a loro volta interagiscono con le API di AEM.

I vantaggi principali includono:

* **Interazione con linguaggio naturale invece del plumbing API**
Gli strumenti MCP descrivono le operazioni disponibili e come chiamarle. LLM utilizza questi schemi per decidere quali strumenti richiamare e con quali parametri.
* **Esperienza coerente nelle applicazioni**
Gli stessi strumenti MCP di AEM possono essere utilizzati da più applicazioni compatibili con MCP, consentendo ai team di lavorare dove sono più produttivi e richiamando le stesse funzionalità AEM sottostanti.
* **Protezione e governance mantenute**
Le richieste agli strumenti MCP di AEM vengono eseguite con l’identità dell’utente autenticato e ogni strumento applica le autorizzazioni AEM esistenti dell’utente. Le operazioni basate sull’intelligenza artificiale seguono le stesse regole di accesso del lavoro manuale in AEM.

## Server MCP forniti da AEM {#mcp-servers-provided-by-aem}

AEM espone i server MCP come endpoint HTTP. Gli endpoint elencati di seguito sono relativi a:

`https://mcp.adobeaemcloud.com/adobe/mcp/`

### Server MCP {#mcp-servers}

| **Server MCP** | **Endpoint** | **Descrizione** |
|---|---|----------------------------------------------------------------------------------------------------------------------|
| **Contenuto** | `/content` | Tutte le operazioni relative ai contenuti di basso livello, tra cui creazione, lettura, aggiornamento ed eliminazione (CRUD) per pagine, frammenti e risorse. |
| **Contenuto (sola lettura)** | `/content-readonly` | Operazioni per contenuti di sola lettura (Get, List/Search) per pagine, frammenti e risorse. |

Gli strumenti specifici esposti da ciascun server MCP possono evolvere nel tempo. In pratica, puoi chiedere all’applicazione abilitata per MCP di individuare gli strumenti tramite un prompt come:

*&quot;Elenca tutti gli strumenti MCP di AEM disponibili su questo server e descrivi le operazioni eseguite.&quot;*

Il client MCP utilizzerà il protocollo MCP per recuperare l&#39;elenco degli strumenti e gli schemi, che il LLM potrà quindi utilizzare.

## Applicazioni MCP supportate {#supported-mcp-applications}

I server MCP di AEM sono progettati per funzionare con un set definito di applicazioni compatibili con MCP. Sono supportate le seguenti applicazioni:

* Claude antropico
* Cursore
* OpenAI ChatGPT
* Microsoft Copilot Studio

Ogni applicazione fornisce la propria esperienza di configurazione, ma i passaggi di alto livello sono simili.

## Panoramica dell’installazione {#setup-overview}

La configurazione di MCP per AEM prevede tre parti principali:

1. **Configurazione una tantum in AEM da parte di un amministratore**, che consente a specifiche applicazioni client MCP di accedere ai server MCP di AEM
1. **Configurazione in ogni applicazione client MCP** in modo che l&#39;applicazione sappia come connettersi ai server MCP di AEM ed eseguire l&#39;accesso OAuth
1. **Selezionare il server MCP** prima di avviare la richiesta, in modo che il client MCP possa utilizzarlo.

### Configurazione AEM {#aem-configuration}

Per impostazione predefinita, l’accesso ai server MCP di AEM è disciplinato dalle autorizzazioni di cui dispongono i singoli utenti in AEM. Quando un utente si autentica tramite un’applicazione client MCP, gli strumenti MCP applicano le stesse regole di accesso delle operazioni manuali in AEM. Un utente può eseguire solo azioni che è già autorizzato a eseguire.

#### Applicazioni client MCP consentite {#permitted-mcp-client-applications}

Le seguenti applicazioni client MCP sono consentite per impostazione predefinita:

* ChatGPT
* Claude
* MS Copilot Studio
* Cursore

#### Limitazione dei server MCP {#restricting-mcp-servers}

Tutti i server MCP vengono inseriti nell&#39;elenco Consentiti per impostazione predefinita. In qualità di amministratore, puoi limitare l’accesso a server MCP specifici a livello di organizzazione, programma o ambiente. Questo offre un controllo granulare sulle funzionalità MCP disponibili per gli utenti all’interno della tua organizzazione.

#### Gestione dell’accesso client MCP {#managing-mcp-client-access}

Gli amministratori possono inoltre disabilitare l&#39;accesso per specifiche applicazioni client MCP, se richiesto dai criteri dell&#39;organizzazione. Se desideri che Adobe abiliti il supporto per altri prodotti client MCP, invia un collegamento al sito web del prodotto. Se hai bisogno di inserire nell&#39;elenco Consentiti un client MCP personalizzato, contatta anche tu.

Per tutte le richieste relative al server MCP, contattaci all&#39;indirizzo **aemcs-mcp-feedback@adobe.com**

### Configurazione applicazione client MCP {#mcp-client-application-configuration}

Questo passaggio viene eseguito da ogni utente (o da un amministratore dell’applicazione client MCP, se supportato). I dettagli di configurazione variano leggermente da un’applicazione all’altra. I client MCP si stanno evolvendo rapidamente e il supporto per i server MCP remoti è in fase di sviluppo attivo. Potrebbe essere necessario abilitare la modalità Sviluppatore per accedere alle funzionalità per l’aggiunta di server remoti, ma il processo generale è il seguente:

1. Aggiungi gli URL del server AEM MCP
   * Configura gli endpoint MCP dalla tabella precedente. Esempio:`https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly`
1. Attiva la connessione
   * Salva o attiva la configurazione in modo che l’applicazione client MCP tenti di connettersi al server MCP di AEM
1. Accedi con Adobe ID
   * Quando richiesto, completa il flusso di accesso di Adobe in modo che l’applicazione possa ottenere token OAuth associati al tuo Adobe ID
1. Verificare gli strumenti individuati
   * Una volta autenticata, l’applicazione rileva gli strumenti MCP dal server. È quindi possibile iniziare a richiedere al LLM di eseguire le operazioni di AEM.

Di seguito sono riportati alcuni esempi di come si presenta questo in ciascuna applicazione supportata a un livello elevato.

**ChatGPT**

![Configura passaggio 1](assets/chatgpt-1.png) di ChatGPT

![Configura passaggio 2](assets/chatgpt-2.png) di ChatGPT

![Configura passaggio 3](assets/chatgpt-3.png) di ChatGPT

![Configura passaggio 4](assets/chatgpt-4.png) di ChatGPT

![Configura passaggio 5](assets/chatgpt-5.png) di ChatGPT

![Configurare il passaggio 6](assets/chatgpt-6.png) di ChatGPT

![Configura passaggio 7](assets/chatgpt-7.png) di ChatGPT

* Aggiungi gli URL del server AEM MCP nell’area in cui sono configurati le connessioni o gli strumenti MCP
* Attiva la connessione e accedi con il tuo Adobe ID quando viene reindirizzato
* In una chat, fai riferimento agli strumenti di AEM configurati nelle tue richieste, ad esempio:

  *&quot;Utilizzando gli strumenti AEM MCP configurati, elenca tutti i siti nel nostro ambiente di authoring.&quot;*

**Claude**

![Configura Claude Passaggio 1](assets/claude-1.png)

![Configura il passaggio Claude 2](assets/claude-2.png)

![Configura il passaggio Claude 3](assets/claude-3.png)

![Configura Claude Passaggio 4](assets/claude-4.png)

![Configura Claude Passaggio 5](assets/claude-5.png)

![Configura Claude Passaggio 6](assets/claude-6.png)

![Configura Claude Passaggio 7](assets/claude-7.png)

* Nella configurazione MCP di Claude, registra gli URL del server MCP di AEM
* Completare il flusso di accesso di Adobe
* Se necessario, abilita la conferma automatica per alcuni strumenti nell’area di configurazione. Questa opzione è consigliata per le operazioni di ricerca o di sola lettura.
* Accertati che il server MCP sia selezionato prima di avviare la conversazione
* Chiedi a Claude di eseguire le attività relative ad AEM; Claude selezionerà gli strumenti AEM esposti dal server MCP in base al tuo prompt.

**Cursore**

![Configura passaggio cursore 1](assets/cursor-1.png)

![Configura passaggio cursore 2](assets/cursor-2.png)

![Configura passaggio cursore 3](assets/cursor-3.png)

![Configura passaggio cursore 4](assets/cursor-4.png)

![Configura passaggio cursore 5](assets/cursor-5.png)

* Nelle impostazioni MCP del cursore, crea una nuova voce del server MCP con gli URL MCP di AEM
* Autentica con il tuo Adobe ID quando richiesto
* Se necessario, attivate o disattivate i singoli strumenti facendo clic sui relativi nomi. Tutti gli strumenti sono attivati per impostazione predefinita.
* Utilizza l’editor o la chat del cursore per richiamare gli strumenti di AEM come parte dei flussi di lavoro di sviluppo o di contenuti.

**Microsoft Copilot Studio**

![Configura il passaggio Copilot 1](assets/copilot-1.png)

![Configura il passaggio Copilot 2](assets/copilot-2.png)

![Configura il passaggio Copilot 3](assets/copilot-3.png)

![Configura il passaggio Copilot 4](assets/copilot-4.png)

![Configura il passaggio Copilot 5](assets/copilot-5.png)

![Configura il passaggio Copilot 6](assets/copilot-6.png)

![Configura Passaggio Copilot 7](assets/copilot-7.png)

![Configura Copilot Passaggio 8](assets/copilot-8.png)

![Configura Copilot Passaggio 9](assets/copilot-9.png)

![Configura il passaggio Copilot 10](assets/copilot-10.png)

* Crea un nuovo agente
* Passare alla sezione dello strumento e fare clic su **Aggiungi strumento**
* Seleziona uno strumento esistente o creane uno nuovo
* Configura un nuovo strumento MCP che punta agli URL del server AEM MCP
* Stabilisci una connessione, che può essere condivisa o dedicata tra agenti
* Accedi con il tuo Adobe ID quando viene reindirizzato
* È possibile attivare la modalità di conferma automatica o richiedere conferma all&#39;utente finale per tutte le interazioni dello strumento
* Durante il test dell&#39;agente, aprire prima la gestione connessione per assegnare una connessione alla sessione, quindi premere **Riprova**.

## Autenticazione {#authentication}

I server MCP ospitati da Adobe implementano OAuth e sono integrati con il sistema di identità di Adobe.

* Quando un&#39;applicazione client MCP si connette a un server AEM MCP, gli utenti visualizzano una finestra di dialogo di accesso di Adobe e si autenticano con il proprio **Adobe ID**
* Dopo aver effettuato correttamente l&#39;accesso, il sistema verifica che l&#39;applicazione client MCP sia consentita nell&#39;organizzazione e che il server MCP richiesto sia consentito. Se uno dei due controlli non riesce, viene visualizzato un messaggio di errore.

![Errore client MCP non consentito](assets/MCP-Client-not-permitted.png)

* Una volta verificata, il server MCP rilascia i token utilizzati dall’applicazione per le successive chiamate allo strumento
* Gli strumenti MCP rispettano le autorizzazioni AEM dell’utente. Un utente che non dispone dell’autorizzazione per modificare un frammento di contenuto in AEM non potrà modificarlo tramite MCP.

In questo modo le operazioni assistite da IA sono conformi al modello di sicurezza e governance di AEM esistente.

## Utilizzo di MCP con AEM {#using-mcp-with-aem}

Una volta configurate le applicazioni client AEM e MCP, puoi lavorare nell’applicazione desiderata e richiedere al LLM di eseguire le operazioni di AEM. Il LLM legge gli schemi degli strumenti MCP, sceglie gli strumenti da chiamare e li sequenzia in base alle esigenze per soddisfare la richiesta.

>[!IMPORTANT]
>
>Per ottenere risultati ottimali, in particolare con prompt che contengono più passaggi o che eseguono il targeting di diversi tipi di contenuto come immagini e testo, abilita un modello di pensiero o seleziona l’opzione Pensiero nel client MCP anziché affidarsi alla modalità Automatica.

### Esempi di casi d’uso {#example-usecases}

Alcuni scenari rappresentativi includono:

* **Individuazione ambiente**
   * Elencare ambienti e licenze per decidere dove eseguire un flusso di lavoro.

* **Gestione siti**
   * Elenca siti
   * Crea, leggi, aggiorna ed elimina pagine e contenuto della pagina.

* **Gestione frammenti di contenuto**
   * Cercare frammenti di contenuto
   * Creare nuovi frammenti
   * Aggiorna i frammenti esistenti quando cambia la messaggistica della campagna.

* **Gestione Assets**
   * Importare risorse
   * Trovare risorse esistenti
   * Pubblicare le risorse.

### Esempio di flussi di lavoro {#example-workflows}

Gli esempi seguenti illustrano il modo in cui un LLM potrebbe concatenare gli strumenti MCP.

1. **Utilizzo di un frammento di contenuto a cui fa riferimento una pagina**
   * **Ottieni contenuto pagina**. Chiamare uno strumento come `get-aem-page-content` per recuperare la pagina e individuare la proprietà `fragmentPath`.
   * **Risolvere il percorso del frammento**. Utilizzare `resolve_fragment_path` per convertire il percorso in un UUID.
   * **Recupera i dati del frammento**. Chiamare `get_fragment` per recuperare i campi correnti.
   * **Aggiorna il frammento**. Chiamare `patch_fragment` per applicare le modifiche al contenuto del frammento.
1. **Creazione di nuovi contenuti basati su un modello**
   * **Rileva modelli**. Utilizzare `list_models` per vedere quali modelli per frammenti di contenuto sono disponibili.
   * **Ispeziona un modello**. Utilizzare `get_model` per comprendere lo schema di campi del modello.
   * **Crea contenuto**. Utilizzare `create_fragment` per creare un nuovo frammento con valori derivati dalla richiesta.
1. **Aggiornamento sicuro del contenuto esistente**
   * **Leggi dati correnti** - Utilizza `get_fragment` per recuperare i dati esistenti e un ETag.
   * **Applica una patch JSON**. Utilizzare `patch_fragment` con il documento ETag e una patch JSON per aggiornare il frammento, supportando la concorrenza ottimistica.

Dal punto di vista dell’utente, questi flussi di lavoro possono essere avviati con prompt quali:

*&quot;Crea un nuovo frammento di contenuto per la campagna primaverile basato sul nostro modello di banner principale e compila i relativi campi da questa descrizione.&quot;*

Il LLM sceglie e coordina automaticamente gli strumenti MCP necessari.

## Gestione delle aspettative {#expectation-management}

Quando si lavora con LLM tramite MCP, tenere presente quanto segue:

* **Funzionalità elevata ma non infallibile**
I moduli LLM possono eseguire attività complesse, ma sono soggetti a errori occasionali. Lo stesso prompt può produrre risultati o presentazioni leggermente diversi senza un motivo evidente. Esamina sempre gli output prima di applicare modifiche al contenuto di produzione.

* **Funzionalità in evoluzione**
I modelli LLM sono in continuo miglioramento. Nel tempo, diventano più intelligenti nel scoprire nuovi modi per combinare gli strumenti MCP per raggiungere i tuoi obiettivi. Un’attività che richiedeva l’invio di più richieste oggi può funzionare senza problemi con un singolo prompt domani.

* **La supervisione umana è essenziale**
Pensa al LLM come a un assistente esperto che ha bisogno di supervisione. Possiede un&#39;ampia conoscenza e può ideare soluzioni creative, ma trae vantaggio dalla tua guida e revisione. Verifica i risultati, in particolare per le operazioni critiche, e fornisci un feedback quando l’output non corrisponde alle tue aspettative.

* **Prestare attenzione alle esecuzioni dello strumento di riconoscimento automatico**
Alcune applicazioni client MCP, come Claude, offrono la possibilità di riconoscere automaticamente le esecuzioni dello strumento richieste da LLM. Anche se può essere utile per operazioni di sola lettura, come la ricerca o il recupero del contenuto, è necessario prestare attenzione con gli strumenti che aggiornano o eliminano il contenuto. Rivedi ogni richiesta di esecuzione dello strumento prima di confermare le azioni che modificano il tuo ambiente AEM.

## Limitazioni {#limitations}

I server MCP di AEM sono attualmente destinati ad essere configurati in ChatGPT, Claude, Cursor e Microsoft Copilot Studio.

Se desideri utilizzare un&#39;applicazione client MCP diversa, contatta il numero **aemcs-mcp-feedback@adobe.com** per richiedere supporto per altri client o per inserire nell&#39;elenco Consentiti uno personalizzato.
