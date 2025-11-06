---
title: Invio e integrazione di moduli
description: Scopri come configurare l’invio dei moduli e integrare i moduli di Forms Experience Builder con sistemi esterni, API e flussi di lavoro aziendali.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: c772556b-dab6-4fa8-b728-1fe52c6596a4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 0%

---

# Invio e integrazione di moduli

>[!NOTE]
>
> Forms Experience Builder è disponibile in un programma di accesso anticipato. Prima di iniziare, assicurati di aver richiesto e ottenuto l’accesso.

Forms Experience Builder fornisce potenti funzionalità di integrazione per collegare i moduli con sistemi esterni, API e flussi di lavoro aziendali. Questa guida illustra come configurare l’invio di moduli e impostare vari scenari di integrazione.

## Opzioni di configurazione dell’invio

### Invii e-mail

Configura i moduli per inviare gli invii tramite e-mail:

**Configurazione e-mail di base:**

- Impostare gli indirizzi e-mail dei destinatari
- Configurare i modelli e-mail
- Aggiungere destinatari CC e CCN
- Configurare le notifiche e-mail

**Funzioni e-mail avanzate:**

- Selezione dinamica dei destinatari
- Modelli e-mail con dati modulo
- Gestione degli allegati
- Conferma della consegna e-mail

### Integrazione REST API

Connettere i moduli alle API e ai servizi esterni:

**Configurazione endpoint API:**

- Impostare gli URL REST API
- Configurare i metodi di autenticazione
- Impostare intestazioni e parametri di richiesta
- Gestire i dati di risposta

**Mappatura dati:**

- Mappare i campi del modulo ai parametri API
- Trasformare i formati dei dati
- Gestire le strutture JSON nidificate
- Gestire le risposte di errore

### Integrazione dell’archiviazione cloud

Archivia gli invii di moduli nei servizi di archiviazione cloud:

**Piattaforme supportate:**

- Archiviazione BLOB di Microsoft Azure
- Amazon S3
- Archiviazione cloud Google
- SharePoint Online

**Opzioni di configurazione:**

- Imposta credenziali archiviazione
- Configurare le strutture di cartelle
- Imposta convenzioni di denominazione file
- Gestire le autorizzazioni di accesso

### Integrazione dei flussi di lavoro

Collegare i moduli ai flussi di lavoro dei processi aziendali:

**Microsoft Power Automate:**

- Attivare i flussi di lavoro all’invio del modulo
- Trasmettere i dati del modulo ai passaggi del flusso di lavoro
- Gestire le risposte del flusso di lavoro
- Gestire i processi di approvazione

**Flusso di lavoro Adobe:**

- Integrare con il flusso di lavoro AEM
- Configurare le catene di approvazione
- Configurare i passaggi di notifica
- Gestire l’elaborazione dei documenti

## Impostazione dell’invio di moduli

### Passaggio 1: accedere alla configurazione dell’invio

1. Aprire il modulo in Forms Experience Builder
2. Passare alle impostazioni di invio
3. Seleziona &quot;Configura invio modulo&quot;
4. Scegli il tipo di integrazione

### Passaggio 2: configurare gli invii e-mail

**Configurazione e-mail di base:**

    Configura l&#39;invio e-mail a hr@company.com con:
    - Oggetto: &quot;Nuova applicazione dipendente&quot;
    - Includi dati modulo nel corpo dell&#39;e-mail
    - Invia conferma al candidato

**Configurazione e-mail avanzata:**

    Configura routing di posta elettronica dinamico:
    - Se reparto è uguale a &quot;IT&quot;, inviare a it-hr@company.com
    - Se reparto è uguale a &quot;Vendite&quot;, inviare a sales-hr@company.com
    - Impostazione predefinita a hr@company.com

### Passaggio 3: configurare l’integrazione API

**Configurazione API REST:**

    Invia dati modulo all&#39;endpoint REST:
    - URL: https://api.company.com/forms/submit
    - Metodo: POST
    - Autenticazione: token Bearer
    - Content-Type: application/json

**Esempio di mappatura dati:**

    Mappa i campi modulo su API:
    - firstName -> user.first_name
    - lastName -> user.last_name
    - email -> user.email_address
    - department -> user.department_id

### Passaggio 4: configurare l’archiviazione cloud

**Configurazione archiviazione BLOB di Azure:**

    Archivia invii moduli in Azure:
    - Contenitore: invii moduli
    - Cartella: /{year}/{month}/{day}/
    - Formato file: JSON con allegati
    - Livello di accesso: privato

## Esempi di integrazione

### Modulo di feedback del cliente

**Configurazione invio:**

- Notifica e-mail al team di supporto
- Memorizzare i dati nel sistema CRM tramite API
- Crea ticket di supporto automaticamente
- Invia e-mail di conferma al cliente

**Implementazione:**
Invia il modulo di feedback cliente a:
1. Invia e-mail a <support@company.com> con dettagli modulo
2. PUBBLICA in API CRM per creare record cliente
3. Attivare il flusso di lavoro per la creazione di ticket di supporto
4. Inviare un messaggio di ringraziamento al cliente

### Modulo di onboarding dipendenti

**Configurazione invio:**

- Invia al team HR le informazioni sulla nuova assunzione
- Archiviare documenti in SharePoint
- Attivare il flusso di lavoro di onboarding
- Creare account utente in vari sistemi

**Implementazione:**
Elabora onboarding dipendenti:
1. Invia un&#39;e-mail a <hr@company.com> con i dettagli del dipendente
2. Caricare i documenti nella cartella dei dipendenti di SharePoint
3. Avvia il flusso di lavoro di onboarding in Power Automate
4. Creare account nel sistema HR, e-mail e altri strumenti

### Modulo generazione lead

**Configurazione invio:**

- Memorizzare i dati dei lead nella piattaforma di automazione marketing
- Invia notifica al team vendite
- Aggiungi lead al sistema CRM
- Attiva sequenza e-mail di follow-up

**Implementazione:**
Generazione lead processo:
1. PUBBLICARE i dati dei lead nell’API di Marketo
2. Creazione del record del lead in Salesforce
3. Inviare un messaggio e-mail al team di vendita con i dettagli del lead
4. Avviare la sequenza di acquisizione automatica delle e-mail

## Scenari di integrazione avanzata

### Elaborazione di moduli in più passaggi

**Integrazione del flusso di lavoro complessa:**

- Convalidare i dati del modulo rispetto a sistemi esterni
- Elabora pagamenti tramite gateway di pagamento
- Generare documenti e contratti
- Inviare notifiche a più stakeholder

### Convalida dei dati in tempo reale

**Convalida basata su API:**

- Convalidare gli indirizzi e-mail in base alla directory aziendale
- Verifica la disponibilità del prodotto nel sistema di inventario
- Verificare le informazioni sul cliente in CRM
- Convalida informazioni di pagamento

### Indirizzamento invio condizionale

**Routing dinamico basato sui dati del modulo:**

- Instradamento a reparti diversi in base al tipo di richiesta
- Invia a diversi sistemi in base al livello del cliente
- Elabora in modo diverso in base allo stato di completamento del modulo
- Gestire diverse regole business per area geografica

## Sicurezza e conformità

### Protezione dei dati

**Crittografia e sicurezza:**

- Crittografa dati sensibili in transito
- Credenziali e token API protetti
- Implementare controlli di accesso appropriati
- Seguire i criteri di conservazione dei dati

### Requisiti di conformità

**GDPR e privacy:**

- Implementare la gestione del consenso
- Fornire funzionalità di esportazione dei dati
- Abilita richieste di eliminazione dati
- Gestisci piste di controllo

**Standard di settore:**

- Conformità HIPAA per i moduli sanitari
- PCI DSS per l&#39;elaborazione dei pagamenti
- Conformità SOX per i moduli finanziari
- Normative specifiche del settore

## Test e convalida

### Test dell’invio

**Scenari di test:**

- Verificare la consegna e la formattazione delle e-mail
- Verifica connettività API e mappatura dati
- Convalidare i caricamenti dell’archiviazione cloud
- Verifica la funzionalità di attivazione del flusso di lavoro

**Gestione errori:**

- Verifica scenari di errore di rete
- Convalida visualizzazione messaggio di errore
- Verifica meccanismi di esecuzione di nuovi tentativi
- Verificare le opzioni di fallback

### Ottimizzazione delle prestazioni

**Strategie di ottimizzazione:**

- Implementare l’elaborazione asincrona
- Utilizza operazioni batch per dati in blocco
- Ottimizza la frequenza di chiamata API
- Memorizza nella cache i dati ad accesso frequente

## Risoluzione dei problemi di integrazione

### Problemi comuni

**Problemi di consegna e-mail:**

- Verifica la configurazione del server SMTP
- Verificare gli indirizzi e-mail dei destinatari
- Controlla le impostazioni del filtro anti-spam
- Verifica formattazione modello e-mail

**Problemi di integrazione API:**

- Verificare gli URL degli endpoint API
- Verifica credenziali di autenticazione
- Convalidare il formato e le intestazioni della richiesta
- Gestione della risposta API di revisione

**Problemi di integrazione dello storage:**

- Conferma credenziali archiviazione
- Verifica autorizzazioni cartella
- Verifica limiti di caricamento file
- Verifica della connettività di rete

### Ottenere aiuto

Per i problemi di integrazione:

- Controlla le [domande frequenti su Forms Experience Builder](forms-experience-builder-frequently-asked-questions.md)
- Rivedi la [Guida introduttiva](forms-experience-builder-getting-started.md)
- Contatta l’amministratore di sistema per assistenza tecnica
- Consulta la documentazione API per i servizi esterni

## Articoli correlati

- [Panoramica di Forms Experience Builder](product-overview.md)
- [Guida introduttiva di Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Implementare e configurare Forms Experience Builder](deploy-forms-experience-builder.md)
- [Importazione e conversione intelligenti](intelligent-import-conversion.md)
- [Domande frequenti](forms-experience-builder-frequently-asked-questions.md)
