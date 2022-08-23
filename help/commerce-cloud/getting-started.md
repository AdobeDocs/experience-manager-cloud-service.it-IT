---
title: Guida introduttiva ad AEM Commerce as a Cloud Service
description: Scopri come distribuire un progetto di AEM abilitato per e-commerce in un ambiente in esecuzione AEM as a Cloud Service. Utilizza le funzioni di Adobe Cloud Manager e una pipeline CI/CD per creare la vetrina di riferimento di Venia in un ambiente in esecuzione.
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: f5e465d90477f1b49e4ff1c5ca9dd47cc5d539bb
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 29%

---

# Guida introduttiva ad AEM Commerce as a Cloud Service {#start}

Per iniziare a utilizzare AEM Commerce as a Cloud Service, è necessario eseguire il provisioning di Experience Manager Cloud Service con il componente aggiuntivo Commerce Integration Framework (CIF). Il componente aggiuntivo CIF è un modulo aggiuntivo per [AEM Sites as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## Onboarding {#onboarding}

L’onboarding per AEM Commerce as a Cloud Service è un processo in due fasi:

1. Abilitare AEM Commerce as a Cloud Service e ottenere il componente aggiuntivo CIF
2. Connettere AEM Commerce as a Cloud Service con la soluzione commerce

La prima fase di onboarding viene eseguita per Adobe. Per maggiori informazioni su prezzi e provisioning, contatta il tuo rappresentante commerciale.

Una volta effettuato il provisioning con il componente aggiuntivo CIF, questo verrà applicato a tutti i programmi Cloud Manager esistenti. Se non disponi di un programma Cloud Manager, dovrai crearne uno nuovo. Per ulteriori informazioni, consulta [Configurare il programma](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

Il secondo passaggio è autonomo per ogni ambiente AEM as a Cloud Service. Dopo il provisioning iniziale del componente aggiuntivo CIF, è necessario effettuare alcune configurazioni aggiuntive.

## Collegamento di AEM con una soluzione Commerce {#solution}

Per collegare il componente aggiuntivo CIF e la [Componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) con una soluzione commerce, devi fornire l’URL dell’endpoint GraphQL tramite una variabile di ambiente Cloud Manager. Il nome della variabile è `COMMERCE_ENDPOINT`. È necessario configurare una connessione protetta tramite HTTPS.

Questa variabile di ambiente viene utilizzata in due posizioni:

- Le chiamate GraphQL da AEM a back-end commerce, tramite alcuni client GraphQl condivisibili comuni, utilizzati dai componenti core CIF AEM e dai componenti del progetto cliente.
- Imposta un URL proxy GraphQL su ogni ambiente AEM in cui la variabile è impostata è disponibile in `/api/graphql`. Viene utilizzato dai componenti lato client CIF degli strumenti di authoring AEM Commerce (componente aggiuntivo CIF) e CIF.

Per ogni ambiente AEM as a Cloud Service, è possibile utilizzare un diverso URL endpoint GraphQL di In questo modo i progetti possono collegare AEM ambienti di staging con sistemi di staging commerce e AEM ambiente di produzione a un sistema di produzione commerce. L’endpoint GraphQL di deve essere disponibile pubblicamente; non sono supportate connessioni VPN private o locali. Facoltativamente, è possibile fornire un’intestazione di autenticazione per utilizzare funzionalità CIF aggiuntive che richiedono l’autenticazione.

Facoltativamente e solo per Adobe Commerce Enterprise / Cloud il componente aggiuntivo CIF supporta l’utilizzo di dati di catalogo in staging per gli autori di AEM. Questo richiede la configurazione di un’intestazione di autorizzazione. Questa intestazione è disponibile e utilizzata solo AEM istanze dell’autore per motivi di sicurezza. AEM le istanze di pubblicazione non possono mostrare dati in fase.

Esistono due opzioni per configurare l’endpoint:

### Interfaccia utente di Cloud Manager (predefinita) {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

Puoi eseguire questa operazione tramite una finestra di dialogo nella pagina Dettagli ambiente . Quando si visualizza questa pagina per un programma abilitato per Commerce, viene visualizzato un pulsante se l’endpoint non è attualmente configurato:

![Informazioni sull’ambiente CM](/help/commerce-cloud/assets/commerce-cmui.png)

Facendo clic su questo pulsante si apre una finestra di dialogo:

![Endpoint Commerce di CM](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

Dopo aver impostato l’endpoint ed eventualmente un’intestazione di autorizzazione per il supporto del catalogo in staging, l’endpoint verrà visualizzato nella pagina dei dettagli. Facendo clic sull’icona Modifica si aprirà la stessa finestra di dialogo in cui l’endpoint può essere modificato, se necessario.

![Informazioni sull’ambiente CM](/help/commerce-cloud/assets/commerce-cmui-done.png)

### Tramite Adobe I/O CLI  {#adobe-cli}

Per collegare AEM con una soluzione commerce tramite Adobe I/O CLI, segui questi passaggi:

1. Ottieni Adobe I/O CLI con il plugin Cloud Manager.

   Controlla la [Documentazione di Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it) su come scaricare, configurare e utilizzare il [Adobe I/O CLI](https://github.com/adobe/aio-cli) con [Plug-in CLI di Cloud Manager](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. Autentica l’Adobe I/O CLI con il programma as a Cloud Service AEM

3. Imposta la variabile `COMMERCE_ENDPOINT` in Cloud Manager.

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   Per informazioni dettagliate, consulta la [documentazione CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid).

   L’URL dell’endpoint GraphQL di e-commerce deve puntare al servizio GraphQl di e-commerce e utilizzare una connessione HTTPS protetta. Esempio: `https://<yourcommercesystem>/graphql`.

4. Abilitare le funzioni di catalogo in fase che richiedono l’autenticazione (facoltativo)

   >[!NOTE]
   >
   >Questa funzione è disponibile solo con Adobe Commerce Enterprise o Cloud Edition. Vedi [Autenticazione basata su token](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) per i dettagli.

   Imposta la `COMMERCE_AUTH_HEADER` variabile segreta in Cloud Manager:

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>A scopo di verifica, puoi elencare tutte le variabili di Cloud Manager utilizzando il seguente comando: `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

Dopodiché, potrai utilizzare AEM Commerce as a Cloud Service e implementare il progetto tramite Cloud Manager.

## Configurazione di archivi e cataloghi {#catalog}

Il componente aggiuntivo CIF e il [Componenti core CIF](https://github.com/adobe/aem-core-cif-components) può essere utilizzato su più strutture di sito AEM collegate a diversi store commerce (o viste store, ecc.). Per impostazione predefinita, il componente aggiuntivo CIF viene distribuito con una configurazione predefinita che si collega all’archivio e al catalogo predefiniti di Adobe Commerce.

Questa configurazione può essere regolata per il progetto tramite la configurazione del Cloud Service CIF, come descritto di seguito:

1. In AEM vai a Strumenti -> Cloud Services -> Configurazione CIF

2. Seleziona la configurazione di e-commerce da modificare

3. Apri le proprietà di configurazione tramite la barra delle azioni

![Configurazione dei Cloud Services CIF](/help/commerce-cloud/assets/cif-cloud-service-config.png)

È possibile configurare le seguenti proprietà:

- Client GraphQL: seleziona il client GraphQL configurato per la comunicazione back-end Commerce. In genere questo dovrebbe rimanere il valore predefinito.
- Visualizzazione archivio: l&#39;identificatore della vista archivio. Se questo campo viene lasciato vuoto, verrà utilizzata la visualizzazione archivio predefinita.
- Percorso proxy GraphQL: percorso URL del proxy GraphQL in AEM per le richieste proxy all’endpoint GraphQL di back-end per e-commerce.
   >[!NOTE]
   >
   > Nella maggior parte delle impostazioni il valore predefinito `/api/graphql` non devono essere modificate. Solo la configurazione avanzata che non utilizza il proxy GraphQL fornito dovrebbe modificare questa impostazione.
- Abilita supporto UID catalogo : abilita il supporto per UID invece di ID nelle chiamate GraphQL di back-end per e-commerce.
   >[!NOTE]
   >
   > Il supporto per gli UID è stato introdotto in Adobe Commerce 2.4.2. Abilitalo solo se il backend commerce supporta uno schema GraphQL della versione 2.4.2 o successiva.
- Identificatore della categoria principale del catalogo: l&#39;identificatore (UID o ID) della directory principale del catalogo store
   >[!CAUTION]
   >
   > A partire dalla versione 2.0.0 dei componenti core CIF , il supporto per `id` è stato rimosso e sostituito con `uid`. Se il progetto utilizza i componenti core CIF versione 2.0.0, è necessario abilitare il supporto per gli UID del catalogo e utilizzare un UID di categoria valido come &quot;Identificatore di categoria principale del catalogo&quot;.

La configurazione mostrata sopra è di riferimento. I progetti devono fornire le proprie configurazioni.

Per configurazioni più complesse che utilizzano più strutture di siti AEM combinate con diversi cataloghi di e-commerce, consulta la sezione [Configurazione di Commerce Multi-Store](configuring/multi-store-setup.md) esercitazione.

## Risorse aggiuntive {#additional-resources}

- [AEM Project Archetype](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [Configurazione di Commerce Multi-Store](configuring/multi-store-setup.md)
