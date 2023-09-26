---
title: Creazione di un programma
description: Scopri come creare il tuo primo programma con Cloud Manager.
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
source-git-commit: d67c5c9baafb9b7478f1d1c2ad924f5a8250a1ee
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 67%

---

# Creazione di un programma {#create-program}

In questa parte del [percorso di onboarding,](overview.md) scopri come creare il primo programma con Cloud Manager.

## Obiettivo {#objective}

Dopo aver rivisto il documento precedente di questo percorso di onboarding, [Accesso a Cloud Manager,](cloud-manager.md) hai appurato di avere accesso a Cloud Manager. Ora puoi creare il primo programma.

Dopo aver letto questo documento, puoi:

* Comprendere e spiegare cos’è un programma.
* Conoscerai la differenza tra i programmi di produzione e i programmi sandbox.
* Crea un programma personalizzato.

## Che cos’è un programma? {#programs}

I programmi rappresentano il livello organizzativo più alto in Cloud Manager. In base alla licenza Adobe in uso, i programmi consentono di organizzare la soluzione e concedere le autorizzazioni di accesso a tali programmi a determinati membri del gruppo.

I programmi Cloud Manager rappresentano set di ambienti di Cloud Manager. Questi programmi supportano set logici di iniziative aziendali, in genere corrispondenti al contratto del livello di servizio (SLA) concesso in licenza. Ad esempio, un programma può rappresentare le risorse Adobe Experience Manager (AEM) per supportare un sito web pubblico globale per un’organizzazione, mentre un altro programma può rappresentare un DAM interno centrale.

Se ricordi l’esempio teorico di WKND Travel and Adventure Enterprises, un tenant che si occupa di media legati ai viaggi, potrebbe avere due programmi. Un programma AEM Sites per la divisione WKND Magazine e un programma AEM Assets per la divisione WKND Media. Diversi membri del gruppo avrebbero quindi accesso a diversi programmi per via della divisione dei lavori.

Esistono due diversi tipi di programmi:

* Un **programma di produzione** viene creato per abilitare il traffico in tempo reale per il sito. Si tratta del tuo ambiente &quot;reale&quot;.
* I **programmi sandbox** vengono generalmente creati a scopi di formazione, esecuzione di demo, abilitazione, POC o documentazione.

Poiché hanno scopi diversi, i diversi ambienti presentano opzioni differenti. Tuttavia, il processo per la loro creazione è analogo. Per questo percorso di onboarding viene creato un ambiente sandbox.

>[!TIP]
>
>Se devi creare un programma di produzione, consulta [Risorse aggiuntive](#additional-resources) sezione per un collegamento alla documentazione che descrive i programmi in dettaglio.

## Creazione di un programma sandbox {#create-sandbox}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Dalla pagina di destinazione di Cloud Manager, fai clic su **Aggiungi programma** nell’angolo in alto a destra dello schermo.

   ![Pagina di destinazione di Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/cloud-manager-my-programs.png)

1. Dalla procedura guidata Crea programma, seleziona **Configurare una sandbox**, quindi specifica un nome per il programma e tocca o fai clic su **Continua**.

   ![Creazione del tipo di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

1. In **Configurare la sandbox** , è possibile scegliere le soluzioni da abilitare nel programma sandbox. Le soluzioni **Sites** e **Assets** sono sempre incluse nei programmi sandbox e vengono selezionate automaticamente. Questo è sufficiente per il tuo esempio di onboarding. Fai clic su **Crea**.

   ![Selezione della soluzione](assets/set-up-sandbox-onboarding.png)

Nella pagina di destinazione viene visualizzata una nuova scheda del programma sandbox e un indicatore di stato che mostra l’avanzamento del processo di configurazione.

![Creazione di un programma sandbox dalla pagina Panoramica](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

Una volta completato il programma, i membri dell’organizzazione vengono assegnati al **Sviluppatore** Il profilo di prodotto può accedere a Cloud Manager e gestire gli archivi Git di Cloud Manager.

## Passaggio successivo {#whats-next}

Ora che hai creato il primo programma, puoi creare degli ambienti da aggiungere. Continua il tuo percorso di onboarding passando al documento successivo [Creare ambienti.](create-environments.md)

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate risorse aggiuntive e opzionali utili per andare oltre il contenuto del percorso di onboarding.

* [Programmi e tipi di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md): scopri la gerarchia di Cloud Manager, le differenze tra i diversi tipi di programmi e come si adattano alla struttura gerarchica.
* [Creazione di programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md): scopri come creare un programma sandbox personalizzato da utilizzare per formazione, demo, POC o altre finalità non di produzione con Cloud Manager.
* [Creazione di programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md): scopri come creare un programma di produzione per ospitare il traffico in tempo reale con Cloud Manager.
* [Utilizzo dei programmi di Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=it): i programmi Cloud Manager rappresentano insiemi di ambienti AEM che supportano set logici di iniziative aziendali, in genere corrispondenti a un contratto del livello di servizio (SLA) acquistato.
* [Team e profili di prodotto di AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md): scopri come i team e i profili di prodotto di AEM as a Cloud Service possono concedere e limitare l’accesso alle soluzioni di Adobe con licenza.
