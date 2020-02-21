---
title: Configurazione dei moduli di ricerca
description: Configurazione dei moduli di ricerca per Adobe Experience Manager come servizio cloud.
translation-type: tm+mt
source-git-commit: c0298d81462138187b04407ba9cfd5041b08873f

---


# Configurazione dei moduli di ricerca {#configuring-search-forms}

Utilizzate **Cerca moduli** per personalizzare i facet e i filtri di ricerca disponibili nei vari pannelli di ricerca dell’ambiente di authoring. La personalizzazione di questi pannelli rende la funzionalità di ricerca versatile in base alle esigenze specifiche.

Sono disponibili [diversi](#predicates-and-their-settings)predicati.

Potete [configurare i moduli](#configuring-your-search-forms) di ricerca utilizzati in varie console e nel browser delle risorse (durante la modifica delle pagine). È possibile accedere alle [finestre di dialogo per la configurazione di questi moduli](#configuring-your-search-forms) tramite:

* **Strumenti**

   * **Generale**

      * **Moduli di ricerca**

Quando accedete per la prima volta a questa console, potete vedere che tutte le configurazioni dispongono di un simbolo lucchetto. Questo indica che la configurazione appropriata è la configurazione predefinita (out-of-the-box) e non può essere eliminata. Una volta personalizzata la configurazione, il blocco scompare, a meno che non si [elimini la configurazione](#deleting-a-configuration-to-reinstate-the-default)personalizzata, nel qual caso viene ripristinata l&#39;impostazione predefinita (e l&#39;indicatore del lucchetto).

![configurazione dei moduli di ricerca](assets/csf-overview.png)

## Configurazioni {#configurations}

Le configurazioni predefinite (elencate in ordine alfabetico) disponibili sono:

* **Barra di ricerca amministrazione risorse:**

   Questa configurazione definisce le opzioni di ricerca disponibili per l’utente quando utilizza la console Risorse.

* **Editor pagina (ricerca documenti):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di documenti nel browser Risorse (durante la modifica di una pagina).

* **Editor pagine (ricerca frammenti esperienza):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di frammenti esperienza nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca immagini):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di immagini nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca manoscritto):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di manoscritti nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca pagine):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di pagine nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca paragrafi):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di paragrafi nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca prodotti):**

   Questa configurazione definisce le opzioni disponibili per la ricerca di prodotti nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca di Scene7)**:

   Questa configurazione definisce le opzioni disponibili per la ricerca di risorse Scene7 nel browser Risorse (durante la modifica di una pagina).

* **Editor pagina (ricerca video)**:

   Questa configurazione definisce le opzioni disponibili per la ricerca di video nel browser Risorse (durante la modifica di una pagina).

* **Barra di ricerca amministrazione progetti:**

   Questa configurazione definisce le opzioni di ricerca disponibili per l&#39;utente durante la ricerca di progetti.

* **Barra di ricerca traduzione progetti:**

   Questa configurazione definisce le opzioni di ricerca disponibili per l&#39;utente durante la ricerca di traduzioni di progetto.

* **Barra di ricerca amministrazione sito**:

   Questa configurazione definisce le opzioni di ricerca disponibili per l’utente quando si utilizza la barra di ricerca della console Siti.

* **Barra di ricerca amministrazione snippet**:

   Questa configurazione definisce le opzioni di ricerca disponibili per l&#39;utente durante la ricerca degli snippet.

* **Barra di ricerca amministrazione Stock**:

   Questa configurazione definisce le opzioni di ricerca disponibili per l&#39;utente durante la ricerca delle risorse.

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
   <td>Funzionalità di ricerca/filtro nel browser Siti per la visualizzazione dei dati di analisi. I filtri di ricerca di Analytics si caricano per corrispondere alle colonne di analisi personalizzate mappate.</td>
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
   <td>Authoring</td>
   <td>Ricerca in base all’autore.</td>
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
   <td>Cercare le risorse sottoposte a Check-Out da un utente specifico.</td>
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
   <td>Cercate le risorse con uno stato di estrazione specifico.</td>
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
   <td>Consente a un autore di cercare/filtrare le pagine che contengono un componente specifico. For example an image gallery.<br /> </td>
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
   <td>Consente di effettuare ricerche nelle risorse in base allo stato di scadenza.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dimensione file</td>
   <td>Consente di effettuare ricerche delle risorse in base alle loro dimensioni.</td>
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
   <td>Cercate le risorse in base al tipo di file/mime.</td>
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
   <td>Predefinito di ricerca per ricerche full-text.</td>
   <td>
    <ul>
     <li>Segnaposto</li>
     <li>Nome proprietà</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Gruppo</td>
   <td>Predicato di ricerca per gruppo (utilizzato solo all'interno del predicato di Insights).</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Filtro nascosto</td>
   <td>Filtro su proprietà e valore, non visibile all'utente.</td>
   <td>
    <ul>
     <li>Nome proprietà*</li>
     <li>Valore proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Approfondimenti</td>
   <td>Effettua una ricerca in base a una selezione di parametri Insights.</td>
   <td>Si tratta di un predicato complesso composto da più predicati:
    <ul>
     <li>Gruppo</li>
     <li>Intervallo</li>
     <li>Opzioni</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Membro della raccolta</td>
   <td>Cercare risorse appartenenti a una raccolta</td>
   <td>
    <ul>
     <li>Descrizione</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Proprietà con più valori</td>
   <td>Consente di eseguire ricerche su più valori di una proprietà specificata.</td>
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
   <td><p>Le opzioni sono nodi di contenuto creati dall'utente.</p> <p>Per ulteriori informazioni, consultate <a href="#addinganoptionspredicate">Aggiunta di un predefinito</a> per le opzioni.</p> </td>
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
   <td>Cercare una o più proprietà dell'opzione.</td>
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
   <td>Pagina Stato</td>
   <td>Consente di cercare le pagine in base al loro stato.</td>
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
   <td>Consente di cercare le risorse che si trovano sotto un percorso specifico.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Aggiungi percorsi di ricerca</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Browser Percorsi</td>
   <td>Specifica un browser di percorsi da cercare.</td>
   <td>
    <ul>
     <li>Segnaposto</li>
     <li>Percorso directory principale</li>
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
   <td>Eseguire la ricerca in una proprietà specificata.</td>
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
   <td>Cercare le risorse in base al loro stato di pubblicazione</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervallo</td>
   <td>Consente di cercare risorse all’interno di un intervallo specificato. Nel pannello Ricerca potete specificare i valori minimo e massimo per l’intervallo.</td>
   <td>
    <ul>
     <li>Etichetta campo</li>
     <li>Nome proprietà*</li>
     <li>Descrizione</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Valutazione</td>
   <td>Consente di effettuare ricerche delle risorse in base al loro punteggio.<br /> </td>
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
   <td>Ricerca di risorse in base alla data relativa della creazione<br /> </td>
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
   <td>Un predicato di ricerca comune che estende il predicato dell'intervallo con la funzionalità di scorrimento. Il valore della proprietà ricercata deve essere compreso tra i limiti del cursore.</td>
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
   <td>Cerca in base allo stato di approvazione e di estrazione.</td>
   <td>Si tratta di un predicato complesso composto da più predicati:
    <ul>
     <li>Stato approvazione</li>
     <li>Stato ritiro</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Tag</td>
   <td>Ricerca basata sui tag.</td>
   <td>
    <ul>
     <li>Campo Lavel</li>
     <li>Segnaposto</li>
     <li>Nome proprietà*</li>
     <li>Mostra opzione di corrispondenza con tutti i tag</li>
     <li>Percorso tag radice</li>
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
   <td>Cerca in base allo stato della traduzione.</td>
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

<!--
>[!NOTE]
>
>* The common search predicates are defined in:
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
>This information is for reference only, you must not make changes to `/libs`.
-->

### Predicate Settings {#predicate-settings}

A seconda del predicato sono disponibili per la configurazione una selezione di impostazioni:

* **Etichetta campo**

   Etichetta che verrà visualizzata come intestazione comprimibile o come etichetta campo del predicato.

* **Descrizione**

   Dettagli descrittivi per l&#39;utente.

* **Segnaposto**

   Testo vuoto o il segnaposto del predicato nel caso in cui non venga immesso testo di filtro.

* **Nome proprietà**

   La proprietà su cui effettuare la ricerca. Utilizza un percorso relativo e i caratteri jolly `*/*/*` specificano la profondità della proprietà relativa al `jcr:content` nodo (ogni asterisco rappresenta un livello di nodo).

   Se si desidera eseguire la ricerca solo su un nodo secondario di primo livello della risorsa con la `x` proprietà sul `jcr:content` nodo, utilizzare `*/jcr:content/x`

* **Profondità proprietà**

   Profondità massima per la ricerca di tale proprietà all&#39;interno delle risorse. È quindi possibile eseguire una ricerca su tale proprietà su una risorsa e su elementi secondari ricorsivi fino a quando il livello degli elementi secondari non è uguale alla profondità specificata.

* **Valore proprietà**

   Il valore della proprietà come stringa assoluta o come lingua di espressione; ad esempio, `cq:Page` oppure

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Testo intervallo**

   Etichetta del campo intervallo nel predicato **Intervallo** date.

* **Percorso opzione**

   L&#39;utente può selezionare il percorso utilizzando il Browser percorsi nella scheda delle impostazioni del predicato. Dopo aver selezionato l&#39;icona **+** viene utilizzata per aggiungere la selezione all&#39;elenco di opzioni valide (quindi l&#39;icona **+** da rimuovere se necessario).

   Le opzioni sono nodi di contenuto creati dall&#39;utente con la struttura seguente:

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Percorso** del nodo Opzioni **Equivale al Percorso** delleopzioni. Solo questo si trova nel campo predicato comune, mentre l&#39;altro è specifico per le risorse.

* **Selezione** singola Se questa opzione è selezionata, le opzioni vengono rappresentate come caselle di controllo che consentono solo una singola selezione. Se selezionata per errore, è possibile deselezionare una casella di controllo.

* **Nome/i proprietà Pubblica e Live Copy** Le etichette delle caselle di controllo Pubblica e Copia dal vivo per il predicato specifico Siti.

* &amp;ast; nelle etichette dei campi della scheda **Impostazioni** , i campi sono obbligatori e, se lasciato vuoto, viene visualizzato un messaggio di errore.

## Configurazione dei moduli di ricerca {#configuring-your-search-forms}

### Creazione/apertura di una configurazione personalizzata {#creating-opening-a-customized-configuration}

1. Passare a **Strumenti**, **Generali**, **Moduli** di ricerca.

1. Selezionate la configurazione da personalizzare.
1. Utilizzate l&#39;icona **Modifica** per aprire la configurazione da aggiornare.
1. Se desiderate una nuova personalizzazione, probabilmente desiderate [aggiungere nuovi campi predicato e definire le impostazioni](#add-edit-a-predicate-field-and-define-field-settings) come necessario. Se esiste una personalizzazione, potete selezionare un campo esistente e [aggiornare le impostazioni](#add-edit-a-predicate-field-and-define-field-settings).
1. Select **Done** to save the configuration. Le modifiche verranno visualizzate al successivo utilizzo della configurazione.

   >[!NOTE]
   >
   >Le configurazioni personalizzate sono memorizzate (a seconda dei casi) in:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### Aggiungere o modificare un campo predefinito e definire le impostazioni dei campi {#add-edit-a-predicate-field-and-define-field-settings}

È possibile aggiungere o modificare i campi e definirne o aggiornarne le impostazioni:

1. [Aprite la configurazione](#creating-opening-a-customized-configuration) personalizzata per l&#39;aggiornamento.
1. Per aggiungere un nuovo campo, aprite la scheda **Seleziona predicato** e trascinate il predicato richiesto nella posizione desiderata. Ad esempio, il predicato **Intervallo date**:

   ![aggiungere un predicato](assets/csf-add-predicate.png)

1. A seconda se:

   * Si sta aggiungendo un nuovo campo:

      Dopo aver aggiunto il predicato, si apre la scheda **Impostazioni** e vengono visualizzate le proprietà che è possibile definire.

   * Aggiornare un predicato esistente:

      Selezionate il campo predicato (a destra), quindi aprite la scheda **Impostazioni** .
   Ad esempio, le impostazioni per il predicato **Intervallo date**:

   ![modifica predicato](assets/csf-modify-predicate.png)

1. Apportate le modifiche necessarie e confermate con **Fine**. Le modifiche verranno visualizzate al successivo utilizzo della configurazione.

### Anteprima della configurazione di ricerca {#previewing-the-search-configuration}

1. Selezionate l’icona Anteprima:

   ![icona Anteprima](assets/csf-preview-icon.png)

1. In questo modo i moduli di ricerca verranno visualizzati (completamente espansi) nella colonna Ricerca della console appropriata.

   ![modulo di anteprima](assets/csf-preview-form.png)

1. **Chiudete** l’anteprima per ripristinare e completare la configurazione.

### Eliminazione di un campo predicato {#deleting-a-predicate-field}

1. [Aprite la configurazione](#creating-opening-a-customized-configuration) personalizzata per l&#39;aggiornamento.
1. Selezionate il campo predicato (a destra), aprite la scheda **Impostazioni** , quindi selezionate l’icona **Elimina** (in basso a sinistra).

   ![icona delete](assets/csf-delete-icon.png)

1. Viene visualizzata una finestra di dialogo per richiedere la conferma dell’azione di eliminazione.

1. Confermate questa e tutte le altre modifiche con **Fine**.

### Eliminazione di una configurazione (per ripristinare le impostazioni predefinite) {#deleting-a-configuration-to-reinstate-the-default}

Una volta personalizzata una configurazione, le impostazioni predefinite verranno ignorate. Potete ripristinare la configurazione predefinita eliminando la configurazione personalizzata.

>[!NOTE]
>
>Non è possibile eliminare le configurazioni predefinite.

L’eliminazione di una configurazione personalizzata viene effettuata dalla console:

1. Selezionate la configurazione desiderata (ad esempio, Editor **pagina (ricerca Paragrafi)**, quindi l’icona **Elimina** nella barra degli strumenti:

   ![restore default](assets/csf-restore-default.png)

1. La configurazione personalizzata verrà eliminata e verrà ripristinata l’impostazione predefinita (come indicato dalla riapparizione del simbolo lucchetto nella console).

### Aggiunta di predefiniti per opzioni {#adding-options-predicates}

I predicati delle opzioni (Opzioni, Proprietà Opzioni) consentono di configurare un elemento da ricercare. Sono solitamente utilizzati per cercare qualcosa direttamente sotto la pagina; ad esempio, una proprietà sul nodo della pagina.

L’esempio seguente (per effettuare ricerche in base al modello utilizzato per creare una pagina) illustra i passaggi da seguire:

1. Creare il nodo che definisce la proprietà su cui eseguire la ricerca.

   Sarà necessario un nodo principale che contenga le definizioni delle singole opzioni per essere disponibili per l&#39;utente.

   I nodi delle singole opzioni richiedono le proprietà:

   * `jcr:title` - l&#39;etichetta del campo da visualizzare nella barra di ricerca
   * `value` - il valore della proprietà su cui effettuare la ricerca

<!--
   ![chlimage_1-379](assets/chlimage_1-379.png)
-->

>[!NOTE]
>
>Non ***devi*** cambiare nulla nel `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricreare l&#39;elemento richiesto, così come esiste in `/libs`, in `/apps`. In questo caso da:
>1. `/libs/cq/gui/content/common/options/predicates`
>1. Apportare modifiche all&#39;interno `/apps.`


1. Aprire la console **Moduli** di ricerca e selezionare la configurazione da aggiornare. Ad esempio, **Siti Admin Search Rail**.

   Quindi fare clic o toccare l&#39;icona **Modifica moduli** di ricerca.

1. A seconda della configurazione, aggiungere alla configurazione una proprietà **Opzioni** o **Opzioni** .
1. Aggiornare i campi, in particolare:

   * **Nome proprietà**

      Specifica la proprietà node da cercare nei nodi target. Esempio:

      `jcr:content/cq:template`

   * **Percorso nodo opzione**

      Selezionate il percorso in cui vengono mantenute le opzioni. Esempio:

      `/apps/cq/gui/content/common/options/predicates/templatetype`

<!--
   ![chlimage_1-380](assets/chlimage_1-380.png)
-->

1. Select **Done** to save your configuration.
1. Passate alla console appropriata (in questo esempio, **Siti**) e aprite la barra **Ricerca** . I nuovi moduli di ricerca definiti e le varie opzioni saranno visibili. Selezionate l’opzione desiderata per visualizzare i risultati della ricerca:

<!--
   ![chlimage_1-381](assets/chlimage_1-381.png)
-->

## Autorizzazioni utente {#user-permissions}

Nella tabella seguente sono elencate le autorizzazioni necessarie per eseguire le azioni di modifica, eliminazione e anteprima sui moduli di ricerca.

<table>
 <tbody>
  <tr>
   <td><strong>Azione</strong></td>
   <td><strong>Autorizzazioni</strong></td>
  </tr>
  <tr>
   <td>Modifica </td>
   <td>Autorizzazioni di lettura e scrittura sul <code>/apps </code>nodo.</td>
  </tr>
  <tr>
   <td>Elimina</td>
   <td>Autorizzazioni di lettura, scrittura, eliminazione sul <code>/apps</code> nodo</td>
  </tr>
  <tr>
   <td>Anteprima</td>
   <td>Autorizzazioni di lettura, scrittura, eliminazione sul <code>/var/dam/content</code> nodo.<br /> Autorizzazioni di lettura e scrittura sul <code>/apps</code> nodo.</td>
  </tr>
 </tbody>
</table>
