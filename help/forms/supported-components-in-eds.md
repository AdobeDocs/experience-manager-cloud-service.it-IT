---
title: Componenti del modulo del servizio AEM Forms Edge Delivery
description: Il servizio AEM Forms Edge Delivery è stato progettato per garantire prestazioni di picco, consentendoti di immaginare il futuro della raccolta dati semplificata e del coinvolgimento degli utenti. L’articolo elenca tutti i componenti Forms disponibili come predefiniti per i moduli EDD.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 1dc4915f0b149ef67dfa22c8d4c6be7538170d38
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 5%

---




# Componenti HTML supportati nella distribuzione Edge del blocco di modulo

AEM Forms Edge Delivery include un blocco modulo. Il blocco di modulo consente di creare facilmente moduli per l&#39;acquisizione e l&#39;archiviazione dei dati acquisiti.

Il blocco Modulo supporta componenti di HTML-5 come testo, e-mail, numero, data e molto altro. Supporta inoltre elementi di area di testo, selezione e set di campi e include funzioni di convalida di input native per HTML-5. Il blocco modulo crea una struttura HTML uniforme per tutti i tipi di campi e i contenitori, garantendo la coerenza. Anche tu [assegnare uno stile ai tipi di campo](https://adobe-rnd.github.io/form-block/customization/styling_form) utilizzando `form.css` file.

## Tipi di input HTML 5 supportati nel blocco modulo

Il blocco modulo supporta una serie di tipi di input HTML 5 ed esegue il rendering dei moduli creati con i componenti core dell’AEM.

Questa tabella illustra la corrispondenza tra i componenti core e i tipi di input HTML-5 in Edge Delivery:

<table>
 <tbody>
  <tr>
   <td><b>Componenti di base</b> </td>
   <td><b>Tipo di ingresso HTML 5</b> </td>
   <td><b>Dettagli</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Contenitore modulo</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">modulo </td>
   <td> Crea un modulo per acquisire gli input dell’utente.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Inserimento testo</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Definisce un campo di immissione testo a riga singola. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Inserimento numero</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">numero</a></td>
   <td>Consente all'utente di immettere un numero. È inoltre possibile aggiungere la convalida incorporata per rifiutare gli input non numerici. Consente all'utente di immettere un numero. È inoltre possibile aggiungere la convalida incorporata per rifiutare gli input non numerici. Inizialmente, il campo di input viene visualizzato come un input numerico. Se un utente applica un pattern di visualizzazione, questo viene modificato in testo per consentire all’autore di applicare la formattazione dei numeri, in quanto HTML 5 non supporta i pattern di visualizzazione. Tuttavia, quando l’utente fa clic su di esso, ritorna a digitare i numeri.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Selettore data</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">data </a></td>
   <td> Crea un campo di input per l’immissione di una data. È possibile immettere la data tramite una casella di testo che convalida la voce oppure tramite un'interfaccia di selezione data dedicata. Inizialmente viene visualizzato il campo di immissione data nativo. Se un utente applica un pattern di visualizzazione, questo viene modificato in testo per consentire all’utente di applicare la formattazione, in quanto HTML 5 non supporta i pattern di visualizzazione. Tuttavia, quando l’utente fa clic su di esso, ritorna a digitare una data.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">Allegato file</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">file</a></td>
   <td> Consente all'utente di scegliere uno o più file dall'archivio del dispositivo. Supporta le convalide avanzate di input dei file, ad esempio i tipi di file accettati, le restrizioni relative alle dimensioni dei file e i limiti minimi/massimi per la selezione dei file. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Elenco a discesa</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">seleziona</a></td>
   <td> Consente agli utenti di selezionare una o più opzioni da un elenco predefinito. Le opzioni possono essere di tipo String, Number o Boolean.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Gruppo di caselle di controllo</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">casella di controllo multipla</a></td>
   <td> Consente agli utenti di selezionare una o più opzioni da un elenco. Vengono generate più caselle di controllo con nomi identici, ognuna corrispondente a un elemento nell'enum. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Gruppo pulsante di opzione</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">radio multipla</a></td>
   <td> Consente a un utente di selezionare un’opzione da un gruppo di opzioni correlate. Più pulsanti di scelta vengono generati con nomi identici, ciascuno corrispondente a un elemento nell'enum.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Pulsante</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">pulsante</a></td>
   <td>Elemento dell’interfaccia utente che consente agli utenti di attivare un’azione quando si fa clic su di essa. </td>
  </tr>
  <tr>
   <td><a href="" https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Pannello</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">set di campi con legenda</a></td>
   <td> Raggruppare le sezioni all'interno di un modulo, dove un elemento *legend* nidificato aggiunge una didascalia per il modulo.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=it">Procedura guidata</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">set di campi</a></td>
   <td>Raggruppa sezioni correlate all'interno di un modulo. Controlla anche la disposizione, supportando le opzioni di visualizzazione per posizionarle in alto o a sinistra. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Testo</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>Un tag p contrassegna un paragrafo. Nel contenuto visivo, i paragrafi sono blocchi di testo separati da righe vuote o da una prima riga rientrata</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Pulsante Invia</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">invia</a></td>
   <td> Elemento dell’interfaccia utente che consente agli utenti di inviare un modulo al server facendo clic su. Se un utente aggiunge una regola di invio a un pulsante, questo funziona come pulsante di invio. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Pulsante Ripristina</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">ripristina</a></td>
   <td>Elemento dell’interfaccia utente che ripristina un modulo facendo clic su. Se un utente aggiunge una regola di ripristino a un pulsante, questo funziona come pulsante di ripristino. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">Input e-mail</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">e-mail</a></td>
   <td> Consente all'utente di immettere e modificare un indirizzo e-mail. Se l’utente aggiunge più attributi, è possibile aggiungere o modificare un elenco di indirizzi e-mail.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Ingresso telefono</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Consente all'utente di immettere e modificare un numero di telefono.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Intestazione</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> intestazione</a></td>
   <td>Include contenuti introduttivi, in genere un gruppo di ausili introduttivi o di navigazione. È supportato all’esterno del contenitore Modulo. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Piè di pagina</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">footer</a></td>
   <td> Contiene informazioni quali dati di copyright o collegamenti a documenti correlati. È supportato all’esterno del contenitore Modulo.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=it">Pannello a soffietto<a></td>
   <td><i>Non ancora supportato nel blocco modulo</i></td>
   <td> Consente di creare sezioni espandibili e comprimibili in un modulo. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=it">Schede orizzontali</a></td>
   <td><i>Non ancora supportato nel blocco modulo</i></td>
   <td>Organizza più sezioni di un modulo in schede separate visualizzate orizzontalmente.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Immagine</a></td>
   <td><i>Non ancora supportato nel blocco modulo</i></td>
   <td> Consente all'utente di includere immagini in un modulo.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Titolo</a></td>
   <td><i>Non ancora supportato nel blocco modulo</i></td>
   <td> Fa riferimento al testo visualizzato nella parte superiore del modulo. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Interruttore</td>
   <td><i>Non ancora supportato nel blocco modulo</i></td>
   <td> Attivazione/disattivazione a due stati che consente all'utente di selezionare due stati, ad esempio l'attivazione o la disattivazione di una funzionalità, di un'impostazione o di una funzionalità.</td>
  </tr>
 </tbody>
</table>


