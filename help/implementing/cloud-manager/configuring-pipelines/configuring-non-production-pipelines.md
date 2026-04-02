---
title: Aggiungere una pipeline non di produzione
description: Scopri come aggiungere una pipeline non di produzione per testare la qualità del codice prima di distribuirla negli ambienti di produzione.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 7663af90b17e4b9d9567041c3bed8e20465c87d9
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 20%

---


# Aggiungere una pipeline non di produzione {#configuring-non-production-pipelines}

Dopo aver configurato un programma e creato almeno un ambiente nell’interfaccia utente di Cloud Manager, puoi aggiungere pipeline non di produzione. Queste pipeline consentono di verificare la qualità del codice prima di distribuirle negli ambienti di produzione.

Per configurare le pipeline non di produzione, l&#39;utente deve avere il ruolo **[Responsabile dell&#39;implementazione](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**.

>[!NOTE]
>
>È possibile [modificare le impostazioni della pipeline](managing-pipelines.md) dopo la configurazione iniziale.

## Aggiungere una nuova pipeline non di produzione {#adding-non-production-pipeline}

Dopo aver configurato un programma e creato almeno un ambiente nell’interfaccia utente di Cloud Manager, puoi aggiungere pipeline non di produzione. Utilizza queste pipeline per testare la qualità del codice prima di implementarle negli ambienti di produzione.

**Per aggiungere una nuova pipeline non di produzione:**

1. Accedi a Cloud Manager dall’indirizzo [experience.adobe.com](https://experience.adobe.com).
1. Nella sezione **Accesso rapido**, fai clic su **Experience Manager**.
1. Nel pannello laterale a sinistra, fai clic su **Cloud Manager**.
1. Selezionare un&#39;organizzazione desiderata.
1. Nella console **Programmi** fare clic su un programma.
1. Nel pannello laterale sinistro, fai clic su **Pipeline**.
1. Nella pagina **Pipeline**, nell&#39;angolo superiore destro, fare clic su **Aggiungi pipeline** > **Aggiungi pipeline non di produzione**.

   ![Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. Nella scheda **Configurazione** della finestra di dialogo **Aggiungi pipeline non di produzione**, seleziona una delle seguenti pipeline non di produzione da creare:

   * **Pipeline di qualità del codice**: crea una pipeline che crea il codice su un ramo GIT, esegue unit test e valuta la qualità del codice senza distribuirlo in un ambiente.
   * **Pipeline di distribuzione**: crea una pipeline che genera il codice, esegue unit test, valuta la qualità del codice e distribuisce in un ambiente non di produzione.

   ![Finestra di dialogo Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Nella sezione **Configurazione pipeline**, digita una descrizione per la pipeline non di produzione nel campo **Nome pipeline non di produzione**.
1. Nella sezione **Opzioni di distribuzione** selezionare uno dei trigger di distribuzione seguenti che si desidera utilizzare:

   * **Manuale**: ti consente di avviare manualmente la pipeline.
   * **Cambiamenti su Git**: avvia la pipeline ogni volta che vengono aggiunti dei commit al ramo Git configurato. Con questa opzione, puoi comunque avviare la pipeline manualmente in base alle esigenze.

1. Selezionare il **comportamento relativo agli errori di metrica importanti** che si desidera utilizzare.

   * **Chiedi ogni volta**: questo comportamento è l’impostazione predefinita che richiede l’intervento manuale per tutti gli errori importanti.
   * **Interrompi subito**: selezionando questa opzione, la pipeline viene annullata ogni volta che si verifica un errore importante. In sostanza, emula un utente che rifiuta manualmente ogni errore.
   * **Continua immediatamente**: se questa opzione è selezionata, la pipeline procede automaticamente ogni volta che si verifica un errore importante. In sostanza, emula un utente che approva manualmente ogni errore.

1. Fai clic su **Continua**.

1. I passaggi rimanenti utilizzati per completare la configurazione della pipeline non di produzione dipendono dal tipo di codice sorgente scelto.
Nella scheda **Codice Source** della finestra di dialogo **Aggiungi pipeline non di produzione**, seleziona il tipo di codice da elaborare con la pipeline non di produzione.

   * **[Utilizzo codice full stack](#full-stack-code)**
   * **[Sto utilizzando la distribuzione di destinazione](#targeted-deployment)**

   Per ulteriori informazioni sui tipi di pipeline, consulta [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).


### Utilizzo il codice full stack {#full-stack-code}

Una pipeline del codice full stack distribuisce simultaneamente le build del codice back-end e front-end contenenti una o più applicazioni server di AEM con la configurazione HTTPD/Dispatcher.

>[!NOTE]
>
>Se per l’ambiente selezionato esiste una pipeline del codice full stack, la selezione verrà disabilitata.

Per completare la configurazione della pipeline non di produzione del codice full stack, effettua le seguenti operazioni:

1. Nella sezione **Codice Source**, definisci le seguenti opzioni.

   * **Ambienti di distribuzione idonei** - Disponibile solo quando si modifica una pipeline non di produzione. Se la pipeline è di distribuzione, seleziona gli ambienti in cui eseguire la distribuzione.
   * **Archivio**: dall&#39;elenco a discesa, scegliere l&#39;archivio Git utilizzato dalla pipeline come origine. Cloud Manager crea il codice dall’archivio scelto qui.

     >[!TIP]
     > 
     >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

   * **Ramo Git**: dall&#39;elenco a discesa, scegli il ramo nell&#39;archivio selezionato da cui deve essere generata la pipeline. Il valore predefinito è `main`. La pipeline utilizza il ramo scelto come origine per la generazione e la distribuzione. Se necessario, fare clic su **Aggiorna** per aggiornare l&#39;elenco dei rami disponibili per l&#39;archivio selezionato. Utilizza questa opzione se un ramo creato di recente non viene visualizzato nell’elenco.
   * **Strategia di compilazione**
      * **Build completa** - Genera tutti i moduli nell&#39;archivio ogni volta
      * BETA **Smart Build** - Genera solo moduli che sono stati modificati dopo l&#39;ultimo commit.<br>Ulteriori informazioni sull&#39;utilizzo di [Smart Build in una pipeline non di produzione](#about-smart-build-non-production-pipeline).

        >[!IMPORTANT]
        >
        >Smart Build è disponibile solo per le pipeline di qualità del codice e per le pipeline di distribuzione del codice full stack di sviluppo.

   * **Casella di controllo Ignora configurazione a livello web**: se selezionata, la pipeline non distribuisce la configurazione a livello web.

1. Nella sezione **Pipeline**, se la pipeline è di distribuzione, puoi scegliere di eseguire una fase di test. Seleziona le opzioni che desideri abilitare in questa fase. Se non è selezionata alcuna opzione, la fase di test non viene visualizzata durante l’esecuzione della pipeline.

   * **Test funzionali del prodotto** - Eseguire [test funzionali del prodotto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) nell&#39;ambiente di sviluppo.
   * **Test funzionali personalizzati** - Eseguire [test funzionali personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) nell&#39;ambiente di sviluppo.
   * **Test dell&#39;interfaccia utente personalizzati** - Eseguire [test dell&#39;interfaccia utente personalizzati](/help/implementing/cloud-manager/ui-testing.md) per le applicazioni personalizzate.
   * **Audit dell&#39;esperienza** - Esegui [Audit dell&#39;esperienza](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Pipeline full stack](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Fai clic su **Salva**.

La pipeline è stata salvata ed è ora possibile [gestire le pipeline]&#x200B;(managing-pipe
lines.md) nella scheda **Pipeline** della pagina **Panoramica del programma**.

### Utilizzo un’implementazione mirata {#targeted-deployment}

Una distribuzione mirata distribuisce il codice solo per parti selezionate dell’applicazione AEM. In tale distribuzione è possibile scegliere di **Includere** uno dei seguenti tipi di codice:

![Opzioni di distribuzione di destinazione](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment1.png)

<!--
* **Config** - Configure settings for various features in your AEM environment.
  * See [Using Config Pipelines](/help/operations/config-pipeline.md) for a list of supported configurations, which include log forwarding, purge-related maintenance tasks, and various CDN configurations, and to manage them in your repository so they are deployed properly.
  * When running a targeted deployment pipeline, configurations are deployed, provided they are saved to the environment, repository, and branch you defined in the pipeline.
  * At any time, there can only be one config pipeline per environment.
* **Configure Edge Delivery Services config pipeline** - Edge Delivery Configuration Pipelines do not have separate development, staging, and production environments. In AEM as a Cloud Service, changes move through development, stage, and production tiers. In contrast, an Edge Delivery Configuration Pipeline applies its configuration directly to all Edge Delivery Sites domains registered in Cloud Manager. To learn more, see [Add an Edge Delivery Pipeline](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).
-->


* **Codice front-end**: configura JavaScript e CSS per il front-end dell&#39;applicazione AEM.
   * Con le pipeline front-end, i team di sviluppo front-end acquisiscono maggiore indipendenza e il processo di sviluppo può essere accelerato.
   * Per informazioni sul funzionamento di questo processo e alcune considerazioni per sfruttare al massimo il suo potenziale, consulta il documento [Sviluppo di Sites con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
* **Configurazione a livello web**: configura le proprietà di Dispatcher per archiviare, elaborare e inviare pagine Web al client.
   * Per ulteriori dettagli, consulta il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines).
   * Se esiste una pipeline del codice a livello web per l’ambiente selezionato, questa selezione è disabilitata.
   * Se una pipeline full stack è già implementata in un ambiente, puoi comunque creare una pipeline di configurazione a livello web per lo stesso ambiente. In questo caso, Cloud Manager ignora la configurazione a livello web nella pipeline full stack.

     >[!NOTE]
     >
     >Le pipeline a livello web e di configurazione non sono supportate con gli archivi privati. Per informazioni dettagliate e l&#39;elenco completo delle limitazioni, vedere [Aggiunta di archivi privati in Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

<!--
The steps to complete the creation of your non-production, targeted deployment pipeline are the same once you choose a deployment type.

1. Choose which deployment type you require.

![Targeted deployment options](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

1. Define the **Eligible Deployment Environments**.

   * If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
-->

1. Nella sezione **Codice Source**, definisci le seguenti opzioni:

   * **Archivio** - Questa opzione definisce da quale archivio GIT la pipeline non di produzione deve recuperare il codice.

     >[!TIP]
     > 
     >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

   * **Ramo Git** - Questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice. Immetti i primi caratteri del nome del ramo: la funzione di completamento automatico di questo campo. trova i rami corrispondenti che puoi selezionare.
   * **Posizione codice**: definisce il percorso nel ramo dell’archivio selezionato dal quale la pipeline deve recuperare il codice.

<!--
   * **Pipeline** - For front-end non-production pipelines, you have the option to enable **[Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)**.
   
   ![Config pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)
-->

1. Se hai abilitato l&#39;audit dell&#39;esperienza, fai clic su **Continua** per passare alla scheda **Audit dell&#39;esperienza** in cui puoi definire i percorsi che devono sempre essere inclusi nell&#39;audit dell&#39;esperienza.

   * Se hai abilitato **Audit dell&#39;esperienza**, consulta il documento [Audit dell&#39;esperienza](/help/implementing/cloud-manager/reports/report-experience-audit.md) per informazioni dettagliate su come configurare.
   * In caso contrario, salta questo passaggio.

1. Fai clic su **Salva** per salvare la pipeline.

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.


## Informazioni sull’utilizzo di Smart Build in una pipeline non di produzione{#about-smart-build-non-production-pipeline}

**Smart Build** in Cloud Manager è una strategia di compilazione ottimizzata per le pipeline non di produzione. Smart Build riduce i tempi di generazione memorizzando nella cache i moduli e ricostruendo solo quelli che sono stati modificati dopo l’ultima esecuzione riuscita. I moduli invariati vengono riutilizzati dalla cache, mentre vengono ricostruiti solo i moduli modificati e le relative dipendenze, migliorando l’efficienza dei flussi di lavoro di sviluppo iterativi.

Smart Build è attualmente disponibile solo per:

* pipeline di qualità del codice.
* Sviluppare pipeline di distribuzione full stack.

>[!NOTE]
>
>La prima esecuzione dopo l’abilitazione di Smart Build si comporta come una Build completa perché la cache è vuota.

Si consiglia di utilizzare Smart Build nei seguenti casi:

* Stai sviluppando attivamente e apportando frequenti modifiche incrementali.
* Il progetto contiene più moduli Maven.
* Le build complete richiedono molto tempo.

Smart Build non è sempre ideale quando si dispone dei seguenti elementi:

* La build si basa principalmente su plug-in che eseguono operazioni al di fuori del grafico delle dipendenze di Maven.
* È necessaria la convalida completa della ricompilazione a ogni esecuzione.

### Comprendere le prestazioni della build{#smart-build-performance}

Il miglioramento delle prestazioni derivante dall’utilizzo di Smart Build dipende da diversi fattori, tra cui i seguenti:

* Il numero di moduli nel progetto.
* Frequenza e ambito delle modifiche al codice.
* La distribuzione delle dipendenze tra i moduli.

In generale, i progetti con molti moduli indipendenti possono vedere il miglioramento maggiore.

### Rinuncia alla cache per modulo{#smart-build-cache-optout}

Smart Build fornisce un controllo dettagliato che consente di disabilitare la memorizzazione nella cache per moduli specifici. Questa funzionalità è utile quando alcuni moduli:

* Utilizzare i plug-in, ad esempio `exec-maven-plugin` o `maven-antrun-plugin`.
* Eseguire operazioni sui file non tracciate dalle dipendenze Maven.
* Il contenuto nella cache produce risultati incoerenti.

### Disattiva la memorizzazione in cache per un modulo{#smart-build-disable-caching}

È possibile aggiungere la seguente proprietà al `pom.xml` del modulo interessato:

```xml
<properties>
  <maven.build.cache.enabled>false</maven.build.cache.enabled>
</properties>
```

Questa sintassi forza la ricostruzione del modulo su ogni esecuzione della pipeline, mentre altri moduli continuano a beneficiare della memorizzazione in cache.

### Limitazioni e considerazioni sull’utilizzo di Smart Build{#smart-build-limitations}

Quando usi Smart Build, tieni presente quanto segue:

* Smart Build si basa sull’analisi delle dipendenze Maven.
* Le modifiche che non rientrano nel grafico delle dipendenze potrebbero non attivare le ricompilazioni.
* Alcuni plug-in potrebbero non essere completamente compatibili con il caching.
* Puoi tornare a **Build completa** in qualsiasi momento modificando la pipeline non di produzione.

Se si verifica un comportamento di compilazione imprevisto, è consigliabile disabilitare la memorizzazione nella cache per moduli specifici o cambiare temporaneamente la strategia di compilazione in **Build completa**.

### Risoluzione dei problemi di Smart Build{#smart-build-troubleshoot}

| Problema | Soluzioni consigliate |
| --- | --- |
| I risultati della build non sono coerenti | · Disattiva la memorizzazione in cache per i moduli interessati.<br>· Verificare il comportamento del plug-in, in particolare `exec`/`antrun`. |
| Nessun miglioramento delle prestazioni | · Verificare che si siano verificate più esecuzioni (riscaldamento della cache).<br>· Verificare se la maggior parte dei moduli cambia frequentemente. |
| Artefatti imprevisti o modifiche mancanti | · Verifica se le modifiche non rientrano nel tracciamento delle dipendenze Maven.<br>· Utilizza **Build completa** per la verifica. |

Consulta [Aggiungere una pipeline non di produzione](#adding-non-production-pipeline) per abilitare Smart Build.











<!--
## Add a non-production pipeline {#adding-non-production-pipeline}

Once you have set up your program and have at least one environment using the Cloud Manager UI, you are ready to add a non-production pipeline by following these steps.

1. Sign into Cloud Manager at [experiece.adobe.com](https://experience.adobe.com).
1. In the **Quick access** section, click **Experience Manager**.
1. In the left side panel, click **Cloud Manager**.
1. Select an organization that you want.
1. On the **My Programs** console, click a program. 

1. Access the **Pipelines** card from the Cloud Manager home screen. Click **+Add** and select **Add Non-Production Pipeline**. 

   ![Add non-production pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. On the **Configuration** tab of the **Add Non-Production Pipeline** dialog, select the type of non-production pipeline you with to add.

   * **Code Quality Pipeline** - Create a pipeline that builds your code, runs unit tests, and evaluates code quality but does NOT deploy.
   * **Deployment Pipeline** - Create a pipeline that builds your code, runs unit tests, evaluates code quality, and deploys to an environment.

   ![Add Non-Production pipeline dialog](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Provide a **Non-Production Pipeline Name** to identify your pipeline along with the following additional information.

   * **Deployment Trigger** - You have the following options when defining the deployment triggers to start the pipeline.
   
     * **Manual** - Use this option to start the pipeline manually.
     * **On Git Changes** - This option starts the CI/CD pipeline whenever commits are added to the configured Git branch. With this option, you can still start the pipeline manually as required.

1. If you choose to create a **Deployment Pipeline**, you must also define the **Important Metric Failures Behavior**.

   * **Ask every time** - This behavior is the default setting and requires manual intervention on any important failure.
   * **Fail Immediately** - If selected, the pipeline is canceled whenever an important failure occurs. It is essentially emulating a user manually rejecting each failure.
   * **Continue Immediately** - If selected, the pipeline procedes automatically whenever an important failure occurs. It is essentially emulating a user manually approving each failure.

1. Click **Continue**.

1. On the **Source Code** tab of the **Add Non-Production Pipeline** dialog, you must select which type of code the pipeline should process.

   * **[Full Stack Code](#full-stack-code)**
   * **[Targeted deployment](#targeted-deployment)**

See [CI/CD Pipelines](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) for more information about the types of pipelines.

The steps to complete the creation of your non-production pipeline vary depending on the type of source code you selected. Follow the links above to jump to the next section of this document so you can complete the configuration of your pipeline.

### Full Stack Code {#full-stack-code}

A full-stack code pipeline simultaneously deploys back-end and front-end code builds containing one or more AEM server applications along with HTTPD/Dispatcher configuration.

>[!NOTE]
>
>If a full-stack code pipeline exists for the selected environment, this selection is disabled.

To finish the configuration of the full-stack code non-production pipeline, follow these steps.

1. On the **Source Code** tab, you must define the following options.

   * **Eligible Deployment Environments** - If your pipeline is a deployment pipeline, you must select to which environments it should deploy.
   * **Repository** - This option defines from which git repo that the pipeline should retrieve the code.

   >[!TIP]
   > 
   >See [Adding and Managing Repositories](/help/implementing/cloud-manager/managing-code/managing-repositories.md) so you can learn how to add and manage repositories in Cloud Manager.

   * **Git Branch** - This option defines from which branch in the selected pipeline should retrieve the code.
     * Enter the first few characters of the branch name and the auto-complete feature of this field. It helps you find the matching branches that you can select.
   * **Ignore Web Tier Configuration** - When checked, the pipeline does not deploy your web tier configuration.
   * **Pipeline** - If your pipeline is a deployment pipeline, you can choose to run a testing phase. Check the options that you want to enable in this phase. If none of the options are selected, the testing phase is not displayed during the pipeline's run.

     * **Product Functional Testing** - Execute [product functional tests](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) against the development environment.
     * **Custom Functional Testing** - Execute [custom functional tests](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) against the development environment.
     * **Custom UI Testing** - Execute [custom UI tests](/help/implementing/cloud-manager/ui-testing.md) for custom applications.
     * **Experience Audit** - Execute [Experience Audit](/help/implementing/cloud-manager/reports/report-experience-audit.md)

   ![Full-stack pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Click **Save**.

The pipeline is saved and you can now [manage your pipelines](managing-pipelines.md) on the **Pipelines** card on the **Program Overview** page.

-->



## Escludi pacchetti Dispatcher {#exclude-dispatcher-packages}

Se desideri che i pacchetti Dispatcher siano generati nella pipeline ma non caricati nell’archiviazione della build, disabilita la pubblicazione. In questo modo si può ridurre il tempo di esecuzione della pipeline.

Aggiungere la seguente configurazione al file del progetto `pom.xml` per disabilitare la pubblicazione dei pacchetti Dispatcher. Imposta una variabile di ambiente nel contenitore della build Cloud Manager per segnalare quando ignorare i pacchetti Dispatcher. La pipeline legge questo flag e li ignora di conseguenza.

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
