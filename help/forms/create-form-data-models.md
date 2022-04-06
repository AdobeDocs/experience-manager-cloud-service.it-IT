---
title: Come si crea il modello dati del modulo?
description: L’integrazione dei dati di Experience Manager Forms offre un’interfaccia utente intuitiva per la creazione e l’utilizzo dei modelli di dati dei moduli. Scopri come creare modelli di dati modulo con o senza origini dati configurate.
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 1e2b58015453c194af02fdae62c3735727981da1
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 0%

---

# Crea modello dati modulo {#create-form-data-model}

![Integrazione dei dati](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] l’integrazione dei dati fornisce un’interfaccia utente intuitiva per creare e utilizzare modelli di dati modulo. Un modello dati modulo si basa su origini dati per lo scambio di dati; tuttavia, è possibile creare un modello dati modulo con o senza un’origine dati. Esistono due approcci per creare un modello dati da a seconda che siano state configurate origini dati:

* **Utilizzo di origini dati preconfigurate**: Se hai configurato origini dati come descritto in [Configurare origini dati](configure-data-sources.md), è possibile selezionarli durante la creazione di un modello dati del modulo. Porta tutti gli oggetti, le proprietà e i servizi del modello dati dalle origini dati selezionate disponibili per l’uso nel modello dati del modulo.

* **Senza origini dati**: Se non sono state configurate origini dati per il modello dati del modulo, è comunque possibile crearlo senza origini dati. È possibile utilizzare il modello dati modulo per creare un Forms adattivo <!--and interactive communication--> e testarli utilizzando dati campione. Quando sono disponibili origini dati, è possibile eseguire un binding del modello dati del modulo con origini dati, che si riflettono automaticamente nel Forms adattivo associato<!--and interactive communications-->.

>[!NOTE]
>
>Devi essere membro di entrambi **fdm-author** e **form-user** gruppi per poter creare e utilizzare il modello dati del modulo. Contatta il tuo [!DNL Experience Manager] amministratore per diventare membro dei gruppi.

## Crea modello dati modulo {#data-sources}

Verificare di aver configurato le origini dati che si desidera utilizzare nel modello dati modulo come descritto in [Configurare origini dati](configure-data-sources.md). Per creare un modello dati modulo basato su origini dati configurate, effettuare le seguenti operazioni:

1. In [!DNL Experience Manager] istanza autore, passa a **[!UICONTROL Forms > Integrazioni dati]**.
1. Tocca **[!UICONTROL Crea > Modello dati modulo]**.
1. Nella finestra di dialogo Crea modello dati modulo :

   * Specificare un nome per il modello dati del modulo.
   * (**Facoltativo**) Specifica titolo, descrizione e tag per il modello dati del modulo.
   * (**Facoltativo e applicabile solo se le origini dati sono configurate**) Tocca l’icona di spunta accanto a **[!UICONTROL Configurazione origine dati]** e seleziona il nodo di configurazione in cui risiedono i servizi cloud per le origini dati che desideri utilizzare. Limita l’elenco delle origini dati disponibili per la selezione nella pagina successiva a quelle disponibili nel nodo di configurazione selezionato. Tuttavia, qualsiasi database JDBC e [!DNL Experience Manager] le origini dati del profilo utente sono elencate per impostazione predefinita. Se non selezioni un nodo di configurazione, vengono elencate le origini dati da tutti i nodi di configurazione.

1. Tocca **[!UICONTROL Successivo]**.

1. (**Applicabile solo se le origini dati sono configurate**) **[!UICONTROL Seleziona origine dati]** in questa schermata sono elencate le eventuali origini dati disponibili. Selezionare le origini dati da utilizzare nel modello dati del modulo.
1. Tocca **[!UICONTROL Crea]** e nella finestra di dialogo di conferma, tocca **[!UICONTROL Apri]** per aprire l’editor per modelli dati modulo.

   Esaminiamo i diversi componenti dell’interfaccia utente dell’Editor modelli dati per moduli.

   ![Un modello dati modulo con tre origini dati: un servizio RESTful, [!DNL Experience Manager] profilo utente e un RDBMS](assets/fdm-ui.png)

   A. **[!UICONTROL Origini dati]** Elenca le origini dati in un modello dati modulo. Espandere un’origine dati per visualizzare gli oggetti e i servizi del modello dati corrispondente.

   B. **[!UICONTROL Aggiorna definizioni origine dati]** Recupera eventuali modifiche nelle definizioni dell’origine dati da origini dati configurate e le aggiorna nella scheda Origini dati dell’Editor modello dati modulo.

   C. **[!UICONTROL Modello]** Area contenuto in cui vengono visualizzati gli oggetti del modello dati aggiunti.

   D. **[!UICONTROL Servizi]** Area contenuto in cui vengono visualizzate operazioni o servizi di origine dati aggiunti.

   E. **[!UICONTROL Barra degli strumenti]** Strumenti per l’utilizzo del modello dati del modulo. La barra degli strumenti mostra più opzioni a seconda dell’oggetto selezionato nel modello dati del modulo.

   F. **[!UICONTROL Aggiungi selezionati]** Aggiunge oggetti e servizi del modello dati selezionati al modello dati del modulo.

Per ulteriori informazioni sull’editor di modelli dati modulo e su come utilizzarlo per modificare e configurare il modello dati modulo, consulta [Utilizzare il modello dati del modulo](work-with-form-data-model.md).

## Aggiorna origini dati {#update}

Per aggiungere o aggiornare origini dati a un modello dati modulo esistente, procedere come segue.

1. Vai a **[!UICONTROL Forms > Integrazioni dati]**, selezionare il Modello dati modulo in cui si desidera aggiungere o aggiornare le origini dati, quindi toccare **[!UICONTROL Proprietà]**.
1. Nelle proprietà del modello dati modulo, passare alla **[!UICONTROL Aggiorna origine]** scheda .

   In **[!UICONTROL Aggiorna origine]** scheda:

   * Tocca l’icona Sfoglia in **[!UICONTROL Configurazione in base al contesto]** e selezionare un nodo di configurazione in cui risiede la configurazione cloud per l&#39;origine dati che si desidera aggiungere. Se non selezioni un nodo, le configurazioni cloud risiedono solo nel `global` quando tocchi , vengono elencati i nodi **[!UICONTROL Aggiungi origini]**.

   * Per aggiungere una nuova origine dati, tocca **[!UICONTROL Aggiungi origini]** e selezionare le origini dati da aggiungere al modello dati del modulo. Tutte le origini dati configurate in `global` e viene visualizzato l&#39;eventuale nodo di configurazione selezionato.

   * Per sostituire un’origine dati esistente con un’altra origine dati dello stesso tipo, tocca **[!UICONTROL Modifica]** per l’origine dati e seleziona dall’elenco delle origini dati disponibili.
   * Per eliminare un’origine dati esistente, tocca **[!UICONTROL Elimina]** per l’origine dati. L’icona Elimina è disabilitata se un oggetto modello dati nell’origine dati viene aggiunto nel modello dati del modulo.

      ![proprietà fdm](assets/fdm-properties.png)

1. Tocca **[!UICONTROL Salva e chiudi]** per salvare gli aggiornamenti.

>[!NOTE]
>
>Dopo aver aggiunto nuove origini dati o aggiornato le origini dati esistenti in un modello dati del modulo, assicurarsi di aggiornare i riferimenti di binding, come appropriato, in Forms adattivo<!--and interactive communications--> che utilizzano il modello dati del modulo aggiornato.

## Configurazioni in base al contesto per modalità di esecuzione specifiche {#runmode-specific-context-aware-config}

[!UICONTROL Modello dati modulo] utilizza [Configurazioni basate sul contesto Sling](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) per supportare diversi parametri dell’origine dati per la connessione con origini dati diverse [!DNL Experience Manager] modalità di esecuzione.

Quando [!UICONTROL Modello dati modulo] utilizza le configurazioni cloud per memorizzare i parametri, che quando vengono archiviati e distribuiti tramite il controllo del codice sorgente (archivio GIT di Cloud-Manager) crea una configurazione cloud con gli stessi parametri per tutte le modalità di esecuzione (Sviluppo, Stage e Produzione). Tuttavia, per i casi d’uso in cui è necessario disporre di set di dati diversi per gli ambienti di test e produzione, utilizziamo i parametri dell’origine dati (ad esempio l’URL dell’origine dati) per diversi [!DNL Experience Manager] modalità di esecuzione.

A questo scopo, devi creare una configurazione OSGi che contenga coppie parametri-valore dell’origine dati. Questo sostituisce la stessa coppia da [!UICONTROL Modello dati modulo] configurazione cloud in fase di esecuzione. Poiché le configurazioni OSGi supportano queste modalità di esecuzione per impostazione predefinita, è possibile sostituire un parametro di origine dati con valori diversi in base alla modalità di esecuzione.

Per abilitare configurazioni cloud specifiche per la distribuzione in [!UICONTROL Modello dati modulo]:

1. Crea la configurazione cloud nell’istanza di sviluppo locale. Per i passaggi dettagliati vedi [Come configurare le origini dati](/help/forms/configure-data-sources.md).

1. Archivia la configurazione cloud nel file system.
   1. Crea pacchetto con filtro `/conf/{foldername}/settings/cloudconfigs/fdm`. Usa lo stesso `{foldername}` come al punto 1. E sostituiscono `fdm` con `azurestorage` per la configurazione di archiviazione di Azure.
   1. Crea e scarica il pacchetto. Per maggiori dettagli, vedi [azioni pacchetto](/help/implementing/developing/tools/package-manager.md).

1. Integrare la configurazione cloud in [!DNL Experience Manager] Progetto Archetype.
   1. Decomprimi il pacchetto scaricato.
   1. Copia `jcr_root` e inseriscila nella cartella `ui.content` > `src` > `main` > `content`.
   1. Aggiorna `ui.content` > `src` > `main` > `content` > `META-INF` > `vault` > `filter.xml` per contenere il filtro `/conf/{foldername}/settings/cloudconfigs/fdm`. Per maggiori dettagli, vedi [modulo ui.content di AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uicontent.html). Quando questo progetto archetipo viene distribuito tramite la pipeline CM, la stessa configurazione cloud viene installata su tutti gli ambienti (o modalità runmode). Per modificare il valore dei campi (come URL) delle configurazioni cloud basate sull’ambiente, utilizza la configurazione OSGi descritta nel passaggio seguente.

1. Crea una configurazione in base al contesto Apache Sling. Per creare la configurazione OSGi:
   1. **Configurare i file di configurazione OSGi in [!DNL Experience Manager] Progetto Archetype.**
Creare file di configurazione OSGi Factory con PID 
`org.apache.sling.caconfig.impl.override.OsgiConfigurationOverrideProvider`. Crea un file con lo stesso nome in ciascuna cartella della modalità di esecuzione in cui i valori devono essere modificati in base alla modalità di esecuzione. Per maggiori dettagli, vedi [Configurazione di OSGi per [!DNL Adobe Experience Manager]](/help/implementing/deploying/configuring-osgi.md#creating-sogi-configurations).

   1. **Imposta il json di configurazione OSGI.** Per utilizzare il provider di sostituzione della configurazione in base al contesto Apache Sling:
      1. Su un&#39;istanza di sviluppo locale `/system/console/configMgr`, seleziona la configurazione OSGi di fabbrica con il nome **[!UICONTROL Provider di sostituzione della configurazione in base al contesto Apache Sling: Configurazione OSGi]**.
      1. Fornisci una descrizione.
      1. Seleziona **[!UICONTROL abilitato]**.
      1. In Sostituzioni, fornisci i campi che devono essere modificati in base all’ambiente nella sintassi di sostituzione sling. Per maggiori dettagli, vedi [Configurazione in base al contesto Apache Sling - Ignora](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration-override.html#override-syntax). Esempio, `cloudconfigs/fdm/{configName}/url="newURL"`.
È possibile aggiungere più sostituzioni selezionando **[!UICONTROL +]**.
      1. Seleziona **[!UICONTROL Salva]**.
      1. Per ottenere il JSON di configurazione OSGi, segui i passaggi in [Generazione di configurazioni OSGi tramite l’SDK Quickstart AEM](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart).
      1. Posiziona JSON nei file di configurazione di fabbrica OSGi creati nel passaggio precedente.
      1. Modifica il valore di `newURL` in base all&#39;ambiente (o modalità runmode).
      1. Per modificare il valore segreto in base alla modalità di esecuzione, è possibile creare una variabile segreta utilizzando [API di cloud manager](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) e successivamente possono essere referenziati nel [Configurazione OSGi](/help/implementing/deploying/configuring-osgi.md#secret-configuration-values).
Quando questo progetto archetipo viene distribuito tramite la pipeline CM, override fornisce valori diversi in ambienti diversi (o modalità di esecuzione).

      >[!NOTE]
      >
      >[!DNL Adobe Managed Service] gli utenti possono crittografare i valori segreti utilizzando il supporto di crypto (per ulteriori informazioni, consulta [supporto per la crittografia delle proprietà di configurazione](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/encryption-support-for-configuration-properties.html#enabling-encryption-support) e inserire testo crittografato nel valore dopo [le configurazioni in base al contesto sono disponibili in service pack 6.5.13.0](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html#runmode-specific-context-aware-config).

1. Aggiornare le definizioni delle origini dati utilizzando l’opzione per aggiornare le definizioni delle origini dati in [Editor modelli dati modulo](#data-sources) per aggiornare la cache FDM tramite l’interfaccia utente FDM e ottenere la configurazione più recente.

## Passaggi successivi {#next-steps}

È ora disponibile un modello dati modulo con origini dati aggiunte. È quindi possibile modificare il modello dati modulo per aggiungere e configurare oggetti e servizi del modello dati, aggiungere associazioni tra oggetti del modello dati, modificare le proprietà, aggiungere oggetti e proprietà del modello dati personalizzato, generare dati di esempio e così via.

Per ulteriori informazioni, consulta [Utilizzare il modello dati del modulo](work-with-form-data-model.md).
