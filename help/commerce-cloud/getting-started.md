---
title: Guida introduttiva ad AEM Commerce as a Cloud Service
description: Scopri come distribuire un progetto AEM abilitato per il commercio in un ambiente AEM as a Cloud Service in esecuzione. Utilizza le funzioni di Adobe Cloud Manager e una pipeline CI/CD per creare la vetrina di riferimento Venia in un ambiente in esecuzione.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: aa7b9daba4242965baf20a77af356952cd7bc279
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 29%

---

# Guida introduttiva ad AEM Commerce as a Cloud Service {#start}

Per iniziare a utilizzare AEM Commerce as a Cloud Service, è necessario eseguire il provisioning di Experience Manager Cloud Service con il componente aggiuntivo Commerce Integration Framework (CIF). Il componente aggiuntivo CIF è un modulo aggiuntivo per [AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## Onboarding {#onboarding}

L’onboarding per AEM Commerce as a Cloud Service è un processo in due fasi:

1. Abilitare AEM Commerce as a Cloud Service e ottenere il componente aggiuntivo CIF
2. Connettere AEM Commerce as a Cloud Service con la soluzione commerce

Il primo passaggio di onboarding è effettuato per Adobe. Per maggiori informazioni su prezzi e provisioning, contatta il tuo rappresentante commerciale.

Una volta effettuato il provisioning con il componente aggiuntivo CIF, questo verrà applicato a tutti i programmi Cloud Manager esistenti. Se non disponi di un programma Cloud Manager, dovrai crearne uno nuovo. Per ulteriori informazioni, consulta [Configurare il programma](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

Il secondo passaggio è autonomo per ogni ambiente AEM as a Cloud Service. Dopo il provisioning iniziale del componente aggiuntivo CIF, è necessario effettuare alcune configurazioni aggiuntive.

## Collegamento dell’AEM con una soluzione Commerce {#solution}

Per collegare il componente aggiuntivo CIF e [Componenti core CIF dell’AEM](https://github.com/adobe/aem-core-cif-components) con una soluzione commerce, devi fornire l’URL dell’endpoint GraphQL tramite una variabile di ambiente Cloud Manager. Il nome della variabile è `COMMERCE_ENDPOINT`. È necessario configurare una connessione protetta tramite HTTPS.

Questa variabile di ambiente viene utilizzata in due posizioni:

- GraphQL chiama dall’AEM al backend di e-commerce, tramite alcuni client GraphQl condivisibili, utilizzati dai componenti core CIF dell’AEM e dai componenti di progetto del cliente.
- Imposta un URL proxy di GraphQL in ciascun ambiente AEM in cui la variabile è impostata come disponibile `/api/graphql`. Questo viene utilizzato dagli strumenti di creazione commerce dell’AEM (componente aggiuntivo CIF) e dai componenti lato client CIF.

Per ogni ambiente AEM as a Cloud Service, è possibile utilizzare un diverso URL endpoint GraphQL di In questo modo i progetti possono collegare gli ambienti di staging AEM con i sistemi di staging commerce e l’ambiente di produzione AEM a un sistema di produzione commerce. L’endpoint GraphQL di deve essere disponibile pubblicamente; non sono supportate connessioni VPN private o locali. Facoltativamente, è possibile fornire un’intestazione di autenticazione per utilizzare funzioni CIF aggiuntive che richiedono l’autenticazione.

Facoltativamente e solo per Adobe Commerce Enterprise / Cloud, il componente aggiuntivo CIF supporta l’utilizzo di dati di catalogo per gli autori di AEM. È necessario configurare un’intestazione di autorizzazione. Questa intestazione è disponibile e utilizzata solo nelle istanze di authoring AEM per motivi di sicurezza. Le istanze di pubblicazione dell’AEM non possono mostrare dati di staging.

Esistono due opzioni per configurare l’endpoint:

### Tramite l’interfaccia utente di Cloud Manager (impostazione predefinita) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Questa operazione può essere eseguita utilizzando una finestra di dialogo nella pagina Dettagli dell’ambiente. Quando si visualizza questa pagina per un programma abilitato per Commerce, se l’endpoint non è attualmente configurato viene visualizzato un pulsante:

![Informazioni sull&#39;ambiente CM](/help/commerce-cloud/assets/commerce-cmui.png)

Fai clic su questo pulsante per aprire una finestra di dialogo:

![Endpoint Commerce CM](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

Dopo aver impostato l’endpoint e, facoltativamente, un’intestazione di autorizzazione per il supporto di cataloghi in staging, l’endpoint viene visualizzato nella pagina dei dettagli. Facendo clic sull’icona Modifica viene aperta la stessa finestra di dialogo in cui è possibile modificare l’endpoint, se necessario.

![Informazioni sull&#39;ambiente CM](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Tramite CLI Adobe I/O  {#adobe-cli}

Per collegare l’AEM a una soluzione commerce tramite Adobe I/O CLI, effettua le seguenti operazioni:

1. Ottieni Adobe I/O CLI con il plugin Cloud Manager.

   Controlla la [Documentazione di Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it) su come scaricare, configurare e utilizzare [CLI ADOBE I/O](https://github.com/adobe/aio-cli) con [Plug-in CLI di Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentica l’interfaccia della riga di comando Adobe I/O con il programma as a Cloud Service AEM

3. Imposta la variabile `COMMERCE_ENDPOINT` in Cloud Manager.

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Per informazioni dettagliate, consulta la [documentazione CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid).

   L’URL dell’endpoint GraphQL di Commerce deve puntare al servizio GraphQl di Commerce e utilizzare una connessione HTTPS sicura. Esempio: `https://<yourcommercesystem>/graphql`.

4. Abilita funzioni di catalogo di staging che richiedono l’autenticazione (facoltativo)

   >[!NOTE]
   >
   >Questa funzione è disponibile solo con Adobe Commerce Enterprise o Cloud Edition. Consulta [Autenticazione basata su token](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) per i dettagli.

   Imposta il `COMMERCE_AUTH_HEADER` variabile segreta in Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>A scopo di verifica, puoi elencare tutte le variabili di Cloud Manager utilizzando il seguente comando: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Dopodiché, potrai utilizzare AEM Commerce as a Cloud Service e implementare il progetto tramite Cloud Manager.

## Configurazione di store e cataloghi {#catalog}

Il componente aggiuntivo CIF e [Componenti core CIF](https://github.com/adobe/aem-core-cif-components) può essere utilizzato su più strutture del sito AEM connesse a diversi store commerciali (o viste store, ecc.). Per impostazione predefinita, il componente aggiuntivo CIF viene distribuito con una configurazione predefinita che si collega all’archivio e al catalogo predefiniti di Adobe Commerce.

Questa configurazione può essere regolata per il progetto tramite la configurazione di Cloud Service CIF, come segue:

1. In AEM vai a Strumenti -> Cloud Services -> Configurazione CIF.

2. Seleziona la configurazione commerce da modificare

3. Apri le proprietà di configurazione tramite la barra delle azioni

![Configurazione Cloud Services CIF](/help/commerce-cloud/assets/cif-cloud-service-config.png)

È possibile configurare le seguenti proprietà:

- Client GraphQL: seleziona il client GraphQL configurato per la comunicazione back-end commerce. In genere, questa impostazione deve rimanere quella predefinita.
- Visualizzazione store: l&#39;identificatore della visualizzazione store. Se vuota, verrà utilizzata la vista archivio predefinita.
- Percorso proxy GraphQL: il percorso URL che il proxy GraphQL dell’AEM utilizza per inoltrare le richieste all’endpoint GraphQL backend di Commerce.
   >[!NOTE]
   >
   > Nella maggior parte delle impostazioni il valore predefinito `/api/graphql` non deve essere modificato. Questa impostazione può essere modificata solo da una configurazione avanzata che non utilizza il proxy GraphQL fornito.
- Abilita supporto UID catalogo: abilita il supporto per UID invece dell’ID nelle chiamate GraphQL di back-end per e-commerce.
   >[!NOTE]
   >
   > Il supporto per gli UID è stato introdotto in Adobe Commerce 2.4.2. Abilita questa opzione solo se il backend di e-commerce supporta uno schema GraphQL della versione 2.4.2 o successiva.
- Identificatore categoria radice catalogo: l’identificatore (UID o ID) della radice del catalogo dell’archivio
   >[!CAUTION]
   >
   > A partire dalla versione 2.0.0 dei componenti core CIF, il supporto per `id` è stato rimosso e sostituito con `uid`. Se il progetto utilizza i componenti core CIF versione 2.0.0, devi abilitare il supporto UID del catalogo e utilizzare un UID di categoria valido come &quot;Identificatore della categoria principale del catalogo&quot;.

La configurazione mostrata sopra è a scopo di riferimento. I progetti devono fornire le proprie configurazioni.

Per configurazioni più complesse che utilizzano più strutture di siti AEM combinate con diversi cataloghi di e-commerce, vedi [Configurazione di più store di Commerce](configuring/multi-store-setup.md) esercitazione.

## Risorse aggiuntive {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Configurazione di più store di Commerce](configuring/multi-store-setup.md)
- [Configurazione di più sistemi commerce](configuring/multiple-commerce-systems-setup.md)

