---
title: Estrazione del contenuto dall’origine
description: Estrazione del contenuto dall’origine
source-git-commit: 6a6fa69d2eb79e41c79a0916bfd6e34ecf490d34
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 41%

---


# Estrazione del contenuto dall’origine {#extracting-content}

## Processo di estrazione nello strumento Content Transfer (Trasferimento contenuti) {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Estrazione dei contenuti"
>abstract="Per estrazione si intende l’estrazione del contenuto dall’istanza AEM di origine in un’area temporanea denominata set di migrazione. Un set di migrazione è un’area di archiviazione cloud fornita da Adobe in cui vengono archiviati temporaneamente i contenuti trasferiti tra l’istanza AEM di origine e l’istanza AEM di Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Estrazione dall&#39;alto verso l&#39;alto"

Per estrarre il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:
>[!NOTE]
>Se Amazon S3 o Azure Data Store viene utilizzato come tipo di archivio dati, puoi eseguire il passaggio facoltativo di pre-copia per accelerare in modo significativo la fase di estrazione. A questo scopo, devi configurare un file `azcopy.config` prima di eseguire l’estrazione. Per ulteriori informazioni, consulta [Gestione degli archivi di contenuti di grandi dimensioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) .

1. Seleziona un set di migrazione dalla procedura guidata **Trasferimento contenuti** e fai clic su **Estrai** per avviare l’estrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-01.png)

1. Viene visualizzata la finestra di dialogo **Migration Set extraction** (Estrazione set di migrazione) e fai clic su **Extract** (Estrai) per avviare la fase di estrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >È presente l’opzione per sovrascrivere il contenitore di staging durante la fase di estrazione.

1. Il campo **Estrazione** ora visualizza lo stato **ESECUZIONE** per indicare che l’estrazione è in corso.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-03.png)

   Una volta completata l’estrazione, lo stato del set di migrazione diventa **FINISHED** (COMPLETATO) e un’icona di nuvola *verde* viene visualizzata nel campo **INFO**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >L’interfaccia utente dispone di una funzione di ricaricamento automatico che ricarica la procedura guidata **Trasferimento contenuti** ogni 30 secondi.
   >Quando si avvia la fase di estrazione, viene applicato il blocco di scrittura, che viene rilasciato dopo *60 secondi*. Pertanto, se si interrompe un’estrazione, prima di riavviare l’estrazione è necessario attendere un minuto affinché il blocco venga rilasciato.

## Estrazione integrativa {#top-up-extraction-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.
>Inoltre, è essenziale che la struttura del contenuto esistente non venga modificata dal momento in cui l’estrazione iniziale viene portata al momento dell’esecuzione dell’estrazione integrativa. Non è possibile eseguire i top-up su contenuto la cui struttura è stata modificata dopo l’estrazione iniziale. Assicurati di limitare questa limitazione durante il processo di migrazione.

Una volta completato il processo di estrazione, puoi trasferire il contenuto delta utilizzando il metodo di estrazione integrativa.

Effettua le seguenti operazioni:

1. Passa alla procedura guidata **Trasferimento contenuti** e seleziona il set di migrazione per il quale desideri eseguire l’estrazione integrativa. Fai clic su **Extract** (Estrai) per avviare l’estrazione integrativa.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-05.png)

1. Viene visualizzata la finestra di dialogo **Migration Set extraction** (Estrazione set di migrazione). Fai clic su **Extract**.

   >[!IMPORTANT]
   >Disattiva l’opzione **Overwrite staging container during extraction** (Sovrascrivi contenitore di staging durante l’estrazione).
   >![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/extraction-06.png)


## Novità {#whats-next}

Dopo aver appreso l’estrazione del contenuto dall’origine nello strumento Content Transfer (Trasferimento contenuti), è ora possibile apprendere il processo di acquisizione nello strumento Content Transfer (Trasferimento contenuti). Per informazioni su come acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), consulta [Inserimento di contenuti in Target nello strumento Content Transfer (Trasferimento contenuti).](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
