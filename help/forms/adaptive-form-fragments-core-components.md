---
title: Cosa sono i frammenti di moduli adattivi?
description: Forms adattivo fornisce un meccanismo per creare un segmento di modulo, ad esempio un pannello o un gruppo di campi, da utilizzare in qualsiasi modulo adattivo. Puoi anche salvare un pannello esistente come frammento.
topic-tags: author
keywords: Aggiungere frammenti di moduli adattivi, frammenti di moduli adattivi, creare un frammento di modulo, aggiungere un frammento a un modulo adattivo, gestire i frammenti
feature: Adaptive Forms, Core Components
exl-id: 3a9ad1b7-2f6f-4ca9-a1c9-549c4238c59e
role: User, Developer
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 12%

---

# Creare e utilizzare frammenti di Forms adattivi in un modulo adattivo basato su componenti core {#adaptive-form-fragments}


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service (Componenti core) | Questo articolo |
| AEM as a Cloud Service (Componenti di base) | [Fai clic qui](/help/forms/adaptive-form-fragments.md) |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/adaptive-form-fragments.html) |

Anche se ogni modulo è progettato per uno scopo specifico, nella maggior parte dei moduli sono presenti alcuni segmenti comuni, ad esempio per fornire dati personali come nome e indirizzo, dettagli sulla famiglia e dettagli sul reddito. Gli sviluppatori di moduli devono creare questi segmenti comuni ogni volta che viene creato un nuovo modulo.

L’Adaptive Forms fornisce un comodo meccanismo per creare segmenti di modulo una sola volta, ad esempio un pannello o un gruppo di campi, e riutilizzarli in Adaptive Forms. Questi segmenti riutilizzabili e autonomi sono denominati frammenti di modulo adattivo.

I frammenti di modulo si integrano perfettamente in più moduli, semplificando la creazione di moduli coerenti e dall’aspetto professionale. I Frammenti di modulo garantiscono riutilizzabilità, standardizzazione e coerenza del brand attraverso la funzionalità “cambia una volta e rifletti ovunque”. Migliora la manutenzione e l’efficienza, poiché gli aggiornamenti apportati in un’unica posizione vengono propagati automaticamente in tutti i moduli che utilizzano questi frammenti.

È possibile aggiungere più volte un frammento a un documento e utilizzare le proprietà di associazione dati dei relativi componenti per collegarlo a diverse origini dati o schemi. Ad esempio, puoi utilizzare lo stesso frammento di indirizzo per un indirizzo permanente, di comunicazione e di fatturazione e collegarlo a campi diversi di un’origine dati o di uno schema.

>[!NOTE]
>
> Puoi personalizzare facilmente l&#39;esperienza del frammento per gli utenti con la [finestra di dialogo per configurazione e finestra di dialogo per progettazione del componente Frammento di modulo](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/adaptive-form-fragment).

## Creare un frammento di modulo adattivo {#create-a-fragment}

Puoi creare un frammento di modulo adattivo da zero o salvare un pannello in un modulo adattivo esistente come frammento. Per creare un frammento di modulo:

1. Accedi all&#39;istanza di AEM Forms all&#39;indirizzo https://[*hostname*]:[*port*]/aem/forms.html.
1. Fai clic su **Crea > Frammento di modulo adattivo**.

   ![Crea frammento di modulo adattivo](/help/forms/assets/adaptive-form-fragment.png)

1. Specifica titolo, nome, descrizione e tag per il frammento. Assicurati di specificare un nome univoco per il frammento. Se esiste un altro frammento con lo stesso nome, il frammento non viene creato.
1. Selezionare un modello di modulo. Forms Puoi creare un frammento di modulo per Forms adattivo basato su Componenti core o su Componenti di base. Per creare un frammento di modulo per moduli basati su Componenti core, seleziona un modello basato su Componenti core.

   Quando crei un frammento di modulo per moduli basati su Componenti core, utilizza l’opzione Seleziona tema modulo per selezionare un tema basato su Componenti core.

1. Fai clic per aprire la scheda **Modello modulo** e dal menu a discesa **Seleziona da** seleziona uno dei seguenti modelli per il frammento:

   ![Mostra il tipo di modello nella scheda Modello modulo](assets/create-af-1-1.png)

   * **Nessuno**: specifica di creare il frammento da zero senza utilizzare alcun modello di modulo.

     >[!NOTE]
     >
     > In Adaptive Forms puoi utilizzare più volte un singolo frammento di modulo (basato su Componenti core). Supporta sia frammenti di modulo basati su nessuno che frammenti di modulo basati su schema.

   * **Schema**: specifica di creare il frammento utilizzando uno schema XML o JSON caricato in AEM Forms. Puoi caricare o selezionare dagli schemi XML o JSON disponibili come modello di modulo per il frammento. Quando si seleziona uno schema XML, è inoltre possibile creare un frammento di modulo adattivo selezionando un complexType presente nello schema selezionato dalla casella a discesa **[!UICONTROL Tipo complesso dello schema XML]**. Quando selezioni uno schema JSON, puoi anche creare un frammento di modulo adattivo selezionando una definizione di schema presente nello schema selezionato dalla casella a discesa **[!UICONTROL Definizioni schema JSON]**.
   * **Modello dati modulo**: specifica di creare il frammento utilizzando un modello dati modulo (FDM). È possibile creare un frammento di modulo adattivo basato su un solo oggetto modello dati in un modello dati modulo (FDM). Espandi il menu a discesa Definizioni modello dati modulo (FDM). Elenca tutti gli oggetti modello dati nel modello dati del modulo specificato (FDM). Seleziona un oggetto modello dati dall’elenco.

   ![Modello dati modulo (FDM)](assets/create-af-3.png)

1. Fai clic su **Crea**, quindi su **Apri** per aprire il frammento, con un modello predefinito, in modalità di modifica. In modalità di modifica puoi aggiungere qualsiasi componente Modulo adattivo al frammento.

<!-- For information about Adaptive Form components, see [Introduction to authoring Adaptive Forms](../../forms/using/introduction-forms-authoring.md). --> Inoltre, se hai selezionato uno schema XML come modello di modulo per il frammento, nel Finder contenuto viene visualizzata una nuova scheda che mostra la gerarchia del modello di modulo. Consente di trascinare gli elementi del modello di modulo sul frammento. <!--The added form-model elements get converted into form components while retaining the original properties from the associated XDP or XSD. -->

Una volta creato il frammento di modulo adattivo basato su uno schema o un modello di dati del modulo (FDM), gli elementi del modello di dati del modulo (FDM) o dello schema vengono visualizzati nella scheda Origini dati del browser Contenuto nell’editor di moduli adattivi. Puoi trascinare gli elementi del modello di modulo sul frammento. Gli elementi del modello modulo aggiunti vengono convertiti in componenti modulo mantenendo le proprietà originali dallo schema associato.


## Aggiungere un frammento a un modulo adattivo {#insert-a-fragment-in-an-adaptive-form}

Per aggiungere un frammento di modulo adattivo a un modulo adattivo:

1. Apri il modulo adattivo in modalità di modifica.
1. Aggiungi al modulo il componente **Frammento modulo adattivo**.
1. Apri la finestra di dialogo Configurazione del componente **Frammento di modulo adattivo**.
1. Seleziona il **Riferimento frammento** nella scheda **Base**. Vengono visualizzati tutti i frammenti di Forms adattivo disponibili per il modulo, a seconda del modello del modulo.

1. Seleziona un frammento di modulo adattivo nel componente **Frammento di modulo adattivo** del modulo adattivo.

   ![seleziona l&#39;opzione Frammenti di modulo adattivi](/help/forms/assets/adaptive-form-fragment-basic.png)

<!-- 
   >[!NOTE]
   >
   >The Adaptive Form fragment is not enabled for authoring from within the Adaptive Form. Moreover, you cannot use an XSD-based fragment in a JSON-based Adaptive Form and the opposite way. 
-->

Il frammento di modulo adattivo viene aggiunto facendo riferimento al modulo adattivo e rimane sincronizzato con il frammento di modulo adattivo autonomo. Ciò implica che qualsiasi modifica apportata al frammento del modulo adattivo si rifletta su tutte le istanze in cui il frammento è incorporato in Adaptive Forms.

<!--### Embed a fragment in Adaptive Form {#embed-a-fragment-in-adaptive-form}

You can choose to embed an Adaptive Form fragment in an Adaptive Form by clicking the ![Embed](assets/Smock_Import_18_N.svg) icon the panel toolbar of the added fragment

The embedded fragment is no longer linked with the standalone fragment. You can edit the components in the embedded fragment from within the Adaptive Form.-->

<!-- 
## Configure fragment appearance {#configure-fragment-appearance}

Any fragment you insert in Adaptive Forms appears as a placeholder image. The placeholder displays titles of up to a maximum of ten child panels in the fragment. You can configure AEM Forms to show the complete fragment instead of the placeholder image.

Perform the following steps to show complete fragments in forms:

1. Go to AEM web console configuration page at https:[*host*]:[*port*]/system/console/configMgr.

1. Search and click **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** to open it in edit mode.
1. Disable **[!UICONTROL Enable Placeholder in place of Fragment]** checkbox to show complete fragments rather than the placeholder image.

-->

### Utilizzo di frammenti all’interno di frammenti {#using-fragments-within-fragments}

Puoi creare frammenti di modulo adattivo nidificati, il che significa che puoi aggiungere un frammento in un altro frammento e avere una struttura di frammenti nidificata.

### Utilizzo di un frammento di modulo più volte in un modulo adattivo {#using-form-fragment-mutiple-times-in-af}

È possibile utilizzare più volte un frammento di modulo basato su schema e non basato su elementi singoli in un modulo adattivo per salvare i dati in modo univoco per ogni campo dei frammenti di modulo. Ad esempio, puoi utilizzare un frammento di modulo indirizzo per raccogliere i dettagli dell’indirizzo per indirizzi permanenti, di comunicazione e di presentazione in un modulo di richiesta di prestito.

![utilizzo di più frammenti nel modulo adattivo](/help/forms/assets/using-multiple-fragment-af.gif)

## Supporto della mappatura automatica per frammenti in un modulo adattivo

Quando crei un frammento di modulo adattivo basato su una definizione di schema JSON, può essere riutilizzato automaticamente nei moduli creati dallo stesso schema.
Se trascini un oggetto schema o qualsiasi oggetto nidificato che corrisponde al mapping di definizione dello schema JSON di un frammento di modulo adattivo, l’oggetto viene sostituito dal frammento di modulo adattivo corrispondente. Invece di aggiungere un pannello con singoli campi, il modulo inserisce il frammento di modulo adattivo mappato.

![Trascina un frammento](/help/forms/assets/fragment.png)

Puoi anche trascinare un frammento di modulo adattivo associato dalla libreria Frammento modulo adattivo in AEM Content Finder e fornire il riferimento di associazione corretto dalla finestra di dialogo Modifica componente del pannello Frammento modulo adattivo.

## Gestire i frammenti {#manage-fragments}

Puoi eseguire diverse operazioni sui frammenti di moduli adattivi utilizzando l’interfaccia utente di AEM Forms.

1. Passa a `https://[hostname]/aem/forms.html`.

1. Fai clic su **Seleziona** nella barra degli strumenti dell&#39;interfaccia utente di AEM Forms e seleziona un frammento di modulo adattivo. La barra degli strumenti mostra le seguenti operazioni che è possibile eseguire sul frammento di modulo adattivo selezionato.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operazione</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>Modifica</p> </td>
   <td><p>Apre il frammento di modulo adattivo selezionato in modalità di modifica.<br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Anteprima</p> </td>
   <td><p>Fornisce opzioni per visualizzare in anteprima il frammento come HTML o come anteprima personalizzata unendo i dati di un file XML con il frammento. Per ulteriori informazioni, vedere <a>Anteprima modulo</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Scarica</p> </td>
   <td><p>Scarica il frammento selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Avvia/Gestisci revisione</p> </td>
   <td><p>Consente di avviare e gestire una revisione del frammento selezionato. Per ulteriori informazioni, vedere <a>Creazione e gestione delle revisioni</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Aggiungi dizionario</p> </td>
   <td><p>Genera un dizionario per la localizzazione del frammento selezionato. Per ulteriori informazioni, vedere <a>Localizzazione di Forms adattivo</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Pubblica/Annulla pubblicazione</p> </td>
   <td><p>Pubblica o annulla la pubblicazione del frammento selezionato.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Elimina</p> </td>
   <td><p>Elimina il frammento selezionato.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Punti chiave da ricordare quando si lavora con i frammenti {#key-points-to-remember-when-working-with-fragments}

* Assicurati che il nome del frammento sia univoco. Il frammento non viene creato se è presente un frammento con lo stesso nome.
* Qualsiasi espressione, script o stile in un frammento di modulo adattivo autonomo viene mantenuto quando viene inserito per riferimento o incorporato in un modulo adattivo.
* Non è possibile modificare un frammento di modulo adattivo, inserito per riferimento, dall’interno di un modulo adattivo. Per modificare, modifica il frammento del modulo adattivo autonomo.
* Quando pubblichi un modulo adattivo, devi pubblicare i frammenti di modulo adattivo autonomi inseriti per riferimento nel modulo adattivo.
* Quando ripubblichi un frammento di modulo adattivo aggiornato, le modifiche si riflettono nelle istanze pubblicate del modulo adattivo in cui viene utilizzato il frammento.
* Il modulo adattivo contenente il componente Verifica non supporta gli utenti anonimi. Inoltre, non è consigliabile utilizzare il componente Verifica in un frammento di modulo adattivo.

## Frammenti di riferimento {#reference-fragments}

Sono disponibili frammenti per moduli adattivi di riferimento che è possibile utilizzare per creare il modulo.
<!-- For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md). -->



## Consulta anche {#see-also}

{{see-also}}