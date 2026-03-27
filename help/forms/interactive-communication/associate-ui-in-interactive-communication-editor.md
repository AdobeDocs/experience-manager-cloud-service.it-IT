---
title: Associate UI in Interactive Communication Editor
description: Scopri l’interfaccia utente associata nell’Editor di comunicazione interattiva consentendo agli agenti che si rivolgono al cliente di generare comunicazioni personalizzate e conformi.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Si applica ad AEM Forms)."
exl-id: 9ba58659-b14c-4ebc-a6d9-e56a4b6aa48b
source-git-commit: f889498f9ee5e71a4d3695dbfbe194d1bbb11488
workflow-type: tm+mt
source-wordcount: '639'
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

Progetta e gestisce la comunicazione interattiva e la configura per l’interfaccia utente associata (compresa l’abilitazione di Visualizzazione associata e del flusso di lavoro opzionale).

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
> Gli associati devono far parte del gruppo **forms-associates**. Per gli autori che inviano anche dall&#39;interfaccia utente Associate nell&#39;istanza Autore, aggiungili anche a **utenti-flusso di lavoro**.

## Casi d’uso dinamici

L’interfaccia utente Associate supporta la generazione immediata e personalizzata di documenti, fondamentale per i settori con esigenze di manutenzione in tempo reale.

| Settore | Casi d’uso di esempio |
|----------|-------------------|
| **Servizi finanziari** | Genera lettere di conferma del prestito in tempo reale, riepiloghi del profilo di rischio e creazione di conti. |
| **Assicurazione** | Produrre immediatamente schede Proof-of-Insurance o riepiloghi di smaltimento richieste di risarcimento. |
| **Assistenza sanitaria** | Creare riepiloghi del piano di trattamento del paziente con copay e programmi calcolati. |
| **Settore pubblico** | Generare sul posto report di verifica della polizia, ricevute di assistenza da parte dei cittadini, lettere di riscontro e riepiloghi degli aggiornamenti dei casi. |
| **Pubblica amministrazione** | Creare riepiloghi sullo stato delle applicazioni, lettere di approvazione del servizio e comunicazioni in tempo reale per le iscrizioni al programma di welfare. |

## Abilitazione dell’interfaccia utente Associa

Gli autori abilitano l&#39;interfaccia utente Associa e, facoltativamente, configurano un flusso di lavoro per gli invii nelle **impostazioni di comunicazione interattiva**:

1. **Abilita visualizzazione associata**. In **Associa proprietà**, selezionare **Abilita modifica visualizzazione associata**, quindi fare clic su **Applica modifiche** e salvare il documento.
2. **Configura flusso di lavoro (facoltativo)** — In **Flusso di lavoro**, attivare **Configura flusso di lavoro per aggiornamento**, selezionare un modello di flusso di lavoro e, facoltativamente, impostare un messaggio di successo e un URL di reindirizzamento.
3. **Configura campi modificabili** - Abilita i campi che gli associati possono modificare e impostare le convalide.
4. **Pubblica e condividi** — pubblica il componente di interoperabilità e condividi il collegamento con gli associati.

Per istruzioni dettagliate sulle schermate e sul comportamento di invio/flusso di lavoro (creazione e associazione durante la pubblicazione), vedi [Abilitare e configurare l&#39;interfaccia utente di associazione per le comunicazioni interattive](/help/forms/interactive-communication/enable-configure-associate-ui.md). Per generare un flusso di lavoro che generi PDF da invii IC, vedere [Flusso di lavoro di invio per l&#39;interfaccia utente associata - output PDF generato da IC](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md).

L&#39;**interfaccia utente associata** colma il divario tra l&#39;authoring di contenuti strutturati e il coinvolgimento dei clienti in tempo reale.\
Grazie alla combinazione di design intuitivo, configurazione back-end affidabile e severi controlli di conformità, le organizzazioni possono fornire **comunicazioni veloci, precise e personalizzate** su larga scala.

## Consulta anche

- [Abilitare e configurare l’interfaccia utente di Associa per le comunicazioni interattive](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [Integrare l’interfaccia utente di Associa nell’applicazione](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Flusso di lavoro di invio per l&#39;interfaccia utente associata - IC Genera output PDF](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md)
