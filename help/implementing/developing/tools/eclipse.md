---
title: AEM Developer Tools for Eclipse
description: AEM Developer Tools for Eclipse
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 1%

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## Panoramica {#overview}

AEM Developer Tools for Eclipse è un plugin Eclipse basato sul [plugin Eclipse per Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) rilasciato sotto la licenza Apache 2.

Offre diverse funzioni che semplificano AEM sviluppo:

* Integrazione perfetta con AEM istanze tramite il connettore Eclipse Server
* Sincronizzazione per contenuti e bundle OSGi
* Supporto per il debug con la funzionalità di sostituzione del codice a caldo
* Avvio semplice di AEM progetti tramite una procedura guidata specifica per la creazione di progetti
* Facile modifica delle proprietà JCR

## Requisiti {#requirements}

Prima di utilizzare gli AEM Developer Tools, è necessario:

* Scaricate e installate [Eclipse IDE for Enterprise Java Developers](https://www.eclipse.org/downloads/packages/).
* Configurate l&#39;installazione dell&#39;eclisse per garantire che vi siano almeno 1 gigabyte di memoria heap modificando il file di configurazione `eclipse.ini` come descritto nelle [Domande frequenti su Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>In macOS, è necessario fare clic con il pulsante destro del mouse su **Eclipse.app**, quindi selezionare **Mostra contenuto pacchetto** per trovare il `eclipse.ini`**.**

## Come installare AEM Developer Tools per Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Una volta soddisfatti i [requisiti](#requirements) sopra, potete installare il plug-in come segue:

1. Aprire il [sito Web AEM Developer Tools.](https://eclipse.adobe.com/aem/dev-tools/)

1. Copiare il **collegamento di installazione**.

   In alternativa potete scaricare un archivio invece di utilizzare il collegamento di installazione. Questo consente l&#39;installazione offline, ma in questo modo non riceverete notifiche di aggiornamento automatiche.

1. In Eclipse, aprire il menu **Help**.
1. Fare clic su **Installa nuovo software**.
1. Fate clic su **Aggiungi...**.
1. In **Name** immettere `AEM Developer Tools`.
1. In **Posizione** copiare l&#39;URL di installazione.
1. Fate clic su **Aggiungi**.
1. Controllare i plug-in **AEM** e **Sling**.
1. Fai clic su **Avanti**.
1. Nella finestra **Install Details** fare di nuovo clic su **Next**.
1. Accettate i contratti di licenza e fate clic su **Fine**.
1. Fare clic su **RestartNow** per riavviare Eclipse.

## La prospettiva AEM {#the-aem-perspective}

In Eclipse una prospettiva determina le azioni e le viste disponibili all’interno di una finestra e abilita l’interazione orientata alle attività con le risorse in Eclipse. Per ulteriori dettagli sulla prospettiva, consultare la [documentazione di Eclipse.](https://help.eclipse.org)

AEM Strumenti di sviluppo per Eclipse fornisce una AEM prospettiva che offre il pieno controllo sui progetti e le istanze AEM. Per aprire la prospettiva AEM:

1. Dalla barra dei menu Eclipse, selezionare **Finestra** -> **Prospettiva** -> **Apri prospettiva** -> **Altro**.
1. Selezionare **AEM** nella finestra di dialogo e fare clic su **Apri**.

![La prospettiva AEM in Eclipse](assets/eclipse-aem-perspective.png)

## Esempio di progetto multi-modulo {#sample-multi-module-project}

AEM Developer Tools for Eclipse è dotato di un progetto multivodulo di esempio che consente di acquisire rapidamente la massima velocità grazie alla configurazione di un progetto in Eclipse, oltre a fungere da guida best practice per diverse funzioni AEM. [Ulteriori informazioni su Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

Per creare il progetto di esempio, effettuate le seguenti operazioni:

1. Nel menu **File** > **New** > **Project**, passare alla sezione **AEM** e selezionare **AEM Sample Multi-Module Project**.

   ![AEM esempio di progetto con più moduli](assets/aem-sample-project.png)

1. Fai clic su **Avanti**.

   >[!NOTE]
   >
   >Questo passaggio potrebbe richiedere alcuni minuti perché m2eclipse deve eseguire la scansione dei cataloghi archetype.

1. Scegliere `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` dal menu, quindi fare clic su **Next**.

   ![Seleziona versione archetipo](assets/select-archetype.png)

1. Immettete i seguenti campi per il progetto di esempio:

   * **Nome**
   * **ID gruppo**
   * **Id Artifact**
   * **appId** : per impostare questo valore potrebbe essere necessario espandere le  **** opzioni Avanzate.
   * **appTitle** - Per impostare questo valore potrebbe essere necessario espandere le  **** opzioni Avanzate.
   * **Pacchetto** : per impostare questo valore potrebbe essere necessario espandere le  **** opzioni Avanzate.

   ![Definizione delle proprietà archetype](assets/archetype-properties.png)

1. Fai clic su **Avanti**.

1. Quindi configurate un server AEM a cui Eclipse si connetterà.

   Per utilizzare la funzione Debugger, è necessario aver avviato AEM in modalità debug, che può essere ottenuta ad esempio aggiungendo quanto segue alla riga di comando:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Connetti al server AEM](assets/connect-server.png)

1. Fare clic su **Fine**. La struttura del progetto viene creata.

   >[!NOTE]
   >
   >In una nuova installazione (più precisamente, quando le dipendenze di colore non sono mai state scaricate) è possibile che il progetto venga creato con errori. In questo caso, seguire la procedura descritta in [Risoluzione della definizione di progetto non valida](#resolving-invalid-project-definition).

## Come importare progetti esistenti {#how-to-import-existing-projects}

È possibile utilizzare la funzione **Nuovo progetto** per creare la struttura giusta:

1. Seguite le istruzioni per creare un [Esempio di progetto multi-modulo](#sample-multi-module-project) e avrete i seguenti progetti creati per voi, che consentiranno una sana separazione delle preoccupazioni:

   * `PROJECT.ui.apps` per  `/apps` e  `/etc` contenuto
   * `PROJECT.ui.content` per  `/content` cui è stato creato
   * `PROJECT.core` per i bundle Java (questi diventeranno interessanti non appena si desidera aggiungere codice Java)
   * `PROJECT.it.launcher` e  `PROJECT.it.tests` per test di integrazione

1. Sostituite il contenuto del progetto `PROJECT.ui.apps` con le cartelle `apps` e `etc` del pacchetto:

   1. Nel pannello Esplora progetti, aprire `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Fare clic con il pulsante destro del mouse sulla cartella `apps` e scegliere **Mostra in** > **System Explorer**.
   1. Eliminate le cartelle `apps` e `etc` che dovrebbero essere visualizzate e inserite qui le cartelle `apps` e `etc` del pacchetto di contenuti.
   1. In Eclipse, fare clic con il pulsante destro del mouse sul progetto `PROJECT.ui.apps` e scegliere **Aggiorna**.

1. Quindi eseguite le stesse operazioni per `PROJECT.ui.content` e sostituite la cartella del contenuto con quella del pacchetto:

   1. Nel pannello Esplora progetti, aprire `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Fare clic con il pulsante destro del mouse sulla cartella del contenuto più profondo e scegliere **Mostra in** -> **System Explorer**.
   1. Eliminate la cartella del contenuto da visualizzare e inserite qui la cartella del contenuto del pacchetto di contenuto.
   1. In Eclipse, fare clic con il pulsante destro del mouse sul progetto `PROJECT.ui.content` e scegliere **Aggiorna**.

1. Ora è necessario aggiornare i file `filter.xml` di questi due progetti in modo che corrispondano al contenuto del pacchetto di contenuti. A questo scopo, aprite il file `META-INF/vault/filter.xml` del pacchetto di contenuti in un editor di testo/codice separato.

   * Questo è un esempio di come può essere visualizzato il file `filter.xml`:

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

1. Per quanto riguarda il contenuto del pacchetto suddiviso in due progetti, dovrete anche dividere queste regole di filtro in due e aggiornare di conseguenza i file `filter.xml` dei due progetti.

   1. In Eclipse, aprire `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Sostituire il contenuto dell&#39;elemento `<workspaceFilter>` con le regole del pacchetto che iniziano con `/apps` e `/etc`
      * Esempio:

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/apps/foo"/>
            <filter root="/apps/foundation/components/bar"/>
            <filter root="/etc/designs/foo"/>
         </workspaceFilter>
         ```
   1. Quindi aprire `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
   1. Sostituisci le regole con quelle del pacchetto che iniziano con `/content`.
      * Esempio:

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. Assicuratevi di salvare tutte le modifiche. Ora potete sincronizzare il nuovo contenuto con l&#39;istanza AEM.

1. Nel pannello Server, accertatevi che la connessione sia avviata e, in caso contrario, avviatela.
1. Fare clic sull&#39;icona **Pulisci e pubblica**.

Al termine, il pacchetto deve essere eseguito sull&#39;istanza e al momento del salvataggio, ogni modifica viene automaticamente sincronizzata con l&#39;istanza.

Se desiderate rigenerare un pacchetto dal progetto, fate clic con il pulsante destro del mouse su `PROJECT.ui.apps` o `PROJECT.ui.content` e scegliete **Esegui come** -> **Installazione Paradiso**.

Ora disponete di una cartella di destinazione creata con il pacchetto all’interno (denominata ad esempio `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Risoluzione dei problemi {#troubleshooting}

### Risoluzione della definizione di progetto non valida {#resolving-invalid-project-definition}

Per risolvere dipendenze non valide e definire il progetto, procedere come segue:

1. Seleziona tutti i progetti creati.
1. Fare clic con il pulsante destro del mouse.
1. Nel menu di scelta rapida, selezionare **Maven** -> **Aggiorna progetti**.
1. Selezionare **Forza aggiornamenti di snapshot/release**.
1. Fai clic su **OK**.

Eclipse scarica le dipendenze richieste. Questo potrebbe richiedere un momento.

## Ulteriori informazioni {#more-information}

Il sito ufficiale Apache Sling IDE tooltool per Eclipse fornisce informazioni utili:

* La [**Apache Sling IDE tooling for Eclipse** User Guide](https://sling.apache.org/documentation/development/ide-tooling.html), questa documentazione vi guiderà attraverso i concetti generali, l&#39;integrazione dei server e le funzionalità di distribuzione supportate dagli strumenti di sviluppo AEM.
* La sezione [Risoluzione dei problemi](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* Elenco [Problemi noti](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

La seguente documentazione ufficiale [Eclipse](https://eclipse.org/) può aiutare a configurare l&#39;ambiente:

* [Guida introduttiva ad Eclipse](https://eclipse.org/users/)
* [Eclipse Luna Help System](https://help.eclipse.org/luna/index.jsp)
* [Integrazione di Maven (m2eclipse)](https://www.eclipse.org/m2e/)
