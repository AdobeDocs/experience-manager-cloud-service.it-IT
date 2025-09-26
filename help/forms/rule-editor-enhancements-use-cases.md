---
title: Questo articolo illustra vari casi d’uso per l’editor di regole in un modulo adattivo basato su componenti core.
description: Questo articolo esplora vari casi d’uso per l’editor di regole in un modulo adattivo basato su componenti core. Viene inoltre evidenziato come le funzioni personalizzate possono essere utilizzate per creare regole personalizzate per i moduli.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 062ed441-6e1f-4279-9542-7c0fedc9b200
source-git-commit: f772a193cce35a1054f5c6671557a6ec511671a9
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 0%

---

# Miglioramenti e casi d’uso dell’editor di regole

<span class="preview"> Queste sono funzionalità non definitive disponibili tramite il nostro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features">canale non definitivo</a>. Questi miglioramenti sono applicabili anche a Edge Delivery Services Forms.

Questo articolo introduce gli ultimi miglioramenti all’editor di regole in Adaptive Forms. Questi aggiornamenti sono progettati per aiutarti a definire più facilmente il comportamento dei moduli, senza scrivere codice personalizzato, e per creare esperienze di modulo più dinamiche, reattive e personalizzate.

La tabella seguente elenca i recenti miglioramenti apportati all’editor di regole in Adaptive Forms, insieme a una breve descrizione e ai vantaggi chiave di ciascuna funzione:

| Miglioramento | Descrizione | Vantaggi |
|---|----|---|
| [Convalida tramite il metodo validate()](#validate-method-in-function-list) | Disponibile nell’elenco delle funzioni per convalidare singoli campi, pannelli o l’intero modulo. | - Convalida granulare a livello di pannello, campo o modulo <br> - Migliore esperienza utente con messaggi di errore mirati <br> - Impedisce la progressione con dati incompleti <br> - Riduce gli errori di invio dei moduli |
| [Scarica documento record](#download-document-of-record) | Funzione predefinita disponibile nell’editor delle regole per scaricare il documento record (DoR). | - Non è richiesto alcuno sviluppo personalizzato per il download del DoR <br> - Esperienza di download coerente tra i moduli |
| [Variabili dinamiche](#support-for-dynamic-variables-in-rules) | Crea regole utilizzando variabili che cambiano in base all’input dell’utente o ad altre condizioni. | - Abilita le condizioni di regola flessibili <br> - Riduce la necessità di duplicare la logica <br> - Elimina la necessità di creare campi nascosti |
| [Regole personalizzate basate su eventi](#custom-event-based-rules-support) | Definisci regole che rispondono a eventi personalizzati oltre i trigger standard. | - Supporta casi d&#39;uso avanzati <br> - Maggiore controllo su quando e come vengono eseguite le regole <br> - Maggiore interattività |
| [Esecuzione del pannello ripetibile in base al contesto](#context-based-rule-execution-for-repeatable-panels) | Le regole ora vengono eseguite nel contesto corretto per ogni pannello ripetuto, anziché solo l’ultima istanza. | - Applicazione accurata delle regole per ogni istanza ripetuta <br> - Riduzione degli errori nelle sezioni dinamiche <br> - Miglioramento dell&#39;esperienza utente con contenuti ripetuti |
| [Supporto per stringa di query, UTM e parametri del browser](#url-and-browser-parameter-based-rules-in-adaptive-forms) | Crea regole che adattano il comportamento del modulo in base a parametri URL o valori specifici del browser. | - Abilita la personalizzazione in base all&#39;origine o all&#39;ambiente <br> - Utile per flussi specifici di marketing o tracciamento <br> - Non è necessario aggiungere script o personalizzazioni |

>[!NOTE]
>
> I miglioramenti sono applicabili anche all&#39;[Editor regole di Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

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
>È possibile utilizzare il metodo **validate()** su moduli, frammenti o singoli campi. Quando un frammento è incluso in un modulo, sia il modulo che il frammento vengono visualizzati come opzioni nel contesto di convalida. In questo caso, il frammento si riferisce ai campi al suo interno, mentre il modulo si riferisce al modulo principale in cui è incorporato il frammento.

## Scarica documento record

L&#39;utilizzo della funzione **DownloadDor()** preconfigurata nell&#39;editor di regole consente di scaricare il documento di record, se il modulo è configurato per generare il documento di record.

>[!NOTE]
>
>Se il modulo non è configurato per il documento di record, viene visualizzato un messaggio di errore quando la regola che utilizza la funzione **downloadDoR()** viene applicata al pulsante.

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

L’editor di regole avanzato supporta la creazione e l’utilizzo di variabili dinamiche (temporanee). Queste variabili possono essere impostate e recuperate durante il ciclo di vita del modulo utilizzando le funzioni integrate **Imposta valore variabile** e **Ottieni valore variabile**.
Queste variabili:

* Non vengono inviati con i dati del modulo.
* Può contenere valori intermedi o calcolati.
* Può essere utilizzato nella logica condizionale e nelle azioni.

**Scenario**: un modulo di acquisto online consente agli utenti di selezionare un prodotto, immettere la quantità e scegliere un paese per la spedizione. Il prezzo del prodotto è un valore fisso acquisito tramite un campo modulo, mentre le spese di spedizione variano in modo dinamico a seconda del paese selezionato.

Per evitare di riempire il modulo con campi nascosti, l’azienda decide di memorizzare le spese di spedizione in una variabile temporanea e di utilizzarlo per i calcoli in tempo reale.

**Implementazione tramite le funzioni Imposta valore variabile e Ottieni valore variabile nell&#39;editor di regole**

>[!VIDEO](https://video.tv.adobe.com/v/3471607/get-set-variable-final-video/?quality=12&learn=on)

Nel frammento **Address** è configurata una regola utilizzando la funzione **Imposta valore variabile** per assegnare una variabile temporanea denominata **extracharge**. Il valore di questa variabile cambia in modo dinamico in base al paese selezionato. Ad esempio:

* Se l&#39;utente seleziona Stati Uniti, **extracharge** è impostato su 500.
* Per qualsiasi altro paese, **extracharge** è impostato su 100.

![Imposta valore variabile](/help/forms/assets/setvalue.png)

Successivamente, quando si calcola il **costo totale spedizione**, viene utilizzata la funzione **Ottieni valore variabile** per recuperare il valore di **extracharge**. Questo valore viene aggiunto al **prezzo prodotto × quantità prodotto** per calcolare l&#39;importo finale da pagare al clic del pulsante.

![Ottieni valore variabile](/help/forms/assets/getvalue.png)

Il campo **Costo totale spedizione** viene aggiornato in modo dinamico per riflettere sia il costo del prodotto che le spese di spedizione quando l&#39;utente modifica il paese o la quantità.
![output](/help/forms/assets/getsetvalue-output.png)

>[!NOTE]
>
> È inoltre possibile aggiungere la funzione **Ottieni valore variabile** nella condizione When.
> > ![Funzione Get Variable Value nella condizione When](/help/forms/assets/when-get-variable.png){width=50%,height=50%, align=center}

Questo approccio consente di eseguire calcoli dinamici e in tempo reale senza aggiungere campi aggiuntivi al modulo, mantenendo la struttura pulita e intuitiva.

## Supporto di regole personalizzate basate su eventi

L&#39;editor di regole avanzato supporta la gestione degli eventi personalizzati utilizzando le funzioni **Invio evento** e **Attivazione evento**. Queste funzioni consentono a diverse parti del modulo di comunicare emettendo e ascoltando eventi personalizzati, abilitando una logica più pulita e modulare senza associare strettamente le azioni a campi specifici.

**Scenario**: un modulo di accesso viene creato utilizzando un frammento di accesso riutilizzabile contenente i campi **Immettere il nome utente** e **Immettere la password**. Quando un utente fornisce credenziali valide, il modulo convalida l&#39;input e avvia il processo **Get OTP**. Dopo che l’utente immette un OTP valido, viene reindirizzato alla pagina appropriata.

Invece di associare la logica direttamente ai campi, il modulo utilizza un approccio basato su eventi con **Dispatch Event** e **On Trigger Event** per migliorare la modularità e la gestibilità.

**Implementazione tramite evento di invio e evento all&#39;attivazione**


>[!VIDEO](https://video.tv.adobe.com/v/3471610/dispatch-trigger-final/?quality=12&learn=on)

Il frammento di accesso viene aggiunto al modulo, contenente campi predefiniti per Nome utente e Password. Nel pulsante **Ottieni OTP** è configurata una regola per visualizzare il **Pannello di convalida**, che include il campo di input per l&#39;immissione e la convalida dell&#39;OTP.

![Ottieni regola OTP](/help/forms/assets/get-otp-rule.png)

Nel **Pannello di convalida** è configurata una regola sul pulsante Convalida. L&#39;integrazione API viene utilizzata per convalidare l&#39;OTP immesso nel campo **Enter OTP**. Se la convalida ha esito positivo, viene attivato un evento **Dispatch** denominato **LoggedIn** con il payload dell&#39;evento contenente la risposta API.

![Nella regola evento trigger](/help/forms/assets/trigger-event-rule.png)

A livello di modulo, una regola è configurata per l&#39;ascolto dell&#39;evento **LoggedIn**. Quando questo evento viene attivato, la regola visualizza il messaggio di reindirizzamento e porta l’utente alla pagina del dashboard.

![regola evento di invio](/help/forms/assets/dispatch-event-rule.png)

Quando l’utente invia il modulo con le credenziali corrette e un OTP valido, l’accesso ha esito positivo e l’utente viene reindirizzato al proprio dashboard.

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

## Risorse aggiuntive

{{see-also-rule-editor}}
