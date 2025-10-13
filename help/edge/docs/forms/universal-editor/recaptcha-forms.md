---
title: Aggiungere Google reCAPTCHA ai moduli nell’editor universale
description: Guida all’implementazione della protezione Google reCAPTCHA nei moduli Edge Delivery Services per prevenire spam e attacchi automatizzati
feature: Edge Delivery Services
keywords: reCAPTCHA nei moduli, Utilizzo di reCAPTCHA nell’editor universale, Aggiunta di reCAPTCHA nei moduli, sicurezza dei moduli, protezione da spam
role: Developer, Admin
level: Intermediate
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: ht
source-wordcount: '1281'
ht-degree: 100%

---


# Aggiungere Google reCAPTCHA ai moduli nell’editor universale

Google reCAPTCHA aiuta a proteggere i moduli distinguendo tra utenti umani e bot automatizzati. Questa guida spiega come implementare sia la versione Enterprise che la versione Standard di reCAPTCHA nell’editor universale.

**Obiettivi:**

- Selezionare la soluzione reCAPTCHA appropriata
- Configurare reCAPTCHA Enterprise o Standard
- Aggiungere reCAPTCHA ai moduli
- Convalidare e testare l’implementazione
- Monitorare e ottimizzare le prestazioni

## Prerequisiti

Prima di iniziare, assicurati di disporre dei seguenti prerequisiti:

### Requisiti di accesso

- Accesso all’authoring di AEM as a Cloud Service
- Accesso all’editor universale con autorizzazioni di modifica dei moduli

### Requisiti tecnici

- Account Google attivo
- Per Enterprise: progetto Google Cloud Platform con fatturazione abilitata
- Per Standard: account Google reCAPTCHA
- Verifica della proprietà del dominio per i moduli

### Requisiti di conoscenza

- Informazioni di base su AEM Forms e l’editor universale
- Familiarità con le configurazioni del servizio cloud
- Informazioni sui concetti di sicurezza dei moduli

## Perché utilizzare reCAPTCHA nei moduli?

| ![Sicurezza](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![Protezione da bot](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![Esperienza utente](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **Sicurezza avanzata** | **Prevenzione di bot e spam** | **Esperienza utente perfetta** |
| Proteggere i moduli da attività fraudolente e attacchi | Impedire ai bot automatizzati l’invio dei moduli | reCAPTCHA invisibile non disturba gli utenti legittimi |

**Concetto chiave:** reCAPTCHA utilizza il machine learning per analizzare il comportamento dell’utente e assegna un punteggio (da 0,0 a 1,0) che indica la probabilità di interazione umana. Punteggi più alti indicano che si tratta di utenti umani; punteggi più bassi suggeriscono la presenza di bot.

**Esempio:** un modulo per il calcolo fiscale che gestisce dati sensibili richiede la protezione da attacchi automatici. reCAPTCHA verifica che gli invii provengano da utenti reali, non da bot.

## Scelta della soluzione reCAPTCHA

I moduli Edge Delivery Services supportano due opzioni Google reCAPTCHA. Utilizza i seguenti criteri per selezionare la soluzione giusta:

### Guida rapida alle decisioni

**Utilizza reCAPTCHA Enterprise se disponi di:**

- Moduli a traffico elevato (>10.000 richieste/mese)
- Requisiti rigorosi di conformità (GDPR, SOX, HIPAA)
- Necessità di analisi avanzate e reporting
- Budget per le funzioni di sicurezza Premium
- Implementazioni complesse su più domini

**Quando utilizzare reCAPTCHA Standard:**

- Traffico da basso a moderato (&lt;10.000 richieste/mese)
- Requisiti di sicurezza di base
- Budget limitato (livello gratuito)
- Configurazione semplice per dominio singolo
- Nessuna esperienza pregressa nell’uso di reCAPTCHA

### Confronto dettagliato

| **Funzione** | **reCAPTCHA Enterprise** | **reCAPTCHA Standard** |
|-------------|--------------------------|------------------------|
| **Costo** | A pagamento (prezzo in base all’utilizzo) | Gratuito |
| **Limite di richieste** | Illimitate | 1 milione di richieste al mese |
| **Analisi avanzate** | Reporting dettagliato | Solo statistiche di base |
| **Regole personalizzate** | Regole specifiche per l’account | Solo regole globali |
| **Supporto di più domini** | Gestione avanzata | Supporto di base |
| **SLA** | Garanzia di tempo di operatività al 99,9% | Tentativo migliore |
| **Assistenza** | Assistenza Enterprise | Assistenza community |
| **Conformità** | Livello Enterprise | Conformità standard |

**Entrambe le soluzioni forniscono:**

- Rilevamento basato su punteggio (scala da 0,0 a 1,0)
- Funzionamento invisibile (non è richiesta alcuna interazione da parte dell’utente)
- Rilevamento di bot basato sull’apprendimento automatico
- Valutazione del rischio in tempo reale

## Configurare reCAPTCHA Enterprise


+++ Passaggio 1: preparare l’ambiente Google Cloud

**Requisiti:**

1. Progetto Google Cloud con fatturazione abilitata
2. ID progetto (dalla dashboard GCP)
3. Verifica del dominio per i moduli
4. Accesso amministratore a GCP e AEM

**Configurazione:**

1. Crea o seleziona un progetto Google Cloud.
   - Passa alla [console di Google Cloud](https://console.cloud.google.com/).
   - Crea un nuovo progetto o selezionane uno esistente.
   - Prendi nota dell’ID del progetto.

2. Abilita API reCAPTCHA Enterprise.
   - Passa a API e servizi > Libreria.
   - Cerca “API reCAPTCHA Enterprise”.
   - Fai clic su Abilita.

3. Crea le credenziali API.
   - Passa a API e servizi > Credenziali.
   - Fai clic su Crea credenziali > Chiave API.
   - Copia e memorizza la chiave API.

4. Crea la chiave del sito.
   - Passa a Sicurezza > reCAPTCHA Enterprise.
   - Fai clic su Crea chiave.
   - Scegli il tipo di chiave basato su punteggio.
   - Aggiungi i tuoi domini.
   - Imposta il punteggio di soglia (consigliato: 0,5).

**Checkpoint di convalida:** assicurati di disporre di:

- ID progetto
- Chiave API
- Chiave sistema
- Dominio verificato in Google Cloud

+++

+++ Passaggio 2: configurare un contenitore della configurazione cloud AEM

![Configurazione della configurazione cloud dettagliata](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)
*Figura: abilitazione delle configurazioni cloud per il contenitore di moduli*

**Configurazione:**

1. Accedi al browser di configurazione
   - Accedi all’istanza di authoring di AEM.
   - Passare a Strumenti > Generale > Browser di configurazione

2. Abilitare configurazioni cloud
   - Individuare il contenitore di configurazione del modulo
   - Selezionare le proprietà
   - Controllare le configurazioni cloud
   - Fare clic su Salva e chiudi

3. Verifica la configurazione.
   - Confermare che “Configurazioni cloud” sia visualizzato nelle proprietà del contenitore

**Punto di controllo di convalida:**

- Configurazioni cloud abilitate per il contenitore
- Il contenitore viene visualizzato nel browser di configurazione
- Le proprietà mostrano “Configurazioni cloud” come abilitato

+++

+++ Passaggio 3: configurare il servizio reCAPTCHA Enterprise in AEM

![Schermata di configurazione Enterprise CAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)
*Figura: interfaccia di configurazione reCAPTCHA Enterprise in AEM*

**Configurazione:**

1. Accedere alla configurazione reCAPTCHA
   - Passa a Strumenti > Servizi cloud > reCAPTCHA.
   - Seleziona il contenitore di configurazione del modulo.
   - Fai clic su Crea.

2. Configurare le impostazioni Enterprise
   - Titolo: nome descrittivo (ad esempio, “Produzione reCAPTCHA”)
   - Nome: nome del sistema (generato automaticamente o personalizzato)
   - Versione: seleziona ReCAPTCHA Enterprise
   - ID progetto: immetti l’ID del progetto Google Cloud
   - Chiave del sito: immetti la chiave del sito da Google Cloud
   - Chiave API: immetti la chiave API di Google Cloud
   - Tipo di chiave: seleziona la chiave del sito basata sul punteggio

3. Imposta la soglia di sicurezza
   - Punteggio della soglia: imposta tra 0,0 e 1,0
   - Valori consigliati:
      - 0,7-0,9: sicurezza alta (può bloccare alcuni utenti legittimi)
      - 0,5-0,7: sicurezza bilanciata (consigliata)
      - 0,1-0,5: sicurezza ridotta (consente a più utenti)

4. Salva e pubblica
   - Fai clic su Crea per salvare la configurazione
   - Fai clic su Pubblica per renderla disponibile

**Punto di controllo per la convalida:**

- Configurazione salvata correttamente
- Tutti i campi obbligatori completati
- Configurazione pubblicata e visibile
- Nessun messaggio di errore

+++

## Configurare reCAPTCHA Standard

+++Passaggio 1: ottenere le chiavi API reCAPTCHA (consulta i dettagli)

>[!IMPORTANT]
>
> I moduli Edge Delivery Services supportano solo reCAPTCHA v2 (basato sul punteggio). Non utilizzare la versione della casella di controllo.

**Generazione della chiave:**

1. Accedi alla console Google reCAPTCHA

   - Pass all’[Admin Console di Google reCAPTCHA](https://www.google.com/recaptcha/admin)
   - Accedi con il tuo account Google

2. Crea un nuovo sito

   - Fai clic su + per aggiungere un nuovo sito
   - Etichetta: inserisci un nome descrittivo
   - Tipo di reCAPTCHA: seleziona reCAPTCHA v2 > “Non sono un robot” invisibile
   - Domini: aggiungi i domini del modulo
   - Accetta i termini e fai clic su Invia

3. Raccogli le chiavi

   - Chiave del sito: copia la chiave del sito (chiave pubblica)
   - Chiave segreta: copia la chiave segreta (chiave privata)

**Punto di controllo per la convalida:**

- Sito creato nella console reCAPTCHA

- Chiave del sito ottenuta

- Chiave segreta ottenuta

- Domini aggiunti e verificati

+++

+++Passaggio 2: configura il contenitore della configurazione di AEM Cloud (consulta i dettagli)

Segui lo stesso processo della configurazione Enterprise:

1. Abilita le configurazioni cloud nel browser di configurazione

2. Verifica la configurazione del contenitore

3. Le impostazioni di conferma vengono salvate

+++

+++Passaggio 3: configurare il servizio standard reCAPTCHA in AEM (consulta i dettagli)

![schermata di configurazione standard di reCAPTCHA](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)
*Figura: interfaccia di configurazione di reCAPTCHA Standard in AEM*

**Configurazione:**

1. Accedere alla configurazione reCAPTCHA

   - Passa a Strumenti > Servizi cloud > reCAPTCHA.
   - Seleziona il contenitore di configurazione del modulo.
   - Fai clic su Crea.

2. Configura le impostazioni Standard.

   - Titolo: nome descrittivo (ad esempio, “reCAPTCHA standard”)
   - Nome: nome del sistema (generato automaticamente o personalizzato)
   - Versione: seleziona reCAPTCHA v2.
   - Chiave sito: immetti la chiave del sito Google reCAPTCHA.
   - Chiave segreta: immetti la chiave segreta Google reCAPTCHA.

3. Salva e pubblica

   - Fai clic su Crea per salvare la configurazione
   - Fai clic su Pubblica per renderla disponibile

**Punto di controllo di convalida:**

- Configurazione creata senza errori

- Entrambe le chiavi immesse correttamente

- Configurazione pubblicata correttamente

- Configurazione visualizzata nell’elenco

+++

## Aggiungere reCAPTCHA a un modulo

Dopo aver configurato il servizio reCAPTCHA, aggiungi la protezione al modulo come segue:

![Aggiunta del componente reCAPTCHA a un modulo](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)
*Figura: aggiunta del componente Captcha invisibile al modulo*

+++&#x200B;1. Aprire il modulo nell’editor universale
Passa al modulo in AEM Sites e fai clic su Modifica per aprirlo nell’editor universale. Attendi il caricamento dell’editor.

- Passa al modulo in AEM Sites.
- Fai clic su Modifica per aprirlo nell’editor universale.
- Attendi il caricamento dell’editor
+++

+++&#x200B;2. Individuare la struttura del modulo
Nella struttura del contenuto (pannello a sinistra), individua la sezione Modulo adattivo ed espandi la struttura del modulo per visualizzare i punti di inserimento.

- Nella struttura del contenuto (pannello a sinistra), individua la sezione Modulo adattivo.
- Espandi la struttura del modulo per visualizzare i punti di inserimento.
+++

+++&#x200B;3. Aggiungere il componente reCAPTCHA
Aggiungi al modulo il componente captcha (invisibile).

- Fai clic sull’icona Aggiungi (+) nella sezione del modulo.
- Dall’elenco dei componenti, seleziona Captcha (invisibile).
- In alternativa, trascina il componente dal pannello Componenti.
+++

+++&#x200B;4. Configurare il componente (facoltativo)
Seleziona il componente captcha appena aggiunto e verifica che utilizzi la configurazione reCAPTCHA che hai creato.

- Seleziona il componente Captcha appena aggiunto.
- Nel pannello Proprietà, verifica che utilizzi la configurazione reCAPTCHA precedentemente salvata.
- Non è necessaria alcuna configurazione aggiuntiva per la configurazione di base.
+++

+++&#x200B;5. Pubblicare le modifiche apportate
Pubblica le modifiche e verifica che non vi siano errori.

- Fai clic su Pubblica nell’editor universale.
- Attendi la conferma.
- Verifica che non vengano visualizzati errori.
+++

### Verificare l’implementazione

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
