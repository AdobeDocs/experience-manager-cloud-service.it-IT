---
title: Estrazione del contenuto dall’origine
description: Estrazione del contenuto dall’origine
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 38%

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
>Se Amazon S3 o Azure Data Store viene utilizzato come tipo di archivio dati, puoi eseguire il passaggio facoltativo di pre-copia per accelerare in modo significativo la fase di estrazione. A questo scopo, devi configurare un `azcopy.config` prima di eseguire l’estrazione. Fai riferimento a [Gestione di archivi di contenuti di grandi dimensioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) per ulteriori dettagli.

>[!IMPORTANT]
>È necessario eseguire lo strumento User Mapping prima di estrarre il contenuto dall’origine. Vedi [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) per ulteriori dettagli.

1. Seleziona un set di migrazione da **Trasferimento dei contenuti** procedura guidata e fai clic su **Extract** per avviare l’estrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-01.png)

1. La **Estrazione set di migrazione** viene visualizzata la finestra di dialogo e fai clic su **Extract** per avviare la fase di estrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >È presente l’opzione per sovrascrivere il contenitore di staging durante la fase di estrazione.

   >[!IMPORTANT]
   >Se la Mappatura utente non è stata eseguita su questo set di migrazione prima di estrarre il contenuto dall’origine, verrà visualizzato un avviso che mostra che il passaggio Mappatura utente è in sospeso, come illustrato nella figura riportata di seguito. Fai clic su **Mappa utenti** per eseguire lo strumento User Mapping (Mappatura utente).
   >![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. La **Estrazione** viene ora visualizzato il campo **IN ESECUZIONE** stato per indicare che l’estrazione è in corso.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-03.png)

   Una volta completata l’estrazione, lo stato del set di migrazione diventa **FINISHED** (COMPLETATO) e un’icona di nuvola *verde* viene visualizzata nel campo **INFO**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >L’interfaccia utente dispone di una funzione di ricaricamento automatico che ricarica il **Trasferimento dei contenuti** procedura guidata ogni 30 secondi.
   >Quando si avvia la fase di estrazione, viene applicato il blocco di scrittura, che viene rilasciato dopo *60 secondi*. Pertanto, se si interrompe un’estrazione, prima di riavviare l’estrazione è necessario attendere un minuto affinché il blocco venga rilasciato.

## Estrazione integrativa {#top-up-extraction-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.
>Inoltre, è essenziale che la struttura del contenuto esistente non venga modificata dal momento in cui l’estrazione iniziale viene portata al momento dell’esecuzione dell’estrazione integrativa. Non è possibile eseguire i top-up su contenuto la cui struttura è stata modificata dopo l’estrazione iniziale. Assicurati di limitare questa limitazione durante il processo di migrazione.

Una volta completato il processo di estrazione, puoi trasferire il contenuto delta utilizzando il metodo di estrazione integrativa.

Effettua le seguenti operazioni:

1. Passa a **Trasferimento dei contenuti** e seleziona il set di migrazione per il quale desideri eseguire l’estrazione integrativa. Fai clic su **Extract** (Estrai) per avviare l’estrazione integrativa.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-05.png)

1. La **Estrazione set di migrazione** viene visualizzata la finestra di dialogo. Fai clic su **Extract**.

   >[!IMPORTANT]
   >Disattiva l’opzione **Overwrite staging container during extraction** (Sovrascrivi contenitore di staging durante l’estrazione).
   >![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-06.png)


## Novità {#whats-next}

Dopo aver appreso l’estrazione del contenuto dall’origine nello strumento Content Transfer (Trasferimento contenuti), è ora possibile apprendere il processo di acquisizione nello strumento Content Transfer (Trasferimento contenuti). Vedi [Inserimento di contenuto in Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) per scoprire come acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti).
