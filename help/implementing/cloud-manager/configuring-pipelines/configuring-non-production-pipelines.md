---
title: Configurazione di pipeline non di produzione
description: Configurazione di pipeline non di produzione
index: false
source-git-commit: 84d04d8399668b8b1051d4edf9de851bca271071
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Configurazione di pipeline non di produzione {#configure-non-production-pipeline}

Oltre alla pipeline principale che viene implementata in fase e produzione, i clienti possono impostare pipeline aggiuntive, denominate pipeline non di produzione .
Esistono due tipi di gasdotti non di produzione:

1. Qualità del codice: Esegue la scansione della qualità del codice sul codice nel ramo git. Questa pipeline esegue i passaggi di creazione e qualità del codice.
1. Distribuzione: Oltre a eseguire i passaggi di build e qualità del codice, questa pipeline distribuisce il codice alla non produzione selezionata per AEM l’ambiente as a Cloud Service.

## Aggiunta di una nuova pipeline non di produzione {#adding-non-production-pipeline}

Nella schermata iniziale, queste pipeline sono elencate in una nuova scheda:

1. Accedere al **Tubi** scheda dalla schermata principale di Cloud Manager. Fai clic su **+Aggiungi** e seleziona **Aggiungi pipeline non di produzione**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Aggiungi pipeline non di produzione**  viene visualizzata la finestra di dialogo. Seleziona il tipo di pipeline che desideri creare, oppure **Pipeline di qualità del codice** o **Pipeline di distribuzione**.

   >[!NOTE]
   >Per le pipeline di distribuzione, è necessario selezionare l&#39;ambiente di distribuzione.

   Inoltre, puoi anche configurare **Trigger distribuzione** e **Comportamento di errori di metrica importanti** da **Opzioni di distribuzione**. Fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. Seleziona **Codice Stack Completo** o **Codice front-end**. Puoi scegliere la **Archivio** e **Ramo Git**. Fai clic su **Salva**.

   >[!NOTE]
   >Prima di iniziare a configurare le pipeline front-end, vedere AEM Percorso di creazione rapida di siti per un flusso di lavoro end-to-end tramite lo strumento di creazione rapida AEM facile da utilizzare. Questo sito di documentazione ti aiuterà a semplificare lo sviluppo front-end del tuo sito AEM e a personalizzare rapidamente il tuo sito senza AEM conoscenza back-end.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. La nuova pipeline non di produzione creata viene ora visualizzata nella **Tubi** il Card.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   La pipeline viene visualizzata sulla scheda nella schermata iniziale con tre azioni, come illustrato di seguito:

   * **Aggiungi** - consente di aggiungere una nuova pipeline.
   * **Accesso alle informazioni sul repository** - consente all’utente di ottenere le informazioni necessarie per accedere all’archivio Git di Cloud Manager.
   * **Ulteriori informazioni** - Informazioni sulla risorsa della documentazione della pipeline CI/CD.