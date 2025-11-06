---
title: Implementare e configurare Forms Experience Builder
description: Scopri come utilizzare Forms Experience Builder per creare e gestire moduli con divulgazione progressiva per tutti i tipi di utenti
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: 977f227e-e941-4797-ba74-53d5b8c60ca9
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1404'
ht-degree: 74%

---

# Implementare e configurare Forms Experience Builder

>[!NOTE]
>
> Forms Experience Builder è disponibile in un programma di accesso anticipato. Prima di iniziare, assicurati di aver richiesto e ottenuto l’accesso. Per istruzioni complete, consulta le informazioni sull&#39;[onboarding](product-overview.md#onboarding) .

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa documentazione è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. Funzioni, comandi ed esempi possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma di accesso anticipato.

Questa guida completa ti aiuta a iniziare a creare e gestire i moduli utilizzando la tecnologia IA conversazionale. Sia che si tratti di un principiante che desidera creare il primo modulo o di un utente avanzato che desidera sfruttare funzionalità sofisticate, può trovare informazioni dettagliate ed esempi pratici per guidare il percorso attraverso le funzionalità di Forms Experience Builder.

## Prerequisiti e configurazione

### Requisiti di accesso

Prima di utilizzare Forms Experience Builder, assicurati di disporre di:

* **Accesso a Forms Experience Builder** - Disponibile tramite il programma di accesso anticipato
* **AEM Forms as a Cloud Service** - Ambiente di authoring di produzione con componenti core di Forms adattivi
* **Nozioni di base** - Familiarità con i concetti dei moduli e i requisiti aziendali

### Verifica che i moduli siano abilitati

Prima di utilizzare Forms Experience Builder, assicurati che [AEM Forms sia abilitato per il tuo ambiente](/help/forms/setup-forms-cloud-service.md).

### Configurare l’ambiente

Il processo di configurazione dipende dall’implementazione di AEM Forms. Scegli il percorso che corrisponde al progetto.

**Per Edge Delivery Services**

Se utilizzi Edge Delivery Services Forms e utilizzi principalmente Universal Editor. [Prepara il progetto per Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md). Questa è una configurazione una tantum per abilitare Forms Experience Builder.

**Per moduli basati su Componenti core**

Se utilizzi Forms adattivo basato su componenti core nell&#39;ambiente di authoring AEM, assicurati che [i componenti core adattivi di Forms siano abilitati](/help/forms/enable-adaptive-forms-core-components.md) per il tuo ambiente.



## Guida rapida

### Accedere al generatore di esperienze Forms

Puoi accedere a Forms Experience Builder da tre posizioni principali, a seconda del flusso di lavoro e del tipo di modulo.


**1. Editor Forms adattivo (per componenti core)**

Puoi avviare il generatore direttamente durante la modifica di un modulo specifico.

1. Passa a **AEM > Forms > Forms &amp; Documents**.
1. [Crea un nuovo modulo utilizzando un modello di Componenti core](/help/forms/creating-adaptive-form-core-components.md) o aprirne uno esistente.
1. Seleziona l&#39;icona **Forms Experience Builder** nella barra degli strumenti dell&#39;editor per aprire l&#39;interfaccia di conversazione.

   ![Icona Assistente IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

**1. Editor universale (per Edge Delivery Services Forms)**

Per i moduli distribuiti tramite Edge Delivery Services, il generatore è integrato nell’Editor universale.

1. Apri il modulo Edge Delivery Services nell’Editor universale.
2. Seleziona l&#39;icona **Forms Experience Builder** nel pannello a destra per avviare l&#39;interfaccia di conversazione.

### Il primo modulo

| Esempio di conversazione |   |
|--------------------------------------------------------------------------------------------------------------------------------------------|---|
| **Prova questa conversazione per creare un modulo di contatto completo (basato sulla demo del Summit):**<br><br>**Tu:** “Crea un modulo di contatto per acquisire informazioni personali tra cui nome completo, indirizzo e-mail, numero di telefono, nome della società, mansione e un campo del messaggio per le richieste”<br><br>**IA:** Seleziona un modello<br>    Un elenco a discesa per selezionare un modello <br><br>**IA:** Seleziona un tema<br>    Un elenco a discesa per selezionare un tema <br><br>**IA:** Crea modulo | ![Il tuo primo modulo](/help/edge/docs/forms/assets/create-form.png) |
| <br>**IA:** Apri modulo creato | </br> Il modulo viene creato e aperto nell’editor |


### Comandi essenziali

| Simbolo | Scopo | Esempio di utilizzo |
|--------|---------|---------------|
| `/` | Azioni e scelte rapide | `/create-form contact form`, `/help validation rules`, `/update-layout wizard` |
| `@` | Fai riferimento ai campi modulo esistenti | `@email`, `@firstName`, `Make @phoneNumber required` |
| Testo normale | Conversazione naturale | “Aggiungi un campo numero di telefono richiesto”, “Crea convalida per e-mail” |

**Esempi di comandi specifici:**

* `/create-form customer survey` - Crea un nuovo modulo di sondaggio cliente
* `/add-field @email validation` - Aggiunge la convalida al campo e-mail esistente
* `/create-rule show @spouse if @maritalStatus equals married` - Crea logica condizionale
* `/configure-submit to email support@company.com` - Configura l’invio di e-mail
* `/help multi-step forms` - Ottiene assistenza sulla creazione di moduli con più passaggi

### Suggerimenti per il successo

* **Sii più specifico**: “Aggiungi un campo e-mail obbligatorio con convalida” funziona meglio di “aggiungi e-mail”
* **Riferimento a campi esistenti**: utilizza `@fieldName` quando modifichi i moduli
* **Chiedi aiuto**: digita `/help` seguito dalla domanda
* **Iterazione**: apporta una modifica alla volta per ottenere risultati ottimali


## Metodi per iniziare a creare un modulo

### Inizia con i prompt del linguaggio naturale

Descrivi i requisiti del modulo in linguaggio naturale; Forms Experience Builder genererà la struttura completa del modulo:

**Esempi:**

* “Crea un modulo per la richiesta di un prestito con informazioni personali, dettagli finanziari e caricamenti di documenti”
* “Crea un modulo per il feedback dei clienti con valutazioni, commenti e categorie di prodotti”
* “Ho bisogno di un modulo di registrazione in più passaggi per una conferenza con elaborazione dei pagamenti”


### Interazioni chiave

#### Aggiunta di elementi modulo

**Aggiunte di base:**

    👤 Tu: “Aggiungi una sezione per informazioni personali”
    👤 Tu: “Includi un caricamento di file per il curriculum”
    👤 Tu: “Aggiungi un menu a discesa per la selezione del Paese”

**Specifiche dettagliate:**

    👤 Tu: “Aggiungi un pannello di informazioni personali con campi per nome completo, data di nascita, numero di telefono e indirizzo e-mail”
    👤 Tu: “Includi un componente protetto di caricamento file per i documenti, limitato ai file PDF sotto i 5 MB”
    👤 Tu: “Aggiungi un elenco a discesa Paese con opzioni per USA, Canada, Regno Unito e Germania”

#### Creazione di un comportamento dinamico

**Logica semplice:**

    👤 Tu: “Mostra campi aggiuntivi quando è selezionato ‘Altro’”
    🤖 IA: “Creata una regola condizionale che mostra campi aggiuntivi quando viene scelto ‘Altro’”
    
    👤 Tu: “Rendi richiesto il campo e-mail”
    🤖 IA: “Aggiornato il campo e-mail affinché sia richiesto con la convalida”
    
    👤 Tu: “Calcola il totale automaticamente”
    🤖 IA: “Aggiunta della logica di calcolo per calcolare automaticamente i totali”

**Regole di business complesse:**

    👤 Tu: “Mostra i campi di informazioni sul coniuge solo quando lo stato civile è impostato su ‘Coniugato’”
    🤖 IA: “Creata una regola condizionale che visualizza i campi del coniuge in base allo stato civile”
    
    👤 Tu: “Calcola il costo totale moltiplicando la quantità e il prezzo, quindi aggiungi il 10% di imposta”
    🤖 IA: “Aggiunta la logica di calcolo con quantità, prezzo e calcolo delle imposte”
    
    👤 Tu: “Abilita il pulsante Invia solo quando tutti i campi richiesti sono completati e i termini accettati”
    🤖 IA: “Creata la logica di convalida che abilita l’invio solo quando tutte le condizioni sono soddisfatte”

#### Layout e progettazione dei moduli

**Modifiche del layout:**

    👤 Tu: “Rendi questo modulo con più passaggi”
    🤖 IA: “Convertito il modulo in un layout progressivo con navigazione”
    
    👤 Tu: “Organizza i campi in due colonne”
    🤖 IA: “Aggiornato il layout per visualizzare i campi in una disposizione a due colonne”
    
    👤 Tu: “Converti in un layout con pannello a soffietto”
    🤖 IA: “Trasformato il modulo per utilizzare le sezioni in stile pannello a soffietto”

**Miglioramenti alla progettazione:**

    👤 Tu: “Crea un modulo stile procedura guidata con 3 passaggi: informazioni personali, preferenze e revisione”
    🤖 IA: “Creato un modulo procedura guidata con tre passaggi distinti e navigazione”
    
    👤 Tu: “Disponi i campi indirizzo in un layout compatto a due colonne&quot;
    🤖 IA “Organizzati i campi indirizzo in un formato compatto a due colonne”
    
    👤 Tu: “Aggiorna il layout in modo che corrisponda al wireframe allegato”
    🤖 IA: “Modificato il layout in modo che corrisponda al riferimento di progettazione fornito”

### Invia configurazione

Forms Experience Builder può configurare vari endpoint di invio per collegare i moduli a sistemi e servizi esterni:

| Cambiare tipo di azione | Comando di configurazione | Caso d’uso |
|------------------|---------------|----------|
| **E-mail** | &quot;Invia modulo a e-mail&quot; | Notifiche e conferme per l’invio di moduli |
| **API REST** | &quot;Invia a endpoint REST&quot; | Applicazioni personalizzate e sistemi di terze parti |
| **Archiviazione cloud** | “Salva in Azure/SharePoint” | Archiviazione dei documenti e gestione dei file |
| **Flusso di lavoro** | “Connettiti a Power Automate” | Automazione e approvazione dei processi aziendali |
| **Marketing** | “Integra con Marketo” | Gestione dei lead e automazione del marketing |

**Esempi di configurazione di invio avanzata:**

    👤 Tu: “Invia invii di moduli a hr@company.com e crea un caso nel nostro sistema CRM”
    🤖 IA: “Configurato l’invio di e-mail e l’azione di invio CRM”
    
    👤 Tu: “Invia dati all’endpoint API REST e attiva il nuovo flusso di lavoro dei clienti”
    🤖 IA: “Configurato l’invio API REST con i trigger del flusso di lavoro”
    
    👤 Tu: “Invia risposte e-mail al team di vendita e aggiungi il lead alla nostra piattaforma di automazione marketing”
    🤖 IA: “Configurato l’invio multicanale con automazione e-mail e marketing”





## Operazioni avanzate dei moduli


### Creazione di regole complesse

Crea una logica di convalida e di business avanzata che risponda alle interazioni degli utenti e garantisca l’integrità dei dati:

    👤 Tu: “Mostra la sezione dell’indirizzo solo se l’utente seleziona ‘Spedisci a indirizzo diverso’”
    🤖 IA: “Creata una regola condizionale che mostra/nasconde il pannello dell’indirizzo in base alla selezione della casella di controllo”

### Creazione di moduli in più passaggi

    👤 Tu: “Crea un modulo progressivo con 3 passaggi: informazioni personali, preferenze, conferma”
    🤖 IA: “Creato un modulo progressivo con navigazione tra passaggi e convalida in ogni fase”

### Tipi di campo avanzati

* Caricamento di file con restrizioni di convalida e dimensione per la gestione dei documenti
* Selettori di date con vincoli e regole aziendali per la programmazione
* Elenchi a discesa con opzioni dinamiche che cambiano in base alle selezioni degli utenti
* Pulsanti di scelta con logica condizionale per alberi decisionali complessi


### Conversione da PDF a modulo

    👤 Tu: “Converti questo PDF in un modulo interattivo”
    🤖 IA: “Analizzato PDF e creato un modulo con i tipi di campo e la convalida appropriati”





## Guida e apprendimento del prodotto

Forms Experience Builder può anche insegnarti le funzionalità di AEM Forms:

### Fai domande come:

* “Come si crea un modulo con più passaggi?”
* “Qual è la differenza tra pannelli e sezioni?”
* “Come si configurano le notifiche e-mail?”
* “Quali sono le best practice per i moduli compatibili con i dispositivi mobili?”
* “Come si applicano i temi ai moduli?”

### Ottieni aiuto per:

* Concetti e terminologia di AEM Forms
* Istruzioni passo dopo passo per le funzioni complesse
* Best practice e consigli
* Risoluzione dei problemi comuni


Per ulteriore supporto, consulta la [Libreria prompt per Forms Experience Builder](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md) principale o contatta l’amministratore di sistema per assistenza tecnica.
