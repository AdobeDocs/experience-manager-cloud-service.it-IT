---
title: Aggiungere utenti e ruoli - Requisiti
description: Aggiungere utenti e ruoli - Requisiti
translation-type: tm+mt
source-git-commit: 2c21414edd6c3178d05c818d2bf57aa152b5956b
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 6%

---


# Aggiungere utenti e ruoli {#add-users-roles}


Molte funzionalità in [!UICONTROL Cloud Manager] richiedono autorizzazioni specifiche per funzionare.

[!UICONTROL Cloud ] Manager definisce attualmente quattro ruoli per gli utenti che determinano la disponibilità di funzionalità specifiche:

* Business Owner (Proprietario)
* Program Manager (Responsabile programma)
* Deployment Manager (Responsabile implementazione)
* Developer (Sviluppatore)

>[!CAUTION]
>
>Per utilizzare [!UICONTROL Cloud Manager], è necessario disporre di un Adobe ID e del contesto di prodotto di Adobe Experience Manager as a Cloud Service.

## Definizioni dei ruoli {#role-definitions}

>[!NOTE]
>
>La figura Sviluppatore in Admin Console non è correlata al ruolo Sviluppatore in [!UICONTROL Cloud Manager].

La tabella seguente riepiloga i ruoli:

| [!UICONTROL Ruoli ] di Cloud Manager | Descrizione |
|--- |--- |
| Business Owner (Proprietario) | Responsabile della definizione dei KPI, dell’approvazione delle implementazioni di produzione e dell’override di importanti errori a 3 livelli. |
| Program Manager (Responsabile programma) | Utilizza [!UICONTROL Cloud Manager] per eseguire la configurazione del team, esaminare lo stato e visualizzare i KPI. Può approvare importanti errori a 3 livelli. |
| Deployment Manager (Responsabile implementazione) | Gestisce le operazioni di distribuzione. Utilizza [!UICONTROL Cloud Manager] per eseguire distribuzioni di stage/produzione. È possibile modificare le pipeline CI/CD. Può approvare importanti errori a 3 livelli. È possibile accedere all’archivio Git. |
| Developer (Sviluppatore) | Sviluppa e verifica il codice personalizzato dell’applicazione. Utilizza principalmente [!UICONTROL Cloud Manager] per visualizzare lo stato. Può accedere all’archivio Git per il commit del codice. |
| Autore del contenuto | In genere non interagisce con [!UICONTROL Cloud Manager]. Per accedere ad AEM puoi utilizzare il commutatore di programma [!UICONTROL Cloud Manager] (dopo aver navigato da [!UICONTROL Experience Cloud]). |

## Profilo del prodotto di integrazione {#integration-product-profile}

Oltre a quanto sopra, Cloud Manager creerà automaticamente un profilo di prodotto denominato &quot;Integrazioni - Cloud Service&quot;. Questo profilo di prodotto viene utilizzato per le integrazioni tra Adobe Experience Manager e altri prodotti Adobe. Questo profilo di prodotto **non deve essere eliminato**. Se elimini accidentalmente questo profilo, dovrà essere ricreato manualmente. Il nome visualizzato per questo profilo **deve essere** `CM_CS_DEFAULT`.
