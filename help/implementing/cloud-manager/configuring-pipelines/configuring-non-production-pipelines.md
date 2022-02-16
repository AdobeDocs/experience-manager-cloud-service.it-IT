---
title: Configurazione di pipeline non di produzione
description: Scopri come configurare le pipeline non di produzione per testare la qualità del codice prima di distribuirle negli ambienti di produzione.
index: true
source-git-commit: e2031cabfa06a4d55dfa3ec0a77d3d3b0f835f5b
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 1%

---


# Configurazione di pipeline non di produzione {#configuring-non-production-pipelines}

Scopri come configurare le pipeline non di produzione per testare la qualità del codice prima di distribuirle negli ambienti di produzione.

## Pipeline non di produzione {#non-production-pipelines}

Oltre a [gasdotti di produzione](#configuring-production-pipelines.md) che viene implementato in ambienti di staging e produzione, puoi anche impostare pipeline non di produzione per convalidare il codice.

Esistono due tipi di gasdotti non di produzione:

* **Pipeline di qualità del codice** - Questa funzione esegue la scansione del codice in un ramo git ed esegue i passaggi di creazione e qualità del codice.
* **Pipeline di distribuzione** - Oltre a eseguire la generazione e i passaggi di qualità del codice come le pipeline di qualità del codice, queste pipeline distribuiscono il codice in un ambiente non di produzione.

>[!NOTE]
>
>È possibile [modificare le impostazioni della pipeline](managing-pipelines.md) dopo la configurazione iniziale.

## Aggiunta di una nuova pipeline non di produzione {#adding-non-production-pipeline}

Dopo aver configurato il programma e disporre di almeno un ambiente utilizzando l’interfaccia utente di Cloud Manager, puoi aggiungere una pipeline non di produzione seguendo questi passaggi.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Accedere al **Tubi** scheda dalla schermata principale di Cloud Manager. Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline non di produzione**.

   ![Aggiungere una pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. Sulla **Configurazione** della scheda **Aggiungi pipeline non di produzione** seleziona il tipo di pipeline non di produzione con cui desideri aggiungere **Pipeline di qualità del codice** o **Pipeline di distribuzione**.

   ![Finestra di dialogo Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Fornisci un **Nome della pipeline non di produzione** per identificare la pipeline con le seguenti informazioni aggiuntive.

   * **Trigger distribuzione** - Quando definisci gli attivatori della distribuzione per avviare la pipeline, sono disponibili le seguenti opzioni.

      * **Manuale** - Utilizzare questa opzione per avviare manualmente la pipeline.
      * **Su modifiche Git** - Questa opzione avvia la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo git configurato. Con questa opzione, potete comunque avviare la pipeline manualmente come necessario.
   * **Comportamento di errori di metrica importanti** - Durante la configurazione o la modifica della pipeline, il **Gestione distribuzione** ha la possibilità di definire il comportamento della pipeline quando si verifica un errore importante in uno qualsiasi dei cancelli di qualità. Opzioni disponibili.

      * **Chiedi sempre** - Questa è l&#39;impostazione predefinita e richiede l&#39;intervento manuale su qualsiasi errore importante.
      * **Non riuscito immediatamente** - Se selezionata, la pipeline verrà annullata ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che rifiuta manualmente ogni errore.
      * **Continua immediatamente** - Se selezionata, la pipeline procede automaticamente ogni volta che si verifica un errore importante. In sostanza, questo sta simulando un utente che approva manualmente ogni errore.


1. Fai clic su **Continua**.

1. Sulla **Codice sorgente** della scheda **Aggiungi pipeline non di produzione** È necessario selezionare il tipo di codice che la pipeline deve elaborare.

   * **[Codice front-end](#front-end-code)**
   * **[Codice Stack Completo](#full-stack-code)**
   * **[Configurazione a livello web](#web-tier-config)**

I passaggi per completare la creazione della pipeline non di produzione variano a seconda dell’opzione per **Codice sorgente** selezionato. Segui i collegamenti sopra riportati per passare alla sezione successiva del documento per completare la configurazione della pipeline.

### Codice front-end {#front-end-code}

Una pipeline di codice front-end implementa build di codice front-end contenenti una o più applicazioni dell’interfaccia utente lato client. Vedere il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) per ulteriori informazioni su questo tipo di pipeline.

Per completare la configurazione della pipeline di non produzione del codice front-end, segui questi passaggi.

1. Sulla **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Ambienti di distribuzione idonei** - Se la pipeline è una pipeline di distribuzione, è necessario selezionare gli ambienti in cui distribuire.
   * **Archivio** - Questa opzione definisce da quale git repo la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Vedere il documento [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

   * **Ramo Git** - Questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice.
   * **Posizione codice** - Questa opzione definisce il percorso nel ramo dell’archivio selezionato da cui la pipeline deve recuperare il codice.

   ![Gasdotto front-end](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. Fai clic su **Salva**.

La pipeline viene salvata ed è ora possibile [gestire le pipeline](managing-pipelines.md) sulla **Tubi** scheda **Panoramica del programma** pagina.

### Codice Stack Completo {#full-stack-code}

Una pipeline di codice a stack completo distribuisce simultaneamente build di codice back-end e front-end contenenti una o più applicazioni server AEM insieme alla configurazione HTTPD/Dispatcher. Vedere il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) per ulteriori informazioni su questo tipo di pipeline.

>[!NOTE]
>
>Se per l’ambiente selezionato esiste già una pipeline di codice con stack completo, questa selezione verrà disabilitata.

Per completare la configurazione della pipeline di non produzione del codice full-stack, segui questi passaggi.

1. Sulla **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Ambienti di distribuzione idonei** - Se la pipeline è una pipeline di distribuzione, è necessario selezionare gli ambienti in cui distribuire.
   * **Archivio** - Questa opzione definisce da quale git repo la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Vedere il documento [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

   * **Ramo Git** - Questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice.
   * **Ignora configurazione livello web** -

   ![pipeline a stack completo](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Fai clic su **Salva**.

La pipeline viene salvata ed è ora possibile [gestire le pipeline](managing-pipelines.md) sulla **Tubi** scheda **Panoramica del programma** pagina.

### Configurazione a livello web {#web-tier-config}

Una pipeline di configurazione a livello web distribuisce configurazioni HTTPD/Dispatcher. Vedere il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) per ulteriori informazioni su questo tipo di pipeline.

>[!NOTE]
>
>Se per l’ambiente selezionato esiste già una pipeline di codice a livello web, questa selezione verrà disabilitata.

Per completare la configurazione della pipeline di non produzione del codice livello web, segui questi passaggi.

1. Sulla **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Ambienti di distribuzione idonei** - Se la pipeline è una pipeline di distribuzione, è necessario selezionare gli ambienti in cui distribuire.
   * **Archivio** - Questa opzione definisce da quale git repo la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Vedere il documento [Aggiunta e gestione di archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per scoprire come aggiungere e gestire archivi in Cloud Manager.

   * **Ramo Git** - Questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice.
   * **Posizione codice** - Questa opzione definisce il percorso nel ramo dell’archivio selezionato da cui la pipeline deve recuperare il codice.
      * Per le pipeline di configurazione livello web, in genere si tratta del percorso contenente `conf.d`, `conf.dispatcher.d`e `opt-in` directory.
      * Ad esempio, se la struttura del progetto è stata generata dal [Archetipo AEM progetto,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) il percorso sarebbe `/dispatcher/src`.

   ![pipeline a livello web](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. Fai clic su **Salva**.

>[!NOTE]
>
>Se disponi di una pipeline full-stack esistente che viene distribuita in un ambiente, la creazione di una pipeline di configurazione del livello web per lo stesso ambiente comporterà l’eliminazione della configurazione del livello web esistente nella pipeline full-stack.

La pipeline viene salvata ed è ora possibile [gestire le pipeline](managing-pipelines.md) sulla **Tubi** scheda **Panoramica del programma** pagina.

## Ignora pacchetti Dispatcher {#skip-dispatcher-packages}

Se desideri che i pacchetti del dispatcher siano generati come parte della pipeline, ma non desideri che vengano pubblicati per creare l’archiviazione, puoi disattivarli, riducendo la durata dell’esecuzione della pipeline.

Per disabilitare la pubblicazione dei pacchetti dispatcher, devi aggiungere la seguente configurazione tramite il tuo progetto `pom.xml` file. Si basa su una variabile di ambiente, che funge da flag impostabile nel contenitore di build di Cloud Manager per definire quando i pacchetti del dispatcher devono essere ignorati.

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
