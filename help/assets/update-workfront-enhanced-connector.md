---
title: Aggiorna [!DNL Workfront for Experience Manager enhanced connector]
description: Aggiorna [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
source-git-commit: 77aceab8db82082185c931202fc6ea8eee79c11e
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Aggiorna [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assets as a Cloud Service] consente di aggiornare [!DNL Workfront for Experience Manager enhanced connector] da una versione precedente alla versione più recente.

>[!TIP]
>
>Stai cercando [!DNL Workfront for Experience Manager enhanced connector] aggiornare la documentazione per AEM 6.5? Fai clic su [qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


Per aggiornare [!DNL Workfront for Experience Manager enhanced connector] all’ultima versione:

1. Scarica la versione più recente del connettore avanzato da [Distribuzione di software di Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) e duplica l’archivio AEM as a Cloud Service da Cloud Manager.

1. Apri l’archivio as a Cloud Service di Experience Manager clonato utilizzando un IDE di tua scelta.

1. Posiziona il file zip del connettore avanzato scaricato al passaggio 1 nel seguente percorso:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Se la `resources` cartella inesistente. Creare la cartella.

1. Aggiorna la versione del connettore avanzato nell&#39;elemento padre `pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version> updated enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

1. Aggiorna la dipendenza in `all module pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <scope>system</scope>
         <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

   >[!NOTE]
   >
   >Assicurati di aggiungere `<scope>` e `<systemPath>` alle dipendenze dei punti 5 e 6.

1. Aggiorna `pom.xml` incorpora. Aggiungi il [!DNL Workfront for Experience Manager enhanced connector] pacchetti a `embeddeds` della sezione `pom.xml` di tutti i sottoprogetti. Incorpora gli aggiornamenti in tutti i moduli `pom.xml`.

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

1. [Rimuovere le dipendenze dai punti di distribuzione di Hoodoo](remove-external-dependencies.md), se del caso.

1. Invia le modifiche all’archivio.

1. Esegui la pipeline in [distribuire le modifiche a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
