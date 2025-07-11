---
title: Ripristinare il contenuto in AEM as a Cloud Service
description: Scopri come ripristinare il contenuto di AEM as a Cloud Service dal backup utilizzando Cloud Manager.
exl-id: 921d0c5d-5c29-4614-ad4b-187b96518d1f
feature: Operations
role: Admin
source-git-commit: 3aff6beda8bcafc884c46ffdc55c530d581543e4
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 23%

---


# Ripristinare il contenuto in AEM as a Cloud Service {#content-restore}

Puoi ripristinare il contenuto di AEM as a Cloud Service dal backup utilizzando Cloud Manager.

## Panoramica {#overview}

Il processo di ripristino self-service di Cloud Manager copia i dati dai backup del sistema Adobe e li ripristina nell’ambiente originale. Viene eseguito un ripristino per riportare alle condizioni originali i dati persi, danneggiati o accidentalmente eliminati.

Il processo di ripristino influisce solo sul contenuto, lasciando invariati il codice e la versione di AEM. Puoi avviare un’operazione di ripristino di singoli ambienti in qualsiasi momento. Se devi ripristinare il codice sorgente distribuito in precedenza in modo semplice e veloce, senza dover avviare una nuova esecuzione della pipeline, puoi utilizzare [Ripristina il codice precedente distribuito](/help/operations/restore-previous-code-deployed.md).

Cloud Manager fornisce due tipi di backup dai quali è possibile ripristinare il contenuto.

* **Punto nel tempo (PIT):** Questa opzione ripristina i backup continui acquisiti nelle ultime 24 ore.
* **Ultima settimana:** questo tipo ripristina i backup del sistema degli ultimi sette giorni, escludendo le 24 ore precedenti.

In entrambi i casi, la versione del codice personalizzato e la versione di AEM rimangono invariate.

>[!TIP]
>
>È inoltre possibile ripristinare i backup [utilizzando l&#39;API pubblica](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/).

>[!WARNING]
>
>* Questa funzione deve essere utilizzata solo in caso di problemi gravi relativi al codice o al contenuto.
>* Il ripristino di un backup comporta l&#39;eliminazione di tutti i dati aggiunti dopo tale backup. Anche la gestione temporanea torna alla versione precedente.
>* Prima di avviare un ripristino del contenuto, prendere in considerazione altre opzioni di ripristino selettivo.

## Opzioni di ripristino selettivo dei contenuti {#selective-options}

Prima di eseguire il ripristino completo del contenuto, prendere in considerazione queste opzioni per ripristinare più facilmente il contenuto.

* Se è disponibile un pacchetto per il percorso eliminato, installarlo nuovamente utilizzando [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md).
* Se il percorso eliminato era una pagina in Sites, utilizzare la funzione [Ripristina struttura](/help/sites-cloud/authoring/sites-console/page-versions.md).
* Se il percorso eliminato era una cartella di risorse e i file originali sono disponibili, ricaricali tramite [la console Assets](/help/assets/add-assets.md).
* Se il contenuto eliminato era costituito da risorse, provare a [ripristinare le versioni precedenti delle risorse](/help/assets/manage-digital-assets.md).

Se nessuna delle opzioni di cui sopra funziona e il contenuto del percorso eliminato è significativo, eseguire un ripristino del contenuto come descritto nelle sezioni seguenti.

## Crea ruolo utente {#user-role}

Per impostazione predefinita, nessun utente dispone dell’autorizzazione per eseguire ripristini del contenuto in ambienti di sviluppo, produzione o staging. Per delegare questa autorizzazione a utenti o gruppi specifici, attenersi alla procedura generale descritta di seguito.

1. Crea un profilo di prodotto con un nome espressivo che faccia riferimento al ripristino del contenuto.
1. Fornisci l&#39;autorizzazione **Accesso al programma** per il programma richiesto.
1. Fornisci l&#39;autorizzazione **Creazione ripristino ambiente** per l&#39;ambiente richiesto o per tutti gli ambienti del programma, a seconda del caso d&#39;uso.
1. Assegna gli utenti a quel profilo.

Per informazioni dettagliate sulla gestione delle autorizzazioni, vedere [Autorizzazioni personalizzate](/help/implementing/cloud-manager/custom-permissions.md).

## Ripristinare il contenuto di un ambiente {#restoring-content}

>[!NOTE]
>
>Un utente deve disporre di [autorizzazioni appropriate](#user-role) per avviare un&#39;operazione di ripristino.

**Per ripristinare il contenuto di un ambiente:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma per il quale si desidera avviare il ripristino.

1. Elencare tutti gli ambienti per il programma eseguendo una delle operazioni seguenti:

   * Dal menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Dati](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambienti**.

     ![Scheda Ambienti](assets/environments-1.png)

   * Dal menu a sinistra, nella sezione **Programma**, fai clic su **Panoramica**, quindi dalla scheda **Ambienti** fai clic sull&#39;icona ![Flusso di lavoro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Mostra tutto**.

     ![Opzione Mostra tutto](assets/environments-2.png)

     >[!NOTE]
     >
     >Nella scheda **Ambienti** sono elencati solo tre ambienti. Fai clic su **Mostra tutto** nella scheda per visualizzare *tutti* gli ambienti del programma.

1. Nella tabella Ambienti, a destra di un ambiente di cui desideri ripristinare il contenuto, fai clic sull&#39;icona ![Altro o sull&#39;icona del menu con i puntini di sospensione](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg), quindi fai clic su **Ripristina contenuto**.

   ![Ripristina contenuto dal menu con i puntini di sospensione](/help/operations/assets/environments-ellipsis-menu.png)

1. Nella scheda **Ripristina contenuto** della pagina dell&#39;ambiente, nell&#39;elenco a discesa **Tempo di ripristino**, selezionare l&#39;intervallo di tempo del ripristino.

   ![Scheda Ripristina contenuto di un ambiente](/help/operations/assets/environments-content-restore-tab.png)

   * Se hai scelto **Ultime 24 ore**, nel campo **Ora** adiacente, specifica l&#39;ora esatta entro le ultime 24 ore da ripristinare.
   * Se hai scelto **Ultima settimana**, nel campo **Giorno** adiacente, seleziona una data negli ultimi sette giorni, escluse le 24 ore precedenti.

1. Dopo aver selezionato una data o specificato un’ora, la sezione successiva **Backup disponibili** mostra un elenco dei backup che è possibile ripristinare.

1. Fai clic sull&#39;icona ![Informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) accanto a un backup per visualizzarne la versione del codice e di AEM, quindi valuta l&#39;impatto del ripristino prima di selezionare un backup (consulta [Scegli il backup corretto](#choosing-backup)).

   ![Informazioni sul backup](assets/backup-info.png)

   Il timestamp visualizzato per le opzioni di ripristino si basa sul fuso orario del computer dell&#39;utente.

1. All&#39;estremità destra della riga che rappresenta il backup da ripristinare, fare clic su ![Ruota in grassetto in senso antiorario o su ripristina](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RotateCCWBold_18_N.svg) per avviare il processo di ripristino.

1. Rivedi i dettagli nella finestra di dialogo **Ripristina contenuto**, quindi fai clic su **Ripristina**.

   ![Conferma ripristino](assets/backup-restore.png)

Il processo di backup viene avviato. Puoi visualizzarne lo stato nell&#39;elenco **[Attività di ripristino](#restore-activity)**. Il tempo necessario per il completamento di un’operazione di ripristino dipende dalle dimensioni e dal profilo del contenuto da ripristinare.

Al termine del ripristino, l’ambiente esegue le seguenti operazioni:

* Esegue lo stesso codice e la stessa versione di AEM utilizzati al momento dell’avvio dell’operazione di ripristino.
* Ha lo stesso contenuto che era disponibile al momento dello snapshot scelto, con gli indici generati di nuovo in modo che corrispondano al codice corrente.

## Scegliere il backup corretto {#choosing-backup}

Il processo di ripristino self-service di Cloud Manager ripristina solo i contenuti in AEM. Per questo motivo, è necessario considerare attentamente le modifiche apportate al codice tra il punto di ripristino desiderato e l’ora corrente. Rivedi la cronologia del commit tra l’ID del commit corrente e quello in fase di ripristino.

Sono possibili diversi scenari.

* Il codice personalizzato dell’ambiente e il ripristino si trovano nello stesso archivio e nello stesso ramo.
* Il codice personalizzato dell’ambiente e il ripristino condividono un archivio, utilizzano un ramo separato e hanno origine da un commit comune.
* Il codice personalizzato dell’ambiente e il ripristino si trovano in archivi diversi.
   * In questo caso, non viene visualizzato un ID commit.
   * Adobe consiglia vivamente di clonare entrambi gli archivi e utilizzare uno strumento di differenze per confrontare i rami.

Inoltre, ricorda che un ripristino potrebbe causare la mancata sincronizzazione degli ambienti di produzione e di staging. Le conseguenze del ripristino dei contenuti sono di tua responsabilità.

## Attività di ripristino {#restore-activity}

L&#39;elenco **Attività di ripristino** mostra lo stato delle dieci richieste di ripristino più recenti, incluse le operazioni di ripristino attive.

![Attività di ripristino](assets/backup-activity.png)

Facendo clic sull&#39;![icona Informazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) per un backup, è possibile scaricare i registri per tale backup e analizzare i dettagli del codice, incluse le differenze tra l&#39;istantanea e i dati al momento dell&#39;avvio del ripristino.

## Backup fuori sede {#offsite-backup}

I backup regolari coprono il rischio di eliminazioni accidentali o di errori tecnici in AEM Cloud Services, ma possono verificarsi rischi aggiuntivi in caso di errore di un’area. Oltre alla disponibilità, il rischio maggiore nel caso di interruzioni di area è la perdita di dati.

AEM as a Cloud Service riduce questo rischio per tutti gli ambienti di produzione AEM. In altre parole, copia continuamente tutto il contenuto di AEM in un’area remota. Questo processo rende i contenuti disponibili per il recupero per tre mesi. Questa funzionalità è nota come backup fuori sede.

AEM Service Reliability Engineering ripristina gli ambienti di staging e produzione di AEM Cloud Service dai backup esterni al sito durante interruzioni dell’attività nell’area dati.

## Limitazioni  {#limitations}

L’utilizzo del meccanismo di ripristino self-service è soggetto alle seguenti limitazioni.

* Le operazioni di ripristino sono limitate a sette giorni, pertanto non è possibile ripristinare uno snapshot creato più di sette giorni prima.
* È consentito un massimo di dieci ripristini riusciti in tutti gli ambienti in un programma per ogni mese di calendario.
* Dopo la creazione dell’ambiente, sono necessarie sei ore prima che venga creato il primo snapshot di backup. Fino alla creazione dello snapshot, non è possibile eseguire alcun ripristino sull’ambiente.
* Un’operazione di ripristino non viene avviata se per l’ambiente è in esecuzione una pipeline di configurazione full stack o a livello web.
* Non è possibile avviare un ripristino se un altro ripristino è già in esecuzione nello stesso ambiente.
* In rari casi, a causa del limite di 24 ore/sette giorni sui backup, il backup selezionato potrebbe non essere disponibile a causa di un ritardo tra la selezione e l’avvio del ripristino.
* I dati provenienti da ambienti eliminati vengono persi in modo permanente e non possono essere recuperati.
