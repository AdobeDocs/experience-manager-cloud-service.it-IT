---
title: Configurare le variabili di pipeline
description: Scopri come utilizzare le variabili della pipeline in Cloud Manager per gestire variabili di configurazione specifiche per la build.
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 18%

---

# Configurare le variabili della pipeline {#configuring-pipeline-variables}

Il processo di build può dipendere da specifiche variabili di configurazione che sarebbe inappropriato inserire nell’archivio Git o che potrebbero dover essere modificate tra le esecuzioni della pipeline che utilizzano lo stesso ramo. Cloud Manager consente di gestire questi dati come variabili della pipeline.

## Variabili di pipeline {#pipeline-variables}

Utilizzando Cloud Manager puoi configurare le variabili della pipeline in diversi modi.

* [Tramite l’interfaccia utente di Cloud Manager](#ui)
* [Utilizzo di Cloud Manager CLI](#cli)
* [Utilizzo dell&#39;API Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

Le variabili possono essere archiviate come testo normale o crittografate quando inattive. In entrambi i casi, le variabili sono rese disponibili all’interno dell’ambiente di build come una variabile di ambiente a cui è possibile fare riferimento dal file `pom.xml` o da altri script della build.

### Convenzioni di denominazione delle variabili della pipeline {#naming-conventions}

I nomi delle variabili devono rispettare le seguenti convenzioni:

* Le variabili possono contenere solo caratteri alfanumerici e il carattere di sottolineatura (`_`).
* I nomi devono essere scritti in lettere maiuscole.
* È previsto un limite di 200 variabili per pipeline.
* Ogni nome non può contenere più di 100 caratteri.
* Ogni valore della variabile `string` deve avere una lunghezza inferiore a 2048 caratteri.
* Ogni valore della variabile di tipo `secretString` deve contenere un massimo di 500 caratteri.

## Tramite l’interfaccia utente di Cloud Manager {#ui}

Le variabili di pipeline possono essere configurate e gestite tramite l’interfaccia utente di Cloud Manager. Per aggiungere, modificare ed eliminare variabili di pipeline è necessario disporre delle autorizzazioni necessarie per modificare la pipeline.

Se una pipeline è in esecuzione, la gestione delle variabili viene bloccata.

### Aggiungere variabili della pipeline {#add-ui}

1. Quando [gestisci le pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), fai clic sul pulsante con i puntini di sospensione della pipeline per la quale desideri creare le variabili della pipeline e seleziona **Visualizza/modifica variabili** dal menu di scelta rapida.

   ![Visualizzare/modificare le variabili della pipeline](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Viene visualizzata la finestra **Configurazione variabili**. Immettere i dettagli della variabile nella prima riga della tabella e fare clic su **Aggiungi**.

   * **Nome configurazione** è un identificatore univoco per la variabile, che deve essere all&#39;origine di [convenzioni di denominazione delle variabili della pipeline](#naming-conventions).
   * **Valore** è il valore che la variabile contiene.
   * **Passaggio applicato** è il passaggio della pipeline a cui si applica la variabile. È obbligatorio.
      * **Build**
      * **Test funzionali**
      * **Test dell&#39;interfaccia utente**
   * **Il tipo** definisce se la variabile è testo normale o crittografata come segreto.

   ![Aggiungi variabile](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. Il viene aggiunto alla tabella. Aggiungi altre variabili secondo necessità, quindi tocca o fai clic su **Salva** per salvare le variabili aggiunte alla pipeline.

### Modifica delle variabili di pipeline {#edit-ui}

1. Quando [gestisci le pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), fai clic sul pulsante con i puntini di sospensione della pipeline per la quale desideri creare le variabili della pipeline e seleziona **Visualizza/modifica variabili** dal menu di scelta rapida.

   ![Visualizzare/modificare le variabili della pipeline](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Viene visualizzata la finestra **Configurazione variabili**. Fai clic sul pulsante con i puntini di sospensione della variabile da modificare e seleziona **Modifica**.

   ![Modifica della variabile](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. Aggiorna il valore della variabile come richiesto e fai clic su **Applica** (il segno di spunta alla fine della riga) per applicare la modifica oppure su **Elimina** (la freccia indietro) per ripristinarla.

   * È possibile modificare solo il valore della variabile.

   ![Modifica di una variabile](/help/implementing/cloud-manager/assets/pipeline-variables-edit-save.png)

1. Fai clic su **Salva**.

Se desideri eliminare una variabile, seleziona **Elimina** invece di **Modifica** dal menu con i puntini di sospensione della variabile della pipeline nella finestra **Configurazione variabili**.

## Utilizzare Cloud Manager CLI {#cli}

Comando CLI per impostare una variabile.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Comando per elencare le variabili.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Per l’utilizzo in un file `pom.xml` Maven, in genere è utile associare queste variabili alle proprietà Maven scrivendo una sintassi simile a quella proposta di seguito.

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```
