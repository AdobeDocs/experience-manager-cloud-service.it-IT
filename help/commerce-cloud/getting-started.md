---
title: Guida introduttiva ad AEM Commerce as a Cloud Service
description: Scopri come distribuire un progetto di AEM abilitato per e-commerce in un ambiente in esecuzione AEM as a Cloud Service. Utilizza le funzioni di Adobe Cloud Manager e una pipeline CI/CD per creare la vetrina di riferimento di Venia in un ambiente in esecuzione.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
translation-type: tm+mt
source-git-commit: e34592d24c8f6c17e6959db1d5c513feaf6381c8
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 52%

---

# Guida introduttiva ad AEM Commerce as a Cloud Service {#start}

Per iniziare a utilizzare AEM Commerce as a Cloud Service, è necessario eseguire il provisioning di Experience Manager Cloud Service con il componente aggiuntivo Commerce Integration Framework (CIF). Il componente aggiuntivo CIF è un modulo aggiuntivo per [AEM Sites as a Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/sites/home.html).

## Onboarding {#onboarding}

L’onboarding per AEM Commerce as a Cloud Service è un processo in due fasi:

1. Abilitare AEM Commerce as a Cloud Service e ottenere il componente aggiuntivo CIF
2. Connettere AEM Commerce come Cloud Service con la soluzione commerce

La prima fase di onboarding viene eseguita per Adobe. Per maggiori informazioni su prezzi e provisioning, contatta il tuo rappresentante commerciale.

Una volta effettuato il provisioning con il componente aggiuntivo CIF, questo verrà applicato a tutti i programmi Cloud Manager esistenti. Se non disponi di un programma Cloud Manager, dovrai crearne uno nuovo. Per ulteriori informazioni, consulta [Configurare il programma](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

Il secondo passaggio è autonomo per ogni ambiente AEM as a Cloud Service. Dopo il provisioning iniziale del componente aggiuntivo CIF, è necessario effettuare alcune configurazioni aggiuntive.

## Collegamento di AEM con una soluzione di e-commerce {#magento}

Per collegare il componente aggiuntivo CIF e i [AEM componenti core CIF](https://github.com/adobe/aem-core-cif-components) a una soluzione commerce, è necessario fornire l’URL dell’endpoint GraphQL tramite una variabile di ambiente Cloud Manager. Il nome della variabile è `COMMERCE_ENDPOINT`. È necessario configurare una connessione protetta tramite HTTPS.
Per ogni ambiente AEM as a Cloud Service, è possibile utilizzare un diverso URL endpoint GraphQL di In questo modo i progetti possono collegare AEM ambienti di staging con sistemi di staging commerce e AEM ambiente di produzione a un sistema di produzione commerce. L’endpoint GraphQL di deve essere disponibile pubblicamente; non sono supportate connessioni VPN private o locali. Facoltativamente, è possibile fornire un’intestazione di autenticazione per utilizzare funzionalità CIF aggiuntive che richiedono l’autenticazione.

Esistono due opzioni per configurare l’endpoint:

### 1) Tramite l’interfaccia utente di Cloud Manager (predefinita)

Puoi eseguire questa operazione tramite una finestra di dialogo nella pagina Dettagli ambiente . Quando si visualizza questa pagina per un programma abilitato per Commerce, viene visualizzato un pulsante se l’endpoint non è attualmente configurato:

![Implementazione finale del badge eco-compatibile](/help/commerce-cloud/assets/commerce-cmui.png)

Facendo clic su questo pulsante si apre una finestra di dialogo:

![Implementazione finale del badge eco-compatibile](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

Dopo aver impostato l’endpoint (e, facoltativamente, il token), l’endpoint verrà visualizzato nella pagina di dettaglio. Facendo clic sull’icona Modifica si aprirà la stessa finestra di dialogo in cui l’endpoint può essere modificato, se necessario.

![Implementazione finale del badge eco-compatibile](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 2) Tramite Adobe I/O CLI

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Per collegare AEM con una soluzione commerce tramite Adobe I/O CLI, segui questi passaggi:

1. Ottieni Adobe I/O CLI con il plugin Cloud Manager.

   Consulta la [documentazione di Adobe Cloud Manager](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) su come scaricare, configurare e utilizzare [Adobe I/O CLI](https://github.com/adobe/aio-cli) con il [plugin CLI di Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentica l’Adobe I/O CLI con il programma AEM as a Cloud Service

3. Imposta la variabile `COMMERCE_ENDPOINT` in Cloud Manager.

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Per informazioni dettagliate, consulta la [documentazione CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid).

   L’URL dell’endpoint GraphQL di e-commerce deve puntare al servizio GraphQl di e-commerce e utilizzare una connessione HTTPS protetta. Esempio: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>A scopo di verifica, puoi elencare tutte le variabili di Cloud Manager utilizzando il seguente comando: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Dopodiché, potrai utilizzare AEM Commerce as a Cloud Service e implementare il progetto tramite Cloud Manager.

## Abilitare le funzioni che richiedono l’autenticazione (facoltativo) {#staging}

>[!NOTE]
>
>Questa funzione è disponibile solo con Magenti Enterprise Edition o Magenti Cloud.

1. Accedi al Magento e crea un token di integrazione. Per ulteriori informazioni, consulta [Autenticazione basata su token](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) . Assicurati che il token di integrazione abbia accesso *solo* alle risorse `Content -> Staging`. Copia il valore `Access Token`.

1. Imposta la variabile segreta `COMMERCE_AUTH_HEADER` in Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

   Consulta [Collegamento AEM Commerce con Magenti](#magento) su come configurare l’Adobe I/O CLI per Cloud Manager.

## Integrazioni con soluzioni commerce di terze parti {#integrations}

Per le integrazioni con soluzioni commerce di terze parti, è necessario un [livello di mappatura API](architecture/third-party.md) per collegare AEM Commerce as a Cloud Service e i componenti core CIF con il tuo sistema commerce. Questo livello di mappatura API viene in genere distribuito su Adobe I/O Runtime. Contatta il tuo rappresentante commerciale per conoscere le integrazioni disponibili e accedere ad Adobe I/O Runtime.
