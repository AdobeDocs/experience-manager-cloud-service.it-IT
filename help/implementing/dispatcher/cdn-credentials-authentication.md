---
title: Configurazione delle credenziali CDN e dell’autenticazione
description: Scopri come configurare le credenziali e l’autenticazione CDN dichiarando le regole in un file di configurazione che viene quindi distribuito utilizzando la pipeline di configurazione di Cloud Manager.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 3a46db9c98fe634bf2d4cffd74b54771de748515
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 3%

---


# Configurazione delle credenziali CDN e dell’autenticazione {#cdn-credentials-authentication}

La rete CDN fornita da Adobe dispone di diverse funzioni e servizi, alcuni dei quali si basano sulle credenziali e sull’autenticazione per garantire un livello adeguato di sicurezza aziendale. Dichiarando le regole in un file di configurazione distribuito utilizzando la pipeline [config](/help/operations/config-pipeline.md) di Cloud Manager, i clienti possono configurare in modo autonomo quanto segue:

* Il valore dell’intestazione HTTP X-AEM-Edge-Key utilizzato dalla rete CDN di Adobe per convalidare le richieste provenienti da una rete CDN gestita dal cliente.
* Token API utilizzato per eliminare le risorse nella cache CDN.
* Un elenco di combinazioni nome utente/password che possono accedere a contenuto con restrizioni, inviando un modulo di autenticazione di base.

Ognuna di queste, inclusa la sintassi di configurazione, è descritta nella propria sezione di seguito.

È presente una sezione sulla modalità di [rotazione delle chiavi](#rotating-secrets), che è una buona pratica di sicurezza.

>[!NOTE]
> I segreti definiti come variabili di ambiente devono essere considerati immutabili. Invece di modificare il loro valore, devi creare un nuovo segreto con un nuovo nome e un riferimento a quel segreto nella configurazione. In caso contrario, si verificherà un aggiornamento inaffidabile dei segreti.

>[!WARNING]
>Non rimuovere le variabili di ambiente a cui si fa riferimento nella configurazione CDN. In caso contrario potrebbero verificarsi errori durante l’aggiornamento della configurazione CDN (ad esempio, l’aggiornamento di regole o di domini e certificati personalizzati).

## Valore intestazione HTTP CDN gestita dal cliente {#CDN-HTTP-value}

Come descritto nella pagina [CDN in AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN), i clienti possono scegliere di instradare il traffico attraverso la propria rete CDN, denominata anche CDN cliente (talvolta denominata BYOCDN).

Come parte della configurazione, la rete CDN di Adobe e la rete CDN del cliente devono concordare un valore dell&#39;intestazione HTTP `X-AEM-Edge-Key`. Questo valore viene impostato su ogni richiesta alla rete CDN del cliente, prima che venga instradato alla rete CDN di Adobe, che poi verifica che il valore sia come previsto, in modo che possa considerare attendibili altre intestazioni HTTP, incluse quelle che consentono di instradare la richiesta all’origine AEM appropriata.

Al valore *X-AEM-Edge-Key* fanno riferimento le proprietà `edgeKey1` e `edgeKey2` in un file denominato `cdn.yaml` o simile, in una cartella `config` di primo livello. Leggi [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md#folder-structure) per informazioni dettagliate sulla struttura delle cartelle e su come distribuire la configurazione.  La sintassi è descritta nell’esempio seguente.

Per ulteriori informazioni di debug ed errori comuni, controllare [Errori comuni](/help/implementing/dispatcher/cdn.md#common-errors).

>[!WARNING]
>L’accesso diretto senza una chiave X-AEM-Edge-Key corretta verrà negato per tutte le richieste che corrispondono alla condizione (nell’esempio seguente, ossia tutte le richieste al livello di pubblicazione). Se devi introdurre gradualmente l&#39;autenticazione, consulta la sezione [Migrazione sicura per ridurre il rischio di traffico bloccato](#migrating-safely).

```
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_052824}}
        edgeKey2: ${{CDN_EDGEKEY_041425}}
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

Consulta [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md#common-syntax) per una descrizione delle proprietà al di sopra del nodo `data`. Il valore della proprietà `kind` deve essere *CDN* e la proprietà `version` deve essere impostata su `1`.

Per ulteriori dettagli, consulta il passaggio tutorial [Configurare e distribuire la regola CDN di convalida dell&#39;intestazione HTTP](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/content-delivery/custom-domain-names-with-customer-managed-cdn#configure-and-deploy-http-header-validation-cdn-rule).

Altre proprietà includono:

* Nodo `Data` che contiene un nodo `authentication` secondario.
* In `authentication`, un nodo `authenticators` e un nodo `rules`, entrambi array.
* Autenticatori: consente di dichiarare un tipo di token o credenziale, che in questo caso è una chiave Edge. Include le seguenti proprietà:
   * name - una stringa descrittiva.
   * tipo - deve essere `edge`.
   * edgeKey1: il valore di *X-AEM-Edge-Key*, che deve fare riferimento a una [variabile di ambiente di tipo segreto Cloud Manager](/help/operations/config-pipeline.md#secret-env-vars). Per il campo Servizio applicato, selezionare Tutto. Si consiglia che il valore (ad esempio, `${{CDN_EDGEKEY_052824}}`) rifletta il giorno in cui è stato aggiunto.
   * edgeKey2: utilizzato per la rotazione dei segreti, come descritto nella [sezione relativa alla rotazione dei segreti](#rotating-secrets) di seguito. Definitelo in modo simile a edgeKey1. È necessario dichiarare almeno uno di `edgeKey1` e `edgeKey2`.
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* Regole: consente di dichiarare quale degli autenticatori deve essere utilizzato e se si tratta del livello di pubblicazione e/o anteprima.  Include:
   * name - una stringa descrittiva.
   * when: condizione che determina quando valutare la regola, in base alla sintassi nell&#39;articolo [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md). In genere, include un confronto del livello corrente (ad esempio, Pubblica) in modo che tutto il traffico live venga convalidato come routing tramite la rete CDN del cliente.
   * action - deve specificare &quot;authentication&quot; (autentica), facendo riferimento all’autenticatore previsto.

>[!NOTE]
>La chiave Edge deve essere configurata come [variabile di ambiente Cloud Manager di tipo segreto](/help/operations/config-pipeline.md#secret-env-vars), prima che venga distribuita la configurazione che vi fa riferimento. Si consiglia di utilizzare una chiave casuale univoca della lunghezza minima di 32 byte. Ad esempio, la libreria di crittografia Open SSL può generare una chiave casuale eseguendo il comando `openssl rand -hex 32`.

### Migrazione sicura per ridurre il rischio di blocco del traffico {#migrating-safely}

Se il sito è già attivo, presta attenzione durante la migrazione alla rete CDN gestita dal cliente, poiché una configurazione errata può bloccare il traffico pubblico; in quanto solo le richieste con il valore di intestazione X-AEM-Edge-Key previsto verranno accettate dalla rete CDN di Adobe. Si consiglia un approccio quando nella regola di autenticazione viene temporaneamente inclusa una condizione aggiuntiva, che causa il blocco della richiesta solo se viene inclusa un’intestazione di test o se viene trovato un percorso corrispondente:

```
    - name: edge-auth-rule
        when:
          allOf:  
            - { reqProperty: tier, equals: "publish" }
            - { reqHeader: x-edge-test, equals: "test" }
        action:
          type: authenticate
          authenticator: edge-auth
```

```
    - name: edge-auth-rule
        when:
          allOf:
            - { reqProperty: tier, equals: "publish" }
            - { reqProperty: path, like: "/test*" }
        action:
          type: authenticate
          authenticator: edge-auth
```

È possibile utilizzare il seguente pattern di richiesta `curl`:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <CONFIGURED_EDGE_KEY>" -H "x-edge-test: test"
```

Dopo aver completato correttamente il test, è possibile rimuovere la condizione aggiuntiva e ridistribuire la configurazione.

### Processo di migrazione se il supporto Adobe ha generato in precedenza il valore dell&#39;intestazione HTTP `X-AEM-Edge-Key` {#migrating-legacy}

>[!NOTE]
>Prima di procedere con la migrazione, pianifica una migrazione di prova nell’ambiente stage per verificare la strategia.

>[!WARNING]
> Non modificare la chiave nella rete CDN gestita dal cliente fino al passaggio 4.

In precedenza, il processo di integrazione con una rete CDN gestita dal cliente coinvolgeva i clienti che richiedevano un valore di intestazione HTTP X-AEM-Edge-Key dal supporto Adobe, anziché definire il valore autonomamente. Per migrare al più recente approccio self-service in cui si definiscono i propri valori chiave edge, segui questi passaggi per garantire una transizione fluida senza tempi di inattività:

1. Configura la configurazione CDN con i segreti nuovi (generati dal cliente) e vecchi (generati da Adobe) specificati come `edgeKey1` e `edgeKey2`. Questa è una variante della documentazione di [rotating secrets](/help/implementing/dispatcher/cdn-credentials-authentication.md#rotating-secrets).

2. Distribuisci i segreti e la configurazione CDN self-service. A questo punto del processo, il vecchio segreto definito da Adobe deve ancora rimanere come valore X-AEM-Edge-Key passato dalla rete CDN gestita dal cliente.

3. Contatta il supporto Adobe, richiedendo che Adobe passi all’utilizzo della configurazione self-service, specificando che è già stata distribuita.

4. Dopo aver confermato di aver eseguito questa azione, Adobe configura la rete CDN gestita dal cliente per utilizzare la nuova chiave definita dal cliente per il valore dell&#39;intestazione HTTP `X-AEM-Edge-Key`.

5. Rimuovi la chiave precedente dalla configurazione CDN e distribuisci nuovamente la pipeline di configurazione.

>[!WARNING]
>Se non hai configurato il fallback con entrambe le chiavi contemporaneamente, potrebbe verificarsi un downtime durante la migrazione.

## Rimuovi token API {#purge-API-token}

I clienti possono [eliminare la cache CDN](/help/implementing/dispatcher/cdn-cache-purge.md) utilizzando un token API di rimozione dichiarato. Il token è dichiarato in un file denominato `cdn.yaml` o simile, in una cartella `config` di primo livello. Leggi [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md#folder-structure) per informazioni dettagliate sulla struttura delle cartelle e su come distribuire la configurazione.

La sintassi è descritta di seguito:

```
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
       - name: purge-auth
         type: purge
         purgeKey1: ${{CDN_PURGEKEY_031224}}
         purgeKey2: ${{CDN_PURGEKEY_021225}}
    rules:
       - name: purge-auth-rule
         when: { reqProperty: tier, equals: "publish" }
         action:
           type: authenticate
           authenticator: purge-auth
```

Consulta [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md#common-syntax) per una descrizione delle proprietà al di sopra del nodo `data`. Il valore della proprietà `kind` deve essere *CDN* e la proprietà `version` deve essere impostata su `1`.

Altre proprietà includono:

* Nodo `data` che contiene un nodo `authentication` secondario.
* In `authentication`, un nodo `authenticators` e un nodo `rules`, entrambi array.
* Autenticatori: consente di dichiarare un tipo di token o credenziali, che in questo caso è una chiave di rimozione. Include le seguenti proprietà:
   * name - una stringa descrittiva.
   * tipo: deve essere purge.
   * purgeKey1 - il valore deve fare riferimento a una [variabile di ambiente di tipo segreto Cloud Manager](/help/operations/config-pipeline.md#secret-env-vars). Per il campo Servizio applicato, selezionare Tutto. Si consiglia che il valore (ad esempio, `${{CDN_PURGEKEY_031224}}`) rifletta il giorno in cui è stato aggiunto.
   * purgeKey2: utilizzato per la rotazione dei segreti, come descritto nella sezione [segreti rotanti](#rotating-secrets) seguente. È necessario dichiarare almeno uno di `purgeKey1` e `purgeKey2`.
* Regole: consente di dichiarare quale degli autenticatori deve essere utilizzato e se si tratta del livello di pubblicazione e/o anteprima.  Include:
   * name - una stringa descrittiva
   * when: condizione che determina quando valutare la regola, in base alla sintassi nell&#39;articolo [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md). In genere, include un confronto del livello corrente (ad esempio, pubblicazione).
   * action - deve specificare &quot;authentication&quot; (autentica), facendo riferimento all’autenticatore previsto.

>[!NOTE]
>La chiave di eliminazione deve essere configurata come [variabile di ambiente Cloud Manager di tipo segreto](/help/operations/config-pipeline.md#secret-env-vars), prima che venga distribuita la configurazione che vi fa riferimento. Si consiglia di utilizzare una chiave casuale univoca della lunghezza minima di 32 byte; ad esempio, la libreria di crittografia Open SSL può generare una chiave casuale eseguendo il comando openssl rand -hex 32

Puoi fare riferimento a [un&#39;esercitazione](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache) incentrata sulla configurazione delle chiavi di eliminazione e sull&#39;esecuzione dell&#39;eliminazione della cache CDN.

## Autenticazione di base {#basic-auth}

Proteggi alcune risorse di contenuto visualizzando una finestra di dialogo di autenticazione di base che richiede un nome utente e una password. Questa funzione è destinata principalmente a casi di utilizzo di autenticazione leggera, come la revisione dei contenuti da parte delle parti interessate del business, anziché essere una soluzione completa per i diritti di accesso degli utenti finali.

L’utente finale visualizzerà una finestra di dialogo di autenticazione di base simile alla seguente:

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


La sintassi è la seguente:

```
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
       - name: my-basic-authenticator
         type: basic
         credentials:
           - user: johndoe
             password: ${{JOHN_DOE_PASSWORD}}
           - user: janedoe
             password: ${{JANE_DOE_PASSWORD}}
    rules:
       - name: basic-auth-rule
         when: { reqProperty: path, like: "/summercampaign" }
         action:
           type: authenticate
           authenticator: my-basic-authenticator
```

Consulta [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md#common-syntax) per una descrizione delle proprietà al di sopra del nodo `data`. Il valore della proprietà `kind` deve essere *CDN* e la proprietà `version` deve essere impostata su `1`.

Inoltre, la sintassi include:

* un nodo `data` che contiene un nodo `authentication`.
* In `authentication`, un nodo `authenticators` e un nodo `rules`, entrambi array.
* Autenticatori: in questo scenario, dichiara un autenticatore di base, con la seguente struttura:
   * name - una stringa descrittiva
   * tipo - deve essere `basic`
   * array di un massimo di 10 credenziali, ognuna delle quali include le seguenti coppie nome/valore, che gli utenti finali possono immettere nella finestra di dialogo autenticazione di base:
      * user (utente): nome dell’utente.
      * password: il valore deve fare riferimento a una variabile di ambiente di tipo segreto [Cloud Manager](/help/operations/config-pipeline.md#secret-env-vars), con **All** selezionato come campo del servizio.
* Regole: consente di dichiarare quali degli autenticatori devono essere utilizzati e quali risorse devono essere protette. Ogni regola include:
   * name - una stringa descrittiva
   * when: condizione che determina quando valutare la regola, in base alla sintassi nell&#39;articolo [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md). In genere, include un confronto del livello di pubblicazione o di percorsi specifici.
   * action - deve specificare &quot;authenticate&quot;, con riferimento all’autenticatore previsto, che è basic-auth per questo scenario

>[!NOTE]
>
>Le password devono essere configurate come [variabili di ambiente Cloud Manager di tipo segreto](/help/operations/config-pipeline.md#secret-env-vars), prima che venga distribuita la configurazione che vi fa riferimento.

## Rotazione dei segreti {#rotating-secrets}

È buona prassi di sicurezza cambiare le credenziali regolarmente. Tieni presente che le variabili di ambiente non devono essere modificate direttamente, ma crea un nuovo segreto e fai riferimento al nuovo nome nella configurazione.

Questo caso d’uso è esemplificato di seguito, utilizzando l’esempio di una chiave edge, anche se la stessa strategia può essere utilizzata anche per le chiavi di eliminazione.

1. Inizialmente è stato definito solo `edgeKey1`, in questo caso denominato `${{CDN_EDGEKEY_052824}}`, che come convenzione consigliata riflette la data di creazione.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
   ```

1. Quando è il momento di ruotare la chiave, creare un nuovo segreto di Cloud Manager, ad esempio `${{CDN_EDGEKEY_041425}}`.
1. Nella configurazione, fare riferimento a essa da `edgeKey2` e distribuire.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. Dopo aver verificato che la vecchia chiave edge non è più utilizzata, rimuoverla rimuovendo `edgeKey1` dalla configurazione.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. Elimina il riferimento segreto precedente (`${{CDN_EDGEKEY_052824}}`) da Cloud Manager e distribuiscilo.

1. Quando sei pronto per la rotazione successiva, segui la stessa procedura; tuttavia, questa volta aggiungerai `edgeKey1` alla configurazione, facendo riferimento a un nuovo segreto di ambiente di Cloud Manager denominato, ad esempio `${{CDN_EDGEKEY_031426}}`.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
         edgeKey1: ${{CDN_EDGEKEY_031426}}
   ```

Quando si ruotano i segreti impostati nelle intestazioni della richiesta, ad esempio per l’autenticazione su un backend, si consiglia di effettuare la rotazione in due passaggi per garantire che il valore dell’intestazione venga cambiato senza spazi vuoti temporanei.

1. Configurazione iniziale prima della rotazione. In questo stato la vecchia chiave viene inviata al backend.

   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_1}}
   ```

1. Introdurre la nuova chiave `API_KEY_2` impostando due volte la stessa intestazione (la nuova chiave deve essere impostata dopo la chiave precedente). Dopo aver distribuito, la nuova chiave verrà visualizzata nel backend.

   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_1}}
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_2}}
   ```

1. Rimuovi la chiave precedente `API_KEY_1` dalla configurazione. Dopo aver distribuito, la nuova chiave verrà visualizzata nel backend ed è possibile rimuovere la variabile di ambiente della chiave precedente.


   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_2}}
   ```


