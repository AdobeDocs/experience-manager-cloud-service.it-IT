---
title: Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)
description: Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti)
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: eae5b6a8903f68d4736e44db9a9e598716a15b75
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 32%

---

# Guida introduttiva allo strumento Content Transfer (Trasferimento contenuti) {#getting-started-content-transfer-tool}

## Disponibilità {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Scarica"
>abstract="Lo strumento Content Transfer (Trasferimento contenuti) può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM). Assicurati di scaricare la versione più recente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="Note sulla versione"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Portale di distribuzione software"

Lo strumento Content Transfer (Trasferimento contenuti) può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Gestione pacchetti nella tua istanza sorgente di Adobe Experience Manager (AEM). Assicurati di scaricare la versione più recente. Per ulteriori informazioni sull&#39;ultima versione, consulta [Note sulla versione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

>[!NOTE]
>Scarica lo strumento Content Transfer (Trasferimento contenuti) dal portale di [Distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

## Esecuzione dello strumento Content Transfer (Trasferimento contenuti)  {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Esecuzione dello strumento Content Transfer (Trasferimento contenuti)"
>abstract="Scopri come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per migrare il contenuto in AEM as a Cloud Service (authoring/pubblicazione)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Vedere Demo"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Tutorial: utilizzo dello strumento Content Transfer (Trasferimento contenuti)"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Segui le indicazioni contenute in questa sezione per apprendere come utilizzare lo strumento Content Transfer (Trasferimento contenuti) per migrare i contenuti in AEM as a Cloud Service (authoring/pubblicazione):

1. Seleziona Adobe Experience Manager e passa a Strumenti -> **Operazioni** -> **Migrazione dei contenuti**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt01.png)

1. Seleziona l’opzione **Trasferimento contenuti** dalla procedura guidata **Migrazione contenuti**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt02.png)


1. La console seguente viene visualizzata quando crei il primo set di migrazione. Fai clic su **Create Migration Set** (Crea set di migrazione) per creare un nuovo set di migrazione.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >Se disponi di set di migrazione esistenti, nella console viene visualizzato l’elenco dei set di migrazione esistenti con il relativo stato corrente.


1. Compila i campi nella schermata **Crea set di migrazione** come descritto di seguito.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt04.png)

   1. **Name** (Nome): inserisci il nome del set di migrazione.
      >[!NOTE]
      >Il nome del set di migrazione non può contenere caratteri speciali.

   1. **Cloud Service Configuration** (Configurazione Cloud Service): inserisci l’URL dell’istanza di authoring di AEM as a Cloud Service di destinazione.

      >[!NOTE]
      >Puoi creare e mantenere un massimo di dieci set di migrazione alla volta durante l’attività di trasferimento dei contenuti.
      >Inoltre, è necessario creare separatamente una migrazione per ciascun ambiente: *Stage*, *Sviluppo* o *Produzione*.

   1. **Access Token** (Token di accesso): inserisci il token di accesso.

      >[!NOTE]
      >Puoi recuperare il token di accesso utilizzando il pulsante **Open access token** . Devi accertarti di appartenere al gruppo di amministratori di AEM nell’istanza di Cloud Service di destinazione.

   1. **Parameters** (Parametri): seleziona i seguenti parametri per creare il set di migrazione:

      1. **Include Version** (Includi versione): seleziona in base alle esigenze. Quando sono incluse le versioni, il percorso `/var/audit` viene automaticamente incluso per eseguire la migrazione degli eventi di controllo.

      ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt05.png)

      >[!NOTE]
      >Se intendi includere versioni come parte di un set di migrazione e stai eseguendo integrazioni con `wipe=false`, devi disattivare l’eliminazione della versione a causa di un limite corrente nello strumento Content Transfer (Trasferimento contenuti). Se preferisci mantenere abilitata l’eliminazione della versione e stai eseguendo i top-up in un set di migrazione, devi eseguire l’acquisizione come `wipe=true`.

      1. **Includi mapping da utenti e gruppi** IMS: Seleziona l’opzione per includere la mappatura da utenti e gruppi IMS.
Per ulteriori informazioni, consulta [Strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) .

      1. **Paths to be included** (Percorsi da includere): utilizza il browser percorsi per selezionare i percorsi interessati dalla migrazione. Il selettore del percorso accetta l’input digitando o selezionando.

         >[!IMPORTANT]
         >Durante la creazione di un set di migrazione, i percorsi seguenti sono soggetti a restrizioni:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (alcuni  `/etc` percorsi possono essere selezionati in CTT)




1. Fai clic su **Salva** dopo aver compilato tutti i campi nella schermata dei dettagli **Crea set di migrazione** .

1. Il set di migrazione verrà visualizzato nella procedura guidata **Trasferimento contenuti** , come illustrato nella figura riportata di seguito.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt07.png)

   Tutti i set di migrazione esistenti vengono visualizzati nella procedura guidata **Trasferimento contenuti** con il relativo stato corrente e le informazioni sullo stato. Puoi vedere alcune di queste icone descritte di seguito.

   * Una *nuvola rossa* indica che non puoi completare il processo di estrazione.
   * Una *nuvola verde* indica che puoi completare il processo di estrazione.
   * Un’*icona gialla* indica che non hai creato il set di migrazione esistente e che quello specifico è stato creato da un altro utente nella stessa istanza.

1. Seleziona un set di migrazione e fai clic su **Proprietà** per visualizzare o modificare le proprietà del set di migrazione. Durante la modifica delle proprietà, non è possibile modificare il **nome del set di migrazione** o l’ **URL del servizio**.

   ![immagine](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt06.png)


## Novità {#whats-next}

Dopo aver imparato a creare un set di migrazione, ora puoi imparare a usare i processi di estrazione e acquisizione nello strumento Content Transfer (Trasferimento contenuti). Prima di apprendere questi processi, devi rivedere [Gestione di archivi di contenuti di grandi dimensioni](help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) per velocizzare in modo significativo le fasi di estrazione e acquisizione dell’attività di trasferimento dei contenuti per spostare i contenuti in AEM as a Cloud Service.
