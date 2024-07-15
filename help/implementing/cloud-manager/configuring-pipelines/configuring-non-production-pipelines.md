---
title: Configurazione delle pipeline non di produzione
description: Scopri come configurare le pipeline non di produzione per eseguire test sulla qualità del codice prima di distribuirle negli ambienti di produzione.
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: a5179851af8ec88e23d79a74265b10cbce2d50f1
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 75%

---


# Configurazione delle pipeline non di produzione {#configuring-non-production-pipelines}

Scopri come configurare le pipeline non di produzione per eseguire test sulla qualità del codice prima di distribuirle negli ambienti di produzione.

Per configurare le pipeline non di produzione, l&#39;utente deve avere il ruolo **[Responsabile dell&#39;implementazione](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**.

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

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Accedi alla scheda **Pipeline** dalla pagina Home di Cloud Manager. Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline non di produzione**.

   ![Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. Dalla scheda **Configurazione** della finestra di dialogo **Aggiungi pipeline non di produzione**, seleziona il tipo di pipeline non di produzione che desideri aggiungere.

   * **Pipeline di qualità del codice**: crea una pipeline che genera il codice, esegue test di unità e valuta la qualità del codice, ma NON la distribuisce.
   * **Pipeline di distribuzione**: crea una pipeline che genera il codice, esegue test di unità, valuta la qualità del codice e distribuisce in un ambiente.

   ![Finestra di dialogo Aggiungi pipeline non di produzione](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Per identificare la pipeline, fornisci un **nome della pipeline non di produzione** con le seguenti informazioni aggiuntive.

   * **Trigger distribuzione**: quando si definiscono i trigger della distribuzione per avviare la pipeline, le opzioni disponibili sono le seguenti.

      * **Manuale**: per avviare la pipeline manualmente.
      * **Cambiamenti su Git**: questa opzione avvia la pipeline CI/CD ogni volta che vengono aggiunti dei commit al ramo Git configurato. Con questa opzione è comunque possibile avviare la pipeline manualmente secondo necessità.

1. Se scegli di creare una **pipeline di distribuzione**, dovrai inoltre definire il **Comportamento in caso di errori di metriche importanti**.

   * **Chiedi ogni volta**: questo comportamento è l’impostazione predefinita che richiede l’intervento manuale per tutti gli errori importanti.
   * **Interrompi subito**: selezionando questa opzione, la pipeline viene annullata ogni volta che si verifica un errore importante. In sostanza, questa opzione simula il rifiuto manuale di ogni errore da parte dell’utente.
   * **Continua immediatamente**: se questa opzione è selezionata, la pipeline procede automaticamente ogni volta che si verifica un errore importante. In sostanza, quest’opzione simula l’approvazione manuale di ogni errore da parte dell’utente.

1. Fai clic su **Continua**.

1. Dalla scheda **Codice sorgente** della finestra di dialogo **Aggiungi pipeline non di produzione**, seleziona il tipo di codice da elaborare con la pipeline.

   * **[Codice full stack](#full-stack-code)**
   * **[Distribuzione di destinazione](#targeted-deployment)**

Per ulteriori informazioni sui tipi di pipeline, consulta [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

I passaggi per completare la creazione della pipeline non di produzione variano a seconda del tipo di codice sorgente selezionato. Accedi ai collegamenti riportati qui sopra per passare alla sezione successiva del documento e completare la configurazione della pipeline.

### Codice full stack {#full-stack-code}

Una pipeline del codice full stack distribuisce simultaneamente le build del codice back-end e front-end contenenti una o più applicazioni server AEM con la configurazione HTTPD/Dispatcher.

>[!NOTE]
>
>Se per l’ambiente selezionato esiste una pipeline del codice full stack, la selezione verrà disabilitata.

Per completare la configurazione della pipeline non di produzione del codice full stack, segui la procedura riportata di seguito.

1. Nella scheda **Codice sorgente** è necessario definire le seguenti opzioni.

   * **Ambienti di distribuzione idonei**: se la pipeline è di distribuzione, seleziona gli ambienti in cui eseguire la distribuzione.
   * **Archivio**: questa opzione definisce da quale archivio Git la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

   * **Ramo Git**: questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice.
      * Immetti i primi caratteri del nome del ramo: la funzione di completamento automatico di questo campo. ti aiuta a trovare i rami corrispondenti che puoi selezionare.
   * **Ignora configurazione a livello web**: se questa opzione è selezionata, la pipeline non distribuisce la configurazione a livello web.
   * **Pipeline**: se si tratta di una pipeline è di distribuzione, puoi scegliere di eseguire una fase di test. Seleziona le opzioni che desideri abilitare in questa fase. Se non è selezionata alcuna opzione, la fase di test non viene visualizzata durante l’esecuzione della pipeline.

      * **Test funzionali del prodotto**: esegui [test funzionali del prodotto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) rispetto all’ambiente di sviluppo.
      * **Test funzionali personalizzato**: esegui [test funzionali personalizzati](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) rispetto all’ambiente di sviluppo.
      * **Test personalizzati dell’interfaccia utente**: esegui [test personalizzati dell’interfaccia utente](/help/implementing/cloud-manager/ui-testing.md) per applicazioni personalizzate.
      * **Audit dell&#39;esperienza** - Esegui [Audit dell&#39;esperienza](/help/implementing/cloud-manager/experience-audit-testing.md)

   ![Pipeline full stack](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Fai clic su **Salva**.

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

### Distribuzione mirata {#targeted-deployment}

Una distribuzione mirata distribuisce il codice solo per parti selezionate dell’applicazione AEM. In tale distribuzione è possibile scegliere di **Includere** uno dei seguenti tipi di codice:

* **Configurazione** - Configura le impostazioni per le regole del filtro del traffico nell&#39;ambiente AEM.
   * Per informazioni su come gestire le regole del filtro del traffico nell&#39;archivio in modo che vengano distribuite correttamente, consulta il documento [Regole del filtro del traffico, incluse le regole WAF](/help/security/traffic-filter-rules-including-waf.md).
   * Durante l&#39;esecuzione di una pipeline di distribuzione di destinazione, le configurazioni [quali le configurazioni WAF](/help/security/traffic-filter-rules-including-waf.md) verranno distribuite, purché vengano salvate nell&#39;ambiente, nell&#39;archivio e nel ramo definiti nella pipeline.
   * In qualsiasi momento può essere presente una sola pipeline di configurazione per ogni ambiente.
* **Codice front-end**: configura JavaScript e CSS per il front-end dell&#39;applicazione AEM.
   * Con le pipeline front-end, i team di sviluppo front-end acquisiscono maggiore indipendenza e il processo di sviluppo può essere accelerato.
   * Per informazioni sul funzionamento di questo processo e alcune considerazioni per sfruttare al massimo il suo potenziale, consulta il documento [Sviluppo di Sites con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
* **Configurazione a livello web**: configura le proprietà del dispatcher per archiviare, elaborare e consegnare le pagine web al client.
   * Per ulteriori dettagli, consulta il documento [Pipeline CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines).
   * Se esiste una pipeline del codice a livello web per l’ambiente selezionato, questa selezione è disabilitata.
   * Se già disponi di una pipeline full stack distribuita in un ambiente, creando una pipeline di configurazione a livello web per lo stesso ambiente la configurazione del livello web esistente nella pipeline full stack verrà ignorata.

>[!NOTE]
>
>Le pipeline a livello web e di configurazione non sono supportate con gli archivi privati. Per dettagli e un elenco completo delle limitazioni, consulta [Aggiunta di archivi privati in Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

I passaggi per completare la creazione della pipeline di distribuzione non di produzione con targeting sono gli stessi quando scegli un tipo di distribuzione.

1. Scegliere il tipo di distribuzione desiderato.

![Opzioni di distribuzione di destinazione](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-targeted-deployment.png)

1. Definisci gli **ambienti di distribuzione idonei**.

   * Se la pipeline è di distribuzione, seleziona gli ambienti in cui eseguire la distribuzione.

1. In **Codice Source**, definire le opzioni seguenti:

   * **Archivio**: questa opzione definisce da quale archivio Git la pipeline deve recuperare il codice.

   >[!TIP]
   > 
   >Per scoprire come aggiungere e gestire archivi in Cloud Manager, consulta [Aggiunta e gestione degli archivi](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

   * **Ramo Git**: questa opzione definisce da quale ramo della pipeline selezionata deve essere recuperato il codice.
      * Immetti i primi caratteri del nome del ramo: la funzione di completamento automatico di questo campo. trova i rami corrispondenti che puoi selezionare.
   * **Posizione codice**: definisce il percorso nel ramo dell’archivio selezionato dal quale la pipeline deve recuperare il codice.
   * **Pipeline** - Per le pipeline front-end non di produzione, è possibile abilitare **[Audit dell&#39;esperienza.](/help/implementing/cloud-manager/experience-audit-testing.md)**

   ![Pipeline di configurazione](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config-deployment-experience-audit.png)

1. Se hai abilitato Audit dell&#39;esperienza, tocca o fai clic su **Continua** per passare alla scheda **Audit dell&#39;esperienza** in cui puoi definire i percorsi che devono sempre essere inclusi nell&#39;Audit dell&#39;esperienza.

   * Se hai abilitato **Audit dell&#39;esperienza**, consulta il documento [Audit dell&#39;esperienza](/help/implementing/cloud-manager/experience-audit-testing.md#configuration) per informazioni dettagliate su come configurare.
   * In caso contrario, salta questo passaggio.

1. Per salvare la pipeline, tocca o fai clic su **Salva**.

Ora che hai salvato la pipeline, puoi [gestire le pipeline](managing-pipelines.md) dalla pagina **Panoramica del programma** nella scheda **Pipeline**.

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
