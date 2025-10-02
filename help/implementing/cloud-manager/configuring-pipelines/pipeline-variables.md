---
title: Variabili delle pipeline in Cloud Manager
description: Scopri come utilizzare le variabili della pipeline in Cloud Manager per gestire variabili di configurazione specifiche per la build.
exl-id: cfcef2e2-0590-457d-a0f9-6092a6d9e0e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ea85deb74f759f8e74d314df0ba081ea23cb5aab
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 14%

---

# Variabili delle pipeline in Cloud Manager {#configuring-pipeline-variables}

Il processo di build può basarsi su variabili di configurazione specifiche che non devono essere memorizzate nell’archivio Git. In alternativa, potrebbe essere necessario regolarli tra un’esecuzione della pipeline e l’altra sullo stesso ramo. Cloud Manager consente di gestire queste impostazioni come variabili della pipeline.

## Informazioni sulle variabili della pipeline {#pipeline-variables}

Utilizzando Cloud Manager puoi configurare le variabili della pipeline in diversi modi.

* [Utilizzo dell’interfaccia utente di Cloud Manager](#ui)
* [Utilizzo di Cloud Manager CLI](#cli)
* [Utilizzo dell&#39;API Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Variables/operation/getPipelineVariables)

Le variabili possono essere archiviate come testo normale o crittografate quando inattive. In entrambi i casi, le variabili sono rese disponibili all’interno dell’ambiente di build come una variabile di ambiente a cui è possibile fare riferimento dal file `pom.xml` o da altri script della build.

## Aggiungere una variabile di pipeline tramite Cloud Manager {#ui}

Le variabili di pipeline possono essere configurate e gestite tramite l’interfaccia utente di Cloud Manager. Contribuiscono a semplificare la gestione delle pipeline, soprattutto quando sono necessarie configurazioni diverse nei diversi passaggi.

Per aggiungere, modificare ed eliminare variabili di pipeline è necessario disporre delle autorizzazioni necessarie per modificare la pipeline.

Se una pipeline è in esecuzione, la gestione delle variabili viene bloccata.

**Per aggiungere una variabile di pipeline tramite Cloud Manager:**

1. Quando [gestisci le pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), fai clic su ![Puntini di sospensione - Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) della pipeline per la quale desideri creare le variabili della pipeline.

1. Scegliere **Visualizza/Modifica variabili** dal menu a discesa.

   ![Visualizza/Modifica variabili pipeline](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Nella finestra di dialogo **Configurazione variabili**, immettere i dettagli nella prima riga della tabella.

   | Campo | Descrizione |
   | --- | --- |
   | Nome | Nome univoco della variabile di configurazione. Identifica la variabile specifica utilizzata nella pipeline. Deve rispettare le seguenti convenzioni di denominazione:<ul><li>Le variabili possono contenere solo caratteri alfanumerici e il carattere di sottolineatura (`_`).</li><li>I nomi devono essere scritti in lettere maiuscole.</li><li>È previsto un limite di 200 variabili per pipeline.</li><li>Ogni nome non può contenere più di 100 caratteri.</li><li>Ogni valore della variabile `string` deve avere una lunghezza inferiore a 2048 caratteri.</li><li>Ogni valore della variabile di tipo `secretString` deve contenere un massimo di 500 caratteri.</li></ul> |
   | Valore | Valore contenuto nella variabile. |
   | Passaggio applicato | Obbligatorio. Passaggio della pipeline a cui si applica la variabile:<ul><li>**Build** - La variabile viene applicata durante il processo di compilazione.</li><li>**Test funzionali** - La variabile viene utilizzata durante il passaggio del test funzionale.</li><li>**Test interfaccia utente** - La variabile viene utilizzata durante la fase di test dell&#39;interfaccia utente.</li>&lt;li&lt;**Distribuzione** - La variabile viene utilizzata durante il passaggio di distribuzione. Ad esempio, utilizza questa variabile per le pipeline di Edge Delivery Services.</li></ul> |
   | Tipo | Seleziona questa opzione se la variabile è in testo normale o crittografata come segreto. |

   ![Aggiungi variabile](/help/implementing/cloud-manager/assets/pipeline-variables-add-variable.png)

1. Fai clic su **Aggiungi**.

   Aggiungi ulteriori variabili in base alle esigenze.

1. Fai clic su **Salva**.

## Modificare una variabile di pipeline {#edit-ui}

1. Quando [gestisci le pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), fai clic su ![Puntini di sospensione - Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) della pipeline per la quale desideri modificare le variabili della pipeline.

1. Scegliere **Visualizza/Modifica variabili** dal menu a discesa.

   ![Visualizza/Modifica variabili pipeline](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Nella finestra di dialogo **Configurazione variabili**, fai clic su ![Puntini di sospensione - Icona altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) della variabile da modificare.

1. Nel menu a discesa, fare clic su **Modifica**.

   ![Modifica della variabile](/help/implementing/cloud-manager/assets/pipeline-variables-edit.png)

1. Aggiorna il valore della variabile come richiesto.

   È possibile modificare solo il valore della variabile.

1. Effettua una delle seguenti operazioni:

   * Fai clic su ![Applica - icona segno di spunta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg) per applicare la modifica.
   * Fai clic sull&#39;icona ![Annulla](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Undo_18_N.svg) per annullare la modifica.

1. Fai clic su **Salva**.


## Eliminare una variabile di pipeline {#delete-ui}

1. Quando [gestisci le pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md), fai clic su ![Puntini di sospensione - Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) della pipeline per la quale desideri eliminare le variabili della pipeline.

1. Scegliere **Visualizza/Modifica variabili** dal menu a discesa.

   ![Visualizza/Modifica variabili pipeline](/help/implementing/cloud-manager/assets/pipeline-variables-view-edit.png)

1. Nella finestra di dialogo **Configurazione variabili**, fai clic su ![Puntini di sospensione - Icona altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) della variabile da rimuovere, quindi fai clic su **Elimina**.

## Impostare le variabili della pipeline utilizzando Cloud Manager CLI {#cli}

Questo comando in CLI (Command Line Interface) imposta una variabile.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Comando per elencare le variabili.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Quando viene utilizzato in un file Maven `pom.xml`, spesso è utile collegare queste variabili alle proprietà Maven utilizzando una sintassi simile a quella del seguente esempio:

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
