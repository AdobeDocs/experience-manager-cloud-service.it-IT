---
title: Browser dell’archivio
seo-title: Repository Browser
description: Il browser dell’archivio fornisce una vista in sola lettura dell’archivio per tutti gli ambienti sui livelli di authoring, pubblicazione e anteprima.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 2%

---

# Browser dell’archivio {#repository-browser}

>[!NOTE]
>
>Il Browser dell’archivio è disponibile sulle versioni 6582 e successive dell’AEM.

>[!INFO]
>
>Puoi anche guardare [questo clip](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) per un rapido video introduttivo su come utilizzare il Browser dell’archivio per eseguire il debug di AEM as a Cloud Service.

## Introduzione {#introduction}

Il browser dell’archivio è uno strumento per sviluppatori che fornisce una visualizzazione di sola lettura nell’archivio per tutti gli ambienti sui livelli di authoring, pubblicazione e anteprima. È progettato per facilitare la visualizzazione della struttura del contenuto e semplificare la visualizzazione o il debug del contenuto.

Accessibile dalla Console per sviluppatori, può essere utilizzato per sfogliare l’archivio di un’istanza di authoring o pubblicazione per un ambiente selezionato.

### Prerequisiti di accesso {#access-prerequisites}

Per accedere a Console sviluppatori o al browser dell’archivio devono essere soddisfatte le seguenti condizioni

Per accedere a Console sviluppatori:

* Per i programmi di produzione, gli utenti devono disporre di **Cloud Manager - Ruolo Sviluppatore** nell’Admin Console
* Per i programmi sandbox, è disponibile per qualsiasi utente con un profilo di prodotto che consente di accedere a AEM as a Cloud Service.

Per accedere al Browser dell’archivio:

* Gli utenti devono disporre di **Cloud Manager - Sviluppatore** Ruolo nell’Admin Console per visualizzare le istanze Author e Publish.
* Inoltre, per l’autore, gli utenti con il profilo di prodotto Utenti AEM possono visualizzare il browser dell’archivio con un accesso in lettura minimo; le autorizzazioni dell’utente vengono rispettate durante la navigazione nell’archivio. Gli utenti con il profilo di prodotto per amministratori dell’AEM possono visualizzare il browser dell’archivio con accesso in lettura completo.

Per ulteriori informazioni sulla configurazione delle autorizzazioni utente, consulta [Documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html).

### Avvio del Browser dell’archivio {#launching-the-repository-browser}

Puoi avviare il browser dell’archivio seguendo la procedura riportata di seguito.

1. In Cloud Manager, fai clic sui tre punti accanto all’ambiente desiderato e seleziona **Console per sviluppatori**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. Quindi, fai clic su **Browser dell’archivio** scheda
1. Scegli un pod corrispondente all’autore, alla pubblicazione o all’anteprima facendo clic sul pulsante **Pod** elenco a discesa.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Avvia il browser dell’archivio facendo clic sul pulsante **Apri Browser Archivio** collegamento più in basso. Viene avviato il browser corrispondente a un’istanza rappresentativa (pod) per il livello scelto. Non è possibile controllare il pod specifico per il livello avviato.

## Funzioni {#features}

### Spostarsi nella gerarchia {#navigate-the-hierarchy}

È possibile utilizzare il riquadro di navigazione a sinistra per spostarsi nella gerarchia dei contenuti. Facendo clic su ogni cartella o nodo, vengono visualizzati i relativi elementi secondari. La struttura delle cartelle riflette la struttura Sling Resource, un super-set della struttura ad albero dei nodi JCR.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

In alternativa, potete passare direttamente a un tracciato immettendolo nella **Percorso** come mostrato di seguito. Questo percorso espande anche la sua posizione nella vista della gerarchia dei contenuti a sinistra.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Quando fai clic su una cartella a sinistra, il campo Percorso si popola automaticamente con la relativa posizione. Questa funzionalità è utile per copiare e incollare il valore per un utilizzo successivo.

Inoltre, quando fai clic su una cartella, l’URL viene modificato dinamicamente per includere il percorso di tale cartella. Questa funzionalità consente l’utilizzo di URL con segnalibro.

Per la pubblicazione, per impostazione predefinita, il Browser dell’archivio mostra solo il contenuto pubblico, pertanto alcune cartelle come `/conf` o `/home` non sono visibili.

Per rendere visibili tali posizioni, effettuare le seguenti operazioni.

1. Fai clic sui tre punti accanto all’ambiente desiderato e seleziona **Gestisci accesso**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Trova l’istanza Publish, quindi fai clic su di essa

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Crea un profilo di prodotto per gli amministratori di pubblicazione. Nell’esempio seguente, viene chiamato **DEV - Pubblicazione per amministratori AEM**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Aggiungi al nuovo profilo di prodotto gli utenti appropriati, corrispondenti a coloro che dovrebbero essere in grado di navigare nel browser dell’archivio di pubblicazione con accesso completo

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Attendere alcuni minuti, quindi aprire **Autore AEM** console
1. Aggiungi il gruppo corrispondente al nuovo profilo di prodotto come membro del gruppo dell’amministratore facendo clic su **Strumenti - Sicurezza - Gruppi sull’autore**, quindi facendo clic su **amministratori** gruppo. Quindi, aggiungete il gruppo come mostrato di seguito

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Attiva il **amministratori** e il nuovo **DEV - Pubblicazione per amministratori AEM** in modo che diventino disponibili al momento della pubblicazione

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Per motivi di sicurezza, è consigliabile rimuovere il nuovo **DEV - Pubblicazione per amministratori AEM** gruppo dal gruppo dell&#39;amministratore il **autore** in modo che il nuovo gruppo sia isolato per la pubblicazione

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Quando si accede al browser dell’archivio per un’istanza di pubblicazione, sono visibili tutte le cartelle, incluse `/home` e `/conf`.

### Visualizza proprietà JCR {#view-jcr-properties}

Facendo clic su un nodo, le relative proprietà JCR vengono visualizzate nel riquadro di destra del browser di navigazione. Di seguito è riportato un esempio per `experience-fragments` nodo.

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### Visualizza contenuto {#view-content}

Puoi utilizzare il browser dell’archivio per visualizzare il contenuto. Fai clic su una risorsa nel riquadro di navigazione per aprire un’anteprima sul lato destro del browser, sotto una scheda denominata dopo la rispettiva risorsa.

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

L’anteprima è disponibile per i seguenti tipi di immagini:

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* icona x
* tiff

E per i seguenti tipi mime basati su testo:

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### Scarica contenuto {#download-content}

Puoi anche utilizzare il browser dell’archivio per scaricare il contenuto. Nell’esempio seguente, puoi premere il tasto **scaricare** collegamento per scaricare `jcr:data` associato al nodo selezionato. Questa funzione è disponibile per tutte le proprietà binarie passando al nodo contenente la definizione della proprietà.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
