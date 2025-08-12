---
title: Caricamento in blocco di entità in IMS dopo l’utilizzo di CTT
description: Panoramica dei file di caricamento in blocco per gruppi e utenti e come utilizzarli in Admin Console per creare gruppi e utenti in IMS.
exl-id: 43ebd6f1-1492-461a-8d9b-2b55dcde9052
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 3%

---

# Caricamento in blocco delle entità principali in IMS dopo aver usato CTT {#bulk-principal-uploading}

>[!CONTEXTUALHELP]
>id="bulk-principal-uploading"
>title="Caricamento in blocco delle entità principali"
>abstract="Panoramica dei file di caricamento in blocco per gruppi e utenti e come utilizzarli in Admin Console per creare gruppi e utenti in IMS."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="Documentazione di AEM Admin Console"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console"

## Introduzione {#introduction}

La migrazione dei contenuti al cloud utilizzando CTT e CAM crea gruppi nell’istanza cloud di AEM, ma non può fare nulla per inserire gruppi o utenti in IMS. Devono esistere in IMS per essere gestiti correttamente dai clienti. Fortunatamente, Admin Console fornisce funzionalità per creare gruppi IMS e utenti in blocco. L’inserimento di CAM facilita questo processo salvando i file di input per la creazione in blocco, consentendo ai clienti di completare questa azione Admin Console come parte del processo di migrazione complessivo. Vengono creati due tipi di file di caricamento in blocco: uno per i gruppi e uno per gli utenti.

Vedi anche [Gestione utenti](https://helpx.adobe.com/it/enterprise/using/users.html) per ulteriori dettagli sulla gestione degli utenti di AEM as a Cloud Service.

## Regole generali per il caricamento dei file {#rules}

Esistono alcune linee guida generali per la modifica e l’utilizzo di entrambi i tipi di file di caricamento:

* Prima di poter seguire queste istruzioni è necessario concedere l’accesso come amministratore all’Admin Console.
* Tieni presente che esistono alcuni modi diversi di creare utenti e gruppi in IMS.  Per informazioni su tutte le opzioni disponibili, consulta [Supporto IMS per Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/ims-support).  Solo i metodi di caricamento in blocco di Admin Console sono descritti qui.
* In IMS sono possibili tre tipi di identità: Adobe ID, Enterprise ID e Federated ID.  Le istruzioni in questa pagina sono fornite solo per **Adobe ID**.  Se devi utilizzare Enterprise ID o Federated ID, consulta la [documentazione Admin Console](https://helpx.adobe.com/ca/enterprise/using/admin-console.html) completa e la documentazione specifica per il [caricamento di Admin Console Bulk Group](https://helpx.adobe.com/ca/enterprise/using/user-groups.html) e il [caricamento di Admin Console Bulk User](https://helpx.adobe.com/ca/enterprise/using/bulk-upload-users.html).  Le specifiche per i file di caricamento sono leggermente diverse per questi due tipi di identità.
* Se un singolo campo CSV consente più voci (ad esempio più profili di prodotto, più gruppi o più amministratori), le voci devono essere racchiuse tra virgolette doppie e separate da una virgola, ad esempio `"profile 1,profile 2"`.

   * In questo caso è possibile utilizzare le virgolette singole anziché le virgolette doppie, ma la modifica del file in Microsoft Excel può causare problemi di analisi. Se si utilizza Excel per modificare questi file, assicurarsi di utilizzare le virgolette doppie anziché le virgolette singole.

## Caricamento gruppo in blocco {#group-upload}

### Caso d’uso: è stata effettuata la migrazione dei gruppi ad AEM as a Cloud Service, ma poiché non sono presenti in IMS/Admin Console, è necessario caricarli in IMS tramite Admin Console.

Per utilizzare la funzionalità di caricamento di gruppo in blocco di Admin Console dopo l’esecuzione di una migrazione CTT/CAM, effettua le seguenti operazioni:

1. Scarica il file del gruppo ausiliario da CAM

   1. In CAM, vai a **Trasferimento contenuti** e seleziona **Processi di acquisizione**.
   1. Fare clic sui puntini di sospensione (...) nella riga dell&#39;acquisizione in questione e scegliere **Visualizza riepilogo entità**.
   1. Nella finestra di dialogo visualizzata, selezionare **Bulk Group File** dall&#39;elenco a discesa in **Download di un file...** e fare clic sul pulsante **Download**.
   1. Salva il file CSV risultante.

1. Modifica il file del gruppo ausiliario

   * Ogni riga rappresenta un gruppo da caricare e contiene quattro campi, i cui nomi costituiscono la prima riga del file:

      * _Nome gruppo utenti_ - Il nome del gruppo è obbligatorio e può contenere un massimo di 255 caratteri.  Questo nome di gruppo deve essere lo stesso in IMS e AEM
      * _Descrizione_ - Questo campo è facoltativo e può contenere un massimo di 255 caratteri
      * _Amministratori gruppo utenti_ - In questo campo deve essere incluso almeno un amministratore gruppo. È possibile assegnare più amministratori separando ogni amministratore con una virgola e racchiudendo l’elenco tra virgolette. La voce per ogni amministratore deve includere il tipo di identità dell’utente, seguito da un trattino e quindi dall’indirizzo e-mail.  Ad esempio
        `"Adobe ID-myAdmin@example.com,Adobe ID-myOtherAdmin@example.com"`. Non includere uno spazio dopo la virgola che separa gli amministratori. Non puoi includere in Admin Console utenti (come amministratori) che al momento non fanno parte dell’organizzazione
      * _Profili di prodotto assegnati_ - Questo campo è facoltativo. Puoi assegnare più profili di prodotto separando ciascun profilo con una virgola e racchiudendo l’elenco tra virgolette. Tuttavia, i profili di prodotto che includi devono già essere impostati per l’organizzazione. Assicurati di specificare il nome del profilo di prodotto e non il nome del prodotto.  L’appartenenza ai profili di prodotto assegnati a un gruppo viene ereditata da tutti gli utenti inseriti in tale gruppo.  Per trovare un profilo di prodotto:

         1. Passa ad Admin Console
         1. Trova il tuo prodotto (ad es. Adobe Experience Manager as a Cloud Service) e fai clic su di esso
         1. Trova l’ambiente (istanza) e fai clic su di esso
         1. Elenca i profili di prodotto e fai clic su quello per il tuo ambiente AEM. Il profilo prodotto si trova nella parte superiore, ovvero &quot;_Utenti AEM - Autore - Programma 12345 - Ambiente 012345_&quot;.

   * Durante la modifica del file CSV, alcune applicazioni possono aggiungere virgolette aggiuntive al momento del salvataggio, causando errori di elaborazione. È buona prassi controllare il file CSV non elaborato in un semplice editor di testo per garantire che ogni campo abbia una sola virgoletta di apertura e una di chiusura (e non devono essere &quot;virgolette intelligenti&quot;).

1. Carica il file del gruppo ausiliario in Admin Console

   1. In Admin Console, vai a **Utenti**, quindi **Gruppi di utenti**
   1. Sul lato destro fare clic sul pulsante &quot;...&quot;. Scegli **Aggiungi gruppi utenti per CSV** dal menu e scegli il tuo file CSV da caricare. Fai clic su **Carica**
   1. Riceverai una risposta che informa che il file CSV è stato caricato (in Admin Console), ma non è ancora stato importato in IMS
   1. Passa allo stesso menu &quot;...&quot; e scegli **Risultati operazione in blocco**. Ti mostrerà un elenco di tentativi di caricamento in blocco e ti dirà (in **Stato**) se il caricamento in blocco è in elaborazione, riuscito o non è riuscito

      * Inizialmente verrà visualizzato Elaborazione, a indicare che non è ancora finito
      * Una volta completato, fai clic sul collegamento **Aggiungi gruppi di utenti** per visualizzare un semplice messaggio di stato per ogni riga.
      * Se invece non è riuscito, fare clic sull&#39;icona piccola in **File** e verranno fornite ulteriori informazioni sul motivo dell&#39;errore.  Si fa riferimento ai numeri di riga del gruppo a partire dalla riga 1.
1. Utilizza Admin Console per verificare le modifiche.

## Caricamento e modifica utenti in blocco {#bulk-user}

Admin Console include due azioni separate per caricare e modificare i dettagli dell’utente. Le istruzioni riportate di seguito consentono di aggiungere nuovi utenti a IMS. Le istruzioni per la modifica degli utenti IMS esistenti si trovano nella sezione seguente denominata [Modifica utente in blocco](#user-edit).

### Caricamento utenti in blocco {#user-upload}

#### Caso d’uso: i gruppi sono stati migrati ad AEM as a Cloud Service e caricati tramite il caricamento in blocco o altri metodi.  Gli utenti potrebbero non essere presenti in IMS/Admin Console, pertanto è necessario caricarli e collegarli ai loro gruppi in IMS tramite Admin Console.

>[!NOTE]
>
>Un utente verrà visualizzato nel file **Bulk User Upload** se si trova in un gruppo acquisito durante la stessa acquisizione da cui è stato creato il file. Può anche apparire se l’utente si trova direttamente su un ACL o un CUG di contenuto migrato, o se è membro di un gruppo integrato o di un gruppo locale che si trova su un ACL o un CUG di contenuto migrato. Per ulteriori informazioni su questi casi, consulta [Migrazione gruppi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

Per utilizzare la funzionalità di caricamento in blocco degli utenti di Admin Console, effettua le seguenti operazioni:

1. Scarica il file utente in blocco da CAM
   1. In CAM, vai a **Trasferimento contenuti** e seleziona **Processi di acquisizione**.
   1. Fare clic sui puntini di sospensione (...) nella riga dell&#39;acquisizione in questione e scegliere **Visualizza riepilogo entità**.
   1. Nella finestra di dialogo visualizzata, seleziona **File utente in blocco** dall&#39;elenco a discesa in **Scarica un file...** e fai clic sul pulsante **Scarica**.
   1. Salva il file CSV risultante
1. Modifica il file utente ausiliario
   * Ogni riga rappresenta un utente da caricare e contiene quindici campi (i nomi dei campi costituiscono la prima riga del file). Alcuni campi sono facoltativi e non sono descritti qui. Consulta [Formato CSV per utenti in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format).  I campi sono:

      * _Tipo di identità_ - Facoltativo.  Se non viene specificato, verrà creato come Adobe ID
      * _Nome utente_ - Facoltativo e non utilizzato per caricamenti Adobe ID
      * _Dominio_ - Facoltativo e non utilizzato per caricamenti Adobe ID
      * _E-mail_ - Obbligatorio.  L’indirizzo e-mail verrà utilizzato per la verifica al primo accesso dell’utente
      * _Nome_: facoltativo.  Deve essere utilizzato perché viene visualizzato in diverse posizioni con Cognome
      * _Cognome_ - Facoltativo.  Deve essere utilizzato perché viene visualizzato in più posizioni
      * _Codice paese_ - Facoltativo e non utilizzato per caricamenti Adobe ID
      * _ID_ - Facoltativo e non utilizzato per caricamenti Adobe ID
      * _Configurazioni prodotto_ - Facoltativo. Questo campo verrà ereditato anche da tutti i gruppi di cui l’utente è membro
      * _Ruoli di amministratore_ - Facoltativo. Utilizzare questo campo se l&#39;utente è un amministratore. Vedi [Formato CSV utenti in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) per i dettagli
      * _Configurazioni di prodotto amministrate_ - Facoltativo.  Per informazioni dettagliate, consulta [Formato CSV per utenti in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format). Questo campo verrà ereditato anche da tutti i gruppi di cui l’utente è membro
      * _Gruppi di utenti_ - Facoltativo. Un elenco di gruppi a cui l’utente deve essere assegnato come membro. Ogni gruppo deve essere un gruppo IMS già esistente. Quando il file utente in blocco viene scaricato da CAM, questo campo viene precompilato con i nomi del gruppo abilitato per IMS di cui l’utente era membro (direttamente o indirettamente) prima della migrazione
      * _Gruppi di utenti amministrati_ - Facoltativo.  Per informazioni dettagliate, consulta [Formato CSV per utenti in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format). Questo campo verrà ereditato anche da tutti i gruppi di cui l’utente è membro
      * _Prodotti amministrati_ - Facoltativo.  Per informazioni dettagliate, consulta [Formato CSV per utenti in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format). Questo campo verrà ereditato anche da tutti i gruppi di cui l’utente è membro
      * _Contratti amministrati_ - Facoltativo.  Vedi [Formato CSV utenti in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) per i dettagli
      * _Accesso per sviluppatori_ - Facoltativo.  Vedi [Formato CSV utenti in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) per i dettagli
      * _Prodotti assegnati automaticamente_ - Facoltativo.  Vedi [Formato CSV utenti in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) per i dettagli

   * Durante la modifica del file CSV, alcune applicazioni possono aggiungere virgolette aggiuntive al momento del salvataggio, causando errori di elaborazione. È buona prassi controllare il file CSV non elaborato in un semplice editor di testo per garantire che ogni campo abbia una sola virgoletta di apertura e una di chiusura (e non devono essere &quot;virgolette intelligenti&quot;)

1. Utilizza Admin Console per importare il file utente in blocco

   1. In Admin Console, vai a Utenti
   1. Fai clic sul pulsante **Aggiungi utenti per CSV**
   1. Trascina e rilascia o seleziona un file CSV per utenti in blocco scaricato da CAM
   1. Fai clic sul pulsante **Carica**
   1. Riceverai una risposta che informa che il file CSV è stato caricato (in Admin Console), ma non è ancora stato importato in IMS.
   1. Passa al menu &quot;...&quot; a destra e scegli **Risultati operazione in blocco**.  Verrà visualizzato un elenco di tentativi di caricamento in blocco e verrà visualizzato (in **Stato**) se il caricamento in blocco è in fase di elaborazione, è riuscito o non è riuscito.

      * Inizialmente verrà visualizzato Elaborazione, a indicare che non è ancora finito
      * Una volta completato, fai clic sul collegamento **Aggiungi utenti** per visualizzare un semplice messaggio di stato per ogni riga
      * In caso contrario, fare clic sull&#39;icona piccola in **File** per ottenere ulteriori informazioni sul motivo dell&#39;errore. Si fa riferimento ai numeri di riga utente a partire dalla riga 1.

1. Utilizza Admin Console per verificare le modifiche.

>[!NOTE]
>
>Dopo un’acquisizione non wipe, è possibile che gli utenti che sono stati precedentemente migrati e quindi creati in IMS vengano visualizzati nel file di caricamento collettivo degli utenti. Questo potrebbe essere per molte ragioni. In questo caso, il caricamento dell’utente di nuovo avrà esito negativo. Prova invece a rimuovere l’utente dal file di caricamento utente in blocco e, se l’utente deve essere aggiunto a gruppi diversi, utilizza il file di modifica utente in blocco come descritto di seguito.

### Modifica utente in blocco {#user-edit}

#### Caso d’uso: gruppi e utenti sono stati migrati ad AEM as a Cloud Service e caricati tramite il caricamento in blocco o altri metodi. Ora è necessario apportare alcune modifiche a più utenti contemporaneamente, ad esempio aggiungerli a un gruppo IMS esistente.

Per utilizzare la funzionalità di modifica in blocco degli utenti di Admin Console, effettua le seguenti operazioni:

1. Scarica il file utente in blocco da Admin Console

   1. In Admin Console, vai a Utenti
   1. Sul lato destro fare clic sul pulsante &quot;...&quot;.  Scegli **Modifica dettagli utente per CSV** dal menu
   1. Fai clic su **Scarica modello CSV** e scegli **Utenti correnti**.  Un file CSV dovrebbe apparire nella cartella Download locale.

1. Modifica il file utente ausiliario

   1. In Admin Console, vai a Utenti
   1. Modifica il file CSV utilizzando un editor di testo (scelta consigliata) o un’applicazione per fogli di calcolo come Excel. L’utilizzo di un’applicazione può apportare modifiche imprevedibili ai dati, pertanto si consiglia di utilizzare un editor di testo per verificare la formattazione del file dopo tutte le modifiche
   1. Le descrizioni dei campi in questo file sono le stesse di cui sopra, in Caricamento utente in blocco
   1. Rimuovi tutti gli utenti che non vengono modificati
   1. Se si modifica il campo Gruppi utente, lasciare i gruppi correnti e aggiungerne di nuovi, in base alle esigenze. Se rimuovi un gruppo esistente, l’utente verrà rimosso da tale gruppo in IMS
   1. Durante la modifica del file CSV, alcune applicazioni possono aggiungere virgolette aggiuntive al momento del salvataggio, causando errori di elaborazione. È buona prassi esaminare il file CSV non elaborato in un semplice editor di testo per garantire che ogni campo abbia una sola virgoletta di apertura e una di chiusura (e non devono essere &quot;virgolette intelligenti&quot;)

1. Caricare il file utente in blocco in Admin Console

   1. In Admin Console, vai a Utenti
   1. Sul lato destro fare clic sul pulsante &quot;...&quot;. Scegli **Modifica dettagli utente per CSV** dal menu
   1. Trascina e rilascia o seleziona il file CSV dell’utente in blocco modificato
   1. Fai clic sul pulsante Carica
   1. Riceverai una risposta che informa che il file CSV è stato caricato (in Admin Console), ma non è ancora stato importato in IMS
   1. Passa al menu &quot;...&quot; a destra e scegli **Risultati operazione in blocco**. Ti mostrerà un elenco di tentativi di caricamento in blocco e ti dirà (sotto Stato) se il caricamento in blocco è in elaborazione, riuscito o non è riuscito.

      * Inizialmente verrà visualizzato Elaborazione, a indicare che non è ancora finito
      * Una volta completato, fai clic sul collegamento **Modifica dettagli utente** per visualizzare un semplice messaggio di stato per ogni riga
      * In caso contrario, fare clic sull&#39;icona piccola in **File** per visualizzare ulteriori informazioni sul motivo dell&#39;errore. Si fa riferimento ai numeri di riga utente a partire dalla riga 1.

1. Utilizza Admin Console per verificare le modifiche.
