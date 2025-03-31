---
title: Aggiungere archivi esterni in Cloud Manager - Versione beta limitata
description: Scopri come aggiungere un archivio esterno in Cloud Manager. Cloud Manager supporta l’integrazione con gli archivi GitHub Enterprise Server, GitLab e Bitbucket.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: 167e6f01cd9bca6191dd47c33561d37a0633be77
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 26%

---

# Aggiungere archivi esterni in Cloud Manager - Versione beta limitata {#external-repositories}

Scopri come aggiungere un archivio esterno in Cloud Manager. Cloud Manager supporta l’integrazione con gli archivi GitHub Enterprise Server, GitLab e Bitbucket.

>[!NOTE]
>
>Questa funzione è disponibile solo tramite il programma di adozione anticipata. Per ulteriori dettagli e per iscriverti come utente iniziale, consulta [Porta il tuo Git, ora con supporto per GitLab e Bitbucket](/help/implementing/cloud-manager/release-notes/2024/2024-10-0.md#gitlab-bitbucket).

## Configurare un archivio esterno

La configurazione di un archivio esterno in Cloud Manager avviene in tre passaggi:

1. [Aggiungere un archivio esterno](#add-external-repo) a un programma selezionato.
1. Fornire un token di accesso all’archivio esterno.
1. Convalida la proprietà dell’archivio GitHub privato.



## Aggiungere un archivio esterno {#add-ext-repo}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[Programmi personali](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma a cui si desidera collegare un repository esterno.

1. Nel menu laterale, in **Programma**, fare clic su ![Icona struttura cartella](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Archivi**.

   ![Pagina Archivi](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. Nell’angolo superiore a destra della pagina **Archivi** fai clic su **Aggiungi archivio**.

1. Nella finestra di dialogo **Aggiungi archivio**, seleziona **Archivio privato** per collegare un archivio Git esterno al programma in uso.

   ![Aggiungi un archivio personale](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. In ciascun campo, fornisci i seguenti dettagli sull’archivio:

   | Campo | Descrizione |
   | --- | --- |
   | **Nome dell’archivio** | Obbligatorio. Un nome espressivo per il nuovo archivio. |
   | **URL dell’archivio** | Obbligatorio. L’URL dell’archivio.<br><br>Se utilizzi un archivio ospitato da GitHub, il percorso deve terminare in `.git`.<br>Ad esempio, *`https://github.com/org-name/repo-name.git`* (il percorso URL è solo a scopo illustrativo).<br><br>Per gli archivi esterni, è necessario utilizzare il seguente formato di percorso URL: <br>`https://git-vendor-name.com/org-name/repo-name.git`<br> o <br>`https://self-hosted-domain/org-name/repo-name.git`<br> e il fornitore Git corrispondente. |
   | **Seleziona il tipo di archivio** | Obbligatorio. Selezionare il tipo di repository in uso:<ul><li>**GitHub** (GitHub Enterprise Server e versione self-hosted di GitHub)</li><li>**GitLab** (sia `gitlab.com` che la versione con hosting autonomo di GitLab) </li><li>**Bitbucket** (sia `bitbucket.org` che Bitbucket Server e la versione con hosting autonomo di Bitbucket)</li></ul>Se il percorso URL dell’archivio precedente include il nome del fornitore Git, ad esempio GitLab o Bitbucket, il tipo di archivio è già preselezionato. |
   | **Descrizione** | Facoltativo. Descrizione dettagliata dell’archivio. |

1. Seleziona **Salva** per aggiungere l’archivio.

1. Nella finestra di dialogo **Convalida della proprietà dell’archivio privato**, fornisci un token di accesso per convalidare la proprietà dell’archivio esterno in modo da potervi accedere.

   ![Selezione di un token di accesso esistente per un archivio](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *Selezione di un token di accesso esistente per un archivio Bitbucket.*

   | Tipo di token | Descrizione |
   | --- | --- |
   | **Usa token di accesso esistente** | Se hai già fornito un token di accesso all’archivio per la tua organizzazione e hai accesso a più archivi, puoi selezionare un token esistente. Utilizza l’elenco a discesa **Nome token** per scegliere il token da applicare all’archivio. In caso contrario, aggiungi un nuovo token di accesso. |
   | **Aggiungere un nuovo token di accesso** | **Tipo di archivio: GitHub**<br><ul><li> Nel campo di testo **Nome token**, digita un nome per il token di accesso che stai creando.<li>Crea un token di accesso personale seguendo le istruzioni riportate nella [documentazione GitHub](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).<li>Per le autorizzazioni richieste, imposta quanto segue:<ul><li>**Autorizzazioni richieste per il token di accesso personale GitHub (PAT)**<br> Queste autorizzazioni garantiscono che Cloud Manager possa convalidare le richieste di pull, gestire i controlli dello stato del commit e accedere ai dettagli dell&#39;archivio necessari. In GitHub, quando generi il token di accesso personale (PAT), accertati che includa quanto segue:<ul><li>**Autorizzazioni archivio:**<ul><li>Richiesta pull (lettura e scrittura)<li>Stati commit (lettura e scrittura)<li>Metadati archivio (sola lettura)</li></li></ul></ul><li>**Eventi webhook richiesti (per archivi ospitati da GitHub)**<br> Questi eventi consentono a Cloud Manager di rispondere all&#39;attività GitHub, ad esempio la convalida di richieste pull, trigger basati su push per le pipeline o la sincronizzazione del codice Edge Delivery Services. Quando configuri manualmente un webhook GitHub, accertati che sia configurato per l’attivazione dei seguenti eventi:<ul><li>**Eventi webhook richiesti:**<ol><li>Richieste pull<li>Push<li>Commenti problema</li></li></ul></ul><ul><li>Nel campo **Token di accesso**, incolla il token appena creato. |
   |  | **Tipo di archivio: GitLab**<ul><li>Nel campo di testo **Nome token**, digita un nome per il token di accesso che stai creando.<li>Crea un token di accesso personale seguendo le istruzioni riportate nella [documentazione GitLab](https://docs.gitlab.com/user/profile/personal_access_tokens/).<li>Per le autorizzazioni richieste, imposta quanto segue:<ul><li>**Autorizzazioni richieste per il token di accesso personale GitLab (PAT)**<br> Questi ambiti consentono a Cloud Manager di accedere ai dati dell&#39;archivio e alle informazioni utente necessarie per la convalida e l&#39;integrazione del webhook. Quando crei il token di accesso personale in GitLab, accertati che includa i seguenti ambiti:<ul><li>**Ambiti token:**<ul><li>api<li>read_user</li></li></ul></ul><li>**Eventi webhook richiesti (per archivi ospitati da GitLab)**<br> Questi eventi webhook consentono a Cloud Manager di attivare le pipeline quando il codice viene inviato o viene inviata una richiesta di unione. Tiene inoltre traccia dei commenti relativi alla convalida delle richieste pull (tramite eventi nota). Quando configuri manualmente un webhook in GitLab, assicurati di includere i seguenti eventi:<ul><li>**Eventi webhook richiesti:**<ol><li>Eventi push<li>Unisci eventi di richiesta<li>Eventi nota</li></li></li></ul></ul></ul><ul><li>Nel campo **Token di accesso**, incolla il token appena creato. |
   |  | **Tipo di archivio: Bitbucket**<ul><li>Nel campo di testo **Nome token**, digita un nome per il token di accesso che stai creando.<li>Crea un token di accesso all&#39;archivio utilizzando la [documentazione Bitbucket](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/).<li>Per le autorizzazioni richieste, imposta quanto segue:<ul><li>**Autorizzazioni richieste per il token di accesso personale (PAT) Bitbucket**<br> Queste autorizzazioni consentono a Cloud Manager di accedere al contenuto dell&#39;archivio, gestire le richieste pull e configurare eventi webhook o di reagire ad essi. Quando crei la password dell’app in Bitbucket, accertati che includa quanto segue:<ul><li>**Autorizzazioni password app richieste:**<ul><li>Archivio (sola lettura)<li>Richieste pull (lettura e scrittura)<li>Webhook (lettura e scrittura)</li></li></ul></ul><li>**Eventi webhook richiesti (per archivi ospitati da Bitbucket)**<br> Questi eventi garantiscono che Cloud Manager possa convalidare le richieste di pull, rispondere ai push del codice e interagire con i commenti per il coordinamento della pipeline. Se imposti manualmente il webhook in Bitbucket, configuralo per attivarlo nei seguenti eventi:<ul><li>**Eventi webhook richiesti:**<ol><li>Richiesta pull: creata<li>Richiesta pull: aggiornata<li>Richieste pull: unite<li>Richiesta pull: commento<li>Archivio: push</li></li></li></ul></ul></ul><ul><li>Nel campo **Token di accesso**, incolla il token appena creato. |

   >[!NOTE]
   >
   >La funzionalità **Aggiungi nuovo token di accesso** è attualmente in fase di adozione anticipata. Ulteriori funzionalità sono in fase di pianificazione. Di conseguenza, le autorizzazioni necessarie per i token di accesso potrebbero cambiare. Inoltre, è possibile che l’interfaccia utente per la gestione dei token venga aggiornata, includendo eventuali funzionalità quali le date di scadenza dei token. Inoltre, potrebbero essere aggiunti controlli automatici per garantire che i token collegati agli archivi rimangano validi.

1. Fai clic su **Convalida**.

Dopo la convalida, l’archivio esterno è pronto per essere utilizzato e collegato a una pipeline.

## Collegare un archivio esterno convalidato a una pipeline {#validate-ext-repo}

1. Aggiungi o modifica una pipeline:
   * [Aggiungere una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Aggiungere una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [Modificare una pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   ![Archivio del codice sorgente della pipeline e ramo Git](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *Finestra di dialogo Aggiungi pipeline non di produzione con l’archivio selezionato e il ramo Git.*

1. Quando aggiungi o modifichi una pipeline, per specificare il percorso **Codice sorgente** per la pipeline nuova o esistente, scegli l‘archivio esterno che desideri utilizzare dall‘elenco a discesa **Archivio**.

1. Nell’elenco a discesa **Ramo Git** seleziona il ramo di origine della pipeline.

1. Fai clic su **Salva**.


>[!TIP]
>
>Per informazioni dettagliate sulla gestione degli archivi in Cloud Manager, consulta [Archivi di Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

## Configurare un webhook per un archivio esterno {#configure-webhook}

Cloud Manager consente di configurare i webhook per gli archivi Git esterni aggiunti. Vedi [Aggiungere un archivio esterno](#add-ext-repo). Questi webhook consentono a Cloud Manager di ricevere eventi correlati a diverse azioni all’interno della soluzione del fornitore Git.

I webhook consentono ad esempio a Cloud Manager di attivare azioni basate su eventi quali i seguenti:

* Creazione richiesta di pull (PR): avvia la funzionalità di convalida PR.
* Eventi push: avvia le pipeline quando il trigger &quot;On Git Commit&quot; è attivato (abilitato).
* Azioni future basate su commenti: consente flussi di lavoro, come l’implementazione diretta da un PR a un ambiente di sviluppo rapido (RDE).

La configurazione del webhook non è necessaria per gli archivi ospitati su `GitHub.com` perché Cloud Manager si integra direttamente tramite l&#39;app GitHub.
Per tutti gli altri archivi esterni per i quali è stato eseguito l’onboarding con un token di accesso, come GitHub Enterprise Server, GitLab e Bitbucket, la configurazione del webhook è disponibile e deve essere impostata manualmente.

**Per configurare un webhook per un repository esterno:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[Programmi personali](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma in cui si desidera configurare un webhook per un archivio Git esterno.

1. Nell’angolo in alto a sinistra della pagina, fai clic sull’![icona Mostra menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu a sinistra.

1. Nel menu a sinistra, sotto l&#39;intestazione **Programma**, fare clic su ![Icona struttura cartella](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Archivi**.

1. Nella pagina **Archivi**, utilizzando la colonna **Tipo** per guidarti nella selezione, individua l&#39;archivio desiderato, quindi fai clic sull&#39;icona ![Puntini di sospensione - Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) accanto a esso.

   ![Opzione Config Webhook nel menu a discesa per un repository selezionato](/help/implementing/cloud-manager/managing-code/assets/repository-config-webhook.png)

1. Dal menu a discesa, fare clic su **Webhook di configurazione**.

   ![Finestra di dialogo Configura webhook](/help/implementing/cloud-manager/managing-code/assets/config-webhook.png)

1. Nella finestra di dialogo **Webhook di configurazione** eseguire le operazioni seguenti:

   1. Accanto al campo **URL webhook**, fare clic sull&#39;icona ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg).
Incolla l’URL in un file di testo normale. L’URL copiato è necessario per le impostazioni del webhook del fornitore Git.
   1. Accanto al campo token/chiave **Segreto webhook**, fai clic su **Genera**, quindi fai clic sull&#39;icona ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg).
Incolla il segreto in un file di testo normale. Il segreto copiato è necessario per le impostazioni del webhook del fornitore Git.
1. Fai clic su **Chiudi**.
1. Passa alla soluzione del fornitore Git (GitHub Enterprise, GitLab o Bitbucket).

   Tutti i dettagli sulla configurazione del webhook e gli eventi necessari per ogni fornitore sono disponibili in [Aggiungi un repository esterno](#add-ext-repo). Al punto 8, vedere la tabella.

1. Individua la sezione **Impostazioni webhook** della soluzione.
1. Incolla l’URL del webhook copiato in precedenza nel campo di testo dell’URL.
   1. Sostituisci il parametro di query `api_key` nell&#39;URL del webhook con la tua vera chiave API.

      Per generare una chiave API, devi creare un progetto di integrazione in Adobe Developer Console. Per informazioni dettagliate, consulta [Creazione di un progetto di integrazione API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/).

1. Incolla il segreto del webhook copiato in precedenza nel campo di testo **Segreto** (o **Chiave segreta**, o **Token segreto**).
1. Configura il webhook per inviare gli eventi appropriati previsti da Cloud Manager.


### Convalida delle richieste pull con webhook

Una volta configurati correttamente i webhook, Cloud Manager attiva automaticamente le esecuzioni della pipeline o i controlli di convalida PR per l’archivio.

Si applicano i seguenti comportamenti:

* **Server GitHub Enterprise**

  Una volta creato, il controllo viene visualizzato come nella schermata seguente. La differenza chiave rispetto a `GitHub.com` è che `GitHub.com` utilizza un&#39;esecuzione di controllo, mentre GitHub Enterprise Server (che utilizza token di accesso personali) genera uno stato di commit:

  ![Conferma stato per indicare il processo di convalida PR su GitHub Enterprise Server](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-github-pr-validation.png)

* **Bitbucket**

  Quando la convalida della qualità del codice è in esecuzione:

  ![Stato durante l&#39;esecuzione della convalida della qualità del codice](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket1.png)

  Utilizza lo stato del commit per tenere traccia dell&#39;avanzamento della convalida PR. Nel caso seguente, la schermata mostra cosa accade quando una convalida della qualità del codice non riesce a causa di un problema del cliente. Viene aggiunto un commento con informazioni dettagliate sull’errore e viene creato un controllo del commit che mostra l’errore (visibile a destra):

  ![Stato di convalida della richiesta pull per Bitbucket](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket2.png)

* **GitLab**

  Le interazioni GitLab si basano esclusivamente sui commenti. Quando inizia la convalida, viene aggiunto un commento. Al termine della convalida (riuscita o non riuscita), il commento iniziale viene rimosso e sostituito con un nuovo commento contenente i risultati della convalida o i dettagli dell’errore.

  Quando la convalida della qualità del codice è in esecuzione:

  ![Quando è in esecuzione la convalida della qualità del codice](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab1.png)

  Al termine della convalida della qualità a freddo:

  ![Al termine della convalida della qualità a freddo](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab2.png)

  Quando la convalida della qualità del codice non riesce e viene restituito un errore:

  ![Quando la convalida della qualità del codice non riesce e viene restituito un errore](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab3.png)

  Quando la convalida della qualità del codice non riesce a causa di problemi del cliente:

  ![Quando la convalida della qualità del codice non riesce a causa di problemi del cliente](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab4.png)


## Risoluzione dei problemi del webhook

* Accertati che l’URL del webhook includa una chiave API valida.
* Controlla che gli eventi del webhook siano configurati correttamente nelle impostazioni del fornitore Git.
* Se la convalida PR o i trigger della pipeline non funzionano, verifica che il segreto webhook sia aggiornato sia in Cloud Manager che nel fornitore Git.








## Limitazioni

* Gli archivi esterni non possono essere collegati alle pipeline di configurazione.
* Le pipeline con archivi esterni (non ospitati su GitHub) e il trigger &quot;On Git Changes&quot; (In caso di modifiche Git) non si avviano automaticamente. Possono essere avviati solo manualmente.


<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->


