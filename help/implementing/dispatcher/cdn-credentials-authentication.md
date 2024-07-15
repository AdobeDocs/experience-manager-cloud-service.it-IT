---
title: Configurazione delle credenziali CDN e dell’autenticazione
description: Scopri come configurare le credenziali e l’autenticazione CDN dichiarando le regole in un file di configurazione che viene quindi distribuito utilizzando la pipeline di configurazione di Cloud Manager.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 73d0a4a73a3e97a91b2276c86d3ed1324de8c361
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 4%

---

# Configurazione delle credenziali CDN e dell’autenticazione {#cdn-credentials-authentication}

>[!NOTE]
>Questa funzione non è ancora disponibile al pubblico. Per partecipare al programma di adozione anticipata, inviare un&#39;e-mail a `aemcs-cdn-config-adopter@adobe.com`.

La rete CDN fornita dall’Adobe dispone di diverse funzioni e servizi, alcuni dei quali si basano sulle credenziali e sull’autenticazione per garantire un livello adeguato di sicurezza aziendale. Dichiarando le regole in un file di configurazione distribuito utilizzando la [pipeline di configurazione di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline), i clienti possono configurare in modo autonomo quanto segue:

* Il valore di intestazione HTTP utilizzato dal CDN Adobe per convalidare le richieste provenienti da un CDN gestito dal cliente.
* Token API utilizzato per eliminare le risorse nella cache CDN.
* Un elenco di combinazioni nome utente/password che possono accedere a contenuto con restrizioni, inviando un modulo di autenticazione di base.


Ognuna di queste, inclusa la sintassi di configurazione, è descritta nella propria sezione di seguito. La sezione [Configurazione comune](#common-setup) illustra la configurazione comune a entrambi, nonché la distribuzione. Infine, è presente una sezione su come [ruotare le chiavi](#rotating-secrets), che è considerata una buona pratica di sicurezza.

## Valore intestazione HTTP CDN gestita dal cliente {#CDN-HTTP-value}

Come descritto nella pagina [CDN in AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN), i clienti possono scegliere di instradare il traffico attraverso la propria rete CDN, denominata anche CDN cliente (talvolta denominata BYOCDN).

Come parte della configurazione, la rete CDN Adobe e la rete CDN cliente devono concordare un valore dell&#39;intestazione HTTP `X-AEM-Edge-Key`. Questo valore viene impostato su ogni richiesta, sulla rete CDN del cliente, prima che venga instradato alla rete CDN dell’Adobe, la quale verifica che il valore sia quello previsto, in modo che possa essere considerato attendibile da altre intestazioni HTTP, incluse quelle che consentono di instradare la richiesta all’origine AEM appropriata.

Il valore `X-AEM-Edge-Key` è dichiarato con la sintassi seguente, con il valore effettivo a cui fanno riferimento le proprietà edgeKey1 e edgeKey2. Consulta la sezione [Configurazione comune](#common-setup) per scoprire come distribuire la configurazione.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
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

La sintassi per il valore `X-AEM-Edge-Key` include:

* Tipo, versione e metadati.
* Nodo dati che contiene un nodo `experimental_authentication` secondario (il prefisso sperimentale verrà rimosso al rilascio della funzione).
* In `experimental_authentication`, un nodo `authenticators` e un nodo `rules`, entrambi array.
* Autenticatori: consente di dichiarare un tipo di token o credenziale, che in questo caso è una chiave Edge. Include le seguenti proprietà:
   * name - una stringa descrittiva.
   * tipo - deve essere `edge`.
   * edgeKey1: il valore di *X-AEM-Edge-Key*, che deve fare riferimento a un token segreto, che non deve essere archiviato in Git, ma dichiarato come [Variabile di ambiente Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) di tipo segreto. Per il campo Servizio applicato, selezionare Tutto. Si consiglia che il valore (ad esempio, `${{CDN_EDGEKEY_052824}}`) rifletta il giorno in cui è stato aggiunto.
   * edgeKey2: utilizzato per la rotazione dei segreti, come descritto nella [sezione relativa alla rotazione dei segreti](#rotating-secrets) di seguito. Definitelo in modo simile a edgeKey1. È necessario dichiarare almeno uno di `edgeKey1` e `edgeKey2`.
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* Regole: consente di dichiarare quale degli autenticatori deve essere utilizzato e se si tratta del livello di pubblicazione e/o anteprima.  Include:
   * name - una stringa descrittiva.
   * when: condizione che determina quando valutare la regola, in base alla sintassi nell&#39;articolo [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md). In genere, include un confronto del livello corrente (ad esempio, Pubblica) in modo che tutto il traffico live venga convalidato come routing tramite la rete CDN del cliente.
   * action - deve specificare &quot;authentication&quot; (autentica), facendo riferimento all’autenticatore previsto.

>[!NOTE]
>La chiave Edge deve essere configurata come variabile di ambiente [Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) di tipo `secret` (con *Tutti* selezionati per il servizio applicato) prima che venga distribuita la configurazione che vi fa riferimento.

## Rimuovi token API {#purge-API-token}

I clienti possono [eliminare la cache CDN](/help/implementing/dispatcher/cdn-cache-purge.md) utilizzando un token API di rimozione dichiarato. Il token viene dichiarato con la sintassi seguente.  Per informazioni su come distribuirla, consulta la sezione [Configurazione comune](#common-setup).

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
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

La sintassi include:

* tipo, versione e metadati.
* nodo dati che contiene un nodo `experimental_authentication` secondario (il prefisso sperimentale verrà rimosso al rilascio della funzione).
* In `experimental_authentication`, un nodo `authenticators` e un nodo `rules`, entrambi array.
* Autenticatori: consente di dichiarare un tipo di token o credenziali, che in questo caso è una chiave di rimozione. Include le seguenti proprietà:
   * name - una stringa descrittiva.
   * tipo: deve essere purge.
   * purgeKey1 - il valore deve fare riferimento a un token segreto, che non deve essere archiviato in Git, ma dichiarato come [Variabili di ambiente Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) di tipo `secret`.
   * Per il campo Servizio applicato, selezionare Tutto. Si consiglia che il valore (ad esempio, `${{CDN_PURGEKEY_031224}}`) rifletta il giorno in cui è stato aggiunto.
   * purgeKey2: utilizzato per la rotazione dei segreti, come descritto nella sezione [rotating secrets](#rotating-secrets) di seguito. È necessario dichiarare almeno uno di `purgeKey1` e `purgeKey2`.
* Regole: consente di dichiarare quale degli autenticatori deve essere utilizzato e se si tratta del livello di pubblicazione e/o anteprima.  Include:
   * name - una stringa descrittiva
   * when: condizione che determina quando valutare la regola, in base alla sintassi nell&#39;articolo [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md). In genere, include un confronto del livello corrente (ad esempio, pubblicazione).
   * action - deve specificare &quot;authentication&quot; (autentica), facendo riferimento all’autenticatore previsto.

>[!NOTE]
>La chiave Edge deve essere configurata come variabile di ambiente [Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) di tipo `secret`, prima che venga distribuita la configurazione che vi fa riferimento.

## Autenticazione di base {#basic-auth}

Proteggi alcune risorse di contenuto visualizzando una finestra di dialogo di autenticazione di base che richiede un nome utente e una password. Questa funzione è destinata principalmente a casi di utilizzo di autenticazione leggera, come la revisione dei contenuti da parte delle parti interessate del business, anziché essere una soluzione completa per i diritti di accesso degli utenti finali.

L’utente finale visualizzerà una finestra di dialogo di autenticazione di base simile alla seguente:

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


La sintassi viene dichiarata come descritto di seguito. Consulta la sezione [Configurazione comune](#common-setup) di seguito per informazioni su come distribuirla.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
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

La sintassi include:

* tipo, versione e metadati.
* un nodo di dati che contiene un nodo `experimental_authentication` (il prefisso sperimentale verrà rimosso al rilascio della funzione).
* In `experimental_authentication`, un nodo `authenticators` e un nodo `rules`, entrambi array.
* Autenticatori: in questo scenario, dichiara un autenticatore di base, con la seguente struttura:
   * name - una stringa descrittiva
   * tipo - deve essere `basic`
   * array di credenziali, ciascuna delle quali include le seguenti coppie nome/valore, che gli utenti finali possono immettere nella finestra di dialogo autenticazione di base:
      * user (utente): nome dell’utente
      * password: il valore deve fare riferimento a un token segreto, che non deve essere memorizzato in Git, ma dichiarato come Variabili di ambiente Cloud Manager di tipo segreto (con **Tutti** selezionati come campo del servizio)
* Regole: consente di dichiarare quali degli autenticatori devono essere utilizzati e quali risorse devono essere protette. Ogni regola include:
   * name - una stringa descrittiva
   * when: condizione che determina quando valutare la regola, in base alla sintassi nell&#39;articolo [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md). In genere, include un confronto del livello di pubblicazione o di percorsi specifici.
   * action - deve specificare &quot;authenticate&quot;, con riferimento all’autenticatore previsto, che è basic-auth per questo scenario

>[!NOTE]
>La chiave Edge deve essere configurata come variabile di ambiente [Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) di tipo `secret`, prima che venga distribuita la configurazione che vi fa riferimento.

## Configurazione comune {#common-setup}

Tutti gli autenticatori sono impostati come segue:

* Innanzitutto, crea la seguente cartella e struttura di file nella cartella di livello principale del progetto Git:

```
config/
     cdn.yaml
```

* In secondo luogo, il file di configurazione `cdn.yaml` deve contenere i nodi descritti negli esempi seguenti. La proprietà `kind` deve essere impostata su `CDN` e la versione deve essere impostata sulla versione dello schema, attualmente `1`. Il nodo dei metadati ha una proprietà &quot;envTypes&quot; che indica su quali tipi di ambiente (dev, stage, prod) verrà valutata questa configurazione.

* Infine, crea una pipeline di configurazione della distribuzione di destinazione in Cloud Manager. Consulta [configurazione delle pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [configurazione delle pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

Tieni presente che:

* Al momento gli RDE non supportano la pipeline di configurazione.
* Puoi utilizzare `yq` per convalidare localmente la formattazione YAML del file di configurazione (ad es. `yq cdn.yaml`).

## Rotazione dei segreti {#rotating-secrets}

È buona prassi di sicurezza modificare occasionalmente le credenziali. Questa operazione può essere eseguita come esemplificato di seguito, utilizzando l&#39;esempio di una chiave di spigolo, anche se la stessa strategia viene utilizzata per le chiavi di rimozione.

* Inizialmente è stato definito solo `edgeKey1`, in questo caso denominato `${{CDN_EDGEKEY_052824}}`, che come convenzione consigliata riflette la data di creazione.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* Quando è il momento di ruotare la chiave, creare un nuovo segreto di Cloud Manager, ad esempio `${{CDN_EDGEKEY_041425}}`.
* Nella configurazione, fare riferimento a essa da `edgeKey2` e distribuire.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Dopo aver verificato che la vecchia chiave edge non è più utilizzata, rimuoverla rimuovendo `edgeKey1` dalla configurazione.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Elimina il riferimento segreto precedente (`${{CDN_EDGEKEY_052824}}`) da Cloud Manager e distribuiscilo.
* Quando sei pronto per la rotazione successiva, segui la stessa procedura; tuttavia, questa volta aggiungerai `edgeKey1` alla configurazione, facendo riferimento a un nuovo segreto di ambiente di Cloud Manager denominato, ad esempio `${{CDN_EDGEKEY_031426}}`.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
