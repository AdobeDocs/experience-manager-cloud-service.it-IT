---
title: Strumenti AEM Developer per Eclipse
description: Strumenti AEM Developer per Eclipse
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: 3af790d9b42eb2f685258eb18352ec4cd752efcc
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 3%

---

# Strumenti AEM Developer per Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## Panoramica {#overview}

AEM Developer Tools per Eclipse è un plug-in Eclipse basato su [Plug-in Eclipse per Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) rilasciato sotto la Licenza Apache 2.

Offre diverse funzioni che semplificano AEM sviluppo:

* Integrazione perfetta con le istanze AEM tramite Eclipse Server Connector
* Sincronizzazione sia per il contenuto che per i bundle OSGi
* Supporto per il debug con funzionalità di scambio a caldo del codice
* Bootstrap semplice dei progetti AEM tramite una Creazione guidata progetto specifica
* Editing semplice delle proprietà JCR

## Requisiti {#requirements}

Prima di utilizzare gli strumenti per sviluppatori AEM, è necessario:

* Scarica e installa [Eclipse IDE per sviluppatori Java aziendali](https://www.eclipse.org/downloads/packages/).
* Configura l&#39;installazione dell&#39;eclipse per assicurarti di disporre di almeno 1 gigabyte di memoria heap modificando il tuo `eclipse.ini` file di configurazione come descritto in [Domande frequenti su Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>Su macOS, è necessario fare clic con il pulsante destro del mouse su **Eclipse.app** quindi seleziona **Mostra contenuto del pacchetto** per trovare il `eclipse.ini`**.**

## Come installare AEM Developer Tools per Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Quando hai soddisfatto il [requisiti](#requirements) sopra, è possibile installare il plug-in come segue:

1. Apri [Sito Web AEM Developer Tools](https://eclipse.adobe.com/aem/dev-tools/).

1. Copia il **Collegamento di installazione**.

   In alternativa, puoi scaricare un archivio invece di utilizzare il collegamento di installazione. Questo consente l’installazione offline ma in questo modo le notifiche di aggiornamento automatico verranno perse.

1. In Eclipse, apri la **Aiuto** menu.
1. Fai clic su **Installazione di un nuovo software**.
1. Fate clic su **Aggiungi...**.
1. In **Nome** enter `AEM Developer Tools`.
1. In **Posizione** copia l’URL di installazione.
1. Fate clic su **Aggiungi**.
1. Controlla entrambi **AEM** e **Sling** plugin.
1. Fai clic su **Avanti**.
1. In **Dettagli di installazione** finestra, fai clic su **Successivo** di nuovo.
1. Accettare i contratti di licenza e fare clic su **Fine**.
1. Fai clic su **RestartNow** per riavviare Eclipse.

## La prospettiva AEM {#the-aem-perspective}

In Eclipse una prospettiva determina le azioni e le visualizzazioni disponibili all’interno di una finestra e abilita l’interazione orientata alle attività con le risorse in Eclipse. Per ulteriori dettagli sulla prospettiva, consulta la sezione [Documentazione Eclipse.](https://help.eclipse.org)

Gli strumenti di sviluppo AEM per Eclipse forniscono una prospettiva AEM che offre il pieno controllo sui progetti e le istanze AEM. Per aprire la prospettiva AEM:

1. Dalla barra del menu Eclipse, seleziona **Finestra** -> **Prospettiva** -> **Apri prospettiva** -> **Altro**.
1. Seleziona **AEM** nella finestra di dialogo e fai clic su **Apri**.

![La prospettiva AEM in Eclipse](assets/eclipse-aem-perspective.png)

## Esempio di progetto con più moduli {#sample-multi-module-project}

AEM Developer Tools per Eclipse viene fornito con un progetto campione con più moduli che consente di imparare rapidamente a usare una configurazione di progetto in Eclipse, oltre a fungere da guida pratica per diverse funzioni AEM. [Ulteriori informazioni su Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

Per creare il progetto di esempio, effettua le seguenti operazioni:

1. In **File** > **Nuovo** > **Progetto** menu, passare alla **AEM** e seleziona **Progetto AEM modulo multiplo di esempio**.

   ![Progetto AEM modulo multiplo di esempio](assets/aem-sample-project.png)

1. Fai clic su **Avanti**.

   >[!NOTE]
   >
   >Questo passaggio potrebbe richiedere un momento perché m2eclipse deve scansionare i cataloghi archetipo.

1. Scegli `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` dal menu , quindi fai clic su **Successivo**.

   ![Seleziona versione archetipo](assets/select-archetype.png)

1. Fornisci i campi seguenti per il progetto di esempio:

   * **Nome**
   * **ID gruppo**
   * **Id Artifact**
   * **appId** - Potrebbe essere necessario espandere il **Avanzate** opzioni per impostare questo valore.
   * **appTitle** - Potrebbe essere necessario espandere il **Avanzate** opzioni per impostare questo valore.
   * **Pacchetto** - Potrebbe essere necessario espandere il **Avanzate** opzioni per impostare questo valore.

   ![Definire le proprietà archetipo](assets/archetype-properties.png)

1. Fai clic su **Avanti**.

1. Quindi configura un server AEM a cui Eclipse si connetterà.

   Per utilizzare la funzione di debug, è necessario aver avviato AEM in modalità di debug, che può essere ottenuta, ad esempio, aggiungendo quanto segue alla riga di comando:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Connettersi al server AEM](assets/connect-server.png)

1. Fai clic su **Fine**. Viene creata la struttura del progetto.

   >[!NOTE]
   >
   >In una nuova installazione (in particolare, quando le dipendenze maven non sono mai state scaricate) il progetto potrebbe essere creato con errori. In questo caso si prega di seguire la procedura descritta in [Risoluzione della definizione del progetto non valida](#resolving-invalid-project-definition).

## Importazione di progetti esistenti {#how-to-import-existing-projects}

È possibile utilizzare **Nuovo progetto** per creare la struttura corretta:

1. Segui le istruzioni per creare un [Esempio di progetto con più moduli](#sample-multi-module-project) e avrete i seguenti progetti creati per voi, che permetterà una sana separazione dei problemi:

   * `PROJECT.ui.apps` per `/apps` e `/etc` content
   * `PROJECT.ui.content` per `/content` creato
   * `PROJECT.core` per i bundle Java (questi diventeranno interessanti non appena si desidera aggiungere il codice Java)
   * `PROJECT.it.launcher` e `PROJECT.it.tests` per test di integrazione

1. Sostituire il contenuto del `PROJECT.ui.apps` con `apps` e `etc` cartelle del pacchetto:

   1. Nel pannello Esplora progetti, apri `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Fai clic con il pulsante destro del mouse sul pulsante `apps` e scegli **Mostra in** > **Esplora sistema**.
   1. Elimina `apps` e `etc` cartelle da visualizzare e posizionare qui le `apps` e `etc` cartelle del pacchetto di contenuti.
   1. In Eclipse, fai clic con il pulsante destro del mouse sul `PROJECT.ui.apps` progetto e scegli **Aggiorna**.

1. Quindi fai lo stesso per il `PROJECT.ui.content` e sostituisci la relativa cartella di contenuto con quella del pacchetto:

   1. Nel pannello Esplora progetti, apri `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Fai clic con il pulsante destro del mouse sulla cartella del contenuto più profondo e scegli **Mostra in** -> **Esplora sistema**.
   1. Elimina la cartella di contenuto da visualizzare e inserisci qui la cartella di contenuto del pacchetto di contenuto.
   1. In Eclipse, fai clic con il pulsante destro del mouse sul `PROJECT.ui.content` progetto e scegli **Aggiorna**.

1. Ora è necessario aggiornare il `filter.xml` i file di questi due progetti devono corrispondere al contenuto del pacchetto di contenuti. Per questo, apri la `META-INF/vault/filter.xml` file del pacchetto di contenuti in un editor di testo/codice separato.

   * Questo è un esempio di come `filter.xml` file può cercare:

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

1. Per quanto riguarda il contenuto del pacchetto diviso in due progetti, dovrai anche dividere queste regole di filtro in due e aggiornare di conseguenza il `filter.xml` i file dei due progetti.

   1. In Eclipse, apri `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Sostituire il contenuto della `<workspaceFilter>` con le regole del pacchetto che iniziano con `/apps` e `/etc`
      * Esempio:

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
      * Esempio:

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. Assicurati di salvare tutte le modifiche. Ora puoi sincronizzare il nuovo contenuto con l’istanza AEM.

1. Nel pannello Server , assicurati che la connessione sia avviata e, in caso contrario, avviala.
1. Fai clic sul pulsante **Pulisci e pubblica** icona.

Al termine, il pacchetto dovrebbe essere in esecuzione sull&#39;istanza e al momento del salvataggio, qualsiasi modifica viene automaticamente sincronizzata con l&#39;istanza.

Per ricreare un pacchetto dal progetto, fai clic con il pulsante destro del mouse sul `PROJECT.ui.apps` o `PROJECT.ui.content` e scegli **Esegui come** -> **Installazione Maven**.

Ora disponi di una cartella di destinazione creata con il pacchetto all’interno di (ad esempio `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Risoluzione dei problemi {#troubleshooting}

### Risoluzione della definizione del progetto non valida {#resolving-invalid-project-definition}

Per risolvere le dipendenze non valide e la definizione del progetto procedere come segue:

1. Seleziona tutti i progetti creati.
1. Fai clic con il pulsante destro del mouse.
1. Nel menu di scelta rapida, seleziona **Maven** -> **Aggiorna progetti**.
1. Controlla **Forza aggiornamenti di snapshot/release**.
1. Fai clic su **OK**.

Eclipse scarica le dipendenze richieste. Questo può richiedere un momento.

## Ulteriori informazioni {#more-information}

Il sito web ufficiale Apache Sling IDE tooling for Eclipse fornisce informazioni utili:

* La [**Strumenti Apache Sling IDE per Eclipse** Guida utente](https://sling.apache.org/documentation/development/ide-tooling.html), questa documentazione ti guida attraverso i concetti generali, le funzionalità di integrazione e distribuzione dei server supportate dagli strumenti di sviluppo AEM.
* La [Sezione Risoluzione dei problemi](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* La [Elenco dei problemi noti](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

funzionario [Eclipse](https://eclipse.org/) può essere utile per configurare l’ambiente:

* [Guida introduttiva di Eclipse](https://eclipse.org/users/)
* [Sistema di Aiuto di Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Integrazione Maven (m2eclipse)](https://www.eclipse.org/m2e/)
