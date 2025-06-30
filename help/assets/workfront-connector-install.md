---
title: Installa [!DNL Workfront for Experience Manager enhanced connector]
description: Installa [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# Installare [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Un utente con accesso amministratore in [!DNL Adobe Experience Manager] come [!DNL Cloud Service] installa il connettore avanzato. Prima dell&#39;installazione, controlla il supporto della piattaforma e altri [prerequisiti per il connettore](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>A giugno 2022, Adobe ha rilasciato una nuova integrazione nativa per la connessione di Workfront con Adobe Experience Manager Assets as a Cloud Service. Questa integrazione è diventata il metodo richiesto per collegare queste due soluzioni. Qualsiasi nuova implementazione futura del connettore avanzato (versione 1.9.8 e successive) per collegare Workfront ad AEM Assets as a Cloud Service è bloccata. Per ulteriori informazioni su come configurare questa integrazione, vedere [Configurare l&#39;integrazione Experience Manager Assets as a Cloud Service](workfront-connector-configure.md).

>[!IMPORTANT]
>
>* Adobe richiede la distribuzione e la configurazione di [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se distribuita e configurata senza un partner certificato o [!DNL Adobe Professional Services], non è supportata da Adobe.
>
>* Adobe potrebbe rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono ridondante questo connettore; in tal caso, i clienti potrebbero dover passare dall&#39;utilizzo di questo connettore.
>
>* Adobe supporta le versioni migliorate del connettore 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per verificare la versione del connettore avanzato, vedere il passaggio 5(a) delle [istruzioni di installazione del connettore avanzato](workfront-connector-install.md).
>
>* Consulta [Esame di certificazione partner per il connettore avanzato Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedere [Guida all&#39;esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

Prima di installare il connettore, effettuare le seguenti operazioni di preinstallazione:

1. Se il programma AEM as a Cloud Service ha configurato il networking avanzato e abilitato l’inserimento di IP nell’elenco Consentiti, devi aggiungere gli IP Workfront a questo elenco per consentire la trasmissione delle sottoscrizioni di eventi e di varie chiamate API ad AEM.

   * [IP cluster Workfront](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=it#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9). Per conoscere il cluster IP in [!DNL Workfront], passare a **[!UICONTROL Configurazione]** > **[!UICONTROL Sistema]** > **[!UICONTROL Informazioni cliente]**.

   * [IP API sottoscrizione eventi Workfront](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html?lang=it)

   >[!IMPORTANT]
   >
   >* Se per il programma è stata configurata la funzionalità di rete avanzata e si sta utilizzando l’elenco di indirizzi IP consentiti, a causa di una limitazione con l’architettura del connettore Workfront avanzato è necessario aggiungere anche l’IP in uscita dal programma all’elenco Consentiti in Cloud Manager.
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* Per trovare l’IP del programma, apri una finestra del terminale ed esegui un comando, ad esempio:
   >
   >    ```
   >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
   >    
   >    ```

1. Verificare che le sovrapposizioni seguenti non esistano nell&#39;archivio [!DNL Experience Manager]. Se disponi di sovrapposizioni preesistenti su questi percorsi, rimuovi le sovrapposizioni o unisci il delta delle modifiche tra i due:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. L&#39;installazione richiede l&#39;impostazione di un progetto Maven in [!DNL Experience Manager] come [!DNL Cloud Service]. Utilizza le seguenti risorse per comprendere come includere un pacchetto di terze parti nel progetto Maven:

   * [Includi pacchetto di terze parti nel progetto Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=it#including-third-party).
   * [Distribuisci con [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=it).

Per installare il componente aggiuntivo in [!DNL Experience Manager] come [!DNL Cloud Service], eseguire la procedura seguente:

1. Scarica il connettore avanzato da [Distribuzione software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Accedi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=it) e clona l&#39;archivio AEM as a Cloud Service da Cloud Manager.

1. Apri l’archivio AEM as a Cloud Service clonato utilizzando un IDE a tua scelta.

1. Posiziona il file zip del connettore avanzato scaricato nel passaggio 1 nel seguente percorso:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Se la cartella `resources` non esiste, crearla.


1. Aggiungi `pom.xml` dipendenze:

   1. Aggiungere una dipendenza nell&#39;elemento padre `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
      ```

      >[!NOTE]
      >
      >Assicurarsi di aggiornare il numero di versione del connettore avanzato prima di copiare la dipendenza nell&#39;elemento padre `pom.xml`.

   1. Aggiungere una dipendenza in `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. Aggiungi `pom.xml` incorporamenti. Aggiungi i pacchetti [!DNL Workfront for Experience Manager enhanced connector] alla sezione `embeddeds` di `pom.xml` di tutti i sottoprogetti. Deve essere incorporato in tutti i moduli `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   La destinazione della sezione incorporata è impostata su `/apps/<path-to-project-install-folder>/install`. Il percorso JCR `/apps/<path-to-project-install-folder>` deve essere incluso nelle regole del filtro nel file `all/src/main/content/META-INF/vault/filter.xml`. Le regole di filtro per l’archivio in genere derivano dal nome del programma. Utilizza il nome della cartella come destinazione nelle regole esistenti.

1. Invia le modifiche all’archivio.

1. Esegui la pipeline per [distribuire le modifiche in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=it).

1. Per creare una configurazione utente di sistema, creare `wf-workfront-users` nel gruppo utenti [!DNL Experience Manager] e assegnare l&#39;autorizzazione `jcr:all` a `/content/dam`. Un utente di sistema `workfront-tools` viene creato automaticamente e le autorizzazioni richieste vengono gestite automaticamente. Tutti gli utenti di [!DNL Workfront] che utilizzano il connettore avanzato vengono aggiunti automaticamente come parte di questo gruppo.

Per informazioni sull&#39;aggiornamento di [!DNL Workfront for Experience Manager enhanced connector] da una versione precedente alla versione più recente, fare clic [qui](update-workfront-enhanced-connector.md).

## Configura la connessione tra [!DNL Experience Manager] come [!DNL Cloud Service] e [!DNL Workfront] {#configure-connection}

Per creare una connessione con [!DNL Workfront], eseguire la procedura seguente:

1. In [!DNL Experience Manager], selezionare **[!UICONTROL Strumenti]** > **[!UICONTROL Servizi cloud]** > **[!UICONTROL Configurazione strumenti Workfront]**.

1. Seleziona `workfront-tools` nel pannello a sinistra e seleziona l&#39;opzione **[!UICONTROL Crea]** nell&#39;area superiore destra della pagina.

1. Nella finestra di dialogo **[!UICONTROL Connessione Workfront]**, fornisci i dettagli richiesti della distribuzione di [!DNL Workfront] e seleziona l&#39;opzione **[!UICONTROL Connetti a Workfront]**. Dopo la connessione, l&#39;integrazione personalizzata del documento [!DNL Workfront] viene creata automaticamente nell&#39;ambiente [!DNL Workfront].

   ![Connetti [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Passare alla scheda **[!UICONTROL Avanzate]** e selezionare l&#39;opzione **[!UICONTROL È il server AEM as a Cloud Service]**.
