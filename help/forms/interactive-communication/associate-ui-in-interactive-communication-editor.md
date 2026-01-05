---
title: Associate UI in Interactive Communication Editor
description: Scopri l’interfaccia utente associata nell’Editor di comunicazione interattiva consentendo agli agenti che si rivolgono al cliente di generare comunicazioni personalizzate e conformi.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 234b6dc747bbba21e9249d526bf894860572dfe5
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 3%

---


# Associate UI in Interactive Communication Editor

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

L&#39;**interfaccia utente associata** è un&#39;interfaccia specializzata e semplificata basata sull&#39;editor di comunicazioni interattive (IC). È progettato per i professionisti che si rivolgono ai clienti, come gli associati sul campo e gli agenti di servizio, per generare comunicazioni personalizzate, conformi e accurate in tempo reale durante le interazioni live.

![Trova documento IC](/help/forms/interactive-communication/assets/associate-ui-preview.png)

## Associa interfaccia utente

L’interfaccia utente Associa fornisce un’area di lavoro pulita a due pannelli che consente una generazione di comunicazioni rapida e sicura:

### Pannello sinistro: immissione dati

- Gli associati inseriscono o confermano le informazioni specifiche del cliente.
- Le convalide, i testi di supporto e i campi obbligatori guidano l’immissione accurata.

### Pannello a destra: anteprima in tempo reale

- Visualizza un&#39;anteprima istantanea del documento finale.
- Aggiorna automaticamente quando l&#39;associato inserisce i dati.

### Generazione immediata di documenti

- Genera o scarica la comunicazione finalizzata.

## Persone e responsabilità utente

L’interfaccia utente Associa è guidata da tre ruoli principali, ciascuno con responsabilità distinte:

### &#x200B;1. Amministratore

Responsabile della configurazione del sistema, della governance, delle integrazioni back-end e dell’accesso degli utenti.

| Responsabilità | Stato attivo |
|---------------|-------|
| Configurazione del sistema | Imposta l’infrastruttura di base, i gruppi di utenti, i modelli di dati dei moduli (FDM) e l’output. |
| Governance e sicurezza | Gestisce le autorizzazioni utente e garantisce la conformità del sistema. |
| Gestione dell’integrazione | Gestisce le integrazioni back-end e le connessioni live dei dati dei clienti. |

### &#x200B;2. Autore

Progetta e gestisce la comunicazione interattiva utilizzando l’interfaccia utente Associa. ß

| Responsabilità | Stato attivo |
|---------------|-------|
| Authoring e progettazione IC | Crea layout, branding e struttura di documento conforme. |
| Configurazione campo | Esegue la mappatura dei campi dati, definisce i campi Modificabili, Obbligatori e di sola lettura. |
| Pubblicazione e abilitazione | Pubblica l&#39;IC e condivide il collegamento per l&#39;accesso associato. |

### &#x200B;3. Associa

Utilizza l’interfaccia utente Associa per assistere i clienti, aggiornare le informazioni e generare comunicazioni conformi.


| Responsabilità | Stato attivo |
|---------------|-------|
| Conferma dei dati | Riempie o convalida i dati dei clienti tramite il pannello di immissione a sinistra. |
| Anteprima e convalida | Assicura la precisione utilizzando il pannello di anteprima in tempo reale. |
| Distribuzione | Genera il PDF/e-mail e lo invia tramite canali approvati. |

>[!NOTE]
>
> Associa deve far parte del gruppo **forms-associates**.

## Casi d’uso dinamici

L’interfaccia utente Associate supporta la generazione immediata e personalizzata di documenti, fondamentale per i settori con esigenze di manutenzione in tempo reale.

| Settore | Casi d’uso di esempio |
|----------|-------------------|
| **Servizi finanziari** | Genera lettere di conferma del prestito in tempo reale, riepiloghi del profilo di rischio e creazione di conti. |
| **Assicurazione** | Produrre immediatamente schede Proof-of-Insurance o riepiloghi di smaltimento richieste di risarcimento. |
| **Assistenza sanitaria** | Creare riepiloghi del piano di trattamento del paziente con copay e programmi calcolati. |
| **Settore pubblico** | Generare sul posto report di verifica della polizia, ricevute di assistenza da parte dei cittadini, lettere di riscontro e riepiloghi degli aggiornamenti dei casi. |
| **Pubblica amministrazione** | Creare riepiloghi sullo stato delle applicazioni, lettere di approvazione del servizio e comunicazioni in tempo reale per le iscrizioni al programma di welfare. |

## Abilitazione dell’associazione del flusso di lavoro dell’interfaccia utente

L’autore può seguire i passaggi seguenti per configurare e pubblicare una comunicazione interattiva (IC) per l’accesso all’interfaccia utente di Associate:

>[!NOTE]
>
> Componenti supportati per l’associazione: Campo data, Campo numerico, Campo testo, Campo data/ora, Campo data, Casella di controllo, Pulsante di scelta, Elenco a discesa.

### Creare il componente di interoperabilità

Progetta e configura la comunicazione interattiva, garantendo che branding, associazioni di dati, regole di conformità e integrazioni siano impostati correttamente.

### Abilita l’interfaccia utente Associa

Dalla barra delle azioni superiore, abilita l’opzione Associa interfaccia utente per rendere il componente di interoperabilità disponibile per i driver associati.

### Abilitare l’interfaccia utente Associa nel componente

### Configura campi modificabili

Nella sezione campi obbligatori, abilita i campi che gli associati possono modificare.
Imposta le convalide per garantire l’immissione accurata e controllata dei dati.

### Pubblica IC

Dopo aver finalizzato tutte le configurazioni, pubblica la comunicazione interattiva per un accesso sicuro.

### Condividi IC pubblicato con associati

Fornisci il collegamento IC pubblicato all’associato, consentendo loro di autenticare, immettere informazioni specifiche per il cliente e generare la comunicazione finale con input validi.

L&#39;**interfaccia utente associata** colma il divario tra l&#39;authoring di contenuti strutturati e il coinvolgimento dei clienti in tempo reale.\
Grazie alla combinazione di design intuitivo, configurazione back-end affidabile e severi controlli di conformità, le organizzazioni possono fornire **comunicazioni veloci, precise e personalizzate** su larga scala.
