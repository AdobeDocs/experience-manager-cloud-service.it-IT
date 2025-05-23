---
title: Quali sono i miglioramenti al servizio Invoke VRE per i moduli basati su componenti core?
description: Miglioramenti al servizio Invoke per l’editor di regole
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
keywords: richiamare i miglioramenti del servizio in VRE, popolare le opzioni a discesa utilizzando il servizio di richiamo, impostare il pannello ripetibile utilizzando l’output del servizio di richiamo, impostare il pannello utilizzando l’output del servizio di richiamo, utilizzare il parametro di output del servizio di richiamo per convalidare un altro campo.
exl-id: 2ff64a01-acd8-42f2-aae3-baa605948cdd
source-git-commit: 2cae8bb1050bc4538f4645d9f064b227fb947d75
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 1%

---

# Utilizzo del servizio Invoke nell’Editor di regole visive per i moduli basati su componenti core

L&#39;editor di regole visive in un modulo adattivo supporta la funzionalità **Richiama servizio**, che consente di selezionare un servizio dall&#39;elenco di modelli di dati modulo (FDM) configurati per l&#39;istanza. Puoi mappare i campi modulo direttamente sui parametri di input del servizio. Per mappare i campi modulo ai parametri di output, utilizza l’opzione payload dell’evento per il servizio del modello dati modulo specificato. Inoltre, l&#39;editor di regole visive consente di creare regole per i gestori di operazioni riuscite e non riuscite per le operazioni **Richiama servizio** in base alle relative risposte di output. I gestori di errori gestiscono l&#39;esecuzione corretta dell&#39;operazione **Richiama servizio**, mentre i gestori di errori risolvono gli errori che si verificano.

### Vantaggi dell’utilizzo del servizio Invoke nell’editor di regole del modulo

Di seguito sono riportati alcuni vantaggi dell’utilizzo dell’operazione Invoke Service nell’editor di regole di un modulo Adobe:

* **Integrazione semplificata**: l&#39;editor di regole visive semplifica il processo di integrazione di servizi o API esterni nel Forms adattivo. Utilizzando il servizio **Invoke**, è possibile collegare facilmente i moduli a varie origini dati e servizi senza la necessità di codifiche complesse, rendendo l&#39;integrazione dei moduli più efficiente.

* **Gestione dinamica delle risposte**: è possibile gestire le risposte di esito positivo e di errore in base alle risposte di output del **servizio Invoke**, consentendo ai moduli di reagire dinamicamente a scenari diversi. Garantisce che i moduli gestiscano in modo appropriato le varie condizioni, migliorando la flessibilità e il controllo.

* **Interazione utente migliorata**: l&#39;utilizzo del servizio **Invoke** nell&#39;editor delle regole consente la convalida in tempo reale nei moduli, fornendo un&#39;esperienza utente migliore. Garantisce inoltre una convalida accurata dei dati sul lato server, riducendo gli errori e migliorando l&#39;affidabilità dei moduli.

## Richiama i gestori del servizio per le risposte di esito positivo e negativo

>[!NOTE]
>
> È possibile utilizzare i gestori degli errori e delle operazioni riuscite del **Richiama servizio** solo per i moduli basati su componenti core. Forms basato su componenti di base non supporta **i gestori di operazioni riuscite e non riuscite del servizio di richiamo**.

L&#39;editor di regole visive consente di creare regole per i gestori di operazioni riuscite e non riuscite per le operazioni **Richiama servizio** in base alle relative risposte di output. L&#39;immagine seguente mostra il **servizio Invoke** nell&#39;editor di regole visive per un modulo adattivo:

![Richiama gestori di servizi](/help/forms/assets/invoke-service-rule-editor.png)

Per aggiungere un gestore operazioni riuscite o non riuscite, fare clic rispettivamente su **[!UICONTROL Aggiungi gestore operazioni riuscite]** o **[!UICONTROL Aggiungi gestore operazioni non riuscite]**.

Quando si fa clic su **[!UICONTROL Aggiungi gestore operazioni riuscite]**, viene visualizzato l&#39;editor di regole **[!UICONTROL Richiama gestore operazioni riuscite del servizio]**, che consente di specificare regole o logica per gestire la risposta di output **Richiama servizio** quando l&#39;operazione ha esito positivo. È possibile specificare regole anche senza definire condizioni; tuttavia, è possibile aggiungere condizioni per il gestore di operazione riuscita facendo clic sull&#39;opzione **[!UICONTROL Aggiungi condizione]**.

![Richiama gestore completamento servizio](/help/forms/assets/invoke-service-success-handler.png)

È possibile aggiungere più regole per gestire le risposte corrette per l&#39;operazione **Richiama servizio**:

![Gestore di operazione riuscita multiplo](/help/forms/assets/invoke-service-multiple-success-handlers.png){width=50%, height=50%}

Analogamente, è possibile aggiungere regole per gestire la risposta di output **Invoke Service** quando l&#39;operazione non riesce. Nell&#39;immagine seguente viene visualizzato l&#39;editor di regole **[!UICONTROL Richiama gestore errori servizio]**:

![Richiama gestore errori servizio](/help/forms/assets/invoke-service-failue-handler.png)

È inoltre possibile aggiungere più regole per gestire le risposte non riuscite dall&#39;operazione **Richiama servizio**.

La funzionalità **Abilita convalida errori sul server** consente l&#39;aggiunta di convalide da parte dell&#39;autore durante la progettazione di un modulo adattivo da eseguire anche sul server.

## Prerequisiti per l’utilizzo del servizio Invoke nell’editor di regole

Di seguito sono riportati i prerequisiti che è necessario soddisfare prima di utilizzare **Invoke Service** nell&#39;editor di regole:

* Assicurati di aver configurato un’origine dati. Per istruzioni sulla configurazione di un&#39;origine dati, [fare clic qui](/help/forms/configure-data-sources.md).
* Crea un modello dati modulo utilizzando l’origine dati configurata. Per istruzioni sulla creazione di un modello dati modulo, [fai clic qui](/help/forms/create-form-data-models.md).
* Assicurati che i Componenti core siano abilitati per il tuo ambiente. Per istruzioni dettagliate su come abilitare i Componenti core per il tuo ambiente, [fai clic qui](/help/forms/enable-adaptive-forms-core-components.md).

## Esplorazione del servizio Invoke attraverso diversi casi d’uso

Il servizio **Invoke** dell&#39;editor di regole visive ti consente di eseguire diverse operazioni utili. Puoi utilizzarlo per popolare le opzioni a discesa, impostare pannelli ripetibili o semplici e convalidare i campi del modulo, il tutto in base alla risposta di output del **servizio Invoke**. In questo modo, è possibile migliorare la flessibilità e l&#39;interattività dei moduli.

La tabella seguente descrive alcuni scenari in cui è possibile utilizzare il servizio **Invoke**:

| **Caso d’uso** | **Descrizione** |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **Popola le opzioni a discesa utilizzando l&#39;output del servizio Invoke** | Compila dinamicamente le opzioni a discesa in base ai dati recuperati dall’output del servizio di richiamo. [Fare clic qui](#use-case-1-populate-dropdown-values-using-the-output-of-invoke-service) per visualizzare l&#39;implementazione. |
| **Imposta il pannello ripetibile utilizzando l&#39;output del servizio di richiamo** | Configura un pannello ripetibile utilizzando i dati dell’output del servizio Invoke, consentendo l’utilizzo di pannelli dinamici. [Fare clic qui](#use-case-2-set-repeatable-panel-using-output-of-invoke-service) per visualizzare l&#39;implementazione. |
| **Imposta il pannello utilizzando l&#39;output di Invoke Service** | Imposta il contenuto o la visibilità di un pannello utilizzando valori specifici dell’output del servizio di richiamo. [Fare clic qui](#use-case-3-set-panel-using-output-of-invoke-service) per visualizzare l&#39;implementazione. |
| **Usa il parametro di output del servizio di richiamo per convalidare altri campi** | Utilizza parametri di output specifici dal servizio di richiamo per convalidare i campi del modulo. [Fare clic qui](#use-case-4-use-output-parameter-of-invoke-service-to-validate-other-fields) per visualizzare l&#39;implementazione. |

Creare un modulo `Get Information` che recuperi i valori in base all&#39;input immesso nella casella di testo `Pet ID`. La schermata seguente mostra il modulo utilizzato in questi casi d’uso:

![Ottieni modulo informazioni](/help/forms/assets/get-information-form.png)

**Campi modulo**

Aggiungi i campi seguenti al modulo:
* **Inserisci ID animale**: Casella di testo
* **Seleziona URL foto**: elenco a discesa
* **Tag**: Pannello
   * Nome: Textbox
   * ID: Textbox
* **Categoria**: Pannello
   * Nome: Textbox
* **Invia**: pulsante Invia

>[!NOTE]
>
> Nel campo **Associa riferimento** della finestra di dialogo **Proprietà** dei campi modulo, seleziona ![foldersearch_18](assets/folder-search-icon.svg) e passa alla proprietà binaria aggiunta nel modello dati modulo.

**Configurazione dei pannelli**

Impostate i pannelli come ripetitivi con i seguenti vincoli:
* Valore minimo: 1
* Valore massimo: 4

È possibile regolare i valori dei pannelli ripetitivi in base alle proprie esigenze.

**Origine dati**

In questo esempio viene utilizzata l&#39;API [Swagger Petstore](https://petstore.swagger.io/) per configurare un&#39;origine dati. Il [Modello dati modulo](/help/forms/create-form-data-models.md) è configurato per il servizio [getPetById](https://petstore.swagger.io/#/pet/getPetById), che recupera i dettagli dell&#39;animale domestico in base all&#39;ID immesso.

Pubblichiamo il seguente JSON utilizzando il servizio [addPet](https://petstore.swagger.io/#/pet/addPet) nell&#39;API [Swagger Petstore](https://petstore.swagger.io/):

```
{
        "id": 101,
        "category": {
            "id": 1,
            "name": "Labrador"
        },
        "name": "Lisa",
        "photoUrls": [
            "https://example.com/photos/lisa1.jpg",
            "https://example.com/photos/lisa2.jpg"
        ],
        "tags": [
            {
                "id": 1,
                "name": "vaccinated"
            },
            {
                "id": 2,
                "name": "friendly"
            },
            {
                "id": 3,
                "name": "house-trained"
            }
        ],
        "status": "available"
    }
```


Le regole e la logica vengono implementate utilizzando l&#39;azione **Richiama servizio** nell&#39;editor delle regole nella casella di testo `Pet ID` per dimostrare i casi d&#39;uso menzionati.

Esaminiamo ora in dettaglio l’implementazione di ogni caso d’uso.

### Caso d’uso 1: popolare i valori a discesa utilizzando l’output del servizio di richiamo

Questo caso d&#39;uso illustra come popolare dinamicamente le opzioni a discesa in base all&#39;output di un `Invoke Service`.

#### Implementazione

Per ottenere questo risultato, creare una regola nella casella di testo `Pet ID` per richiamare il servizio `getPetById`. Nella regola, impostare la proprietà `enum` del menu a discesa `photo-url` su `photoUrls` in **[!UICONTROL Aggiungi gestore di successo]**.

![Imposta valore elenco a discesa](/help/forms/assets/set-dropdownoption.png)

#### Output

Immettere `101` nella casella di testo `Pet ID` per popolare dinamicamente le opzioni del menu a discesa in base al valore immesso.

![Risultato](/help/forms/assets/output1.png)

### Caso d’uso 2: impostare un pannello ripetibile utilizzando l’output del servizio di richiamo

Questo caso d&#39;uso illustra come popolare i pannelli ripetibili in modo dinamico in base all&#39;output di un **servizio Invoke**.

#### Considerazioni

* Verificare che il nome del pannello ripetibile corrisponda al parametro del **servizio Invoke** per il quale si desidera impostare il pannello.
* Il pannello si ripete per il numero di valori restituiti dal campo **Invoke Service** corrispondente.

#### Implementazione

Creare una regola nella casella di testo `Pet ID` per richiamare il servizio `getPetById`. In **[!UICONTROL Aggiungi gestore operazioni riuscite]**, aggiungi un&#39;altra risposta del gestore operazioni riuscite. Impostare il valore del pannello `tags` su `tags` nella regola.

![Crea regola per pannello ripetibile](/help/forms/assets/create-rule-repeatable-panel.png)

#### Output

Immettere `101` nella casella di testo `Pet ID` per popolare il pannello ripetibile in modo dinamico in base al valore di input.

![Output](/help/forms/assets/output2.png)

### Caso d’uso 3: impostare il pannello utilizzando l’output del servizio di richiamo

In questo caso d&#39;uso viene illustrato come impostare in modo dinamico il valore di un pannello in base all&#39;output di un **servizio Invoke**.

#### Considerazioni

* Verificare che il nome del pannello corrisponda al parametro del **servizio Invoke** per il quale si desidera impostare il pannello.
* Il pannello si ripete per il numero di valori restituiti dal campo Invoke Service corrispondente.

#### Implementazione

Creare una regola nella casella di testo `Pet ID` per richiamare il servizio `getPetById`. In **[!UICONTROL Aggiungi gestore operazioni riuscite]**, aggiungi un&#39;altra risposta del gestore operazioni riuscite. Impostare il valore della casella di testo `categoryname` su `category.name` nella regola.

![Crea regola per pannello ripetibile](/help/forms/assets/set-panel-values.png)

#### Output

Immettere `101` nella casella di testo `Pet ID` per popolare il pannello in modo dinamico in base al valore di input.

![Output](/help/forms/assets/output3.png)

### Caso d’uso 4: utilizzo del parametro di output del servizio Invoke per convalidare altri campi

Questo caso d&#39;uso illustra come utilizzare l&#39;output di un **richiama servizio** per convalidare dinamicamente altri campi modulo.

#### Implementazione

Creare una regola nella casella di testo `Pet ID` per richiamare il servizio `getPetById`. In **[!UICONTROL Aggiungi gestore errori]**, aggiungere una risposta del gestore errori. Nascondi il pulsante **Invia** se viene immesso un `Pet ID` non corretto.

![Gestore errori](/help/forms/assets/create-rule-failure-handler.png)

#### Output

Immettere `102` nella casella di testo `Pet ID` e il pulsante **Invia** è nascosto.

![Output](/help/forms/assets/output4.png)

## Domande frequenti

**D: cosa succede se ho creato una regola utilizzando il servizio Invoke e quindi eseguo l&#39;aggiornamento alla versione più recente dei componenti core?**

**A:** Quando si esegue l&#39;aggiornamento alla versione più recente dei componenti core, la regola **Richiama servizio** viene aggiornata automaticamente all&#39;interfaccia utente più recente, in quanto è compatibile con le versioni precedenti.

**Q: è possibile aggiungere più regole per gestire le risposte di esito positivo o negativo per l&#39;operazione di richiamo del servizio?**

**A:** Sì, è possibile aggiungere più regole per gestire le risposte di esito positivo o negativo per l&#39;operazione **Richiama servizio**.

## Articoli correlati

* [Configurare origini dati](configure-data-sources.md)
* [Crea modello dati modulo (FDM)](create-form-data-models.md)
* [Utilizzare il modello dati del modulo (FDM)](work-with-form-data-model.md)
* [Usa modello dati modulo (FDM)](using-form-data-model.md)


## Risorse aggiuntive

{{see-also-rule-editor}}
