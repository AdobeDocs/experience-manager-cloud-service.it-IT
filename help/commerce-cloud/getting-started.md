---
title: Guida introduttiva AEM Commerce come Cloud Service
description: Guida introduttiva AEM Commerce come Cloud Service
translation-type: tm+mt
source-git-commit: 170a6f4f3aa07b9aa917014b7a682ead9ed595c1
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 3%

---


# Guida introduttiva AEM Commerce come Cloud Service {#start}

Per iniziare a utilizzare AEM Commerce come Cloud Service, è necessario eseguire il provisioning del proprio Experience Manager Cloud Service di  con il componente aggiuntivo Commerce Integration Framework (CIF). Il componente aggiuntivo CIF è un modulo aggiuntivo in cima ai [AEM Sites come Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/sites/home.html).

## Onboarding {#onboarding}

L&#39;onboarding per AEM Commerce come Cloud Service è un processo in due fasi:

1. Ottieni AEM Commerce come Cloud Service abilitato e provisioning del componente aggiuntivo CIF
2. Connect AEM Commerce come Cloud Service con l&#39;ambiente di Magenti

Il primo passo è  Adobe. Dovrete fornire informazioni come l&#39;organizzazione IMS, l&#39;URL dell&#39;endpoint GraphQL dell&#39;ambiente di Magento, ecc. come parte del processo di provisioning. Per maggiori informazioni su prezzi e provisioning, contattate il vostro rappresentante commerciale.

Una volta effettuato il provisioning con il componente aggiuntivo CIF, questo verrà applicato a tutti i programmi Cloud Manager esistenti. Se non disponi di un programma Cloud Manager, dovrai crearne uno nuovo. Per ulteriori informazioni, vedere [Configurazione del programma](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

Il secondo passo è self-service per ogni AEM come ambiente Cloud Service. Dopo il provisioning iniziale del componente aggiuntivo CIF, è necessario effettuare alcune configurazioni aggiuntive.

## Collegamento AEM Commerce con Magento {#magento}

Per collegare il componente aggiuntivo CIF e i componenti [](https://github.com/adobe/aem-core-cif-components) AEM CIF di base all&#39;ambiente di Magento, è necessario fornire l&#39;URL dell&#39;endpoint GraphQL Magenti tramite una variabile di ambiente di Cloud Manager. Il nome della variabile è `COMMERCE_ENDPOINT`. È necessario configurare una connessione protetta tramite HTTPS.
Per ogni AEM può essere utilizzato un URL endpoint GraphQL di Magento diverso come ambiente Cloud Service. In questo modo i progetti possono collegare AEM ambienti di gestione temporanea con sistemi di gestione temporanea dei Magenti e AEM ambiente di produzione a un sistema di produzione Magento. L&#39;endpoint GraphQL del Magento deve essere disponibile pubblicamente, le connessioni VPN private o locali non sono supportate.

Per collegare AEM Commerce con il Magento, procedere come segue:

1. Ottenete l&#39;interfaccia CLI I/O del Adobe  con il plug-in Cloud Manager

   Controllate la documentazione [di](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) Adobe Cloud Manager su come scaricare, configurare e utilizzare la CLI [I/O di](https://github.com/adobe/aio-cli) Adobe con il plug-in CLI di [Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autenticazione CLI con il AEM come programma di Cloud Service

3. Imposta la `COMMERCE_ENDPOINT` variabile in Cloud Manager

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Per informazioni dettagliate, vedere [Documenti](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) CLI.

   L&#39;URL dell&#39;endpoint GraphQL di Magento deve puntare a  servizio GraphQl e utilizzare una connessione HTTPS protetta. Esempio: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>Puoi elencare tutte le variabili di Cloud Manager utilizzando il seguente comando per eseguire un doppio controllo: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!Note]
>
>In alternativa, puoi utilizzare l&#39;API [](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) Cloud Manager per configurare anche le variabili di Cloud Manager.

Con questo, sei pronto a utilizzare AEM Commerce come Cloud Service e puoi distribuire il tuo progetto tramite Cloud Manager.

## Integrazioni commerciali di terze parti {#integrations}

Per le integrazioni di commercio di terze parti, è necessario un livello [di mappatura](architecture/third-party.md) API per collegare AEM Commerce come Cloud Service e componenti CIF di base con il sistema di e-commerce. Questo livello di mappatura API viene in genere distribuito su Adobe I/O Runtime. Contatta il tuo rappresentante commerciale per le integrazioni disponibili e per accedere ad Adobe I/O Runtime.
