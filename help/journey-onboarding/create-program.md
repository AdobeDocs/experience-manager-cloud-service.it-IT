---
title: Creare un programma
description: Scopri come utilizzare Cloud Manager per creare il tuo primo programma.
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
source-git-commit: fbf1e0b7cefb1dc981d7ee106283280fb2225007
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 4%

---

# Creare un programma {#create-program}

In questa parte del [percorso di bordo,](overview.md) imparerai a utilizzare Cloud Manager per creare il tuo primo programma.

## Obiettivo {#objective}

Dopo aver esaminato il documento precedente in questo percorso di onboarding, [Access Cloud Manager,](cloud-manager.md) hai garantito l’accesso appropriato a Cloud Manager. Ora puoi creare il tuo primo programma.

Dopo aver letto questo documento:

* Comprendere cos&#39;è un programma.
* Scopri la differenza tra i programmi di produzione e sandbox.
* Puoi creare il tuo programma.

## Cos&#39;è un programma? {#programs}

I programmi rappresentano il livello di organizzazione più alto di Cloud Manager. A seconda della licenza con l&#39;Adobe, i programmi ti consentono di organizzare la soluzione e concedere l&#39;accesso a determinati membri del team a tali programmi.

I programmi Cloud Manager rappresentano set di ambienti Cloud Manager. Questi programmi supportano set logici di iniziative aziendali, in genere corrispondenti a un contratto a livello di servizio (SLA, Service Level Agreement) concesso in licenza. Ad esempio, un programma può rappresentare le risorse AEM per supportare un sito web pubblico globale per un&#39;organizzazione, mentre un altro programma rappresenta un DAM interno centrale.

Se si ricorda l&#39;esempio della teorica WKND Travel and Adventure Enterprises, che è un locatario che si concentra sui media relativi ai viaggi, potrebbero avere due programmi: un programma Sites per la divisione WKND Magazine e un programma Assets per la divisione WKND Media. I diversi membri del gruppo avrebbero quindi accesso ai diversi programmi a causa della loro divisione dei requisiti di lavoro.

Esistono due diversi tipi di programmi:

* A **programma di produzione** viene creato per abilitare il traffico live per il sito. Questo è il tuo ambiente &quot;reale&quot;.
* A **programma sandbox** viene generalmente creato per scopi di formazione, esecuzione di demo, abilitazione, POC o documentazione.

Poiché hanno scopi diversi, i diversi ambienti hanno opzioni diverse. Tuttavia, il processo di creazione è simile. Per questo percorso di onboarding creeremo un ambiente sandbox.

>[!NOTE]
>
>Per impostazione predefinita, un utente con accesso a un ambiente AEM avrà anche il ruolo Utente di Cloud >Manager . Questo ruolo in e di per sé è insufficiente per consentire all&#39;utente di accedere alla visualizzazione dei dettagli del programma. Un utente con solo il ruolo utente di Cloud Manager può navigare tramite le opzioni del menu di programma fino all’URL dell’autore dell’ambiente AEM (se esistono ambienti). Gli utenti devono contattare il proprio amministratore se desiderano ottenere l&#39;accesso a livello di programma.

## Creazione di un programma sandbox {#create-sandbox}

Segui questi passaggi per creare un programma sandbox.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Dalla pagina di destinazione di Cloud Manager, fai clic su **Aggiungi programma** nell’angolo in alto a destra dello schermo.

   ![Pagina di destinazione di Cloud Manager](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

1. Dalla procedura guidata Crea programma, seleziona **Configurare una sandbox**, specificare un nome di programma e quindi fare clic su **Crea**.

   ![Creazione del tipo di programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

Nella pagina di destinazione verrà visualizzata una nuova scheda del programma sandbox con un indicatore di stato durante il processo di configurazione.

![Creazione di sandbox dalla pagina della panoramica](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

Una volta completato il programma, i membri dell&#39;organizzazione vengono assegnati al **Sviluppatore** il profilo di prodotto può accedere a Cloud Manager e gestire gli archivi Git di Cloud Manager.

## Novità {#whats-next}

Ora che il tuo primo programma è stato creato, puoi creare ambienti per esso. Continua il tuo percorso di onboarding esaminando il documento [Creare ambienti.](create-environments.md)

## Risorse aggiuntive {#additional-resources}

Segui le risorse aggiuntive per ulteriori informazioni su:

* [Programmi e tipi di programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) - Scopri la gerarchia di Cloud Manager e come i diversi tipi di programmi si adattano alla sua struttura e come si differenziano.
* [Creazione di programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) - Scopri come utilizzare Cloud Manager per creare un tuo programma sandbox per scopi di formazione, demo, POC o per altri scopi non di produzione.
* [Creazione di programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) - Scopri come utilizzare Cloud Manager per creare un tuo programma di produzione per ospitare il traffico live.
* [Utilizzo di Adobe Cloud Manager - Programmi](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) - I programmi Cloud Manager rappresentano insiemi di ambienti AEM che supportano set logici di iniziative aziendali, in genere corrispondenti a un contratto a livello di servizio (SLA, Service Level Agreement) acquistato.
