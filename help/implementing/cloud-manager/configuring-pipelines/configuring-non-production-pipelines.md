---
title: Configurazione delle pipeline non di produzione
description: Scopri come configurare le pipeline non di produzione per eseguire test sulla qualità del codice prima di distribuirle negli ambienti di produzione.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: aac397310babe1aa1e950c176459beaf665b72ce
workflow-type: ht
source-wordcount: '1369'
ht-degree: 100%

---


# Configurazione delle pipeline non di produzione {#configuring-non-production-pipelines}

Scopri come configurare le pipeline non di produzione per eseguire test sulla qualità del codice prima di distribuirle negli ambienti di produzione.

## Pipeline non di produzione {#non-production-pipelines}

Oltre alle [pipeline di produzione](#configuring-production-pipelines.md), che distribuiscono negli ambienti di staging e di produzione, per convalidare il codice è possibile configurare anche delle pipeline non di produzione.

Esistono due tipi di pipeline non di produzione:

* **Pipeline di qualità del codice**: eseguono controlli di qualità del codice in un ramo Git ed eseguono i passaggi di generazione e qualità del codice.
* **Pipeline di distribuzione**: oltre a eseguire i passaggi di generazione e qualità del codice analogamente alle pipeline di qualità del codice, queste pipeline distribuiscono il codice in un ambiente non di produzione.

>[!NOTE]
>
>È possibile [modificare le impostazioni della pipeline](managing-pipelines.md) dopo la configurazione iniziale.

## Aggiunta di una nuova pipeline non di produzione {#adding-non-production-pipeline}

Dopo aver configurato il programma e disporre di almeno un ambiente che utilizza l’interfaccia utente di Cloud Manager, puoi aggiungere una pipeline non di produzione seguendo la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Accedi alla scheda **Pipeline** dalla pagina Home di Cloud Manager. Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline non di produzione**.

   ![Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. Dalla scheda **Configurazione** della finestra di dialogo **Aggiungi pipeline non di produzione**, seleziona il tipo di pipeline non di produzione che desideri aggiungere.

   * **Pipeline di qualità del codice**: crea una pipeline che genera il codice, esegue test di unità e valuta la qualità del codice, ma NON la distribuisce.
   * **Pipeline di distribuzione**: crea una pipeline che genera il codice, esegue test di unità, valuta la qualità del codice e distribuisce in un ambiente.

   ![Finestra di dialogo Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Per identificare la pipeline, fornisci un **nome della pipeline non di produzione** con le seguenti informazioni aggiuntive.

   * **Trigger distribuzione**: quando si definiscono i trigger della distribuzione per avviare la pipeline, le opzioni disponibili sono le seguenti.

      * **Manuale**: per avviare la pipeline manualmente.
      * **Alla modifica Git**: per avviare la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo Git configurato. Con questa opzione è comunque possibile avviare la pipeline manualmente secondo necessità.

1. Se scegli di creare una **pipeline di distribuzione** dovrai inoltre definire il **comportamento degli errori di metriche importanti**.

   * **Chiedi ogni volta**: impostazione predefinita che richiede l’intervento manuale per tutti gli errori importanti.
   * **Interrompi subito**: selezionando questa opzione, la pipeline viene annullata ogni volta che si verifica un errore importante. In sostanza, quest’opzione simula un utente che rifiuta manualmente ogni errore.
   * **Continua immediatamente**: selezionando questa opzione, la pipeline avanza automaticamente ogni volta che si verifica un errore importante. In sostanza, quest’opzione simula un utente che approva manualmente ogni errore.

1. Fai clic su **Continua**.

1. Dalla scheda **Codice sorgente** della finestra di dialogo **Aggiungi pipeline non di produzione**, seleziona il tipo di codice da elaborare con la pipeline.

   * **[Codice front-end](#front-end-code)**
   * **[Codice full stack](#full-stack-code)**
   * **[Configurazione a livello web](#web-tier-config)**

I passaggi per completare la creazione della pipeline non di produzione variano a seconda dell’opzione **Codice sorgente** selezionata. Accedi ai collegamenti riportati qui sopra per passare alla sezione successiva del documento e completare la configurazione della pipeline.

### Codice front-end {#front-end-code}

Una pipeline del codice front-end distribuisce le build del codice front-end contenenti una o più applicazioni dell’interfaccia utente lato client. Per ulteriori informazioni su questo tipo di pipeline, consulta il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end).

Per completare la configurazione della pipeline non di produzione del codice front-end, segui la procedura riportata di seguito.

1. Nella scheda **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Ambienti di distribuzione idonei**: se la pipeline è di distribuzione, seleziona gli ambienti in cui eseguire la distribuzione.
   * **Archivio**: definisce l’archivio Git dal quale la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta il documento [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

   * **Ramo Git**: definisce il ramo della pipeline selezionata dal quale recuperare il codice.
      * Digitando i primi caratteri del nome del ramo, la funzione di completamento automatico del campo troverà i rami corrispondenti per supportare nella selezione.
   * **Posizione codice**: definisce il percorso nel ramo dell’archivio selezionato dal quale la pipeline deve recuperare il codice.

   ![Pipeline front-end](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. Fai clic su **Salva**.

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

### Codice full stack {#full-stack-code}

Una pipeline del codice full stack distribuisce simultaneamente le build del codice back-end e front-end contenenti una o più applicazioni server di AEM con la configurazione HTTPD/Dispatcher. Per ulteriori informazioni su questo tipo di pipeline, consulta il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline).

>[!NOTE]
>
>Se per l’ambiente selezionato esiste già una pipeline del codice full stack, la selezione viene disabilitata.

Per completare la configurazione della pipeline non di produzione del codice full stack, segui la procedura riportata di seguito.

1. Nella scheda **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Ambienti di distribuzione idonei**: se la pipeline è di distribuzione, seleziona gli ambienti in cui eseguire la distribuzione.
   * **Archivio**: definisce l’archivio Git dal quale la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta il documento [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

   * **Ramo Git**: definisce il ramo della pipeline selezionata dal quale recuperare il codice.
      * Digitando i primi caratteri del nome del ramo, la funzione di completamento automatico del campo troverà i rami corrispondenti per supportare nella selezione.
   * **Ignora configurazione a livello web**: se l’opzione è selezionata, la pipeline non distribuisce la configurazione a livello web.

   * **Pipeline**: se la tua pipeline non è di distribuzione, puoi scegliere di eseguire una fase di test. Controlla le opzioni che desideri abilitare in questa fase. Se non è selezionata nessuna delle opzioni, la fase di test non verrà visualizzata durante l’esecuzione della pipeline.

      * **Test funzionali del prodotto**: esegui [test funzionali del prodotto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) rispetto all’ambiente di sviluppo.
      * **Test funzionali personalizzato**: esegui [test funzionali personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) rispetto all’ambiente di sviluppo.
      * **Test personalizzati dell’interfaccia utente**: esegui [test personalizzati dell’interfaccia utente](/help/implementing/cloud-manager/ui-testing.md) per applicazioni personalizzate.

   ![Pipeline full stack](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Fai clic su **Salva**.

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

### Configurazione a livello web {#web-tier-config}

Una pipeline di configurazione a livello web distribuisce configurazioni HTTPD/Dispatcher. Per ulteriori informazioni su questo tipo di pipeline, consulta il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline).

>[!NOTE]
>
>Se per l’ambiente selezionato esiste già una pipeline del codice a livello web, la selezione viene disabilitata.

Per completare la configurazione della pipeline non di produzione del codice a livello web, segui la procedura riportata di seguito.

1. Nella scheda **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Ambienti di distribuzione idonei**: se la pipeline è di distribuzione, seleziona gli ambienti in cui eseguire la distribuzione.
   * **Archivio**: definisce l’archivio Git dal quale la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta il documento [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

   * **Ramo Git**: definisce il ramo della pipeline selezionata dal quale recuperare il codice.
   * **Posizione codice**: definisce il percorso nel ramo dell’archivio selezionato dal quale la pipeline deve recuperare il codice.
      * Per le pipeline di configurazione a livello web, in genere si tratta del percorso contenente le directory `conf.d`, `conf.dispatcher.d` e `opt-in`.
      * Ad esempio, se la struttura del progetto è stata generata dall’[archetipo del progetto AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) il percorso è `/dispatcher/src`.

   ![Pipeline a livello web](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. Fai clic su **Salva**.

>[!NOTE]
>
>Se già disponi di una pipeline full stack distribuita in un ambiente, creando una pipeline di configurazione a livello web per lo stesso ambiente la configurazione del livello web esistente nella pipeline full stack verrà ignorata.

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

## Sviluppo di Sites con la pipeline front-end {#developing-with-front-end-pipeline}

Con le pipeline front-end, i team di sviluppo front-end acquisiscono maggiore indipendenza e il processo di sviluppo può essere accelerato.

Per informazioni sul funzionamento di questo processo e alcune considerazioni per sfruttare al massimo il suo potenziale, consulta il documento [Sviluppo di Sites con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).

## Ignorare i pacchetti Dispatcher {#skip-dispatcher-packages}

Se desideri che i pacchetti dispatcher vengano generati come parte della pipeline, ma non che vengano pubblicati nell’archivio della build, puoi disabilitare la pubblicazione riducendo in tal modo la durata dell’esecuzione della pipeline.

Per disabilitare la pubblicazione dei pacchetti dispatcher, aggiungi la seguente configurazione tramite il file di progetto `pom.xml`. Si basa su una variabile di ambiente che funge da flag impostabile nel contenitore della build di Cloud Manager per definire quando ignorare i pacchetti dispatcher.

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
