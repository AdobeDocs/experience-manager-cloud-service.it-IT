---
title: Installa [!DNL Workfront for Experience Manager enhanced connector]
description: Installa [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: d0d89c3905b2bf357de8a7599245c9360444e53b
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# Installa [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html) |
| AEM as a Cloud Service | Questo articolo |

Un utente con accesso amministratore in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] installa il connettore avanzato. Prima dell’installazione, controlla il supporto della piattaforma e altro ancora [prerequisiti per il connettore](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* L’Adobe richiede l’implementazione e la configurazione del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se implementato e configurato senza un partner certificato o [!DNL Adobe Professional Services], non è supportato da Adobe.
>
>* Adobe può rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono questo connettore ridondante; in tal caso, i clienti potrebbero dover passare dall’utilizzo di questo connettore.
>
>* Adobe supporta le versioni migliorate del connettore 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per verificare la versione del connettore avanzato, vedere il punto 5(a) di [istruzioni per l&#39;installazione del connettore avanzato](workfront-connector-install.md).
>
>* Consulta [Connettore avanzato per la certificazione dei partner per Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedere [Guida all’esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


Prima di installare il connettore, effettuare le seguenti operazioni di preinstallazione:

1. Se il programma as a Cloud Service per l’AEM ha configurato il networking avanzato e abilitato l’inserimento nell’elenco Consentiti IP, devi aggiungere gli IP Workfront a questo elenco per consentire la trasmissione all’AEM delle sottoscrizioni di eventi e di varie chiamate API.

   * [IP cluster Workfront](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=en#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9). Per conoscere il cluster IP in [!DNL Workfront], passa a **[!UICONTROL Configurazione]** > **[!UICONTROL Sistema]** > **[!UICONTROL Informazioni Cliente]**.

   * [IP API per abbonamento a eventi di Workfront](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html)
   >[!IMPORTANT]
   >
   >* Se hai configurato la funzione Rete avanzata per il programma e utilizzi l’inserimento di IP nell’elenco Consentiti, a causa di una limitazione con l’architettura del connettore Workfront avanzato è necessario aggiungere anche l’IP in uscita dal programma all’elenco Consentiti in Cloud Manager.
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* Per trovare l’IP del programma, apri una finestra del terminale ed esegui un comando, ad esempio:

      >
      >    ```TXT
      >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
      >
      >    ```

1. Assicurati che le seguenti sovrapposizioni non esistano in [!DNL Experience Manager] archivio. Se disponi di sovrapposizioni preesistenti su questi percorsi, rimuovi le sovrapposizioni o unisci il delta delle modifiche tra i due:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. Questa installazione richiede le conoscenze necessarie per impostare un progetto Maven in [!DNL Experience Manager] as a [!DNL Cloud Service]. Utilizza le seguenti risorse per comprendere come includere un pacchetto di terze parti nel progetto Maven:

   * [Includi pacchetto di terze parti nel progetto Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Distribuisci con [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=it).

Per installare il componente aggiuntivo in [!DNL Experience Manager] as a [!DNL Cloud Service], effettua le seguenti operazioni:

1. Scarica il connettore avanzato da [Distribuzione di software di Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) e clona l’archivio AEM as a Cloud Service da Cloud Manager.

1. Apri l’archivio AEM as a Cloud Service clonato utilizzando un IDE a tua scelta.

1. Posiziona il file zip del connettore avanzato scaricato nel passaggio 1 nel seguente percorso:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Se il `resources` cartella inesistente, crea la cartella.


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
      >Assicurati di aggiornare il numero di versione del connettore avanzato prima di copiare la dipendenza nell’elemento padre `pom.xml`.

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


1. Aggiungi `pom.xml` incorpora. Aggiungi il [!DNL Workfront for Experience Manager enhanced connector] pacchetti a `embeddeds` sezione del `pom.xml` di tutti i sottoprogetti. Deve essere incorporato nel modulo all `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   La destinazione della sezione incorporata è impostata su `/apps/<path-to-project-install-folder>/install`. Questo percorso JCR `/apps/<path-to-project-install-folder>` deve essere incluso nelle regole del filtro in `all/src/main/content/META-INF/vault/filter.xml` file. Le regole di filtro per l’archivio in genere derivano dal nome del programma. Utilizza il nome della cartella come destinazione nelle regole esistenti.

1. Invia le modifiche all’archivio.

1. Esegui la pipeline per [distribuire le modifiche in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. Per creare una configurazione utente di sistema, creare `wf-workfront-users` in [!DNL Experience Manager] Gruppo di utenti e assegnazione dell’autorizzazione `jcr:all` a `/content/dam`. Un utente di sistema `workfront-tools` viene creato automaticamente e le autorizzazioni richieste vengono gestite automaticamente. Tutti gli utenti da [!DNL Workfront] che utilizzano il connettore avanzato vengono aggiunti automaticamente come parte di questo gruppo.

Per informazioni sull&#39;aggiornamento di [!DNL Workfront for Experience Manager enhanced connector] da una versione precedente alla versione più recente, fai clic su [qui](update-workfront-enhanced-connector.md).

## Configurare la connessione tra [!DNL Experience Manager] as a [!DNL Cloud Service] e [!DNL Workfront] {#configure-connection}

Per creare una connessione con [!DNL Workfront], effettua le seguenti operazioni:

1. In entrata [!DNL Experience Manager], seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurazione strumenti Workfront]**.

1. Seleziona `workfront-tools` nel pannello a sinistra e seleziona **[!UICONTROL Crea]** in alto a destra.

1. In **[!UICONTROL Connessione Workfront]** , fornisci i dettagli richiesti della tua [!DNL Workfront] distribuzione e selezionare **[!UICONTROL Connetti a Workfront]** opzione. Una volta stabilita la connessione, il [!DNL Workfront] l’integrazione personalizzata dei documenti viene creata automaticamente in [!DNL Workfront] ambiente.

   ![Connetti [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Accedi a **[!UICONTROL Avanzate]** e seleziona l’opzione **[!UICONTROL Il server è as a Cloud Service per AEM]**.
