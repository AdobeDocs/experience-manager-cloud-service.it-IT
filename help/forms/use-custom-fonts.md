---
title: 'Usa font personalizzati '
description: 'Usa font personalizzati '
source-git-commit: 94fe397d6ce08380ef08b65b47fe2c1aeb015ca3
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# Usa font personalizzati

**La documentazione sulle comunicazioni di Cloud Service è disponibile in versione beta**

È possibile utilizzare Forms as a Cloud Service Communications per combinare un modello XDP, un documento PDF basato su XDP o un modulo Acrobat (AcroForm) con dati XML per generare documenti PDF. È inoltre possibile utilizzare Comunicazioni per combinare, ridisporre e integrare documenti PDF e XDP e ottenere informazioni sui documenti PDF.

Oltre alle operazioni precedentemente menzionate, è possibile utilizzare i font inclusi nei font di Cloud Service o personalizzati (font approvati dall’organizzazione) per eseguire il rendering dei documenti PDF generati. Puoi utilizzare il progetto di sviluppo del Cloud Service per aggiungere font personalizzati all’ambiente del Cloud Service.

## Comportamento dei documenti PDF

È possibile [incorporare un font](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) a un documento PDF. Quando un font è incorporato, il documento PDF appare identico in tutte le piattaforme. Utilizza i font incorporati per garantire un aspetto coerente. Quando un font non è incorporato, il rendering del font dipende dalle impostazioni di rendering dei client visualizzatore di PDF come Acrobat o Acrobat Reader. Se il font è disponibile nel computer client, PDF utilizza il font specificato, altrimenti viene eseguito il rendering di PDF con un font di fallback predefinito.

## Aggiungi font personalizzati al tuo ambiente Forms as a Cloud Service {#custom-fonts-cloud-service}

Per aggiungere font personalizzati all’ambiente del Cloud Service:

1. Imposta e apri la [progetto di sviluppo locale](setup-local-development-environment.md). È possibile utilizzare qualsiasi IDE desiderato.
1. Nella struttura di cartelle di livello superiore del progetto, crea una cartella (modulo) per salvare i font personalizzati e aggiungere font personalizzati alla cartella. Ad esempio, fonts/src/main/resources
   ![Cartella Font](assets/fonts.png)

1. Apri il file pom.xml del modulo dei font del progetto di sviluppo.
1. Aggiungi il plugin jar al file pom:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
           </archive>
       </configuration>
   </plugin>
   ```


1. Aggiungi il `<Font-Archive-Version>` voce manifest del file .pom e imposta il valore della versione a 1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   <addDefaultEntries/>
                   <addDefaultImplementationEntries/>
               </manifest>
               <manifestEntries>
                   <Font-Archive-Version>1</Font-Archive-Version>
                   <Font-Archive-Contents>/</Font-Archive-Contents>
               </manifestEntries> 
           </archive>
       </configuration>
   </plugin>
   ```

1. Aggiungi la cartella dei font a `<modules>` elencati nel file pom. Esempio:

   ```xml
   <modules>
       <module>all</module>
       <module>core</module>
       <module>ui.frontend</module>
       <module>ui.apps</module>
       <module>ui.apps.structure</module>
       <module>ui.config</module>
       <module>ui.content</module>
       <module>it.tests</module>
       <module>dispatcher</module>
       <module>dispatcher.ams</module>
       <module>dispatcher.cloud</module>
       <module>ui.tests</module>
       <module>fonts</module>
   </modules>
   ```

   La cartella dei font contiene tutti i font personalizzati.

1. Archivia il codice aggiornato e [eseguire la pipeline](/help/implementing/cloud-manager/deploy-code.md) per distribuire i font nell’ambiente di Cloud Service.

1. (Facoltativo) Apri il prompt dei comandi, accedi alla cartella del progetto locale ed esegui il comando sottostante. Il comando contiene i font in un file .jar insieme alle informazioni pertinenti. Puoi usare il file .jar per aggiungere font personalizzati a un ambiente di sviluppo locale di un Cloud Service Forms.

   ```shell
   mvn clean install
   ```

## Aggiungi font personalizzati al tuo ambiente di sviluppo del Cloud Service Forms locale {#custom-fonts-cloud-service-sdk}

1. Avvia l&#39;ambiente di sviluppo locale.
1. Passa a `<aem install directory>/crx-quickstart/install` cartella.
1. Posiziona il `<jar file contaning custom fonts and relevant deployment code>.jar` nella cartella di installazione. Se non disponi del file .jar, esegui i passaggi elencati in [Aggiungi font personalizzati al tuo ambiente Forms as a Cloud Service](#custom-fonts-cloud-service) per generare il file.
1. Esegui il [ambiente SDK basato su docker](setup-local-development-environment.md#docker-microservices)


   >[!NOTE]
   >
   >Ogni volta che distribuisci un file .jar di font personalizzati aggiornati nell’ambiente di sviluppo locale, riavvia l’ambiente SDK basato su docker.