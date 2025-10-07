---
title: Strumenti per sviluppatori AEM per Eclipse
description: Scopri come utilizzare AEM Developer Tools per Eclipse, un plug-in di Eclipse basato sul plug-in di Eclipse per Apache Sling.
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ba42d58a4e55efdada35cc7706d736a7314ba743
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 2%

---

# Strumenti per sviluppatori AEM per Eclipse{#aem-developer-tools-for-eclipse}

![Logo Strumenti per sviluppatori Experience Manager per Eclipse](assets/eclipse-logo.png)

## Panoramica {#overview}

_Experience Manager Developer Tools per Eclipse_ è un plug-in Eclipse basato sul [plug-in Eclipse per Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) rilasciato con la licenza Apache 2.

Offre diverse funzioni che facilitano lo sviluppo di AEM:

* Integrazione perfetta con le istanze di AEM tramite il connettore server Eclipse
* Sincronizzazione per i bundle OSGi e per i contenuti
* Supporto del debug con funzionalità di hot-swapping del codice
* Creazione guidata progetto: semplice Bootstrap di progetti AEM
* Facile modifica delle proprietà JCR

## Requisiti {#requirements}

Prima di utilizzare gli strumenti per sviluppatori di AEM, è necessario:

* Scarica e installa [Eclipse IDE per sviluppatori Java™ Enterprise](https://www.eclipse.org/downloads/packages/).
* Configurare l&#39;installazione di eclipse per assicurarsi di disporre di almeno 1 GB di memoria heap modificando il file di configurazione `eclipse.ini` come descritto nelle [Domande frequenti su Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)

>[!NOTE]
>
>In macOS, è necessario fare clic con il pulsante destro del mouse su **Eclipse.app**, quindi selezionare **Mostra contenuto pacchetto** per trovare `eclipse.ini`**.**

## Installare AEM Developer Tools per Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Dopo aver soddisfatto i [requisiti](#requirements) di cui sopra, puoi installare il plug-in come segue:

1. Aprire il [sito Web AEM Developer Tools](https://eclipse.adobe.com/).

<!-- had to update the link again - was https://eclipse.adobe.com/com.adobe.granite.ide.p2update-1.3.0.zip -->
<!-- RB: OLD URL was (https://eclipse.adobe.com/aem/dev-tools/) This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. Copia il **collegamento di installazione**.

   In alternativa, è possibile scaricare un archivio invece di utilizzare il collegamento di installazione. Questo metodo consente l&#39;installazione offline, ma non si ricevono notifiche di aggiornamento automatico in questo modo.

1. In Eclipse aprire il menu **Guida**.
1. Fare clic su **Installa nuovo software**.
1. Fare clic su **Aggiungi...**.
1. Nel campo **Name**, immetti `AEM Developer Tools`.
1. Nel campo **Posizione**, copia l&#39;URL di installazione.
1. Fai clic su **Aggiungi**.
1. Controlla entrambi i plug-in **AEM** e **Sling**.
1. Fai clic su **Avanti**.
1. Nella finestra **Installa dettagli**, fai di nuovo clic su **Avanti**.
1. Accettare i contratti di licenza e fare clic su **Fine**.
1. Fare clic su **RiavviaOra** per riavviare Eclipse.

## La prospettiva di AEM {#the-aem-perspective}

In Eclipse, una prospettiva determina le azioni e le viste disponibili all’interno di una finestra e consente un’interazione orientata alle attività con le risorse in Eclipse. Per ulteriori dettagli su Prospettiva, consulta la [documentazione di Eclipse](https://help.eclipse.org/latest/index.jsp).

_Gli strumenti di sviluppo Experience Manager per Eclipse_ forniscono una prospettiva AEM che ti offre il controllo completo sui tuoi progetti e istanze AEM. Per aprire la prospettiva di AEM:

1. Dalla barra dei menu Eclipse, seleziona **Finestra** > **Prospettiva** > **Apri prospettiva** > **Altro**.
1. Seleziona **AEM** nella finestra di dialogo e fai clic su **Apri**.

![La prospettiva di AEM in Eclipse](assets/eclipse-aem-perspective.png)

## Esempio di progetto con più moduli {#sample-multi-module-project}

Il _Experience Manager Developer Tools per Eclipse_ viene fornito con un esempio di progetto con più moduli che consente di iniziare rapidamente a utilizzare la configurazione di un progetto in Eclipse. Funge anche da guida alle best practice per diverse funzioni di AEM. [Ulteriori informazioni su Archetipo progetto](https://github.com/adobe/aem-project-archetype).

Per creare il progetto di esempio, segui la procedura riportata di seguito.

1. Nel menu **File** > **Nuovo** > **Progetto**, individua la sezione **AEM** e seleziona **Progetto con più moduli di esempio AEM**.

   ![Progetto con più moduli di esempio AEM](assets/aem-sample-project.png)

1. Fai clic su **Avanti**.

   >[!NOTE]
   >
   >Questo passaggio potrebbe richiedere alcuni minuti perché m2eclipse deve eseguire la scansione dei cataloghi dell’archetipo.

1. Scegli `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` dal menu, quindi fai clic su **Avanti**.

   ![Seleziona la versione dell&#39;archetipo](assets/select-archetype.png)

1. Fornisci i campi seguenti per il progetto di esempio:

   * **Nome**
   * **ID gruppo**
   * **ID elemento**
   * **appId** - Potrebbe essere necessario espandere le opzioni **Avanzate** per impostare questo valore.
   * **appTitle** - Potrebbe essere necessario espandere le opzioni **Advanced** per impostare questo valore.
   * **Pacchetto** - Potrebbe essere necessario espandere le opzioni **Avanzate** per impostare questo valore.

   ![Definire le proprietà dell&#39;archetipo](assets/archetype-properties.png)

1. Fai clic su **Avanti**.

1. Quindi configura un server AEM a cui si connette Eclipse.

   Per utilizzare la funzione di debugger, è necessario avviare AEM in modalità di debug, ottenibile aggiungendo quanto segue alla riga di comando:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Connetti al server AEM](assets/connect-server.png)

1. Fare clic su **Fine**. Viene creata la struttura del progetto.

   >[!NOTE]
   >
   >In una nuova installazione (nello specifico, quando le dipendenze Maven non sono mai state scaricate) puoi creare il progetto con errori. In questo caso, seguire la procedura descritta in [Risoluzione della definizione del progetto non valida](#resolving-invalid-project-definition).

## Importare Progetti Esistenti {#how-to-import-existing-projects}

È possibile utilizzare la funzionalità **Nuovo progetto** per creare la struttura corretta:

1. Segui le istruzioni per creare un [progetto con più moduli di esempio](#sample-multi-module-project) e hai creato i seguenti progetti, che consentono una valida separazione dei problemi:

   * `PROJECT.ui.apps` per il contenuto di `/apps` e `/etc`
   * `PROJECT.ui.content` per `/content` creato
   * `PROJECT.core` per bundle Java™ (diventano interessanti quando si desidera aggiungere codice Java™)
   * `PROJECT.it.launcher` e `PROJECT.it.tests` per gli integration test

1. Sostituisci il contenuto del progetto `PROJECT.ui.apps` con le cartelle `apps` e `etc` del pacchetto:

   1. Nel pannello Esplora progetti, apri `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Fare clic con il pulsante destro del mouse sulla cartella `apps` e scegliere **Mostra in** > **Esplora risorse**.
   1. Eliminare le cartelle `apps` e `etc` da visualizzare e inserire qui le cartelle `apps` e `etc` del pacchetto di contenuti.
   1. In Eclipse fare clic con il pulsante destro del mouse sul progetto `PROJECT.ui.apps` e scegliere **Aggiorna**.

1. Eseguire quindi le stesse operazioni per `PROJECT.ui.content` e sostituire la cartella dei contenuti con quella dei pacchetti:

   1. Nel pannello Esplora progetti, apri `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Fare clic con il pulsante destro del mouse sulla cartella dei contenuti più profondi e scegliere **Mostra in** > **Esplora sistemi**.
   1. Elimina la cartella dei contenuti da visualizzare e inserisci qui la cartella dei contenuti del pacchetto di contenuti.
   1. In Eclipse fare clic con il pulsante destro del mouse sul progetto `PROJECT.ui.content` e scegliere **Aggiorna**.

1. Ora è necessario aggiornare i file `filter.xml` di questi due progetti in modo che corrispondano al contenuto del pacchetto di contenuti. Per questo, apri il file `META-INF/vault/filter.xml` del pacchetto di contenuti in un editor di testo/codice separato.

   * Ecco un esempio di come può apparire il file `filter.xml`:

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

1. Per quanto riguarda il contenuto del pacchetto diviso in due progetti, è necessario suddividere queste regole di filtro in due e aggiornare di conseguenza i file `filter.xml` dei due progetti.

   1. In Eclipse aprire `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Sostituisci il contenuto dell&#39;elemento `<workspaceFilter>` con le regole del pacchetto che iniziano con `/apps` e `/etc`
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

1. Assicurati di salvare tutte le modifiche. Ora puoi sincronizzare il nuovo contenuto con l’istanza di AEM.

1. Nel pannello Server, accertatevi che la connessione sia avviata e, in caso contrario, avviatela.
1. Fai clic sull&#39;icona **Pulisci e pubblica**.

Al termine, il pacchetto dovrebbe essere in esecuzione sull’istanza e, al momento del salvataggio, qualsiasi modifica viene sincronizzata automaticamente con l’istanza.

Se desideri ricreare un pacchetto dal progetto, fai clic con il pulsante destro del mouse su `PROJECT.ui.apps` o `PROJECT.ui.content` e scegli **Esegui come** > **Installazione Maven**.

È ora disponibile una cartella di destinazione creata con il pacchetto all&#39;interno (denominata, ad esempio, `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Risoluzione di problemi {#troubleshooting}

### Risoluzione di una definizione di progetto non valida {#resolving-invalid-project-definition}

Per risolvere le dipendenze non valide e la definizione del progetto procedere come segue:

1. Seleziona tutti i progetti creati.
1. Fare clic con il pulsante destro del mouse.
1. Nel menu di scelta rapida, seleziona **Maven** > **Aggiorna progetti**.
1. Controlla **Forza aggiornamenti di snapshot/release**.
1. Fai clic su **OK**.

Eclipse scarica le dipendenze richieste. L&#39;operazione potrebbe richiedere alcuni minuti.

## Ulteriori informazioni {#more-information}

Il sito web ufficiale Apache Sling IDE tooling per Eclipse fornisce informazioni utili:

* La [**Guida utente di Apache Sling IDE tooling per Eclipse**](https://sling.apache.org/documentation/development/ide-tooling.html), questa documentazione ti guida attraverso i concetti generali, l&#39;integrazione del server e le funzionalità di distribuzione supportate dagli strumenti di sviluppo di AEM.
* La [sezione Risoluzione dei problemi](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* [Elenco dei problemi noti](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

La seguente documentazione ufficiale di [Eclipse](https://www.eclipse.org/) può essere utile per configurare l&#39;ambiente:

* [Guida introduttiva a Eclipse](https://eclipseide.org/getting-started/)
* [Guida di Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integrazione Maven (m2eclipse)](https://www.eclipse.org/m2e/)
