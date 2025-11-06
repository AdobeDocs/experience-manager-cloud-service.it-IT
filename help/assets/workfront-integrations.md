---
title: Integrazione di [!DNL Experience Manager Assets] con  [!DNL Adobe Workfront]
description: Introduzione all'integrazione tra [!DNL Assets] e [!DNL Workfront]
role: Admin, Leader, Developer
feature: Workfront Integrations and Apps
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 13%

---

# [!DNL Adobe Experience Manager] come integrazione [!DNL Cloud Service] [!DNL Assets] con [!DNL Adobe Workfront] {#assets-integration-overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Workfront] è un&#39;applicazione per la gestione dell&#39;intero ciclo di vita del lavoro in un&#39;unica posizione. L’integrazione tra [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] consente alle organizzazioni di migliorare la velocità dei contenuti e il time-to-market, grazie a un collegamento intrinseco tra il lavoro e la gestione delle risorse digitali. Nel contesto di gestione del proprio lavoro in Workfront, gli utenti possono accedere ai documenti e alle immagini necessari.

Le offerte di Adobe per [integrare [!DNL Workfront] e [!DNL Adobe Experience Manager Assets] in modo nativo (supporto di Assets Essentials e Assets as a Cloud Service)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html?lang=it).

Con l’integrazione nativa di Experience Manager, puoi:

* Configurazione rapida dell&#39;integrazione all&#39;interno di Workfront.

* Creazione automatica di cartelle collegate tra Workfront e Experience Manager.

* Sincronizza facilmente i metadati per le risorse collegate esistenti.

* Aggiorna automaticamente i metadati del progetto quando vengono modificati in Workfront.

* Collega in modo semplice più archivi Experience Manager Assets a un ambiente Workfront o più ambienti Workfront a un archivio Experience Manager Assets tra gli ID organizzazione.


## Connettore avanzato Adobe Workfront per Experience Manager {#enhanced-connector-information}


A giugno 2022, Adobe ha rilasciato una nuova integrazione nativa per la connessione di Workfront con Adobe Experience Manager Assets as a Cloud Service. Questa integrazione è diventata il metodo richiesto per collegare queste due soluzioni. Qualsiasi nuova implementazione futura del connettore avanzato (versione 1.9.8 e successive) per collegare Workfront ad AEM Assets as a Cloud Service è bloccata. Per ulteriori informazioni su come configurare questa integrazione, vedere [Configurare l&#39;integrazione Experience Manager Assets as a Cloud Service](workfront-connector-configure.md).

>[!NOTE]
>
>Adobe non supporta l’utilizzo in parallelo del connettore avanzato Workfront for Experience Manager e dell’integrazione Experience Manager.

Per le installazioni precedenti a giugno 2022, di seguito sono riportati alcuni punti da considerare per la distribuzione e la configurazione di [!DNL Adobe Workfront for Experience Manager enhanced connector]:

* Adobe richiede la distribuzione e la configurazione di [!DNL Adobe Workfront for Experience Manager enhanced connector] solo tramite partner certificati o [!DNL Adobe Professional Services]. Se distribuita e configurata senza un partner certificato o [!DNL Adobe Professional Services], non è supportata da Adobe.
* Adobe potrebbe rilasciare aggiornamenti a [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] che rendono ridondante questo connettore; in tal caso, i clienti potrebbero dover passare dall&#39;utilizzo di questo connettore.
* Adobe supporta le versioni migliorate del connettore 1.7.4 e successive. Le versioni precedenti prerelease e personalizzate non sono supportate. Per verificare la versione del connettore avanzato, vedere il passaggio 5(a) delle [istruzioni di installazione del connettore avanzato](workfront-connector-install.md).
* Consulta [Esame di certificazione partner per il connettore avanzato Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Per informazioni sull&#39;esame, vedere [Guida all&#39;esame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).