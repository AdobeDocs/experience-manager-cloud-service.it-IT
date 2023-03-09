---
title: Estrazione di contenuto dall’origine (legacy)
description: Estrazione del contenuto dall’origine
hide: true
hidefromtoc: true
exl-id: 9f43356c-ba51-48bc-97f5-f1f5db81e7f3
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 34%

---

# Estrazione di contenuto dall’origine (legacy) {#extracting-content}

## Processo di estrazione nello strumento Content Transfer {#extraction-process}

Per estrarre il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti), effettua le seguenti operazioni:
>[!NOTE]
>Se come tipo di archivio dati viene utilizzato Amazon S3 o Azure Data Store, puoi eseguire il passaggio di pre-copia facoltativo per velocizzare in modo significativo la fase di estrazione. A questo scopo, devi configurare un’ `azcopy.config` prima di eseguire l’estrazione. Fai riferimento a [Gestione di archivi di contenuti di grandi dimensioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) per ulteriori dettagli.

>[!IMPORTANT]
>Prima di estrarre il contenuto dalla sorgente, è necessario eseguire lo strumento di mappatura utenti. Consulta [Utilizzo dello strumento di mappatura utenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en) per ulteriori dettagli.

1. Seleziona un set di migrazione da **Trasferimento dei contenuti** e fai clic su **Extract** per avviare l’estrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-01.png)

1. Il **Estrazione del set di migrazione** viene visualizzata la finestra di dialogo e fai clic su **Extract** per avviare la fase di estrazione.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >Facoltativamente, puoi sovrascrivere il contenitore di staging durante la fase di estrazione.

   >[!IMPORTANT]
   >Se per questo set di migrazione non è stata eseguita la mappatura utente prima di estrarre il contenuto dall’origine, viene visualizzato un avviso che indica che il passaggio Mappatura utente è in sospeso, come illustrato nella figura seguente. Seleziona **Mappa utenti** per eseguire lo strumento Mappatura utente.
   >![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. Il **Estrazione** ora visualizza il campo **IN ESECUZIONE** stato per indicare che l’estrazione è in corso.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-03.png)

   Una volta completata l’estrazione, lo stato del set di migrazione diventa **FINISHED** (COMPLETATO) e un’icona di nuvola *verde* viene visualizzata nel campo **INFO**.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >L’interfaccia utente dispone di una funzione di ricaricamento automatico che ricarica il **Trasferimento dei contenuti** ogni 30 secondi.
   >Quando si avvia la fase di estrazione, viene applicato il blocco di scrittura, che viene rilasciato dopo *60 secondi*. Pertanto, se si interrompe un’estrazione, prima di riavviare l’estrazione è necessario attendere un minuto affinché il blocco venga rilasciato.

## Estrazione integrativa {#top-up-extraction-process}

Lo strumento Content Transfer (Trasferimento contenuti) dispone di una funzione che supporta l’integrazione di contenuti differenziali, per trasferire solo le modifiche apportate dall’ultima attività di trasferimento dei contenuti.

>[!NOTE]
>Dopo il trasferimento iniziale dei contenuti, si consiglia di eseguire frequenti integrazioni dei contenuti differenziali in modo da ridurre il periodo di blocco dei contenuti per il trasferimento finale dei contenuti differenziali, prima della pubblicazione in Cloud Service.
>Inoltre, assicurati che la struttura del contenuto esistente non venga modificata dal momento in cui viene eseguita l’estrazione iniziale a quello in cui viene eseguita l’estrazione integrativa. I top up non possono essere eseguiti su contenuti la cui struttura è stata modificata dopo l’estrazione iniziale. Assicurati di limitare questo valore durante il processo di migrazione.

Una volta completato il processo di estrazione, puoi trasferire il contenuto delta utilizzando il metodo di estrazione integrativa.

Effettua le seguenti operazioni:

1. Accedi a **Trasferimento dei contenuti** e selezionare il set di migrazione per il quale si desidera eseguire l’estrazione integrativa. Fai clic su **Extract** (Estrai) per avviare l’estrazione integrativa.

   ![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-05.png)

1. Il **Estrazione del set di migrazione** viene visualizzata. Fai clic su **Extract**.

   >[!IMPORTANT]
   >Disattiva l’opzione **Overwrite staging container during extraction** (Sovrascrivi contenitore di staging durante l’estrazione).
   >![immagine](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-06.png)


## Passaggio successivo {#whats-next}

Dopo aver appreso le nozioni di &quot;Estrazione del contenuto dall’origine&quot; nello strumento Content Transfer (Trasferimento contenuti), ora puoi imparare il processo di acquisizione nello strumento Content Transfer (Trasferimento contenuti). Consulta [Acquisizione di contenuti in Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) per scoprire come acquisire il set di migrazione dallo strumento Content Transfer (Trasferimento contenuti).
