---
title: Browser dell’archivio
seo-title: Repository Browser
description: Il browser del repository fornisce una visualizzazione in sola lettura nell'archivio per tutti gli ambienti sui livelli di authoring, pubblicazione e anteprima.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: b4d28a0c827fb07d6f731118078ecdf448e2f58b
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 2%

---

# Browser dell’archivio {#repository-browser}

>[!NOTE]
>
>Il browser Repository è disponibile nelle versioni AEM 6582 e successive.

>[!INFO]
>
>Puoi anche guardare [questa clip](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) per una rapida introduzione video su come utilizzare il browser Repository per eseguire il debug AEM as a Cloud Service.

## Introduzione {#introduction}

Il browser dell’archivio è uno strumento per sviluppatori che fornisce una visualizzazione in sola lettura nell’archivio per tutti gli ambienti sui livelli di authoring, pubblicazione e anteprima. È progettato per facilitare la visualizzazione della struttura del contenuto al fine di facilitare la visualizzazione o il debug del contenuto.

Accessibile da Developer Console, può essere utilizzato per sfogliare l’archivio di un’istanza di authoring o pubblicazione per un ambiente selezionato.

### Prerequisiti per l’accesso {#access-prerequisites}

Per accedere alla Console per sviluppatori o al browser Repository è necessario soddisfare le seguenti condizioni

Per accedere alla Console per sviluppatori:

* Per i programmi di produzione, gli utenti devono avere **Cloud Manager - Ruolo sviluppatore** nell&#39;Admin Console
* Per i programmi sandbox, è disponibile per qualsiasi utente con un profilo di prodotto che consente loro di accedere a AEM as a Cloud Service.

Per accedere al browser del repository:

* Gli utenti devono avere **Cloud Manager - Sviluppatore** Ruolo nell’Admin Console per visualizzare le istanze Author e Publish .
* Inoltre, per l&#39;autore, gli utenti con il profilo di prodotto Utenti AEM possono visualizzare il browser del repository con accesso in lettura minimo; le autorizzazioni dell&#39;utente vengono rispettate quando si naviga nell&#39;archivio. Gli utenti con il profilo di prodotto Amministratori AEM possono visualizzare il browser del repository con accesso in lettura completo.

Per ulteriori informazioni sulla configurazione delle autorizzazioni utente, consulta la [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Avvio del browser del repository {#launching-the-repository-browser}

Il browser del repository può essere avviato seguendo i passaggi seguenti.

1. In Cloud Manager, fai clic sui tre punti accanto all’ambiente desiderato e seleziona **Console per sviluppatori**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. Fai clic su **Browser del repository** scheda
1. Scegli un pod corrispondente all’autore, alla pubblicazione o all’anteprima facendo clic sul pulsante **Pod** elenco a discesa.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Avvia il browser del repository facendo clic sul **Apri browser Repository** link più giù. Verrà avviato il browser corrispondente a un’istanza rappresentativa (pod) per il livello scelto. Verrà avviato il browser corrispondente a un’istanza rappresentativa (pod) per il livello scelto. Non è possibile controllare il pod specifico per quel livello avviato.

## Funzioni {#features}

### Spostarsi nella gerarchia {#navigate-the-hierarchy}

È possibile utilizzare il riquadro di navigazione a sinistra per spostarsi nella gerarchia dei contenuti. Facendo clic su ciascuna cartella o nodo vengono visualizzati i relativi elementi secondari. La struttura delle cartelle riflette la struttura Sling Resource, che è un super-set della struttura del nodo JCR.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

<!-- Alexandru: temporarily commenting this out, please don't delete. 

Alternatively, you can navigate directly to a path by entering it in the **Path** field, as shown below. This will also expand its location in the content hierarcy view on the left.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Whenever you click a folder on the left, the Path field automatically populates with its location. This is useful for copying and pasting the value for later usage.

Additionally, when you click on a folder, the URL is dynamically modified to include the path to that folder. This allows for bookmarkable URLs.

-->

Per la pubblicazione, per impostazione predefinita, il browser Repository mostrerà solo contenuto pubblico, quindi alcune cartelle come `/conf` o `/home` non sarà visibile.

Per rendere tali posizioni visibili, è necessario seguire la procedura seguente.

1. Fai clic sui tre punti accanto all’ambiente desiderato e seleziona **Gestisci accesso**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Trova la tua istanza di pubblicazione, quindi fai clic su di essa

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Crea un nuovo profilo di prodotto per gli amministratori di pubblicazione. Nell’esempio seguente, si chiama **DEV - Pubblicazione amministratori AEM**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Aggiungi gli utenti appropriati, corrispondenti a chi deve essere in grado di navigare nel browser dell’archivio di pubblicazione con accesso completo, al nuovo profilo di prodotto

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Attendi alcuni minuti, quindi apri il **autore AEM** console
1. Aggiungi il gruppo corrispondente al nuovo profilo di prodotto come membro del gruppo di amministratori . Per eseguire questa operazione, fai clic su **Strumenti - Sicurezza - Gruppi sull&#39;autore**, quindi facendo clic sul pulsante **amministratori** gruppo. Quindi, aggiungi il gruppo come mostrato di seguito

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Attiva la **amministratori** e il nuovo **DEV - Pubblicazione amministratori AEM** in modo che siano disponibili al momento della pubblicazione

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Come buona pratica per la sicurezza, rimuovi il nuovo **DEV - Pubblicazione amministratori AEM** dal gruppo amministratori su **autore** quindi il nuovo gruppo è isolato per pubblicare

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Quando accedi al browser del repository per un&#39;istanza di pubblicazione, tutte le cartelle sono visibili, tra cui `/home` e `/conf`.

### Visualizza proprietà JCR {#view-jcr-properties}

Facendo clic su un nodo verranno visualizzate le relative proprietà JCR nel riquadro a destra del browser di navigazione. Di seguito è riportato un esempio per `experience-fragments` nodo.

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### Visualizza contenuto {#view-content}

Puoi utilizzare il browser del repository per visualizzare il contenuto facendo clic su una risorsa nel riquadro di navigazione. Viene visualizzata un’anteprima sul lato destro del browser, sotto una scheda denominata per la relativa risorsa.

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

L’anteprima è attualmente disponibile per i tipi di immagine nell’elenco seguente:

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* Web
* bmp
* x-icon
* sciocco

E per i seguenti tipi di mime basati su testo:

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### Download del contenuto {#download-content}

È inoltre possibile utilizzare il browser del repository per scaricare i contenuti. Nell’esempio seguente, puoi premere il pulsante **scaricare** collegamento per scaricare `jcr:data` associato al nodo selezionato. Questa funzione è disponibile per tutte le proprietà binarie passando al nodo contenente la definizione della proprietà.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
