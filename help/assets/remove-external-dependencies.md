---
title: Rimuovere le dipendenze esterne per le installazioni esistenti
description: Rimuovere le dipendenze esterne per le installazioni esistenti
feature: Integrations
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
source-git-commit: b71a78696d4b347c97b077d84b455f53a1747a07
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 17%

---

# Rimuovere le dipendenze esterne per le installazioni esistenti {#remove-external-depedencies}

Adobe consiglia di eseguire i passaggi di configurazione per le installazioni di connettori avanzate esistenti per Workfront per rimuovere le dipendenze dai punti di distribuzione Hoodoo.

>[!NOTE]
>
>Esegui i passaggi di configurazione solo se hai installato il connettore avanzato per Workfront prima di marzo 2022. A partire da marzo 2022, non vi sono dipendenze dai punti di distribuzione di Hoodoo per le nuove installazioni di connettori migliorati per Workfront.

Per rimuovere le dipendenze esterne:

1. Rimuovi dalla pagina padre la seguente configurazione dell&#39;archivio Hoodoo `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. Rimuovi la seguente configurazione del server dal `settings.xml` file, disponibile all&#39;indirizzo `./cloudmanager/maven/settings.xml`:

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

1. Esegui il [nuovi passaggi di installazione](workfront-connector-install.md).
