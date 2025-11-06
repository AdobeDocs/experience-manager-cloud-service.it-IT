---
title: Configurazione dei moduli di ricerca
description: Configurazione di Search Forms per Adobe Experience Manager as a Cloud Service.
exl-id: b06649c4-cc91-44e3-8699-00e90140b90d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 10%

---

# Configurazione dei moduli di ricerca {#configuring-search-forms}

Adobe Experience Manager as a Cloud Service viene fornito con un potente meccanismo di [ricerca](/help/sites-cloud/authoring/search.md).

In combinazione con questo, sono disponibili anche una serie di opzioni predefinite che consentono di filtrare il contenuto. Questi contengono facet predefiniti come **Data di modifica**, **Stato pubblicazione** o **Stato LiveCopy** per consentirti di espandere rapidamente le risorse necessarie.

![ricerca e utilizzo filtro](assets/csf-usage.png)

L’obiettivo di questi elementi è quello di aiutarti a individuare i contenuti in modo rapido e semplice da:

* [Ricerca e filtro](/help/sites-cloud/authoring/search.md#search-and-filter)
* [Selettore della barra](/help/sites-cloud/authoring/basic-handling.md#rail-selector)
* il [browser Assets](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser) (durante la modifica delle pagine)

>[!NOTE]
>
>È possibile configurare il servizio [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md) sottostante.

Utilizzando **Cerca in Forms**, puoi personalizzare ed estendere questi pannelli in base alle tue esigenze specifiche.

**Cerca in Forms** fornisce una selezione predefinita di [predicati](#predicates-and-their-settings) che puoi combinare e definire. Le [finestre di dialogo per la configurazione di questi moduli](#configuring-your-search-forms) sono accessibili tramite:

* **Strumenti**
   * **Generale**
      * **Cerca in Forms**

## Forms predefinito {#default-forms}

La prima volta che accedi alla console **Cerca in Forms** puoi vedere che tutte le configurazioni hanno un simbolo di lucchetto. Ciò indica che la configurazione corrispondente è quella predefinita (predefinita) e non può essere eliminata. Una volta personalizzato e salvato, il blocco scompare. Verrà nuovamente visualizzato quando [elimini la configurazione personalizzata](#deleting-a-configuration-to-reinstate-the-default), nel qual caso verrà ripristinato il valore predefinito (e l&#39;indicatore del lucchetto).

![configurazione della panoramica dei moduli di ricerca](assets/csf-overview.png)

Le configurazioni predefinite (elencate in ordine alfabetico) disponibili sono:

* **Barra di ricerca amministrazione Assets**
* **Editor pagina (ricerca documenti)**
* **Editor pagina (ricerca frammenti esperienza)**
* **Editor pagina (ricerca immagini)**
* **Editor pagina (ricerca manoscritto)**
* **Editor pagina (ricerca pagine)**
* **Editor pagina (ricerca paragrafi)**
* **Editor pagina (ricerca prodotti)**
* **Editor pagina (ricerca Scene7)**
* **Editor pagina (ricerca video)**
* **Barra di ricerca amministrazione progetto**
* **Barra di ricerca traduzione progetto**
* **Barra di ricerca amministrazione siti**
* **Barra di ricerca amministrazione snippet**
* **Barra di ricerca amministrazione Stock**
* **Barra di ricerca modelli per frammenti di contenuto**
* **Barra di ricerca amministrazione progetto**
* **Barra di ricerca traduzione progetto**

>[!NOTE]
>
>Per ulteriori dettagli sui moduli di ricerca relativi alle risorse, vedi [Assets - Facet di ricerca](/help/assets/search-facets.md).


## Predicati e relative impostazioni {#predicates-and-their-settings}

### Predicati {#predicates}

Sono disponibili i seguenti predicati, a seconda della configurazione:

<table>
 <tbody>
  <tr>
   <th>Predicato</th>
   <th>Scopo</th>
   <th>Impostazioni</th>
  </tr>
  <tr>
   <td>Analisi</td>
   <td>Funzionalità di ricerca/filtro nel browser Sites quando vengono visualizzati i dati basati su Analytics. I filtri di ricerca di Analytics si caricano per corrispondere alle colonne di analisi personalizzate mappate.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Stato approvazione</td>
   <td>Cerca in base allo stato di approvazione.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Autore</td>
   <td>Cerca in base all'autore.</td>
   <td>
    <ul>
     <li>Segnaposto</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Ritirato da</td>
   <td>Cercare le risorse estratte da un utente specifico.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Segnaposto</li>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Stato ritiro</td>
   <td>Cercare le risorse con uno stato di pagamento specifico.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Componenti</td>
   <td>Consente all’autore di cercare/filtrare le pagine contenenti un componente specifico. Ad esempio, una raccolta immagini.<br /> </td>
   <td>
    <ul>
     <li>Segnaposto</li>
     <li>Nome proprietà*</li>
     <li>Profondità proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervallo date</td>
   <td>Cerca le risorse create all’interno di un intervallo specificato per una proprietà data. Nel pannello Ricerca, potete specificare le date di inizio e fine.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Segnaposto</li>
     <li>Nome proprietà*</li>
     <li>Testo intervallo (Da)*</li>
     <li>Testo intervallo (A)*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Stato scadenza</td>
   <td>Cerca le risorse in base allo stato di scadenza.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dimensione file</td>
   <td>Filtra le risorse in base alla loro dimensione.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Percorso opzione</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tipo file</td>
   <td>Cerca le risorse in base al tipo di file/mime.</td>
   <td>
    <ul>
     <li>Etichetta campo</li> 
     <li>Nome proprietà*</li>
     <li>Percorso tipo mime</li>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Testo completo</td>
   <td>Predicato di ricerca per ricerche full-text. È mappato con l’operatore "jcr:contains".</td>
   <td>
    <ul>
     <li>Segnaposto</li>
     <li>Nome proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Gruppo</td>
   <td>Predicato di ricerca per gruppo (utilizzato solo all’interno del predicato Insights).</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Filtro nascosto</td>
   <td>Un filtro per proprietà e valore, non visibile all’utente.</td>
   <td>
    <ul>
     <li>Nome proprietà*</li>
     <li>Valore proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Approfondimenti</td>
   <td>Cerca in base a una selezione di parametri di Insights.</td>
   <td>Si tratta di un predicato complesso composto da più predicati:
    <ul>
     <li>Gruppo</li>
     <li>Intervallo</li>
     <li>Opzioni</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Membro di raccolta</td>
   <td>Cercare le risorse che sono membri di una raccolta</td>
   <td>
    <ul>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Proprietà con più valori</td>
   <td>Eseguire ricerche su più valori di una proprietà specificata.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Segnaposto</li>
     <li>Nome proprietà*</li>
     <li>Supporto delimitatore</li>
     <li>Delimitatori di input</li>
     <li>Ignora maiuscole/minuscole</li>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Opzioni</td>
   <td><p>Le opzioni sono nodi di contenuto creati dall’utente.</p> <p>Per ulteriori informazioni, vedere <a href="#addinganoptionspredicate">Aggiunta di un predicato opzioni</a>.</p> </td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Selezione singola</li>
     <li>Aggiungi opzioni</li>
     <li>Manuale</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Proprietà Options</td>
   <td>Cerca in una o più proprietà dell’opzione.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Percorso nodo opzioni</li>
     <li>Profondità proprietà</li>
     <li>Selezione singola</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Stato pagina</td>
   <td>Filtra le pagine in base al loro stato.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà pubblicazione*</li>
     <li>Nome proprietà pagine bloccate*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Percorso</td>
   <td>Filtra in base a un percorso specifico. È possibile specificare più percorsi come opzioni.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Aggiungi percorsi di ricerca</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Browser Percorsi</td>
   <td>Fornisci un browser percorsi per eseguire ricerche in un percorso principale predefinito.</td>
   <td>
    <ul>
     <li>Segnaposto</li>
     <li>Percorso principale</li>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Percorso nascosto</td>
   <td>Un filtro sul percorso, non visibile all’utente.</td>
   <td>
    <ul>
     <li>Nome proprietà (`path`)</li>
     <li>Valore proprietà (`/content/dam`)</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Proprietà</td>
   <td>Cerca in una proprietà specificata.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Segnaposto</li>
     <li>Nome proprietà</li>
     <li>Ricerca parziale</li>
     <li>Ignora maiuscole/minuscole</li>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Stato pubblicazione</td>
   <td>Filtra le risorse in base al loro stato di pubblicazione.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervallo</td>
   <td>Cerca le risorse che si trovano all’interno di un intervallo specificato. Nel pannello Ricerca, potete specificare i valori minimo e massimo per l'intervallo.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Valutazione</td>
   <td>Cerca le risorse in base alla valutazione media.<br /> </td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Percorso opzione</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Data relativa</td>
   <td>Filtra le risorse in base alla data relativa di creazione. Ad esempio, 1 settimana fa, 1 mese fa.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Data relativa</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervallo cursore</td>
   <td>Un predicato di ricerca comune che estende il predicato di intervallo con la funzionalità del cursore. Il valore della proprietà ricercata deve essere compreso tra i limiti del cursore.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Percorso nodo opzioni</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Stato</td>
   <td>Cerca in base allo stato di approvazione e pagamento.</td>
   <td>Si tratta di un predicato complesso composto da più predicati:
    <ul>
     <li>Stato approvazione</li>
     <li>Stato ritiro</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Tag</td>
   <td>Cerca in base ai tag.</td>
   <td>
    <ul>
     <li>Lavello da campo</li>
     <li>Segnaposto</li>
     <li>Nome proprietà*</li>
     <li>Mostra opzione di corrispondenza con tutti i tag</li>
     <li>Percorso tag principale</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelli</td>
   <td>Cerca in base al modello selezionato.</td>
   <td>
    <ul>
     <li>Segnaposto</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Stato traduzione</td>
   <td>Cerca in base allo stato di traduzione.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
    </ul> 
   </td>
  </tr>
 </tbody>
</table>

<!--
  <tr>
   <td>Date ???</td>
   <td>Slider-based search of assets based on a date property.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Asset Last Modified ?????</td>
   <td>Date the asset was last modified.<br /> </td>
   <td>A customized predicate, based on the Date Predicate.</td>
  </tr>
  <tr>
   <td>Range Options ???</td>
   <td>A specific search predicate for Assets and the same as common Slider Predicate. Is still available due to backward compatibilty issues.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Option Path</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tag </td>
   <td>Search assets based on tags. You can configure the Path property to populate various tags in the Tags list.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Option Path</li>
     <li>Description</li>
    </ul> </td>
  </tr>
-->

>[!NOTE]
>
>I predicati di ricerca comuni sono definiti in:
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>Queste informazioni sono solo a scopo di riferimento. Non è necessario modificare `/libs`.

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### Impostazioni predicato {#predicate-settings}

A seconda del predicato, è disponibile una selezione di impostazioni per la configurazione, tra cui:

* **Etichetta campo**

  L’etichetta che verrà visualizzata come intestazione comprimibile o come etichetta del campo del predicato.

* **Descrizione**

  Dettagli descrittivi per l’utente.

* **Segnaposto**

  Testo vuoto o il segnaposto del predicato se non viene immesso testo filtrante.

* **Nome proprietà**

  Proprietà su cui eseguire la ricerca. Utilizza un percorso relativo e i caratteri jolly `*/*/*` specificano la profondità della proprietà relativa al nodo `jcr:content` (ogni asterisco rappresenta un livello di nodo).

  Se si desidera eseguire una ricerca solo in un nodo figlio di primo livello della risorsa con la proprietà `x` nel nodo `jcr:content`, utilizzare `*/jcr:content/x`

* **Profondità proprietà**

  Profondità massima per la ricerca di tale proprietà nelle risorse. Quindi una ricerca su quella proprietà può essere eseguita su una risorsa e su elementi figlio ricorsivi fino a quando il livello degli elementi figlio non è uguale alla profondità specificata.

* **Valore proprietà**

  Il valore della proprietà come stringa assoluta o come linguaggio di espressione, ad esempio `cq:Page` o

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Testo intervallo**

  Etichetta del campo intervallo nel predicato **Intervallo date**.

* **Percorso opzione**

  L’utente può selezionare il percorso utilizzando Browser percorsi nella scheda Impostazione predicati. Dopo aver selezionato l&#39;icona **+** viene utilizzata per aggiungere la selezione all&#39;elenco di opzioni valide (quindi l&#39;icona **-** da rimuovere, se necessario).

  Le opzioni sono nodi di contenuto creati dall’utente con la seguente struttura:

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Percorso nodo opzioni**
Effettivamente come il **Percorso opzioni**, solo questo è nel campo predicato comune, l&#39;altro è specifico per le risorse.

* **Selezione singola**
Se questa opzione è selezionata, le opzioni vengono visualizzate come caselle di controllo che consentono una sola selezione. Se selezionata per errore, è possibile deselezionare una casella di controllo.

* **Nome/i proprietà pubblicazione e Live Copy**
Le etichette per le caselle di controllo di pubblicazione e Live Copy per il predicato specifico di Sites.

* Il &ast; sulle etichette dei campi nella scheda **Impostazioni** indica che i campi sono obbligatori e se lasciato vuoto, verrà visualizzato un messaggio di errore.

## Configurazione del Forms di ricerca {#configuring-your-search-forms}

### Creazione/apertura di una configurazione personalizzata {#creating-opening-a-customized-configuration}

1. Passa a **Strumenti**, **Generale**, **Cerca in Forms**.

1. Seleziona la configurazione da personalizzare.
1. Utilizza l&#39;icona **Modifica** per aprire la configurazione per l&#39;aggiornamento.
1. Se una nuova personalizzazione si desidera [aggiungere nuovi campi predicato e definire le impostazioni](#add-edit-a-predicate-field-and-define-field-settings) in base alle esigenze. Se esiste una personalizzazione, è possibile selezionare un campo esistente e [aggiornare le impostazioni](#add-edit-a-predicate-field-and-define-field-settings).
1. Seleziona **Fine** per salvare la configurazione. Le modifiche saranno visibili al prossimo utilizzo della configurazione.

   >[!NOTE]
   >
   >Le configurazioni personalizzate vengono memorizzate (come appropriato) in:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### Aggiungere/modificare un campo predicato e definire le impostazioni dei campi {#add-edit-a-predicate-field-and-define-field-settings}

Puoi aggiungere o modificare i campi e definirne/aggiornarne le impostazioni:

1. [Apri la configurazione personalizzata](#creating-opening-a-customized-configuration) per l&#39;aggiornamento.
1. Se si desidera aggiungere un nuovo campo, aprire la scheda **Seleziona predicato** e trascinare il predicato richiesto nella posizione desiderata. Ad esempio, il predicato **Intervallo date**:

   ![aggiungi un predicato](assets/csf-add-predicate.png)

1. A seconda che:

   * Stai aggiungendo un nuovo campo:

     Dopo aver aggiunto il predicato, si apre la scheda **Impostazioni** in cui sono visualizzate le proprietà che è possibile definire.

   * Desideri aggiornare un predicato esistente:

     Seleziona il campo del predicato (a destra), quindi apri la scheda **Impostazioni**.

   Ad esempio, le impostazioni per il predicato **Intervallo date**:

   ![modifica predicato](assets/csf-modify-predicate.png)

1. Apporta le modifiche necessarie e conferma con **Fine**. Le modifiche saranno visibili al prossimo utilizzo della configurazione.

### Anteprima della configurazione della ricerca {#previewing-the-search-configuration}

1. Seleziona l’icona Anteprima:

   ![icona anteprima](assets/csf-preview-icon.png)

1. Visualizza i moduli di ricerca così come sono visualizzati (completamente espansi) nella colonna Ricerca della console appropriata.

   ![anteprima modulo](assets/csf-preview-form.png)

1. **Chiudi** l&#39;anteprima per restituire e completare la configurazione.

### Eliminazione di un campo predicato {#deleting-a-predicate-field}

1. [Apri la configurazione personalizzata](#creating-opening-a-customized-configuration) per l&#39;aggiornamento.
1. Seleziona il campo del predicato (a destra), apri la scheda **Impostazioni**, quindi seleziona l&#39;icona **Elimina** (in basso a sinistra).

   ![icona Elimina](assets/csf-delete-icon.png)

1. Una finestra di dialogo richiede la conferma dell’azione di eliminazione.

1. Conferma questa e altre modifiche con **Fine**.

### Eliminazione di una configurazione (per ripristinare il valore predefinito) {#deleting-a-configuration-to-reinstate-the-default}

Dopo aver personalizzato una configurazione, i valori predefiniti verranno sostituiti. Puoi ripristinare la configurazione predefinita eliminando la configurazione personalizzata.

>[!NOTE]
>
>Non è possibile eliminare le configurazioni predefinite.

L’eliminazione di una configurazione personalizzata viene eseguita dalla console:

1. Seleziona la configurazione richiesta (ad esempio, **Editor pagina (ricerca paragrafi)**) e quindi l&#39;icona **Elimina** nella barra degli strumenti:

   ![ripristina predefinito](assets/csf-restore-default.png)

1. La configurazione personalizzata viene eliminata e il valore predefinito viene ripristinato (questo viene indicato dalla ricomparsa del simbolo del lucchetto nella console).

### Aggiunta di predicati di opzioni {#adding-options-predicates}

I predicati di opzione (Opzioni, Proprietà opzioni) consentono di configurare un elemento da cercare. Vengono in genere utilizzati per cercare elementi direttamente sotto la pagina, ad esempio una proprietà sul nodo della pagina.

L’esempio seguente (per eseguire ricerche in base al modello utilizzato per creare una pagina), illustra i passaggi necessari:

1. Crea il nodo che definisce la proprietà su cui eseguire la ricerca.

   Per essere disponibile per l’utente, è necessario un nodo principale contenente le definizioni delle singole opzioni.

   I nodi delle singole opzioni richiedono le proprietà seguenti:

   * `jcr:title` - etichetta del campo da visualizzare nella barra di ricerca
   * `value` - valore della proprietà in cui eseguire la ricerca

   ![Definizione predicato](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >***must*** non modificare nulla nel percorso `/libs`.
   >
   >Il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell&#39;istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
   >
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >
   >1. Ricreare l&#39;elemento richiesto, in quanto esiste in `/libs`, in `/apps`. In questo caso da:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Apporta le modifiche in `/apps.`

1. Apri la console **Cerca in Forms** e seleziona la configurazione da aggiornare. Ad esempio, **Barra di ricerca amministrazione siti**. Quindi seleziona **Modifica**.

1. A seconda della configurazione, aggiungere una **Opzioni** o **Proprietà opzioni** alla configurazione.
1. Aggiornare i campi, in particolare:

   * **Nome proprietà**

     Specifica la proprietà del nodo da cercare sui nodi di destinazione. Ad esempio:

     `jcr:content/cq:template`

   * **Percorso nodo opzione**

     Seleziona il percorso in cui si trovano le opzioni. Ad esempio:

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![Predicati opzione](assets/csf-options-predicate-02.png)

1. Seleziona **Fine** per salvare la configurazione.
1. Passa alla console appropriata (in questo esempio, **Sites**) e apri la barra **Ricerca - Filtri**. Sono visibili i nuovi moduli di ricerca definiti e le varie opzioni. Seleziona l’opzione desiderata per visualizzare i risultati della ricerca.

   ![opzioni in uso](assets/csf-options-usage.png)


## Autorizzazioni utente {#user-permissions}

Nella tabella seguente sono elencate le autorizzazioni necessarie per eseguire azioni di modifica, eliminazione e anteprima sui moduli di ricerca.

<table>
 <thead>
  <tr>
   <td><strong>Azione</strong></td>
   <td><strong>Autorizzazioni</strong></td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Modifica </td>
   <td>Autorizzazioni di lettura e scrittura sul nodo <code>/apps </code>.</td>
  </tr>
  <tr>
   <td>Eliminare</td>
   <td>Autorizzazioni di lettura, scrittura ed eliminazione sul nodo <code>/apps</code></td>
  </tr>
  <tr>
   <td>Anteprima</td>
   <td>Autorizzazioni di lettura, scrittura ed eliminazione sul nodo <code>/var/dam/content</code>.<br /> autorizzazioni di lettura e scrittura sul nodo <code>/apps</code>.</td>
  </tr>
 </tbody>
</table>
