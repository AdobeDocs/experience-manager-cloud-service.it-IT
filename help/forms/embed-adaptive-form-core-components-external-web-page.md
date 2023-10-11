---
title: Come possiamo incorporare un modulo adattivo in una pagina web esterna?
description: Scopri come incorporare un modulo adattivo in una pagina web esterna
contentOwner: Khushwant Singh
docset: CloudService
role: Developer
exl-id: 198f6f76-1134-4818-89a0-6ddc84ff956c
source-git-commit: fb3d3732f698015151d9703bfddfe94b531d31b6
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 1%

---

# Incorporare un modulo adattivo basato su componenti core in una pagina web esterna {#embed-adaptive-form-in-external-web-page}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Questo articolo |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html) |


È possibile [incorporare moduli adattivi in una pagina AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md) o una pagina web ospitata al di fuori dell’AEM. Il modulo adattivo incorporato è completamente funzionante e gli utenti possono compilare e inviare il modulo senza uscire dalla pagina. Consente all’utente di rimanere nel contesto di altri elementi della pagina web e interagire contemporaneamente con il modulo.

## Prerequisiti {#prerequisites}

Prima di incorporare un modulo adattivo in un sito web esterno, effettua le seguenti operazioni

* Pubblica il modulo adattivo da incorporare nell’istanza di pubblicazione del server AEM Forms.
* Crea o identifica una pagina web sul sito web che ospiti il modulo adattivo. Assicurati che la pagina web possa [leggere i file jQuery da una rete CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) oppure dispone di una copia locale di jQuery incorporata. jQuery è necessaria per eseguire il rendering di un modulo adattivo.
* Quando il server AEM e la pagina web si trovano su domini diversi, esegui i passaggi elencati nella sezione, [consentire ad AEM Forms di distribuire moduli adattivi a un sito tra più domini](#cross-site).

## Incorpora modulo adattivo {#embed-adaptive-form}

Per incorporare un modulo adattivo, inserisci alcune righe di JavaScript nella pagina web. L’API nel codice invia una richiesta HTTP al server AEM per le risorse dei moduli adattivi e inserisce il modulo adattivo nel contenitore di moduli specificato.

Per incorporare il modulo adattivo:

1. Creare una pagina Web nel sito Web con il codice seguente:

   ```html
        <!doctype html>
        <html>
          <head>
            <title>This is the title of the webpage!</title>
            <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
          </head>
          <body>
          <div class="customafsection"/>
            <p>This section is replaced with the adaptive form.</p>
   
         <script>
         var options = {path:"/content/forms/af/myadaptiveform.html", CSS_Selector:".customafsection"};
         alert(options.path);
         var loadAdaptiveForm = function(options){
         //alert(options.path);
            if(options.path) {
                // options.path refers to the path of the adaptive form
                // For Example: /content/forms/af/ABC, where ABC is the adaptive form
                // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
                var path = options.path;
                $.ajax({
                    url  : path ,
                    type : "GET",
                    data : {
                        // wcmmode=disabled is only required for author instance
                        // wcmmode : "disabled"
                    },
                    async: false,
                    success: function (data) {
                        // If jquery is loaded, set the inner html of the container
                        // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not        evaluate the script tag in HTML as per the HTML5 spec
                        // For example: document.getElementById().innerHTML
                        if(window.$ && options.CSS_Selector){
                            // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the        script tag.
                            $(options.CSS_Selector).html(data);
                        }
                    },
                    error: function (data) {
                        // any error handler
                    }
                });
            } else {
                if (typeof(console) !== "undefined") {
                    console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
                }
            }
         }(options);
   
         </script>
          </body>
        </html>
   ```

1. Nel codice incorporato:

   * Modifica il valore di *options.path* variabile con il percorso dell’URL di pubblicazione del modulo adattivo. Se il server AEM è in esecuzione su un percorso di contesto, accertati che l’URL includa il percorso di contesto. Menziona sempre il nome completo del modulo adattivo, inclusa l’estensione.   Ad esempio, il codice di cui sopra e adaptive from risiedono sullo stesso server di moduli AEM, in modo che l’esempio utilizzi il percorso contestuale del modulo adattivo /content/forms/af/locbasic.html.
   * CSS_Selector è il selettore CSS del contenitore di moduli in cui è incorporato il modulo adattivo. Ad esempio, la classe css .customafsection è il selettore CSS nell&#39;esempio precedente.

Il modulo adattivo è incorporato nella pagina web. Osserva quanto segue nel modulo adattivo incorporato:

* Le bozze e i moduli inviati sono disponibili nella scheda Bozze e invii del portale Forms.
* L’azione di invio configurata nel modulo adattivo originale viene mantenuta nel modulo incorporato.
* Le regole dei moduli adattivi vengono mantenute e sono completamente funzionali nel modulo incorporato.
* Il targeting delle esperienze e i test A/B configurati nel modulo adattivo originale non funzionano nel modulo incorporato.
* Se Adobe Analytics è configurato nel modulo originale, i dati di analisi vengono acquisiti nel server Adobe Analytics. Tuttavia, non è disponibile nel rapporto di Forms Analytics.
* In Forms adattivo basato su componenti core, le librerie client (ClientLibs) sono incluse e caricate insieme ai componenti Intestazione e Piè di pagina di un modulo. Pertanto, quando incorpori un Forms adattivo basato su componenti core in una pagina web, questo include sempre Intestazione e piè di pagina del modulo.

## Topologia di esempio {#sample-topology}

La pagina web esterna che incorpora il modulo adattivo invia le richieste al server AEM, che in genere si trova dietro il firewall in una rete privata. Per garantire che le richieste vengano indirizzate in modo sicuro al server AEM, si consiglia di impostare un server proxy inverso.

Vediamo un esempio di come configurare un server proxy inverso Apache 2.4 senza Dispatcher. In questo esempio, ospiterai il server AEM con `/forms` percorso e mappa contestuali `/forms` proxy inverso. In questo modo, ogni richiesta di `/forms` sul server Apache sono indirizzati all’istanza AEM. Questa topologia consente di ridurre il numero di regole a livello di Dispatcher, in quanto tutte le richieste hanno il prefisso `/forms` indirizzare al server AEM.

1. Apri `httpd.conf` e rimuovi il commento dalle seguenti righe di codice. In alternativa, è possibile aggiungere queste righe di codice nel file.

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. Imposta le regole proxy aggiungendo le seguenti righe di codice nel `httpd-proxy.conf` file di configurazione.

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   Sostituisci `[AEM_Instance]` con l’URL di pubblicazione del server AEM nelle regole.

Se non si monta il server AEM su un percorso contestuale, le regole proxy a livello di Apache saranno le seguenti:

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>Se configuri un’altra topologia, accertati di aggiungere l’URL di invio, il precaricamento e altri URL al inserisco nell&#39;elenco Consentiti di invio a livello di dispatcher.

## Best practice {#best-practices}

Quando incorpori un modulo adattivo in una pagina web, considera le seguenti best practice:

* Assicurati che le regole di stile definite nel CSS della pagina web non siano in conflitto con il CSS dell’oggetto modulo. Per evitare i conflitti, puoi riutilizzare il CSS della pagina web nel tema del modulo adattivo utilizzando la libreria client AEM. Per informazioni sull’utilizzo della libreria client nei temi dei moduli adattivi, consulta [Temi in AEM Forms](/help/forms/using-themes-in-core-components.md).
* Fare in modo che il contenitore del modulo nella pagina Web utilizzi l&#39;intera larghezza della finestra. In questo modo le regole CSS configurate per i dispositivi mobili funzionano senza modifiche. Se il contenitore del modulo non occupa l’intera larghezza della finestra, è necessario scrivere file CSS personalizzati per adattare il modulo a dispositivi mobili diversi.
* Utilizzare `[getData](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API per ottenere la rappresentazione XML o JSON dei dati del modulo nel client.
* Utilizzare `[unloadAdaptiveForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)` API per scaricare il modulo adattivo dal DOM HTML.
* Imposta l’intestazione access-control-origin quando invii una risposta dal server AEM.

## Consentire ad AEM Forms di distribuire moduli adattivi a un sito tra più domini {#cross-site}

1. Nell’istanza di pubblicazione dell’AEM, vai a Gestione configurazione della console web dell’AEM all’indirizzo `https://'[server]:[port]'/system/console/configMgr`.
1. Individuare e aprire **Filtro referrer Apache Sling** configurazione.
1. Nel campo Host consentiti specifica il dominio in cui si trova la pagina web. Consente all&#39;host di effettuare richieste POST al server AEM. È inoltre possibile utilizzare espressioni regolari per specificare una serie di domini di applicazioni esterni.
