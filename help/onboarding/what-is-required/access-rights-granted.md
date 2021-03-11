---
title: Diritti Di Accesso Concessi - Requisiti
description: Diritti Di Accesso Concessi - Requisiti
translation-type: tm+mt
source-git-commit: 4904d7728befd3562940b35c7d44dbf9cae87fee
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 11%

---


# Diritti di accesso concessi {#access-rights-granted}

Adobe creerà un identificatore **Organizzazione** per la società in Adobe Identity Management System (IMS), in cui è possibile gestire tutti gli utenti e le relative autorizzazioni. Ogni utente, che deve essere membro di questa organizzazione e avrà accesso a uno qualsiasi dei servizi [!UICONTROL Experience Cloud], dovrà disporre del proprio **Adobe ID**.

## Tipi di identità utente {#user-identity-types}

Per iniziare a utilizzare un Adobe ID, visita [Manage Adobe Identity Types](https://helpx.adobe.com/enterprise/using/identity.html) per istruzioni dettagliate su come ottenere un Adobe ID utilizzando uno dei tipi di identità disponibili.

## Utenti e ruoli {#users-and-roles}

Una volta creata l’organizzazione per la società, l’amministratore designato vi verrà aggiunto come primo membro. Per impostazione predefinita, all’amministratore vengono assegnate le autorizzazioni di amministratore, il [!UICONTROL prodotto] **AEM Managed Services** e uno o più [!UICONTROL profili di prodotto] **Cloud Manager**.

1. Una volta che l’amministratore di sistema ti concede l’accesso a Cloud Manager, riceverai un’e-mail che ti porterà alla pagina di accesso di Cloud Manager, accessibile anche tramite [Adobe Experience Cloud](https://my.cloudmanager.adobe.com/).

1. Dalla pagina di destinazione di Cloud Manager, fai clic su **Gestisci accesso**.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

1. Dopo aver fatto clic su **Gestisci accesso**, passa a **Admin Console** da dove puoi gestire i ruoli utente o le autorizzazioni per Cloud Manager.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin1.png)

   Dall’Admin Console è possibile eseguire attività SysAdmin quali:
   * [Gestione dei ruoli](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-roles)
   * [Gestione dell’accesso all’istanza di authoring](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-access-aem)

>[!NOTE]
>Per ulteriori informazioni sugli utenti e le definizioni dei ruoli in Cloud Manager, visita la sezione [Utenti e ruoli](#users-roles) .

Con questi diritti concessi, il tuo amministratore è ora configurato con un single sign-on (utilizzando Adobe ID) per accedere ai servizi [!UICONTROL Experience Cloud], accedere agli ambienti cloud AEM e utilizzare [!UICONTROL Cloud Manager].

## Utenti e ruoli {#users-roles}

Molte funzionalità in [!UICONTROL Cloud Manager] richiedono autorizzazioni specifiche per funzionare.

[!UICONTROL Cloud ] Manager definisce attualmente quattro ruoli per gli utenti che determinano la disponibilità di funzionalità specifiche:

* Business Owner (Proprietario)
* Program Manager (Responsabile programma)
* Deployment Manager (Responsabile implementazione)
* Developer (Sviluppatore)

>[!CAUTION]
>
>Per utilizzare [!UICONTROL Cloud Manager], è necessario disporre di un Adobe ID e di Adobe Experience Manager come contesto di prodotto Cloud Service.

### Definizioni dei ruoli {#role-definitions}

>[!NOTE]
>
>La persona sviluppatore in Admin Console non è correlata al ruolo Sviluppatore in [!UICONTROL Cloud Manager].

La tabella seguente riepiloga i ruoli:

| [!UICONTROL Ruoli ] di Cloud Manager | Descrizione |
|--- |--- |
| Business Owner (Proprietario) | Responsabile della definizione dei KPI, dell’approvazione delle implementazioni di produzione e dell’override di importanti errori a 3 livelli. |
| Program Manager (Responsabile programma) | Utilizza [!UICONTROL Cloud Manager] per eseguire la configurazione del team, esaminare lo stato e visualizzare i KPI. Può approvare importanti errori a 3 livelli. |
| Deployment Manager (Responsabile implementazione) | Gestisce le operazioni di distribuzione. Utilizza [!UICONTROL Cloud Manager] per eseguire distribuzioni di stage/produzione. È possibile modificare le pipeline CI/CD. Può approvare importanti errori a 3 livelli. È possibile accedere all’archivio Git. |
| Developer (Sviluppatore) | Sviluppa e verifica il codice personalizzato dell’applicazione. Utilizza principalmente [!UICONTROL Cloud Manager] per visualizzare lo stato. Può accedere all’archivio Git per il commit del codice. |
| Autore del contenuto | In genere non interagisce con [!UICONTROL Cloud Manager]. Per accedere a AEM può essere utilizzato il commutatore di programma [!UICONTROL Cloud Manager] (dopo aver navigato da [!UICONTROL Experience Cloud]). |

### Profilo del prodotto di integrazione {#integration-product-profile}

Oltre a quanto sopra, Cloud Manager creerà automaticamente un profilo di prodotto denominato &quot;Integrazioni - Cloud Service&quot;. Questo profilo di prodotto viene utilizzato per le integrazioni tra Adobe Experience Manager e altri prodotti Adobe. Questo profilo di prodotto **non deve essere eliminato**. Se elimini accidentalmente questo profilo, dovrà essere ricreato manualmente. Il nome visualizzato per questo profilo **deve essere** `CM_CS_DEFAULT`.

