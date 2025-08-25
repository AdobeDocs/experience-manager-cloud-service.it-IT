---
title: Introduzione alla creazione di moduli adattivi
description: AEM Forms fornisce un’interfaccia semplice, ma potente per l’authoring dei moduli adattivi. Fornisce una serie di componenti e strumenti che è possibile utilizzare per creare i moduli.
content-type: reference
topic-tags: author, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Adaptive Forms, Foundation Components
exl-id: 16f86dae-86fb-481b-8978-b8898705ed7e
role: User, Developer
source-git-commit: 4c42888af1e846c011242af2c328e553bb811cfd
workflow-type: tm+mt
source-wordcount: '2496'
ht-degree: 91%

---

# Editor di moduli adattivi {#introduction-to-authoring-adaptive-forms}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/getting-started/introduction-forms-authoring.html) |
| AEM as a Cloud Service | Questo articolo |

## Panoramica {#overview}

I moduli adattivi consentono di creare moduli coinvolgenti e reattivi, che si rivelano, inoltre, dinamici e adattivi. [!DNL AEM Forms] fornisce un’interfaccia utente intuitiva e componenti pronti all’uso per la creazione e l’utilizzo dei moduli adattivi. È possibile scegliere di creare un modulo adattivo basato su un modello o schema di modulo o senza un modello di modulo. È importante scegliere con attenzione il modello di modulo, che deve risultare adatto non solo alle proprie esigenze, ma deve consentire di accrescere gli investimenti e le risorse infrastrutturali esistenti. Per creare un modulo adattivo, è possibile scegliere tra le seguenti opzioni:

* **Utilizzo di un modello dati modulo (FDM)**
  [Integrazione dei dati](data-integration.md) consente di integrare entità e servizi da diverse origini dati in un modello dati modulo (FDM) che è possibile utilizzare per creare Forms adattivo. Scegli Modello dati modulo (FDM) se il modulo adattivo che stai creando richiede il recupero e la scrittura di dati da e verso più origini dati.

* **Utilizzo di un modello di modulo XDP**
Si tratta di un modello di modulo ideale per gli investimenti in moduli basati su XFA o XDP. Fornisce un modo diretto per convertire i moduli basati su XFA in moduli adattivi. Eventuali regole XFA esistenti vengono mantenute nei moduli adattivi associati. I moduli adattivi risultanti supportano i costrutti XFA, ad esempio convalide, eventi, proprietà e pattern.

* **Utilizzo di una definizione di schema XML (XSD) o di uno schema JSON**
Gli schemi XML e JSON rappresentano la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end della tua organizzazione. È possibile associare lo schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema sono disponibili per l’uso nella scheda Oggetti modello dati del browser dei contenuti durante la creazione di moduli adattivi.

* **Non utilizzare nessun modello di modulo ossia creare senza un modello di modulo**
I moduli adattivi creati con questa opzione non utilizzano alcun modello di modulo. I dati XML generati da tali moduli hanno una struttura piatta con campi e valori corrispondenti.

  >[!NOTE]
  >
  > È possibile modificare le proprietà del modello di modulo dall’editor di moduli adattivi o dall’editor di modelli di moduli adattivi. Per ulteriori informazioni, consulta [Modificare le proprietà del modello di modulo di un modulo adattivo](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model).

Per creare un modulo adattivo, consulta [Creazione di un modulo adattivo](creating-adaptive-form.md).

## Interfaccia utente per la creazione di moduli adattivi {#adaptive-form-authoring-ui}

L’interfaccia utente touch per la creazione di moduli adattivi è intuitiva e fornisce:

* Funzione di trascinamento
* Componenti standard per moduli
* Archivio integrato per le risorse

Quando crei o modifichi un modulo adattivo esistente, utilizzi i seguenti elementi dell’interfaccia utente:

* [Barra laterale](#sidebar)
* [Barra degli strumenti della pagina](#page-toolbar)
* [Barra degli strumenti del componente](#component-toolbar)
* [Pagina Modulo adattivo](#af-page)

<!-- ![Adaptive Form authoring UI](assets/formeditor.png)

**A.** Sidebar **B.** Page toolbar **C.** Adaptive Form page -->

### Barra laterale {#sidebar}

La barra laterale consente di:

* Cercare, visualizzare e utilizzare le risorse nell’archivio Digital Asset Management (DAM) di AEM.
* Vedere il contenuto del modulo, ad esempio pannelli, componenti, campi e layout.
* Aggiungere componenti al modulo.
* Modificare le proprietà dei componenti.

![Barra laterale](assets/sidebar-comps.png)

**A.** Browser dei contenuti **B.** Browser delle proprietà **C.** Browser delle risorse **D.** Browser delle componenti

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

La barra laterale comprende i seguenti browser:

* **Browser dei contenuti**
Nel browser dei contenuti puoi visualizzare:

   * **Oggetti modulo**
Mostra la gerarchia degli oggetti del modulo. L’autore può passare a un componente specifico del modulo toccando quell’elemento nella struttura degli oggetti modulo. L’autore può cercare gli oggetti e riorganizzarli da questa struttura.

   * **Oggetti modello dati**
Consente di visualizzare la gerarchia del modello di modulo.
Consente di trascinare e rilasciare gli elementi del modello di modulo sul modulo adattivo. Gli elementi aggiunti vengono automaticamente convertiti in componenti modulo mantenendo le proprietà originali. È possibile visualizzare gli oggetti del modello dati quando il modulo utilizza lo schema XML, lo schema JSON o il modello XDP.

* **Browser proprietà**

  Consente di modificare le proprietà di un componente. Le proprietà cambiano in base a un componente. Per visualizzare le proprietà del contenitore Modulo adattivo:

  Seleziona un componente, quindi seleziona ![livello campo](assets/Smock_SelectContainer_18_N.svg) > **[!UICONTROL Contenitore modulo adattivo]**, quindi seleziona ![proprietà](assets/Smock_Wrench_18_N.svg).

* **Browser risorse**

  Separa contenuti di tipi diversi come immagini, documenti, pagine, filmati e così via.

* **Browser componenti**

  Include i componenti che è possibile utilizzare per creare un modulo adattivo. È possibile trascinare i componenti dal modulo adattivo per aggiungere elementi al modulo e configurare gli elementi aggiunti in base ai requisiti. La tabella seguente descrive i componenti elencati nel browser Componenti.

<table>
 <tbody>
  <tr>
   <th><strong>Componente</strong></th>
   <th><strong>Funzionalità</strong></th>
  </tr>
  <tr>
   <td>Blocco Adobe Sign</td>
   <td>Aggiunge un blocco di testo con segnaposto per la compilazione dei campi durante l’accesso tramite Adobe Sign.</td>
  </tr>
  <tr>
   <td>Pulsante</td>
   <td>Aggiunge un pulsante che è possibile configurare per eseguire azioni quali salvataggio, ripristino, passare a elemento precedente/successivo e così via.</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>Aggiunge la convalida CAPTCHA utilizzando il servizio Google reCAPTCHA.</td>
  </tr>
  <tr>
   <td>Grafico</td>
   <td>Aggiunge un grafico che è possibile utilizzare in moduli adattivi e documenti per la rappresentazione visiva di dati bidimensionali in pannelli e righe di tabella ripetibili.</td>
  </tr>
  <tr>
   <td>Casella di selezione</td>
   <td>Aggiunge una casella di controllo.</td>
  </tr>
  <tr>
   <td>Campo immissione data</td>
   <td>Utilizza il componente Campo di immissione data nel modulo per consentire ai clienti di compilare il giorno, il mese e l’anno in tre caselle separate. Puoi personalizzare l’aspetto del componente e modificare il formato della data. Ad esempio, puoi lasciare che i tuoi clienti inseriscano le date in formato MM/GG/AAAA o GG/MM/AAAA.</td>
  </tr>
  <tr>
   <td>Selettore data</td>
   <td>Aggiunge un campo di calendario per scegliere una data.</td>
  </tr>
  <tr>
   <td>Frammento di documento</td>
   <td>Consente di aggiungere componenti riutilizzabili di una corrispondenza.</td>
  </tr>
  <tr>
   <td>Gruppo di frammenti di documenti</td>
   <td>Consente di aggiungere un gruppo di frammenti di documento correlati che è possibile utilizzare in un modello di lettera come una singola unità.</td>
  </tr>
  <tr>
   <td>Elenco a discesa</td>
   <td>Aggiunge un elenco a discesa, a selezione singola o multipla</td>
  </tr>
  <tr>
   <td>E-mail</td>
   <td><p>Aggiunge un campo per acquisire l’indirizzo e-mail. Il componente E-mail, per impostazione predefinita, convalida gli indirizzi e-mail utilizzando la seguente espressione regolare.</p> <p><code>^[a-zA-Z0-9.!#$%&amp;'*+/=?^_&grave;{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>Allegato file</td>
   <td><p>Aggiunge un pulsante che consente agli utenti di sfogliare e allegare documenti di supporto a un modulo.</p> <p><strong>Nota: </strong>il componente Allegato file supporta un set predefinito di formati di file in moduli adattivi abilitati per Adobe Sign. Per ulteriori informazioni, consulta <a href="https://helpx.adobe.com/it/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">Formati di file supportati</a>.</p> </td>
  </tr>
  <tr>
   <td>Elenco allegato file</td>
   <td>Aggiunge un campo che elenca tutti gli allegati caricati utilizzando il componente Allegato file.</td>
  </tr>
  <tr>
   <td>Piè di pagina<br /> </td>
   <td>Aggiunge l’intestazione di pagina che in genere include il logo di una società, il titolo del modulo e il riepilogo.<br /> </td>
  </tr>
  <tr>
   <td>Intestazione</td>
   <td>Aggiunge il piè di pagina che in genere include informazioni sul copyright e collegamenti ad altre pagine. </td>
  </tr>
  <tr>
   <td>Immagine</td>
   <td>Consente di inserire un'immagine.</td>
  </tr>
  <tr>
   <td>Scelta dell'immagine</td>
   <td>Consente ai clienti di selezionare un’immagine per fornire informazioni. Puoi utilizzare le informazioni per fornire servizi personalizzati ai tuoi clienti.</td>
  </tr>
  <tr>
   <td>Pulsante Successivo</td>
   <td>Aggiunge un pulsante per passare al pannello successivo in un modulo.</td>
  </tr>
  <tr>
   <td>Casella numerica</td>
   <td>Aggiunge un campo per l’acquisizione di valori numerici</td>
  </tr>
  <tr>
   <td>Stepper numerico</td>
   <td>Utilizza l’opzione Stepper numerico nel modulo per consentire ai clienti di immettere un valore numerico che può aumentare o diminuire in base a un passaggio predefinito.</td>
  </tr>
  <tr>
   <td>Pannello</td>
   <td><p>Aggiunge un pannello o un sottopannello.</p> <p>Puoi anche aggiungere un componente pannello dalla barra degli strumenti del pannello principale utilizzando il pulsante <span class="uicontrol">Aggiungi pannello</code>  pulsante. Allo stesso modo, puoi aggiungere una barra degli strumenti specifica per il pannello utilizzando il pulsante <span class="uicontrol">Aggiungi barra degli strumenti del</code> pulsante. È possibile configurare la posizione della barra degli strumenti del pannello utilizzando la finestra di dialogo Modifica pannello.</p> </td>
  </tr>
  <tr>
   <td>Casella password</td>
   <td>Aggiunge un campo per l’acquisizione di una password.</td>
  </tr>
  <tr>
   <td>Pulsante Indietro</td>
   <td>Aggiunge un pulsante necessario agli utenti per tornare alla pagina o al pannello precedente.</td>
  </tr>
  <tr>
   <td>Pulsante di scelta</td>
   <td>Aggiunge pulsanti di scelta.</td>
  </tr>
  <tr>
   <td>Pulsante Ripristina</td>
   <td>Aggiunge un pulsante per ripristinare i campi del modulo.</td>
  </tr>
  <tr>
   <td>Pulsante di salvataggio</td>
   <td>Aggiunge un pulsante per salvare i dati del modulo.</td>
  </tr>
  <tr>
   <td>Firma scarabocchio</td>
   <td>Aggiunge un campo per l’acquisizione delle firme scarabocchio.</td>
  </tr>
  <tr>
   <td>Separatore</td>
   <td>Abilita la separazione visiva dei pannelli nel modulo.</td>
  </tr>
  <tr>
   <td>Passaggio di firma</td>
   <td>Visualizza le informazioni fornite nel modulo e i campi firma che consentono all’utente di verificare e firmare il modulo.</td>
  </tr>
  <tr>
   <td>Testo</td>
   <td>Consente di specificare testo statico.</td>
  </tr>
  <tr>
   <td>Pulsante Invia</td>
   <td>Aggiunge un pulsante di invio per inoltrare il modulo all’azione di invio configurata.</td>
  </tr>
  <tr>
   <td>Passaggio di riepilogo</td>
   <td>Invia il modulo e visualizza il testo di riepilogo specificato dagli autori dopo l’invio del modulo. </td>
  </tr>
  <tr>
   <td>Interruttore</td>
   <td>Aggiunge un interruttore che esegue un’azione di mostra/nascondi o attivazione/disattivazione. Non è possibile aggiungere più di due opzioni nel componente Interruttore. Poiché un interruttore può avere solo due valori, on o off, obbligatorio non è applicabile. Almeno un valore viene salvato indipendentemente dall’input dell’utente. <br /> </td>
  </tr>
  <tr>
   <td>Tabella</td>
   <td>Aggiunge una tabella che consente di organizzare i dati in righe e colonne. </td>
  </tr>
  <tr>
   <td>Telefono</td>
   <td><p>Aggiunge un campo per acquisire il numero di telefono. Il componente Telefono permette agli autori di configurare uno dei seguenti tipi di numeri di telefono: Ciascun tipo è associato a un'espressione regolare predefinita per la convalida.</p>
    <ul>
     <li>Tipo International è convalidato da <code>^[+][0-9]{0,14}$</code>.</li>
     <li>Il tipo USPhoneNumber viene convalidato da <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>Il tipo UKPhoneNumber viene convalidato da <code>text{'+'99 999 999 9999}</code>.</li>
     <li>Il tipo personalizzato non fornisce un pattern di convalida predefinito. Prende il valore dell'ultimo tipo di numero di telefono selezionato. È inoltre possibile specificare un pattern di convalida personalizzato.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Condizioni d’uso<br /> </td>
   <td>Aggiunge un campo che gli autori possono utilizzare per specificare i termini e le condizioni che gli utenti devono leggere prima di compilare il modulo.</td>
  </tr>
  <tr>
   <td>Casella di testo </td>
   <td><p>Aggiunge una casella di testo in cui l’utente può specificare le informazioni richieste. </p> <p>Per impostazione predefinita, il componente Casella di testo accetta solo testo normale. È possibile abilitare un componente Casella di testo per accettare il testo RTF. Un componente testo RTF fornisce opzioni per aggiungere intestazioni, modificare gli stili dei caratteri (grassetto, corsivo, sottolineare i caratteri), creare elenchi ordinati e non ordinati, modificare lo sfondo del testo e il colore del testo e aggiungere collegamenti ipertestuali. Per abilitare il testo RTF per una casella di testo, attiva l’opzione<strong> Consenti RTF</strong> nelle proprietà del componente.</p> </td>
  </tr>
  <tr>
   <td>Titolo</td>
   <td>Specifica un titolo per il modulo adattivo.</td>
  </tr>
  <tr>
   <td>Passaggio verifica</td>
   <td><p>Aggiunge un segnaposto per visualizzare il modulo compilato per la verifica da parte dell’utente.</p> <p><strong>Nota</strong>: il modulo adattivo contenente il componente Verifica non supporta gli utenti anonimi. Inoltre, si sconsiglia di utilizzare il componente Verifica in un frammento di modulo adattivo.</p> </td>
  </tr>
 </tbody>
</table>

### Barra degli strumenti della pagina {#page-toolbar}

La barra degli strumenti della pagina in alto contiene opzioni che consentono di visualizzare l’anteprima del modulo, modificarne le proprietà e il layout. È possibile visualizzare l’anteprima del modulo durante la creazione e apportare le modifiche necessarie. Nella barra degli strumenti della pagina sono disponibili le seguenti opzioni:

* **Attiva/Disattiva pannello laterale** ![attiva/disattiva pannello laterale](assets/Smock_RailLeft_18_N.svg): consente di mostrare o nascondere la barra laterale.

* **Informazioni sulla pagina** ![opzioni tema](assets/Smock_Properties_18_N.svg): consente di visualizzare le proprietà della pagina, pubblicare/annullare la pubblicazione di un modulo, avviare un flusso di lavoro del modulo e aprire il modulo nell’interfaccia classica.

* **Emulatore** ![righello](assets/Smock_Devices_18_N.svg): consente di emulare l’aspetto del modulo per diverse dimensioni di visualizzazione, ad esempio tablet e telefoni.

* **Modifica**: consente di selezionare altre modalità, ad esempio: **[!UICONTROL Modifica]**, **[!UICONTROL Stile]**, **[!UICONTROL Sviluppatore]** e **[!UICONTROL Progettazione]**.

   * **Modifica**: consente di modificare le proprietà del modulo e dei suoi componenti. Ad esempio, aggiungere un componente, rilasciare un’immagine e specificare campi obbligatori.
   * **Stile**: consente di definire lo stile dei componenti del modulo. Ad esempio, in modalità stile è possibile selezionare un pannello e specificarne il colore di sfondo.

   * **Sviluppatore**: consente a uno sviluppatore di:

      * Scoprire di quali moduli sono composti.
      * Eseguire il debug di ciò che sta accadendo dove e quando, che a sua volta aiuta a risolvere i problemi.

      * **Design**. Consente di abilitare o disabilitare i componenti personalizzati o i componenti predefiniti non elencati nella barra laterale.

* **Anteprima**: consente di visualizzare un’anteprima dell’aspetto del modulo quando viene pubblicato.

### Barra degli strumenti del componente {#component-toolbar}

![Barra degli strumenti del componente nell’interfaccia touch](assets/component-toolbar.png)

Quando selezioni un componente, viene visualizzata una barra degli strumenti che consente di utilizzarlo. Sono disponibili opzioni per tagliare, incollare, spostare e specificare le proprietà dei componenti. Le opzioni disponibili sono:

A.**Configura**: quando selezioni **[!UICONTROL Configura]**, le proprietà del componente sono visibili nella barra laterale. La configurazione di queste proprietà ti consente di personalizzare l’esperienza di acquisizione dei dati. Puoi modificare il nome dell’elemento del componente, specificare il testo dell’etichetta nel campo Titolo del componente. Il nome dell’elemento consente di acquisire i valori immessi dall’utente utilizzando il componente. Nelle proprietà del componente, specifichi il comportamento del componente e gestisci l’input dell’utente. Configura le proprietà nella barra laterale per acquisire i dati utente e utilizzalo per un’ulteriore elaborazione. Le proprietà per il contenitore Modulo adattivo consentono di specificare le librerie client, i layout, i temi, le impostazioni del documento di record, salvare le impostazioni, le impostazioni di invio e le impostazioni dei metadati.

B.**Copia**: é possibile utilizzare l’opzione Copia per copiare un componente e incollarlo in altre posizioni del modulo Quando incolli un componente, il componente incollato ottiene un nuovo nome di elemento ma mantiene le proprietà del componente copiato.

C.**Taglia**: é possibile utilizzare l’opzione Taglia per spostare un componente da una posizione all’altra nel modulo adattivo.

D. **Elimina**: consente di eliminare il componente dal modulo.

E. **Inserisci**: consente di inserire un componente sopra il componente selezionato.

F. **Incolla**: consente di incollare il componente tagliato o copiato utilizzando le opzioni descritte in precedenza.

G. **Modifica regole**: consente di aprire l’editor di regole. Per ulteriori informazioni, <!-- see [Rule Editor](rule-editor.md). -->

H. **Gruppo**: consente di selezionare più componenti se si desidera tagliare, copiare o incollare più componenti contemporaneamente.

I. **Elemento principale**: consente di selezionare l’elemento principale di un componente. Ad esempio, un campo di testo si trova all’interno di una sottosezione, che si trova in una sezione. La sezione si trova nel pannello principale della guida e il contenitore Modulo adattivo è l’elemento principale di un pannello principale della guida. Per un componente, è possibile visualizzare tutte le opzioni con la gerarchia ordinata dal basso verso l’alto.

Se ad esempio si seleziona **[!UICONTROL Elemento padre]** per una casella di testo, è possibile visualizzare:

* Sottosezione
* Sezione
* guideRootPanel
* Contenitore Modulo adattivo

J. **Altri**: fornisce ulteriori opzioni per lavorare con il componente selezionato.

* Visualizza espressione SOM
* Salva un pannello come frammento (solo per i pannelli)
* Aggiungi pannello secondario (solo per pannelli)
* Aggiungi barra degli strumenti del pannello (solo per i pannelli)
* Sostituisci (non per pannelli)

### Pagina Modulo adattivo {#af-page}

La pagina Modulo adattivo è il modulo effettivo. È come qualsiasi altra pagina WCM modellata come il componente WCM `cq:Page`. L’immagine seguente mostra la struttura del contenuto di un tipico Modulo adattivo.

![Struttura del contenuto di una pagina WCM per Modulo adattivo](assets/afstructure.png)

La struttura del contenuto contiene in genere i seguenti componenti primari:

* **guideContainer**: il livello principale di un modulo adattivo, contrassegnato come **[!UICONTROL Inizio del Modulo adattivo]** nell’interfaccia utente del Modulo adattivo. In questo componente puoi specificare:

   * *Layout mobile del Modulo adattivo*: definisce l’aspetto del modulo su dispositivi mobili.
   * *Pagina di ringraziamento*: definisce la pagina in cui l’utente viene reindirizzato dopo l’invio del modulo.
   * *Invia azione*: definisce la modalità di elaborazione del modulo sul server dopo l’invio del modulo da parte dell’utente.
   * *Attribuzione stile*: specifica il percorso del file CSS utilizzato per personalizzare l’aspetto del modulo.

* **rootPanel:** pannello principale di un modulo adattivo. Può contenere pannelli secondari sotto il nodo elementi. A ogni pannello, incluso il pannello principale, può essere associato un layout. Il layout del pannello determina il layout del modulo. Ad esempio, nel layout Pannello a soffietto, i relativi elementi vengono disposti come passaggi del Pannello a soffietto.

* **Barra degli strumenti:** a un contenitore Modulo adattivo è associata una barra degli strumenti globale, che è globale per il modulo. Questa barra degli strumenti può essere aggiunta utilizzando **[!UICONTROL Aggiungi barra degli strumenti]** nella barra di modifica, che consente agli autori di aggiungere azioni come Invia, Salva, Ripristina e così via.

* **Risorse:** questo nodo contiene informazioni aggiuntive utilizzate per la creazione dei moduli. Ad esempio, dettagli del modello di modulo, localizzazione e così via.

## Assistente AI in AEM

Per i clienti che hanno [completato i criteri dei prerequisiti](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access), l&#39;Assistente per l&#39;intelligenza artificiale in AEM è disponibile per gli utenti della loro organizzazione. Consulta [Assistente AI in AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).

## Consulta anche {#see-also}

{{see-also}}
