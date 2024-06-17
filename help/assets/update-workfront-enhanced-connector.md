---
title: Aggiorna [!DNL Workfront for Experience Manager enhanced connector]
description: Aggiorna [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Aggiorna [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assets as a Cloud Service] consente di aggiornare [!DNL Workfront for Experience Manager enhanced connector] da una versione precedente alla versione più recente.

>[!TIP]
>
>Stai cercando [!DNL Workfront for Experience Manager enhanced connector] Aggiornare la documentazione di AEM 6.5? Clic [qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


Per aggiornare [!DNL Workfront for Experience Manager enhanced connector] alla versione più recente:

1. Scarica la versione più recente del connettore avanzato da [Distribuzione di software di Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Accesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) e clona l’archivio AEM as a Cloud Service da Cloud Manager.

1. Apri l’archivio as a Cloud Service dell’Experience Manager clonato utilizzando un IDE a tua scelta.

1. Posiziona il file zip del connettore avanzato scaricato nel passaggio 1 nel seguente percorso:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Se il `resources` cartella inesistente, crea la cartella.

1. Aggiorna la versione del connettore avanzato nell’elemento padre `pom.xml`.

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

1. Aggiornare la dipendenza in `all module pom.xml`.

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
   >Assicurati di aggiungere `<scope>` e `<systemPath>` alle dipendenze nei passaggi 5 e 6.

1. Aggiorna `pom.xml` incorpora. Aggiungi il [!DNL Workfront for Experience Manager enhanced connector] pacchetti a `embeddeds` sezione del `pom.xml` di tutti i sottoprogetti. Incorpora gli aggiornamenti in tutti i moduli `pom.xml`.

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

1. [Rimuovere le dipendenze dai punti di distribuzione Hoodoo](remove-external-dependencies.md), se presente.

1. Invia le modifiche all’archivio.

1. Esegui la pipeline per [distribuire le modifiche in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
