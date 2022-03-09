---
title: Installare la versione [!DNL Workfront for Experience Manager enhanced connector]
description: Installare la versione [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: a5776453b261e6f4e6c891763934b236bade8f7f
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# Installare la versione [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

Un utente con accesso amministratore in [!DNL Adobe Experience Manager] come [!DNL Cloud Service] installa il connettore avanzato. Prima di eseguire l’installazione, controlla il supporto della piattaforma e altri [prerequisiti per il connettore](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>L&#39;Adobe richiede la distribuzione e la configurazione del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se implementato e configurato senza un partner certificato o [!DNL Adobe Professional Services], non è supportato da Adobe.
>
>Adobe può rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono tale connettore ridondante; in questo caso, potrebbe essere richiesto ai clienti di effettuare la transizione dall’utilizzo di questo connettore.

Prima di installare il connettore, segui questi passaggi di preinstallazione:

1. [Configurare il firewall](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). Per conoscere il cluster IP in [!DNL Workfront], passa a [!UICONTROL Configurazione] > [!UICONTROL Sistema] > [!UICONTROL Informazioni cliente].

1. Sul dispatcher, consenti intestazioni HTTP denominate `authorization`, `username`e `apikey`. Consenti `GET`, `POST`e `PUT` richieste a `/bin/workfront-tools`.

1. Assicurati che i percorsi seguenti non esistano in [!DNL Experience Manager] archivio:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Questa installazione richiede la conoscenza per impostare un progetto Maven in [!DNL Experience Manager] come [!DNL Cloud Service]. Utilizza le risorse seguenti per comprendere come includere un pacchetto di terze parti nel progetto Maven:

   * [Includere un pacchetto di terze parti nel progetto Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Distribuisci con [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=it).

Per installare il componente aggiuntivo in [!DNL Experience Manager] come [!DNL Cloud Service], segui questi passaggi:

1. Scarica il connettore avanzato da [Distribuzione di software di Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) e duplica l’archivio AEM as a Cloud Service da Cloud Manager.

1. Apri l’archivio as a Cloud Service clonato AEM utilizzando un IDE di tua scelta.

1. Posiziona il file zip del connettore avanzato scaricato al passaggio 1 nel seguente percorso:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Se la `resources` cartella inesistente. Creare la cartella.


1. Aggiungi `pom.xml` dipendenze:

   1. Aggiungi una dipendenza nell&#39;elemento padre `pom.xml`.

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
      >Assicurati di aggiornare il numero di versione del connettore avanzato prima di copiare la dipendenza nell&#39;elemento padre `pom.xml`.

   1. Aggiungi una dipendenza in `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. Aggiungi `pom.xml` incorpora. Aggiungi il [!DNL Workfront for Experience Manager enhanced connector] pacchetti a `embeddeds` della sezione `pom.xml` di tutti i sottoprogetti. Deve essere incorporato nel modulo all `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   Il target della sezione incorporata è impostato su `/apps/<path-to-project-install-folder>/install`. Questo percorso JCR `/apps/<path-to-project-install-folder>` deve essere incluso nelle regole di filtro nel `all/src/main/content/META-INF/vault/filter.xml` file. Le regole di filtro per l&#39;archivio sono in genere derivate dal nome del programma. Utilizza il nome della cartella come destinazione nelle regole esistenti.

1. Invia le modifiche all’archivio.

1. Esegui la pipeline in [distribuire le modifiche a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. Per creare una configurazione utente di sistema, crea `wf-workfront-users` in [!DNL Experience Manager] Gruppo di utenti e assegna l’autorizzazione `jcr:all` a `/content/dam`. Utente di sistema `workfront-tools` viene creato automaticamente e le autorizzazioni richieste vengono gestite automaticamente. Tutti gli utenti da [!DNL Workfront] che utilizzano il connettore avanzato vengono aggiunti automaticamente come parte di questo gruppo.

## Configura la connessione tra [!DNL Experience Manager] come [!DNL Cloud Service] e [!DNL Workfront] {#configure-connection}

Per creare una connessione con [!DNL Workfront], segui questi passaggi:

1. In [!DNL Experience Manager], seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione strumenti Workfront]**.

1. Seleziona `workfront-tools` nel pannello a sinistra e seleziona **[!UICONTROL Crea]** nell’area in alto a destra della pagina.

1. In **[!UICONTROL Connessione Workfront]** , fornire i dettagli richiesti [!DNL Workfront] distribuzione e seleziona **[!UICONTROL Connessione a Workfront]** opzione . Una volta connessa correttamente, la [!DNL Workfront] l’integrazione personalizzata dei documenti viene creata automaticamente in [!DNL Workfront] ambiente.

   ![Connetti [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Passa a **[!UICONTROL Avanzate]** e seleziona l’opzione **[!UICONTROL È as a Cloud Service il server AEM]**.
