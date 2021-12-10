---
title: Integrare DocuSign con un modulo adattivo
description: Scopri come utilizzare DocuSign con un modulo adattivo per raccogliere le firme elettroniche.
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 0%

---

# Utilizzo di DocuSign con un modulo adattivo {#integrate-aem-forms-with-DocuSign}

DocuSign è una soluzione di firma elettronica di rilievo. Puoi utilizzarlo per firmare un accordo via e-mail. È possibile integrare DocuSign con un modulo adattivo. Consente di inviare un modulo adattivo per le firme elettroniche a più destinatari. L’utilizzo delle firme elettroniche consente di:

- Chiudi le offerte da qualsiasi dispositivo con processi di proposta, preventivo e contratto completamente automatizzati.
- Completa più velocemente i processi delle risorse umane e dai ai tuoi dipendenti le esperienze digitali.
- Taglia i tempi del ciclo di contratto e accedi più rapidamente ai tuoi fornitori.

AEM Forms as a Cloud Service fornisce un [azione di invio personalizzata per DocuSign](#deploy-custom-submit-action). L’azione di invio consente di inviare i moduli adattivi per le firme elettroniche utilizzando le API di DocuSign.

| È inoltre possibile utilizzare la soluzione di firma elettronica di Adobe, Adobe Sign, per apporre la firma elettronica a un modulo adattivo. AEM Forms offre un’integrazione molto più profonda con Adobe Sign e offre controlli molto più precisi come la firma sequenziale e parallela, metodi di autenticazione multipli, esperienza di firma in-form e altro ancora. Per ulteriori informazioni, consulta [Utilizzo di Adobe Sign in un modulo adattivo](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Prerequisiti {#prerequisites}

Per integrare DocuSign con AEM Forms sono necessari i seguenti requisiti:

- Un segno docu [account sviluppatore](https://developers.docusign.com/platform/account/)
- Un&#39;applicazione DocuSign
- Credenziali (ID client e segreto client) dell’applicazione API DocuSign.
- [Azione di invio personalizzata e servizio Cloud per DocuSign](https://github.com/adobe/aem-forms-docusign-sample)
- (Solo per ambiente di sviluppo locale) [Imposta documento di registrazione](setup-local-development-environment.md#docker-microservices).

## Configurare l’azione di invio personalizzata e il servizio Cloud per DocuSign {#deploy-custom-submit-action}

AEM Forms as a Cloud Service fornisce un’azione di invio personalizzata per DocuSign. L’azione di invio consente di inviare i moduli adattivi per le firme elettroniche utilizzando le API di DocuSign. Il codice per l’azione di invio personalizzata è disponibile in [AEM Forms esegue l’esempio di archivio Git pubblico](https://github.com/adobe/aem-forms-docusign-sample). Puoi distribuire il codice così come si trova nell’ambiente AEM Forms o personalizzarlo in base ai requisiti della tua organizzazione.

Esegui i seguenti passaggi per configurare l’azione di invio personalizzata predefinita e il Cloud Service DocuSign:

1. [Clona il progetto as a Cloud Service di AEM Forms](setup-local-development-environment.md#forms-cloud-service-local-development-environment) o creare un [!DNL Experience Manager Forms] come [!DNL Cloud Service] basato su [Archetipo AEM 27](https://github.com/adobe/aem-project-archetype) o successiva. Per creare un [!DNL Experience Manager Forms] come [!DNL Cloud Service] progetto basato su Archetype AEM:
   </br> Apri il prompt dei comandi ed esegui il comando sottostante per creare un [!DNL Experience Manager Forms] Progetto as a Cloud Service:

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Inoltre, cambia `appTitle`, `appId`e `groupId`, nel comando precedente per riflettere l&#39;ambiente.

1. Clona il [aem-forms-amples](https://github.com/adobe/aem-forms-docusign-sample) archivio. Questo archivio contiene un&#39;azione di invio personalizzata per DocuSign e i dettagli di configurazione per connettersi al server DocuSign.

1. Apri il progetto as a Cloud Service di AEM Forms creato al passaggio 1 per la modifica nell’IDE che preferisci.

1. Apri `[AEM Forms as a Cloud Service project]\pom.xml` per la modifica e apportare le seguenti modifiche:

   1. Aggiungi il seguente testo alla fine del `<properties>` tag:

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. Aggiungi il seguente testo alla fine del `<repositories>` tag:

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      Se non esiste `<repositories>` crea il tag sotto il tag `<properties>` tag .

   1. Aggiungi il seguente testo alla fine del `<dependencyManagement>` tag:

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Esegui i seguenti passaggi nella `all/pom.xml` file disponibile nella cartella di progetto del Cloud Service:

   1. Aggiungi il seguente testo alla fine del `<embeddeds>` tag:

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. Aggiungi il seguente testo alla fine del `<dependencies>` tag:

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. Apri il prompt dei comandi e passa a `aem-forms-samples\forms-integration-docusign` (clonato al punto 3) ed esegui il seguente comando:

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` fa riferimento al nome della cartella creata nel passaggio 1 di questa procedura.

1. Distribuisci il progetto nell’ambiente di sviluppo locale. È possibile utilizzare il comando seguente per distribuire nell&#39;ambiente di sviluppo locale

   `mvn -PautoInstallPackage clean install`

   Dopo aver eseguito questi passaggi, è possibile visualizzare una nuova azione di invio personalizzata [Invia con firme elettroniche DocuSign](#enabledocusign) disponibili nell’elenco delle opzioni di invio per un modulo adattivo e un [Configurazione del servizio cloud DocuSign](#configure-docusign-with-aem-forms) nell’ambiente di sviluppo locale.

1. Compila e [Distribuisci il codice nel tuo [!DNL AEM Forms] Ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Integrare [!DNL DocuSign] con [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

Dopo aver impostato i prerequisiti, esegui i seguenti passaggi per l’integrazione [!DNL DocuSign] con [!DNL AEM Forms] nelle istanze Autore .

1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL DocuSign]** e seleziona una cartella in cui ospitare la configurazione.

1. Nella pagina delle configurazioni, tocca **[!UICONTROL Crea]** per creare [!DNL DocuSign] configurazione in AEM Forms.
1. In **[!UICONTROL Generale]** della scheda **[!UICONTROL Crea configurazione DocuSign]** pagina, specifica un **[!UICONTROL Nome]** per la configurazione e tocca **[!UICONTROL Successivo]**. Facoltativamente, puoi specificare un **[!UICONTROL Titolo]**.

1. Copia l&#39;URL nella finestra del browser corrente su un blocco note. L’URL deve essere configurato [!DNL DocuSign] applicazione con [!DNL AEM Forms] in un passaggio successivo.

1. Configura le impostazioni OAuth per la [!DNL DocuSign] domanda:

   1. Apri una finestra del browser e accedi al tuo [!DNL DocuSign] [account sviluppatore](https://admindemo.docusign.com/apps-and-keys).
   1. Apri l’app configurata per [!DNL AEM Forms].
   1. In **[!UICONTROL URI di reindirizzamento]** aggiungi l’URL copiato nel passaggio precedente e fai clic su **[!UICONTROL Salva]**.
   1. Annotare le chiavi di integrazione e segrete.

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un [!DNL DocuSign] applicazione e ottenere le chiavi, vedi [Configurare le impostazioni di oAuth per l&#39;applicazione](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys) documentazione per gli sviluppatori.

1. Torna alla pagina **[!UICONTROL Crea configurazione DocuSign]** pagina. In **[!UICONTROL Impostazioni]** scheda **[!UICONTROL URL OAuth]** Il campo cita il seguente URL predefinito:

   `https://account-d.docusign.com/oauth/auth`

1. Specifica la **[!UICONTROL ID client]** (Chiave di integrazione DocuSign) e **[!UICONTROL Segreto client]** (Chiave segreta DocuSign).

1. Tocca **[!UICONTROL Connetti a DocuSign]**. Quando viene richiesto di specificare le credenziali, specificare il nome utente e la password dell’account utilizzato durante la creazione [!DNL DocuSign] applicazione. Quando viene richiesto di confermare l’accesso per `your developer account`, fai clic su **[!UICONTROL Consenti accesso]**. Se le credenziali sono corrette, viene visualizzato un messaggio di successo.

1. Tocca **[!UICONTROL Crea]** per creare [!DNL DocuSign] configurazione.

1. Seleziona la configurazione e fai clic su **[!UICONTROL Pubblica]**, seleziona la configurazione e fai clic su **[!UICONTROL Pubblica]**. Replica la configurazione negli ambienti di pubblicazione corrispondenti.

1. Ripeti tutti i passaggi precedenti sulle istanze di sviluppo, stage e produzione (a seconda di quale dei due passaggi successivi) per completare la configurazione [!DNL DocuSign] con [!DNL AEM Forms] per il tuo ambiente.

Ora, il tuo ambiente AEM Forms è configurato per utilizzare DocuSign. Aggiungi il contenitore di configurazione utilizzato per il Cloud Service a tutti i Forms adattivi per i quali [!DNL DocuSign]. È possibile specificare un contenitore di configurazione dalle proprietà di un modulo adattivo.

### Utilizzo [!DNL DocuSign] in un modulo adattivo {#enabledocusign}

È possibile attivare [!DNL DocuSign] per un modulo adattivo esistente o per creare un [!DNL DocuSign] modulo adattivo abilitato. Scegliere una delle seguenti opzioni:

- [Crea un [!DNL DocuSign] modulo adattivo abilitato](#create-an-adaptive-form-for-docusign)
- [Abilita [!DNL DocuSign] per un modulo adattivo esistente](#editafsign).

#### Creare un modulo adattivo per DocuSign {#create-an-adaptive-form-for-docusign}

Per creare un modulo adattivo abilitato alla firma:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**. Viene visualizzato un elenco di modelli. Seleziona un modello e tocca **[!UICONTROL Successivo]**.
1. In **[!UICONTROL Base]** scheda:

   1. Specifica la **[!UICONTROL Nome]** e **[!UICONTROL Titolo]** per il modulo adattivo.

   1. Seleziona la [contenitore di configurazione](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato mentre [integrazione [!DNL DocuSign] con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).
   Il contenitore di configurazione contiene [!DNL DocuSign] Cloud Services configurati per il tuo ambiente. Questi servizi sono disponibili per la selezione nell’editor di moduli adattivi.

1. In **[!UICONTROL Modello Modulo]** seleziona una delle opzioni seguenti:

   - Se si dispone di un modello di modulo personalizzato e si richiede un documento di record basato sul modello di modulo, selezionare la **[!UICONTROL Associa modello di modulo come modello del documento di record]** e selezionare un modello Documento di record. Quando si utilizza l’opzione , i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non vengono visualizzati tutti i campi del modulo adattivo.

   - Se non si dispone di un modello di modulo personalizzato, selezionare la **[!UICONTROL Genera documento di registrazione]** opzione . Quando si utilizza l’opzione , nel documento inviato per la firma vengono visualizzati tutti i campi del modulo adattivo.

1. Tocca **[!UICONTROL Crea.]** Viene creato un modulo adattivo abilitato per la firma. Puoi aggiungere il tuo [!DNL DocuSign] campi al modulo e inviarlo per la firma.
1. Apri il modulo adattivo in modalità di modifica. In **[!UICONTROL Contenuto]** tocca **[!UICONTROL Contenitore modulo]** e toccare ![Configura](assets/configure-icon.svg).

1. In **[!UICONTROL Invio]** sezione , seleziona **[!UICONTROL Invia con firme elettroniche DocuSign]** dal **[!UICONTROL Invia azione]** elenco a discesa.

1. In **[!UICONTROL Configurazione azione]** sezione, toccare **[!UICONTROL Aggiungi]** per aggiungere un destinatario e specificare l’indirizzo e-mail del destinatario. Tocca **[!UICONTROL Aggiungi]** per aggiungere altri destinatari.

1. Specifica l’oggetto del messaggio e-mail nella **[!UICONTROL Oggetto e-mail]** campo . Seleziona **Includi allegati** per includere allegati nel messaggio e-mail.

1. Tocca ![Salva](assets/save_icon.svg) per salvare le proprietà.

#### Abilita [!DNL DocuSign] per un modulo adattivo {#editafsign}

Per utilizzare [!DNL DocuSign] in un modulo adattivo esistente:

1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo e tocca **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Base]** seleziona la scheda [contenitore di configurazione](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante l&#39;integrazione [!DNL DocuSign] con [!DNL AEM Forms].
1. In **[!UICONTROL Modello Modulo]** seleziona una delle opzioni seguenti:

   - Se si dispone di un modello di modulo personalizzato e si richiede un documento di record basato sul modello di modulo, selezionare la **[!UICONTROL Associa modello di modulo come modello del documento di record]** e selezionare un modello Documento di record. Quando si utilizza l’opzione , i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non vengono visualizzati tutti i campi del modulo adattivo.

   - Se non si dispone di un modello di modulo personalizzato, selezionare la **[!UICONTROL Genera documento di registrazione]** opzione . Quando si utilizza l’opzione , nel documento inviato per la firma vengono visualizzati tutti i campi del modulo adattivo.

1. Tocca **[!UICONTROL Salva e chiudi]**. Il modulo adattivo è abilitato per [!DNL DocuSign]. Ora puoi aggiungere il tuo [!DNL DocuSign] campi al modulo e inviarlo per la firma.

1. Apri il modulo adattivo in modalità di modifica. In **[!UICONTROL Contenuto]** tocca **[!UICONTROL Contenitore modulo]** e toccare ![Configura](assets/configure-icon.svg).

1. In **[!UICONTROL Invio]** sezione , seleziona **[!UICONTROL Invia con firme elettroniche DocuSign]** dal **[!UICONTROL Invia azione]** elenco a discesa.

1. In **[!UICONTROL Configurazione azione]** sezione, toccare **[!UICONTROL Aggiungi]** per aggiungere un destinatario e specificare l’indirizzo e-mail del destinatario. Tocca **[!UICONTROL Aggiungi]** per aggiungere altri destinatari.

1. Specifica l’oggetto del messaggio e-mail nella **[!UICONTROL Oggetto e-mail]** campo . Seleziona **Includi allegati** per includere allegati nel messaggio e-mail.

1. Tocca ![Salva](assets/save_icon.svg) per salvare le proprietà.
