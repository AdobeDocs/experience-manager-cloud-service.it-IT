---
title: Questo articolo illustra vari casi d’uso per l’editor di regole in un modulo adattivo basato su componenti core.
description: Questo articolo esplora vari casi d’uso per l’editor di regole in un modulo adattivo basato su componenti core. Viene inoltre evidenziato come le funzioni personalizzate possono essere utilizzate per creare regole personalizzate per i moduli.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
source-git-commit: 4ff533de73fcb91fb2b68cfdb3fd2602645ff7aa
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 0%

---

# Miglioramenti e casi d’uso dell’editor di regole

<span class="preview"> Queste sono funzionalità non definitive disponibili tramite il nostro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features">canale non definitivo</a>.

Questo articolo introduce gli ultimi miglioramenti all’editor di regole in Adaptive Forms. Questi aggiornamenti sono progettati per aiutarti a definire più facilmente il comportamento dei moduli, senza scrivere codice personalizzato, e per creare esperienze di modulo più dinamiche, reattive e personalizzate.

La tabella seguente elenca i recenti miglioramenti apportati all’editor di regole in Adaptive Forms, insieme a una breve descrizione e ai vantaggi chiave di ciascuna funzione.:

| Miglioramento | Descrizione | Vantaggi |
|---|----|---|
| **Convalida tramite il metodo `validate()`** | Disponibile nell’elenco delle funzioni per convalidare singoli campi, pannelli o l’intero modulo. | - Convalida granulare a livello di pannello, campo o modulo <br> - Migliore esperienza utente con messaggi di errore mirati <br> - Impedisce la progressione con dati incompleti <br> - Riduce gli errori di invio dei moduli |
| **Scarica DOR** | Funzione predefinita disponibile nell’editor delle regole per scaricare il documento record (DoR). | - Non è richiesto alcuno sviluppo personalizzato per il download del DoR <br> - Esperienza di download coerente tra i moduli |
| **Variabili dinamiche** | Crea regole utilizzando variabili che cambiano in base all’input dell’utente o ad altre condizioni. | - Abilita le condizioni di regola flessibili <br> - Riduce la necessità di duplicare la logica <br> - Elimina la necessità di creare campi nascosti |
| **Regole personalizzate basate su eventi** | Definisci regole che rispondono a eventi personalizzati oltre i trigger standard. | - Supporta casi d&#39;uso avanzati <br> - Maggiore controllo su quando e come vengono eseguite le regole <br> - Maggiore interattività |
| **Esecuzione del pannello ripetibile in base al contesto** | Le regole ora vengono eseguite nel contesto corretto per ogni pannello ripetuto, anziché solo l’ultima istanza. | - Applicazione accurata delle regole per ogni istanza ripetuta <br> - Riduzione degli errori nelle sezioni dinamiche <br> - Miglioramento dell&#39;esperienza utente con contenuti ripetuti |
| **Supporto per stringa di query, UTM e parametri del browser** | Crea regole che adattano il comportamento del modulo in base a parametri URL o valori specifici del browser. | - Abilita la personalizzazione in base all&#39;origine o all&#39;ambiente <br> - Utile per flussi specifici di marketing o tracciamento <br> - Non è necessario aggiungere script o personalizzazioni |

Esaminiamo ora in dettaglio ogni metodo con casi d’uso specifici per aiutarti a capire come queste funzioni possono essere utilizzate per fornire un’esperienza personalizzata agli utenti

## Metodo Validate nell&#39;elenco funzioni

Funzionalità di convalida migliorate che consentono di utilizzare il metodo **validate()** nell&#39;elenco delle funzioni per convalidare pannelli, campi o interi moduli. Ad esempio, in un modulo di richiesta di prestito in più passaggi, è necessario convalidare diverse sezioni prima di consentire agli utenti di procedere al passaggio successivo.

**Scenario:** un istituto finanziario offre un modulo di richiesta di prestito in più fasi in cui gli utenti devono completare diverse sezioni, ad esempio:

* Dati personali
* Dettagli impiego
* Dettagli del prestito
* Rivedi e invia

Prima che un utente si sposti da un passaggio all’altro, il modulo deve convalidare solo i campi all’interno della sezione corrente. Ad esempio, l’utente non deve essere autorizzato a passare a &quot;Dettagli impiego&quot; a meno che tutti i campi obbligatori in &quot;Dati personali&quot; non siano compilati correttamente.

**Implementazione tramite validate() nell&#39;editor di regole**

Un pulsante **Next** in ciascun pannello attiva una regola utilizzando il metodo **validate()**. La regola controlla se tutti i campi del pannello corrente sono validi. Se la convalida viene superata, il modulo passa al pannello successivo. In caso contrario, vengono visualizzati messaggi di errore che consigliano all’utente di correggere l’input.

La schermata seguente mostra la regola applicata al pulsante **Next**:

![Pulsante Convalida Successivo](/help/forms/assets/validate-next.png)

Nella regola precedente, il pulsante **Successivo** controlla se i campi nella sezione **Dettagli personali** sono validi. Se i dettagli non sono validi, lo stato attivo viene spostato sul campo **Name** nel pannello **Personal Details**.

![output](/help/forms/assets/valid-output.png)

>[!NOTE]
>
> È possibile utilizzare il metodo **validate()** su moduli, frammenti o singoli campi. Quando un frammento è incluso in un modulo, sia il modulo che il frammento vengono visualizzati come opzioni nel contesto di convalida. In questo caso, il frammento si riferisce ai campi al suo interno, mentre il modulo si riferisce al modulo principale in cui è incorporato il frammento.

## Funzione DownloadDor as OOTB nell’editor di regole

L&#39;utilizzo della funzione **DownloadDor()** preconfigurata nell&#39;editor di regole consente di scaricare il documento di record, se il modulo è configurato per generare il documento di record.

>[!NOTE]
>
> Se il modulo non è configurato per il documento di record, viene visualizzato un messaggio di errore quando la regola che utilizza la funzione **downloadDoR()** viene applicata al pulsante.

**Scenario**: un&#39;agenzia governativa fornisce un modulo di richiesta digitale per il rilascio dei certificati. Dopo aver inviato il modulo, i candidati spesso richiedono una copia del modulo compilato per i loro registri o per condividere con un altro reparto. Per migliorare l’esperienza utente, l’agenzia vuole dare ai richiedenti la possibilità di scaricare un documento Record (DoR) immediatamente dopo la presentazione o in qualsiasi fase prima della presentazione finale.

**Implementazione tramite DownloadDor() nell&#39;editor di regole**

Al modulo viene aggiunto un pulsante **Download** tramite l&#39;editor di regole. Una regola è configurata per attivare la funzione **DownloadDor()** quando si fa clic sul pulsante.

La schermata seguente mostra la regola applicata al pulsante **Scarica**:

![Regola pulsante di download](/help/forms/assets/download-button-rule.png)

>[!NOTE]
>
> Il campo **Input** consente all&#39;utente di specificare il nome di file per un documento scaricabile. Questo è un parametro facoltativo.

Se il modulo è configurato per la generazione DoR, questa funzione genera e scarica il PDF immediatamente, senza richiedere alcuna funzione personalizzata.

![Documento record](/help/forms/assets/download-dor-output.png)

## Supporto per le variabili dinamiche nelle regole

L’editor di regole avanzato ora supporta la creazione e l’utilizzo di variabili dinamiche (temporanee). Queste variabili possono essere impostate e recuperate durante il ciclo di vita del modulo utilizzando le funzioni integrate **Imposta valore variabile** e **Ottieni valore variabile**.
Queste variabili:

* Non vengono inviati con i dati del modulo.
* Può contenere valori intermedi o calcolati.
* Può essere utilizzato nella logica condizionale e nelle azioni.

**Scenario**: una società di e-commerce fornisce un modulo d&#39;ordine in cui gli utenti possono selezionare un prodotto e un metodo di spedizione preferito. Mentre il prezzo del prodotto viene acquisito tramite un campo modulo, le spese di spedizione vengono determinate in modo dinamico in base al metodo selezionato e al paese scelto.

Per mantenere pulita la struttura del modulo ed evitare di aggiungere campi nascosti non necessari, l’azienda desidera gestire le spese di spedizione come valore temporaneo che supporta il calcolo in tempo reale dell’importo totale.

**Implementazione tramite le funzioni Imposta valore variabile e Ottieni valore variabile nell&#39;editor di regole**

Regola configurata per impostare una variabile temporanea denominata **extracharge** utilizzando la funzione **Imposta valore variabile**. Il valore di questa variabile dipende dal paese selezionato. Ad esempio, se l’utente seleziona &quot;Stati Uniti&quot;, il valore viene impostato su 50. Per qualsiasi altro paese, è impostato su 100.

![Imposta valore variabile](/help/forms/assets/setvalue.png)

Successivamente, quando si calcola il costo totale della spedizione, la funzione **Ottieni valore variabile** recupera il valore **extracharge** in base al paese selezionato.

![Ottieni valore variabile](/help/forms/assets/getvalue.png)

Questo valore viene quindi aggiunto alle spese di spedizione del prodotto e il risultato viene visualizzato nel campo **Costo totale spedizione**.

![output](/help/forms/assets/getsetvalue-output.png)

Questo approccio consente di calcolare e visualizzare dinamicamente i costi aggiuntivi senza archiviarli in un campo visibile, consentendo un’esperienza utente pulita, reattiva e priva di codice.


## Supporto di regole personalizzate basate su eventi

L&#39;editor di regole avanzato supporta la gestione degli eventi personalizzati utilizzando le funzioni **Invio evento** e **Attivazione evento**. Queste funzioni consentono a diverse parti del modulo di comunicare emettendo e ascoltando eventi personalizzati, abilitando una logica più pulita e modulare senza associare strettamente le azioni a campi specifici.

**Scenario**: un modulo di domanda di lavoro è integrato con un sistema HR esterno che esegue la verifica in background. Una volta completato il controllo, il sistema aggiorna il modulo con **Verifica in background completata!** messaggio. Il modulo deve regolare dinamicamente ciò che il candidato vede in base a questo risultato.

Invece di associare la logica direttamente al campo che riceve lo stato, il modulo utilizza un approccio personalizzato basato su eventi per migliorare la modularità e la manutenibilità.

**Implementazione tramite evento di invio e evento all&#39;attivazione**

Quando lo stato del controllo in background viene aggiornato, una regola utilizza **Dispatch Event** per emettere un evento personalizzato come **bgvmsg** insieme al risultato dello stato. Una regola separata ascolta questo evento utilizzando **Evento all&#39;attivazione**.

Le schermate seguenti mostrano le regole applicate alla &quot;Verifica in background completata?&quot; e il campo di testo &quot;bgvmsg&quot;.

![evento di invio](/help/forms/assets/dispatch-event-rule.png)

![su evento trigger](/help/forms/assets/trigger-event-rule.png)

Quando l’evento viene rilevato, controlla lo stato e aggiorna il modulo di conseguenza. Ad esempio:

* Se il controllo in background viene superato, nel modulo viene visualizzato un messaggio di conferma.
* Se sono necessari documenti aggiuntivi, nel modulo viene visualizzata una sezione in cui viene chiesto al richiedente di caricare le informazioni richieste, insieme a un messaggio di avviso.

![Output evento di invio](/help/forms/assets/dispatch-trigger-output.png)

Supporto per eventi personalizzati che consentono agli sviluppatori di creare e attivare eventi personalizzati utilizzabili come condizioni nell’editor di regole.

## Esecuzione di regole basate sul contesto per pannelli ripetibili

Forms adattivo supporta l’esecuzione di regole in base al contesto per i pannelli ripetibili. Questo consente di applicare le regole in modo specifico all’istanza del pannello in cui l’utente interagisce, anziché influenzare tutte le istanze o impostare come predefinita l’ultima.

**Scenario**: un modulo per l&#39;ordine dei prodotti consente agli utenti di aggiungere più prodotti in pannelli separati. Ogni pannello include un campo **Numero di prodotti** e un campo **Costo totale**. Quando un utente aggiorna la quantità di un prodotto, il modulo deve ricalcolare il prezzo totale, ma solo per quel pannello specifico, non per tutti gli altri.

**Implementazione tramite regole in base al contesto nell&#39;editor di regole**

Una regola è configurata nel campo **Numero di prodotto** all&#39;interno del pannello di prodotto ripetibile.

Nella schermata seguente viene visualizzata la regola per il campo **Numero di prodotto** all&#39;interno del pannello dei prodotti ripetibile:

![numero di regole prodotto](/help/forms/assets/number-of-product-rule.png)

Quando la quantità viene modificata, la regola recupera il prezzo unitario del prodotto selezionato e calcola il costo totale solo per quel pannello.

![Output regola in base al contesto](/help/forms/assets/context-aware-rule-output.png)

## Regole basate su URL e parametri di browser in Adaptive Forms

Forms adattivo supporta l’esecuzione dinamica delle regole utilizzando parametri esterni trasmessi tramite l’URL del modulo o derivati dall’ambiente del browser dell’utente. Questo consente esperienze di modulo personalizzate e in base al contesto, in base alla provenienza del visitatore o al dispositivo che sta utilizzando.

## Tipi di parametri consentiti

| Tipo di parametro | Opzioni supportate | Descrizione | Esempio di valore |
| --- | --- | --- | ---|
| Parametro query | `ref` (solo valori stringa) | Coppia chiave-valore generica nell&#39;URL dopo `?` | `?ref=partner123` |
| Parametro UTM | UTM Source<br>UTM Medium<br>UTM Campaign<br>UTM Termine<br>UTM Contenuto | Parametri di query speciali utilizzati per il tracciamento delle campagne | `?utm_source=google&utm_medium=email` |
| Parametro URL | Nome host<br>Percorso | Estrae i componenti strutturali dell&#39;URL del modulo | `hostname=www.example.com`, `path=/signup` |
| Parametro browser | Agente browser<br>Lingua browser<br>Piattaforma browser | Valori derivati dal browser o dal dispositivo dell’utente | `Browser Agent=Mozilla`, `Language=en-US` |

**Scenario**: un modulo di generazione di lead deve adattare il relativo messaggio di benvenuto in base all&#39;origine del traffico. Quando un utente arriva al modulo tramite una campagna pubblicitaria di Google (utilizzando utm_source=google nell’URL), il modulo deve mostrare un saluto personalizzato.

**Implementazione tramite il parametro UTM**

Una regola è configurata in un campo di testo che visualizza un messaggio personalizzato agli utenti di Google e utilizza il parametro **utm_source**.

La schermata seguente mostra la regola configurata sul messaggio di testo:

![regola per SMS](/help/forms/assets/utm-param-rule.png)

Se il valore del parametro **utm_source** è uguale a &quot;google&quot;, un messaggio personalizzato sarà &quot;Ciao utenti di Google, benvenuti nell&#39;annuncio di Campaign!&quot; viene visualizzato.

![utm-param-output](/help/forms/assets/utm-param-output.png)

Questo consente agli esperti di marketing di fornire contenuti rilevanti agli utenti in base alla campagna che li ha inseriti nel modulo senza richiedere l’immissione manuale dei campi o script personalizzati.

Questi miglioramenti espandono in modo significativo le funzionalità dell’editor di regole di Forms adattivo, fornendo agli sviluppatori strumenti potenti per creare moduli più dinamici, interattivi e intelligenti. Ogni miglioramento soddisfa specifiche esigenze aziendali mantenendo la facilità d’uso che rende l’Editor di regole accessibile sia agli utenti tecnici che a quelli non tecnici.