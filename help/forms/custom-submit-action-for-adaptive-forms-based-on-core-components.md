---
title: Come si crea un’azione di invio personalizzata per un modulo adattivo basato sui componenti core?
description: Scopri come creare un’azione di invio personalizzata per consentire a un Forms adattivo di elaborare i dati prima di inviarli utilizzando l’azione di invio personalizzata.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Intermediate
exl-id: a369b585-d148-4b5a-8afe-d5673ea865d0
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 1%

---

# Creare un’azione di invio personalizzata per Adaptive Forms (Componenti core)

Un’azione di invio consente agli utenti di selezionare la destinazione dei dati acquisiti da un modulo e di definire funzionalità aggiuntive da eseguire all’invio del modulo. Il modulo AEM supporta più azioni di [invio pronte all&#39;uso (OOTB)](/help/forms/configure-submit-actions-core-components.md), ad esempio l&#39;invio di un&#39;e-mail o il salvataggio di dati in SharePoint o OneDrive.

Puoi anche creare un&#39;azione di invio personalizzata per aggiungere funzionalità non incluse nelle [opzioni predefinite](/help/forms/configure-submit-actions-core-components.md#select-and-configure-a-submit-action-for-an-adaptive-form-select-and-configure-submit-action). Ad esempio, integra i dati del modulo con un’applicazione di terze parti o attiva una notifica SMS personalizzata in base all’input dell’utente.

<!-- ![Custom Submit Image](/help/forms/assets/custom-submit-action-hero-image.png)
-->

## Prerequisiti

Prima di iniziare la creazione della prima azione di invio personalizzata per Adaptive Forms, assicurati di disporre dei seguenti elementi:

* **Editor di testo normale (IDE)**: mentre qualsiasi editor di testo normale può funzionare, un ambiente di sviluppo integrato (IDE) come Microsoft Visual Studio Code offre funzionalità avanzate per semplificare la modifica.

* **Git**: questo sistema di controllo della versione è necessario per la gestione delle modifiche al codice. Se non lo hai installato, scaricalo da https://git-scm.com.

## Creare la prima azione di invio personalizzata per il modulo

Il diagramma seguente illustra i passaggi necessari per creare un’azione di invio personalizzata per un modulo adattivo:

![Flusso di lavoro per azione di invio personalizzata](/help/forms/assets/custom-submit-action-workflow.png){width=50%, height-50%}

### Clona l’archivio Git di AEM as a Cloud Service.

1. Aprire la riga di comando e scegliere una directory in cui archiviare l&#39;archivio AEM as a Cloud Service, ad esempio `/cloud-service-repository/`.

1. Esegui il comando seguente per clonare l’archivio:

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **Dove trovare queste informazioni?**

   Per istruzioni dettagliate su come individuare questi dettagli, consulta l&#39;articolo di Adobe Experience League &quot;[Accesso a Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=it#accessing-git)&quot;.

   **Il progetto è pronto!**

   Al termine del comando viene visualizzata una nuova cartella creata nella directory locale. Questa cartella prende il nome dall’applicazione (ad esempio, app-id). Questa cartella contiene tutti i file e il codice scaricati dall’archivio Git di AEM as a Cloud Service. Puoi trovare `<appid>` per il tuo progetto AEM nel file `archetype.properties`.

   ![Proprietà Archetipo](/help/forms/assets/custom-submit-action-archetype-app-id.png)

   In questa guida questa cartella viene indicata come `[AEMaaCS project directory]`.

## Aggiungi nuova azione di invio

1. Apri la cartella dell’archivio in un editor.

   ![Archivio clonato](/help/forms/assets/custom-submit-action-clone-repo.png)

1. Passare alla seguente directory all&#39;interno di `[AEMaaCS project directory]`:

   ```
   /ui.apps/src/main/content/jcr_root/apps/<app-id>/
   ```

   **Importante**: sostituisci `<app-id>` con il tuo ID applicazione effettivo.

1. Crea una nuova cartella per l’azione di invio personalizzata e assegnagli un nome a tua scelta. Ad esempio, assegnare alla cartella il nome `customsubmitaction`.

   ![Crea cartella azioni di invio personalizzate](/help/forms/assets/custom-submit-action-create-folder.png)

1. Passa alla directory dell’azione di invio personalizzata aggiunta.

   All&#39;interno di `[AEMaaCS project directory]`, passa al seguente percorso:

   `/ui.apps/src/main/content/jcr_root/apps/<app-id>/customsubmitaction/`

   `Important`: sostituisci `<app-id>` con l&#39;ID applicazione effettivo.

1. Crea un nuovo file di configurazione.
Nella cartella `customsubmitaction`, creare un nuovo file denominato `.content.xml`.

   ![Crea file di configurazione](/help/forms/assets/custom-submit-action-create-config-folder.png)

1. Apri il file e incolla il seguente contenuto, sostituendo `[customsubmitaction]` con il nome dell&#39;azione di invio

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
   jcr:description="[customsubmitaction]"
   jcr:primaryType="sling:Folder"
   
   guideComponentType="fd/af/components/guidesubmittype"
   guideDataModel="basic,xfa,xsd"
   submitService="[customsubmitaction]"/>
   ```

   Ad esempio, sostituisci `[customsubmitaction]` con il nome dell&#39;azione di invio personalizzato `Custom Submit Action`.

   ![Crea file di configurazione azione di invio personalizzato](/help/forms/assets/custom-submit-action-config-file.png)

   >[!NOTE]
   >
   > Ricordare il nome di [customsubmitaction], poiché lo stesso nome viene visualizzato nell&#39;elenco a discesa `Submit action` durante la creazione di un modulo.


**Includi la nuova cartella in`filter.xml`**

1. Passa al file `/ui.apps/src/main/content/META-INF/vault/filter.xml` nella directory del progetto [AEMaaCS].

1. Apri il file e aggiungi la seguente riga alla fine:

   ```
   <filter root="/apps/<app-id>/[customsubmitaction-folder]"/>
   ```

   Aggiungere ad esempio la seguente riga di codice per aggiungere la cartella `customsubmitaction` nel file `filter.xml`:

   ```
   <filter root="/apps/wknd/customsubmitaction"/>
   ```

   ![Aggiungi le cartelle create nel file filter.xml](/help/forms/assets/custom-submit-action-filter-xml.png)

1. Salvare le modifiche.

### Implementa il servizio per l’azione di invio aggiunta.

1. Passare alla seguente directory all&#39;interno di `[AEMaaCS project directory]`:
   `/core/src/main/java/com/<app-id>/core/service/`
   `Important`: sostituisci `<app-id>` con l&#39;ID applicazione effettivo.
1. Crea un nuovo file Java per implementare il servizio per l’azione di invio aggiunta. Ad esempio, aggiungere un nuovo file Java come `CustomSubmitService.java`.

   ![Cartella azioni di invio personalizzate](/help/forms/assets/custom-submit-action-custom-submit-folder.png)

1. Apri questo file e aggiungi il codice per l’implementazione dell’azione di invio personalizzata.

   Il codice Java seguente, ad esempio, è un servizio OSGi che gestisce l&#39;invio del modulo registrando i dati inviati e restituendo uno stato `OK`. Aggiungi il seguente codice nel file `CustomSubmitService.java`:

   ```
   package com.wknd.core.service;
   
   import com.adobe.aemds.guide.model.FormSubmitInfo;
   import com.adobe.aemds.guide.service.FormSubmitActionService;
   import java.util.HashMap;
   import java.util.Map;
   import org.osgi.service.component.annotations.Component;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
       @Component(
       service = FormSubmitActionService.class,
       immediate = true
           )
       public class CustomSubmitService implements FormSubmitActionService {
   
       private static final String serviceName = "Custom Submit Action";
   
       private static Logger log = LoggerFactory.getLogger(CustomSubmitService.class);
   
       @Override
       public String getServiceName() {
       return serviceName;
       }
   
       @Override
       public Map<String, Object> submit(FormSubmitInfo formSubmitInfo) {
       String data = formSubmitInfo.getData();
       log.info("Using custom submit action service, [data] --> " + data);
       Map<String, Object> result = new HashMap<>();
       result.put("status", "OK");
       return result;
        }
       }
   ```

   ![Servizio azione invio personalizzato](/help/forms/assets/custom-submit-action-service.png)

1. Salvare le modifiche.

### Distribuisci il codice.

**Distribuisci il codice per l&#39;ambiente di sviluppo locale**

* Distribuire AEM as a Cloud Service `[AEMaaCS project directory]` nell&#39;ambiente di sviluppo locale per provare la nuova azione di invio nel computer locale. Per implementare nell’ambiente di sviluppo locale:

   1. Assicurati che l’ambiente di sviluppo locale sia operativo. Se non hai già configurato un ambiente di sviluppo locale, consulta la guida su [Configurare un ambiente di sviluppo locale per AEM Forms](/help/forms/setup-local-development-environment.md).

   1. Aprire la finestra del terminale o il prompt dei comandi.

   1. Passare a `[AEMaaCS project directory]`.

   1. Esegui il comando seguente:

      ```
      mvn -PautoInstallPackage clean install
      ```

      ![Distribuzione locale](/help/forms/assets/custom-submit-action-local-deployment.png)

**Distribuire il codice per l&#39;ambiente Cloud Service**

* Distribuire AEM as a Cloud Service, `[AEMaaCS project directory]`, nell&#39;ambiente Cloud Service. Per eseguire l’implementazione nell’ambiente Cloud Service:

   1. Eseguire il commit delle modifiche:

      Dopo aver aggiunto la nuova configurazione dell’azione di invio personalizzata, conferma le modifiche con un messaggio Git cancellato. (ad esempio, &quot;Aggiunta nuova azione di invio personalizzata&quot;).

   1. Distribuisci il codice aggiornato:

      Attiva una distribuzione del codice tramite la [pipeline full stack esistente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=it#setup-pipeline). Genera e distribuisce automaticamente il codice aggiornato con il nuovo supporto per l’azione di invio personalizzata.

      Se non hai già configurato una pipeline, consulta la guida su [come impostare una pipeline per AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=it#setup-pipeline).

      ![Distribuzione cloud](/help/forms/assets/custom-submit-action-cloud-deployment.png)

      **Come confermare l&#39;installazione?**

      Una volta creato correttamente il progetto, l&#39;azione di invio personalizzata viene visualizzata nell&#39;elenco a discesa `Submit action` durante la creazione di un modulo.

      ![Elenco a discesa Azione di invio personalizzata](/help/forms/assets/custom-submit-action-drop-down-list.png)

  Il tuo ambiente è ora pronto per utilizzare l’azione di invio personalizzata aggiunta durante la creazione di un modulo.

### Anteprima di un modulo adattivo con nuova azione di invio aggiunta

1. Accedi all’istanza di AEM Forms as a Cloud Service.
1. Vai a **Forms** > **Forms e documenti**.

   ![Forms e documenti](/help/forms/assets/custom-submit-action-fnd.png)

1. Seleziona un modulo adattivo e fai clic su **Modifica**. Il modulo si apre in modalità di modifica.

   ![Modifica modulo](/help/forms/assets/custom-submit-action-edit-af.png)

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fare clic sulla scheda **[!UICONTROL Invio]**.
1. Dall&#39;elenco a discesa **[!UICONTROL Azione invio]**, selezionare l&#39;azione di invio. Selezionare ad esempio l&#39;azione di invio come `Custom Submit Action`.

   ![Modulo di invio personalizzato](/help/forms/assets/custom-submit-action-select-submit-action.png)

1. Compila il modulo e invialo.

   ![Invia modulo](/help/forms/assets/custom-submit-action-submit-form.png)

   ![Messaggio di ringraziamento](/help/forms/assets/custom-submit-action-thankyou-msg.png)

   Dopo aver inviato il modulo, è possibile controllare la **configurazione della console Web Adobe Experience Manager** per verificare l&#39;azione dell&#39;azione di invio personalizzata nell&#39;ambiente di sviluppo locale.
1. Passa a `http://<host>:<port>/system/console/configMgr`.

1. Passare a **Supporto log console Web Adobe Experience Manager** in `http://<host>:<port>/system/console/slinglog`.

   ![ConfigMgr](/help/forms/assets/custom-submit-action-sling-log.png)

1. Fare clic sull&#39;opzione `logs/error.log`.
   ![Apri il file error.log](/help/forms/assets/custom-submit-action-error-log.png)

1. Aprire il file `error.log` per verificare che i dati siano stati aggiunti alla fine.

   ![file error.log](/help/forms/assets/custom-submit-action-form-data-display.png)

   >[!NOTE]
   >
   > * Per visualizzare i registri di errore nell’ambiente AEM as a Cloud Service, puoi utilizzare Splunk.
   > * Se un servizio azione di invio personalizzato rileva un errore non gestito, AEM as a Cloud Service restituisce un HTML della pagina di errore 502.


## Domande frequenti

**D: perché il modulo adattivo mostra una pagina di errore 5.x.x dopo l’invio?**
Errore non gestito del servizio azione di invio personalizzata. AEM Cloud Service restituisce quindi la pagina di errore predefinita.

<!--
## Best practices

 * It is recommended to use the OSGi service approach for creating a custom submit action, as it is faster than the AEM servlet approach. 

## Next steps
-->

## Articoli correlati

{{af-submit-action}}

<!-- The [Adaptive Forms Core Components](https://github.com/adobe/aem-core-forms-components) repository includes a sample folder, `customsubmission/logsubmit`, to simplify the process of adding new custom submit actions. It also provides the Java service implementation for the `logsubmit` custom submit action, named `CustomAFSubmitService`.java. These resources are available on GitHub. -->
