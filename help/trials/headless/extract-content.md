---
title: Estrarre contenuti tramite l’API GraphQL
description: Scopri come utilizzare Frammenti di contenuto e l’API GraphQL come sistema di gestione dei contenuti headless.
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---


# Estrarre contenuti tramite l’API GraphQL {#extract-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql"
>title="Estrarre contenuto utilizzando l’API di GraphQL"
>abstract="In questo modulo imparerai come utilizzare Frammenti di contenuto e l’API GraphQL come sistema di gestione dei contenuti headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide"
>title="Avvia GraphQL Explorer"
>abstract="GraphQL fornisce un’API basata su query che consente alle applicazioni client esterne di eseguire query AEM solo per il contenuto necessario, utilizzando una singola chiamata API. Segui questo modulo per scoprire come eseguire due diversi tipi di query. Quindi scopri come recuperare il contenuto dal frammento di contenuto creato nel modulo precedente.<br><br>Avvia questo modulo in una nuova scheda facendo clic qui sotto."
>additional-url="https://video.tv.adobe.com/v/328618" text="Video introduttivo sull’estrazione del contenuto"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="Ottimo lavoro! Hai imparato i due tipi di query di base e come eseguire query sul tuo contenuto. Ora scopri come utilizzare l’API GraphQL AEM per creare query efficienti che distribuiscono contenuti in un formato previsto dall’app."
>abstract=""

## Query per un elenco di contenuti di esempio {#list-query}

Fai clic su **Avvia GraphQL Explorer** questo pulsante consente di aprire GraphQL Explorer in una nuova scheda.

![Editor query GraphQL](assets/extract-content/query-editor.png)

Utilizzando GraphQL Explorer è possibile creare e convalidare query rispetto al contenuto headless prima di utilizzarle per alimentare il contenuto dell&#39;app o del sito web. Vediamo come si fa!

1. La versione di prova AEM headless viene fornita con un endpoint precaricato con frammenti di contenuto da cui è possibile estrarre contenuto a scopo di test. Seleziona la **AEM Demo Assets** dall&#39;endpoint **Endpoint** menu a discesa nell’angolo in alto a destra dell’editor.

   ![Seleziona endpoint](assets/extract-content/select-endpoint.png)

1. Copia il seguente frammento di codice per una query di elenco del precaricato **AEM Demo Assets** punto finale. Una query a elenco restituisce un elenco di tutto il contenuto che utilizza un modello specifico di frammento di contenuto. Le pagine di inventario e categoria in genere utilizzano questo formato di query.

   ```text
   {
       adventureList {
         items {
            _path
            adventureTitle
            adventurePrice
            adventureTripLength
            adventurePrimaryImage {
              ... on ImageRef {
               _path
               mimeType
               width
               height
             }
           }
         }
      }
    }
   ```

1. Sostituisci il contenuto esistente nell’editor delle query incollando il codice copiato.

   ![Query elenco](assets/extract-content/list-query.png)

1. Una volta incollato, fai clic sul pulsante **Play** in alto a sinistra dell’editor delle query per eseguire la query.

1. I risultati vengono visualizzati nel pannello a destra, accanto all’editor delle query. Se la query non è corretta, viene visualizzato un errore nel pannello di destra.

   ![Elenca risultati query](assets/extract-content/list-query-results.png)

Hai appena convalidato una query di elenco per un elenco completo di tutti i frammenti di contenuto. Questo processo consente di garantire che la risposta sia ciò che l&#39;app si aspetta, con risultati che illustrano come le app e i siti web recupereranno il contenuto creato in AEM.

## Query per un contenuto specifico di esempio {#bypath-query}

L’esecuzione di una query byPath consente di recuperare il contenuto per un frammento di contenuto specifico. Le pagine di dettaglio del prodotto e le pagine che si concentrano su un set specifico di contenuto in genere richiedono questo tipo di query. Vediamo come funziona!

1. Copia il seguente frammento di codice per una query byPath del precaricato **AEM Demo Assets** punto finale.

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         adventureTitle
         adventureDescription {
           json
         }
         adventurePrimaryImage {
           ... on ImageRef {
             _path
             width
             height
           }
         }
       }
     }
   }
   ```

1. Sostituisci il contenuto esistente nell’editor delle query incollando il codice copiato.

   ![query byPath](assets/extract-content/bypath-query.png)

1. Una volta incollato, fai clic sul pulsante **Play** in alto a sinistra dell’editor delle query per eseguire la query.

1. I risultati vengono visualizzati nel pannello a destra, accanto all’editor delle query. Se la query non è corretta, viene visualizzato un errore nel pannello di destra.

   ![risultati della query byPath](assets/extract-content/bypath-query-results.png)

Hai appena convalidato una query byPath per recuperare un frammento di contenuto specifico identificato dal percorso di tale frammento.

## Query del contenuto personale {#own-queries}

Dopo aver eseguito i due tipi principali di query, puoi eseguire una query sul tuo contenuto.

1. Per eseguire query con frammenti di contenuto personalizzati, modifica l’endpoint dalla **AEM Demo Assets** nella cartella **Il progetto** cartella.

   ![Seleziona un endpoint personalizzato](assets/extract-content/select-endpoint.png)

1. Elimina tutto il contenuto esistente nell’editor delle query. Quindi digitare parentesi graffa aperta `{` e premere Ctrl+Spazio o Opzione+Spazio per un elenco completo automatico dei modelli definiti nell&#39;endpoint. Seleziona il modello creato che termina in `List` dalle opzioni .

   ![Modelli automatici completi nell’editor delle query](assets/extract-content/auto-complete-models.png)

1. Definire gli elementi che la query deve contenere per il modello Frammento di contenuto selezionato. Di nuovo, digitare la parentesi aperta `{`, quindi premere Ctrl+Spazio o Opzione+Spazio per un elenco di completamento automatico. Seleziona `items` dalle opzioni .

   ![Completamento automatico degli elementi nell’editor delle query](assets/extract-content/auto-complete-items.png)

1. Definisci i campi che la query deve contenere per il modello di frammento di contenuto selezionato. Ancora una volta, digita la parentesi aperta `{`, quindi premere Ctrl+Spazio o Opzione+Spazio per un elenco completo automatico dei campi disponibili nel modello Frammento di contenuto. Selezionare dall&#39;elenco i campi desiderati dal modello.

   ![Completamento automatico dei campi nell’editor delle query](assets/extract-content/auto-complete-fields.png)

1. Delimitare più campi con una virgola (`,`) o spazio e premere nuovamente Ctrl+Spazio o Opzione+Spazio per selezionare altri campi.

1. Quando lavori, puoi toccare o fare clic sul pulsante **Prettificare** per formattare automaticamente il codice in modo da facilitarne la lettura.

   ![Prettificare](assets/extract-content/prettify.png)

1. Al termine, tocca o fai clic sul pulsante **Play** in alto a sinistra dell’editor per eseguire la query.

   ![Risultati della query](assets/extract-content/custom-query-results.png)

1. I risultati vengono visualizzati nel pannello a destra, accanto all’editor delle query.

In questo modo i contenuti possono essere inviati a esperienze digitali omnicanale.
