---
title: Forms Experience Builder
description: Creare moduli potenti più rapidamente utilizzando i frammenti di modulo
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 6134772ea9916fc17fb7fc8a30e18799a81d4994
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 40%

---


# Introduzione a Forms Experience Builder

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa documentazione è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. Funzionalità, comandi ed esempi possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

AEM Forms Experience Builder sfrutta la potenza dell’intelligenza artificiale generativa per democratizzare e accelerare la creazione e l’aggiornamento delle esperienze di moduli digitali. Consentendo flussi di lavoro basati sulle finalità guidati dalle interazioni del linguaggio naturale, consente agli utenti di progettare, modificare e ottimizzare i moduli in modo semplice e rapido.

Basato sulle moderne tecnologie web e su servizi di IA avanzati, Forms Experience Builder consente agli utenti tecnici e non tecnici di creare moduli sofisticati di livello professionale tramite interfacce conversazionali. Questo approccio rivoluzionario riduce il time-to-value da giorni ad ore, elimina gli ostacoli tecnici attraverso la semplicità dell’interfaccia e ridimensiona gli sforzi di modernizzazione dell’intero ecosistema di moduli.



## Funzionalità di base

Forms Experience Builder offre due flussi di lavoro principali per la creazione di potenti moduli digitali:

### &#x200B;1. Creazione di moduli basati sull’intelligenza artificiale

**Generazione moduli in linguaggio naturale**

Crea moduli completi da zero utilizzando descrizioni in inglese semplice. È sufficiente descrivere le proprie esigenze, ad esempio &quot;Creare un modulo di feedback del cliente con scale di valutazione e campi di commento&quot; e Forms Experience Builder genera la struttura appropriata del modulo. Utilizza il generatore di esperienze degli editor visivi per aggiungere altri campi, regole di convalida e logica di invio.

**Gestione campi dinamici**

Aggiungi, modifica o rimuovi campi modulo tramite comandi conversazionali. L’IA comprende il contesto e può suggerire in modo intelligente i tipi di campi, le regole di convalida e i miglioramenti all’interfaccia utente in base alle tue esigenze.

**Ottimizzazione layout**

Aggiorna i layout e le configurazioni dei moduli tramite il linguaggio naturale. Richiedi modifiche quali &quot;Modifica il layout del modulo al layout della procedura guidata&quot; e Forms Experience Builder applica le regolazioni di stile e layout appropriate.

**Configurazione completa azione di invio**

Configura l’invio dei moduli da integrare con i sistemi aziendali esistenti:

- **Integrazione e-mail**: configura notifiche e conferme e-mail automatiche
- **Endpoint API REST**: connessione ad applicazioni e servizi personalizzati
- **Archiviazione cloud**: integrazione con Blob Storage di Azure, SharePoint e OneDrive
- **Automazione dei flussi di lavoro**: connessione a Power Automate e a Workfront Fusion
- **Piattaforme di marketing**: integrazione diretta con Marketo per la gestione dei lead
- **Flussi di lavoro di AEM**: sfrutta le funzionalità esistenti del flusso di lavoro di AEM


### &#x200B;2. Importazione e conversione intelligenti

**Formati di importazione supportati**

Trasforma moduli e documenti esistenti in esperienze digitali interattive. Forms Experience Builder supporta:

- **Acroforms**: PDF forms interattivo con strutture di campi esistenti
- **PDF XFA**: architetture di moduli basate su XML complesse
- **PDF semplici**: documenti statici convertiti in moduli interattivi
- **Immagini e schermate**: formati JPG e PNG (verifica con il team i limiti di dimensione)
- **Forms disegnato a mano**: schizzi e fotografie su carta


**Processo di conversione intelligente**

Il contenuto caricato viene analizzato in:

- Rileva tipi di campo e relazioni
- Mantieni il layout nella misura del possibile
- Migliora con un design reattivo moderno
- Aggiungere convalida avanzata e logica condizionale
- Ottimizza per accessibilità ed esperienza mobile

## Come funziona

Forms Experience Builder adotta un approccio semplice e conversazionale:

    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │ 1 Descrivere    │───▶│ 2. IA Crea │───▶│ 3. Perfeziona e    │
    │ modulo      │    Modulo iniziale di │   │    Configurazione di │      │
    │ requisiti   │    │                 │    │                 │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
    │                       │                       │
    │                       │                       │
    ▼                       ▼                       ▼
    ┌───────────────────────────────────────────────────────────────────────────┐
    │ Modulo di → &quot;Crea un modulo di richiesta di prestito&quot; con relativo                  │
    │ &quot;Aggiungi campo e-mail&quot;           Campi → e di base                          │
    │ &quot;Imposta il valore del campo e-mail su @firstname@gmail.com&quot; → regole di convalida   │
    └───────────────────────────────────────────────────────────────────────────┘

## Scenari di esempio

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Transform PDF Forms to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Trasformare moduli PDF in moduli adattivi</p>
                    <p class="is-size-6">Converti Acroform, PDF XFA o documenti PDF semplici in moduli digitali interattivi e reattivi con funzionalità avanzate.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Modernize Legacy XFA Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Modernizzare la versione precedente di XFA Forms</p>
                    <p class="is-size-6">Trasforma applicazioni XFA complesse in esperienze digitali moderne e accessibili con flussi di lavoro degli utenti migliorati.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Convert Screenshots to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Conversione di schermate in Forms digitale</p>
                    <p class="is-size-6">Trasforma immagini, schermate o moduli disegnati a mano in esperienze digitali completamente funzionali.</p>
                </div>
            </div>
        </div>
    </div>
</div>

<!-- #### Import and Enhance Web Forms

Import existing HTML forms and enhance them with advanced features while preserving existing functionality.

**Key benefits:**

- Advanced validation and business logic
- Conditional field behaviors
- Multi-channel submission options
- Enhanced user experience design -->

## Confronto tra Forms Experience Builder e sviluppo tradizionale

| Aspetto | Creazione di moduli tradizionali | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **Tempo di creazione** | 2-3 giorni | 2-3 ore |
| **Conoscenza tecnica** | Obbligatorio | Non obbligatorio |
| **Regole di convalida** | Codifica manuale | Linguaggio naturale |
| **Accessibilità** | Implementazione manuale | Conformità incorporata |


## Vantaggi per le organizzazioni

<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Democratized Form Creation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Creazione di moduli democratizzati</p>
                    <p class="is-size-6">Consentire agli utenti non tecnici di creare moduli sofisticati senza alcuna conoscenza di programmazione attraverso conversazioni in linguaggio naturale.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Reduced Time to Value (TTV)">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">TTV (Time-to-Value) ridotto</p>
                    <p class="is-size-6">Accelera notevolmente lo sviluppo dei moduli da giorni ad ore, consentendo un più rapido lancio sul mercato per le iniziative digitali.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Interface Simplicity">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Semplicità dell’interfaccia</p>
                    <p class="is-size-6">Elimina la curva di apprendimento con un'interfaccia di conversazione intuitiva, riducendo i tempi di formazione e aumentando l'adozione.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Scaling Modernization Efforts">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Ridimensionamento degli sforzi di modernizzazione</p>
                    <p class="is-size-6">Modernizza in modo efficiente i portfolio di moduli legacy, preservando la logica di business e migliorando l’esperienza utente nell’intero ecosistema dei moduli.</p>
                </div>
            </div>
        </div>
    </div>
</div>

## Onboarding

Forms Experience Builder è attualmente disponibile come parte del programma per l’accesso anticipato (EA). Per partecipare e ottenere l&#39;accesso, è necessario disporre delle seguenti informazioni:

### Informazioni richieste

- **ID organizzazione IMS**: identificatore organizzazione Adobe
- **ID programma**: identificatore del programma specifico in Adobe Experience Cloud
- **Dettagli progetto**: Timeline, ambito e casi d&#39;uso previsti
- **E-mail ufficiale di lavoro**: associata all&#39;account Adobe della tua organizzazione


### Ottenere l’ID organizzazione IMS e l’ID programma

Per i passaggi dettagliati per individuare l’ID organizzazione IMS e l’ID programma, consulta:

- [Guida alla configurazione dell&#39;organizzazione Adobe Experience Cloud](/help/onboarding/cloud-manager-introduction.md)
- [Gestione di programmi e ambienti](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

### Richiedi accesso

1. Raccogli l’ID organizzazione IMS e l’ID programma utilizzando le guide precedenti
2. Invia un&#39;e-mail a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) richiedendo l&#39;accesso
3. Includi nella richiesta:
   - Nome organizzazione e ID organizzazione IMS
   - ID programma
   - Timeline e ambito del progetto
   - Casi d’uso previsti e obiettivi aziendali

>[!IMPORTANT]
>
> **Programma di disponibilità limitata**: l&#39;accesso a Forms Experience Builder è soggetto all&#39;approvazione delle parti interessate interne. Adobe esaminerà la tua richiesta in base alla capacità del programma e all’allineamento con i criteri di accesso anticipato. L&#39;approvazione non è garantita e dipende dalla disponibilità del programma corrente.

Per ulteriori informazioni sul programma Accesso anticipato e sulle relative funzioni, consulta la [documentazione rellativa all’accesso anticipato di AEM Forms](/help/forms/early-access-ea-features.md).


## Guida introduttiva

Per iniziare a utilizzare Forms Experience Builder, visita la [documentazione di Forms Experience Builder](forms-ai-assistant-getting-started.md). Puoi accedere a Forms Experience Builder tramite l’editor di AEM Forms o l’editor universale, a seconda del flusso di lavoro preferito.

Per le organizzazioni che mirano a trasformare i processi di creazione dei moduli, Forms Experience Builder offre una soluzione potente e intuitiva che combina la flessibilità dell’intelligenza artificiale conversazionale con la robustezza della gestione dei moduli di livello Enterprise.
