---
title: Utilizzo di MCP con AEM as a Cloud Service
description: Scopri come utilizzare Model Context Protocol con AEM as a Cloud Service
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: ddb7fc8c-affc-4374-8e08-d45d96017109
source-git-commit: d4b216294791958c29a4cca736bc041a7bf4ad0c
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 0%

---

# Utilizzo di MCP con AEM as a Cloud Service {#using-mcp-with-aem-as-a-cloud-service}

## Introduzione {#introduction}

Molti team di Adobe Experience Manager (AEM) ora lavorano in ambienti di sviluppo integrato (IDE) e applicazioni basate su chat come Cursor, OpenAI ChatGPT, Anthropic Claude e Microsoft Copilot Studio. Queste applicazioni supportano il protocollo MCP (Model Context Protocol), che consente alle applicazioni di esporre gli strumenti back-end a modelli LLM (Large Language Model) in modo standardizzato.

Con l’integrazione MCP di AEM, utenti tipo diversi possono collaborare intorno allo stesso contenuto:

* **Gli sviluppatori** possono orchestrare operazioni e flussi di lavoro per contenuti dalla loro applicazione IDE o chat
* **I professionisti** e gli architetti di contenuti possono gestire siti e frammenti di contenuto e importare risorse con l&#39;assistenza dell&#39;intelligenza artificiale, pur mantenendo il modello di autorizzazione esistente di AEM.

>[!IMPORTANT]
>
> Per gli scenari che modificano o eliminano il contenuto, i professionisti devono utilizzare l’interfaccia di AI Assistant anziché richiamare direttamente gli strumenti MCP. Gli agenti AEM gestiti dall’Assistente AI includono protezioni integrate.
>

Questo articolo spiega cosa fornisce la funzionalità MCP di AEM, quali applicazioni MCP sono supportate, come configurarla e come utilizzarla nella pratica.

## Perché MCP è utile per i clienti AEM {#why-mcp-is-useful-for-aem-customers}

Le moderne applicazioni IDE e chat utilizzano MCP come metodo per consentire a un LLM di richiamare gli strumenti esposti dietro i server MCP. I clienti possono descrivere il proprio intento nel linguaggio naturale anziché scrivere codice in base a specifiche API di basso livello. Ad esempio, un prompt come *&quot;aggiorna il banner principale per questa campagna in tutte le pagine&quot;* consente al LLM di richiamare gli strumenti MCP appropriati, che quindi interagiscono con le API di AEM.

I vantaggi principali includono:

* **Interazione con linguaggio naturale anziché API plumbing**
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
|---|---|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Contenuto** | `/content` | Operazioni per contenuti quali creazione, lettura, aggiornamento ed eliminazione (CRUD) per pagine e frammenti di contenuto, importazione di risorse e ricerca di risorse.                                                                          <br>Invia un&#39;e-mail a aemagentsteam@adobe.com per attivare la **ricerca risorse**. Includi il nome dell’organizzazione e il caso d’uso nell’e-mail. |
| **Contenuto (sola lettura)** | `/content-readonly` | Operazioni per contenuti di sola lettura (Get, List/Search) per pagine e frammenti di contenuto, oltre alla ricerca di risorse.                                                                             <br>Invia un&#39;e-mail a aemagentsteam@adobe.com per attivare la **ricerca risorse**. Includi il nome dell’organizzazione e il caso d’uso nell’e-mail. |
| **Cloud Manager** | `/cloudmanager` | Gestisci le entità Cloud Manager, inclusi programmi, ambienti, archivi e pipeline, che possono anche essere attivati. |
| **Governance delle esperienze** | `/experience-governance` | Valuta i contenuti (testo, immagini, pagine) in base alle regole di governance del brand ed elenca configurazioni e controlli del brand.<br/>I clienti devono iscriversi alla versione di prova di [agenti o disporre di una licenza a pagamento](https://experienceleague.adobe.com/it/docs/experience-cloud-ai/experience-cloud-ai/agents/trial?lang=en) per accedere a Experience Governance MCP. |

Gli strumenti specifici esposti da ciascun server MCP possono evolvere nel tempo. In pratica, puoi chiedere all’applicazione abilitata per MCP di individuare gli strumenti tramite un prompt come:

```
"List all AEM MCP tools available from this server and describe what they do."
```

Il client MCP utilizza il protocollo MCP per recuperare l&#39;elenco degli strumenti e gli schemi, che il LLM può quindi utilizzare.

Per ulteriori informazioni sulle funzionalità e su come utilizzarle, fare riferimento all&#39;[esercitazione sul server MCP di contenuti](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/ai/mcp-servers/accelerate-content-operations-with-aem-mcp-server) e al [video sul server MCP di Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/ai/mcp-servers/cloud-manager).

## Applicazioni MCP supportate {#supported-mcp-applications}

I server MCP di AEM sono progettati per funzionare con un set definito di applicazioni compatibili con MCP. Ogni applicazione fornisce la propria esperienza di configurazione, ma i passaggi di alto livello sono simili.

### Applicazioni chat (Web e desktop) {#chat-applications}

* Claude antropico
* OpenAI ChatGPT

### Strumenti per sviluppatori (estensioni IDE, app desktop, CLI) {#developer-tools}

* Codice Claude antropico (CLI, JetBrains, codice VS, cursore)
* Codice incremento (CLI, JetBrains, codice VS, cursore)
* App desktop con rientro aggiuntivo
* Cline (JetBrains, codice VS, cursore)
* Cursore
* Copilota GitHub (JetBrains, codice VS)
* Kiro (app desktop, CLI)
* Codice OpenAI (app desktop)
* OpenAI Codex CLI
* Windsurf

### Piattaforme aziendali {#enterprise-platforms}

* Microsoft Copilot Studio

## Panoramica dell’installazione {#setup-overview}

La configurazione di MCP per AEM prevede due parti principali:

1. **Configurazione in ogni applicazione client MCP** in modo che l&#39;applicazione sappia come connettersi ai server MCP di AEM ed eseguire l&#39;accesso OAuth
1. **Selezionare il server MCP** prima di avviare la richiesta, in modo che il client MCP possa utilizzarlo.

Sono disponibili guide dettagliate relative a entrambi i passaggi per:

* [Claude antropico](/help/ai-in-aem/mcp-support/setup-claude.md)
* [OpenAI ChatGPT](/help/ai-in-aem/mcp-support/setup-chatgpt.md)
* [Cursore](/help/ai-in-aem/mcp-support/setup-cursor.md)
* [JetBrains con copilota GitHub](/help/ai-in-aem/mcp-support/setup-jetbrains-copilot.md)
* [Microsoft Copilot Studio](/help/ai-in-aem/mcp-support/setup-microsoft-copilot-studio.md)

### Configurazione AEM {#aem-configuration}

Per impostazione predefinita, le autorizzazioni di cui dispongono i singoli utenti all’interno di AEM regolano l’accesso ai server MCP di AEM. Quando un utente si autentica tramite un’applicazione client MCP, gli strumenti MCP applicano le stesse regole di accesso delle operazioni manuali in AEM. Un utente può eseguire solo azioni che è già autorizzato a eseguire.

#### Applicazioni client MCP consentite {#permitted-mcp-client-applications}

Tutte le applicazioni elencate in [Applicazioni MCP supportate](#supported-mcp-applications) sono consentite per impostazione predefinita.

#### Limitazione dei server MCP {#restricting-mcp-servers}

Tutti i server MCP vengono inseriti nell&#39;elenco Consentiti per impostazione predefinita. In qualità di amministratore, puoi limitare l’accesso a server MCP specifici a livello di organizzazione, programma o ambiente. Questa restrizione offre un controllo granulare sulle funzionalità MCP disponibili per gli utenti all’interno dell’organizzazione.

#### Gestione dell’accesso client MCP {#managing-mcp-client-access}

Gli amministratori possono inoltre disabilitare l&#39;accesso per specifiche applicazioni client MCP, se richiesto dai criteri dell&#39;organizzazione. Se desideri che Adobe abiliti il supporto per altri prodotti client MCP, invia un collegamento al sito web del prodotto. Se hai bisogno di inserire nell&#39;elenco Consentiti un client MCP personalizzato, contatta anche tu.

Per tutte le richieste relative al server MCP, contattaci all&#39;indirizzo **aemcs-mcp-feedback@adobe.com**

### Configurazione applicazione client MCP {#mcp-client-application-configuration}

Ogni utente esegue questo passaggio oppure un amministratore dell&#39;applicazione client MCP può eseguirlo laddove supportato. I dettagli di configurazione variano leggermente da un’applicazione all’altra. I client MCP si stanno evolvendo rapidamente e il supporto per i server MCP remoti è in fase di sviluppo attivo. Potrebbe essere necessario abilitare la modalità Sviluppatore per accedere alle funzionalità per l’aggiunta di server remoti, ma il processo generale è il seguente:

1. Aggiungi uno o più URL del server AEM MCP
   * Configura uno o più endpoint MCP dalla tabella precedente. Esempio:`https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly`
1. Attiva la connessione
   * Salva o attiva la configurazione in modo che l’applicazione client MCP tenti di connettersi al server MCP di AEM
1. Accedi con Adobe ID
   * Quando richiesto, completa il flusso di accesso di Adobe in modo che l’applicazione possa ottenere token OAuth associati al tuo Adobe ID
1. Verificare gli strumenti individuati
   * Una volta autenticata, l’applicazione rileva gli strumenti MCP dal server. È quindi possibile iniziare a richiedere al LLM di eseguire le operazioni di AEM.

Per l&#39;elenco completo delle applicazioni supportate, vedere [Applicazioni MCP supportate](#supported-mcp-applications).

## Autenticazione {#authentication}

I server MCP ospitati da Adobe implementano OAuth e sono integrati con il sistema di identità di Adobe.

* Quando un&#39;applicazione client MCP si connette a un server AEM MCP, gli utenti visualizzano una finestra di dialogo di accesso di Adobe e si autenticano con il proprio **Adobe ID**
* Dopo aver effettuato correttamente l&#39;accesso, il sistema verifica che l&#39;applicazione client MCP sia consentita nell&#39;organizzazione e che il server MCP richiesto sia consentito. Se uno dei due controlli non riesce, viene visualizzato un messaggio di errore.

![Errore client MCP non consentito](assets/MCP-Client-not-permitted.png)

* Una volta verificata, il server MCP rilascia i token utilizzati dall’applicazione per le successive chiamate allo strumento
* Gli strumenti MCP rispettano le autorizzazioni AEM dell’utente. Solo gli utenti che dispongono dell’autorizzazione per modificare un frammento di contenuto in AEM possono modificarlo tramite MCP.

Questo approccio garantisce che le operazioni assistite da IA siano conformi al modello di sicurezza e governance di AEM esistente.

## Utilizzo di MCP con AEM {#using-mcp-with-aem}

Una volta configurate le applicazioni client AEM e MCP, puoi lavorare nell’applicazione desiderata e richiedere al LLM di eseguire le operazioni di AEM. Il LLM legge gli schemi degli strumenti MCP, sceglie gli strumenti da chiamare e li sequenzia in base alle esigenze per soddisfare la richiesta.

>[!IMPORTANT]
>
>I prompt contenenti più passaggi o destinati a diversi tipi di contenuto, ad esempio immagini e testo, funzionano al meglio con un modello pensante. Abilita un modello di pensiero o seleziona l’opzione Pensiero nel client MCP invece di fare affidamento sulla modalità Automatica.

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

* **Importazione risorse**
   * Importa risorse con controllo stato

* **Ricerca Assets**

  >[!NOTE]
  >
  >Invia un’e-mail a aemagentsteam@adobe.com per abilitare la ricerca delle risorse. Includi il nome dell’organizzazione e il caso d’uso nell’e-mail.

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

```
"Create a new content fragment for the spring campaign based on our hero banner model and fill in its fields from this brief."
```

Il LLM sceglie e coordina automaticamente gli strumenti MCP necessari.

## Gestione delle aspettative {#expectation-management}

Quando si lavora con LLM tramite MCP, tenere presente quanto segue:

* **Funzionalità elevata ma non infallibile**
I moduli LLM possono eseguire attività complesse, ma sono soggetti a errori occasionali. Lo stesso prompt può produrre risultati o presentazioni leggermente diversi senza un motivo evidente. Esamina sempre gli output prima di applicare modifiche al contenuto di produzione.

* **Funzionalità in evoluzione**
I modelli LLM sono in continuo miglioramento. Nel tempo, diventano più intelligenti nel scoprire nuovi modi per combinare gli strumenti MCP per raggiungere i tuoi obiettivi. Un’attività che richiedeva l’invio di più richieste oggi può funzionare senza problemi con un singolo prompt domani.

* **La supervisione umana è essenziale:**
Pensa al LLM come a un assistente esperto che ha bisogno di supervisione. Possiede un&#39;ampia conoscenza e può ideare soluzioni creative, ma trae vantaggio dalla tua guida e revisione. Verifica i risultati, in particolare per le operazioni critiche, e fornisci un feedback quando l’output non corrisponde alle tue aspettative.

* **Prestare attenzione alle esecuzioni dello strumento di riconoscimento automatico**
Alcune applicazioni client MCP, come Claude, offrono la possibilità di riconoscere automaticamente le esecuzioni dello strumento richieste da LLM. Anche se questa opzione può essere utile per operazioni di sola lettura, come la ricerca o il recupero del contenuto, occorre prestare attenzione con gli strumenti che aggiornano o eliminano il contenuto. Rivedi ogni richiesta di esecuzione dello strumento prima di confermare le azioni che modificano il tuo ambiente AEM.

## Limitazioni {#limitations}

AEM attualmente supporta la configurazione dei server MCP nelle applicazioni elencate in [Applicazioni MCP supportate](#supported-mcp-applications).

Se desideri utilizzare un&#39;applicazione client MCP diversa, contatta il numero **aemcs-mcp-feedback@adobe.com** per richiedere supporto per altri client o per inserire nell&#39;elenco Consentiti uno personalizzato.
