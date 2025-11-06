---
title: Come si applicano le firme elettroniche a un modulo utilizzando le firme scarabocchio?
description: Scopri come applicare firme elettroniche a un modulo utilizzando le firme scarabocchio.
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 55%

---

# Firma elettronica di un modulo tramite firme a mano{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html) |
| AEM as a Cloud Service | Questo articolo |


È possibile utilizzare il componente **Firma scarabocchio** per disegnare una firma (scarabocchio) in un modulo adattivo. <!-- The Signature step component displays a PDF version of the Adaptive Form. You require a Document of Record option enabled or form template based Adaptive Forms to use the Signature step component. -->

![Finestra di dialogo del segno a mano](assets/scribble-signature.png)

## Varie opzioni disponibili nella finestra Firma

* **A:** Fai clic sull&#39;icona **Pennello pittura** per disegnare la firma su un&#39;area di lavoro.
* **B:** fai clic sull’icona **Cancella** per cancellare la firma nell’area di lavoro.
* **C:** fai clic sull’icona **Geolocalizzazione** per aggiungere la geolocalizzazione insieme alla firma.
* **D:** fai clic sull’icona **Tastiera** per digitare il tuo nome nell’area di lavoro.

Dopo aver selezionato l&#39;icona Fine ![aem_forms_save](assets/aem_forms_save.png) nella finestra Firma a mano a mano, non è possibile modificare la firma. Nel caso in cui desideri modificare la firma, è necessario ignorare quella corrente e riapporla utilizzando l’opzione Pennello/Tastiera.

È possibile selezionare l&#39;icona **Configura** ![configura icona](assets/configure.png) per impostare le proporzioni dell&#39;area di lavoro Firma scarabocchio.

* Quando le proporzioni dell’area di lavoro Firma a mano sono inferiori a 1, le informazioni sulla geolocalizzazione vengono aggiunte nella parte inferiore dell’area di lavoro Firma a mano.
* Quando le proporzioni dell’area di lavoro Firma scarabocchio sono superiori a 1, le informazioni sulla geolocalizzazione vengono aggiunte al lato destro dell’area di lavoro Firma scarabocchio.


![firma a mano libera](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>Le firme vengono sempre salvate in formato PNG.

## Configurare un modulo adattivo per utilizzare la firma scarabocchio {#configure-an-adaptive-form-to-use-scribble-signature}

1. Aprire un modulo adattivo in modalità di modifica.
1. Trascina il componente **Firma scarabocchio** dal browser componenti al modulo adattivo.
1. Seleziona l&#39;icona **Configura** ![configura](assets/configure.png). Apre il browser delle proprietà e visualizza le proprietà del componente Firma scarabocchio. [Configurare le proprietà della firma scarabocchio](#properties-of-scribble-signature-component) come descritto nella sezione successiva.

   ![Firma a mano](/help/forms/assets/scribblesig.png)

1. Seleziona l&#39;icona Fine ![aem_forms_save](assets/aem_forms_save.png) per salvare le modifiche. La firma è stata configurata correttamente.

## Configurare le proprietà del componente Firma scarabocchio

Puoi personalizzare facilmente il componente Firma a mano per i visitatori con la finestra di dialogo per configurazione.

### Scheda Base

![Scheda Base](/help/forms/assets/scribblesig-basic.png)

* **Nome**: è possibile identificare facilmente un componente modulo con il suo nome univoco sia nel modulo che nell’editor di regole, ma il nome non deve contenere spazi o caratteri speciali.

* **Titolo** : con il relativo titolo è possibile identificare facilmente un componente in un modulo e, per impostazione predefinita, il titolo viene visualizzato sopra il componente. Se non aggiungi un titolo, al posto del testo del titolo viene visualizzato il nome del componente.

* **Consenti testo formattato per titolo**: questa funzione permette agli utenti di formattare i titoli in testo normale, incorporando opzioni come il grassetto, il corsivo, il testo sottolineato, vari font, dimensioni dei font, colori e altre opzioni per migliorare la presentazione visiva e la personalizzazione. Offre maggiore flessibilità e controllo creativo nel far risaltare i titoli all’interno di documenti, siti web o applicazioni.\
  Dopo aver selezionato la casella di controllo **Consenti testo formattato per titolo**, le opzioni di formattazione diventano visibili per applicare lo stile al titolo del componente. Per accedere a tutte le opzioni di formattazione disponibili, fai clic sulla scheda ![Icona schermo intero](/help/forms/assets/fullscreen-icon.png).

  ![Supporto testo RTF](/help/forms/assets/richtext-support-title.png)

* **Nascondi titolo**: seleziona l’opzione per nascondere il titolo del componente.
* **Campo obbligatorio** - Selezionare l&#39;opzione per rendere obbligatorio il campo.
* **Messaggio campo obbligatorio** - Il **Messaggio campo obbligatorio** è un messaggio personalizzabile visualizzato agli utenti quando tentano di inviare un modulo senza compilare un campo obbligatorio.
* **Riferimento associazione modello dati** - Un riferimento associazione è un riferimento a un elemento dati archiviato in un&#39;origine dati esterna e utilizzato in un modulo. Il riferimento di binding consente di eseguire un binding dinamico dei dati ai campi del modulo, in modo che il modulo possa visualizzare i dati più aggiornati dell’origine dati. Ad esempio, è possibile utilizzare un riferimento di binding per visualizzare il nome e l’indirizzo di un cliente in un modulo, in base all’ID cliente immesso nel modulo. È inoltre possibile utilizzare il riferimento di binding per aggiornare l’origine dati con i dati immessi nel modulo. In questo modo, AEM Forms consente di creare moduli che interagiscono con origini dati esterne, fornendo un’esperienza utente fluida per la raccolta e la gestione dei dati.
* **Nascondi oggetto** - Selezionare l&#39;opzione per nascondere il componente dal modulo. Il componente rimane accessibile per altri scopi, ad esempio per i calcoli nell’editor di regole. Questa funzione è utile quando devi memorizzare informazioni che non devono essere viste o modificate direttamente dall’utente.
* **Disabilita oggetto** - Selezionare l&#39;opzione per disabilitare il componente. Il componente disabilitato non è attivo o modificabile dall’utente finale. L’utente può visualizzare il valore del campo, ma non può modificarlo. Il componente rimane accessibile per altri scopi, ad esempio per i calcoli nell’editor di regole.
* **Proporzioni** - Le proporzioni in un componente Firma a mano definiscono la relazione proporzionale tra la larghezza e l&#39;altezza.
* **Layout campo** - L&#39;opzione **Layout campo** determina il modo in cui gli elementi del modulo, incluse le etichette (didascalie) e i messaggi di errore, vengono posizionati rispetto al componente. **Didascalia ed errore come parte superiore del widget** posiziona la didascalia (etichetta) del campo e i messaggi di errore sopra il componente. **Eredita dalla configurazione modulo adattivo** utilizza le impostazioni di layout dei campi predefinite specificate nella configurazione del modulo adattivo.
* **Classe CSS** - La **classe CSS** consente di applicare stili personalizzati a un componente assegnando una o più classi CSS definite nel foglio di stile. Consente di personalizzare lo stile e il layout in modo coerente all’interno del modulo adattivo.

### Contenuto della guida

![Scheda Contenuto Guida](/help/forms/assets/scribblesig-help.png)

* **Breve descrizione**: una breve descrizione è una breve spiegazione testuale che fornisce informazioni aggiuntive o chiarimenti sullo scopo di un campo modulo specifico. Aiuta l’utente a capire quale tipo di dati deve essere immesso nel campo e può fornire linee guida o esempi per garantire che le informazioni immesse siano valide e soddisfino i criteri desiderati. Per impostazione predefinita, le descrizioni brevi rimangono nascoste. Abilita l’opzione **Mostra sempre una breve descrizione** per visualizzarla sotto il componente.

* **Mostra sempre una breve descrizione**: abilita l’opzione per visualizzare la descrizione breve sotto il componente.

* **Descrizione lunga** - Si riferisce a informazioni o indicazioni aggiuntive fornite all&#39;utente per aiutarlo a compilare correttamente un campo modulo. Viene visualizzato quando l’utente fa clic sull’icona dell’aiuto (i) posta vicino al componente. Fornisce informazioni più dettagliate rispetto al testo dell’etichetta o del segnaposto di un campo modulo ed è progettato per aiutare l’utente a comprendere i requisiti o i vincoli del campo. Può inoltre offrire suggerimenti o esempi per rendere più semplice e precisa la compilazione del modulo.

### Scheda Accessibilità {#accessibility}

![Scheda Accessibilità](/help/forms/assets/scribblesig-acc.png)

Nella scheda **Accessibilità** è possibile impostare i valori per le etichette di [accessibilità ARIA](https://www.w3.org/WAI/standards-guidelines/aria/) del componente. Sono disponibili varie opzioni per l’utilizzo del testo per l’assistente vocale:

* **Precedenza Reader per schermo** - Precedenza Reader per schermo si riferisce a testo aggiuntivo che deve essere letto dalle tecnologie per l&#39;accessibilità, come le utilità per la lettura dello schermo, utilizzate da persone ipovedenti. Questo testo fornisce una descrizione audio dello scopo del campo modulo e può includere informazioni sul titolo, la descrizione, il nome del campo ed eventuali messaggi rilevanti (testo personalizzato). Il testo dell’assistente vocale consente di garantire l’accesso al modulo da parte di qualsiasi utente, comprese le persone ipovedenti, consentendo di comprendere appieno il campo del modulo e i relativi requisiti.

   * **Testo personalizzato**: seleziona questa opzione per utilizzare il testo personalizzato per le etichette di accessibilità ARIA. Selezionando questa opzione, viene visualizzata la finestra di dialogo Testo personalizzato. Puoi aggiungere informazioni rilevanti nella finestra di dialogo Testo personalizzato.
   * **Descrizione breve**: selezionare questa opzione per utilizzare la descrizione per le etichette di accessibilità ARIA.
   * **Titolo**: seleziona questa opzione per utilizzare il titolo per le etichette di accessibilità ARIA.
   * **Nome**: seleziona questa opzione per utilizzare il nome per le etichette di accessibilità ARIA.
   * **Nessuno**: seleziona questa opzione in caso tu non voglia aggiungere etichette di accessibilità ARIA.

<!--

 * **Element Name**: Specify name of the component.

    * **Title:** Specify unique title of the component.
    * **Template message:** Specify the message to be displayed while the signature PDF is being loaded. Adobe Sign services take some time to prepare and load signature PDF.
    * **Signing Service:** Select the **Scribble Signature** option.

    * **CSS Class**: Specify CSS class of the client library, if any. Adobe recommends using [themes](themes.md) and [in-line styles](inline-style-adaptive-forms.md) instead of CSS Class.
## Sign an Adaptive Form using Scribble Signature {#sign-an-adaptive-form-using-scribble-signature}

1. After you fill an Adaptive Form and reach the Signature Step page, the signature screen is displayed.

   ![Signature screen for EchoSign page](assets/esignscribblesign.jpg)

1. Click **[!UICONTROL Sign]**. The scribble sign dialog appears. Sign the form and click the Done ![aem_forms_save](assets/aem_forms_save.png) icon to save the signature.

   ![Scribble sign dialog](assets/scribblewidget.png)

1. Click complete to finish the signing process.

   ![Complete the signing process](assets/scribblecomplete.jpg)

The signatures are added to the form and the form control moves to the next panel. -->

## Consulta anche {#see-also}

{{see-also}}