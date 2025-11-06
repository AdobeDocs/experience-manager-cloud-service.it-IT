---
title: Guida introduttiva ad AEM Commerce as a Cloud Service
description: Scopri come distribuire un progetto di e-commerce Adobe Experience Manager (AEM) utilizzando Adobe Cloud Manager, una pipeline CI/CD e la vetrina di riferimento Venia.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 9%

---


# Guida introduttiva ad AEM Commerce as a Cloud Service {#start}

Per iniziare a utilizzare Adobe Experience Manager (AEM) Commerce as a Cloud Service, è necessario eseguire il provisioning di Experience Manager Cloud Service con il componente aggiuntivo Commerce integration framework (CIF). Il componente aggiuntivo CIF è un modulo aggiuntivo per [AEM Sites as a Cloud Service.](/help/sites-cloud/sites-cloud-changes.md)

>[!TIP]
>
>**Hai considerato Edge Delivery Services?**
>
>Edge Delivery Services è la soluzione preferita da Adobe per la creazione di una vetrina. Per ulteriori informazioni, vedere il documento [Introduzione e panoramica](/help/commerce-cloud/introduction.md).

## Onboarding {#onboarding}

L’onboarding per AEM Commerce as a Cloud Service è un processo in due fasi:

1. Abilitare AEM Commerce as a Cloud Service e ottenere il componente aggiuntivo CIF
1. Collegare AEM Commerce as a Cloud Service con la soluzione commerce

Il primo passaggio di onboarding viene eseguito da Adobe. Per maggiori dettagli su prezzi e provisioning, contatta il tuo rappresentante commerciale.

Dopo il provisioning con il componente aggiuntivo CIF, questo viene applicato a tutti i programmi Cloud Manager esistenti. Se non disponi di un programma Cloud Manager, devi crearne uno. Per ulteriori dettagli, consulta [Configurare il programma.](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html?lang=it)

Il secondo passaggio è autonomo per ogni ambiente AEM as a Cloud Service. Dopo il provisioning iniziale del componente aggiuntivo CIF è necessario eseguire alcune configurazioni aggiuntive.

## Collegamento di AEM a una soluzione Commerce {#solution}

Per collegare il componente aggiuntivo CIF e i [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) con una soluzione commerce, è necessario fornire l&#39;URL dell&#39;endpoint GraphQL tramite una variabile di ambiente Cloud Manager. Il nome della variabile è `COMMERCE_ENDPOINT`. È necessario configurare una connessione protetta tramite HTTPS.

Questa variabile di ambiente viene utilizzata in due posizioni:

* GraphQL chiama da AEM al backend commerce, tramite alcuni client GraphQl condivisibili, utilizzati dai componenti core di AEM CIF e dai componenti di progetto del cliente.
* Configurare un URL proxy di GraphQL in ogni ambiente AEM in cui la variabile è impostata disponibile in `/api/graphql`. Questo URL viene utilizzato dagli strumenti di creazione di AEM Commerce (componente aggiuntivo CIF) e dai componenti lato client di CIF.

Per ogni ambiente AEM as a Cloud Service è possibile utilizzare un URL endpoint GraphQL diverso. In questo modo i progetti possono collegare gli ambienti di staging di AEM con i sistemi di staging di commerce e l’ambiente di produzione di AEM a un sistema di produzione di commerce. L&#39;endpoint GraphQL deve essere disponibile pubblicamente; le connessioni VPN private o locali non sono supportate. Facoltativamente, è possibile fornire un’intestazione di autenticazione per utilizzare funzioni CIF aggiuntive che richiedono l’autenticazione.

Facoltativamente, e solo per Adobe Commerce Enterprise / Cloud, il componente aggiuntivo CIF supporta l’utilizzo di dati di catalogo in staging per gli autori di AEM. Questi dati richiedono la configurazione di un’intestazione di autorizzazione. Questa intestazione è disponibile e utilizzata solo nelle istanze di AEM Author per motivi di sicurezza. Le istanze di pubblicazione di AEM non possono mostrare dati di staging.

Esistono due opzioni per configurare l’endpoint:

### Tramite l’interfaccia utente di Cloud Manager (impostazione predefinita) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Questa configurazione può essere eseguita utilizzando una finestra di dialogo nella pagina Dettagli dell’ambiente. Quando si visualizza questa pagina per un programma abilitato per Commerce, se l’endpoint non è attualmente configurato viene visualizzato un pulsante:

![Informazioni sull&#39;ambiente CM](/help/commerce-cloud/cif-storefront/assets/commerce-cmui.png)

Facendo clic su questo pulsante si apre una finestra di dialogo:

![endpoint Commerce CM](/help/commerce-cloud/cif-storefront/assets/commerce-cm-endpoint.png)

Dopo aver impostato l’endpoint e, facoltativamente, un’intestazione di autorizzazione per il supporto di cataloghi in staging, l’endpoint viene visualizzato nella pagina dei dettagli. Facendo clic sull&#39;icona Modifica per aprire la stessa finestra di dialogo in cui è possibile modificare il punto finale, se necessario.

![Informazioni sull&#39;ambiente CM](/help/commerce-cloud/cif-storefront/assets/commerce-cmui-done.png)

### Tramite Adobe I/O CLI  {#adobe-cli}

Per collegare AEM a una soluzione commerce tramite Adobe I/O CLI, segui questi passaggi:

1. Ottieni Adobe I/O CLI con il plug-in Cloud Manager.

   * Consulta la [documentazione di Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=it) su come scaricare, configurare e utilizzare [Adobe I/O CLI](https://github.com/adobe/aio-cli) con il plug-in [Cloud Manager CLI.](https://github.com/adobe/aio-cli-plugin-cloudmanager)

1. Autentica Adobe I/O CLI con il programma AEM as a Cloud Service.

1. Imposta la variabile `COMMERCE_ENDPOINT` in Cloud Manager.

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   * Per informazioni dettagliate, consulta la [documentazione CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid).

   * L’URL dell’endpoint GraphQL di Commerce deve puntare al servizio GraphQl di Commerce e utilizzare una connessione HTTPS sicura. Ad esempio: `https://<yourcommercesystem>/graphql`.

1. Abilita le funzioni di catalogo in staging che richiedono l’autenticazione (facoltativo).

   >[!NOTE]
   >
   >Questa funzione è disponibile solo con Adobe Commerce Enterprise o Cloud Edition. Per ulteriori informazioni, vedere [Autenticazione basata su token](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens).

   * Imposta la variabile segreta `COMMERCE_AUTH_HEADER` in Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>A scopo di verifica, puoi elencare tutte le variabili di Cloud Manager utilizzando il seguente comando: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Ora puoi utilizzare AEM Commerce as a Cloud Service e distribuire il progetto tramite Cloud Manager.

## Configurazione di store e cataloghi {#catalog}

Il componente aggiuntivo CIF e i [componenti core CIF](https://github.com/adobe/aem-core-cif-components) possono essere utilizzati in più strutture del sito AEM connesse a diversi store commerce (o viste store, ecc.). Per impostazione predefinita, il componente aggiuntivo CIF viene distribuito con una configurazione predefinita che si collega all’archivio e al catalogo predefiniti di Adobe Commerce.

Questa configurazione può essere regolata per il progetto tramite la configurazione di CIF Cloud Service, come segue:

1. In AEM vai a Strumenti > Cloud Services > Configurazione CIF.

1. Seleziona la configurazione commerce da modificare.

1. Apri le proprietà di configurazione tramite la barra delle azioni.

![Configurazione servizi cloud CIF](/help/commerce-cloud/cif-storefront/assets/cif-cloud-service-config.png)

È possibile configurare le seguenti proprietà:

* Client GraphQL: seleziona il client GraphQL configurato per la comunicazione back-end commerce. In genere, questo client deve rimanere quello predefinito.
* Visualizzazione store: l&#39;identificatore della visualizzazione store. Se vuota, viene utilizzata la visualizzazione predefinita dello store.
* Percorso proxy GraphQL: il percorso URL che il proxy GraphQL in AEM utilizza per inoltrare le richieste all’endpoint GraphQL back-end di commerce.

  >[!NOTE]
  >
  > Nella maggior parte delle impostazioni, il valore predefinito `/api/graphql` non deve essere modificato. Questa impostazione può essere modificata solo da una configurazione avanzata che non utilizza il proxy GraphQL fornito.

* Abilita il supporto per Catalog UID: abilita il supporto per UID invece dell’ID nelle chiamate GraphQL back-end per e-commerce.

  >[!NOTE]
  >
  > Il supporto per gli UID è stato introdotto in Adobe Commerce 2.4.2. Abilita gli UID solo se il backend di e-commerce supporta uno schema GraphQL della versione 2.4.2 o successiva.

* Identificatore categoria principale catalogo: l’identificatore (UID o ID) della directory principale del catalogo principale dello store

  >[!CAUTION]
  >
  > A partire dalla versione 2.0.0 dei Componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. Se il progetto utilizza i componenti core di CIF versione 2.0.0, devi abilitare il supporto per Catalog UID e utilizzare una categoria valida di UID come &quot;Identificatore categoria radice catalogo&quot;.

La configurazione mostrata sopra è a scopo di riferimento. I progetti devono fornire le proprie configurazioni.

Per impostazioni più complesse, l&#39;utilizzo di più strutture di siti AEM combinate con diversi cataloghi di e-commerce è illustrato nell&#39;esercitazione [Configurazione di più store di Commerce](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md).

## Risorse aggiuntive {#additional-resources}

* [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
* [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Configurazione di Commerce Multi-Store](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md)
* [Configurazione di più sistemi Commerce](/help/commerce-cloud/cif-storefront/configuring/multiple-commerce-systems-setup.md)
