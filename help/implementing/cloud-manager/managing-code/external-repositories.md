---
title: Aggiungere archivi esterni in Cloud Manager (Early Adopter)
description: Scopri come aggiungere un archivio esterno in Cloud Manager. Cloud Manager supporta l’integrazione con gli archivi GitHub, GitLab e Bitbucket.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 4%

---


# Aggiungere archivi esterni in Cloud Manager {#external-repositories}

Scopri come aggiungere un archivio esterno in Cloud Manager. Cloud Manager supporta l’integrazione con gli archivi GitHub, GitLab e Bitbucket.

>[!NOTE]
>
>Questa funzionalità è disponibile solo per [il programma di adozione anticipata](/help/implementing/cloud-manager/release-notes/current.md#early-adoption).

## Configurare un archivio esterno

La configurazione di un archivio esterno in Cloud Manager consiste di tre passaggi:

1. [Aggiungere un repository esterno](#add-external-repo) a un programma selezionato.
1. Fornisci un token di accesso all’archivio esterno.
1. Convalida la proprietà dell’archivio GitHub privato.


## Aggiungere un archivio esterno {#add-ext-repo}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[Programmi personali](/help/implementing/cloud-manager/navigation.md#my-programs)** selezionare il programma a cui si desidera collegare un repository esterno.

1. Nel menu laterale, in **Servizi**, seleziona ![Icona cartella](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Archivi**.

   ![Pagina Archivi](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. Nell&#39;angolo superiore destro della pagina **Archivi** fare clic su **Aggiungi archivio**.

1. Nella finestra di dialogo **Aggiungi archivio**, seleziona **Archivio privato** per collegare un archivio Git esterno al programma.

   ![Aggiungi un archivio personale](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. In ciascun campo, fornisci i seguenti dettagli sull’archivio:

   | Campo | Descrizione |
   | --- | --- |
   | **Nome archivio** | Obbligatorio. Un nome espressivo per il nuovo archivio. |
   | **URL archivio** | Obbligatorio. URL dell’archivio.<br><br> Se utilizzi un archivio ospitato da GitHub, il percorso deve terminare in `.git`.<br>Ad esempio, *`https://github.com/org-name/repo-name.git`* (il percorso URL è solo a scopo illustrativo).<br><br>Se si utilizza un repository esterno, è necessario utilizzare il seguente formato di percorso URL:<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> o<br>`https://self-hosted-domain/org-name/repo-name.git`<br>E corrispondere al fornitore Git. |
   | S **Seleziona tipo di archivio** | Obbligatorio. Selezionare il tipo di repository in uso: **GitHub**, **GitLab** o **BitBucket**. Se il percorso URL dell’archivio precedente include il nome del fornitore Git, ad esempio GitLab o Bitbucket, il tipo di archivio è già preselezionato. |
   | **Descrizione** | Facoltativo. Descrizione dettagliata dell’archivio. |

1. Seleziona **Salva** per aggiungere l&#39;archivio.

1. Nella finestra di dialogo **Convalida proprietà archivio privato**, fornisci un token di accesso per convalidare la proprietà dell&#39;archivio esterno in modo da potervi accedere.

   ![Selezione di un token di accesso esistente per un repository](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *Selezione di un token di accesso esistente per un archivio BitBucket.*

   | Tipo di token | Descrizione |
   | --- | --- |
   | **Usa token di accesso esistente** | Se hai già fornito un token di accesso all’archivio per la tua organizzazione e hai accesso a più archivi, puoi selezionare un token esistente. Utilizza l&#39;elenco a discesa **Nome token** per scegliere il token da applicare all&#39;archivio. In caso contrario, aggiungi un nuovo token di accesso. |
   | **Aggiungi nuovo token di accesso** | **Tipo di archivio: GitHub**<br>· Nel campo di testo **Nome token**, digita un nome per il token di accesso che stai creando.<br>· Creare un token di accesso personale seguendo le istruzioni riportate nella [documentazione GitHub](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).<br>· Autorizzazioni richieste:<br>  · `Read access to metadata`.<br>  · `Read and write access to code and pull requests`.<br>· Nel campo **Token di accesso**, incolla il token appena creato. |
   |  | **Tipo di archivio: GitLab**<br>· Nel campo di testo **Nome token**, digita un nome per il token di accesso che stai creando.<br>· Creare un token di accesso personale seguendo le istruzioni riportate nella [documentazione GitLab](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html).<br>· Autorizzazioni richieste:<br>  · `api`<br>  · `read_api`<br>  · `read_repository`<br>  · `write_repository`<br>· Nel campo **Token di accesso**, incolla il token appena creato. |
   |  | **Tipo di archivio: Bitbucket**<br>· Nel campo di testo **Nome token**, digitare un nome per il token di accesso che si sta creando.<br>· Crea un token di accesso all&#39;archivio utilizzando la [documentazione Bitbucket](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/).<br>· Autorizzazioni richieste:<br>  · `Read and write access to code and pull requests`. |

   >[!NOTE]
   >
   >La funzionalità **Aggiungi nuovo token di accesso** è attualmente in fase di adozione anticipata. Sono in fase di pianificazione ulteriori funzionalità. Di conseguenza, le autorizzazioni richieste per i token di accesso potrebbero cambiare. Inoltre, è possibile aggiornare l’interfaccia utente per la gestione dei token, includendo potenzialmente funzionalità quali le date di scadenza dei token. Inoltre, controlli automatici per garantire che i token collegati agli archivi rimangano validi.

1. Fare clic su **Convalida**.

Dopo la convalida, l’archivio esterno è pronto per essere utilizzato e collegato a una pipeline.

## Collegare un archivio esterno convalidato a una pipeline {#validate-ext-repo}

1. Aggiungere o modificare una pipeline:
   * [Aggiungere una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Aggiungere una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [Modificare una pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   ![Archivio del codice sorgente della pipeline e ramo Git](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *Finestra di dialogo Aggiungi pipeline non di produzione con l&#39;archivio selezionato e il ramo Git,*

1. Quando aggiungi o modifichi una pipeline, per specificare il percorso **Codice Source** per la pipeline nuova o esistente, scegli l&#39;archivio esterno che desideri utilizzare dall&#39;elenco a discesa **Archivio**.

1. Nell&#39;elenco a discesa **Ramo Git** selezionare il ramo come origine per la pipeline.

1. Fai clic su **Salva**.


>[!TIP]
>
>Per informazioni dettagliate sulla gestione degli archivi in Cloud Manager, consulta [Archivi di Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).


## Limitazioni

* Gli archivi esterni non possono essere collegati alle pipeline di configurazione.
* Pipeline che utilizzano archivi esterni (esclusi gli archivi ospitati da GitHub) e l&#39;opzione **Trigger distribuzione** [!UICONTROL **In caso di modifiche Git**], i trigger non vengono avviati automaticamente. Devono essere avviati manualmente.




