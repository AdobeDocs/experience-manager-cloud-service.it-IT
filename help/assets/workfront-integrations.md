---
title: '[!DNL Experience Manager Assets] integrazione con [!DNL Adobe Workfront]'
description: Introduzione all’integrazione tra [!DNL Assets] e [!DNL Workfront]
role: Admin, Leader, Architect
feature: Workfront Integrations and Apps
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] integrazione con [!DNL Adobe Workfront] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Workfront] è un&#39;applicazione per la gestione dell&#39;intero ciclo di vita del lavoro in un&#39;unica posizione. L’integrazione tra [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] consente alle organizzazioni di velocizzare le attività relative ai contenuti e il time-to-market, grazie a un collegamento intrinseco tra il lavoro e la gestione delle risorse digitali. Nel contesto della gestione del proprio lavoro in Workfront, gli utenti possono accedere ai documenti e alle immagini richiesti.

Adobe di offerte a [integrare [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] in modalità nativa (Assets Essentials di supporto e Assets as a Cloud Service)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html).

Con l’integrazione nativa di Experience Manager, puoi:

* Configurazione rapida dell&#39;integrazione all&#39;interno di Workfront.

* Creazione automatica di cartelle collegate tra Workfront e Experience Manager.

* Sincronizza facilmente i metadati per le risorse collegate esistenti.

* Aggiorna automaticamente i metadati del progetto quando vengono modificati in Workfront.

* Collega in modo semplice più archivi Experience Manager Assets a un ambiente Workfront o più ambienti Workfront a un archivio Experience Manager Assets tra gli ID organizzazione.


## Connettore avanzato Adobe Workfront per Experience Manager {#enhanced-connector-information}


A giugno 2022, Adobe ha rilasciato una nuova integrazione nativa per la connessione di Workfront con Adobe Experience Manager Assets as a Cloud Service. Questa integrazione è diventata il metodo richiesto per collegare queste due soluzioni. Qualsiasi nuova implementazione futura del connettore avanzato (versione 1.9.8 e successive) per collegare Workfront ad AEM Assets as a Cloud Service è bloccata. Per ulteriori informazioni su come impostare questa integrazione, consulta [Configurare l’integrazione di Experience Manager Assets as a Cloud Service](workfront-connector-configure.md).

>[!NOTE]
>
>Adobe non supporta l’utilizzo parallelo di Workfront per il connettore avanzato Experience Manager e l’integrazione Experience Manager.

Per le installazioni precedenti a giugno 2022, di seguito sono riportati alcuni punti da considerare per la distribuzione e la configurazione di [!DNL Adobe Workfront for Experience Manager enhanced connector]:

* L’Adobe richiede l’implementazione e la configurazione del [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se implementato e configurato senza un partner certificato o [!DNL Adobe Professional Services], non è supportato da Adobe.
* Adobe può rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono questo connettore ridondante; in tal caso, i clienti potrebbero dover passare dall’utilizzo di questo connettore.
* Adobe supporta le versioni migliorate del connettore 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per verificare la versione del connettore avanzato, vedere il punto 5(a) di [istruzioni per l&#39;installazione del connettore avanzato](workfront-connector-install.md).
* Consulta [Connettore avanzato per la certificazione dei partner per Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedere [Guida all’esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).