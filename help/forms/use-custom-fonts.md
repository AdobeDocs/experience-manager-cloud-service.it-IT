---
title: 'Usa font personalizzati '
description: 'Usa font personalizzati '
source-git-commit: 10fe582edc8ffc93ea3f8564a64259882bba1d6f
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Usa font personalizzati

**La documentazione sulle comunicazioni di Cloud Service è disponibile in versione beta**

È possibile utilizzare Forms as a Cloud Service Communications per combinare un modello XDP, un documento PDF basato su XDP o un modulo Acrobat (AcroForm) con dati XML per generare documenti PDF. È possibile utilizzare i font inclusi nel Cloud Service o i font personalizzati (font approvati dall’organizzazione) per eseguire il rendering dei documenti PDF generati. Puoi utilizzare il progetto di sviluppo del Cloud Service per aggiungere font personalizzati all’ambiente del Cloud Service.

## Comportamento dei documenti PDF

È possibile [incorporare un font](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/#tag/PDFOutputOptions) a un documento PDF. Quando un font è incorporato, il documento PDF appare identico su tutte le piattaforme. Utilizzava un font incorporato per garantire un aspetto e un aspetto coerenti. Quando un font non è incorporato, il rendering del font dipende dalle impostazioni di rendering del client di visualizzazione di PDF. Se il font è disponibile nel computer client, PDF utilizza il font specificato, altrimenti il font utilizzato per il rendering di PDF sarà un font di fallback.

## Aggiungi font personalizzati al tuo ambiente Forms as a Cloud Service

Per aggiungere font personalizzati all’ambiente del Cloud Service:

1. Imposta e apri il progetto di sviluppo locale. È possibile utilizzare qualsiasi IDE desiderato.
1. Nella struttura di cartelle di livello superiore del progetto, crea una cartella per salvare i font personalizzati e aggiungere font personalizzati alla cartella. Ad esempio, fonts/src/main/resources
   ![Cartella Font](assets/fonts.png)

1. Apri il file pom.xml di primo livello del progetto di sviluppo.
1. Aggiungi `<Font-Archive-Version>` voce manifest al file .pom e imposta il valore della versione a 1:

   ```xml
   <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-jar-plugin</artifactId>
       <version>3.1.2</version>
       <configuration>
           <archive>
               <manifest>
                   </addDefaultEntries>
                   </addDefaultImplementationEntries>
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

1. Archivia il codice aggiornato e [eseguire la pipeline](/help/implementing/cloud-manager/deploy-code.md) per distribuire i font nell’ambiente di Cloud Service.
