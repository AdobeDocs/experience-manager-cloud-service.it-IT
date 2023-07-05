---
title: Configurazione dei moduli di ricerca
description: Configurazione di Search Forms per Adobe Experience Manager as a Cloud Service.
exl-id: b06649c4-cc91-44e3-8699-00e90140b90d
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 17%

---

# Configurazione dei moduli di ricerca {#configuring-search-forms}

Adobe Experience Manager as a Cloud Service viene fornito con un potente [Ricerca](/help/sites-cloud/authoring/getting-started/search.md) meccanismo.

In combinazione con questo, sono disponibili anche una serie di opzioni predefinite che consentono di filtrare il contenuto. Questi contengono facet predefiniti come **Data di modifica**, **Stato pubblicazione**, o **Stato LiveCopy** consente di analizzare rapidamente le risorse necessarie.

![ricerca e utilizzo dei filtri](assets/csf-usage.png)

L’obiettivo di questi elementi è quello di aiutarti a individuare i contenuti in modo rapido e semplice da:

* [Ricerca e filtro](/help/sites-cloud/authoring/getting-started/search.md#search-and-filter)
* [Selettore della barra](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)
* il [Browser risorse](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) (durante la modifica delle pagine)

>[!NOTE]
>
>Puoi configurare il sottostante [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md) servizio.

Utilizzo di **Cerca in Forms**, puoi personalizzare ed estendere questi pannelli in base alle tue esigenze specifiche.

Il **Cerca in Forms** fornisci una selezione preconfigurata di [predicati](#predicates-and-their-settings) che puoi combinare e definire. Il [finestre di dialogo per la configurazione di questi moduli](#configuring-your-search-forms) accessibile tramite:

* **Strumenti**
   * **Generale**
      * **Moduli di ricerca**

## Forms predefinito {#default-forms}

La prima volta che accedi a **Cerca in Forms** console è possibile vedere che tutte le configurazioni hanno un simbolo lucchetto. Ciò indica che la configurazione corrispondente è quella predefinita (predefinita) e non può essere eliminata. Una volta personalizzato e salvato, il blocco scompare. Riapparirà quando [elimina la configurazione personalizzata](#deleting-a-configuration-to-reinstate-the-default), nel qual caso viene ripristinato il valore predefinito (e l’indicatore del lucchetto).

![panoramica sulla configurazione dei moduli di ricerca](assets/csf-overview.png)

Le configurazioni predefinite (elencate in ordine alfabetico) disponibili sono:

* **Barra di ricerca amministrazione risorse**
* **Editor pagina (ricerca documenti)**
* **Editor pagine (ricerca frammenti esperienza)**
* **Editor pagina (ricerca immagini)**
* **Editor pagina (ricerca manoscritto)**
* **Editor pagina (ricerca pagine)**
* **Editor pagina (ricerca paragrafi)**
* **Editor pagina (ricerca prodotti)**
* **Editor pagina (ricerca di Scene7)**
* **Editor pagina (ricerca video)**
* **Barra di ricerca amministrazione progetti**
* **Barra di ricerca traduzione progetti**
* **Barra di ricerca amministrazione sito**
* **Barra di ricerca amministrazione snippet**
* **Barra di ricerca amministrazione Stock**
* **Barra di ricerca dei modelli per frammenti di contenuto**
* **Barra di ricerca amministrazione progetti**
* **Barra di ricerca traduzione progetti**

>[!NOTE]
>
>Per ulteriori dettagli sui moduli di ricerca relativi a Assets, vedi [Risorse - Facet di ricerca](/help/assets/search-facets.md)


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
   <td>Analytics</td>
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
   <td>Consente all’autore di cercare/filtrare le pagine contenenti un componente specifico. Ad esempio, una galleria di immagini.<br /> </td>
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
   <td><p>Le opzioni sono nodi di contenuto creati dall’utente.</p> <p>Consulta <a href="#addinganoptionspredicate">Aggiunta di un predicato opzioni</a> per ulteriori informazioni.</p> </td>
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
   <td>Opzioni Proprietà</td>
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
>Queste informazioni sono solo a scopo di riferimento, non è necessario apportare modifiche a `/libs`.

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

  Proprietà su cui eseguire la ricerca. Utilizza un percorso relativo e i caratteri jolly `*/*/*` specifica la profondità della proprietà relativa al `jcr:content` (ogni asterisco rappresenta un livello di nodo).

  Se desideri eseguire la ricerca solo su un nodo figlio di primo livello della risorsa che ha `x` proprietà sul `jcr:content` utilizzo del nodo `*/jcr:content/x`

* **Profondità proprietà**

  Profondità massima per la ricerca di tale proprietà nelle risorse. Quindi una ricerca su quella proprietà può essere eseguita su una risorsa e su elementi figlio ricorsivi fino a quando il livello degli elementi figlio non è uguale alla profondità specificata.

* **Valore proprietà**

  Il valore della proprietà come stringa assoluta o come linguaggio di espressione; ad esempio, `cq:Page` o

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Testo intervallo**

  Etichetta del campo intervallo nel **Intervallo date** predicato.

* **Percorso opzione**

  L’utente può selezionare il percorso utilizzando Browser percorsi nella scheda Impostazione predicati. Dopo aver selezionato **+** viene utilizzata per aggiungere la selezione all’elenco delle opzioni valide (quindi **-** da rimuovere se necessario).

  Le opzioni sono nodi di contenuto creati dall’utente con la seguente struttura:

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Percorso nodo opzioni**
Effettivamente uguale al **Percorso opzioni**, solo questo campo si trova nel predicato comune, l’altro è specifico per le risorse.

* **Selezione singola**
Se questa opzione è selezionata, le opzioni vengono visualizzate come caselle di controllo che consentono una sola selezione. Se selezionata per errore, è possibile deselezionare una casella di controllo.

* **Nome/i proprietà Publish e Live Copy**
Le etichette per le caselle di controllo di pubblicazione e Live Copy per il predicato specifico di Sites.

* &amp;ast; sulle etichette dei campi nel **Impostazioni** indica che i campi sono obbligatori e se questo campo viene lasciato vuoto, viene visualizzato un messaggio di errore.

## Configurazione del Forms di ricerca {#configuring-your-search-forms}

### Creazione/apertura di una configurazione personalizzata {#creating-opening-a-customized-configuration}

1. Accedi a **Strumenti**, **Generale**, **Cerca in Forms**.

1. Seleziona la configurazione da personalizzare.
1. Utilizza il **Modifica** per aprire la configurazione per l’aggiornamento.
1. Se desideri effettuare una nuova personalizzazione, [aggiungere nuovi campi predicato e definire le impostazioni](#add-edit-a-predicate-field-and-define-field-settings) secondo necessità. Se esiste una personalizzazione, puoi selezionare un campo esistente e [aggiornare le impostazioni](#add-edit-a-predicate-field-and-define-field-settings).
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
1. Per aggiungere un nuovo campo, aprire **Seleziona predicato** e trascina il predicato richiesto nella posizione desiderata. Ad esempio, il **Predicato intervallo di date**:

   ![aggiungi un predicato](assets/csf-add-predicate.png)

1. A seconda che:

   * Stai aggiungendo un nuovo campo:

     Dopo l’aggiunta del predicato, **Impostazioni** viene aperta e vengono visualizzate le proprietà che possono essere definite.

   * Desideri aggiornare un predicato esistente:

     Seleziona il campo predicato (a destra), quindi apri il **Impostazioni** scheda.

   Ad esempio, le impostazioni per **Predicato intervallo di date**:

   ![modifica predicato](assets/csf-modify-predicate.png)

1. Apporta le modifiche necessarie e conferma con **Fine**. Le modifiche saranno visibili al prossimo utilizzo della configurazione.

### Anteprima della configurazione della ricerca {#previewing-the-search-configuration}

1. Seleziona l’icona Anteprima:

   ![icona anteprima](assets/csf-preview-icon.png)

1. Visualizza i moduli di ricerca così come sono visualizzati (completamente espansi) nella colonna Ricerca della console appropriata.

   ![modulo di anteprima](assets/csf-preview-form.png)

1. **Chiudi** l’anteprima per restituire e completare la configurazione.

### Eliminazione di un campo predicato {#deleting-a-predicate-field}

1. [Apri la configurazione personalizzata](#creating-opening-a-customized-configuration) per l&#39;aggiornamento.
1. Seleziona il campo predicato (a destra), apri la **Impostazioni** e quindi selezionare la scheda **Elimina** in basso a sinistra.

   ![icona elimina](assets/csf-delete-icon.png)

1. Una finestra di dialogo richiede la conferma dell’azione di eliminazione.

1. Conferma questa e altre modifiche con **Fine**.

### Eliminazione di una configurazione (per ripristinare il valore predefinito) {#deleting-a-configuration-to-reinstate-the-default}

Dopo aver personalizzato una configurazione, i valori predefiniti verranno sostituiti. Puoi ripristinare la configurazione predefinita eliminando la configurazione personalizzata.

>[!NOTE]
>
>Non è possibile eliminare le configurazioni predefinite.

L’eliminazione di una configurazione personalizzata viene eseguita dalla console:

1. Seleziona la configurazione richiesta (ad esempio, **Editor pagina (ricerca paragrafi)**) e quindi il **Elimina** nella barra degli strumenti:

   ![ripristina predefinito](assets/csf-restore-default.png)

1. La configurazione personalizzata viene eliminata e il valore predefinito viene ripristinato (questo viene indicato dalla ricomparsa del simbolo del lucchetto nella console).

### Aggiunta di predicati di opzioni {#adding-options-predicates}

I predicati di opzione (Opzioni, Proprietà opzioni) consentono di configurare un elemento da cercare. Vengono in genere utilizzati per cercare elementi direttamente sotto la pagina, ad esempio una proprietà sul nodo della pagina.

L’esempio seguente (per eseguire ricerche in base al modello utilizzato per creare una pagina), illustra i passaggi necessari:

1. Crea il nodo che definisce la proprietà su cui eseguire la ricerca.

   Per essere disponibile per l’utente, è necessario un nodo principale contenente le definizioni delle singole opzioni.

   I nodi delle singole opzioni richiedono le proprietà seguenti:

   * `jcr:title` : l’etichetta del campo da visualizzare nella barra di ricerca
   * `value` : il valore della proprietà in cui eseguire la ricerca

   ![Definizione predicato](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >Tu ***deve*** non modificare nulla in `/libs` percorso.
   >
   >Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe benissimo essere sovrascritto quando applichi un hotfix o un feature pack).
   >
   >Il metodo consigliato per la configurazione e altre modifiche è:
   >
   >1. Ricrea l&#39;elemento richiesto, in quanto esiste in `/libs`, in `/apps`. In questo caso da:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Apporta le modifiche in `/apps.`

1. Apri **Cerca in Forms** e selezionare la configurazione da aggiornare. Ad esempio: **Barra di ricerca amministrazione siti**. Quindi seleziona **Modifica**.

1. A seconda della configurazione, aggiungi un **Opzioni** o **Proprietà Options** alla configurazione.
1. Aggiornare i campi, in particolare:

   * **Nome proprietà**

     Specifica la proprietà del nodo da cercare sui nodi di destinazione. Ad esempio:

     `jcr:content/cq:template`

   * **Percorso nodo opzione**

     Seleziona il percorso in cui si trovano le opzioni. Ad esempio:

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![Predicati opzione](assets/csf-options-predicate-02.png)

1. Seleziona **Fine** per salvare la configurazione.
1. Passa alla console appropriata (in questo esempio, **Sites**) e aprire la **Ricerca - Filtri** barra. Sono visibili i nuovi moduli di ricerca definiti e le varie opzioni. Seleziona l’opzione desiderata per visualizzare i risultati della ricerca.

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
   <td>Autorizzazioni di lettura e scrittura su <code>/apps </code>nodo.</td>
  </tr>
  <tr>
   <td>Eliminare</td>
   <td>Autorizzazioni di lettura, scrittura ed eliminazione su <code>/apps</code> nodo</td>
  </tr>
  <tr>
   <td>Anteprima</td>
   <td>Autorizzazioni di lettura, scrittura ed eliminazione su <code>/var/dam/content</code> nodo.<br /> Autorizzazioni di lettura e scrittura su <code>/apps</code> nodo.</td>
  </tr>
 </tbody>
</table>
