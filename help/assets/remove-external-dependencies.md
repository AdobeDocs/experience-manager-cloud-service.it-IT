---
title: Rimuovere le dipendenze esterne per le installazioni esistenti
description: Rimuovere le dipendenze esterne per le installazioni esistenti
feature: Workfront Integrations and Apps
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
role: Admin
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 17%

---

# Rimuovere le dipendenze esterne per le installazioni esistenti {#remove-external-depedencies}

Adobe consiglia di eseguire i passaggi di configurazione per le installazioni dei connettori avanzati esistenti affinché Workfront rimuova le dipendenze dai punti di distribuzione Hoodoo.

>[!NOTE]
>
>Esegui i passaggi di configurazione solo se hai installato il connettore avanzato per Workfront prima di marzo 2022. Non vi sono dipendenze dai punti di distribuzione Hoodoo per le nuove installazioni di connettori avanzati per Workfront a partire da marzo 2022.

Per rimuovere le dipendenze esterne:

1. Rimuovi la seguente configurazione dell&#39;archivio Hoodoo dall&#39;elemento padre `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. Rimuovere la seguente configurazione del server dal file `settings.xml`, disponibile in `./cloudmanager/maven/settings.xml`:

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

1. Eseguire i [nuovi passaggi dell&#39;installazione](workfront-connector-install.md).
