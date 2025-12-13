---
title: Come si precompilano i campi del modulo adattivo?
description: 'Utilizzare i dati esistenti per precompilare i campi di un modulo adattivo: gli utenti possono precompilare le informazioni di base in un modulo accedendo con i propri profili social.'
topic-tags: develop
feature: Adaptive Forms, Foundation Components
exl-id: e2a87233-a0d5-48f0-b883-915fe56f105f
role: User, Developer
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2044'
ht-degree: 1%

---

# Precompilare i campi di un modulo adattivo{#prefill-adaptive-form-fields}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base.

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/prepopulate-adaptive-form-fields.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

## Introduzione {#introduction}

È possibile precompilare i campi di un modulo adattivo utilizzando dati esistenti. Quando un utente apre un modulo, i valori di tali campi vengono precompilati. Per precompilare i dati in un modulo adattivo, rendi i dati utente disponibili come XML/JSON precompilato nel formato conforme alla struttura dei dati precompilata di Adaptive Forms.

## Applicabilità e casi d’uso

### Assicurazione

## AEM Forms può precompilare i dati delle applicazioni assicurative?

Sì. AEM Forms supporta la precompilazione dei campi modulo utilizzando origini dati back-end, consentendo agli assicuratori di riutilizzare i dati esistenti relativi a clienti o policy e di ridurre l’immissione manuale.

## Struttura dei dati preriempimento {#the-prefill-structure}

Un modulo adattivo può contenere una combinazione di campi associati e non associati. I campi associati sono campi trascinati dalla scheda Content Finder e che contengono il valore della proprietà `bindRef` non vuoto nella finestra di dialogo di modifica del campo. I campi non associati vengono trascinati direttamente dal browser componenti di Sidekick e hanno un valore `bindRef` vuoto.

È possibile precompilare sia i campi associati che quelli non associati di un modulo adattivo. I dati di precompilazione contengono le sezioni afBoundData e afUnBoundData per precompilare sia i campi associati che quelli non associati di un modulo adattivo. La sezione `afBoundData` contiene i dati di precompilazione per i campi e i pannelli associati. Questi dati devono essere conformi allo schema del modello di modulo associato:

- Per Forms adattivo che utilizza il [modello di modulo XFA](#xfa-based-af), utilizza il file XML di precompilazione conforme allo schema di dati del modello XFA.
- Per Forms adattivo che utilizza [lo schema XML](#xml-schema-af), utilizza il precompilatore XML conforme alla struttura dello schema XML.
- Per Forms adattivo che utilizza lo schema [JSON](#json-schema-based-adaptive-forms), utilizza il codice JSON di precompilazione conforme allo schema JSON.
- Per il Forms adattivo che utilizza lo schema FDM, utilizza il JSON di precompilazione conforme allo schema FDM.
- Per Forms adattivo con [nessun modello di modulo](#adaptive-form-with-no-form-model), non sono presenti dati associati. Ogni campo è un campo non associato e viene precompilato utilizzando l&#39;XML non associato.

### Esempio di struttura XML di preriempimento {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         .
         .
    </data>
  </afUnboundData>
</afData>
```

### Esempio di struttura JSON di preriempimento {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

Per i campi associati con lo stesso bindref o campi non associati con lo stesso nome, i dati specificati nel tag XML o nell’oggetto JSON vengono compilati in tutti i campi. Ad esempio, due campi in un modulo sono mappati al nome `textbox` nei dati di precompilazione. Durante il runtime, se il primo campo della casella di testo contiene &quot;A&quot;, nella seconda casella di testo viene automaticamente inserito &quot;A&quot;. Questo collegamento è denominato collegamento in tempo reale dei campi del modulo adattivo.

### Modulo adattivo con modello di modulo XFA {#xfa-based-af}

La struttura dell’XML di precompilazione e dell’XML inviato per Adaptive Forms basato su XFA è la seguente:

- **Struttura XML precompilata**: l&#39;XML precompilato per il modulo adattivo basato su XFA deve essere conforme allo schema dati del modello di modulo XFA. Per precompilare i campi non associati, racchiudere la struttura XML di precompilazione nel tag `/afData/afBoundData`.

- **Struttura XML inviato**: se non viene utilizzato alcun XML di precompilazione, l&#39;XML inviato contiene dati per i campi associati e non associati nel tag wrapper `afData`. Se si utilizza un XML di precompilazione, il codice XML inviato ha la stessa struttura del codice XML di precompilazione. Se l&#39;XML di precompilazione inizia con il tag radice `afData`, anche l&#39;XML di output ha lo stesso formato. Se il file XML di precompilazione non ha il wrapper `afData/afBoundData` e inizia direttamente dal tag radice dello schema come `employeeData`, anche il file XML inviato inizia con il tag `employeeData`.

Prefill-Submit-Data-ContentPackage.zip

[Ottieni file](assets/prefill-submit-data-contentpackage.zip)
Campione contenente i dati di precompilazione e i dati inviati

### FORMS adattivo basato su schema XML  {#xml-schema-af}

La struttura dell&#39;XML di precompilazione e dell&#39;XML inviato per Forms adattivo basato su schema XML è la seguente:

- **Struttura XML precompilato**: l&#39;XML precompilato deve essere conforme allo schema XML associato. Per precompilare i campi non associati, racchiudi la struttura XML di precompilazione nel tag /afData/afBoundData.
- **Struttura XML inviato**: se non viene utilizzato alcun XML di precompilazione, il codice XML inviato contiene dati per i campi associati e non associati nel tag wrapper `afData`. Se si utilizza il codice XML di precompilazione, il codice XML inviato ha la stessa struttura del codice XML di precompilazione. Se l&#39;XML di precompilazione inizia con il tag radice `afData`, l&#39;XML di output ha lo stesso formato. Se il file XML di precompilazione non ha il wrapper `afData/afBoundData` e inizia direttamente dal tag radice dello schema come `employeeData`, anche il file XML inviato inizia con il tag `employeeData`.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">

    <xs:element name="sample" type="SampleType"/>

    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

Per i campi il cui modello è lo schema XML, i dati vengono precompilati nel tag `afBoundData` come mostrato nel codice XML di esempio seguente. Può essere utilizzato per precompilare un modulo adattivo con uno o più campi di testo non associati.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>Si consiglia di non utilizzare campi non associati nei pannelli associati (pannelli con `bindRef` non vuoto creati trascinando i componenti dalla scheda Sidekick o Origini dati). Potrebbe causare la perdita di dati di questi campi non associati. Inoltre, si consiglia di assegnare nomi univoci ai campi nel modulo, in particolare per i campi non associati.

#### Esempio senza afData e wrapper afBoundData {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Forms adattivo basato su schema JSON {#json-schema-based-adaptive-forms}

Per il Forms adattivo basato sullo schema JSON, di seguito è descritta la struttura del JSON di precompilazione e del JSON inviato. Per ulteriori informazioni, vedere [Creazione di Forms adattivi utilizzando lo schema JSON](adaptive-form-json-schema-form-model.md).

- **Struttura JSON di precompilazione**: il JSON di precompilazione deve essere conforme allo schema JSON associato. Facoltativamente, può essere racchiuso nell&#39;oggetto /afData/afBoundData se desideri precompilare anche i campi non associati.
- **Struttura JSON inviato**: se non si utilizza un JSON di precompilazione, il JSON inviato contiene dati sia per i campi associati che per quelli non associati nel tag wrapper afData. Se si utilizza il JSON di precompilazione, il JSON inviato ha la stessa struttura del JSON di precompilazione. Se il JSON di precompilazione inizia con l’oggetto principale afData, il JSON di output ha lo stesso formato. Se il JSON di precompilazione non ha il wrapper afData/afBoundData e inizia direttamente dall’oggetto principale dello schema, come utente, anche il JSON inviato inizia con l’oggetto utente.

```json
{
  "id": "https://some.site.somewhere/entry-schema#",
  "$schema": "https://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "address": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string"
        },
        "age": {
          "type": "integer"
        }
      }
    }
  }
}
```

Per i campi che utilizzano il modello di schema JSON, i dati vengono precompilati nell’oggetto afBoundData come mostrato nel JSON di esempio di seguito. Può essere utilizzato per precompilare un modulo adattivo con uno o più campi di testo non associati. Di seguito è riportato un esempio di dati con wrapper `afData/afBoundData`:

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

Di seguito è riportato un esempio senza wrapper `afData/afBoundData`:

```json
{
  "user": {
    "address": {
      "city": "Noida",
      "country": "India"
    }
  }
}
```

>[!NOTE]
>
> L&#39;utilizzo di campi non associati nei pannelli associati (pannelli con bindRef non vuoto creati trascinando componenti dalla scheda Sidekick o Origini dati) è **non** consigliato in quanto potrebbe causare la perdita di dati dei campi non associati. Si consiglia di avere nomi di campo univoci nel modulo, in particolare per i campi non associati.
>

### Modulo adattivo senza modello di modulo {#adaptive-form-with-no-form-model}

Per Forms adattivo senza modello di modulo, i dati per tutti i campi si trovano sotto il tag `<data>` di `<afUnboundData> tag`.

Inoltre, prendi nota di quanto segue:

I tag XML per i dati utente inviati per vari campi vengono generati utilizzando il nome dei campi. Pertanto, i nomi dei campi devono essere univoci.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## Configurazione del servizio di precompilazione {#configuring-prefill-service-using-configuration-manager}

Utilizzare la proprietà `alloweddataFileLocations` della **configurazione predefinita del servizio di precompilazione** per impostare il percorso dei file di dati o un&#39;espressione regolare per i percorsi dei file di dati.

Il seguente file JSON mostra un esempio:

```JSON
  {
  "alloweddataFileLocations": "`file:///C:/Users/public/Document/Prefill/.*`"
  }
```

Per impostare i valori di una configurazione, [Genera configurazioni OSGi utilizzando AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=it#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [distribuisci la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=it#deployment-process) nell&#39;istanza Cloud Service.

>[!NOTE]
>
> - Per impostazione predefinita, la precompilazione è consentita tramite file crx per tutti i tipi di Forms adattivo (XSD, XDP, JSON, FDM e non basati su modello modulo). La precompilazione è consentita solo con file JSON e XML.
> - Il protocollo crx si occupa della sicurezza dei dati precompilati ed è quindi consentito per impostazione predefinita. La precompilazione tramite altri protocolli utilizzando regex generico potrebbe causare vulnerabilità. Nella configurazione, specifica una configurazione URL sicura per proteggere i dati.

## Il curioso caso dei pannelli ripetibili {#the-curious-case-of-repeatable-panels}

In genere, i campi associati (schema modulo) e non associati vengono creati nello stesso modulo adattivo, ma di seguito sono riportate alcune eccezioni nel caso in cui i campi associati siano ripetibili:

- I pannelli ripetibili non associati non sono supportati per l’Adaptive Forms che utilizza il modello di modulo XFA, XSD, lo schema JSON o lo schema FDM.
- Non utilizzare campi non associati nei pannelli ripetibili associati.

>[!NOTE]
>
> Di regola, non combinare campi associati e non associati se sono intersecati nei dati compilati dall’utente nei campi non associati. Se possibile, è necessario modificare lo schema o il modello di modulo XFA e aggiungere una voce per i campi non associati, in modo che anch&#39;esso diventi associato e i relativi dati siano disponibili come altri campi nei dati inviati.

## Protocolli supportati per la precompilazione dei dati utente {#supported-protocols-for-prefilling-user-data}

Il Forms adattivo può essere precompilato con i dati utente in formato dati precompilati tramite i seguenti protocolli se configurato con regex valido:

### Il protocollo crx:// {#the-crx-protocol}

```javascript
http
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

Il nodo specificato deve avere una proprietà denominata `jcr:data` e contenere i dati.

### Il protocollo file://  {#the-file-protocol-nbsp}

```javascript
https://`servername`/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

Il file di riferimento deve trovarsi sullo stesso server.

### Il protocollo https:// {#the-http-protocol}

```javascript
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://servername/somesamplexmlfile.xml
```

### Il protocollo service:// {#the-service-protocol}

```javascript
https://`servername`/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

- SERVICE_NAME fa riferimento al nome del servizio di precompilazione OSGI. Consulta [Creare ed eseguire un servizio di precompilazione](prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
- IDENTIFIER rimanda a tutti i metadati richiesti dal servizio di precompilazione OSGI per recuperare i dati di precompilazione. Un identificatore dell’utente connesso è un esempio di metadati che potrebbe essere utilizzato.

>[!NOTE]
>
> Il passaggio dei parametri di autenticazione non è supportato.

### Impostazione dell’attributo dei dati in slingRequest {#setting-data-attribute-in-slingrequest}

È inoltre possibile impostare l&#39;attributo `data` in `slingRequest`, dove l&#39;attributo `data` è una stringa contenente XML o JSON, come illustrato nel codice di esempio seguente (ad esempio per XML):

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

Puoi scrivere una stringa XML o JSON semplice contenente tutti i tuoi dati e impostarla in slingRequest. Puoi eseguire facilmente questa operazione nel JSP di rendering per qualsiasi componente che desideri includere nella pagina in cui puoi impostare l’attributo dati slingRequest.

Ad esempio, dove desideri una progettazione specifica per la pagina con un tipo specifico di intestazione. A questo scopo, puoi scrivere il tuo `header.jsp`, che puoi includere nel componente Pagina e impostare l&#39;attributo `data`.

Un altro buon esempio è un caso d’uso in cui si desidera precompilare i dati all’accesso tramite account social come Facebook, Twitter o LinkedIn. In questo caso, è possibile includere una JSP semplice in `header.jsp`, che recupera i dati dall&#39;account utente e imposta il parametro di dati.

prefill-page component.zip

[Ottieni file](assets/prefill-page-component.zip)
Esempio di prefill.jsp nel componente pagina

## [!DNL AEM Forms] servizio di precompilazione personalizzato {#aem-forms-custom-prefill-service}

Puoi utilizzare il servizio di preriempimento personalizzato per gli scenari in cui si leggono costantemente i dati da un’origine predefinita. Il servizio di precompilazione legge i dati dalle origini dati definite e precompila i campi del modulo adattivo con il contenuto del file di dati di precompilazione. Consente inoltre di associare in modo permanente i dati precompilati a un modulo adattivo.

### Creare ed eseguire un servizio di precompilazione {#create-and-run-a-prefill-service}

Il servizio di precompilazione è un servizio OSGi ed è fornito tramite bundle OSGi. Puoi creare il bundle OSGi, caricarlo e installarlo in [!DNL AEM Forms] bundle. Prima di iniziare a creare il bundle:

- [Scarica  [!DNL AEM Forms] Client SDK](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html)
- Scarica il pacchetto boilerplate

- Inserisci il file di dati (dati di precompilazione) nel crx-repository. È possibile inserire il file in qualsiasi posizione nella cartella \content del repository crx.

[Ottieni il file](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Creare un servizio di preriempimento {#create-a-prefill-service}

Il pacchetto boilerplate (esempio di pacchetto del servizio di precaricamento) contiene un&#39;implementazione di esempio del servizio di precaricamento [!DNL AEM Forms]. Apri il pacchetto boilerplate in un editor di codice. Ad esempio, apri il progetto boilerplate in Eclipse per la modifica. Dopo aver aperto il pacchetto boilerplate in un editor di codice, esegui i seguenti passaggi per creare il servizio.

1. Apri il file src\main\java\com\adobe\test\Prefill.java per la modifica.
1. Nel codice, imposta il valore di:

   - `nodePath:` La variabile del percorso del nodo che punta alla posizione dell&#39;archivio crx contiene il percorso del file di dati (precaricamento). Ad esempio, /content/prefilldata.xml
   - `label:` Il parametro label specifica il nome visualizzato del servizio. Ad esempio, Servizio di precompilazione predefinito

1. Salvare e chiudere il file `Prefill.java`.
1. Aggiungere il pacchetto `AEM Forms Client SDK` al percorso di compilazione del progetto standard.
1. Compila il progetto e crea il file .jar per il bundle.

#### Avviare e utilizzare il servizio di precompilazione {#start-and-use-the-prefill-service}

Per avviare il servizio di precompilazione, caricare il file JAR nella console Web [!DNL AEM Forms] e attivare il servizio. Ora il servizio inizia a essere visualizzato nell’editor di Forms adattivo. Per associare un servizio di precompilazione a un modulo adattivo:

1. Apri il modulo adattivo nell’editor di Forms e apri il pannello Proprietà per il contenitore modulo.
1. Nella console Proprietà, passa al contenitore [!DNL AEM Forms] > Base > Servizio preriempimento.
1. Selezionare il servizio di precompilazione predefinito e fare clic su **[!UICONTROL Salva]**. Il servizio è associato al modulo.

<!-- ## Prepopulate data at client {#prefill-at-client}

When you prefill an Adaptive Form, the [!DNL AEM Forms] server merges data with an Adaptive Form and delivers the filled form to you. By default, the data merge action takes place at the server.

You can configure the [!DNL AEM Forms] server to perform the data merge action at the client instead of the server. It significantly reduces the time required to prefill and render Adaptive Forms. By default, the feature is disabled. You can enable it from the Configuration Manager or command line.

* To enable or disable from configuration manager:
  1. Open AEM Configuration Manager.
  1. Locate and open the Adaptive Form and Interactive Communication Web Channel Configuration
  1. Enable the Configuration.af.clientside.datamerge.enabled.name option
* To enable or disable from the command line:
  * To enable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

  * To disable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   To take full advantage of the prepopulate data at client option, update your prefill service to return [FileAttachmentMap](https://helpx.adobe.com/it/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) and [CustomContext](https://helpx.adobe.com/it/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) -->