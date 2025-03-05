---
title: Proteggere il Forms con reCAPTCHA - Guida visiva
description: Scopri come aggiungere facilmente Google reCAPTCHA ai moduli Edge Delivery Services per evitare invii di spam e bot
feature: Edge Delivery Services
keywords: reCAPTCHA nei moduli, Utilizzo di reCAPTCHA nell’editor universale, Aggiunta di reCAPTCHA nei moduli, sicurezza dei moduli, protezione da posta indesiderata
role: Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 1%

---


# Proteggere il Forms dallo spam con Google reCAPTCHA

<span class="preview"> Questa funzionalità è disponibile tramite il programma di accesso anticipato. Per richiedere l&#39;accesso, invia un&#39;e-mail dal tuo indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> con il nome dell&#39;organizzazione GitHub e il nome dell&#39;archivio.</span>



## Perché utilizzare reCAPTCHA nei moduli?

| ![Sicurezza](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![Protezione bot](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![Esperienza utente](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **Sicurezza avanzata** | **Prevenzione di bot e spam** | **Esperienza utente perfetta** |
| Proteggere i moduli da attività fraudolente e attacchi dannosi | Impedire che i bot automatizzati inondino i moduli con contenuti irrilevanti o dannosi | L&#39;invisibile reCAPTCHA funziona dietro le quinte senza interrompere gli utenti legittimi |

Ad esempio, un modulo per il calcolo delle imposte con informazioni finanziarie riservate deve essere protetto da eventuali abusi. reCAPTCHA verifica che le richieste provengano da utenti autentici, non da sistemi automatizzati.

## Scegli la tua soluzione reCAPTCHA

Edge Delivery Services Forms supporta due opzioni Google reCAPTCHA:

| ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/enterprise.svg) | ![reCAPTCHA Standard](/help/edge/docs/forms/universal-editor/assets/standard.svg) |
|:-------------:|:-------------:|
| [**reCAPTCHA Enterprise**](#set-up-recaptcha-enterprise) | [**reCAPTCHA Standard**](#set-up-recaptcha-standard) |
| Rilevamento di frodi di livello enterprise Premium con funzioni aggiuntive e personalizzazione | Servizio gratuito con rilevamento basato su punteggio che opera in modo invisibile in background |
| Ideale per: organizzazioni di grandi dimensioni con esigenze di sicurezza complesse | Ideale per: progetti di piccole e medie dimensioni con esigenze di protezione di base |

Entrambe le opzioni utilizzano il rilevamento basato sul punteggio (da 0,0 a 1,0) per identificare le interazioni uomo-bot senza interrompere l’esperienza utente.

## Configurazione di reCAPTCHA Enterprise

### Passaggio 1: ottenere le credenziali di Google Cloud

Prima di configurare reCAPTCHA Enterprise, è necessario:

- Un [progetto Google Cloud](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) con [ID progetto](https://support.google.com/googleapi/answer/7014113)
- [API Enterprise CAPTCHA abilitata](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api) per il progetto
- Una [chiave API](https://console.cloud.google.com/apis/credentials) per l&#39;autenticazione
- [chiave del sito](https://console.cloud.google.com/security/recaptcha) per il dominio

### Passaggio 2: creare un contenitore di configurazione cloud

![Configurazione della configurazione cloud dettagliata](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. Accedi all’istanza di authoring di AEM
2. Passa a **Strumenti** > **Generale** > **Browser configurazioni**
3. Trova il modulo e seleziona **Proprietà**
4. Abilita **Configurazioni cloud** nella finestra di dialogo
5. Salvare e pubblicare la configurazione

### Passaggio 3: configurare il servizio enterprise reCAPTCHA

![schermata di configurazione Enterprise CAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. Vai a **Strumenti** > **Servizi cloud** > **reCAPTCHA**
2. Passa al modulo e fai clic su **Crea**
3. Nella finestra di dialogo:
   - Seleziona la versione **ReCAPTCHA Enterprise**
   - Inserisci un titolo e un nome
   - Aggiungi l&#39;ID progetto, la chiave del sito e la chiave API
   - Seleziona **Chiave sito basata su punteggio** come tipo di chiave
   - Imposta un punteggio di soglia (0-1) per distinguere gli esseri umani dai bot
4. Fai clic su **Crea** e pubblica la configurazione

## Configurazione dello standard reCAPTCHA

### Passaggio 1: ottenere le chiavi API

Prima di iniziare, [ottieni una coppia di chiavi API reCAPTCHA](https://www.google.com/recaptcha/admin) (chiave del sito e chiave segreta) dalla console reCAPTCHA di Google.

>[!IMPORTANT]
>
>I moduli di Edge Delivery Services supportano solo la versione **reCAPTCHA basata su punteggio**.

### Passaggio 2: creare un contenitore di configurazione cloud

Segui gli stessi passaggi della versione Enterprise per creare e pubblicare un contenitore di configurazione cloud.

### Passaggio 3: configurare il servizio standard reCAPTCHA

![schermata di configurazione standard di reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. Vai a **Strumenti** > **Servizi cloud** > **reCAPTCHA**
2. Passa al modulo e fai clic su **Crea**
3. Nella finestra di dialogo:
   - Seleziona la versione **ReCAPTCHA v2**
   - Inserisci un titolo e un nome
   - Aggiungi chiave sito e chiave segreta
4. Fai clic su **Crea** e pubblica la configurazione

## Aggiungere reCAPTCHA al modulo

Dopo aver configurato reCAPTCHA, è ora di aggiungerlo al modulo:

![Aggiunta del componente reCAPTCHA a un modulo](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

1. Aprire il modulo in Universal Editor
2. Passa alla sezione Modulo adattivo nella struttura del contenuto
3. Fai clic sull&#39;icona **Aggiungi** e seleziona **Captcha (invisibile)** dall&#39;elenco dei componenti del modulo adattivo
   - *In alternativa, trascinare e rilasciare il componente nel modulo*
4. Fai clic su **Pubblica** per aggiornare il modulo con la protezione reCAPTCHA

Il modulo è ora protetto. Visualizza in:
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name>`

![Modulo con protezione reCAPTCHA abilitata](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## Convalida dell’integrazione reCAPTCHA

Dopo aver aggiunto reCAPTCHA al modulo, è essenziale verificarne il corretto funzionamento. Ecco come convalidare l’implementazione:

### Verifica visiva

Mentre reCAPTCHA v2 (basato su punteggio) funziona in modo invisibile, puoi confermarne la presenza:

1. **Controllare l&#39;origine della pagina**: fare clic con il pulsante destro del mouse sulla pagina del modulo e selezionare &quot;Visualizza Source pagina&quot;
   - Cerca l’inclusione dello script reCAPTCHA con la chiave del sito
   - Esempio: `<script src="https://www.google.com/recaptcha/api.js?render=YOUR_SITE_KEY"></script>`

2. **Controlla richieste di rete**: utilizzo degli strumenti di sviluppo del browser (F12)
   - Invia il modulo e cerca le richieste di rete a `google.com/recaptcha`
   - Queste richieste indicano che reCAPTCHA è attivo nel modulo

### Test funzionale

Per verificare che reCAPTCHA protegga effettivamente il modulo:

1. **Test invio normale**:
   - Compila il modulo con dati validi
   - Inviare il modulo a un ritmo normale
   - Verifica invio modulo completato

2. **Test del comportamento di tipo bot**:
   - Apri il modulo in una finestra di navigazione privata/in incognito
   - Compila il modulo molto rapidamente (comportamento automatizzato)
   - Invia più volte in rapida successione
   - Se reCAPTCHA funziona, questi invii potrebbero essere bloccati o contrassegnati

3. **Verifica record invio modulo**:
   - Rivedere i dati di invio del modulo
   - Ogni invio deve includere un punteggio reCAPTCHA
   - I punteggi più vicini a 1.0 indicano possibili utenti umani
   - I punteggi più vicini a 0,0 indicano una potenziale attività da bot

### Utilizzo di Google reCAPTCHA Admin Console

Per gli utenti Enterprise, la console Google Cloud fornisce analisi dettagliate:

1. Passa alla [console Google Cloud](https://console.cloud.google.com/)
2. Passa a **Sicurezza** > **reCAPTCHA**
3. Seleziona la chiave del sito
4. Esaminare i grafici e le statistiche di valutazione
5. Cerca:
   - Traffic pattern
   - Distribuzioni punteggio
   - Attività potenzialmente fraudolente

Per gli utenti reCAPTCHA standard, le statistiche di base sono disponibili in [reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin/).

### Regolazione dell’implementazione

In base ai risultati della convalida:

- Se gli utenti legittimi sono bloccati, è consigliabile ridurre il punteggio di soglia
- Se ricevi ancora spam, prendi in considerazione di aumentare il punteggio di soglia
- Per problemi persistenti, controlla la configurazione reCAPTCHA e assicurati che tutte le chiavi siano immesse correttamente

Ricorda che reCAPTCHA utilizza l’apprendimento automatico per migliorare nel tempo, pertanto la sua efficacia potrebbe aumentare man mano che apprende i pattern di traffico del sito.

## Risoluzione dei problemi e domande frequenti

| ![Domanda](/help/edge/docs/forms/universal-editor/assets/question.svg) | ![Risposta](/help/edge/docs/forms/universal-editor/assets/answer.svg) |
|:-------------:|:-------------:|
| **Cosa succede se non si crea una configurazione reCAPTCHA?** | Il sistema cercherà una configurazione nel Contenitore globale. Se non ne esiste nessuno, verrà visualizzato un errore. |
| **Cosa succede se creo più configurazioni?** | Il sistema utilizza automaticamente la prima configurazione creata. |
| **Perché le mie modifiche non sono visibili nell&#39;URL pubblicato?** | Assicurati di ripubblicare il modulo dopo aver apportato modifiche. |
| **Quali servizi reCAPTCHA sono supportati?** | Edge Delivery Services Forms supporta solo i servizi reCAPTCHA basati su punteggio. |

## Passaggi successivi

Ora che hai protetto il modulo con reCAPTCHA:

- **Convalida l&#39;implementazione**: segui i [passaggi di convalida](#-validating-your-recaptcha-integration) per assicurarti che reCAPTCHA funzioni correttamente
- **Monitoraggio delle prestazioni**: controlla regolarmente il dashboard di Google reCAPTCHA per individuare attività sospette e distribuzioni di punteggio
- **Impostazioni ottimizzate**: regola il punteggio di soglia in base alle tue esigenze di sicurezza e al feedback sull&#39;esperienza utente
- **Rimani aggiornato**: assicurati che l&#39;implementazione di reCAPTCHA sia sempre aggiornata con gli ultimi consigli di sicurezza di Google
- **Formazione del team**: condividi informazioni sul funzionamento di reCAPTCHA e su come interpretare le analisi
- **Raccogli feedback**: monitora l&#39;esperienza utente per evitare che utenti legittimi vengano bloccati

Tenere presente che la protezione efficace dei moduli è un processo continuo che richiede un monitoraggio e adeguamenti regolari.


