---
title: Creazione di programmi di produzione
description: Scopri come creare un programma di produzione per ospitare il traffico in tempo reale con Cloud Manager.
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: ecb168e9261b3e3ed89e4cbe430b3da9f777a795
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 88%

---


# Creazione di programmi di produzione {#create-production-program}

Un programma di produzione è destinato agli utenti che hanno familiarità con AEM e Cloud Manager e sono pronti per iniziare a scrivere, creare e testare il codice allo scopo di distribuirlo per ospitare il traffico in tempo reale.

Per ulteriori informazioni sui tipi di programmi, consulta il documento [Informazioni su programmi e tipi di programmi.](program-types.md)

## Creazione di un programma di produzione {#create}

Per creare un programma di produzione, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic su **Aggiungi programma** in alto a destra.

   ![Pagina di destinazione di Cloud Manager](assets/log-in.png)

1. Per creare un programma di produzione, seleziona **Configura per produzione** nella procedura guidata Crea programma nome e specifica un nome.

   ![Procedura guidata per la creazione di un programma](assets/create-production-program.png)

1. Se lo desideri, puoi anche aggiungere un’immagine al programma trascinando un file immagine nell’area **Aggiungi un’immagine del programma** oppure fai clic per selezionare un’immagine da un browser di file. Tocca o fai clic su **Continua**.

1. Se si dispone dei diritti necessari, il **Sicurezza** verrà visualizzata e fornirà l’opzione per attivare **HIPAA** e/o **Protezione WAF-DDOS** per il programma di produzione. Se necessario per il programma che stai creando, seleziona le opzioni applicabili e quindi tocca o fai clic su **Continua**.

   * Impossibile abilitare o disabilitare HIPAA dopo la creazione del programma.
      * [Ulteriori informazioni](https://www.adobe.com/go/hipaa-ready_it) sull’implementazione della soluzione compatibile HIPAA di Adobe.
   * Una volta attivata, la protezione WAF-DDOS può essere configurata impostando un [pipeline non di produzione.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

   {{waf-limited-release}}

   ![Opzioni di protezione](assets/create-production-program-security.png)

1. Dalla scheda **Soluzioni e componenti aggiuntivi**, seleziona le soluzioni da includere nel programma.

   * Se non sai per certo se ti servono uno o più programmi per le varie soluzioni disponibili, seleziona quella che più ti interessa. Potrai attivare altre soluzioni in un secondo tempo [modificando il programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md). Per ulteriori consigli sulla configurazione del programma, consulta [Introduzione ai programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).
   * Se in precedenza avevi selezionato **Abilita protezione avanzata**, puoi selezionare solo il numero di soluzioni coperto dai diritti HIPAA.

   ![Selezione delle soluzioni](assets/setup-prod-select.png)

1. Per visualizzare i componenti aggiuntivi facoltativi, come l’opzione per il componente **Commerce** in **Sites**, fai clic sulla freccia che precede il nome della soluzione.

   ![Selezione dei componenti aggiuntivi](assets/setup-prod-commerce.png)

1. Dopo aver selezionato le soluzioni e i componenti aggiuntivi, fai clic su **Continua**.

1. Nella scheda **Data di pubblicazione**, inserisci la data di pubblicazione pianificata per il programma di produzione.

   ![Definizione della data di pubblicazione pianificata](assets/setup-go-live.png)

   * Questa data può essere modificata in qualsiasi momento.
   * Questa data è solo per uso informativo e attiva il widget di pubblicazione sulla pagina della panoramica del programma per fornire collegamenti rapidi alla documentazione sulle best practice di AEM as a Cloud Service, al fine di allinearsi con il percorso che culmina in un’esperienza di pubblicazione fluida e di successo.

1. Fai clic su **Crea**.

Il programma viene creato da Cloud Manager e visualizzato nella pagina di destinazione, disponibile per la selezione.

![Panoramica di Cloud Manager](assets/navigate-cm.png)

## Accesso al programma {#accessing}

1. Quando visualizzi la scheda del programma nella pagina di destinazione, seleziona il pulsante con i puntini di sospensione per visualizzare le opzioni di menu disponibili.

   ![Panoramica del programma](assets/program-overview.png)

1. Per accedere alla pagina **Panoramica** di Cloud Manager, seleziona **Panoramica del programma**.

1. La principale scheda di invito all’azione nella pagina della panoramica ti guiderà attraverso la creazione di un ambiente, una pipeline non di produzione e infine una pipeline di produzione.

   ![Panoramica del programma](assets/set-up-prod5.png)

Se in qualsiasi momento è necessario passare a un altro programma o tornare alla pagina della panoramica per crearne uno nuovo, fai clic sul nome del programma nella parte superiore sinistra della schermata per visualizzare l’opzione **Accedi a**.

![Accedi a](assets/create-program-a1.png)

>[!NOTE]
>
>A differenza di un [programma sandbox](introduction-sandbox-programs.md#auto-creation), un programma di produzione richiede che l’utente con il ruolo di Cloud Manager appropriato crei il progetto e aggiunga un ambiente tramite l’interfaccia utente self-service.
