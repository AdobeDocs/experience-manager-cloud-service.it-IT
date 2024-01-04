---
title: Panoramica di Universal Editor per sviluppatori AEM
description: Se sei uno sviluppatore AEM interessato al funzionamento di Universal Editor e a come utilizzarlo nel progetto, questo documento offre un’introduzione end-to-end che ti guida attraverso la strumentazione del progetto WKND per lavorare con Universal Editor.
source-git-commit: 16f2922a3745f9eb72f7070c30134e5149eb78ce
workflow-type: tm+mt
source-wordcount: '3082'
ht-degree: 0%

---


# Panoramica di Universal Editor per sviluppatori AEM {#developer-overview}

Se sei uno sviluppatore AEM interessato al funzionamento di Universal Editor e a come utilizzarlo nel progetto, questo documento offre un’introduzione end-to-end che ti guida attraverso la strumentazione del progetto WKND per lavorare con Universal Editor.

{{universal-editor-status}}

## Scopo {#purpose}

Questo documento fornisce un’introduzione per gli sviluppatori sia sulle modalità di funzionamento dell’Editor universale che su come dotare l’applicazione di strumenti per utilizzarla.

A tal fine, prende un esempio standard che la maggior parte degli sviluppatori AEM conosce, i Componenti core e il sito WKND e strumenta alcuni componenti di esempio da modificare utilizzando l’editor universale.

>[!TIP]
>
>Questo documento illustra i passaggi aggiuntivi necessari per illustrare il funzionamento dell’editor universale e ha lo scopo di approfondire la comprensione dell’editor da parte dello sviluppatore. Non prende quindi la via più diretta per strumentare un&#39;app, ma la più illustrativa dell&#39;Editor Universale e come funziona.
>
>Per iniziare a utilizzare il sistema il più rapidamente possibile, vedere la [Guida introduttiva dell’Editor universale in AEM](/help/implementing/universal-editor/getting-started.md) documento.

## Prerequisiti {#prerequisites}

Per seguire questa panoramica, è necessario disporre dei seguenti elementi.

* [Un’istanza di sviluppo locale di AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=it)
   * L&#39;istanza di sviluppo locale deve essere [configurato con HTTPS a scopo di sviluppo su `localhost`.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=it)
   * [È necessario installare il sito demo WKND.](https://github.com/adobe/aem-guides-wknd)
* [Accesso all’editor universale](/help/implementing/universal-editor/getting-started.md#onboarding)
* [Un servizio Universal Editor locale](/help/implementing/universal-editor/local-dev.md) in esecuzione a scopo di sviluppo

Al di là della generale familiarità con lo sviluppo web, questo documento presuppone una conoscenza di base con lo sviluppo dell’AEM. Se non ha esperienza con lo sviluppo dell’AEM, prenda in considerazione la revisione [l’esercitazione WKND prima di continuare.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

## Avviare l’AEM e accedere all’editor universale {#sign-in}

Se non lo hai già fatto, devi avere la tua istanza di sviluppo AEM locale in esecuzione con WKND installato e HTTPS abilitato come [descritte nei prerequisiti.](#prerequisites) Questa panoramica presuppone che l’istanza sia in esecuzione alle `https://localhost:8443`.

1. Apri la pagina mastro principale in lingua inglese WKND nell’editor AEM.

   ```text
   https://localhost:8443/editor.html/content/wknd/language-masters/en.html
   ```

1. In **Informazioni pagina** dell’editor, seleziona **Visualizza come pubblicato**. Viene aperta la stessa pagina in una nuova scheda con l’editor AEM disabilitato.

   ```text
   https://localhost:8443/content/wknd/language-masters/en.html?wcmmode=disabled
   ```

1. Copia questo collegamento.

1. Ora accedi a Universal Editor.

   ```text
   https://experience.adobe.com/#/aem/editor
   ```

1. Incolla il collegamento copiato in precedenza del contenuto WKND in **URL sito** dell’Editor universale e fai clic su **Apri**.

   ![Aprire la pagina WKND nell’editor universale](assets/dev-ue-open.png)

## L’editor universale tenta di caricare il contenuto {#sameorigin}

Universal Editor carica il contenuto da modificare in un frame. Le impostazioni predefinite dell’AEM per le opzioni X-Frame evitano questo problema, che può essere chiaramente visto nel browser come un errore e dettagliato nell’output della console quando si tenta di caricare la copia locale di WKND.

![Errore del browser a causa dell’opzione SAMEORIGIN](assets/dev-sameorigin.png)

Opzione X-Frame `sameorigin` impedisce il rendering delle pagine AEM all’interno di un frame. È necessario rimuovere questa intestazione per consentire il caricamento delle pagine nell’Editor universale.

1. Apri Configuration Manager.

   ```text
   https://localhost:8443/system/console/configMgr
   ```

1. Modificare la configurazione OSGi `org.apache.sling.engine.impl.SlingMainServlet`

   ![Proprietà OSGi per SAMEORIGIN](assets/dev-sameorigin-osgi.png)

1. Elimina la proprietà `X-Frame-Options=SAMEORIGIN` della proprietà **Intestazioni di risposta aggiuntive**.

1. Salva le modifiche.

Ora, se ricarichi l’editor universale, vedrai che la pagina AEM si carica.

>[!TIP]
>
>* Consulta il documento [Guida introduttiva dell’Editor universale in AEM](/help/implementing/universal-editor/getting-started.md#sameorigin) per ulteriori dettagli su questa configurazione OSGi.
>* Consulta il documento [Configurazione di OSGi per Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) per maggiori dettagli sull’OSGi in AEM.

## Gestione dei cookie dello stesso sito {#samesite-cookies}

Quando Universal Editor carica la pagina, questa viene caricata nella pagina di accesso AEM per garantire che l&#39;utente sia autenticato per apportare modifiche.

Tuttavia, non puoi accedere correttamente. Visualizzando la console del browser, potete notare che il browser ha bloccato l&#39;input sul frame

![Input bloccato](assets/dev-cross-origin.png)

Il cookie del token di accesso viene inviato a AEM come dominio di terze parti. Pertanto, i cookie dello stesso sito devono essere consentiti nell’AEM.

1. Apri Configuration Manager.

   ```text
   https://localhost:8443/system/console/configMgr
   ```

1. Modificare la configurazione OSGi `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`

   ![Proprietà OSGi per i cookie dello stesso sito](assets/dev-cross-origin-osgi.png)

1. Modificare la proprietà **Attributo SameSite per il cookie token di accesso** a `None`.

1. Salva le modifiche.

Ora, se ricarichi l’Editor universale, potrai accedere all’AEM e caricare la pagina di destinazione.

>[!TIP]
>
>* Consulta il documento [Guida introduttiva dell’Editor universale in AEM](/help/implementing/universal-editor/getting-started.md#samesite-cookies) per ulteriori dettagli su questa configurazione OSGi.
>* Consulta il documento [Configurazione di OSGi per Adobe Experience Manager as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) per maggiori dettagli sull’OSGi in AEM.

## Universal Editor si connette al frame remoto {#ue-connect-remote-frame}

Dopo aver caricato la pagina nell&#39;editor universale e aver effettuato l&#39;accesso a AEM, l&#39;editor universale tenta di connettersi al frame remoto. Questa operazione viene eseguita tramite una libreria JavaScript che deve essere caricata nel frame remoto. Se la libreria JavaScript non è presente, la pagina crea un errore di timeout nella console.

![Errore di timeout](assets/dev-timeout.png)

Devi aggiungere la libreria JavaScript necessaria al componente page dell’app WKND.

1. Apri CRXDE Liti.

   ```text
   https://localhost:8443/crx/de
   ```

1. Sotto `/apps/wknd/components/page`, modifica il file `customheaderlibs.html`.

   ![Modifica del file customheaderlibs.html](assets/dev-customheaderlibs.png)

1. Aggiungi la libreria JavaScript alla fine del file.

   ```html
   <script src="https://cdn.jsdelivr.net/gh/adobe/universal-editor-cors/dist/universal-editor-embedded.js"></script>
   ```

1. Clic **Salva tutto** e quindi ricaricare Universal Editor.

La pagina ora viene caricata con la libreria JavaScript appropriata per consentire all’editor universale di connettersi alla pagina e l’errore di timeout non viene più visualizzato nella console.

>[!TIP]
>
>* La libreria può essere caricata nell’intestazione o nel piè di pagina.
>* Il `universal-editor-embedded.js` libreria [è disponibile su NPM](https://www.npmjs.com/package/@adobe/universal-editor-cors) e puoi ospitarlo autonomamente, se necessario, o inserirlo direttamente nell’applicazione.

## Definizione di una connessione per rendere le modifiche permanenti {#connection}

La pagina WKND ora viene caricata correttamente nell’editor universale e la libreria JavaScript viene caricata per collegare l’editor all’app.

Tuttavia, probabilmente hai notato rapidamente che non puoi interagire con la pagina nell’Editor universale. Editor universale non può modificare la pagina. Affinché l’editor universale possa modificare il contenuto, è necessario definire una connessione in modo che sappia dove scriverlo. Per lo sviluppo locale, devi riscrivere all’istanza di sviluppo AEM locale all’indirizzo `https://localhost:8443`.

1. Apri CRXDE Liti.

   ```text
   https://localhost:8443/crx/de
   ```

1. Sotto `/apps/wknd/components/page`, modifica il file `customheaderlibs.html`.

   ![Modifica del file customheaderlibs.html](assets/dev-instrument-app.png)

1. Aggiungi alla fine del file i metadati necessari per la connessione all’istanza AEM locale.

   ```html
   <meta name="urn:adobe:aue:system:aem" content="aem:https://localhost:8443">
   ```

1. Aggiungere alla fine del file i metadati necessari per la connessione al servizio Universal Editor locale.

   ```html
   <meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
   ```

1. Clic **Salva tutto** e quindi ricaricare Universal Editor.

Ora Universal Editor non solo può caricare correttamente il contenuto dall’istanza di sviluppo AEM locale, ma sa anche dove mantenere eventuali modifiche apportate utilizzando il servizio Universal Editor locale. Questo è il primo passaggio per rendere l’app modificabile con l’Editor universale.

>[!TIP]
>
>* Consulta il documento [Guida introduttiva dell’Editor universale in AEM](/help/implementing/universal-editor/getting-started.md#connection) per ulteriori dettagli sui metadati della connessione.
>* Consulta il documento [Architettura di Universal Editor](/help/implementing/universal-editor/architecture.md#service) per maggiori dettagli sulla struttura di Universal Editor.
>* Consulta il documento [Sviluppo locale AEM con Universal Editor](/help/implementing/universal-editor/local-dev.md) per ulteriori dettagli su come connettersi a una versione con hosting autonomo di Universal Editor.

## Strumentazione dei componenti {#instrumenting-components}

Tuttavia, probabilmente noterai che è ancora possibile fare poco con l’Editor universale. Se tenti di fare clic sul teaser nella parte superiore della pagina WKND nell’Universal Editor, non puoi selezionarlo (o altro sulla pagina).

I componenti devono inoltre essere dotati di strumenti per poter essere modificati con l’Editor universale. A questo scopo, devi modificare il componente teaser. Pertanto, è necessario sovrapporre i Componenti core, in quanto tali componenti si trovano in `/libs`, che è immutabile.

1. Apri CRXDE Liti.

   ```text
   https://localhost:8443/crx/de
   ```

1. Seleziona il nodo `/libs/core/wcm/components` e fai clic su **Sovrapponi nodo** sulla barra degli strumenti.

1. Con `/apps/` selezionato come **Posizione sovrapposizione**, fai clic su **OK**.

   ![Sovrapponi il teaser](assets/dev-overlay-teaser.png)

1. Seleziona la `teaser` nodo sotto `/libs/core/wcm/components` e fai clic su **Copia** nella barra degli strumenti.

1. Seleziona il nodo sovrapposto in corrispondenza di `/apps/core/wcm/components` e fai clic su **Incolla** nella barra degli strumenti.

1. Fare doppio clic sul file `/apps/core/wcm/components/teaser/v2/teaser/teaser.html` per modificarlo.

   ![Modifica del file teaser.html](assets/dev-edit-teaser.png)

1. Alla fine del primo `div` alla riga 26 circa, aggiungere i dettagli della strumentazione per il componente.

   ```text
   itemscope
   itemid="urn:aem:${resource.path}"
   itemtype="component"
   data-editor-itemlabel="Teaser"
   ```

1. Clic **Salva tutto** nella barra degli strumenti e ricarica Universal Editor.

1. Nell’Editor universale, fai clic sul componente teaser nella parte superiore della pagina per verificare che ora sia possibile selezionarlo.

1. Se si fa clic su **Struttura contenuto** nella barra delle proprietà di Universal Editor, puoi vedere che l’editor ha riconosciuto tutti i teaser sulla pagina ora che l’hai instrumentato. Il teaser selezionato è quello evidenziato.

   ![Selezione del componente teaser instrumentato](assets/dev-select-teaser.png)

>[!TIP]
>
>Consulta il documento [Utilizzo di Sling Resource Merger in Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/sling-resource-merger.md) per ulteriori dettagli sui nodi sovrapposti.

## Sottocomponenti strumento del teaser {#subcomponents}

Ora puoi selezionare il teaser, ma non modificarlo. Questo perché il teaser è un composito di diversi componenti come il componente Immagine e Titolo. Devi instrumentare questi sottocomponenti per modificarli.

1. Apri CRXDE Liti.

   ```text
   https://localhost:8443/crx/de
   ```

1. Seleziona il nodo `/apps/core/wcm/components/teaser/v2/teaser/` e fare doppio clic su `title.html` file.

   ![Modificare il file title.html](assets/dev-edit-title.png)

1. Inserisci le seguenti proprietà alla fine del `h2` (vicino alla riga 17).

   ```text
   itemprop="jcr:title"
   itemtype="text"
   data-editor-itemlabel="Title"
   ```

1. Clic **Salva tutto** nella barra degli strumenti e ricarica Universal Editor.

1. Fai clic sul titolo dello stesso componente teaser nella parte superiore della pagina per verificare che ora sia possibile selezionarlo. La struttura del contenuto mostra anche il titolo come parte del componente teaser selezionato.

   ![Seleziona il titolo nel teaser](assets/dev-select-title.png)

Ora puoi modificare il titolo del componente teaser.

## Cosa significa tutto questo? {#what-does-it-mean}

Ora che puoi modificare il titolo del teaser, soffermiamoci a esaminare cosa hai realizzato e come.

Il componente teaser è stato identificato nell’editor universale strumentandolo.

* `itemscope` lo identifica come elemento per Universal Editor.
* `itemid` identifica la risorsa in AEM che viene modificata.
* `itemtype` definisce che gli elementi devono essere trattati come un componente pagina (anziché, ad esempio, come un contenitore).
* `data-editor-itemlabel` visualizza un’etichetta intuitiva nell’interfaccia utente per il teaser selezionato.

Hai anche instrumentato il componente titolo all’interno del componente teaser.

* `itemprop` è l’attributo JCR scritto.
* `itemtype` è la modalità di modifica dell’attributo. In questo caso, con l’editor di testo, poiché è un titolo (anziché l’editor Rich Text).

## Definizione delle intestazioni di autenticazione {#auth-header}

Ora puoi modificare il titolo del teaser in linea e le modifiche vengono mantenute nel browser.

![Titolo modificato del teaser](assets/dev-edited-title.png)

Tuttavia, se ricarichi il browser, il titolo precedente viene ricaricato. Questo perché, anche se l’editor universale sa come connettersi all’istanza AEM, non può ancora autenticarsi nell’istanza AEM per riscrivere le modifiche in JCR.

Se visualizzi la scheda di rete degli strumenti di sviluppo del browser e cerchi `update`, quando si tenta di modificare il titolo, si verifica un errore 500.

![Errore durante la modifica del titolo](assets/dev-edit-error.png)

Quando si utilizza l’editor universale per modificare il contenuto dell’AEM di produzione, l’editor universale utilizza lo stesso token IMS utilizzato per accedere all’editor e autenticarsi nell’AEM per facilitare la riscrittura in JCR.

Quando si sviluppa localmente, non è possibile utilizzare il provider di identità AEM, pertanto è necessario fornire manualmente un modo per l’autenticazione impostando esplicitamente un’intestazione di autenticazione.

1. Nell&#39;interfaccia di Universal Editor, fare clic su **Intestazioni di autenticazione** nella barra degli strumenti.

1. Copia l’intestazione di autenticazione necessaria per autenticarti nell’istanza AEM locale e fai clic su **Salva**.

   ![Configurazione delle intestazioni di autenticazione](assets/dev-authentication-headers.png)

1. Ricarica l’Editor universale e ora modifica il titolo del teaser.

Non vengono più segnalati errori nella console del browser e le modifiche vengono mantenute nell’istanza di sviluppo AEM locale.

Se studi il traffico negli strumenti di sviluppo del browser e cerchi il `update` eventi, puoi visualizzare i dettagli dell’aggiornamento.

![Modifica del titolo del teaser completata](assets/dev-edit-title-successfully.png)

```json
{
  "op": "patch",
  "connections": {
    "aem": "aem:https://localhost:8443"
  },
  "path": {
    "itemid": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "itemtype": "text",
    "itemprop": "jcr:title"
  },
  "value": "Tiny Toon Adventures"
}
```

* `op` è l’operazione, che in questo caso è una patch del contenuto esistente del campo modificato.
* `connections` è la connessione all’istanza AEM locale
* `path` è il nodo esatto e le proprietà aggiornate nel JCR
* `value` è l’aggiornamento che hai effettuato.

Puoi vedere la modifica persistente in JCR.

![Aggiornamento in JCR](assets/dev-write-back-jcr.png)

>[!TIP]
>
>Sono disponibili molti strumenti online per generare le intestazioni di autenticazione necessarie a scopo di test e sviluppo.
>
>Esempio di intestazione di autenticazione di base `Basic YWRtaW46YWRtaW4=` è per la combinazione utente/password di `admin:admin` come avviene per lo sviluppo locale dell’AEM.

## Strumentazione dell’app per la barra delle proprietà {#properties-rail}

Ora disponi di un’app dotata di strumenti per essere modificabile tramite l’Editor universale.

La modifica è attualmente limitata alla modifica in linea del titolo del teaser. Tuttavia, in alcuni casi la modifica diretta non è sufficiente. Il testo, come il titolo del teaser, può essere modificato nella posizione in cui si trova con l’input della tastiera. Tuttavia, gli elementi più complicati devono poter essere visualizzati e consentire la modifica di dati strutturati separati da come vengono riprodotti nel browser. A questo serve la barra delle proprietà.

Ora aggiorna l’app per utilizzare la barra delle proprietà per la modifica. A questo scopo, torna al file di intestazione del componente page dell&#39;app, in cui sono già state stabilite le connessioni all&#39;istanza di sviluppo AEM locale e al servizio Universal Editor locale. Qui devi definire i componenti modificabili nell’app e i relativi modelli di dati.

1. Apri CRXDE Liti.

   ```text
   https://localhost:8443/crx/de
   ```

1. Sotto `/apps/wknd/components/page`, modifica il file `customheaderlibs.html`.

   ![Modifica del file customheaderlibs.html](assets/dev-instrument-properties-rail.png)

1. Aggiungi lo script necessario per mappare i campi alla fine del file.

   ```html
   <script type="application/vnd.adobe.aem.editor.component-definition+json">
   {
     "groups": [
       {
         "title": "General Components",
         "id": "general",
         "components": [
           {
             "title": "Teaser",
             "id": "teaser",
             "plugins": {
               "aem": {
                 "page": {
                   "resourceType": "wknd/components/teaser"
                 }
               }
             },
             "model": {
               "id": "teaser",
               "fields": [
                 {
                   "component": "text-input",
                   "name": "jcr:title",
                   "label": "Title",
                   "valueType": "string"
                 },
                 {
                   "component": "text-area",
                   "name": "jcr:description",
                   "label": "Description",
                   "valueType": "string"
                 }
               ]
             }
           }
         ]
       }
     ]
   }
   </script>
   ```

1. Clic **Salva tutto** nella barra degli strumenti.

## Cosa significa tutto questo? {#what-does-it-mean-2}

Per poter essere modificati tramite la barra delle proprietà, i componenti devono essere assegnati a `groups`, pertanto ogni definizione inizia come un elenco di gruppi contenenti i componenti.

* `title` è il nome del gruppo.
* `id` è l’identificatore univoco del gruppo, in questo caso i componenti generali che compongono il contenuto della pagina, a differenza, ad esempio, dei componenti avanzati per il layout di pagina.

Ogni gruppo ha quindi una matrice di `components`.

* `title` è il nome del componente.
* `id` è l’identificatore univoco del componente, in questo caso un teaser.

Ogni componente ha quindi una definizione del plug-in che definisce come il componente viene mappato all’AEM.

* `aem` è il plug-in che gestisce la modifica. Può essere considerato come il servizio che elabora il componente.
* `page` definisce il tipo di componente, in questo caso un componente pagina standard.
* `resourceType` è la mappatura della componente effettiva dell’AEM.

Ogni componente deve quindi essere mappato su un `model` per definire i singoli campi modificabili.

* `id` è l’identificatore univoco del modello, che deve corrispondere all’ID del componente.
* `fields` è un array dei singoli campi.
* `component` è il tipo di input, ad esempio testo o area di testo.
* `name` è il nome del campo nel JCR a cui è mappato il campo.
* `label` è la descrizione del campo che viene visualizzato nell’interfaccia utente dell’editor.
* `valueType` è il tipo di dati.

## Strumentazione del componente per la barra Proprietà {#properties-rail-component}

È inoltre necessario definire a livello di componente quale modello utilizzare.

1. Apri CRXDE Liti.

   ```text
   https://localhost:8443/crx/de
   ```

1. Fare doppio clic sul file `/apps/core/wcm/components/teaser/v2/teaser/teaser.html` per modificarlo.

   ![Modifica del file teaser.html](assets/dev-edit-teaser.png)

1. Alla fine del primo `div` all&#39;incirca alla riga 32, dopo il `itemscope` , aggiungi i dettagli della strumentazione per il modello che verrà utilizzato dal componente teaser.

   ```text
   data-editor-itemmodel="teaser"
   ```

1. Clic **Salva tutto** nella barra degli strumenti e ricarica Universal Editor.

1. Fai clic sul titolo del teaser per modificarlo ancora una volta.

1. Fai clic sulla barra delle proprietà per visualizzare la scheda delle proprietà e visualizzare i campi appena instrumentati.

   ![Barra delle proprietà instrumentata](assets/dev-properties-rail-instrumented.png)

Ora puoi modificare il titolo del teaser in linea come in precedenza o nella barra delle proprietà. In entrambi i casi, le modifiche vengono mantenute nell’istanza di sviluppo AEM locale.

## Aggiungi campi aggiuntivi alla barra delle proprietà {#add-fields}

Utilizzando la struttura di base del modello dati per il componente già implementato, puoi aggiungere campi aggiuntivi seguendo lo stesso modello.

Ad esempio, puoi aggiungere un campo per regolare lo stile del componente.

1. Apri CRXDE Liti.

   ```text
   https://localhost:8443/crx/de
   ```

1. Sotto `/apps/wknd/components/page`, modifica il file `customheaderlibs.html`.

   ![Modifica del file customheaderlibs.html](assets/dev-instrument-styles.png)

1. Aggiungi un elemento aggiuntivo al `fields` per il campo di stile. Ricordati di aggiungere una virgola dopo l’ultimo campo prima di inserirne uno nuovo.

   ```json
   {
      "component": "select",
      "name": "cq:styleIds",
      "label": "Style",
      "valueType": "string",
        "multi": true,
      "options": [
        {"name": "hero", "value":"1555543212672"},
        {"name": "card", "value":"1605057868937"}
      ]
   }
   ```

1. Clic **Salva tutto** nella barra degli strumenti e ricarica Universal Editor.

1. Fai clic sul titolo del teaser per modificarlo ancora una volta.

1. Fai clic sulla barra delle proprietà e osserva che è presente un nuovo campo per regolare lo stile del componente.

   ![La barra delle proprietà dotata di strumenti con il campo di stile](assets/dev-style-instrumented.png)

Qualsiasi campo nel JCR del componente può essere esposto in questo modo nell’Editor universale.

## Riepilogo {#summary}

Congratulazioni. Ora puoi personalizzare le tue app per l’AEM in modo che funzionino con l’Editor universale.

Quando inizi a dotare la tua app di strumenti, tieni presente i passaggi di base eseguiti in questo esempio.

1. [Puoi configurare l’ambiente di sviluppo.](#prerequisites)
   * AEM in esecuzione in locale su HTTPS con WKND installato
   * Servizio Universal Editor in esecuzione in locale su HTTPS
1. Hai aggiornato le impostazioni OSGi dell’AEM per consentirne il caricamento remoto del contenuto.
   * [&quot;org.apache.sling.engine.impl.SlingMainServlet&quot;](#sameorigin)
   * [&quot;com.day.crx.security.token.impl.impl.TokenAuthenticationHandler&quot;](#samesite-cookies)
1. [Hai aggiunto il ](#ue-connect-remote-frame)
1. [Hai definito una connessione per rendere persistenti le modifiche in ](#connection)
   * È stata definita una connessione all’istanza di sviluppo AEM locale.
   * È stata inoltre definita una connessione al servizio Universal Editor locale.
1. [È stato instrumentato il componente teaser.](#instrumenting-components)
1. [Hai instrumentato i sottocomponenti del teaser.](#subcomponents)
1. [È stata definita un&#39;intestazione di autenticazione personalizzata che consente di salvare le modifiche utilizzando il servizio Universal Editor locale.](#auth-header)
1. [Hai instrumentato l&#39;app per utilizzare la barra delle proprietà.](#properties-rail)
1. [Hai instrumentato il componente teaser per utilizzare la barra delle proprietà.](#properties-rail-component)

Puoi seguire questi stessi passaggi per dotare la tua app di strumenti per l’utilizzo con l’Editor universale. Tutte le proprietà nel JCR possono essere esposte all’Editor universale.

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni e dettagli sulle funzioni di Universal Editor, consulta i seguenti documenti.

* Per iniziare a utilizzare il sistema il più rapidamente possibile, vedere la [Guida introduttiva dell’Editor universale in AEM](/help/implementing/universal-editor/getting-started.md) documento.
* Consulta il documento [Guida introduttiva dell’Editor universale in AEM](/help/implementing/universal-editor/getting-started.md#sameorigin) per ulteriori dettagli sulle configurazioni OSGi necessarie.
* Consulta il documento [Guida introduttiva dell’Editor universale in AEM](/help/implementing/universal-editor/getting-started.md#connection) per ulteriori dettagli sui metadati della connessione.
* Consulta il documento [Architettura di Universal Editor](/help/implementing/universal-editor/architecture.md#service) per maggiori dettagli sulla struttura di Universal Editor.
* Consulta il documento [Sviluppo locale AEM con Universal Editor](/help/implementing/universal-editor/local-dev.md) per ulteriori dettagli su come connettersi a una versione con hosting autonomo di Universal Editor.
* Consulta il documento [Utilizzo di Sling Resource Merger in Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/sling-resource-merger.md) per ulteriori dettagli sui nodi sovrapposti.
