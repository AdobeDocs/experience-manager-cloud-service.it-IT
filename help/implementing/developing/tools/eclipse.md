---
title: Strumenti AEM Developer per Eclipse
description: Scopri come utilizzare AEM Developer Tools per Eclipse, un plug-in di Eclipse basato sul plug-in di Eclipse per Apache Sling.
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 2%

---

# Strumenti AEM Developer per Eclipse{#aem-developer-tools-for-eclipse}

![Logo Experience Manager Developer Tools per Eclipse](assets/eclipse-logo.png)

## Panoramica {#overview}

_Strumenti per sviluppatori Experience Manager per Eclipse_ è un plug-in Eclipse basato su [Plug-in Eclipse per Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) rilasciata con la Licenza Apache 2.

Offre diverse funzioni che facilitano lo sviluppo dell’AEM:

* Integrazione perfetta con le istanze AEM tramite il connettore server Eclipse
* Sincronizzazione per i bundle OSGi e per i contenuti
* Supporto del debug con funzionalità di hot-swapping del codice
* Bootstrap semplice di progetti AEM tramite una procedura guidata specifica per la creazione di progetti
* Facile modifica delle proprietà JCR

## Requisiti {#requirements}

Prima di utilizzare gli strumenti per sviluppatori di AEM, è necessario:

* Scarica e installa [IDE Eclipse per sviluppatori Java™ Enterprise](https://www.eclipse.org/downloads/packages/).
* Configurare l&#39;installazione dell&#39;eclissi per assicurarsi di disporre di almeno 1 GB di memoria heap modificando `eclipse.ini` file di configurazione come descritto in [Domande frequenti su Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>In macOS, è necessario fare clic con il pulsante destro del mouse **Eclipse.app** e quindi selezionare **Mostra contenuto pacchetto** per trovare `eclipse.ini`**.**

## Come installare gli strumenti per sviluppatori AEM per Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Quando hai soddisfatto il [requisiti](#requirements) sopra, è possibile installare il plug-in come segue:

1. Apri [Sito Web degli strumenti per sviluppatori AEM](https://eclipse.adobe.com/com.adobe.granite.ide.p2update-1.3.0.zip). <!-- RB: OLD URL was (https://eclipse.adobe.com/aem/dev-tools/) This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. Copia il **Collegamento di installazione**.

   In alternativa, è possibile scaricare un archivio invece di utilizzare il collegamento di installazione. Questo metodo consente l&#39;installazione offline, ma non si ricevono notifiche di aggiornamento automatico in questo modo.

1. In Eclipse, apri il file **Aiuto** menu.
1. Clic **Installare un nuovo software**.
1. Clic **Aggiungi...**.
1. In **Nome** campo, immetti `AEM Developer Tools`.
1. In **Posizione** , copiare l&#39;URL di installazione.
1. Clic **Aggiungi**.
1. Controlla entrambi **AEM** e **Sling** plug-in.
1. Fai clic su **Avanti**.
1. In **Dettagli di installazione** finestra, fai clic su **Successivo** di nuovo.
1. Accettare i contratti di licenza e fare clic su **Fine**.
1. Clic **RestartNow** per riavviare Eclipse.

## La prospettiva dell&#39;AEM {#the-aem-perspective}

In Eclipse, una prospettiva determina le azioni e le viste disponibili all’interno di una finestra e consente un’interazione orientata alle attività con le risorse in Eclipse. Per ulteriori dettagli su Prospettiva, vedi [Documentazione di Eclipse.](https://help.eclipse.org/latest/index.jsp)

_Strumenti di sviluppo Experience Manager per Eclipse_ fornisci una Prospettiva AEM che ti offra il pieno controllo sui tuoi progetti e istanze AEM. Per aprire la prospettiva AEM:

1. Dalla barra dei menu di Eclipse, seleziona **Finestra** -> **Prospettiva** -> **Prospettiva aperta** -> **Altro**.
1. Seleziona **AEM** nella finestra di dialogo e fai clic su **Apri**.

![La prospettiva AEM in Eclipse](assets/eclipse-aem-perspective.png)

## Esempio di progetto con più moduli {#sample-multi-module-project}

Il _Strumenti per sviluppatori Experience Manager per Eclipse_ viene fornito con un esempio di progetto con più moduli che ti consente di imparare rapidamente a utilizzare la configurazione di un progetto in Eclipse. Funge anche da guida alle best practice per diverse funzioni dell’AEM. [Ulteriori informazioni su Archetipo progetto](https://github.com/adobe/aem-project-archetype).

Per creare il progetto di esempio, segui la procedura riportata di seguito.

1. In **File** > **Nuovo** > **Progetto** , passare al menu **AEM** sezione e seleziona **Esempio di progetto con più moduli AEM**.

   ![Esempio di progetto con più moduli AEM](assets/aem-sample-project.png)

1. Fai clic su **Avanti**.

   >[!NOTE]
   >
   >Questo passaggio potrebbe richiedere un attimo perché m2eclipse deve scansionare i cataloghi dell’archetipo.

1. Scegli `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` dal menu, quindi fai clic su **Successivo**.

   ![Seleziona la versione dell’archetipo](assets/select-archetype.png)

1. Fornisci i campi seguenti per il progetto di esempio:

   * **Nome**
   * **ID gruppo**
   * **ID artefatto**
   * **appId** - Potrebbe essere necessario espandere **Avanzate** per impostare questo valore.
   * **appTitle** - Potrebbe essere necessario espandere **Avanzate** per impostare questo valore.
   * **Pacchetto** - Potrebbe essere necessario espandere **Avanzate** per impostare questo valore.

   ![Definire le proprietà dell’archetipo](assets/archetype-properties.png)

1. Fai clic su **Avanti**.

1. Quindi configura un server AEM a cui si connette Eclipse.

   Per utilizzare la funzione di debugger, è necessario aver avviato AEM in modalità di debug, ottenibile aggiungendo quanto segue alla riga di comando:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Connettersi al server AEM](assets/connect-server.png)

1. Clic **Fine**. Viene creata la struttura del progetto.

   >[!NOTE]
   >
   >In una nuova installazione (nello specifico, quando le dipendenze Maven non sono mai state scaricate) puoi creare il progetto con errori. In questo caso, seguire la procedura descritta in [Risoluzione di una definizione di progetto non valida](#resolving-invalid-project-definition).

## Importare Progetti Esistenti {#how-to-import-existing-projects}

È possibile utilizzare **Nuovo progetto** funzione per creare la struttura adatta alle tue esigenze:

1. Segui le istruzioni per creare una [Esempio di progetto con più moduli](#sample-multi-module-project) e hai creato i seguenti progetti, che permettono una sana separazione delle preoccupazioni:

   * `PROJECT.ui.apps` per `/apps` e `/etc` contenuto
   * `PROJECT.ui.content` per `/content` che è stato creato
   * `PROJECT.core` per i bundle Java™ (che diventano interessanti quando si desidera aggiungere codice Java™)
   * `PROJECT.it.launcher` e `PROJECT.it.tests` per i test di integrazione

1. Sostituisci il contenuto della `PROJECT.ui.apps` progetto con `apps` e `etc` cartelle del pacchetto:

   1. Nel pannello Esplora progetti, apri `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Fare clic con il pulsante destro del mouse `apps` cartella e scegli **Mostra in** > **Esplora sistema**.
   1. Elimina `apps` e `etc` cartelle che ora dovresti visualizzare e inserire qui le `apps` e `etc` cartelle del pacchetto di contenuti.
   1. In Eclipse, fai clic con il pulsante destro del mouse su `PROJECT.ui.apps` progetto e scelta **Aggiorna**.

1. Quindi fai lo stesso per `PROJECT.ui.content` e sostituisci la cartella dei contenuti con uno dei pacchetti:

   1. Nel pannello Esplora progetti, apri `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Fai clic con il pulsante destro del mouse sulla cartella dei contenuti più profondi e scegli **Mostra in** -> **Esplora sistema**.
   1. Elimina la cartella dei contenuti da visualizzare e inserisci qui la cartella dei contenuti del pacchetto di contenuti.
   1. In Eclipse, fai clic con il pulsante destro del mouse su `PROJECT.ui.content` progetto e scelta **Aggiorna**.

1. Ora è necessario aggiornare `filter.xml` i file di questi due progetti in modo che corrispondano al contenuto del pacchetto di contenuti. Per questo, apri il `META-INF/vault/filter.xml` del pacchetto di contenuti in un editor di testo/codice separato.

   * Questo è un esempio di come `filter.xml` il file può avere un aspetto simile a:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. Per quanto riguarda il contenuto del pacchetto diviso in due progetti, devi anche dividere queste regole di filtro in due e aggiornare di conseguenza `filter.xml` file dei due progetti.

   1. In Eclipse, apri `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Sostituisci il contenuto della `<workspaceFilter>` con le regole del pacchetto che iniziano con `/apps` e `/etc`
      * Ad esempio:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/apps/foo"/>
           <filter root="/apps/foundation/components/bar"/>
           <filter root="/etc/designs/foo"/>
        </workspaceFilter>
        ```

   1. Quindi apri `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
   1. Sostituisci le regole con quelle del pacchetto che iniziano con `/content`.
      * Ad esempio:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. Assicurati di salvare tutte le modifiche. Ora puoi sincronizzare il nuovo contenuto con l’istanza AEM.

1. Nel pannello Server, accertatevi che la connessione sia avviata e, in caso contrario, avviatela.
1. Fai clic su **Pulisci e pubblica** icona.

Al termine, il pacchetto dovrebbe essere in esecuzione sull’istanza e, al momento del salvataggio, qualsiasi modifica viene sincronizzata automaticamente con l’istanza.

Se desideri ricreare un pacchetto dal progetto, fai clic con il pulsante destro del mouse su `PROJECT.ui.apps` o `PROJECT.ui.content` e scegli **Esegui come** -> **Installazione Maven**.

Ora disponi di una cartella di destinazione creata con il pacchetto all’interno (denominata, ad esempio `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Risoluzione dei problemi {#troubleshooting}

### Risoluzione di una definizione di progetto non valida {#resolving-invalid-project-definition}

Per risolvere le dipendenze non valide e la definizione del progetto procedere come segue:

1. Seleziona tutti i progetti creati.
1. Fare clic con il pulsante destro del mouse.
1. Nel menu di scelta rapida, selezionare **Maven** -> **Aggiorna Progetti**.
1. Verifica **Forza aggiornamenti di snapshot/release**.
1. Fai clic su **OK**.

Eclipse scarica le dipendenze richieste. L&#39;operazione potrebbe richiedere alcuni minuti.

## Ulteriori informazioni {#more-information}

Il sito web ufficiale Apache Sling IDE tooling per Eclipse fornisce informazioni utili:

* Il [**Strumenti IDE Apache Sling per Eclipse** Guida utente](https://sling.apache.org/documentation/development/ide-tooling.html), questa documentazione descrive i concetti generali, l’integrazione dei server e le funzionalità di implementazione supportate dagli strumenti di sviluppo AEM.
* Il [Sezione Risoluzione dei problemi](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* Il [Elenco dei problemi noti](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

Il seguente funzionario [Eclipse](https://www.eclipse.org/) La documentazione di può essere utile per configurare l’ambiente:

* [Guida introduttiva a Eclipse](https://www.eclipse.org/getting-started/)
* [Guida di Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integrazione Maven (m2eclipse)](https://www.eclipse.org/m2e/)
