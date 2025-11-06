---
title: Come risolvere i problemi di installazione e configurazione per l’ambiente AEM Forms as a Cloud Service?
description: Risoluzione dei problemi di installazione e configurazione dell’ambiente AEM Forms as a Cloud Service.
contentOwner: khsingh
feature: Adaptive Forms
role: User
exl-id: 249ec8f2-4176-428a-bfcf-80b381ec7263
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 1%

---

# Configurazione {#installation-and-configuration}

Durante la configurazione di un ambiente Cloud Service, si possono verificare alcuni dei seguenti problemi:

## Opzione Forms non disponibile

Opzione **[!UICONTROL Forms]** non disponibile nella pagina **[!UICONTROL Navigazione]**.

![Opzione Forms non disponibile](assets/installation-configuration-forms-option-unavailable-troubleshooting.png)

Per abilitare l&#39;opzione **[!UICONTROL Forms]**:

1. Accedi a [Cloud Manager](https://experience.adobe.com/)
1. Individua il programma e fai clic sull&#39;icona ![L&#39;opzione Forms non è disponibile](assets/Smock_Edit_18_N.svg). Viene visualizzata la pagina Modifica programma del programma.
1. Apri la scheda **[!UICONTROL Soluzioni e componenti aggiuntivi]**.
1. Seleziona l&#39;opzione **[!UICONTROL Forms]** e fai clic su **[!UICONTROL Salva]**.

   ![Selezionare l&#39;opzione Forms](assets/installation-configuration-select-forms-option.png)

1. [Crea](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=it#how-to-use) e [esegui](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=it) entrambe le pipeline di produzione e non di produzione.

Dopo la generazione e la distribuzione della pipeline, l&#39;opzione **[!UICONTROL Forms]** nella pagina **[!UICONTROL Navigazione]**.

<!--  
## Environment creation fails {#environment-creation-fails}

Users are unable to create an [!DNL AEM Forms] as a Cloud Service environment. The environment creation fails after running for some time.

A missing profile can lead to environment creation failure. Check that the profile exists in Admin Console. If the profile does not exist, perform the following steps to create the profile:

1. Log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not any other ID or Federated ID to login.
1. Click the **[!UICONTROL Automated Forms Conversion Service]** option.
1. Click **[!UICONTROL New Profile]** in the Products tab.
1. Specify Name, Display Name, and Description for the profile. Click **[!UICONTROL Done]**. A profile is created.

If the profile exists and issues still persist, contact Adobe Support. -->

## La pipeline di compilazione non riesce {#build-pipeline-fails}

Gli utenti non possono eseguire la pipeline di build. La pipeline ha esito negativo dopo un certo periodo di tempo dall’esecuzione.

Per risolvere il problema, apri Cloud Manager, seleziona l&#39;opzione **[!UICONTROL Aggiorna]** per il tuo ambiente ed esegui la pipeline.


## I bundle non sono nello stato attivo {#bundles-inactive-state}

Per risolvere il problema, effettuare le seguenti operazioni:

1. Avvia AEM e attendi che venga avviato completamente fino a quando tutti i bundle non sono attivi.
1. Arresta AEM (Ctrl + C).
1. Inserire il file Forms `.far` nella cartella di installazione.
1. Riavvia il server AEM.