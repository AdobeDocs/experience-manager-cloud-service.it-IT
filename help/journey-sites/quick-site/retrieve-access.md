---
title: Recuperare le informazioni di accesso all’archivio Git
description: Scopri in che modo lo sviluppatore front-end utilizza Cloud Manager per accedere alle informazioni dell’archivio Git.
exl-id: 3ef1cf86-6da4-4c09-9cfc-acafc8f6dd5c
solution: Experience Manager Sites
feature: Developing
role: Admin, Developer
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: ht
source-wordcount: '874'
ht-degree: 100%

---

# Recuperare le informazioni di accesso all’archivio Git {#retrieve-access}

{{traditional-aem}}

Scopri in che modo lo sviluppatore front-end utilizza Cloud Manager per accedere alle informazioni dell’archivio Git.

## Percorso affrontato finora {#story-so-far}

Se sei uno sviluppatore front-end responsabile solo della personalizzazione del tema del sito, puoi anche non sapere come è stato impostato AEM e passare alla sezione [Obiettivo](#objective) di questo documento.

Se hai anche il ruolo di amministratore di Cloud Manager o AEM, oltre a sviluppatore front-end, hai appreso nel documento precedente relativo al percorso di creazione rapida di un sito AEM, [Concedere l’accesso allo sviluppatore front-end,](grant-access.md), come effettuare l’onboarding dello sviluppatore front-end in modo che abbia accesso all’archivio Git, e ora dovresti aver appreso quanto segue:

* Come aggiungere uno sviluppatore front-end come utente.
* Come assegnare i ruoli richiesti allo sviluppatore front-end.

Questo articolo fa il passo successivo per mostrare come lo sviluppatore front-end utilizza l’accesso a Cloud Manager per recuperare le credenziali di accesso all’archivio Git AEM.

Ora che esiste un sito creato in base a un modello, è presente una pipeline impostata, l’onboarding dello sviluppatore è stato effettuato e dispone di tutte le informazioni necessarie, questo articolo lascia da parte il punto di vista degli amministratori e si occupa esclusivamente del ruolo di sviluppatore front-end.

## Obiettivo {#objective}

Questo documento spiega come, con il ruolo di sviluppatore front-end, puoi accedere a Cloud Manager e recuperare le credenziali di accesso all’archivio Git AEM. Dopo aver letto potrai:

* Comprendere ad alto livello cosa è Cloud Manager.
* Aver recuperato le credenziali per accedere al Git AEM in modo da poter eseguire il commit delle personalizzazioni.

## Ruolo responsabile {#responsible-role}

Questa parte del percorso è dedicata allo sviluppatore front-end.

## Requisiti  {#requirements}

Lo strumento Creazione rapida del sito consente agli sviluppatori front-end di lavorare in modo indipendente senza conoscere AEM o come è configurato. Tuttavia, l’amministratore di Cloud Manager deve integrare lo sviluppatore front-end nel team di progetto e l’amministratore AEM deve fornire alcune informazioni richieste. Assicurati di disporre delle seguenti informazioni prima di continuare.

* Dall’amministratore AEM:
   * File di origine del tema da personalizzare
   * Percorso di una pagina di esempio da utilizzare come base di riferimento
   * Credenziali utente proxy per testare le personalizzazioni nel contenuto live AEM
   * Requisiti di progettazione front-end
* Dall’amministratore di Cloud Manager:
   * Un’e-mail di benvenuto da Cloud Manager con informazioni sull’accesso
   * Il nome del programma o URL all’interno di Cloud Manager

Se manca qualcuno di questi elementi, contatta l’amministratore AEM o l’amministratore di Cloud Manager.

Si presume che lo sviluppatore front-end abbia un’ampia esperienza con i flussi di lavoro di sviluppo front-end e con gli strumenti comuni installati, tra cui:

* Git
* npm
* webpack
* Un editor preferito

## Informazioni su Cloud Manager {#understanding-cloud-manager}

Cloud Manager consente alle organizzazioni di gestire autonomamente AEM nel cloud. Include un framework di integrazione continua e distribuzione continua (CI/CD, Continuous Integration/Continuous Delivery) che consente ai team IT e ai partner dell’implementazione di accelerare la distribuzione di personalizzazioni o aggiornamenti senza compromettere prestazioni o sicurezza.

Per lo sviluppatore front-end, è il gateway per:

* Accedere a informazioni sull’archivio Git AEM per eseguire il commit delle personalizzazioni front-end.
* Avviare la pipeline di distribuzione per distribuire le personalizzazioni.

L’amministratore di Cloud Manager ti avrà inserito nel processo come utente di Cloud Manager. Dovresti aver ricevuto un&#39;e-mail di benvenuto simile alla seguente.

![E-mail di benvenuto](assets/welcome-email.png)

Se non hai ricevuto questa e-mail, contatta l’amministratore di Cloud Manager.

## Accesso a Cloud Manager {#access-cloud-manager}

1. Accedi ad Adobe Experience Cloud all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) oppure fai clic sul collegamento fornito nell’e-mail di benvenuto.

1. Cloud Manager elenca i vari programmi disponibili. Seleziona quello a cui devi accedere, secondo le indicazioni dell’amministratore di Cloud Manager. Se si tratta del primo progetto front-end per AEMaaCS, probabilmente è disponibile un solo programma.

   ![Selezione di un programma in Cloud Manager](assets/cloud-manager-select-program.png)

Viene visualizzata una panoramica del programma. La pagina avrà un aspetto diverso ma simile a questo esempio.

![Panoramica di Cloud Manager](assets/cloud-manager-overview.png)

## Recuperare le informazioni di accesso all’archivio  {#repo-access}

1. Nella sezione **Pipeline** della pagina Cloud Manager, seleziona il pulsante **Accedi alle informazioni sull’archivio**.

   ![Pipeline](assets/pipelines-repo-info.png)

1. Viene visualizzata la finestra di dialogo **Informazioni archivio**.

   ![Informazioni sull’archivio](assets/repo-info.png)

1. Seleziona il pulsante **Genera password** per creare una password personale.

1. Salva la password generata in un gestore di password sicuro. La password non verrà mai più visualizzata.

1. Copia anche i campi **username** e **Riga di comando Git**. In seguito, utilizzerai queste informazioni per accedere all’archivio.

1. Seleziona **Chiudi**.

## Passaggio successivo {#what-is-next}

Dopo aver completato questa parte del percorso di creazione rapida sito di AEM, è necessario:

* Comprendere ad alto livello cosa è Cloud Manager.
* Come recuperare le credenziali per accedere al Git AEM in modo da poter eseguire il commit delle personalizzazioni.

Sviluppa ulteriormente queste conoscenze e continua il percorso di creazione rapida del sito AEM consultando il documento [Personalizzare il tema del sito](customize-theme.md), dove scoprirai come è stato creato il tema del sito, come personalizzarlo e come eseguire il test utilizzando contenuti live AEM.

## Risorse aggiuntive {#additional-resources}

Ti consigliamo di passare alla parte successiva del percorso Creazione rapida sito, con il documento [Personalizzare il tema del sito](customize-theme.md). Inoltre, di seguito trovi alcune risorse aggiuntive facoltative, utili per approfondire i concetti menzionati in questo documento, ma che non sono un requisito obbligatorio per procedere nel percorso.

* [Documentazione di Adobe Experience Manager Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it): esplora la documentazione di Cloud Manager per informazioni dettagliate sulle sue funzioni.
