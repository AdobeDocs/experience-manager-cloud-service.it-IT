---
title: Guida introduttiva ad AEM Commerce as a Cloud Service
description: Guida introduttiva ad AEM Commerce as a Cloud Service
translation-type: tm+mt
source-git-commit: 5a90db8791dd92cceb811b9ed2beda3ecb4a974d
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 100%

---


# Guida introduttiva ad AEM Commerce as a Cloud Service {#start}

Per iniziare a utilizzare AEM Commerce as a Cloud Service, è necessario eseguire il provisioning di Experience Manager Cloud Service con il componente aggiuntivo Commerce Integration Framework (CIF). Il componente aggiuntivo CIF è un modulo aggiuntivo per [AEM Sites as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/sites/home.html).

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

## Onboarding {#onboarding}

L’onboarding per AEM Commerce as a Cloud Service è un processo in due fasi:

1. Abilitare AEM Commerce as a Cloud Service e ottenere il componente aggiuntivo CIF
2. Collegare AEM Commerce as a Cloud Service con l’ambiente Magento

Il primo passaggio è realizzato da Adobe. Occorrerà fornire informazioni come l’organizzazione IMS, l’URL dell’endpoint GraphQL dell’ambiente Magento, ecc. come parte del processo di provisioning. Per maggiori informazioni su prezzi e provisioning, contatta il tuo rappresentante commerciale.

Una volta effettuato il provisioning con il componente aggiuntivo CIF, questo verrà applicato a tutti i programmi Cloud Manager esistenti. Se non disponi di un programma Cloud Manager, dovrai crearne uno nuovo. Per ulteriori informazioni, consulta [Configurare il programma](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

Il secondo passaggio è autonomo per ogni ambiente AEM as a Cloud Service. Dopo il provisioning iniziale del componente aggiuntivo CIF, è necessario effettuare alcune configurazioni aggiuntive.

## Collegamento di AEM Commerce con Magento {#magento}

Per collegare il componente aggiuntivo CIF e i [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) all’ambiente Magento, è necessario fornire l’URL dell’endpoint GraphQL di Magento tramite una variabile di ambiente Cloud Manager. Il nome della variabile è `COMMERCE_ENDPOINT`. È necessario configurare una connessione protetta tramite HTTPS.
Per ogni ambiente AEM as a Cloud Service, è possibile utilizzare un diverso URL endpoint GraphQL di Magento. In questo modo i progetti possono collegare gli ambienti di staging di AEM ai sistemi di staging di Magento, e l’ambiente di produzione di AEM a un sistema di produzione di Magento. L’endpoint GraphQL di Magento deve essere disponibile pubblicamente; non sono supportate connessioni VPN private o locali.

Per collegare AEM Commerce a Magento, procedi come segue:

1. Ottieni Adobe I/O CLI con il plugin Cloud Manager.

   Consulta la [documentazione di Adobe Cloud Manager](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) su come scaricare, configurare e utilizzare [Adobe I/O CLI](https://github.com/adobe/aio-cli) con il [plugin CLI di Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentica la CLI con il programma AEM as a Cloud Service.

3. Imposta la variabile `COMMERCE_ENDPOINT` in Cloud Manager.

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Per informazioni dettagliate, consulta la [documentazione CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid).

   L’URL dell’endpoint GraphQL di Magento deve puntare al servizio GraphQl e utilizzare una connessione HTTPS protetta. Esempio: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>A scopo di verifica, puoi elencare tutte le variabili di Cloud Manager utilizzando il seguente comando: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!NOTE]
>
>In alternativa, puoi utilizzare l’[API di Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) per configurare anche le variabili di Cloud Manager.

Dopodiché, potrai utilizzare AEM Commerce as a Cloud Service e implementare il progetto tramite Cloud Manager.

## Integrazioni con soluzioni commerce di terze parti {#integrations}

Per le integrazioni con soluzioni commerce di terze parti, è necessario un [livello di mappatura API](architecture/third-party.md) per collegare AEM Commerce as a Cloud Service e i componenti core CIF con il tuo sistema commerce. Questo livello di mappatura API viene in genere distribuito su Adobe I/O Runtime. Contatta il tuo rappresentante commerciale per conoscere le integrazioni disponibili e accedere ad Adobe I/O Runtime.
