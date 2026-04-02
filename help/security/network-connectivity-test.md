---
title: Test connettività di rete
description: Utilizza il test di connettività di rete in Cloud Manager per convalidare la configurazione di rete avanzata e VPN dal percorso di uscita del programma prima di abilitare la rete negli ambienti.
feature: Security
role: Admin
source-git-commit: b29b3a980a0bc1c619fb23c52acda79fae9bf945
workflow-type: tm+mt
source-wordcount: '2047'
ht-degree: 2%

---


# Test connettività di rete {#network-connectivity-test}

Il **test della connettività di rete** è uno strumento di diagnostica di Cloud Manager che consente di convalidare la configurazione di rete avanzata e VPN prima dell&#39;attivazione della rete avanzata negli ambienti e prima della pubblicazione. Utilizzalo per verificare che gli host e le porte che AEM deve raggiungere, inclusi gli endpoint interni o privati, siano raggiungibili attraverso lo stesso percorso di connettività utilizzato da Rete avanzata.

Il test viene eseguito dall&#39;**infrastruttura proxy in uscita** che appartiene alla configurazione di rete avanzata del programma, non da un pod Author o Publish. Utilizza lo stesso percorso di rete in uscita utilizzato da AEM quando è attiva la funzione Rete avanzata. Questa progettazione è particolarmente utile per gli scenari **VPN**: prima di andare in diretta, puoi confermare la risoluzione DNS, il routing di rete, le regole del firewall e la disponibilità del servizio per i sistemi privati o locali.

Per informazioni sul provisioning della VPN, sull&#39;IP in uscita dedicato o sull&#39;uscita da porta flessibile, vedere [Configurazione di reti avanzate per AEM as a Cloud Service](/help/security/configuring-advanced-networking.md).

>[!IMPORTANT]
>
>Un test di connettività di successo dimostra che il percorso di rete da Rete avanzata può raggiungere la destinazione. Il codice dell&#39;applicazione deve essere ancora configurato per utilizzare il proxy di rete avanzato quando necessario (ad esempio, variabili di ambiente relative al proxy e port forwarding). Se il codice ignora il proxy, è possibile che non venga visualizzato il traffico dal percorso di uscita previsto anche quando il test viene superato.

## Quando utilizzare questo strumento {#when-to-use}

* Dopo la creazione della **rete avanzata** al livello **programma** e **prima** o durante l&#39;attivazione in **ambienti**.
* Per convalidare la connettività **VPN** ai sistemi privati o locali che utilizzi (ad esempio, nomi host interni o indirizzi IP privati).
* Per limitare i problemi DNS rispetto ai problemi firewall o di routing quando un servizio non risponde come previsto.

>[!NOTE]
>
>Questo strumento è destinato ai programmi che utilizzano la rete avanzata (VPN, IP in uscita dedicato o uscita da porta flessibile). Non è un test generico della connettività standard di AEM senza rete avanzata.

## Prerequisiti {#prerequisites}

* Un programma Cloud Manager.
* Infrastruttura di rete avanzata già creata per il programma (vedere [Configurazione di reti avanzate](/help/security/configuring-advanced-networking.md)).

## Eseguire un test {#how-to-run-a-test}

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e apri la tua organizzazione e il tuo programma.
1. Apri la scheda **Ambienti** per il programma. Nella barra laterale sinistra, selezionare **Infrastruttura di rete**.

1. Nella pagina **Infrastruttura di rete**, individuare l&#39;infrastruttura nella tabella. Seleziona una riga per aprire l&#39;esperienza di test oppure apri il menu delle azioni di riga (![icona Adobe Spectrum Small More per il menu delle azioni di riga con puntini di sospensione orizzontali](assets/ellipsis.svg)) e scegli **Test**.

   ![Area Ambienti del programma Cloud Manager con la tabella Infrastruttura di rete, le righe dell&#39;infrastruttura e il menu Azioni riga utilizzati per avviare il test Connettività di rete](assets/network-connectivity-test-cloud-manager-open-test-from-infrastructure-list.png)

1. Viene visualizzata la finestra di dialogo **Test di rete**. Immetti **Host** e **Porta**, seleziona **Prova** e controlla la risoluzione DNS, l&#39;apertura della porta, la connettività HTTP e la raggiungibilità nell&#39;area dei risultati. Nella finestra di dialogo vengono visualizzate azioni facoltative come **Copia negli Appunti** e la cronologia dei test recenti. Consulta [Informazioni sui risultati](#understanding-results) per informazioni su come interpretare ogni sezione.

   ![Finestra di dialogo Test connettività di rete Cloud Manager con campi Host e Porta, azione di test e risultati per risoluzione DNS, apertura porta, connettività HTTP e raggiungibilità](assets/network-connectivity-test-cloud-manager-results-dialog.png)

### Campi di input {#input-fields}

| Campo | Descrizione | Esempi |
| --- | --- | --- |
| **Host** | Il nome host o l’indirizzo IP del servizio che AEM deve raggiungere. | `internal-api.example.com`, `10.0.1.50` |
| **Porta** | Porta TCP sull&#39;host di destinazione (1-65535). I valori comuni possono essere visualizzati in un elenco di collegamenti (ad esempio, 80, 443, 587, 22). | `443` |

### Passaggi {#test-steps}

1. Immettere **Host** e **Porta**.
1. Seleziona **Test**. I risultati vengono in genere visualizzati entro pochi secondi.
1. Facoltativo: utilizzare **Copia negli Appunti** per acquisire il risultato JSON completo (utile per i casi di supporto).
1. È possibile elencare i test recenti per le esecuzioni rapide.

## I risultati {#understanding-results}

Lo strumento riporta diverse dimensioni. Insieme descrivono se la destinazione è raggiungibile da Advanced Networking e come si sono comportati i controlli in base a HTTP.

### Risoluzione DNS {#dns-resolution}

| Risultato | Significato |
| --- | --- |
| `ips: ["10.0.1.50"]` | Risoluzione DNS completata. Il nome host è stato risolto negli indirizzi IP elencati utilizzando i resolver associati alla configurazione di rete avanzata. |
| `error: "DNS resolution error: ..."` | Risoluzione DNS non riuscita. I server DNS configurati non sono riusciti a risolvere il nome host (nome errato, risolutore non raggiungibile, record mancante e cause simili). |

>[!NOTE]
>
>Se si immette un **IP numerico** invece di un nome host, la risoluzione DNS viene ignorata per tale valore e l&#39;IP viene utilizzato direttamente.

### Porta aperta {#port-open}

| Risultato | Significato |
| --- | --- |
| `Yes` / true | Connessione TCP riuscita: la porta è aperta e accetta le connessioni. |
| `No` / false | La porta è chiusa, filtrata da un firewall o l&#39;host non è raggiungibile. |

### Connettività HTTP {#http-connectivity}

Tentativo di richiesta HTTP/HTTPS su **ogni porta**. Lo strumento tenta sempre prima **HTTPS**, quindi torna a **HTTP**. Se nessuna delle due funziona, il risultato viene mappato a un breve messaggio di **errore** leggibile (vedi la tabella seguente).

**Output di successo**

| Output | Significato |
| --- | --- |
| `protocol: "https"`, `status_code: 200`, `reason: "200 OK"` | Connessione HTTPS completata. |
| `protocol: "http"`, `status_code: 301`, `reason: "301 Moved Permanently"` | Connessione HTTP completata. Il servizio sta eseguendo il reindirizzamento (in genere a HTTPS). Questo è normale. |

**Output di errori classificati**

| Errore | Nota | Significato |
| --- | --- | --- |
| `"Not an HTTP/HTTPS service"` | `"The service appears to be a non-HTTP service (e.g., database, message queue, or custom TCP). Use the port_open and reachability fields to verify connectivity."` | La porta è aperta, ma il servizio non parla HTTP. Questo è previsto per database, SFTP, TCP personalizzato e servizi simili. |
| `"Connection refused"` | `"The port is not accepting connections. Verify the service is running and listening on this port."` | Su questa porta non è in ascolto nulla. |
| `"Connection timed out"` | `"The connection timed out. Check firewall rules and network routing."` | Un problema di firewall o di routing impedisce la connessione. |
| `"No IPs resolved for host"` | - | Risoluzione DNS non riuscita; impossibile testare HTTP. |

>[!NOTE]
>
>Qualsiasi codice di stato HTTP dal servizio di destinazione (ad esempio, `200`, `301`, `302`, `403`, `404` o `500`) è un **segnale di successo** per la connettività. Significa che il **percorso di rete** funziona. Il codice di stato riflette la risposta del servizio stesso, non l’integrità complessiva della rete. Per i servizi non HTTP, lo strumento indica **Non è un servizio HTTP/HTTPS**. Utilizzare **Porta aperta** e **Raggiungibilità** come indicatori affidabili per tali servizi.

### Raggiungibilità {#reachability}

| Risultato | Significato |
| --- | --- |
| **Raggiungibile** | L&#39;host e la porta di destinazione sono raggiungibili dall&#39;infrastruttura di rete avanzata. La configurazione di rete è corretta. |
| **Non raggiungibile: porta non accessibile** | Il DNS è stato risolto correttamente, ma il protocollo TCP sulla porta non è riuscito. Si tratta in genere di un firewall o di un problema di routing. |
| **Non raggiungibile: risoluzione DNS non riuscita** | Impossibile risolvere il nome host con la configurazione. Questo indica un problema di configurazione DNS. |

### Più risolutori DNS {#multiple-dns-resolvers}

Se l&#39;infrastruttura di rete avanzata definisce **più resolver DNS**:

* Quando **tutti i resolver restituiscono risultati identici**, viene visualizzato un **singolo risultato consolidato** con etichetta `default`.
* Quando i risolutori restituiscono **risultati diversi**, il risultato di ciascun risolutore viene visualizzato **separatamente** (con etichetta `resolver_1`, `resolver_2` e così via), **con l&#39;IP del risolutore**, in modo da individuare il server DNS che causa l&#39;incoerenza.

## Risoluzione dei problemi {#troubleshooting}

Gli scenari seguenti associano ciò che è probabile vedere nello strumento con i passaggi per limitare la causa. Per la **copia completa negli Appunti** JSON che illustra le stesse situazioni, vedi [Output di esempio](#example-outputs).

### Risoluzione DNS non riuscita {#dns-failed}

#### Output

Il nome host non è stato risolto utilizzando le impostazioni DNS di rete avanzate. Impossibile verificare la porta. Nella visualizzazione dei risultati, **Risoluzione DNS** mostra una stringa di errore e **Raggiungibilità** segnala un errore DNS:

```
DNS Resolution: error: "DNS resolution error: ..."
Reachability: "Unreachable: DNS resolution failed"
```

#### Consigli

1. **Verificare che il nome host sia corretto**. Verificare la presenza di errori di battitura e che si stia utilizzando la **zona DNS** prevista (la zona errata è un errore comune).
1. Assicurati che i **risolutori DNS**, ovvero quelli configurati nell&#39;infrastruttura di rete, siano **raggiungibili dall&#39;intervallo CIDR di rete avanzata** (lo stesso spazio di indirizzi utilizzato dallo strumento e da AEM per i controlli in uscita). Se si utilizza il DNS privato, tali server devono essere raggiungibili tramite il tunnel VPN o all&#39;interno dello spazio di indirizzi di rete che il routing espone alla rete avanzata.
1. **Verificare che i server DNS configurati siano in grado di risolvere il nome host**. Le reti avanzate utilizzano **solo** i resolver definiti nella configurazione dell&#39;infrastruttura di rete, **non** DNS pubblici (ad esempio, `8.8.8.8`). Se il DNS interno non dispone di record per tale nome host, la risoluzione non riesce.
1. **Per le impostazioni VPN:** Verificare che gli indirizzi IP del server DNS si trovino nello spazio degli indirizzi VPN (CIDR di rete remota per cui è stato creato il tunnel). I resolver su una subnet non instradata attraverso il tunnel VPN non sono raggiungibili da Rete avanzata.

### Il DNS funziona ma la porta non è accessibile {#dns-ok-port-blocked}

#### Output

Lo strumento può risolvere l&#39;host, ma TCP alla porta non riesce. Un riepilogo è spesso simile al seguente:

```
DNS Resolution: ips: ["10.0.1.50"]
Port Open: No
Reachability: "Unreachable: Port not accessible"
```

#### Consigli

1. **Rivedi le regole del firewall e dell&#39;elenco Consentiti sul servizio di destinazione**. È necessario consentire il traffico in ingresso dall&#39;intervallo CIDR dell&#39;infrastruttura di rete avanzata (e dagli indirizzi IP in uscita utilizzati da AEM). Se utilizzi una VPN, includi CIDR di rete remota come richiesto dalla progettazione.
1. **Verificare che il servizio sia in esecuzione** e **in ascolto sull&#39;host e sulla porta** immessi nel test.
1. **Per le impostazioni VPN:** Verificare che il tunnel sia attivo, che il routing raggiunga la subnet di destinazione e che l&#39;indirizzo di destinazione si trovi nello spazio degli indirizzi di rete remoto presente sulla VPN.
1. Nell&#39;infrastruttura, esaminare **i gruppi di sicurezza di rete (NSG), le regole di sicurezza o equivalenti** che potrebbero bloccare la porta tra la rete avanzata e la destinazione.
1. **Confermare il numero di porta**. Verificare che il processo sia effettivamente in ascolto sulla porta da testare.

### Il Test Mostra Che È Raggiungibile, Ma AEM Non Si Connette {#reachable-but-aem-fails}

#### Output

Il controllo della connettività ha esito positivo. Un riepilogo sintetico è spesso simile al seguente:

```
Port Open: Yes
Reachability: "Reachable"
```

Questo risultato significa che il percorso dalla rete avanzata all&#39;host e alla porta testati è aperto. Non garantisce che il traffico dell’applicazione AEM utilizzi quel percorso: quando il codice viene eseguito, i registri del servizio potrebbero ancora non mostrare richieste dall’IP in uscita previsto.

#### Consigli

1. **Il codice dell&#39;applicazione deve essere configurato per utilizzare il proxy**. Il test di connettività verifica il funzionamento del percorso di rete, ma AEM deve instradare esplicitamente le richieste tramite il **proxy di rete avanzato** (ad esempio, tramite la variabile di ambiente **`AEM_PROXY_HOST`**). Se il codice effettua connessioni dirette senza il proxy, il traffico non passa attraverso l&#39;infrastruttura di rete avanzata.
1. **Verifica le impostazioni proxy nei client HTTP**. I client HTTP devono utilizzare la stessa configurazione proxy (`AEM_PROXY_HOST` e l&#39;inoltro delle porte, se applicabile).
1. **Verificare la configurazione dell&#39;inoltro porte** per la rete avanzata al livello **ambiente**: in `portForwards` ogni voce deve mappare **`portOrig`** a **`portDest`** nell&#39;host **destinazione** destro. **`portOrig`** è la **porta a cui il codice dell&#39;applicazione AEM si connette** quando apre la connessione in uscita tramite il proxy. **`portDest`** è la **porta effettiva sul servizio di destinazione** in cui il processo remoto è in ascolto. L&#39;**host di destinazione** è il **nome host o indirizzo del servizio** utilizzato nell&#39;inoltro. Tutti e tre devono corrispondere alla modalità di scrittura dell&#39;applicazione per la connessione.
1. **Seleziona`nonProxyHosts`**. Se l&#39;host di destinazione è elencato, le richieste **ignorano il proxy** per tale host e non seguiranno il percorso di rete avanzato convalidato.

### HTTP mostra un errore ma la porta è aperta {#http-error-port-open}

#### Output

TCP riesce, ma il probe HTTP/HTTPS segnala ancora un errore. Un riepilogo è spesso simile al seguente:

```
Port Open: Yes
HTTP Connectivity: error: "Connection error: ..." or "Both HTTPS and HTTP failed. ..."
Reachability: "Reachable"
```

#### Consigli

1. **Il servizio potrebbe non parlare HTTP o HTTPS**, ad esempio TCP raw, gRPC o un altro protocollo. Il probe HTTP può avere esito negativo mentre `Port open: Yes` e `Reachability: Reachable` confermano il funzionamento del percorso di rete. Utilizza questi campi come fonte di verità per i servizi non HTTP.
1. **Verifica la configurazione di TLS e certificati**. Se HTTPS non riesce ma HTTP riesce (a volte indicato da una nota come `HTTPS failed, HTTP succeeded`), il servizio potrebbe avere problemi di certificato o offrire HTTP solo su tale porta.

### Timeout richiesta {#timeout}

#### Output

```json
{ "error": "Request timeout" }
```

#### Consigli

1. **Consenti tempo di risposta del servizio**. Il controllo utilizza un timeout di 5 secondi. I target che rispondono più lentamente di quello si interromperanno anche quando sono altrimenti sani.
1. **Account per la latenza di rete**. Sulle connessioni VPN, un&#39;elevata latenza o un tunnel non integro può spingere il percorso di andata e ritorno oltre il limite; rivedere lo stato e il routing del tunnel.
1. **Esegui di nuovo il test**. I guasti di rete una tantum possono produrre un timeout che non si ripete.

## Output di esempio {#example-outputs}

### Test HTTPS riuscito (ad esempio, API interna sulla porta 443) {#example-output-successful-https}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": true,
      "http_connectivity": {
        "protocol": "https",
        "status_code": 200,
        "reason": "200 OK"
      },
      "reachability": "Reachable"
    }
  ]
}
```

### Test del servizio non HTTP riuscito (ad esempio, database sulla porta 5432) {#example-output-successful-non-http}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": true,
      "http_connectivity": {
        "error": "Not an HTTP/HTTPS service",
        "note": "The service appears to be a non-HTTP service (e.g., database, message queue, or custom TCP). Use the port_open and reachability fields to verify connectivity."
      },
      "reachability": "Reachable"
    }
  ]
}
```

>[!NOTE]
>
>L&#39;errore HTTP è previsto per i servizi non HTTP. **Apertura porta: true** e **Raggiungibilità: raggiungibile** confermare il funzionamento del percorso di rete.

### Risoluzione DNS non riuscita {#example-output-dns-resolution-failure}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "error": "DNS resolution error: dial udp 10.0.0.2:53: i/o timeout"
      },
      "port_open": false,
      "http_connectivity": {
        "error": "DNS resolution failed"
      },
      "reachability": "Unreachable: DNS resolution failed"
    }
  ]
}
```

### Porta non accessibile (firewall / servizio inattivo) {#example-output-port-not-accessible}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": false,
      "http_connectivity": {
        "error": "Connection error: dial tcp 10.0.1.50:443: i/o timeout"
      },
      "reachability": "Unreachable: Port not accessible"
    }
  ]
}
```

## Note importanti {#important-notes}

### Quali operazioni non vengono eseguite dal test {#what-this-test-does-not-do}

* Il test non viene eseguito dall’interno di un pod di authoring o pubblicazione di AEM. Viene eseguito da **infrastruttura proxy in uscita**. In questo modo viene convalidato il livello di rete e non la configurazione proxy a livello di applicazione nel codice.
* Non convalida le impostazioni proxy dell’applicazione AEM. Anche quando il risultato è `Reachable`, il codice AEM deve essere ancora configurato per l&#39;utilizzo del proxy.
* Non convalida di per sé la configurazione dell’inoltro porta a livello di ambiente. Verifica la connettività raw dal percorso dell’infrastruttura.
* Non invia payload personalizzati. I test HTTP emettono una richiesta `GET` di base a `/`.

### Tempo di risposta {#response-time}

* **Tipico:** circa 2-3 secondi.
* **Massimo:** timeout di circa cinque secondi.
* **Tutti i risolutori DNS** e i controlli di connettività vengono eseguiti in parallelo.

### Servizi HTTP e non HTTP {#http-vs-non-http-services}

Lo strumento tenta una connessione HTTP/HTTPS su ogni porta. Per i servizi non HTTP (ad esempio, PostgreSQL sulla porta 5432, MySQL su 3306, SFTP su 22, Redis su 6379), il controllo HTTP può non riuscire con un errore di connessione, come previsto. Utilizza `Port open` e `Reachability` per confermare la connettività per questi servizi.

## Informazioni correlate {#related-information}

* [Configurazione di networking avanzato per AEM as a Cloud Service](/help/security/configuring-advanced-networking.md)
* [Tutorial di rete avanzati su Experience League](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/networking/advanced-networking)
