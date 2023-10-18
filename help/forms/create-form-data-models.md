---
title: Come si crea il modello dati del modulo?
description: Scopri come creare un modello di dati modulo (FDM) e inviare o recuperare dati a un’origine dati utilizzando un modulo adattivo o un flusso di lavoro AEM.
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: a942e87a33775851631a1fe123fa3e8d2686bb30
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 2%

---

# Crea modello dati modulo {#create-form-data-model}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html) |
| AEM as a Cloud Service | Questo articolo |


![Integrazione dei dati](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] l’integrazione dei dati fornisce un’interfaccia utente intuitiva per creare e utilizzare i modelli di dati dei moduli. Un modello dati modulo si basa su origini dati per lo scambio di dati; tuttavia, è possibile creare un modello dati modulo con o senza un&#39;origine dati. Esistono due approcci per creare un modello dati da a seconda che siano state configurate o meno le origini dati:

* **Utilizzo di origini dati preconfigurate**: se hai configurato le origini dati come descritto in [Configurare le origini dati](configure-data-sources.md), è possibile selezionarli durante la creazione di un modello di dati del modulo. Raccoglie tutti gli oggetti, le proprietà e i servizi del modello dati dalle origini dati selezionate disponibili per l’utilizzo nel modello dati del modulo.

* **Senza origini dati**: se non hai configurato le origini dati per il modello dati del modulo, puoi comunque crearlo senza origini dati. Puoi utilizzare il modello dati del modulo per creare Forms adattivo <!--and interactive communication--> e testarli utilizzando dati di esempio. Quando le origini dati sono disponibili, è possibile associare il modello dati del modulo alle origini dati, che si riflettono automaticamente nel Forms adattivo associato<!--and interactive communications-->.

>[!NOTE]
>
>Devi essere membro di entrambi **fdm-author** e **forms-user** gruppi per creare e utilizzare il modello dati del modulo. Contatta il tuo [!DNL Experience Manager] per diventare un membro dei gruppi.

## Crea modello dati modulo {#data-sources}

Verifica di aver configurato le origini dati che intendi utilizzare nel modello dati del modulo come descritto in [Configurare le origini dati](configure-data-sources.md). Per creare un modello dati modulo basato su origini dati configurate, effettuare le seguenti operazioni:

1. In entrata [!DNL Experience Manager] istanza di authoring, passa a **[!UICONTROL Forms > Integrazioni dati]**.
1. Tocca **[!UICONTROL Crea > Modello dati modulo]**.
1. Nella finestra di dialogo Crea modello dati modulo:

   * Specifica un nome per il modello dati del modulo.
   * (**Facoltativo**) Specifica titolo, descrizione e tag per il modello di dati del modulo.
   * (**Facoltativo e applicabile solo se le origini dati sono configurate** a) Toccare l&#39;icona di spunta accanto al **[!UICONTROL Configurazione origine dati]** e seleziona il nodo di configurazione in cui risiedono i servizi cloud per le origini dati che desideri utilizzare. Limita l’elenco delle origini dati disponibili per la selezione nella pagina successiva a quelle disponibili nel nodo di configurazione selezionato. Tuttavia, qualsiasi [!DNL Experience Manager] le origini dati del profilo utente sono elencate per impostazione predefinita. Se non si seleziona un nodo di configurazione, vengono elencate le origini dati di tutti i nodi di configurazione.

1. Tocca **[!UICONTROL Successivo]**.

1. (**Applicabile solo se le origini dati sono configurate**) La **[!UICONTROL Seleziona origine dati]** nella schermata sono elencate le origini dati disponibili, se presenti. Selezionare le origini dati da utilizzare nel modello dati del modulo.
1. Tocca **[!UICONTROL Crea]** e nella finestra di dialogo di conferma tocca **[!UICONTROL Apri]** per aprire l’editor modello dati modulo.

   Esaminiamo i diversi componenti dell’interfaccia utente dell’editor del modello dati modulo.

   ![Un modello di dati modulo con tre origini dati: un servizio RESTful, [!DNL Experience Manager] e un RDBMS](assets/fdm-ui.png)

   R. **[!UICONTROL Origini dati]** Elenca le origini dati in un modello dati modulo. Espandere un&#39;origine dati per visualizzare i relativi servizi e oggetti modello dati.

   B. **[!UICONTROL Aggiorna definizioni origine dati]** Recupera eventuali modifiche nelle definizioni dell’origine dati dalle origini dati configurate e le aggiorna nella scheda Origini dati dell’editor modelli dati modulo.

   C. **[!UICONTROL Modello]** Area contenuto in cui vengono visualizzati gli oggetti modello dati aggiunti.

   D. **[!UICONTROL Servizi]** Area del contenuto in cui vengono visualizzati operazioni o servizi dell&#39;origine dati aggiunti.

   E. **[!UICONTROL Barra degli strumenti]** Strumenti per utilizzare il modello dati del modulo. La barra degli strumenti mostra più opzioni a seconda dell’oggetto selezionato nel modello dati del modulo.

   F. **[!UICONTROL Aggiungi selezionati]** Aggiunge al modello dati del modulo gli oggetti e i servizi modello dati selezionati.

Per ulteriori informazioni sull’editor del modello dati modulo e su come utilizzarlo per modificare e configurare il modello dati modulo, consulta [Utilizzare il modello dati del modulo](work-with-form-data-model.md).

## Aggiornare le origini dati {#update}

Per aggiungere o aggiornare origini dati a un modello dati modulo esistente, eseguire le operazioni seguenti.

1. Vai a **[!UICONTROL Forms > Integrazioni dati]**, seleziona il modello dati modulo in cui desideri aggiungere o aggiornare le origini dati e tocca **[!UICONTROL Proprietà]**.
1. Nelle proprietà del modello dati modulo, vai al **[!UICONTROL Aggiorna origine]** scheda.

   In **[!UICONTROL Aggiorna origine]** scheda:

   * Tocca l’icona Sfoglia in **[!UICONTROL Configurazione in base al contesto]** e selezionare un nodo di configurazione in cui risiede la configurazione cloud per l&#39;origine dati che si desidera aggiungere. Se non selezioni un nodo, le configurazioni cloud che risiedono solo nel `global` Il nodo viene elencato quando tocchi **[!UICONTROL Aggiungi origini]**.

   * Per aggiungere una nuova origine dati, tocca **[!UICONTROL Aggiungi origini]** e seleziona le origini dati da aggiungere al modello dati del modulo. Tutte le origini dati configurate in `global` e viene visualizzato il nodo di configurazione selezionato, se presente.

   * Per sostituire un’origine dati esistente con un’altra origine dati dello stesso tipo, tocca il **[!UICONTROL Modifica]** per l&#39;origine dati e selezionarla dall&#39;elenco delle origini dati disponibili.
   * Per eliminare un’origine dati esistente, tocca il **[!UICONTROL Elimina]** per l&#39;origine dati. L’icona Elimina è disabilitata se nel modello dati del modulo viene aggiunto un oggetto modello dati nell’origine dati.

     ![fdm-properties](assets/fdm-properties.png)

1. Tocca **[!UICONTROL Salva e chiudi]** per salvare gli aggiornamenti.

>[!NOTE]
>
>Dopo aver aggiunto nuove origini dati o aggiornato le origini dati esistenti in un modello dati del modulo, assicurati di aggiornare i riferimenti di associazione, a seconda delle necessità, in Adaptive Forms<!--and interactive communications--> che utilizzano il modello dati del modulo aggiornato.

## Configurazioni in base al contesto per modalità di esecuzione specifiche {#runmode-specific-context-aware-config}

[!UICONTROL Modello dati modulo] utilizza [Configurazioni in base al contesto di Sling](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) per supportare diversi parametri di origine dati per la connessione con origini dati per diversi [!DNL Experience Manager] modalità di esecuzione.

Quando [!UICONTROL Modello dati modulo] utilizza le configurazioni cloud per memorizzare i parametri, che quando vengono archiviati e distribuiti tramite il controllo del codice sorgente (archivio GIT di Cloud-Manager) creano una configurazione cloud con gli stessi parametri per tutte le modalità di esecuzione (Sviluppo, Stage e Produzione). Tuttavia, per i casi di utilizzo in cui è necessario disporre di set di dati diversi per ambienti di test e di produzione, utilizziamo i parametri dell’origine dati (ad esempio, URL dell’origine dati) per diversi [!DNL Experience Manager] modalità di esecuzione.

A questo scopo, devi creare una configurazione OSGi che contenga coppie parametri-valore dell’origine dati. Questo sostituisce la stessa coppia da [!UICONTROL Modello dati modulo] configurazione cloud in fase di esecuzione. Poiché le configurazioni OSGi supportano queste modalità di esecuzione per impostazione predefinita, puoi sostituire un parametro dell’origine dati con valori diversi in base alla modalità di esecuzione.

Per abilitare le configurazioni cloud specifiche per l’implementazione in [!UICONTROL Modello dati modulo]:

1. Crea la configurazione cloud nell’istanza di sviluppo locale. Per i passaggi dettagliati, consulta [Come configurare le origini dati](/help/forms/configure-data-sources.md).

1. Memorizza la configurazione cloud nel file system.
   1. Crea pacchetto con filtro `/conf/{foldername}/settings/cloudconfigs/fdm`. Usa lo stesso `{foldername}` come nel passaggio 1. E sostituisci `fdm` con `azurestorage` per la configurazione dell’archiviazione Azure.
   1. Creare e scaricare il pacchetto. Per ulteriori informazioni, consulta [azioni del pacchetto](/help/implementing/developing/tools/package-manager.md).

1. Integrare la configurazione cloud in [!DNL Experience Manager] Progetto Archetipo.
   1. Decomprimi il pacchetto scaricato.
   1. Copia `jcr_root` e inseriscilo nella tua cartella `ui.content` > `src` > `main` > `content`.
   1. Aggiorna `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` per contenere il filtro `/conf/{foldername}/settings/cloudconfigs/fdm`. Per ulteriori informazioni, consulta [Modulo ui.content di Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). Quando questo progetto di archetipo viene distribuito tramite la pipeline CM, la stessa configurazione cloud viene installata in tutti gli ambienti (o modalità di esecuzione). Per modificare il valore dei campi (come URL) delle configurazioni cloud basate sull’ambiente, utilizza la configurazione OSGi descritta nel passaggio seguente.

1. Crea una configurazione in base al contesto di Apache Sling. Per creare la configurazione OSGi:
   1. **Configurare i file di configurazione OSGi in [!DNL Experience Manager] Progetto Archetipo.**
Creare file di configurazione di fabbrica OSGi con PID `org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`. Creare un file con lo stesso nome in ogni cartella della modalità di esecuzione in cui è necessario modificare i valori per ogni modalità di esecuzione. Per ulteriori informazioni, consulta [Configurazione di OSGi per [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **Imposta il codice JSON di configurazione OSGI.** Per utilizzare il provider di override della configurazione in base al contesto di Apache Sling:
      1. Sull’istanza di sviluppo locale `/system/console/configMgr`, seleziona factory OSGi configuration (Configurazione OSGi in fabbrica) con il nome **[!UICONTROL Provider di sostituzione configurazione in base al contesto Apache Sling: configurazione OSGi]**.
      1. Fornisci una descrizione.
      1. Seleziona **[!UICONTROL abilitato]**.
      1. In sostituzioni, fornisci i campi che devono essere modificati in base all’ambiente nella sintassi di sostituzione Sling. Per ulteriori informazioni, consulta [Configurazione in base al contesto di Apache Sling - Override](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). Esempio: `cloudconfigs/fdm/{configName}/url="newURL"`.
È possibile aggiungere più sostituzioni selezionando **[!UICONTROL +]**.
      1. Seleziona **[!UICONTROL Salva]**.
      1. Per ottenere il JSON di configurazione OSGi, segui i passaggi descritti in [Generazione di configurazioni OSGi tramite QuickStart per SDK AEM](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart).
      1. Inserisci JSON nei file di configurazione di fabbrica OSGi creati nel passaggio precedente.
      1. Modifica il valore di `newURL` in base all’ambiente (o in modalità di esecuzione).
      1. Per modificare il valore segreto in base alla modalità di esecuzione, è possibile creare una variabile segreta utilizzando [API di cloud manager](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) e versioni successive possono essere utilizzate nella [Configurazione OSGi](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
Quando questo progetto di archetipo viene distribuito tramite pipeline CM, l’override fornirà valori diversi in ambienti diversi (o in modalità di esecuzione).
      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] gli utenti possono crittografare i valori segreti utilizzando il supporto di crittografia (per i dettagli, vedi [supporto della crittografia per le proprietà di configurazione](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) e inserisci il testo crittografato nel valore dopo [configurazioni in base al contesto disponibili in service pack 6.5.13.0](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. Aggiornare le definizioni dell&#39;origine dati utilizzando l&#39;opzione per aggiornare le definizioni dell&#39;origine dati in [Editor modello dati modulo](#data-sources) per aggiornare la cache FDM tramite l’interfaccia utente di FDM e ottenere la configurazione più recente.

## Passaggi successivi {#next-steps}

Ora disponi di un modello dati modulo con origini dati aggiunte. È quindi possibile modificare il modello dati modulo per aggiungere e configurare oggetti e servizi del modello dati, aggiungere associazioni tra oggetti del modello dati, modificare proprietà, aggiungere oggetti e proprietà del modello dati personalizzato, generare dati di esempio e così via.

Per ulteriori informazioni, consulta [Utilizzare il modello dati del modulo](work-with-form-data-model.md).


>[!MORELIKETHIS]
>
>* [Utilizzare il modello di dati del modulo](/help/forms/using-form-data-model.md)