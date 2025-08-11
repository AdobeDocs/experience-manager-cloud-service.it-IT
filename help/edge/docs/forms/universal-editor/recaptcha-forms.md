---
title: Aggiungere Google reCAPTCHA a Forms in Universal Editor
description: Guida all’implementazione della protezione Google reCAPTCHA nei Edge Delivery Services Form per prevenire spam e attacchi automatizzati
feature: Edge Delivery Services
keywords: reCAPTCHA nei moduli, Utilizzo di reCAPTCHA nell’editor universale, Aggiunta di reCAPTCHA nei moduli, sicurezza dei moduli, protezione da spam
role: Developer, Admin
level: Intermediate
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 4%

---


# Aggiungere Google reCAPTCHA a Forms in Universal Editor

Google reCAPTCHA aiuta a proteggere i moduli distinguendo tra utenti umani e bot automatizzati. Questa guida spiega come implementare sia la versione Enterprise che la versione Standard di reCAPTCHA in Universal Editor.

**Obiettivi:**

- Seleziona la soluzione reCAPTCHA appropriata
- Configurare reCAPTCHA Enterprise o Standard
- Aggiungere reCAPTCHA ai moduli
- Convalidare e testare l’implementazione
- Monitorare e ottimizzare le prestazioni

## Prerequisiti

Prima di iniziare, assicurati di disporre dei seguenti elementi:

### Requisiti di accesso

- Accesso all’authoring di AEM as a Cloud Service
- Accesso all’editor universale con autorizzazioni di modifica dei moduli
- Iscrizione al programma di accesso anticipato per le funzioni reCAPTCHA

### Requisiti tecnici

- Account Google attivo
- Per Enterprise: progetto Google Cloud Platform con fatturazione abilitata
- Per Standard: account Google reCAPTCHA
- Verifica della proprietà del dominio per i moduli

### Requisiti di conoscenza

- Nozioni di base su AEM Forms e Universal Editor
- Familiarità con le configurazioni del servizio cloud
- Informazioni sui concetti di protezione dei moduli

## Perché utilizzare reCAPTCHA nel Forms?

| ![Sicurezza](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![Protezione da bot](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![Esperienza utente](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **Sicurezza avanzata** | **Prevenzione di bot e spam** | **Esperienza utente perfetta** |
| Proteggere i moduli da attività e attacchi fraudolenti | Impedisci l&#39;invio automatico di moduli da parte di bot | Il reCAPTCHA invisibile non danneggia gli utenti legittimi |

**Concetto chiave:** reCAPTCHA utilizza l&#39;apprendimento automatico per analizzare il comportamento dell&#39;utente e assegna un punteggio (da 0,0 a 1,0) che indica la probabilità di interazione umana. Punteggi più alti indicano gli utenti umani; punteggi più bassi suggeriscono i bot.

**Esempio:** Un modulo di calcolo fiscale che gestisce dati sensibili richiede la protezione da attacchi automatici. reCAPTCHA verifica che le richieste provengano da utenti reali, non da bot.

## Scegli la tua soluzione reCAPTCHA

Edge Delivery Services Forms supporta due opzioni Google reCAPTCHA. Utilizza i seguenti criteri per selezionare la soluzione giusta:

### Guida rapida alle decisioni

**Utilizzare reCAPTCHA Enterprise se si dispone di:**

- Moduli a traffico elevato (>10.000 richieste/mese)
- Requisiti di conformità rigidi (RGPD, SOX, HIPAA)
- Necessità di analisi avanzate e reporting
- Budget per le funzionalità di sicurezza Premium
- Distribuzioni complesse su più domini

**Utilizzare reCAPTCHA Standard se si dispone di:**

- Traffico da basso a moderato (&lt;10.000 richieste/mese)
- Requisiti di sicurezza di base
- Budget limitato (livello gratuito)
- Configurazione semplice a dominio singolo
- Novità di reCAPTCHA

### Confronto dettagliato

| **Funzionalità** | **reCAPTCHA Enterprise** | **reCAPTCHA Standard** |
|-------------|--------------------------|------------------------|
| **Costo** | Pagato (prezzo basato sull&#39;utilizzo) | Gratuito |
| **Limite richieste** | Senza limiti | 1 milione di richieste al mese |
| **Analisi avanzata** | Reporting dettagliato | Solo statistiche di base |
| **Regole personalizzate** | Regole specifiche per l’account | Solo regole globali |
| **Supporto di più domini** | Gestione avanzata | Supporto di base |
| **SLA** | Garanzia di uptime al 99,9% | Massima efficienza |
| **Supporto** | Supporto Enterprise | Sostegno comunitario |
| **Conformità** | Di livello Enterprise | Conformità standard |

**Entrambe le soluzioni forniscono:**

- Rilevamento basato su punteggio (scala da 0,0 a 1,0)
- Funzionamento invisibile (non è richiesta alcuna interazione da parte dell’utente)
- Rilevamento di bot basato sull’apprendimento automatico
- Valutazione del rischio in tempo reale

## Configurare reCAPTCHA Enterprise


+++ Passaggio 1: preparare l’ambiente Google Cloud

**Requisiti:**

1. Progetto Google Cloud con fatturazione abilitata
2. ID progetto (dal dashboard GCP)
3. Verifica del dominio per i moduli
4. Accesso amministratore a GCP e AEM

**Configurazione:**

1. Crea o seleziona un progetto Google Cloud
   - Vai a [Console Google Cloud](https://console.cloud.google.com/)
   - Crea un nuovo progetto o selezionane uno esistente
   - Prendi nota dell&#39;ID progetto

2. Abilita API reCAPTCHA Enterprise
   - Vai a API e servizi > Libreria
   - Cerca &quot;reCAPTCHA Enterprise API&quot;
   - Fai clic su Abilita

3. Creare le credenziali API
   - Vai a API e servizi > Credenziali
   - Fai clic su Crea credenziali > Chiave API.
   - Copiare e memorizzare la chiave API

4. Crea chiave sito
   - Vai a Sicurezza > reCAPTCHA Enterprise
   - Fai clic su Crea chiave
   - Scegli il tipo di chiave basato su punteggio
   - Aggiungi i tuoi domini
   - Imposta il punteggio di soglia (consigliato: 0,5)

**Checkpoint di convalida:** Verifica di disporre di:

- ID progetto
- Chiave API
- Chiave sistema
- Dominio verificato in Google Cloud

+++

+++ Passaggio 2: configurare il contenitore di configurazione cloud di AEM

![Configurazione della configurazione cloud dettagliata](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)
*Figura: abilitazione delle configurazioni cloud per il contenitore di moduli*

**Configurazione:**

1. Accedi al browser configurazioni
   - Accedere all’istanza di authoring AEM
   - Vai a Strumenti > Generale > Browser configurazioni

2. Abilita configurazioni cloud
   - Individuare il contenitore di configurazione del modulo
   - Seleziona proprietà
   - Verifica configurazioni cloud
   - Fai clic su Salva e chiudi

3. Verificare la configurazione
   - Conferma che &quot;Configurazioni cloud&quot; sia visualizzato nelle proprietà del contenitore

**Checkpoint di convalida:**

- Configurazioni cloud abilitate per il contenitore
- Il contenitore viene visualizzato nel browser configurazioni
- Le proprietà mostrano &quot;Configurazioni cloud&quot; come abilitato

+++

+++ Passaggio 3: configurare il servizio enterprise reCAPTCHA in AEM

![schermata di configurazione Enterprise CAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)
*Figura: interfaccia di configurazione Enterprise reCAPTCHA in AEM*

**Configurazione:**

1. Accedi alla configurazione reCAPTCHA
   - Vai a Strumenti > Cloud Services > reCAPTCHA
   - Seleziona il contenitore di configurazione del modulo
   - Fai clic su Crea.

2. Configurare le impostazioni Enterprise
   - Titolo: nome descrittivo (ad esempio, &quot;Production reCAPTCHA&quot;)
   - Nome: nome del sistema (generato automaticamente o personalizzato)
   - Versione: seleziona ReCAPTCHA Enterprise
   - ID progetto: immetti l&#39;ID del progetto Google Cloud
   - Chiave sito: immetti la chiave del sito da Google Cloud
   - Chiave API: immetti la chiave API di Google Cloud
   - Tipo di chiave: seleziona la chiave del sito basata su punteggio

3. Imposta soglia di protezione
   - Punteggio soglia: impostato tra 0,0 e 1,0
   - Valori consigliati:
      - 0.7-0.9: Elevata sicurezza (può bloccare alcuni utenti legittimi)
      - 0.5-0.7: Sicurezza bilanciata (consigliata)
      - 0.1-0.5: Protezione inferiore (per consentire più utenti)

4. Salva e pubblica
   - Fai clic su Crea per salvare la configurazione
   - Fai clic su Pubblica per renderlo disponibile

**Checkpoint di convalida:**

- Configurazione salvata correttamente
- Tutti i campi obbligatori completati
- Configurazione pubblicata e visibile
- Nessun messaggio di errore

+++

## Configurare reCAPTCHA Standard

+++Passaggio 1: ottenere le chiavi API reCAPTCHA (consulta i dettagli)

>[!IMPORTANT]
>
> Edge Delivery Services Forms supporta solo reCAPTCHA v2 (basato su punteggio). Non utilizzare la versione della casella di controllo.

**Generazione chiave:**

1. Accedere alla console Google reCAPTCHA

   - Vai a [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin)
   - Accedi con il tuo account Google

2. Crea nuovo sito

   - Fai clic su + per aggiungere un nuovo sito
   - Etichetta: inserisci un nome descrittivo
   - reCAPTCHA Tipo: selezionare reCAPTCHA v2 > &quot;I&#39;m not a robot&quot; Invisibile
   - Domini: aggiungi i domini del modulo
   - Accetta i termini e fai clic su Invia

3. Raccogli Le Tue Chiavi

   - Chiave sito: copia la chiave del sito (chiave pubblica)
   - Chiave segreta: copia la chiave privata

**Checkpoint di convalida:**

- Sito creato nella console reCAPTCHA

- Chiave sito ottenuta

- Chiave segreta ottenuta

- Domini aggiunti e verificati

+++

+++Passaggio 2: configurare il contenitore della configurazione cloud di AEM (consulta i dettagli)

Seguire lo stesso processo della configurazione Enterprise:

1. Abilitare le configurazioni cloud nel browser configurazioni

2. Verifica la configurazione del contenitore

3. Le impostazioni di conferma vengono salvate

+++

+++Passaggio 3: configurare il servizio standard reCAPTCHA in AEM (consulta i dettagli)

![schermata di configurazione standard di reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)
*Figura: interfaccia di configurazione di reCAPTCHA Standard in AEM*

**Configurazione:**

1. Accedi alla configurazione reCAPTCHA

   - Vai a Strumenti > Cloud Services > reCAPTCHA
   - Seleziona il contenitore di configurazione del modulo
   - Fai clic su Crea.

2. Configura impostazioni standard

   - Titolo: nome descrittivo (ad esempio, &quot;Standard reCAPTCHA&quot;)
   - Nome: nome del sistema (generato automaticamente o personalizzato)
   - Versione: Seleziona ReCAPTCHA v2
   - Chiave sito: immetti la chiave del sito Google reCAPTCHA
   - Chiave segreta: immetti la chiave segreta Google reCAPTCHA

3. Salva e pubblica

   - Fai clic su Crea per salvare la configurazione
   - Fai clic su Pubblica per renderlo disponibile

**Checkpoint di convalida:**

- Configurazione creata senza errori

- Entrambe le chiavi immesse correttamente

- Configurazione pubblicata correttamente

- La configurazione viene visualizzata nell&#39;elenco

+++

## Aggiungere reCAPTCHA al modulo

Dopo aver configurato il servizio reCAPTCHA, aggiungi la protezione al modulo come segue:

![Aggiunta del componente reCAPTCHA a un modulo](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)
*Figura: aggiunta del componente Captcha invisibile al modulo*

+++1 Apri modulo nell’editor universale
Vai al modulo in AEM Sites e fai clic su Modifica per aprirlo in Universal Editor. Attendi il caricamento dell’editor.

- Vai al modulo in AEM Sites
- Fai clic su Modifica per aprire in Editor universale
- Attendere il caricamento dell’editor
+++

+++2 Individuare la struttura del modulo
Nella struttura del contenuto (pannello a sinistra), individua la sezione Modulo adattivo ed espandi la struttura del modulo per visualizzare i punti di inserimento.

- Nella struttura del contenuto (pannello a sinistra), individua la sezione Modulo adattivo
- Espandere la struttura del modulo per visualizzare i punti di inserimento
+++

+++3 Aggiungi componente reCAPTCHA
Aggiungi il componente Captcha (invisibile) al modulo.

- Fai clic sull’icona Aggiungi (+) nella sezione del modulo
- Dall’elenco dei componenti, seleziona Captcha (invisibile)
- In alternativa, trascina e rilascia il componente dal pannello Componenti
+++

+++4 Configura componente (facoltativo)
Seleziona il componente captcha appena aggiunto e verifica che utilizzi la configurazione reCAPTCHA.

- Seleziona il componente captcha appena aggiunto
- Nel pannello Proprietà, verificate che utilizzi la configurazione reCAPTCHA
- Non è necessaria alcuna configurazione aggiuntiva per la configurazione di base
+++

+++5 Pubblicare Le Modifiche
Pubblica le modifiche e verifica che non siano presenti errori.

- Fai clic su Pubblica nell’editor universale
- Attendi conferma
- Verifica che non vengano visualizzati errori
+++

### Verifica implementazione

Il modulo protetto è ora disponibile all’indirizzo:

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/
<form-name>
```

**URL di esempio:**

```
https://main--my-forms--company.aem.live/content/forms/af/
contact-us-form
```
