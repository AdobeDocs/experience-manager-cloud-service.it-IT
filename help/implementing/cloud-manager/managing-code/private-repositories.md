---
title: Aggiungere un archivio GitHub privato in Cloud Manager
description: Scopri come configurare Cloud Manager per l’utilizzo di archivi GitHub privati.
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 45645a963c42f1335ff2019ffe2aa516ee084a9f
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 33%

---

# Aggiungere un archivio GitHub Cloud privato in Cloud Manager {#private-repositories}

Configurando Cloud Manager per l&#39;integrazione con GitHub Cloud privato (archivi in hosting su `github.com`), puoi convalidare il codice direttamente in GitHub utilizzando Cloud Manager. Questa configurazione elimina la necessità di sincronizzare regolarmente il codice con l’archivio Adobe.

>[!NOTE]
>
>Puoi anche aggiungere i seguenti tipi di archivio con i webhook:
>
>* Archivi GitHub Enterprise Server (versione self-hosted di GitHub)
>* Archivi GitLab (sia `gitlab.com` che versioni con hosting autonomo di GitLab)
>* Archivi Bitbucket (sia `bitbucket.org` che Bitbucket Server, versione con hosting autonomo di BitBucket)
>
>Vedi [Aggiungi archivi esterni in Cloud Manager - versione beta privata](/help/implementing/cloud-manager/managing-code/external-repositories.md).

<!-- CONSIDER ADDING MORE DETAIL... THE WHY. Some key points about this capability include the following:

* **Direct Integration**: With this setup, you can directly link your private GitHub repositories to Cloud Manager, allowing for seamless code validation, deployment, and CI/CD (Continuous Integration/Continuous Deployment) pipelines without needing to maintain a separate sync process with Adobe's default Git repository.

* **Customization and Autonomy**: Companies often prefer managing their own source code repositories for security, control, and integration purposes. "Build your own GitHub" allows organizations to maintain their internal development processes while leveraging the full functionality of Cloud Manager for building, testing, and deploying AEM (Adobe Experience Manager) applications.

* **Simplified Workflow**: It reduces the overhead of synchronizing code between multiple repositories by allowing Cloud Manager to access the organization's private repository directly, making the development cycle faster and more efficient.

* **CI/CD Pipelines**: Teams can still benefit from Adobe Cloud Manager's automated build, test, and deployment processes, as the integration allows the CI/CD pipelines to pull code from the organization's own GitHub repository.

In essence, a "Build your own GitHub" in Adobe Cloud Manager empowers teams to manage their own GitHub repositories while still using the robust deployment and validation capabilities of Cloud Manager.

>[!NOTE]
>
>This feature is exclusive to public GitHub. Support for self-hosted GitHub is not available. -->

## Configurazione {#configuration}

La configurazione di un archivio cloud GitHub privato in Cloud Manager consiste di due passaggi:

1. [Aggiungere un archivio GitHub Cloud privato](#add-repo) a un programma selezionato.
1. Quindi, [convalida la proprietà dell&#39;archivio GitHub Cloud privato](#validate-ownership).



### Aggiungere un archivio GitHub Cloud privato a un programma {#add-repo}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[Programmi personali](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma a cui si desidera collegare un archivio Git privato.

1. Nel menu laterale, in **Servizi**, seleziona l’![icona della cartella](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Archivi**.

   ![Pagina Archivi](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. Nell’angolo superiore a destra della pagina **Archivi** fai clic su **Aggiungi archivio**.

1. Nella finestra di dialogo **Aggiungi archivio**, seleziona **Archivio privato** come tipo di archivio.

   ![Aggiungi un archivio personale](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. In ciascun campo, fornisci i seguenti dettagli sull’archivio:

   | Campo | Descrizione |
   | --- | --- |
   | Nome archivio | Un nome espressivo per il nuovo archivio. |
   | URL archivio | URL dell&#39;archivio privato, che deve terminare in `.git`.<br>Ad esempio, *`https://github.com/org-name/repo-name.git`* (il percorso URL è solo a scopo illustrativo). |
   | Descrizione (facoltativo) | Descrizione dettagliata dell’archivio. |

1. Seleziona **Salva**.
Ora puoi [convalidare la proprietà dell&#39;archivio privato](#validate-ownership).

>[!TIP]
>
>Per informazioni dettagliate sulla gestione degli archivi in Cloud Manager, consulta [Archivi di Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).


### Convalidare la proprietà di un archivio GitHub privato {#validate-ownership}

Cloud Manager ora è a conoscenza del tuo archivio GitHub, ma deve ancora accedervi. Per concedere l’accesso, devi installare l’app Adobe GitHub e verificare di essere il proprietario dell’archivio specificato.

**Per convalidare la proprietà di un archivio GitHub privato:**

1. Dopo aver aggiunto il tuo archivio, segui i passaggi rimanenti nella finestra di dialogo **Convalida proprietà archivio privato**.

   ![Convalida delle proprietà dell’archivio privato](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

   |  | Descrizione |
   | --- | --- |
   | **Passaggio 1: app GitHub** | Cloud Manager utilizza un’app GitHub per interagire con l’archivio privato in modo sicuro.<br>· Un proprietario dell&#39;organizzazione GitHub deve installare l&#39;app che si trova in `https://github.com/apps/cloud-manager-for-aem` e concedere l&#39;accesso all&#39;archivio.<br>· Per informazioni dettagliate sull&#39;installazione e sulla concessione dell&#39;accesso, vedere la documentazione di GitHub. |
   | **Passaggio 2: file segreto** | Per migliorare la protezione, è necessario creare un file segreto nel ramo predefinito dell’archivio.<br>· Fare clic su **Genera**, quindi su **Conferma**. Cloud Manager genera il contenuto del file privato nel campo di testo **Contenuto file segreto**.<br>· Fare clic sull&#39;icona ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) per copiare il contenuto da tale campo. Il contenuto del file segreto verrà visualizzato una sola volta. Se non copiate il contenuto prima di chiudere questa finestra di dialogo, rigenerate il segreto. |

1. Crea un nuovo file nel ramo predefinito dell’archivio GitHub denominato:

   `.well-known/adobe/cloud-manager-challenge`

1. Incolla il contenuto del file segreto nel nuovo file appena creato e salvalo.

   Una volta installata l’app e che il file segreto esiste nell’archivio, continua il passaggio.

1. Nella finestra di dialogo **Convalida proprietà repository privato**, fare clic su **Convalida**.

L’app può essere installata e un file segreto può essere creato in qualsiasi ordine. Tuttavia, entrambi i passaggi devono essere completati prima di poter eseguire la convalida.

Fino alla convalida, l’archivio viene elencato con un’icona rossa, che indica che non è ancora stato convalidato e non può ancora essere utilizzato.

![Archivio non convalidato](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

La colonna **Tipo** nella tabella della pagina **Archivi** identifica gli archivi forniti da Adobe (**Adobe**) e i tuoi archivi privati (**GitHub**).

Se in un secondo momento dovrai tornare all&#39;archivio per completare la convalida, nella pagina **Archivi** fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) nella riga che rappresenta l&#39;archivio GitHub appena aggiunto. Nell&#39;elenco a discesa selezionare **Convalida proprietà**.



## Utilizzare archivi GitHub Cloud privati con Cloud Manager {#using}

Dopo la convalida dell’archivio GitHub in Cloud Manager, l’integrazione è completa. Puoi utilizzare l’archivio con Cloud Manager.

**Per utilizzare archivi GitHub Cloud privati con Cloud Manager:**

1. Quando crei una richiesta pull, viene avviata automaticamente una verifica GitHub.

   ![Verifiche GitHub](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. Per ogni richiesta pull, verrà creata automaticamente una [pipeline di qualità del codice full stack](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Tale pipeline viene avviata ogni volta che la richiesta pull viene aggiornata.

1. Il controllo GitHub rimane in esecuzione fino al completamento del controllo di qualità del codice. I risultati di qualità del codice sono propagati quindi alla verifica GitHub.

   ![Controlli di qualità del codice GitHub](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

Quando la richiesta di pull viene unita o chiusa, la pipeline di qualità del codice full stack creata viene eliminata automaticamente.

>[!TIP]
>
>Consulta [Annotazioni di controllo GitHub](github-annotations.md) per informazioni dettagliate sulle informazioni fornite tramite GitHub durante l&#39;esecuzione dei controlli delle richieste pull.

>[!TIP]
>
>Puoi controllare le pipeline create automaticamente per convalidare ogni richiesta pull in un archivio privato. Consulta la sezione [Configurazione verifica GitHub per archivi privati](github-check-config.md) per ulteriori informazioni.



## Associare archivi GitHub Cloud privati alle pipeline {#pipelines}

Gli archivi privati convalidati possono essere associati a [pipeline full-stack e front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).



## Note sull’utilizzo {#usage-notes}

* Le pipeline a livello web e di configurazione non sono supportate con gli archivi privati.
* Quando si utilizzano archivi privati su pipeline di produzione full stack, non viene creato e né inviato alcun tag Git.
* Se l’app GitHub Adobe viene rimossa dall’organizzazione GitHub, rimuove la funzione di convalida delle richieste pull per tutti gli archivi.
* Le pipeline che utilizzano archivi GitHub Cloud privati e il trigger di build &quot;on-commit&quot; non vengono avviati automaticamente quando un nuovo commit viene inviato al ramo selezionato.
* La [funzionalità di riutilizzo degli artefatti](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) non si applica agli archivi privati.
* Non è possibile sospendere la convalida della richiesta di pull utilizzando il controllo GitHub di Cloud Manager.
Se l’archivio GitHub viene convalidato in Cloud Manager, Cloud Manager tenta sempre di convalidare le richieste pull create per tale archivio.
* Se l’organizzazione GitHub dispone di restrizioni IP, crea un caso di supporto per ricevere l’elenco degli indirizzi IP consentiti.
