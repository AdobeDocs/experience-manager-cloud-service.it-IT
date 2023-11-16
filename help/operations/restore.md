---
title: Ripristino del contenuto in AEM as a Cloud Service
description: Scopri come ripristinare il contenuto di AEM as a Cloud Service dal backup utilizzando Cloud Manager.
exl-id: 921d0c5d-5c29-4614-ad4b-187b96518d1f
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 71%

---


# Ripristino del contenuto in AEM as a Cloud Service {#content-restore}

Scopri come ripristinare il contenuto di AEM as a Cloud Service dal backup utilizzando Cloud Manager.

>[!NOTE]
>
>Questa funzione è disponibile solo per [il programma early adopter](/help/implementing/cloud-manager/release-notes/current.md#early-adoption) e presenta alcune limitazioni oltre a quelle documentate nell’articolo. Nella prima fase di adozione:
>
>* La funzione è disponibile solo negli ambienti di sviluppo.
>* Il ripristino dei contenuti è limitato a due al mese per programma.
>
>Per informazioni dettagliate sul sistema di backup e ripristino esistente per AEM as a Cloud Service, consultare il documento [Backup e ripristino in AEM as a Cloud Service](/help/operations/backup.md)

## Panoramica {#overview}

Il processo di ripristino self-service di Cloud Manager copia i dati dai backup del sistema Adobe e li ripristina nell’ambiente originale. Viene eseguito un ripristino per riportare alle condizioni originali i dati persi, danneggiati o accidentalmente eliminati.

Il processo di ripristino influisce solo sul contenuto, lasciando invariati il codice e la versione di AEM. È possibile avviare un’operazione di ripristino dei singoli ambienti in qualsiasi momento.

Cloud Manager fornisce due tipi di backup dai quali è possibile ripristinare il contenuto.

* **Punto nel tempo (PIT)** Questo tipo ripristina i backup continui del sistema delle ultime 24 ore dall’ora corrente.
* **Ultima settimana:** questo tipo ripristina i backup del sistema degli ultimi sette giorni, escludendo le 24 ore precedenti.

In entrambi i casi, la versione del codice personalizzato e la versione dell’AEM rimangono invariate.

>[!TIP]
>
>È inoltre possibile ripristinare i backup [utilizzando l’API pubblica.](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/)

## Ripristino del contenuto {#restoring-content}

Determina innanzitutto l’intervallo di tempo del contenuto da ripristinare. Quindi, per ripristinare il contenuto dell’ambiente da un backup, esegui questi passaggi.

>[!NOTE]
>
>Un utente con **Proprietario business** o **Responsabile dell’implementazione** per avviare un&#39;operazione di ripristino, è necessario che il ruolo sia connesso.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma per il quale si desidera avviare il ripristino.

1. Dalla sezione **Panoramica del programma** pagina, nella **Ambienti** , fai clic sul pulsante con i puntini di sospensione accanto all’ambiente per il quale desideri avviare il ripristino e seleziona **Ripristina contenuto**.

   ![Opzione Ripristina](assets/backup-option.png)

   * In alternativa, puoi passare direttamente alla scheda **Ripristina contenuto** dalla pagina dei dettagli di un ambiente specifico.

1. Nella scheda **Ripristina contenuto** della pagina dei dettagli dell’ambiente, seleziona innanzitutto l’arco temporale del ripristino nel menu a discesa **Tempo di ripristino**.

   1. Se si seleziona **Ultime 24 ore** il vicino **Ora** Questo campo consente di specificare l’ora esatta entro le ultime 24 ore da ripristinare.

      ![Ultime 24 ore](assets/backup-time.png)

   1. Se si seleziona **Ultima settimana** il vicino **Giorno** consente di selezionare una data negli ultimi sette giorni, escluse le 24 ore precedenti.

      ![Ultima settimana](assets/backup-date.png)

1. Dopo aver selezionato una data o specificato un’ora, la sezione successiva **Backup disponibili** mostra un elenco dei backup che è possibile ripristinare.

   ![Backup disponibili](assets/backup-available.png)

1. Quando [scegli il backup](#choosing-the-right-backup) da ripristinare, utilizza l’icona delle informazioni per visualizzare informazioni relative alla versione del codice e di AEM incluse nel backup e valuta le implicazioni del ripristino.

   ![Informazioni sul backup](assets/backup-info.png)

   * Tieni presente che la marca temporale visualizzata per le opzioni di ripristino si basa sul fuso orario del computer dell’utente.

1. Per avviare il processo di ripristino, fai clic sull’icona **Ripristina** a destra della riga del backup da ripristinare.

1. Rivedi i dettagli nella finestra di dialogo **Ripristina contenuto**, quindi conferma la richiesta facendo clic su **Ripristina**.

   ![Conferma ripristino](assets/backup-restore.png)

Il processo di backup viene avviato e puoi visualizzarne lo stato in **[Attività di ripristino](#restore-activity)** elenco. Il tempo necessario per il completamento di un’operazione di ripristino dipende dalle dimensioni e dal profilo del contenuto da ripristinare.

Dopo il corretto ripristino:

* l’ambiente esegue le stesse versioni del codice e di AEM presenti al momento dell’avvio dell’operazione di ripristino;
* l’ambiente ha lo stesso contenuto che era disponibile al momento dello snapshot scelto, con gli indici generati di nuovo in base al codice corrente.

## Scelta del backup corretto {#choosing-backup}

Il processo di ripristino self-service di Cloud Manager ripristina solo i contenuti a AEM. Per questo motivo, è necessario considerare attentamente le modifiche apportate al codice tra il punto di ripristino desiderato e l’ora corrente, esaminando la cronologia del commit tra l’ID commit corrente e quello in fase di ripristino.

Sono possibili diversi scenari.

* Il codice personalizzato di ambiente e ripristino si trovano nello stesso archivio e nello stesso ramo.
* Il codice personalizzato di ambiente e ripristino si trovano nello stesso archivio, ma in un ramo diverso con un impegno comune.
* Il codice personalizzato di ambiente e ripristino si trovano in archivi diversi.
   * In questo caso, non verrà visualizzato un ID impegno.
   * È fortemente consigliato di clonare entrambi gli archivi e utilizzare uno strumento di differenze per confrontare i rami.

Inoltre, è da tenere presente che un ripristino potrebbe causare la mancata sincronizzazione degli ambienti di produzione e pre-produzione. Le conseguenze del ripristino dei contenuti sono di tua responsabilità.

## Attività di ripristino {#restore-activity}

Il **Attività di ripristino** L’elenco mostra lo stato delle dieci richieste di ripristino più recenti, comprese le operazioni di ripristino attive.

![Attività di ripristino](assets/backup-activity.png)

Facendo clic sull’icona delle informazioni di uno dei backup, puoi scaricarne i relativi registri e analizzare i dettagli del codice, comprese le differenze tra l’istantanea e i dati al momento dell’avvio del ripristino.

## Backup fuori sede {#offsite-backup}

I backup regolari coprono il rischio di eliminazioni accidentali o di errori tecnici in AEM Cloud Services, ma possono verificarsi rischi aggiuntivi in caso di errore di un’area. Oltre alla disponibilità, il rischio maggiore nel caso di interruzioni di area è la perdita di dati.

AEM as a Cloud Service riduce questo rischio per tutti gli ambienti di produzione AEM copiando in modo continuo tutti i contenuti AEM in un’area remota, rendendoli disponibili per il ripristino per un periodo di tre mesi. Questa funzionalità viene definita backup fuori sede.

Il ripristino di AEM Cloud Services per gli ambienti di pre-produzione e produzione dal backup fuori sede viene eseguito da AEM Service Reliability Engineering in caso di interruzioni dati di un’area.

## Limitazioni  {#limitations}

L’utilizzo del meccanismo di ripristino self-service è soggetto alle seguenti limitazioni.

* Le operazioni di ripristino sono limitate a sette giorni, pertanto non è possibile ripristinare uno snapshot creato più di sette giorni prima.
* È consentito un massimo di dieci ripristini riusciti in tutti gli ambienti in un programma per ogni mese di calendario.
* Dopo la creazione dell’ambiente, sono necessarie sei ore prima che venga creato il primo snapshot di backup. Fino alla creazione dello snapshot, non è possibile eseguire alcun ripristino sull’ambiente.
* Un’operazione di ripristino non viene avviata se per l’ambiente è in esecuzione una pipeline di configurazione full stack o a livello web.
* Non è possibile avviare un ripristino se un altro ripristino è già in esecuzione nello stesso ambiente.
* In rari casi, a causa del limite di 24 ore/sette giorni sui backup, il backup selezionato potrebbe non essere disponibile a causa di un ritardo tra la selezione e l’avvio del ripristino.
* I dati provenienti da ambienti eliminati vengono persi in modo permanente e non possono essere recuperati.
