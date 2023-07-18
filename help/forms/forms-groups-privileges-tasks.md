---
title: Integrato [!DNL AEM Forms] Gruppi as a Cloud Service
description: Elenco dei gruppi di utenti e delle autorizzazioni predefiniti assegnati a ciascun gruppo
exl-id: bd66ce92-14d9-47fe-b5d3-022e3e468d25
source-git-commit: 8ac35abd1335b4e31a6dc0d8812cc9df333e69a4
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 9%

---

# Gruppi e autorizzazioni {#aem-forms-on-osgi-groups-and-privileges}

È possibile [creare gruppi](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) e assegnare criteri e [utenti](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) ai gruppi. Questi criteri controllano le autorizzazioni degli utenti che fanno parte del gruppo.

Una volta effettuata la configurazione [!DNL AEM Forms] as a Cloud Service, i gruppi elencati nella tabella seguente, ad esempio [!DNL forms-users] e forms-power-user, sono automaticamente disponibili per l&#39;assegnazione:

<table>
 <tbody>
  <tr>
   <td>Gruppo</td> 
   <td>Autorizzazioni</td> 
  </tr>
  <tr>
   <td>[!DNL forms-users] <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Creare, visualizzare in anteprima, pubblicare e inviare Forms adattivo</li> 
    <!-- <li>Create, preview, and publish interactive communications and document fragments</li> -->
     <li>Caricare risorse in un’istanza AEM</li> 
     <li>Creare temi</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>[!DNL forms-power-user]</td> 
   <td>
    <ul> 
     <li>Create, preview, publish, and submit Adaptive Forms</li> 
     <li>Create, preview, and publish interactive communications and document fragments</li> 
     <li>Create scripts for Adaptive Forms using code editor</li> 
     <li>Upload assets including scripts</li> 
     <li>Create themes</li> 
     <li>Import packages containing XDP</li> 
    </ul> </td> 
  </tr>
 <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>Review submissions</li> 
     <li>Approve or reject submissions</li> 
    </ul> </td> 
  </tr> -->
  <tr>
   <td>[!DNL template-authors] <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Creazione e anteprima di Adaptive Forms <!-- or interactive communications --> modelli</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>[!DNL fdm-authors]</p> </td> 
   <td>
    <ul> 
     <li>Creare e modificare un modello di dati modulo</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Access Correspondence Management letters or interactive communications using Agent UI</li> 
    </ul> </td> 
  </tr> --> 
  <!-- <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> -->
    <!-- <li>Create an inbox application</li>  -->
    <!-- <li>Create a workflow model</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL workflow-users]</td> 
   <td>
    <ul> 
     <li>Use AEM inbox applications<br /> -->
     <!-- 
     <strong>Note: </strong>You must have cm-agent-users and [!DNL workflow-users] group assignments to access Interactive Communications Agent UI in AEM inbox.</li>  -->
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL fd-administrators]</td> 
   <td>
    <ul> 
     <!-- <li>Configure PDF Generator</li> --> 
     <!-- <li>Configure Watched folder</li> -->
     <li>Gestire le applicazioni del flusso di lavoro</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

## Consulta anche

* [Onboarding in un ambiente di Cloud Service](/help/forms/setup-forms-cloud-service.md)
* [Configurare un ambiente di sviluppo locale](/help/forms/setup-local-development-environment.md)
* [Migrazione da AEM 6.5 Forms a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [Creare un modulo adattivo indipendente](/help/forms/creating-adaptive-form-core-components.md)
* [Aggiungere un modulo adattivo alla pagina di AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)



