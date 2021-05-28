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
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 30%

---

# Guida introduttiva ad AEM Commerce as a Cloud Service {#start}

Per iniziare a utilizzare AEM Commerce as a Cloud Service, è necessario eseguire il provisioning di Experience Manager Cloud Service con il componente aggiuntivo Commerce Integration Framework (CIF). Il componente aggiuntivo CIF è un modulo aggiuntivo per [AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## Onboarding {#onboarding}

L’onboarding per AEM Commerce as a Cloud Service è un processo in due fasi:

1. Abilitare AEM Commerce as a Cloud Service e ottenere il componente aggiuntivo CIF
2. Connettere AEM Commerce come Cloud Service con la soluzione commerce

La prima fase di onboarding viene eseguita per Adobe. Per maggiori informazioni su prezzi e provisioning, contatta il tuo rappresentante commerciale.

Una volta effettuato il provisioning con il componente aggiuntivo CIF, questo verrà applicato a tutti i programmi Cloud Manager esistenti. Se non disponi di un programma Cloud Manager, dovrai crearne uno nuovo. Per ulteriori informazioni, consulta [Configurare il programma](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

Il secondo passaggio è autonomo per ogni ambiente AEM as a Cloud Service. Dopo il provisioning iniziale del componente aggiuntivo CIF, è necessario effettuare alcune configurazioni aggiuntive.

## Collegamento di AEM con una soluzione Commerce {#magento}

Per collegare il componente aggiuntivo CIF e i [AEM componenti core CIF](https://github.com/adobe/aem-core-cif-components) a una soluzione commerce, è necessario fornire l’URL dell’endpoint GraphQL tramite una variabile di ambiente Cloud Manager. Il nome della variabile è `COMMERCE_ENDPOINT`. È necessario configurare una connessione protetta tramite HTTPS.

Questa variabile di ambiente viene utilizzata in due posizioni:

- Le chiamate GraphQL da AEM a back-end commerce, tramite alcuni client GraphQl condivisibili comuni, utilizzati dai componenti core CIF AEM e dai componenti del progetto cliente.
- Imposta un URL proxy GraphQL su ogni ambiente AEM la variabile è impostata su `/api/graphql`. Viene utilizzato dai componenti lato client CIF degli strumenti di authoring AEM Commerce (componente aggiuntivo CIF) e CIF.

Per ogni ambiente AEM as a Cloud Service, è possibile utilizzare un diverso URL endpoint GraphQL di In questo modo i progetti possono collegare AEM ambienti di staging con sistemi di staging commerce e AEM ambiente di produzione a un sistema di produzione commerce. L’endpoint GraphQL di deve essere disponibile pubblicamente; non sono supportate connessioni VPN private o locali. Facoltativamente, è possibile fornire un’intestazione di autenticazione per utilizzare funzionalità CIF aggiuntive che richiedono l’autenticazione.

Facoltativo e solo per Adobe Commerce Enterprise / Cloud il componente aggiuntivo CIF supporta l’utilizzo di dati di catalogo in staging per gli autori di AEM. Questo richiede la configurazione di un token di autorizzazione. Il token di autorizzazione configurato è disponibile e utilizzato solo nelle istanze AEM autore per motivi di sicurezza. AEM le istanze di pubblicazione non possono mostrare dati in fase.

Esistono due opzioni per configurare l’endpoint:

### Interfaccia utente di Cloud Manager (predefinita) {#cm-ui}

Puoi eseguire questa operazione tramite una finestra di dialogo nella pagina Dettagli ambiente . Quando si visualizza questa pagina per un programma abilitato per Commerce, viene visualizzato un pulsante se l’endpoint non è attualmente configurato:

![Informazioni sull’ambiente CM](/help/commerce-cloud/assets/commerce-cmui.png)

Facendo clic su questo pulsante si apre una finestra di dialogo:

![Endpoint Commerce di CM](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

Dopo aver impostato l’endpoint (facoltativamente un token di autenticazione per il supporto del catalogo in staging), l’endpoint verrà visualizzato nella pagina dei dettagli. Facendo clic sull’icona Modifica si aprirà la stessa finestra di dialogo in cui l’endpoint può essere modificato, se necessario.

![Informazioni sull’ambiente CM](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Tramite Adobe I/O CLI {#adobe-cli}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Per collegare AEM con una soluzione commerce tramite Adobe I/O CLI, segui questi passaggi:

1. Ottieni Adobe I/O CLI con il plugin Cloud Manager.

   Consulta la [documentazione di Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it) su come scaricare, configurare e utilizzare [Adobe I/O CLI](https://github.com/adobe/aio-cli) con il [plugin CLI di Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentica l’Adobe I/O CLI con il programma AEM as a Cloud Service

3. Imposta la variabile `COMMERCE_ENDPOINT` in Cloud Manager.

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Per informazioni dettagliate, consulta la [documentazione CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid).

   L’URL dell’endpoint GraphQL di e-commerce deve puntare al servizio GraphQl di e-commerce e utilizzare una connessione HTTPS protetta. Esempio: `https://demo.magentosite.cloud/graphql`.

4. Abilitare le funzioni di catalogo in fase che richiedono l’autenticazione (facoltativo)

   >[!NOTE]
   >
   >Questa funzione è disponibile solo con Adobe Commerce Enterprise o Cloud Edition. Per ulteriori informazioni, consulta [Autenticazione basata su token](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) .

   Imposta la variabile segreta `COMMERCE_AUTH_HEADER` in Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>A scopo di verifica, puoi elencare tutte le variabili di Cloud Manager utilizzando il seguente comando: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Dopodiché, potrai utilizzare AEM Commerce as a Cloud Service e implementare il progetto tramite Cloud Manager.

## Configurazione di archivi e cataloghi {#catalog}

Il componente aggiuntivo CIF e i [componenti core CIF](https://github.com/adobe/aem-core-cif-components) possono essere utilizzati su più strutture di siti AEM connesse a diversi store di e-commerce (o viste store, ecc.). Per impostazione predefinita, il componente aggiuntivo CIF viene distribuito con una configurazione predefinita che si collega allo store e al catalogo predefiniti di Adobe Commerce (Magento).

Questa configurazione può essere regolata per il progetto tramite la configurazione del Cloud Service CIF, come descritto di seguito:

1. In AEM vai a Strumenti -> Cloud Services -> Configurazione CIF

2. Seleziona la configurazione di e-commerce da modificare

3. Apri le proprietà di configurazione tramite la barra delle azioni

![Configurazione dei Cloud Services CIF](/help/commerce-cloud/assets/cif-cloud-service-config.png)

È possibile configurare le seguenti proprietà:

- Client GraphQL: seleziona il client GraphQL configurato per la comunicazione back-end Commerce. In genere questo dovrebbe rimanere il valore predefinito.
- Visualizzazione archivio: l&#39;identificatore della vista archivio (Magento). Se questo campo viene lasciato vuoto, verrà utilizzata la visualizzazione archivio predefinita.
- Percorso proxy GraphQL: percorso URL del proxy GraphQL in AEM per le richieste proxy all’endpoint GraphQL di back-end per e-commerce.
   >[!NOTE]
   >
   > Nella maggior parte delle impostazioni il valore predefinito `/api/graphql` non deve essere modificato. Solo la configurazione avanzata che non utilizza il proxy GraphQL fornito dovrebbe modificare questa impostazione.
- Abilita supporto UID catalogo : abilita il supporto per UID invece di ID nelle chiamate GraphQL di back-end per e-commerce.
   >[!NOTE]
   >
   > Il supporto per gli UID è stato introdotto in Adobe Commerce (Magento) 2.4.2. Abilitare questa opzione solo se il backend commerce supporta uno schema GraphQL della versione 2.4.2 o successiva.
- Identificatore della categoria principale del catalogo: l&#39;identificatore (UID o ID) della directory principale del catalogo store

La configurazione mostrata sopra è di riferimento. I progetti devono fornire le proprie configurazioni.

Per configurazioni più complesse che utilizzano più strutture di siti AEM combinate con diversi cataloghi di e-commerce, consulta l’ esercitazione [Configurazione di più store di Commerce](configuring/multi-store-setup.md) .

## Risorse aggiuntive {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Configurazione di Commerce Multi-Store](configuring/multi-store-setup.md)
