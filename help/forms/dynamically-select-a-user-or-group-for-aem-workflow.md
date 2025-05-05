---
title: Come selezionare gli utenti nel flusso di lavoro AEM?
description: Scopri come selezionare un utente o un gruppo per un flusso di lavoro  [!DNL AEM Forms]  in fase di esecuzione.
content-type: troubleshooting
topic-tags: publish
feature: Adaptive Forms
role: User
hide: true
hidefromtoc: true
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# Selezione dinamica di utenti o gruppi nel flusso di lavoro AEM {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

Scopri come selezionare un utente o un gruppo per un flusso di lavoro [!DNL AEM Forms] in fase di esecuzione.

Nelle organizzazioni di grandi dimensioni è necessario selezionare dinamicamente gli utenti per un processo. Ad esempio, selezionando un agente sul campo per servire un cliente in base alla vicinanza dell’agente al cliente. In questo caso, l’agente viene selezionato in modo dinamico.

Assegna l&#39;attività e [!DNL Adobe Sign] passaggi di [flussi di lavoro incentrati su Forms in OSGi](aem-forms-workflow.md) forniscono opzioni per la selezione dinamica di un utente. Puoi utilizzare i bundle ECMAScript o OSGi per selezionare in modo dinamico un assegnatario per il passaggio Assegna attività o per selezionare i firmatari per il passaggio Firma documento.

## Utilizzare ECMAScript per selezionare dinamicamente un utente o un gruppo {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript è un linguaggio di script. Viene utilizzato per applicazioni server e scripting lato client. Per selezionare dinamicamente un utente o un gruppo utilizzando ECMAScript, effettuare le seguenti operazioni:

1. Apri CRXDE Lite. URL: `https://'[server]:[port]'/crx/de/index.jsp`
1. Creare un file con estensione .ecma nel percorso seguente. Se il percorso (struttura del nodo) non esiste, crealo:

   * (Percorso per il passaggio Assegna attività) `/apps/fd/dashboard/scripts/participantChooser`
   * (Percorso per passaggio firma) `/apps/fd/workflow/scripts/adobesign`

1. Aggiungere al file .ecma ECMAScript, che ha la logica per selezionare dinamicamente un utente. Fare clic su **[!UICONTROL Salva tutto]**.

   Per gli script di esempio, vedere [Esempi di ECMAScript per la selezione dinamica di un utente o di un gruppo](dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group).

1. Aggiungi il nome visualizzato dello script. Questo nome viene visualizzato nei passaggi del flusso di lavoro. Per specificare il nome:

   1. Espandere il nodo di script, fare clic con il pulsante destro del mouse sul nodo **[!UICONTROL jcr:content]** e scegliere **[!UICONTROL Mixin]**.
   1. Aggiungi la proprietà `mix:title` nella finestra di dialogo Modifica mixin e fai clic su **OK**.
   1. Aggiungi la seguente proprietà al nodo jcr:content dello script:

      | Nome | Tipo | Valore |
      |--- |--- |--- |
      | jcr:title | Stringa | Specifica il nome dello script. Ad esempio, scegli l’agente di campo più vicino. Questo nome viene visualizzato nei passaggi Assegna attività e Firma documento. |

   1. Fare clic su **Salva tutto**. Lo script diventa disponibile per la selezione nei componenti del flusso di lavoro AEM.

      ![script](assets/script.png)

### Esempi di ECMAScript per scegliere dinamicamente un utente o un gruppo {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

Nell&#39;esempio seguente ECMAScript viene selezionato in modo dinamico un assegnatario per il passaggio Assegna attività. In questo script, viene selezionato un utente in base al percorso del payload. Prima di utilizzare questo script, accertati che tutti gli utenti menzionati nello script siano presenti nell’AEM. Se gli utenti menzionati nello script non esistono nell’AEM, il relativo processo può non riuscire.

```javascript
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

Nell&#39;esempio seguente ECMAScript viene selezionato in modo dinamico un assegnatario per il passaggio [!DNL Adobe Sign]. Prima di utilizzare lo script seguente, verifica che le informazioni utente (indirizzi e-mail e numeri di telefono) menzionate nello script siano corrette. Se le informazioni utente menzionate nello script non sono corrette, il processo correlato potrebbe non riuscire.

>[!NOTE]
>
>Quando si utilizza ECMAScript per [!DNL Adobe Sign], lo script deve trovarsi nell&#39;archivio crx in /apps/fd/workflow/scripts/adobesign/ e deve disporre di una funzione denominata getAdobeSignRecipients per restituire un elenco degli utenti.

```javascript
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## Utilizzare l’interfaccia Java per scegliere dinamicamente un utente o un gruppo {#use-java-interface-to-dynamically-choose-a-user-or-group}

È possibile utilizzare l&#39;interfaccia Java [RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) per scegliere in modo dinamico un utente o un gruppo per [!DNL Adobe Sign] e assegnare i passaggi dell&#39;attività. È possibile creare un bundle OSGi che utilizza l&#39;interfaccia Java [RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) e distribuirlo al server [!DNL AEM Forms]. Rende l&#39;opzione disponibile per la selezione nei componenti Assegna attività e [!DNL Adobe Sign] del flusso di lavoro AEM.

Sono necessari [[!DNL AEM Forms] file JAR dell&#39;SDK client](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it) e [file JAR granite](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) per compilare l&#39;esempio di codice elencato di seguito. Aggiungi questi file jar come dipendenze esterne al progetto del bundle OSGi. Puoi utilizzare qualsiasi IDE Java per creare un bundle OSGi. La procedura seguente descrive come utilizzare Eclipse per creare un bundle OSGi:

1. Aprire Eclipse IDE. Passa a **[!UICONTROL File]**> **[!UICONTROL Nuovo progetto]**.
1. Nella schermata della procedura guidata, seleziona **[!UICONTROL Progetto Maven]** e fai clic su **[!UICONTROL Avanti]**.
1. Nel nuovo progetto Maven, mantieni le impostazioni predefinite e fai clic su **[!UICONTROL Avanti]**. Seleziona un archetipo e fai clic su **[!UICONTROL Avanti]**. Ad esempio, maven-archetype-quickstart. Specifica **[!UICONTROL ID gruppo]**, **[!UICONTROL ID artefatto]**, **[!UICONTROL versione]** e **[!UICONTROL pacchetto]** per il progetto, quindi fai clic su **[!UICONTROL Fine]**. Il progetto viene creato.
1. Apri il file pom.xml per la modifica e sostituisci tutto il contenuto del file con quanto segue:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. Aggiungere il codice sorgente che utilizza l&#39;interfaccia Java [RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) per scegliere in modo dinamico un utente o un gruppo per il passaggio Assegna attività. Per il codice di esempio, vedere [Esempio per la scelta dinamica di un utente o di un gruppo tramite l&#39;interfaccia Java](#-sample-scripts-for).
1. Apri un prompt dei comandi e passa alla directory contenente il progetto del bundle OSGi. Utilizza il seguente comando per creare il bundle OSGi:

   `mvn clean install`

1. Carica il bundle in un server [!DNL AEM Forms]. È possibile utilizzare Gestione pacchetti AEM per importare il bundle nel server [!DNL AEM Forms].

Una volta importato il bundle, l’opzione per scegliere l’interfaccia Java per selezionare dinamicamente un utente o un gruppo diventa disponibile in per i passaggi di Adobe Sign e Assegna attività.

### Esempio di codice Java per scegliere dinamicamente un utente o un gruppo {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

Il codice di esempio seguente sceglie in modo dinamico un assegnatario per il passaggio di Adobe Sign. Il codice viene utilizzato in un bundle OSGi. Prima di utilizzare il codice riportato di seguito, verifica che le informazioni utente (indirizzi e-mail e numeri di telefono) indicate nel codice siano corrette. Se le informazioni utente menzionate nel codice non sono corrette, il processo correlato potrebbe non riuscire.

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```

>[!MORELIKETHIS]
>
>* [Utilizza il flusso di lavoro di AEM Forms per l&#39;automazione dei processi aziendali](/help/forms/aem-forms-workflow.md)