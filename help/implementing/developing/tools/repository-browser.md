---
title: Browser dell’archivio
seo-title: Repository Browser
description: Il browser dell’archivio fornisce una vista in sola lettura dell’archivio per tutti gli ambienti sui livelli di authoring, pubblicazione e anteprima.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---

# Browser dell’archivio {#repository-browser}

>[!NOTE]
>
>Il Browser dell’archivio è disponibile su AEM versione 6582 e successive.

>[!INFO]
>
>È inoltre possibile guardare [questo clip](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=it) per una breve introduzione video su come utilizzare il Browser dell&#39;archivio per eseguire il debug di AEM as a Cloud Service.

## Introduzione {#introduction}

Il browser dell’archivio è uno strumento per sviluppatori che fornisce una visualizzazione di sola lettura nell’archivio per tutti gli ambienti sui livelli di authoring, pubblicazione e anteprima. È progettato per facilitare la visualizzazione della struttura del contenuto e semplificare la visualizzazione o il debug del contenuto.

Accessibile da [AEM as a Cloud Service Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console), può essere utilizzato per sfogliare l&#39;archivio di un&#39;istanza di authoring o di pubblicazione per un ambiente selezionato.

### Prerequisiti di accesso {#access-prerequisites}

Per accedere ad AEM as a Cloud Service Developer Console o al browser dell’archivio devono essere soddisfatte le seguenti condizioni

Per accedere ad AEM as a Cloud Service Developer Console, vedi [Accesso a Developer Console](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#developer-console-access).

Per accedere al Browser dell’archivio, i requisiti sono gli stessi di AEM as a Cloud Service Developer Console (specificati sopra). Per visualizzare il contenuto del Browser dell’archivio per una particolare istanza:

* Istanze di authoring: gli utenti con il profilo di prodotto Utenti AEM per l&#39;**istanza di authoring** possono visualizzare il browser dell&#39;archivio con accesso in lettura minimo; le autorizzazioni dell&#39;utente vengono rispettate durante la navigazione nell&#39;archivio. Gli utenti con il profilo di prodotto per amministratori di AEM possono visualizzare il browser dell’archivio con accesso in lettura completo.

* Istanze di pubblicazione: gli utenti con il profilo di prodotto Utenti AEM per l&#39;**istanza di pubblicazione** possono visualizzare il browser dell&#39;archivio con un accesso di lettura minimo. Senza questo set di profili di prodotto, gli utenti potranno navigare come utenti anonimi e alcuni percorsi non verranno visualizzati a causa di autorizzazioni limitate.

Per ulteriori informazioni sulla configurazione delle autorizzazioni utente, consulta la [documentazione di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html?lang=it).

### Avvio del Browser dell’archivio {#launching-the-repository-browser}

Puoi avviare il browser dell’archivio seguendo la procedura riportata di seguito.

1. In Cloud Manager, fai clic sui tre punti accanto all&#39;ambiente desiderato e seleziona **Developer Console**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. Fare clic sulla scheda **Browser dell&#39;archivio**
1. Scegliere un pod corrispondente all&#39;autore, alla pubblicazione o all&#39;anteprima facendo clic sull&#39;elenco a discesa **Pod**.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Avviare il browser del repository facendo clic sul collegamento **Apri browser del repository** più in basso. Viene avviato il browser corrispondente a un’istanza rappresentativa (pod) per il livello scelto. Non è possibile controllare il pod specifico per il livello avviato.

## Funzioni {#features}

### Spostarsi nella gerarchia {#navigate-the-hierarchy}

È possibile utilizzare il riquadro di navigazione a sinistra per spostarsi nella gerarchia dei contenuti. Facendo clic su ogni cartella o nodo, vengono visualizzati i relativi elementi secondari. La struttura delle cartelle riflette la struttura Sling Resource, un super-set della struttura ad albero dei nodi JCR.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

In alternativa, è possibile passare direttamente a un percorso immettendolo nel campo **Percorso**, come illustrato di seguito. Questo percorso espande anche la sua posizione nella vista della gerarchia dei contenuti a sinistra.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Quando fai clic su una cartella a sinistra, il campo Percorso si popola automaticamente con la relativa posizione. Questa funzionalità è utile per copiare e incollare il valore per un utilizzo successivo.

Inoltre, quando fai clic su una cartella, l’URL viene modificato dinamicamente per includere il percorso di tale cartella. Questa funzionalità consente l’utilizzo di URL con segnalibro.

Per la pubblicazione, per impostazione predefinita, il Browser dell&#39;archivio visualizza solo il contenuto pubblico, pertanto alcune cartelle come `/conf` o `/home` non sono visibili.

Per rendere visibili tali posizioni, effettuare le seguenti operazioni.

1. Fai clic sui tre punti accanto all&#39;ambiente desiderato e seleziona **Gestisci accesso**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Trova l’istanza Publish, quindi fai clic su di essa

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Crea un profilo di prodotto per gli amministratori di pubblicazione. Nell&#39;esempio seguente, è denominato **DEV - AEM Administrators Publish**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Aggiungi al nuovo profilo di prodotto gli utenti appropriati, corrispondenti a coloro che dovrebbero essere in grado di navigare nel browser dell’archivio di pubblicazione con accesso completo

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Attendi alcuni minuti, quindi apri la console **AEM Author**
1. Aggiungere il gruppo corrispondente al nuovo profilo di prodotto come membro del gruppo dell&#39;amministratore facendo clic su **Strumenti - Protezione - Gruppi sull&#39;autore** e quindi sul gruppo **amministratori**. Quindi, aggiungete il gruppo come mostrato di seguito

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Attiva il gruppo **amministratori** e il nuovo gruppo **DEV - AEM Administrators Publish** in modo che diventino disponibili al momento della pubblicazione

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Come buona prassi di sicurezza, rimuovere il nuovo gruppo **DEV - AEM Administrators Publish** dal gruppo dell&#39;amministratore in **author** in modo che il nuovo gruppo sia isolato per la pubblicazione

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. Quando si accede al browser dell&#39;archivio per un&#39;istanza di pubblicazione, sono visibili tutte le cartelle, inclusi `/home` e `/conf`.

### Visualizza proprietà JCR {#view-jcr-properties}

Facendo clic su un nodo, le relative proprietà JCR vengono visualizzate nel riquadro di destra del browser di navigazione. Di seguito è riportato un esempio per il nodo `experience-fragments`.

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

Puoi anche utilizzare il browser dell’archivio per scaricare il contenuto. Nell&#39;esempio seguente, è possibile premere il collegamento **download** per scaricare `jcr:data` associato al nodo selezionato. Questa funzione è disponibile per tutte le proprietà binarie passando al nodo contenente la definizione della proprietà.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
