---
title: Funzioni obsolete e rimosse
description: Note sulla versione specifiche per le funzioni obsolete e rimosse in  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: 04ec933125da9ee3c84ffd948b144581d31763d6
workflow-type: tm+mt
source-wordcount: '2485'
ht-degree: 100%

---

# Funzioni e API obsolete e rimosse {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Funzioni obsolete e rimosse in AEM as a Cloud Service"
>abstract="AEM as a Cloud Service dispone di un modello di distribuzione nativo per il cloud. Alcune funzionalità sono state sostituite da controparti native per il cloud e sono ora visualizzate in questa scheda."

Adobe valuta costantemente le funzionalità dei prodotti, per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne, al fine di migliorare il valore complessivo per la clientela, tenendo comunque in considerazione la compatibilità con le versioni precedenti. Inoltre, poiché [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] offre un modello di distribuzione nativo per il cloud, alcune funzionalità sono state sostituite da controparti native per il cloud.

Per comunicare l’imminente rimozione/sostituzione delle funzionalità [!DNL Experience Manager], si applicano le seguenti regole:

1. Innanzitutto viene annunciato che una data funzione diventa obsoleta. Le funzionalità obsolete rimangono comunque disponibili, ma non vengono più aggiornate.
1. Le funzionalità annunciate come obsolete vengono rimosse nella versione principale successiva, non appena possibile. La data effettiva per la rimozione viene annunciata.

Questo processo offre ai clienti almeno un ciclo di rilascio per adattare la loro implementazione a una nuova versione o alla funzionalità che prenderà il posto di quella dichiarata obsoleta, prima che venga definitivamente rimossa.

## Funzioni obsolete {#deprecated-features}

In questa sezione sono elencate le funzionalità contrassegnate come obsolete in [!DNL Experience Manager] as a [!DNL Cloud Service]. In genere, le funzioni pianificate per la rimozione in una versione futura vengono impostate come obsolete e ne viene indicata un’alternativa.

Consigliamo ai clienti di verificare se utilizzano la funzione/funzionalità nella loro implementazione corrente e di pianificarne la modifica adottando l’alternativa fornita.

| Funzionalità | Funzione obsoleta | Sostituzione |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | [API di utilizzo di JavaScript](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) | [API di utilizzo di Java](https://experienceleague.adobe.com/it/docs/experience-manager-htl/content/java-use-api) |
| [!DNL Sites] | Proprietà di Frammenti di esperienza per **Stato social media**. | La funzione verrà rimossa presto. |
| [!DNL Sites] | Frammenti di contenuto semplici basati su modelli. | [Frammenti di contenuto strutturati basati su modelli](/help/assets/content-fragments/content-fragments-models.md) ora. |
| [!DNL Assets] | Flusso di lavoro di `DAM Asset Update` per elaborare le immagini acquisite. | Per l’inserimento delle risorse si utilizzano ora i [microservizi per le risorse](/help/assets/asset-microservices-overview.md). |
| [!DNL Assets] | Carica risorse direttamente in [!DNL Experience Manager]. Consulta [API di caricamento risorse obsolete](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Utilizza il [caricamento binario diretto](/help/assets/add-assets.md). Per informazioni di carattere tecnico, consulta l’articolo sulle [API di caricamento diretto](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Alcuni passaggi](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) del flusso di lavoro `DAM Asset Update` non sono supportati, inclusa la chiamata di strumenti della riga di comando come [!DNL ImageMagick]. | [I microservizi per le risorse](/help/assets/asset-microservices-overview.md) sostituiscono numerosi flussi di lavoro. Per l’elaborazione personalizzata, utilizza i [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Transcodifica FFmpeg dei video. | Per generare le miniature FFmpeg, utilizza i [microservizi per le risorse](/help/assets/asset-microservices-overview.md). Per la transcodifica FFmpeg, utilizza [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | Interfaccia utente di replica ad albero nella scheda “Distribuisci” dell’agente di replica (rimozione dopo il 30 settembre 2021) | [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o approcci al [flusso di lavoro della struttura dei contenuti di pubblicazione](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | Né la scheda Distribuzione nella schermata di amministrazione dell’agente di replica né l’API di replica possono essere utilizzate per replicare pacchetti di contenuti superiori a 10 MB. È invece possibile utilizzare [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o il [flusso di lavoro della struttura dei contenuti di pubblicazione](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | Le integrazioni che utilizzano credenziali generate dai progetti di Adobe Developer Console perderanno gradualmente il supporto per le credenziali dell’account servizio (JWT). Non sarà possibile creare nuove credenziali dell’account servizio (JWT) in Adobe Developer Console a partire dal 1° maggio 2024, anche se le credenziali dell’account servizio (JWT) esistenti possono ancora essere utilizzate per le integrazioni già configurate fino al 1° gennaio 2025, momento in cui le credenziali dell’account servizio (JWT) esistenti non funzioneranno più e i clienti dovranno effettuare la migrazione alle credenziali da server a server OAuth. [Ulteriori informazioni](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console). | [Migra](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) alle credenziali da server a server OAuth. |

## Funzioni rimosse {#removed-features}

In questa sezione sono elencate le funzionalità che sono state rimosse da [!DNL Experience Manager] con [!DNL Experience Manager] as a [!DNL Cloud Service].

| Area | Funzione obsoleta | Sostituzione | Data di rimozione prevista |
| ------------ | ------------------ | ----------- | ------------------- |
| Interfaccia utente | L’interfaccia utente classica viene rimossa dall’interfaccia utente del prodotto. Sono disponibili alcune finestre di dialogo dell’interfaccia utente classica per alcune funzionalità, come Verifica collegamenti, Pulizia versione e alcune configurazioni di Cloud Service. I prossimi [aggiornamenti dei prodotti](/help/release-notes/home.md) potrebbero rimuovere ulteriormente la disponibilità dell’interfaccia utente classica. | Interfaccia standard | Rimosso |
| [!DNL Dynamic Media] | Le integrazioni precedenti con [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=it#integration) e la [modalità ibrida di Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=it#dynamic) non sono disponibili in [!DNL Experience Manager] as a [!DNL Cloud Service]. | Utilizza la versione di [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) fornita con [!DNL Experience Manager] as a [!DNL Cloud Service]. | Rimosso |
| [!DNL Sites] | Portal Director e componente Portlet | Queste funzionalità sono diventate obsolete in [!DNL Experience Manager] 6.4 e ora sono state rimosse da [!DNL Experience Manager]. | Rimosso |
| [!DNL Sites] | Importazione progettazione | Questa funzionalità è stata rimossa perché le sezioni non modificabili dell’archivio [!DNL Experience Manager] non sono accessibili in fase di esecuzione. | Rimosso |
| [!DNL Assets] | La condivisione di [!DNL Assets] con il servizio di base Experience Cloud Assets e i servizi Creative Cloud non è disponibile. | Per l’integrazione con [!DNL Adobe Creative Cloud], utilizza [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html). | Rimosso |
| [!DNL Foundation] | Supporto per le origini dati Apache Sling (OSGi bundle org.apache.sling.datasource) | N/D | Rimosso |
| [!DNL Foundation] | Supporto per i modelli di script JST (OSGi bundle org.apache.sling.scripting.jst) | N/D | Rimosso |
| [!DNL Foundation] | Supporto per Apache Felix Http Whiteboard | OSGi Http Whiteboard | Marzo 2022 |
| [!DNL Foundation] | Supporto per com.adobe.granite.oauth.server | Integrazione di Adobe IMS | Marzo 2023 |
| [!DNL Foundation] | Supporto per la funzione org.apache.sling.serviceusermapping per [ottenere l’ID utente del servizio](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-) | N/D | 30/08/24 |


## API AEM {#aem-apis}

Di seguito è riportato un ampio elenco delle API AEM obsolete con la relativa data di rimozione prevista. I clienti dovranno rimuovere le API dal proprio codice entro la data di rimozione prevista. L’eventuale uso delle API dopo la data di rimozione causerà errori nell’ambiente di SDK/sviluppo locale e nel processo di compilazione di Cloud Manager.

<details>
  <summary>Espandi per visualizzare l’elenco delle API obsolete.</summary>
<table style="table-layout:auto">
  <tr>
    <th>Pacchetto/Classe</th>
    <th>Commenti</th>
    <th>Data di rimozione</th>
    <th>Data di rimozione prevista</th>
  </tr>
<tbody>
  <tr>
    <td>org.apache.sling.commons.auth<br>org.apache.sling.commons.auth.spi</td>
    <td>Utilizzare le interfacce Auth Core/Auth Core SPI Sling come alternativa. <a href="#org.apache.sling.commons.auth">Consulta le note sulla rimozione di seguito.</a></td>
    <td>2015</td>
    <td>30/07/2021</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>30/07/2021</td>
  </tr>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>Utilizzare l’API Discovery di Sling in alternativa</td>
    <td>2015</td>
    <td>rimosso</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
    <td>01/03/2021</td>
    <td>rimosso</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
    <td>05/03/2021</td>
    <td>rimosso</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>L’implementazione Apache Johnzon di <a href="https://johnzon.apache.org/index.html">javax.json</a> è consigliata e deve essere utilizzata. </td>
    <td>30/04/2021</td>
    <td>31/12/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>Gli strumenti personalizzati di gestione della persistenza non sono supportati in AEM as a Cloud Service.</td>
    <td>30/04/2021</td>
    <td>rimosso</td>
  </tr>
  <tr>
    <td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 è in modalità di manutenzione. Utilizzare Commons Lang 3.</td>
    <td>30/04/2021</td>
    <td>31/12/2021</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 è in modalità di manutenzione. Utilizzare Commons Collections 4.</td>
    <td>30/04/2021</td>
    <td>31/12/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>Si consiglia l’uso dell’API HealthCheck di Apache Felix</td>
    <td>30/04/2021</td>
    <td>rimosso</td>
  </tr>
  <tr>
    <td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n</td>
    <td>La console Web Felix non è supportata negli ambienti cloud</td>
    <td>30/04/2021</td>
    <td>30/07/2021</td>
  </tr>
  <tr> <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml</td>
    <td>I pacchetti Eclipse Jetty e Felix Http Jetty non sono più supportati. <a href="#org.eclipse.jetty">Consulta le note sulla rimozione di seguito.</a></td>
    <td>27/05/2021</td>
    <td>26/08/2021</td>
  </tr>
  <tr> <td>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.util<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread
</td>
    <td>I pacchetti Eclipse Jetty e Felix Http Jetty non sono più supportati.</td>
    <td>27/05/2021</td>
    <td>26/08/2021</td>
  </tr>  
  <tr>     <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>L’uso di questa API non è più supportato in AEM as a Cloud Service. <a href="#com.mongodb">Consulta le note sulla rimozione di seguito.</a></td>
    <td>27/05/2021</td>
    <td>30/07/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>Il metatipo Apache Felix e le API SCR sono obsoleti.  Utilizza invece il metatipo OSGi e le API Declarative Service.</td>
    <td>27/05/2021</td>
    <td>rimosso</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>Le classi di implementazione dei registri non sono compatibili con AEM as a Cloud Service.</td>
    <td>04/07/2021</td>
    <td>rimosso</td>
  </tr>
  <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>Questa API è obsoleta poiché Apache Abdera è un progetto ritirato nel 2017. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Consulta le note sulla rimozione di seguito.</a></td>
    <td>29/07/2021</td>
    <td>29/09/2021</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>Questa API è obsoleta poiché Apache Abdera è un progetto ritirato dal 2017.</td>
    <td>08/04/2019</td>
    <td>29/09/2021</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>API AEM 6.x legacy.</td>
    <td>08/04/2019</td>
    <td>rimosso</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Questa API non è supportata in Cloud Service.</td>
    <td>30/09/2021</td>
    <td>rimosso</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>Le classi di utilità correlate ad Apache Xerces vengono rimosse nelle versioni successive con un’importante modifica della versione. Poiché queste utilità sono destinate all’uso interno in Filevault, l’API è obsoleta e verrà eliminata dalla superficie API pubblica.</td>
    <td>01/09/2021</td>
    <td>rimosso</td>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>API AEM 6.x legacy. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Consulta le note sulla rimozione di seguito.</a></td>
    <td>08/04/2019</td>
    <td>29/09/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>Apache Felix Http Whiteboard non è più supportato. Esegui la migrazione del codice a OSGi HTTP Whiteboard. <a href="#org.apache.felix.http.whiteboard">Consulta le note sulla rimozione di seguito.</a></td>
    <td>27/01/2022</td>
    <td>24/03/2022</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>Questa API è obsoleta, esegui la migrazione del codice alle API XML fornite da JDK.</td>
    <td>27/01/2022</td>
    <td>24/03/2022</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>Questa API di logback interna non è supportata da AEM as a Cloud Service.</td>
    <td>27/01/2022</td>
    <td>24/03/2022</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>Questa API log4j interna non è supportata da AEM as a Cloud Service.</td>
    <td>27/01/2022</td>
    <td>24/03/2022</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1 ha raggiunto la fine del ciclo di vita nel 2015 e non è più supportato.</td>
    <td>27/01/2022</td>
    <td>24/03/2022</td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>Questa API di logback interna non è supportata da AEM as a Cloud Service.</td>
    <td>27/01/2022</td>
    <td>rimosso</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>È necessario aggiornare Handlebars da 4.0.5 a 4.3.0 a causa di vulnerabilità di sicurezza. Questo pacchetto non è più presente nella versione aggiornata di Handlebars.</td>
    <td>05/05/2022</td>
    <td>05/08/2022</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>Questa API non è più supportata. Utilizza invece org.apache.sling.api.resource.ResourceResolverFactory.</td>
    <td>29/09/2022</td>
    <td>24/11/2022</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>Questa API è obsoleta. Utilizza invece Apache Sling’s Builders.</td>
    <td>31/10/2022</td>
    <td>01/01/2023</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>Questa API non è supportata da AEM as a Cloud Service.</td>
    <td>15/5/2023</td>
    <td>15/6/2023</td>
  </tr><td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Le librerie Core Guava di Google sono obsolete.</td>
    <td>15/5/2023</td>
    <td>15/6/2023</td>
  </tr>
  <tr>
    <td>org.slf4j.event    </td>
    <td>Questa API slf4j interna non è supportata da AEM as a Cloud Service.</td>
    <td>11/04/2022</td>
    <td>30/08/2024</td>
  </tr>
  <tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>L’uso di questa API non è più supportato in AEM as a Cloud Service.</td>
    <td>17/05/2024</td>
    <td>30/06/2024</td>
  </tr>
  <tr>
    <td>com.day.cq.xss<br>com.day.cq.xss.taglib<br>com.day.cq.xss.impl</td>
    <td>Utilizza invece org.apache.sling.xss.</td>
    <td>12/12/2023</td>
    <td>30/06/2024</td>
  </tr>
  <tr>
    <td>com.adobe.granite.xss<br>com.adobe.granite.xss.impl</td>
    <td>Utilizza invece org.apache.sling.xss.</td>
    <td>12/12/2023</td>
    <td>30/06/2024</td>
  </tr>  
  <tr>
    <td>com.drew.*</td>
    <td>L’estrazione dei metadati da immagini e video dovrebbe essere eseguita tramite Asset Compute nel Cloud Service oppure tramite Apache POI o Apache Tika.</td>
    <td>17/09/2024</td>
    <td>17/12/2024</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.blob.*</td>
    <td></td>
    <td>23/09/2024</td>
    <td>23/12/2024</td>
  </tr>       
</tbody>
</table>
</details>

### Rimozione di `org.apache.sling.commons.auth*` {#org.apache.sling.commons.auth}

Se stai utilizzando `org.apache.sling.commons.auth` e/o `org.apache.sling.commons.auth.spi`, è possibile sostituirli eseguendo la migrazione del codice in `org.apache.sling.auth` resp. `org.apache.sling.auth.spi`. Se stai utilizzando una versione precedente di [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/), assicurati di eseguire l’aggiornamento alla versione più recente.

Elenco azioni:
* Aggiornamento di ACS AEM Commons alla versione più recente
* Esegui la migrazione da `org.apache.sling.commons.auth` e/o `org.apache.sling.commons.auth.spi` a `org.apache.sling.auth` resp.`org.apache.sling.auth.spi`.

### Rimozione di `org.eclipse.jetty*` {#org.eclipse.jetty}

Se stai utilizzando un elemento del pacchetto `org.eclipse.jetty` o uno dei relativi pacchetti secondari, è possibile eseguire la migrazione ad altre librerie di terze parti con funzionalità simile. Se la migrazione non è fattibile, aggiungi al progetto i bundle richiesti dall’elenco seguente.

Elenco azioni:
* Sostituisci l’utilizzo di pacchetti `org.eclipse.jetty` con altre librerie di terze parti/proprio codice o
* seleziona i bundle richiesti da questo elenco e aggiungili al progetto:
   * `org.eclipse.jetty:jetty-client:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-http:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-io:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-security:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-servlet:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-server:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util-ajax:9.4.54.v20240208`

### Rimozione di `com.mongodb` {#com.mongodb}

Aggiungi l’API client Mongo al progetto.

Elenco azioni:
* Aggiungi questo bundle al progetto
   * `org.mongodb:mongo-java-driver:3.12.7`

### Utilizzo di `org.apache.abdera*` e `org.apache.sling.atom.taglib` {#org.apache.abdera_or_org.apache.sling.atom.taglib}

Sostituisci l’utilizzo di qualsiasi pacchetto di `org.apache.abdera` e `org.apache.sling.atom.taglib` con una libreria di terze parti che fornisce funzionalità simili o il tuo codice.

Elenco azioni:
* Sostituisci l’utilizzo dei pacchetti di `org.apache.abdera` e `org.apache.sling.atom.taglib` con altre librerie di terze parti/proprio codice.

### Utilizzo di `org.apache.felix.http.whiteboard` {#org.apache.felix.http.whiteboard}

Sostituisci l’utilizzo di `org.apache.felix.http.whiteboard` con [OSGi Http Whiteboard](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html). L’API OSGi ufficiale dispone di funzionalità simili e, in molti casi, la sostituzione richiede solo di modificare le proprietà di registrazione del servizio.

Elenco azioni:
* Sostituisci l’utilizzo di `org.apache.felix.http.whiteboard` con [OSGi Http Whiteboard](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)

## Configurazione OSGI {#osgi-configuration}

I due elenchi seguenti riflettono l’area di configurazione OSGi di AEM as a Cloud Service e descrivono che cosa è possibile configurare.

1. Elenco di configurazioni OSGi che non devono essere configurate dal codice cliente
1. Un elenco di configurazioni OSGi le cui proprietà possono essere configurate, ma devono rispettare le regole di convalida indicate. Queste regole includono se è necessaria la dichiarazione della proprietà, il tipo e, in alcuni casi, l’intervallo di valori consentito.

Se una configurazione OSGI non è elencata, potrebbe essere configurata dal codice cliente.

Queste regole vengono convalidate durante il processo di compilazione di Cloud Manager. Con il passare del tempo è possibile aggiungere altre regole e la data di applicazione prevista è indicata nella tabella. I clienti sono tenuti a rispettare queste regole entro la data di applicazione prevista. Il mancato rispetto delle regole dopo la data di rimozione genererà errori nel processo di compilazione di Cloud Manager. I progetti Maven devono includere [plug-in Maven di Build Analyzer nell’SDK di AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=it) per segnalare gli errori di configurazione OSGI durante lo sviluppo dell’SDK locale.

Ulteriori informazioni sulla configurazione OSGI sono disponibili in [questa posizione](/help/implementing/deploying/configuring-osgi.md).

+++Configurazioni OSGi che non possono essere modificate.
* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Data annuncio: 30/4/2021, Data applicazione: 31/7/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Data annuncio: 30/4/2021, Data applicazione: 31/7/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Data annuncio: 30/4/2021, Data applicazione: 31/7/2021)
* **`org.apache.felix.http (Factory)`** (Data annuncio: 30/4/2021, Data applicazione: 31/7/2021)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (Data annuncio: 25/8/2021, Data applicazione: 26/11/2021)
+++

+++Le configurazioni OSGi sono soggette alle regole di convalida della build.
* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Data annuncio: 30/4/2021, Data applicazione: 31/7/2021)
* `org.apache.felix.eventadmin.ThreadPoolSize`
   * Tipo: numero intero
   * Intervallo richiesto: 2-100
* `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
   * Tipo: doppio
* `org.apache.felix.eventadmin.Timeout`
   * Tipo: numero intero
* `org.apache.felix.eventadmin.RequireTopic`
   * Tipo: booleano
* `org.apache.felix.eventadmin.IgnoreTimeout`
   * Obbligatorio
   * Tipo: array di stringhe
   * Intervallo richiesto: deve includere almeno tutti `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
* `org.apache.felix.eventadmin.IgnoreTopic`
   * Tipo: array di stringhe
* **`org.apache.felix.http`** (Data annuncio: 30/4/2021, Data applicazione: 31/7/2021)
   * `org.apache.felix.http.timeout`
      * Tipo: numero intero
   * `org.apache.felix.http.session.timeout`
      * Tipo: numero intero
   * `org.apache.felix.http.jetty.threadpool.max`
      * Tipo: numero intero
   * `org.apache.felix.http.jetty.headerBufferSize`
      * Tipo: numero intero
   * `org.apache.felix.http.jetty.requestBufferSize`
      * Tipo: numero intero
   * `org.apache.felix.http.jetty.responseBufferSize`
      * Tipo: numero intero
   * `org.apache.felix.http.jetty.maxFormSize`
      * Tipo: numero intero
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * Tipo: booleano
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Tipo: stringa
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Tipo: stringa
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Tipo: stringa
   * `org.eclipse.jetty.servlet.SessionPath`
      * Tipo: stringa
   * `org.eclipse.jetty.servlet.MaxAge`
      * Tipo: numero intero
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * Tipo: numero intero
   * `org.apache.felix.jetty.gziphandler.enable`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * Tipo: numero intero
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * Tipo: numero intero
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * Tipo: numero intero
   * `org.apache.felix.jetty.gzip.syncFlush`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Tipo: stringa
   * `org.apache.felix.jetty.gzip.includedMethods`
      * Tipo: array di stringhe
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * Tipo: array di stringhe
   * `org.apache.felix.jetty.gzip.includedPaths`
      * Tipo: array di stringhe
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * Tipo: array di stringhe
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * Tipo: array di stringhe
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * Tipo: array di stringhe
   * `org.apache.felix.http.session.invalidate`
      * Tipo: booleano
   * `org.apache.felix.http.session.container.attribute`
      * Tipo: array di stringhe
   * `org.apache.felix.http.session.uniqueid`
      * Tipo: booleano
* **`org.apache.sling.scripting.cache`** (Data annuncio: 30/4/2021, Data applicazione: 31/7/2021)
   * `org.apache.sling.scripting.cache.size`
      * Tipo: numero intero
      * Intervallo richiesto: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Obbligatorio
      * Tipo: array di stringhe
      * Intervallo richiesto: deve includere js
* **`com.day.cq.mailer.DefaultMailService`** (Data annuncio:30/4/2021, Data applicazione: 31/7/2021)
   * `smtp.host`
      * Tipo: stringa
   * `smtp.port`
      * Tipo: numero intero
      * Intervallo richiesto: 465, 587 o 25
   * `smtp.user`
      * Tipo: stringa
   * `smtp.password`
      * Tipo: stringa
   * `from.address`
      * Tipo: stringa
   * `smtp.ssl`
      * Tipo: stringa
   * `smtp.starttls`
      * Tipo: booleano
   * `smtp.requiretls`
      * Tipo: booleano
   * `debug.email`
      * Tipo: booleano
   * `oauth.flow`
      * Tipo: booleano
* **`org.apache.sling.commons.log.LogManager.factory.config`** (Data annuncio: 16/11/21, Data applicazione: 16/2/21)
   * `org.apache.sling.commons.log.level`
      * Tipo: enumerazione
      * Intervallo richiesto: INFO, DEBUG o TRACE
   * `org.apache.sling.commons.log.names`
      * Tipo: stringa
   * `org.apache.sling.commons.log.file`
      * Tipo: stringa
   * `org.apache.sling.commons.log.additiv`
      * Tipo: booleano
+++

