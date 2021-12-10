---
title: 'Risoluzione dei problemi di installazione e configurazione  '
seo-title: Troubleshooting installation and configuration
description: Risoluzione dei problemi di installazione e configurazione
seo-description: Troubleshooting installation and configuration
contentOwner: khsingh
exl-id: 249ec8f2-4176-428a-bfcf-80b381ec7263
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Configurazione {#installation-and-configuration}

Durante la configurazione di un ambiente di Cloud Service è possibile riscontrare alcuni dei seguenti problemi:

## Opzione Forms non disponibile

La **[!UICONTROL Forms]** l’opzione non è disponibile nel **[!UICONTROL Navigazione]** pagina.

![Opzione Forms non disponibile](assets/installation-configuration-forms-option-unavailable-troubleshooting.png)

Per abilitare **[!UICONTROL Forms]** opzione:

1. Accedi a [Cloud Manager](https://experience.adobe.com/)
1. Individua il programma e fai clic sul pulsante ![Opzione Forms non disponibile](assets/Smock_Edit_18_N.svg) icona. Viene visualizzata la pagina Modifica programma per il programma.
1. Apri **[!UICONTROL Soluzioni e componenti aggiuntivi]** scheda .
1. Seleziona la **[!UICONTROL Forms]** e fai clic su **[!UICONTROL Salva]**.

   ![Selezionare l’opzione Forms](assets/installation-configuration-select-forms-option.png)
1. [Crea](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use) e [eseguire](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) oleodotti di produzione e di non produzione.

Dopo la creazione e l’implementazione della pipeline, l’ **[!UICONTROL Forms]** l&#39;opzione **[!UICONTROL Navigazione]** pagina.

<!--  
## Environment creation fails {#environment-creation-fails}

Users are unable to create an [!DNL AEM Forms] as a Cloud Service environment. The environment creation fails after running for some time.

A missing profile can lead to environment creation failure. Check that the profile exists in Admin Console. If the profile does not exist, perform the following steps to create the profile:

1. Log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not any other ID or Federated ID to login.
1. Click the **[!UICONTROL Automated Forms Conversion Service]** option.
1. Click **[!UICONTROL New Profile]** in the Products tab.
1. Specify Name, Display Name, and Description for the profile. Click **[!UICONTROL Done]**. A profile is created.

If the profile exists and issues still persist, contact Adobe Support. -->

## Errore di creazione della pipeline {#build-pipeline-fails}

Gli utenti non possono eseguire la pipeline di compilazione. La pipeline non riesce dopo essere stata eseguita per un certo periodo di tempo.

Per risolvere il problema, apri Cloud Manager, seleziona la **[!UICONTROL Aggiorna]** per il tuo ambiente ed esegui la pipeline.
