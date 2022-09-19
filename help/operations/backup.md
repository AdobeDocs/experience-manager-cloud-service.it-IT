---
title: Ripristino del contenuto in AEM as a Cloud Service
description: Scopri come ripristinare il contenuto di AEM as a Cloud Service dal backup utilizzando Cloud Manager.
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: e816bd55b8b5febb19566f3d6009e6f5e823b22e
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 95%

---


# Ripristino del contenuto in AEM as a Cloud Service {#content-restore}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Backup e ripristino"
>abstract="Scopri come ripristinare il contenuto di AEM as a Cloud Service dal backup utilizzando Cloud Manager."

Scopri come ripristinare il contenuto di AEM as a Cloud Service dal backup utilizzando Cloud Manager.

>[!NOTE]
>
>* Questa funzione viene implementata in modo graduale e potrebbe non essere ancora abilitata in tutti gli tenant in Cloud Manager.
>* Questa funzione è attualmente limitata agli ambienti di staging e sviluppo. L&#39;utilizzo delle funzioni e il feedback provenienti da questi tipi di ambiente garantiranno il successo dell&#39;implementazione negli ambienti di produzione nel prossimo futuro.


## Panoramica {#overview}

Il processo di ripristino self-service di Cloud Manager copia i dati dai backup del sistema Adobe e li ripristina nell’ambiente originale. Il ripristino viene eseguito per riportare alle condizioni originali i dati persi, danneggiati o accidentalmente eliminati.

Il processo di ripristino influisce solo sul contenuto, lasciando invariati il codice e la versione di AEM. È possibile avviare un’operazione di ripristino dei singoli ambienti in qualsiasi momento.

Cloud Manager fornisce due tipi di backup dai quali è possibile ripristinare il contenuto.

* **Punto nel tempo (PIT):** questo tipo ripristina i backup continui del sistema delle ultime 24 ore dall’ora corrente.
* **Ultima settimana:** questo tipo ripristina i backup del sistema degli ultimi sette giorni, escludendo le 24 ore precedenti.

In entrambi i casi, la versione del codice personalizzato e la versione di AEM rimangono invariate.

Le metriche delle prestazioni per il ripristino dei contenuti in AEM as a ContentService fanno riferimento ai benchmark standardizzati:

* **Obiettivo del tempo di ripristino (RTO):** l’obiettivo del tempo di ripristino varia a seconda delle dimensioni dell’archivio, ma in linea di massima, una volta iniziata la sequenza di ripristino, dovrebbe richiedere circa 30 minuti.
* **Obiettivo del punto di ripristino (RPO):** l’obiettivo del punto di ripristino è un massimo di 24 ore

>[!TIP]
>
>È inoltre possibile ripristinare i backup [utilizzando l’API pubblica.](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)

## Limitazioni  {#limitations}

L’utilizzo del meccanismo di ripristino self-service è soggetto alle seguenti limitazioni.

* Le operazioni di ripristino sono limitate a sette giorni, pertanto non è possibile ripristinare uno snapshot creato più di sette giorni prima.
* È consentito un massimo di dieci ripristini riusciti in tutti gli ambienti in un programma per ogni mese di calendario.
* Dopo la creazione dell’ambiente, sono necessarie sei ore prima che venga creato il primo snapshot di backup. Fino alla creazione dello snapshot, non è possibile eseguire alcun ripristino sull’ambiente.
* Un’operazione di ripristino non viene avviata se per l’ambiente è in esecuzione una pipeline di configurazione full stack o a livello web.
* Non è possibile avviare un ripristino se è già in esecuzione un altro ripristino nello stesso ambiente.
* In rari casi, a causa del limite di 24 ore/sette giorni sui backup, il backup selezionato potrebbe non essere disponibile a causa di un ritardo tra la selezione e l’avvio del ripristino.
* I dati provenienti da ambienti eliminati vengono persi in modo permanente e non possono essere recuperati.

## Ripristino del contenuto {#restoring-content}

Determina innanzitutto l’intervallo di tempo del contenuto da ripristinare. Quindi, per ripristinare il contenuto dell’ambiente da un backup, esegui questi passaggi.

>[!NOTE]
>
>Per avviare un’operazione di ripristino, è necessario che un utente con ruolo **Proprietario business** o **Responsabile della distribuzione** abbia effettuato l’accesso.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fai clic sul programma per il quale desideri avviare il ripristino.

1. Nella pagina **Panoramica programma** e nella scheda **Ambienti**, fai clic sul pulsante con i tre puntini accanto all’ambiente per il quale vuoi avviare il ripristino e seleziona **Ripristina contenuto**.

   ![Opzione Ripristina](assets/backup-option.png)

   * In alternativa, puoi passare direttamente alla scheda **Ripristina contenuto** dalla pagina dei dettagli di un ambiente specifico.

1. Nella scheda **Ripristina contenuto** della pagina dei dettagli dell’ambiente, seleziona innanzitutto l’intervallo di tempo del ripristino nel menu a discesa **Tempo di ripristino**.

   1. Se selezioni **Ultime 24 ore** il campo vicino, **Orario**, consente di specificare l’ora esatta entro le ultime 24 ore da ripristinare.

      ![Ultime 24 ore](assets/backup-time.png)

   1. Se selezioni **Ultima settimana** il campo vicino, **Giorno**, consente di selezionare una data negli ultimi sette giorni, escluse le 24 ore precedenti.

      ![Ultima settimana](assets/backup-date.png)

1. Dopo aver selezionato una data o specificato un’ora, la sezione successiva **Backup disponibili** mostra un elenco dei backup che è possibile ripristinare.

   ![Backup disponibili](assets/backup-available.png)

1. Quando [scegli il backup](#choosing-the-right-backup) da ripristinare, utilizza l’icona delle informazioni per visualizzare informazioni relative alla versione del codice e di AEM incluse nel backup e valuta le implicazioni del ripristino.

   ![Informazioni sul backup](assets/backup-info.png)

   * Tieni presente che la marca temporale visualizzata per le opzioni di ripristino si basa sul fuso orario del computer dell’utente.

1. Per avviare il processo di ripristino, fai clic sull’icona **Ripristina** a destra della riga del backup da ripristinare.

1. Rivedi i dettagli nella finestra di dialogo **Ripristina contenuto**, quindi conferma la richiesta facendo clic su **Ripristina**.

   ![Conferma ripristino](assets/backup-restore.png)

Il processo di backup viene avviato e puoi visualizzarne lo stato nella tabella **[Attività di ripristino](#restore-activity)**. Il tempo necessario per il completamento di un’operazione di ripristino dipende dalle dimensioni e dal profilo del contenuto da ripristinare.

Dopo il corretto ripristino:

* l’ambiente esegue le stesse versioni del codice e di AEM presenti al momento dell’avvio dell’operazione di ripristino;
* l’ambiente ha lo stesso contenuto che era disponibile al momento dello snapshot scelto, con gli indici generati di nuovo in base al codice corrente.

## Scelta del backup corretto {#choosing-backup}

I ripristini provvedono unicamente a ripristinare il contenuto in AEM. Per questo motivo, è necessario considerare attentamente le modifiche del codice apportate tra il punto di ripristino desiderato e l’ora corrente, verificando la cronologia impegno tra l’ID impegno corrente e quello sul quale viene effettuato il ripristino.

Sono possibili diversi scenari.

* Il codice personalizzato di ambiente e ripristino si trovano nello stesso archivio e nello stesso ramo.
* Il codice personalizzato di ambiente e ripristino si trovano nello stesso archivio, ma in un ramo diverso con un impegno comune.
* Il codice personalizzato di ambiente e ripristino si trovano in archivi diversi.
   * In questo caso, non verrà visualizzato un ID impegno.
   * È fortemente consigliato di clonare entrambi gli archivi e utilizzare uno strumento di differenze per confrontare i rami.

Inoltre, è da tenere presente che un ripristino potrebbe causare la mancata sincronizzazione degli ambienti di produzione e pre-produzione. Le conseguenze del ripristino dei contenuti sono di tua responsabilità.

## Attività di ripristino {#restore-activity}

La tabella **Attività di ripristino** mostra lo stato delle dieci richieste di ripristino più recenti, comprese le operazioni di ripristino attive.

![Attività di ripristino](assets/backup-activity.png)

Facendo clic sull’icona delle informazioni di uno dei backup, puoi scaricarne i relativi registri e analizzare i dettagli del codice, comprese le differenze tra l’istantanea e i dati al momento dell’avvio del ripristino.

## Backup fuori sede {#offsite-backup}

I backup regolari coprono il rischio di eliminazioni accidentali o di errori tecnici in AEM Cloud Services, ma possono verificarsi rischi aggiuntivi in caso di errore di un’area. Oltre alla disponibilità, il rischio maggiore nel caso di interruzioni di area è la perdita di dati.

AEM as a Cloud Service riduce questo rischio per tutti gli ambienti di produzione AEM copiando in modo continuo tutti i contenuti AEM in un’area remota, rendendoli disponibili per il ripristino per un periodo di tre mesi. Questa funzionalità viene definita backup fuori sede.

Il ripristino di AEM Cloud Services per gli ambienti di pre-produzione e produzione dal backup fuori sede viene eseguito da AEM Service Reliability Engineering in caso di interruzioni dati di un’area.
