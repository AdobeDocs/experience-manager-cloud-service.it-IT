---
title: Come integrare DocuSign con un modulo adattivo?
description: Scopri come utilizzare DocuSign con un modulo adattivo per raccogliere firme elettroniche.
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 0%

---

# Utilizzo di DocuSign con un modulo adattivo {#integrate-aem-forms-with-DocuSign}

DocuSign è una soluzione di firma elettronica importante. È possibile utilizzarlo per firmare un accordo tramite posta elettronica. È possibile integrare DocuSign con un modulo adattivo. Consente di inviare un modulo adattivo per le firme elettroniche a più destinatari. L’utilizzo delle firme elettroniche consente di:

- Chiudere le offerte da qualsiasi dispositivo con procedure di proposta, preventivo e contratto completamente automatizzate.
- Completa i processi relativi alle risorse umane più rapidamente e offri ai tuoi dipendenti le esperienze digitali.
- Ridurre i tempi di ciclo del contratto e integrare i fornitori più rapidamente.

AEM Forms as a Cloud Service fornisce una [azione di invio personalizzata per DocuSign](#deploy-custom-submit-action). L’azione invia consente di inviare i moduli adattivi per le firme elettroniche utilizzando le API DocuSign.

| Puoi anche utilizzare la soluzione di firma elettronica di Adobe, Adobe Sign, per firmare elettronicamente un modulo adattivo. AEM Forms offre un’integrazione molto più profonda con Adobe Sign e controlli molto più precisi, come la firma sequenziale e parallela, più metodi di autenticazione, esperienza di firma interna ai moduli e altro ancora. Per ulteriori informazioni, consulta [Utilizzo di Adobe Sign in un modulo adattivo](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Prerequisiti {#prerequisites}

Per integrare DocuSign con AEM Forms sono necessari i seguenti elementi:

- A DocuSign [account sviluppatore](https://developers.docusign.com/platform/account/)
- Un&#39;applicazione DocuSign
- Credenziali (ID client e segreto client) dell’applicazione API DocuSign.
- [Azione di invio personalizzata e servizio cloud per DocuSign](https://github.com/adobe/aem-forms-docusign-sample)
- (Solo per l’ambiente di sviluppo locale) [Imposta documento di record](setup-local-development-environment.md#docker-microservices).

## Configurare l’azione di invio personalizzata e Cloud Service per DocuSign {#deploy-custom-submit-action}

AEM Forms as a Cloud Service fornisce un’azione di invio personalizzata per DocuSign. L’azione invia consente di inviare i moduli adattivi per le firme elettroniche utilizzando le API DocuSign. Il codice per l’azione di invio personalizzata è disponibile su [AEM Forms campiona l’archivio Git pubblico](https://github.com/adobe/aem-forms-docusign-sample). Puoi distribuire il codice così come si trova nell’ambiente AEM Forms o personalizzarlo in base ai requisiti della tua organizzazione.

Per configurare l’azione di invio personalizzata predefinita e il Cloud Service DocuSign, effettua le seguenti operazioni:

1. [Clonare l’as a Cloud Service progetto AEM Forms](setup-local-development-environment.md#forms-cloud-service-local-development-environment) o creare un [!DNL Experience Manager Forms] as a [!DNL Cloud Service] progetto basato su [AEM Archetipo 27](https://github.com/adobe/aem-project-archetype) o più tardi. Per creare un [!DNL Experience Manager Forms] as a [!DNL Cloud Service] progetto basato su Archetipo AEM:
   </br> Apri il prompt dei comandi ed esegui il comando seguente per creare un [!DNL Experience Manager Forms] Progetto as a Cloud Service:

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Inoltre, modifica `appTitle`, `appId`, e `groupId`, nel comando precedente per riflettere l’ambiente.

1. Clona il [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample) archivio. Questo archivio contiene l&#39;azione di invio personalizzata per DocuSign e i dettagli di configurazione per la connessione al server DocuSign.

1. Apri l’as a Cloud Service progetto AEM Forms creato nel passaggio 1 per la modifica nell’IDE che preferisci.

1. Apri `[AEM Forms as a Cloud Service project]\pom.xml` file per la modifica e apportare le seguenti modifiche:

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

      In caso contrario `<repositories>` , crea il tag sotto il `<properties>` tag.

   1. Aggiungi il seguente testo alla fine del `<dependencyManagement>` tag:

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Effettua i seguenti passaggi nella `all/pom.xml` file disponibile nella cartella dei progetti di Cloud Service:

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

1. Apri il prompt dei comandi e passa a `aem-forms-samples\forms-integration-docusign` (clonato nel passaggio 3) ed esegui il comando seguente:

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` fa riferimento al nome della cartella creata nel passaggio 1 di questa procedura.

1. Implementa il progetto nell’ambiente di sviluppo locale. Puoi utilizzare il seguente comando per distribuire nell’ambiente di sviluppo locale

   `mvn -PautoInstallPackage clean install`

   Dopo aver eseguito questi passaggi, puoi visualizzare una nuova azione di invio personalizzata [Invia con firme elettroniche DocuSign](#enabledocusign) disponibile nell’elenco delle opzioni di invio per un modulo adattivo e un [Configurazione servizio cloud DocuSign](#configure-docusign-with-aem-forms) nell&#39;ambiente di sviluppo locale.

1. Compila e [Distribuisci il codice nel tuo [!DNL AEM Forms] ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Integrare [!DNL DocuSign] con [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

Dopo aver impostato i prerequisiti, effettua le seguenti operazioni per integrare [!DNL DocuSign] con [!DNL AEM Forms] sulle istanze Autore.

1. Accedi a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL DocuSign]** e seleziona una cartella per ospitare la configurazione.

1. Nella pagina Configurazioni, seleziona **[!UICONTROL Crea]** per creare [!DNL DocuSign] in AEM Forms.
1. In **[!UICONTROL Generale]** scheda di **[!UICONTROL Crea configurazione DocuSign]** , specificare un **[!UICONTROL Nome]** per la configurazione, quindi seleziona **[!UICONTROL Successivo]**. Facoltativamente, puoi specificare un valore **[!UICONTROL Titolo]**.

1. Copiare l&#39;URL nella finestra del browser corrente in un blocco note. L’URL è necessario per configurare [!DNL DocuSign] applicazione con [!DNL AEM Forms] in un passaggio successivo.

1. Configurare le impostazioni OAuth per [!DNL DocuSign] applicazione:

   1. Apri una finestra del browser e accedi al tuo [!DNL DocuSign] [account sviluppatore](https://admindemo.docusign.com/apps-and-keys).
   1. Apri l’app configurata per [!DNL AEM Forms].
   1. In **[!UICONTROL URI di reindirizzamento]** , aggiungi l’URL copiato nel passaggio precedente e fai clic su **[!UICONTROL Salva]**.
   1. Prendi nota dell’integrazione e delle chiavi segrete.

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un [!DNL DocuSign] e ottenere le chiavi, consulta [Configurare le impostazioni OAuth per l&#39;applicazione](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys) documentazione per gli sviluppatori.

1. Torna a **[!UICONTROL Crea configurazione DocuSign]** pagina. In **[!UICONTROL Impostazioni]** , la scheda **[!UICONTROL URL OAuth]** nel campo è indicato il seguente URL predefinito:

   `https://account-d.docusign.com/oauth/auth`

1. Specifica la **[!UICONTROL ID client]** (chiave di integrazione DocuSign) e **[!UICONTROL Segreto client]** (Chiave segreta DocuSign).

1. Seleziona **[!UICONTROL Connetti a DocuSign]**. Quando vengono richieste le credenziali, specifica il nome utente e la password dell’account utilizzato durante la creazione [!DNL DocuSign] applicazione. Quando ti viene richiesto di confermare l’accesso per `your developer account`, fai clic su **[!UICONTROL Consenti accesso]**. Se le credenziali sono corrette, viene visualizzato un messaggio di operazione riuscita.

1. Seleziona **[!UICONTROL Crea]** per creare [!DNL DocuSign] configurazione.

1. Seleziona la configurazione e fai clic su **[!UICONTROL Publish]**, seleziona la configurazione e fai clic su **[!UICONTROL Publish]**. Replica la configurazione negli ambienti di pubblicazione corrispondenti.

1. Ripeti tutti i passaggi precedenti sulle istanze di sviluppo, staging e produzione (a seconda di quale sia il passaggio rimasto) per completare la configurazione [!DNL DocuSign] con [!DNL AEM Forms] per il tuo ambiente.

Ora l’ambiente AEM Forms è configurato per l’utilizzo di DocuSign. Accertati di aggiungere il contenitore di configurazione utilizzato per il Cloud Service a tutti i Forms adattivi abilitati per [!DNL DocuSign]. È possibile specificare un contenitore di configurazione dalle proprietà di un modulo adattivo.

### Utilizzare [!DNL DocuSign] in un modulo adattivo {#enabledocusign}

È possibile abilitare [!DNL DocuSign] per un modulo adattivo esistente o crea un [!DNL DocuSign] è stato abilitato Adaptive Form. Scegliere una delle opzioni seguenti:

- [Creare un [!DNL DocuSign] Modulo adattivo abilitato](#create-an-adaptive-form-for-docusign)
- [Abilita [!DNL DocuSign] per un modulo adattivo esistente](#editafsign).

#### Creare un modulo adattivo per DocuSign {#create-an-adaptive-form-for-docusign}

Per creare un modulo adattivo abilitato alla firma:

1. Accedi a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**. Viene visualizzato un elenco di modelli. Seleziona un modello e seleziona **[!UICONTROL Successivo]**.
1. In **[!UICONTROL Base]** scheda:

   1. Specifica la **[!UICONTROL Nome]** e **[!UICONTROL Titolo]** per il modulo adattivo.

   1. Seleziona la [Contenitore configurazione](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante [integrazione [!DNL DocuSign] con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

   Il contenitore di configurazione contiene [!DNL DocuSign] Cloud Service configurati per l’ambiente. Questi servizi sono disponibili per la selezione nell’editor di moduli adattivi.

1. In **[!UICONTROL Modello modulo]** , selezionare una delle opzioni seguenti:

   - Se si dispone di un modello di modulo personalizzato e si richiede un documento di record basato sul modello di modulo, selezionare **[!UICONTROL Associa modello modulo come modello del documento record]** e selezionare un modello di documento record. Quando si utilizza l&#39;opzione, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   - Se non si dispone di un modello di modulo personalizzato, selezionare **[!UICONTROL Genera documento di record]** opzione. Quando utilizzi l’opzione, nel documento inviato per la firma vengono visualizzati tutti i campi del modulo adattivo.

1. Seleziona **[!UICONTROL Crea.]** Viene creato un modulo adattivo abilitato alla firma. Puoi aggiungere il tuo [!DNL DocuSign] nel modulo e inviarlo per la firma.
1. Apri il modulo adattivo in modalità di modifica. In **[!UICONTROL Contenuto]** , seleziona la scheda **[!UICONTROL Contenitore modulo]** e seleziona ![Configura](assets/configure-icon.svg).

1. In **[!UICONTROL Invio]** sezione, seleziona **[!UICONTROL Invia con firme elettroniche DocuSign]** dal **[!UICONTROL Azione di invio]** elenco a discesa.

1. In **[!UICONTROL Configurazione azione]** sezione, seleziona **[!UICONTROL Aggiungi]** per aggiungere un destinatario e specificarne l’indirizzo e-mail. Seleziona **[!UICONTROL Aggiungi]** per aggiungere altri destinatari.

1. Specifica l’oggetto del messaggio e-mail nel **[!UICONTROL Oggetto e-mail]** campo. Seleziona **Includi allegati** per includere allegati nel messaggio e-mail.

1. Seleziona ![Salva](assets/save_icon.svg) per salvare le proprietà.

#### Abilita [!DNL DocuSign] per un modulo adattivo {#editafsign}

Da utilizzare [!DNL DocuSign] in un modulo adattivo esistente:

1. Accedi a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona il modulo adattivo e seleziona **[!UICONTROL Proprietà]**.
1. In **[!UICONTROL Base]** , seleziona la scheda [Contenitore configurazione](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante l’integrazione [!DNL DocuSign] con [!DNL AEM Forms].
1. In **[!UICONTROL Modello modulo]** , selezionare una delle opzioni seguenti:

   - Se si dispone di un modello di modulo personalizzato e si richiede un documento di record basato sul modello di modulo, selezionare **[!UICONTROL Associa modello modulo come modello del documento record]** e selezionare un modello di documento record. Quando si utilizza l&#39;opzione, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   - Se non si dispone di un modello di modulo personalizzato, selezionare **[!UICONTROL Genera documento di record]** opzione. Quando utilizzi l’opzione, nel documento inviato per la firma vengono visualizzati tutti i campi del modulo adattivo.

1. Seleziona **[!UICONTROL Salva e chiudi]**. Il modulo adattivo è abilitato per [!DNL DocuSign]. Ora puoi aggiungere il tuo [!DNL DocuSign] nel modulo e inviarlo per la firma.

1. Apri il modulo adattivo in modalità di modifica. In **[!UICONTROL Contenuto]** , seleziona la scheda **[!UICONTROL Contenitore modulo]** e seleziona ![Configura](assets/configure-icon.svg).

1. In **[!UICONTROL Invio]** sezione, seleziona **[!UICONTROL Invia con firme elettroniche DocuSign]** dal **[!UICONTROL Azione di invio]** elenco a discesa.

1. In **[!UICONTROL Configurazione azione]** sezione, seleziona **[!UICONTROL Aggiungi]** per aggiungere un destinatario e specificarne l’indirizzo e-mail. Seleziona **[!UICONTROL Aggiungi]** per aggiungere altri destinatari.

1. Specifica l’oggetto del messaggio e-mail nel **[!UICONTROL Oggetto e-mail]** campo. Seleziona **Includi allegati** per includere allegati nel messaggio e-mail.

1. Seleziona ![Salva](assets/save_icon.svg) per salvare le proprietà.
