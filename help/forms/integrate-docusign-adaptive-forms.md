---
title: Come integrare DocuSign con un modulo adattivo?
description: Scopri come utilizzare DocuSign con un modulo adattivo per raccogliere firme elettroniche.
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 1%

---

# Utilizzo di DocuSign con un modulo adattivo {#integrate-aem-forms-with-DocuSign}

DocuSign è una soluzione di firma elettronica importante. È possibile utilizzarlo per firmare un accordo tramite posta elettronica. È possibile integrare DocuSign con un modulo adattivo. Consente di inviare un modulo adattivo per le firme elettroniche a più destinatari. L’utilizzo delle firme elettroniche consente di:

- Chiudere le offerte da qualsiasi dispositivo con procedure di proposta, preventivo e contratto completamente automatizzate.
- Completa i processi relativi alle risorse umane più rapidamente e offri ai tuoi dipendenti le esperienze digitali.
- Ridurre i tempi di ciclo del contratto e integrare i fornitori più rapidamente.

AEM Forms as a Cloud Service fornisce [un&#39;azione di invio personalizzata per DocuSign](#deploy-custom-submit-action). L’azione invia consente di inviare i moduli adattivi per le firme elettroniche utilizzando le API DocuSign.

| Puoi anche utilizzare la soluzione di firma elettronica di Adobe, Adobe Sign, per apporre la firma elettronica a un modulo adattivo. AEM Forms offre un’integrazione molto più profonda con Adobe Sign e controlli molto più precisi, come la firma sequenziale e parallela, più metodi di autenticazione, esperienza di firma interna ai moduli e altro ancora. Per ulteriori informazioni, consulta [Utilizzo di Adobe Sign in un modulo adattivo](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Prerequisiti {#prerequisites}

Per integrare DocuSign con AEM Forms sono necessari i seguenti elementi:

- Un account DocuSign [sviluppatore](https://developers.docusign.com/platform/account/)
- Un&#39;applicazione DocuSign
- Credenziali (ID client e segreto client) dell’applicazione API DocuSign.
- [Azione di invio personalizzata e servizio cloud per DocuSign](https://github.com/adobe/aem-forms-docusign-sample)
- (Solo per l&#39;ambiente di sviluppo locale) [Imposta documento di record](setup-local-development-environment.md#docker-microservices).

## Configurare l’azione di invio personalizzata e Cloud Service per DocuSign {#deploy-custom-submit-action}

AEM Forms as a Cloud Service fornisce un’azione di invio personalizzata per DocuSign. L’azione invia consente di inviare i moduli adattivi per le firme elettroniche utilizzando le API DocuSign. Il codice per l&#39;azione di invio personalizzata è disponibile nell&#39;[archivio Git pubblico degli esempi di AEM Forms](https://github.com/adobe/aem-forms-docusign-sample). Puoi distribuire il codice così come si trova nell’ambiente AEM Forms o personalizzarlo in base ai requisiti della tua organizzazione.

Per configurare l’azione di invio personalizzata predefinita e DocuSign Cloud Service, effettua le seguenti operazioni:

1. [Clona il progetto AEM Forms as a Cloud Service](setup-local-development-environment.md#forms-cloud-service-local-development-environment) o crea un progetto [!DNL Experience Manager Forms] come progetto [!DNL Cloud Service] basato su [AEM Archetype 27](https://github.com/adobe/aem-project-archetype) o versione successiva. Per creare un [!DNL Experience Manager Forms] come progetto [!DNL Cloud Service] basato su Archetipo AEM:
   </br> Aprire il prompt dei comandi ed eseguire il comando seguente per creare un progetto as a Cloud Service [!DNL Experience Manager Forms]:

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Inoltre, modifica `appTitle`, `appId` e `groupId` nel comando precedente per riflettere l&#39;ambiente.

1. Clona l&#39;archivio [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample). Questo archivio contiene l&#39;azione di invio personalizzata per DocuSign e i dettagli di configurazione per la connessione al server DocuSign.

1. Apri il progetto AEM Forms as a Cloud Service creato nel passaggio 1 per la modifica nell’IDE che preferisci.

1. Apri il file `[AEM Forms as a Cloud Service project]\pom.xml` per la modifica e apporta le seguenti modifiche:

   1. Aggiungere il testo seguente alla fine del tag `<properties>`:

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. Aggiungere il testo seguente alla fine del tag `<repositories>`:

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      Se non è presente alcun tag `<repositories>`, creare il tag sotto il tag `<properties>`.

   1. Aggiungere il testo seguente alla fine del tag `<dependencyManagement>`:

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Eseguire i passaggi seguenti nel file `all/pom.xml` disponibile nella cartella dei progetti di Cloud Service:

   1. Aggiungere il testo seguente alla fine del tag `<embeddeds>`:

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. Aggiungere il testo seguente alla fine del tag `<dependencies>`:

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. Aprire il prompt dei comandi, passare a `aem-forms-samples\forms-integration-docusign` (clonato nel passaggio 3) ed eseguire il comando seguente:

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` fa riferimento al nome della cartella creata nel passaggio 1 di questa procedura.

1. Implementa il progetto nell’ambiente di sviluppo locale. Puoi utilizzare il seguente comando per distribuire nell’ambiente di sviluppo locale

   `mvn -PautoInstallPackage clean install`

   Dopo aver eseguito questi passaggi, puoi visualizzare una nuova azione di invio personalizzata [Invia con le firme elettroniche DocuSign](#enabledocusign) disponibile nell&#39;elenco delle opzioni di invio per un modulo adattivo e una [configurazione del servizio cloud DocuSign](#configure-docusign-with-aem-forms) nell&#39;ambiente di sviluppo locale.

1. Compila e [distribuisci il codice nell&#39;ambiente [!DNL AEM Forms] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=it#customer-releases).

## Integra [!DNL DocuSign] con [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

Dopo aver impostato i prerequisiti, effettuare le seguenti operazioni per integrare [!DNL DocuSign] con [!DNL AEM Forms] nelle istanze di authoring.

1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL DocuSign]** e seleziona una cartella per ospitare la configurazione.

1. Nella pagina Configurazioni, seleziona **[!UICONTROL Crea]** per creare la configurazione [!DNL DocuSign] in AEM Forms.
1. Nella scheda **[!UICONTROL Generale]** della pagina **[!UICONTROL Crea configurazione DocuSign]**, specificare **[!UICONTROL Nome]** per la configurazione e selezionare **[!UICONTROL Avanti]**. Facoltativamente, puoi specificare un **[!UICONTROL Titolo]**.

1. Copiare l&#39;URL nella finestra del browser corrente in un blocco note. L&#39;URL è necessario per configurare l&#39;applicazione [!DNL DocuSign] con [!DNL AEM Forms] in un passaggio successivo.

1. Configurare le impostazioni OAuth per l&#39;applicazione [!DNL DocuSign]:

   1. Apri una finestra del browser e accedi al tuo account [!DNL DocuSign] [sviluppatore](https://admindemo.docusign.com/apps-and-keys).
   1. Apri l&#39;app configurata per [!DNL AEM Forms].
   1. Nella casella **[!UICONTROL URI reindirizzamento]** aggiungere l&#39;URL copiato nel passaggio precedente e fare clic su **[!UICONTROL Salva]**.
   1. Prendi nota dell’integrazione e delle chiavi segrete.

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un&#39;applicazione [!DNL DocuSign] e ottenere le chiavi, vedere [Configurare le impostazioni OAuth per la documentazione per gli sviluppatori dell&#39;applicazione](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys).

1. Tornare alla pagina **[!UICONTROL Crea configurazione DocuSign]**. Nella scheda **[!UICONTROL Impostazioni]**, il campo **[!UICONTROL URL OAuth]** fa riferimento al seguente URL predefinito:

   `https://account-d.docusign.com/oauth/auth`

1. Specificare **[!UICONTROL ID client]** (chiave di integrazione DocuSign) e **[!UICONTROL Segreto client]** (chiave segreta DocuSign).

1. Selezionare **[!UICONTROL Connetti a DocuSign]**. Quando vengono richieste le credenziali, specificare il nome utente e la password dell&#39;account utilizzato durante la creazione dell&#39;applicazione [!DNL DocuSign]. Quando viene richiesto di confermare l&#39;accesso per `your developer account`, fare clic su **[!UICONTROL Consenti accesso]**. Se le credenziali sono corrette, viene visualizzato un messaggio di operazione riuscita.

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione di [!DNL DocuSign].

1. Seleziona la configurazione e fai clic su **[!UICONTROL Pubblica]**, seleziona la configurazione e fai clic su **[!UICONTROL Pubblica]**. Replica la configurazione negli ambienti di pubblicazione corrispondenti.

1. Ripeti tutti i passaggi precedenti per le istanze di sviluppo, stage e produzione (qualsiasi sia rimasto) per completare la configurazione di [!DNL DocuSign] con [!DNL AEM Forms] per il tuo ambiente.

Ora l’ambiente AEM Forms è configurato per l’utilizzo di DocuSign. Accertati di aggiungere il contenitore di configurazione utilizzato per Cloud Service a tutto il Forms adattivo abilitato per [!DNL DocuSign]. È possibile specificare un contenitore di configurazione dalle proprietà di un modulo adattivo.

### Usa [!DNL DocuSign] in un modulo adattivo {#enabledocusign}

È possibile abilitare [!DNL DocuSign] per un modulo adattivo esistente o crearne uno abilitato per [!DNL DocuSign]. Scegliere una delle opzioni seguenti:

- [Crea un modulo adattivo abilitato per  [!DNL DocuSign] &#x200B;](#create-an-adaptive-form-for-docusign)
- [Attiva [!DNL DocuSign] per un modulo adattivo esistente](#editafsign).

#### Creare un modulo adattivo per DocuSign {#create-an-adaptive-form-for-docusign}

Per creare un modulo adattivo abilitato alla firma:

1. Passa ad **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Seleziona **[!UICONTROL Crea]** e **[!UICONTROL Modulo adattivo]**. Viene visualizzato un elenco di modelli. Seleziona un modello e seleziona **[!UICONTROL Avanti]**.
1. Nella scheda **[!UICONTROL Base]**:

   1. Specifica il **[!UICONTROL Nome]** e il **[!UICONTROL Titolo]** per il modulo adattivo.

   1. Seleziona il [contenitore di configurazione](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante l&#39;[integrazione [!DNL DocuSign] con [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

   Il contenitore di configurazione contiene i servizi cloud [!DNL DocuSign] configurati per l&#39;ambiente. Questi servizi sono disponibili per la selezione nel generatore di moduli adattivi.

1. Nella scheda **[!UICONTROL Modello modulo]** selezionare una delle opzioni seguenti:

   - Se si dispone di un modello di modulo personalizzato e si richiede un documento di record basato sul modello di modulo, selezionare l&#39;opzione **[!UICONTROL Associa modello di modulo come modello di documento record]** e selezionare un modello di documento record. Quando si utilizza l&#39;opzione, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   - Se non si dispone di un modello di modulo personalizzato, selezionare l&#39;opzione **[!UICONTROL Genera documento di record]**. Quando utilizzi l’opzione, nel documento inviato per la firma vengono visualizzati tutti i campi del modulo adattivo.

1. Seleziona **[!UICONTROL Crea]**. Viene creato un modulo adattivo abilitato alla firma. Puoi aggiungere i campi [!DNL DocuSign] al modulo e inviarlo per la firma.
1. Apri il modulo adattivo in modalità di modifica. Nella scheda **[!UICONTROL Contenuto]**, seleziona **[!UICONTROL Contenitore modulo]** e ![Configura](assets/configure-icon.svg).

1. Nella sezione **[!UICONTROL Invio]**, selezionare **[!UICONTROL Invia con firme elettroniche DocuSign]** dall&#39;elenco a discesa **[!UICONTROL Azione invio]**.

1. Nella sezione **[!UICONTROL Configurazione azione]**, seleziona **[!UICONTROL Aggiungi]** per aggiungere un destinatario e specificare l&#39;indirizzo e-mail del destinatario. Seleziona di nuovo **[!UICONTROL Aggiungi]** per aggiungere altri destinatari.

1. Specifica l&#39;oggetto del messaggio e-mail nel campo **[!UICONTROL Oggetto e-mail]**. Selezionare **Includi allegati** per includere gli allegati nel messaggio di posta elettronica.

1. Seleziona ![Salva](assets/save_icon.svg) per salvare le proprietà.

#### Abilita [!DNL DocuSign] per un modulo adattivo {#editafsign}

Per utilizzare [!DNL DocuSign] in un modulo adattivo esistente:

1. Passa ad **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Moduli]** > **[!UICONTROL Moduli e documenti]**.
1. Seleziona il modulo adattivo e seleziona **[!UICONTROL Proprietà]**.
1. Nella scheda **[!UICONTROL Base]**, seleziona il [contenitore di configurazione](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) creato durante l&#39;integrazione di [!DNL DocuSign] con [!DNL AEM Forms].
1. Nella scheda **[!UICONTROL Modello modulo]** selezionare una delle opzioni seguenti:

   - Se si dispone di un modello di modulo personalizzato e si richiede un documento di record basato sul modello di modulo, selezionare l&#39;opzione **[!UICONTROL Associa modello di modulo come modello di documento record]** e selezionare un modello di documento record. Quando si utilizza l&#39;opzione, i documenti inviati per la firma visualizzano solo i campi basati sul modello di modulo associato. Non visualizza tutti i campi del modulo adattivo.

   - Se non si dispone di un modello di modulo personalizzato, selezionare l&#39;opzione **[!UICONTROL Genera documento di record]**. Quando utilizzi l’opzione, nel documento inviato per la firma vengono visualizzati tutti i campi del modulo adattivo.

1. Seleziona **[!UICONTROL Salva e chiudi]**. Modulo adattivo abilitato per [!DNL DocuSign]. Ora puoi aggiungere i campi [!DNL DocuSign] al modulo e inviarlo per la firma.

1. Apri il modulo adattivo in modalità di modifica. Nella scheda **[!UICONTROL Contenuto]**, seleziona **[!UICONTROL Contenitore modulo]** e ![Configura](assets/configure-icon.svg).

1. Nella sezione **[!UICONTROL Invio]**, selezionare **[!UICONTROL Invia con firme elettroniche DocuSign]** dall&#39;elenco a discesa **[!UICONTROL Azione invio]**.

1. Nella sezione **[!UICONTROL Configurazione azione]**, seleziona **[!UICONTROL Aggiungi]** per aggiungere un destinatario e specificare l&#39;indirizzo e-mail del destinatario. Seleziona di nuovo **[!UICONTROL Aggiungi]** per aggiungere altri destinatari.

1. Specifica l&#39;oggetto del messaggio e-mail nel campo **[!UICONTROL Oggetto e-mail]**. Selezionare **Includi allegati** per includere gli allegati nel messaggio di posta elettronica.

1. Seleziona ![Salva](assets/save_icon.svg) per salvare le proprietà.
