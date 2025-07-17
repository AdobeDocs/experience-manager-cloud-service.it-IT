---
title: Architettura dei moduli HTML5
description: HTML5 Forms viene distribuito come pacchetto all’interno dell’istanza AEM incorporata ed espone la funzionalità come endpoint REST su HTTP/S utilizzando l’architettura RESTful Apache Sling.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
hide: true
hidefromtoc: true
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '1996'
ht-degree: 0%

---

# Architettura dei moduli HTML5{#architecture-of-html-forms}

<span class="preview"> La funzionalità HTML5 Forms è disponibile come parte del programma di accesso anticipato. Per richiedere l’accesso, invia un’e-mail dal tuo ID e-mail ufficiale (di lavoro) a aem-forms-ea@adobe.com.
</span>

## Architettura {#architecture}

La funzionalità di HTML5 Forms viene distribuita come pacchetto all&#39;interno dell&#39;istanza AEM incorporata ed è esposta come endpoint REST su HTTP/S utilizzando RESTful [Apache Sling Architecture](https://sling.apache.org/).

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Utilizzo di Sling Framework {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) è incentrato sulle risorse. Utilizza un URL di richiesta per risolvere prima la risorsa. Ogni risorsa ha una proprietà **sling:resourceType** (o **sling:resourceSuperType**). In base a questa proprietà, al metodo di richiesta e alle proprietà dell’URL della richiesta, viene quindi selezionato uno script sling per gestire la richiesta. Questo script sling può essere un JSP o un servlet. Per i moduli HTML5, i nodi **Profile** fungono da risorse sling e **Profile Renderer** funge da script sling che gestisce la richiesta di rendering del modulo mobile con un profilo specifico. Un **modulo di rendering profili** è una JSP che legge i parametri da una richiesta e chiama il servizio Forms OSGi.

Per informazioni dettagliate sull&#39;endpoint REST e sui parametri di richiesta supportati, vedere [Rendering del modello di modulo](/help/forms/rendering-form-template.md).

Quando un utente effettua una richiesta da un dispositivo client come un browser iOS o Android™, Sling risolve prima il nodo del profilo in base all’URL della richiesta. Da questo nodo profilo vengono letti **sling:resourceSuperType** e **sling:resourceType** per determinare tutti gli script disponibili che possono gestire questa richiesta di rendering del modulo. Quindi utilizza i selettori di richieste Sling insieme al metodo di richiesta per identificare lo script più adatto per la gestione di questa richiesta. Una volta che la richiesta raggiunge una JSP di rendering del profilo, JSP chiama il servizio OSGi di Forms.

Per ulteriori dettagli sulla risoluzione dello script Sling, consulta [Scheda di riferimento rapido di AEM Sling](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it) o [Scomposizione URL Apache Sling](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html).

#### Flusso di chiamata di elaborazione modulo tipico {#typical-form-processing-call-flow}

I moduli di HTML5 memorizzano nella cache tutti gli oggetti intermedi necessari per elaborare (rendering o invio) un modulo alla prima richiesta. Non memorizza in cache gli oggetti dipendenti dai dati, in quanto tali oggetti potrebbero cambiare.

Mobile Form mantiene due diversi livelli di cache, PreRender cache e Render cache. La cache di preRender contiene tutti i frammenti e le immagini di un modello risolto, mentre la cache di rendering contiene contenuto renderizzato come HTML.

![Flusso di lavoro per moduli HTML5](assets/cacheworkflow.png)

Flusso di lavoro per moduli HTML5

I moduli HTML5 non memorizzano in cache i modelli con riferimenti mancanti di frammenti e immagini. Se i moduli di HTML5 richiedono più tempo del normale, controlla i registri del server per individuare eventuali riferimenti e avvisi mancanti. Verificare inoltre che non venga raggiunta la dimensione massima dell&#39;oggetto.

Il servizio OSGi di Forms elabora una richiesta in due passaggi:

* **Generazione dello stato del layout e del modulo iniziale**: il servizio di rendering OSGi di Forms chiama il componente Cache di Forms per determinare se il modulo è già stato memorizzato nella cache e non è stato invalidato. Se il modulo è memorizzato in cache ed è valido, viene distribuito dalla cache al HTML generato. Se il modulo viene invalidato, il servizio di rendering Forms OSGi genera il layout modulo iniziale e lo stato del modulo in formato XML. Questo XML viene trasformato in layout HTML e stato iniziale del modulo JSON dal servizio Forms OSGi e quindi memorizzato nella cache per le richieste successive.
* **Forms precompilato**: durante il rendering, se un utente richiede moduli con dati precompilati, il servizio di rendering OSGi di Forms chiama il contenitore del servizio Forms e genera un nuovo stato del modulo con dati uniti. Tuttavia, poiché il layout è già generato nel passaggio precedente, questa chiamata è più veloce della prima chiamata. Questa chiamata esegue solo l’unione dei dati ed esegue gli script sui dati.

Se nel modulo sono presenti aggiornamenti o risorse utilizzate all’interno del modulo, il componente Cache modulo lo rileva e la cache per quel particolare modulo viene invalidata. Una volta completata l’elaborazione da parte del servizio OSGi di Forms, JSP aggiunge al modulo i riferimenti e lo stile della libreria JavaScript e restituisce la risposta al client. Un server Web tipico come [Apache](https://httpd.apache.org/) può essere utilizzato qui con la compressione HTML attivata. Un server web ridurrebbe in modo significativo le dimensioni della risposta, il traffico di rete e il tempo necessario per lo streaming dei dati tra server e computer client.

Quando un utente invia il modulo, il browser invia lo stato del modulo in formato JSON al proxy del servizio [submit](/help/forms/service-proxy.md); il proxy del servizio di invio genera un XML dati utilizzando i dati JSON e invia tale XML dati all&#39;endpoint di invio.

## Componenti {#components}

Per abilitare HTML5 Forms è necessario il pacchetto del componente aggiuntivo AEM Forms. Per informazioni sull&#39;installazione del pacchetto del componente aggiuntivo AEM Forms, vedere [Installazione e configurazione di AEM Forms](/help/forms/setup-local-development-environment.md).

### Componenti OSGi (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe XFA Forms Renderer (com.adobe.livecycle.adobe-lc-forms-core)** è il nome visualizzato del bundle OSGi per HTML5 Forms visualizzato nella visualizzazione Bundle della console di amministrazione Felix `(https://[host]:[port]/system/console/bundles)`.

Questo componente contiene componenti OSGi per le impostazioni di rendering, gestione della cache e configurazione.

#### Servizio Forms OSGi {#forms-osgi-service}

Questo servizio OSGi contiene la logica per il rendering di un XDP come HTML e gestisce l’invio di un modulo per generare l’XML dei dati. Questo servizio utilizza il contenitore del servizio Forms. Il contenitore del servizio Forms chiama internamente il componente nativo `XMLFormService.exe` che esegue l&#39;elaborazione.

Se viene ricevuta una richiesta di rendering, questo componente chiama il contenitore del servizio Forms per generare informazioni su layout e stato che vengono ulteriormente elaborate per generare gli stati DOM dei moduli HTML e JSON.

Questo componente è anche responsabile della generazione di dati XML da JSON dello stato del modulo inviato.

#### Componente cache {#cache-component}

HTML5 forms utilizza la memorizzazione nella cache per ottimizzare la velocità effettiva e i tempi di risposta. Puoi configurare il livello del servizio cache per ottimizzare il compromesso tra prestazioni e utilizzo dello spazio.

<table>
 <tbody>
  <tr>
   <th>Strategia cache</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Nessuna</td>
   <td>Non memorizzare in cache gli artefatti<br /> </td>
  </tr>
  <tr>
   <td>Conservatore</td>
   <td>Memorizza nella cache solo gli artefatti intermedi generati prima del rendering del modulo, ad esempio il modello contenente frammenti e immagini in linea</td>
  </tr>
  <tr>
   <td>Aggressivo</td>
   <td>Memorizza nella cache contenuto HTML sottoposto a rendering<br /> Memorizza nella cache tutti gli artefatti memorizzati nella cache a livello conservativo.<br /> <strong>Nota</strong>: questa strategia offre prestazioni migliori, ma consuma più memoria per l'archiviazione degli artefatti memorizzati nella cache.</td>
  </tr>
 </tbody>
</table>

I moduli HTML5 eseguono il caching in memoria utilizzando la strategia LRU. Se la strategia della cache è impostata su Nessuno, la cache non verrà creata e i dati esistenti, se presenti, verranno cancellati. Oltre alla strategia di caching, puoi anche configurare la dimensione totale della cache in memoria, che può essere utile per avere la dimensione massima associata alla cache e, se va oltre, utilizzerà la modalità LRU per liberare le risorse della cache.

>[!NOTE]
>
>La cache in memoria non è condivisa tra i nodi del cluster.

#### Servizio di configurazione {#configuration-service}

Il servizio di configurazione consente di ottimizzare i parametri di configurazione e le impostazioni della cache per i moduli HTML5.

Per aggiornare queste impostazioni, vai a CQ Felix Admin Console (disponibile all&#39;indirizzo https://&lt;&#39;[server]:[porta]&#39;/system/console/configMgr), cerca e seleziona Configurazione Forms mobile.

Puoi configurare la dimensione della cache o disabilitarla utilizzando il servizio di configurazione. È inoltre possibile abilitare il debug utilizzando il parametro Opzioni di debug. Ulteriori informazioni sul debug dei moduli sono disponibili all&#39;indirizzo [Debug dei moduli HTML5](/help/forms/debug.md).

### Componenti runtime (adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

Il pacchetto runtime contiene le librerie lato client utilizzate per il rendering di HTML Form.

**Componenti importanti disponibili come parte del pacchetto runtime:**

#### Motore di script {#scripting-engine}

L’implementazione XFA di Adobe supporta due tipi di linguaggi di script per consentire l’esecuzione logica definita dall’utente nei moduli: JavaScript e FormCalc.

Il motore di script di HTML Forms è scritto in JavaScript per supportare l’API di script XFA in entrambi questi linguaggi.

Al momento del rendering, lo script FormCalc viene tradotto (e memorizzato nella cache) in JavaScript sul server in modo trasparente per l’utente o la finestra di progettazione.

Questo motore di script utilizza alcune funzionalità di ECMAScript5 come Object.defineProperty. Il motore o la libreria viene distribuito come libreria client CQ con il nome di categoria **xfaforms.profile**. Fornisce inoltre l&#39;**API FormBridge** per consentire l&#39;interazione di applicazioni o portali esterni con il modulo. Utilizzando FormBridge, un&#39;app esterna può nascondere alcuni elementi a livello di programmazione, ottenerne o impostarne i valori o modificarne gli attributi.

Per ulteriori dettagli, vedere l&#39;articolo [Bridge](/help/forms/integrate-form-bridge-forms-portal.md) del modulo.

#### Motore di layout {#layout-engine}

Il layout e l&#39;aspetto visivo dei moduli HTML5 si basano sulle funzioni di SVG 1.1, jQuery, BackBone e CSS3. L’aspetto iniziale di un modulo viene generato e memorizzato nella cache del server. La modifica del layout iniziale e le ulteriori modifiche incrementali al layout del modulo vengono gestite sul client. Per ottenere questo risultato, il pacchetto Runtime contiene un motore di layout scritto in JavaScript e basato su jQuery/Backbone. Questo motore gestisce tutti i comportamenti dinamici, ad esempio Aggiungi/Rimuovi istanze ripetibili, layout di oggetti di crescita. Questo motore di layout esegue il rendering di un modulo una pagina alla volta. Inizialmente, un utente visualizza solo una pagina e la barra di scorrimento orizzontale tiene conto solo della prima pagina. Tuttavia, quando un utente scorre verso il basso, inizia il rendering della pagina successiva. Questa rappresentazione pagina per pagina riduce il tempo necessario per il rendering della prima pagina in un browser e migliora le prestazioni percepite del modulo. Questo motore/libreria fa parte della libreria client CQ con il nome di categoria **xfaforms.profile**.

Il motore di layout contiene anche un set di widget utilizzati per acquisire il valore dei campi modulo da un utente. Questi widget sono modellati come [jQuery UI Widget](https://api.jqueryui.com/jQuery.widget/) che implementano alcuni contratti aggiuntivi per funzionare senza problemi con il motore di layout.

Per ulteriori dettagli sui widget e i contratti corrispondenti, vedere [Widget personalizzati per HTML5 forms](/help/forms/custom-widgets.md).

#### Attribuzione stile {#styling}

Lo stile associato agli elementi HTML viene aggiunto in linea o in base al blocco CSS incorporato. Alcuni stili comuni che non dipendono dalla forma fanno parte della libreria client CQ con il nome di categoria xfaforms.profile.

Oltre alle proprietà di stile predefinite, ogni elemento modulo contiene alcune classi CSS basate su tipo di elemento, nome e altre proprietà. Utilizzando queste classi, è possibile ridefinire gli elementi specificando il proprio CSS.

Per ulteriori dettagli sugli stili e le classi predefiniti, vedere [Introduzione agli stili](/help/forms/css-styles.md).

#### Script lato server e servizi Web {#server-side-script-and-web-services}

Tutti gli script contrassegnati per l&#39;esecuzione sul server o per la chiamata a un servizio Web (indipendentemente dalla posizione in cui è contrassegnato per l&#39;esecuzione) vengono sempre eseguiti sul server.

Il motore di script client:

1. Effettua una chiamata sincrona al server passando lo stato corrente del modulo sotto forma di JSON
1. Esegue lo script o il servizio Web sul server
1. Genera un nuovo stato JSON
1. Unisce il nuovo stato JSON sul client quando viene restituita la risposta.

#### Bundle risorse di localizzazione {#localization-resource-bundles}

I moduli di HTML5 supportano la lingua italiana (it), spagnola (es), portoghese brasiliano (pt_BR), cinese semplificato (zh_CN), cinese tradizionale (solo supporto limitato) (zh_TW), coreano (ko_KR), inglese (en_US), francese (fr_FR), tedesco (de_DE) e giapponese (ja). In base alle impostazioni locali ricevute nell’intestazione della richiesta, il Bundle di risorse corrispondente viene inviato al client. Questo bundle di risorse viene aggiunto a JSP profilo come libreria client CQ con nome categoria **xfaforms.I18N**. È possibile ignorare la logica di prelievo del pacchetto delle impostazioni internazionali nel profilo.

### Componenti Sling (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Il pacchetto Sling contiene contenuti relativi a Profili e Profile Renderer.

#### Profili {#profiles}

I profili sono i nodi Resource in Sling che rappresentano un modulo o una famiglia di Forms. A livello CQ, questi profili sono nodi JCR. I nodi si trovano nella cartella **/content** nell&#39;archivio JCR e possono trovarsi in qualsiasi sottocartella della cartella **/content**.

#### Rendering profilo {#profile-renderers}

Il nodo Profilo ha una proprietà **sling:resourceSuperType** con valore **xfaforms/profile**. Questa proprietà invia internamente le richieste di inoltro allo script sling per i nodi di profilo nella cartella **/libs/xfaforms/profile**. Questi script sono pagine JSP, ovvero contenitori per la creazione di moduli HTML e degli artefatti JS/CSS richiesti. Le pagine includono riferimenti a:

* **xfaforms.I18N.&lt;impostazioni locali>**: questa libreria contiene dati localizzati.
* **xfaforms.profile**: questa libreria contiene l&#39;implementazione per il motore di script e layout XFA.

Queste librerie sono modellate come librerie client CQ e sfruttano i vantaggi della concatenazione automatica, della minimizzazione e della compressione delle librerie JavaScript del framework CQ.
Per ulteriori informazioni sulle librerie client CQ, consulta la [documentazione Clientlib CQ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it).

Come descritto in precedenza, il modulo di rendering del profilo JSP chiama il servizio Forms tramite un’inclusione sling. Questa JSP imposta anche varie opzioni di debug in base alla configurazione amministratore o ai parametri di richiesta.

I moduli di HTML5 consentono agli sviluppatori di creare profili e di personalizzare l&#39;aspetto dei moduli. HTML Form consente ad esempio agli sviluppatori di integrare i moduli in un pannello o in una sezione &lt;div> di un portale HTML esistente.
Per ulteriori dettagli sulla creazione di profili personalizzati, vedere [Creazione di un profilo personalizzato](/help/forms/custom-profile.md).
