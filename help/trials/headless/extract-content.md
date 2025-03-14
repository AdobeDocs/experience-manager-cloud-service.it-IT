---
title: Estrarre contenuti utilizzando l’API GraphQL
description: Scopri come utilizzare Frammenti di contenuto e l’API GraphQL come sistema di gestione dei contenuti headless.
hidefromtoc: true
index: false
exl-id: f5e379c8-e63e-41b3-a9fe-1e89d373dc6b
feature: Headless
role: Admin, User, Developer
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: ht
source-wordcount: '1069'
ht-degree: 100%

---


# Estrarre contenuti utilizzando l’API GraphQL {#extract-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql"
>title="Estrarre contenuto utilizzando l’API GraphQL"
>abstract="In questo modulo imparerai come utilizzare i frammenti di contenuto e l’API GraphQL come sistema di gestione dei contenuti headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide"
>title="Avvia GraphQL Explorer"
>abstract="GraphQL fornisce un’API basata su query che consente alle applicazioni client esterne di eseguire query AEM solo per il contenuto necessario, utilizzando una singola chiamata API. Segui questo modulo per scoprire come eseguire due diversi tipi di query. Quindi scopri come recuperare il contenuto dal frammento di contenuto creato nel modulo precedente.<br><br>Avvia questo modulo in una nuova scheda facendo clic qui sotto."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_graphql_guide_footer"
>title="Ottimo lavoro Hai scoperto i due tipi di query di base e come eseguire query sui tuoi contenuti. Ora scopri come utilizzare l’API GraphQL AEM per creare query efficienti che distribuiscono contenuti in un formato previsto dall’app."
>abstract=""

## Query per un elenco di contenuti di esempio {#list-query}

Inizia da GraphQL Explorer in una nuova scheda. Qui puoi creare e convalidare le query rispetto al contenuto headless prima di utilizzarle per alimentare il contenuto dell’app o del sito web.

1. La versione di prova AEM headless viene fornita con un endpoint precaricato con frammenti di contenuto da cui è possibile estrarre contenuto a scopo di test. Assicurati che l’endpoint **AEM Demo Assets** sia selezionato nel menu a discesa **Endpoint** nell’angolo in alto a destra dell’editor.

1. Copia il seguente frammento di codice per una query di elenco dell’endopoint **AEM Demo Assets** precaricato. Una query a elenco restituisce un elenco di tutto il contenuto che utilizza un modello specifico di frammento di contenuto. Le pagine di inventario e categoria in genere utilizzano questo formato di query.

   ```text
   {
    adventureList {
     items {
       _path
       title
       price
       tripLength
       primaryImage {
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

1. Una volta incollato, fai clic sul pulsante **Riproduzione** in alto a sinistra dell’editor delle query per eseguire la query.

1. I risultati vengono visualizzati nel pannello a destra, accanto all’editor delle query. Se la query non è corretta, viene visualizzato un errore nel pannello di destra.

   ![Query elenco](assets/do-not-localize/list-query-1-3-4-5.png)

Hai appena convalidato una query di elenco per un elenco completo di tutti i frammenti di contenuto. Questo processo consente di garantire che la risposta sia ciò che l’app si aspetta, con risultati che illustrano come le app e i siti web recupereranno il contenuto creato in AEM.

## Query per un contenuto specifico di esempio {#bypath-query}

L’esecuzione di una query byPath ti consente di recuperare il contenuto per un frammento di contenuto specifico. Le pagine di dettaglio del prodotto e le pagine che si concentrano su un set specifico di contenuto in genere richiedono questo tipo di query.

1. Copia il seguente frammento di codice per una query byPath dell’endpoint **AEM Demo Assets** precaricato.

   ```text
    {
     adventureByPath(
       _path: "/content/dam/aem-demo-assets/en/adventures/bali-surf-camp/bali-surf-camp"
     ) {
       item {
         _path
         title
         description {
           json
         }
         primaryImage {
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

1. Una volta incollato, fai clic sul pulsante **Riproduzione** in alto a sinistra dell’editor delle query per eseguire la query.

1. I risultati vengono visualizzati nel pannello a destra, accanto all’editor delle query. Se la query non è corretta, viene visualizzato un errore nel pannello di destra.

   ![Risultati della query byPath](assets/do-not-localize/bypath-query-2-3-4.png)

Hai appena convalidato una query byPath per recuperare un frammento di contenuto specifico identificato dal percorso di tale frammento.

## Query del contenuto personale {#own-queries}

Dopo aver eseguito i due tipi principali di query, puoi eseguire una query sul contenuto.

1. Per eseguire query con frammenti di contenuto personalizzati, modifica l’endpoint dalla cartella **AEM Demo Assets** alla cartella **Progetto**.

1. Elimina tutto il contenuto esistente nell’editor delle query. Quindi digita parentesi graffa aperta `{` e premi Ctrl+Spazio o Opzione+Spazio per un elenco completo automatico dei modelli definiti nell’endpoint. Seleziona il modello creato che termina in `List` dalle opzioni. Se hai seguito gli esempi nei moduli precedenti, dovresti trovare `adventureList` nell’elenco di completamento automatico.

   ![Avvia query personalizzata](assets/do-not-localize/custom-query-1.png)

1. Definisci gli elementi che la query deve contenere per il modello Frammento di contenuto selezionato. Di nuovo, digita la parentesi aperta `{`, quindi premi Ctrl+Spazio o Opzione+Spazio per un elenco di completamento automatico. Seleziona `items` dalle opzioni.

1. Seleziona il pulsante **Migliora** per formattare automaticamente il codice in modo da facilitarne la lettura.

1. Al termine, seleziona il pulsante **Riproduci** in alto a sinistra dell’editor per eseguire la query. L’editor completa automaticamente gli `items`, che vengono brevemente evidenziati in giallo e la query viene eseguita.

1. I risultati vengono visualizzati nel pannello a destra, accanto all’editor delle query.

   ![Esegui query personalizzata](assets/do-not-localize/custom-query-2.png)

In questo modo i contenuti possono essere inviati a esperienze digitali omnicanale.

## Query persistenti {#persisted-queries}

Le query persistenti sono il meccanismo preferito per l’esposizione dell’API GraphQL alle applicazioni client. Una volta che una query è persistente, può essere richiesta utilizzando una richiesta GET e memorizzata nella cache per un recupero rapido.

Verrà creata una query persistente che include i dati che si desidera utilizzare dall’applicazione client.

1. I dati creati come frammento di contenuto vengono utilizzati prima, quindi assicurati che l’endpoint del **tuo progetto** sia selezionato nel menu a discesa **Endpoint** nell’angolo in alto a destra dell’editor.

1. Copia il seguente frammento di codice.

   ```text
      {
      adventureList {
       items {
         title
         description {
           plaintext
         }
         price
         image {
           ... on ImageRef {
             _publishUrl
             mimeType
           }
         }
       }
     }
   }
   ```

1. Sostituisci il contenuto esistente nell’editor delle query incollando il codice copiato.

   >[!NOTE]
   >
   >Se non hai utilizzato le stesse descrizioni dei campi illustrate nei moduli precedenti, aggiorna i nomi dei campi in questa query.
   >
   >Utilizza la funzione di completamento automatico di GraphQL (Ctrl+Spazio o Opzione+Spazio) come descritto in precedenza per identificare le proprietà disponibili.

1. Una volta incollato, fai clic sul pulsante **Riproduzione** in alto a sinistra dell’editor delle query per eseguire la query.

1. I risultati vengono visualizzati nel pannello a destra, accanto all’editor delle query. Se la query non è corretta, viene visualizzato un errore nel pannello di destra.

   ![Crea query personalizzata](assets/do-not-localize/own-query.png)

1. Quando la query ti soddisfa, fai clic sul pulsante **Salva con nome** nella parte superiore dell’editor delle query per renderla persistente.

1. Nel menu a comparsa **Nome della query**, assegna alla query il nome `adventure-list`.

1. Seleziona **Salva con nome**.

   ![Rendi persistente la query](assets/do-not-localize/persist-query.png)

1. La query è resa persistente, come confermato da un messaggio del banner nella parte inferiore dello schermo. La query viene ora visualizzata anche nel pannello a sinistra delle query persistenti nella finestra.

1. Affinché la query persistente sia disponibile pubblicamente, deve essere pubblicata, in modo analogo alla pubblicazione dei frammenti di contenuto. Fai clic sul pulsante **Pubblica** in alto a destra dell’editor di query per pubblicare la query.

1. La pubblicazione viene confermata da una notifica del banner.

È ora disponibile una nuova query persistente che conterrà solo le proprietà e i formati specifici definiti.
