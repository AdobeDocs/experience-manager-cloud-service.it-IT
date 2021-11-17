---
title: Installare la versione [!DNL Workfront for Experience Manager enhanced connector]
description: Installare la versione [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: 8ca25f86a8d0d61b40deaff0af85e56e438efbdc
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

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
   * [Distribuisci con [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

Per installare il componente aggiuntivo in [!DNL Experience Manager] come [!DNL Cloud Service], segui questi passaggi:

1. Aggiungi `pom.xml` dipendenze:

   1. Aggiungi una dipendenza nell&#39;elemento padre `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>1.7.4</version>
      </dependency>
      ```

   1. Aggiungi una dipendenza in tutto il modulo [!DNL pom.xml].

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
         </dependency>
      ```

1. Aggiungi `pom.xml` autenticazione.

   1. Includi la seguente configurazione dell’archivio nel file pom.xml all’interno del profilo adobe-public, in modo che le dipendenze del connettore (sopra) possano essere risolte in fase di creazione (sia localmente che da Cloud Manager). Al momento dell’acquisto di una licenza verranno fornite le credenziali per l’accesso all’archivio. Le credenziali dovranno essere aggiunte al file settings.xml nella sezione server .

      ```XML
      <repository>
         <id>hoodoo-maven</id>
         <name>Hoodoo Repository</name>
         <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
      </repository>
      ```

   1. Crea un file denominato `./cloudmanager/maven/settings.xml` nella directory principale del progetto. Per supportare un archivio Maven protetto da password, vedi [come impostare il progetto](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md). Inoltre, un esempio `settings.xml` file di riferimento. Infine, aggiorna il tuo locale `settings.xml` per la compilazione locale.

      ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
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

1. Per creare una configurazione utente di sistema, crea `wf-workfront-users` in [!DNL Experience Manager] Gruppo di utenti e assegna l’autorizzazione `jcr:all` a `/content/dam`. Utente di sistema `workfront-tools` viene creato automaticamente e le autorizzazioni richieste vengono gestite automaticamente. Tutti gli utenti da [!DNL Workfront] che utilizzano il connettore avanzato vengono aggiunti automaticamente come parte di questo gruppo.

## Configura la connessione tra [!DNL Experience Manager] come [!DNL Cloud Service] e [!DNL Workfront] {#configure-connection}

Per creare una connessione con [!DNL Workfront], segui questi passaggi:

1. In [!DNL Experience Manager], seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione strumenti Workfront]**.

1. Seleziona `workfront-tools` nel pannello a sinistra e seleziona **[!UICONTROL Crea]** nell’area in alto a destra della pagina.

1. In **[!UICONTROL Connessione Workfront]** , fornire i dettagli richiesti [!DNL Workfront] distribuzione e seleziona **[!UICONTROL Connessione a Workfront]** opzione . Una volta connessa correttamente, la [!DNL Workfront] l’integrazione personalizzata dei documenti viene creata automaticamente in [!DNL Workfront] ambiente.

   ![Connetti [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Passa a **[!UICONTROL Avanzate]** e seleziona l’opzione **[!UICONTROL È as a Cloud Service il server AEM]**.
