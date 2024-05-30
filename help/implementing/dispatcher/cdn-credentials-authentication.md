---
title: Configurazione delle credenziali e dell’autenticazione CDN
description: Scopri come configurare le credenziali e l’autenticazione CDN dichiarando le regole in un file di configurazione che viene quindi distribuito utilizzando la pipeline di configurazione di Cloud Manager.
feature: Dispatcher
source-git-commit: ee993798739232da794dbf7ff0a643ca93effa7d
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 2%

---

# Configurazione delle credenziali e dell’autenticazione CDN {#cdn-credentials-authentication}

>[!NOTE]
>Questa funzione non è ancora disponibile al pubblico. Per partecipare al programma di adozione anticipata, invia un messaggio e-mail a `aemcs-cdn-config-adopter@adobe.com`.

La rete CDN fornita dall’Adobe dispone di diverse funzioni e servizi, alcuni dei quali si basano sulle credenziali e sull’autenticazione per garantire un livello adeguato di sicurezza aziendale. Dichiarando le regole in un file di configurazione distribuito utilizzando [Pipeline di configurazione di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline), i clienti possono configurare in modo autonomo quanto segue:

* Il valore di intestazione HTTP utilizzato dal CDN Adobe per convalidare le richieste provenienti da un CDN gestito dal cliente.
* Token API utilizzato per eliminare le risorse nella cache CDN.

Ognuna di queste, inclusa la sintassi di configurazione, è descritta nella propria sezione di seguito. Il [Configurazione comune](#common-setup) illustra la configurazione comune a entrambi, nonché la distribuzione. Infine, è disponibile una sezione su come [ruotare i tasti](#rotating-secrets), che è considerata una buona pratica in materia di sicurezza.

## Valore intestazione HTTP CDN gestita dal cliente {#CDN-HTTP-value}

Come descritto nella [CDN in AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) , i clienti possono scegliere di indirizzare il traffico attraverso la propria rete CDN, che viene definita Customer CDN (o BYOCDN).

Come parte della configurazione, la rete CDN di Adobe e la rete CDN del cliente devono concordare un valore di `X-AEM-Edge-Key` intestazione HTTP. Questo valore viene impostato su ogni richiesta, sulla rete CDN del cliente, prima che venga instradato alla rete CDN dell’Adobe, la quale verifica che il valore sia quello previsto, in modo che possa essere considerato attendibile da altre intestazioni HTTP, incluse quelle che consentono di instradare la richiesta all’origine AEM appropriata.

Il `X-AEM-Edge-Key` Il valore viene dichiarato con la sintassi seguente. Consulta la [Configurazione comune](#common-setup) per scoprire come distribuirlo.

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
        onFailure: log # optional, default: log, enum: log/block
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

La sintassi per il `X-AEM-Edge-Key` il valore include:

* Tipo, versione e metadati.
* Nodo dati contenente un elemento figlio `experimental_authentication` (il prefisso sperimentale verrà rimosso al rilascio della funzione).
* In experiment_authentication, con un nodo di autenticazione e un nodo di regole, entrambi array.
* Autenticatori: consente di dichiarare un tipo di token o credenziale, che in questo caso è una chiave Edge. Include le seguenti proprietà:
   * name - una stringa descrittiva.
   * tipo: deve essere edge.
   * edgeKey1: il relativo valore deve fare riferimento a un token segreto, che non deve essere memorizzato in Git, ma dichiarato come [Variabile di ambiente di Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) di tipo segreto. Per il campo Servizio applicato, selezionare Tutto. Si consiglia di specificare il valore (ad esempio,`${{CDN_EDGEKEY_052824}}`) riflette il giorno in cui è stato aggiunto.
   * edgeKey2: utilizzato per la rotazione dei segreti, descritta nella [sezione segreti a rotazione](#rotating-secrets) di seguito. Almeno uno di `edgeKey1` e `edgeKey2` deve essere dichiarato.
   * OnFailure: definisce l’azione in uno dei seguenti modi: `log` o `block`, quando una richiesta non corrisponde a `edgeKey1` o `edgeKey2`. Per `log`, l’elaborazione delle richieste continuerà, mentre `block` restituirà un errore 403. Il `log` Questo valore è utile quando esegui il test di un nuovo token su un sito live, in quanto puoi prima verificare che la rete CDN accetti correttamente il nuovo token prima di passare a `block` riduce inoltre la possibilità di perdita di connettività tra la rete CDN del cliente e la rete CDN di Adobe, a causa di una configurazione errata.
* Regole: consente di dichiarare quale degli autenticatori deve essere utilizzato e se si tratta del livello di pubblicazione e/o anteprima.  Include:
   * name - una stringa descrittiva.
   * quando: una condizione che determina quando la regola deve essere valutata, in base alla sintassi nella [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md) articolo. In genere, include un confronto del livello corrente (ad esempio, Pubblica) in modo che tutto il traffico live venga convalidato come routing tramite la rete CDN del cliente.
   * action - deve specificare &quot;authentication&quot; (autentica), facendo riferimento all’autenticatore previsto.

>[!NOTE]
>La chiave Edge deve essere configurata come [Variabile di ambiente di Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) variabile di tipo `secret`, prima della distribuzione della configurazione a cui fa riferimento.

## Rimuovi token API {#purge-API-token}

I clienti possono eliminare la cache CDN utilizzando un token API di rimozione dichiarato. Il token viene dichiarato con la sintassi seguente.  Consulta la [Configurazione comune](#common-setup) per scoprire come distribuirlo.

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
* nodo dati contenente un elemento figlio `experimental_authentication` (il prefisso sperimentale verrà rimosso al rilascio della funzione).
* Sotto `experimental_authentication`, con un singolo nodo di autenticazione.
* Autenticatori: consente di dichiarare un tipo di token o credenziali, che in questo caso è una chiave di rimozione. Include le seguenti proprietà:
   * name - una stringa descrittiva.
   * tipo: deve essere purge.
   * purgeKey1: il relativo valore deve fare riferimento a un token segreto, che non deve essere memorizzato in Git, ma dichiarato come [Variabili di ambiente di Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) di tipo `secret`.
   * Per il campo Servizio applicato, selezionare Tutto. Si consiglia di specificare il valore (ad esempio, `${{CDN_PURGEKEY_031224}}`) riflette il giorno in cui è stato aggiunto.
   * purgeKey2: utilizzato per la rotazione dei segreti, come descritto in [sezione segreti a rotazione](#rotating-secrets) sezione successiva. Almeno uno di `purgeKey1` e `purgeKey2` deve essere dichiarato.
* Regole: consente di dichiarare quale degli autenticatori deve essere utilizzato e se si tratta del livello di pubblicazione e/o anteprima.  Include:
   * name - una stringa descrittiva
   * quando: una condizione che determina quando la regola deve essere valutata, in base alla sintassi nella [Regole filtro traffico](/help/security/traffic-filter-rules-including-waf.md) articolo. In genere, include un confronto del livello corrente (ad esempio, pubblicazione).
   * action - deve specificare &quot;authentication&quot; (autentica), facendo riferimento all’autenticatore previsto.

>[!NOTE]
>La chiave Edge deve essere configurata come [Variabile di ambiente di Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) variabile di tipo `secret`, prima della distribuzione della configurazione a cui fa riferimento.

## Configurazione comune {#common-setup}

Tutti gli autenticatori sono impostati come segue:

* Innanzitutto, crea la seguente cartella e struttura di file nella cartella di livello principale del progetto Git:

```
config/
     cdn.yaml
```

* In secondo luogo, `cdn.yaml` Il file di configurazione deve contenere i nodi descritti negli esempi seguenti. Il `kind` deve essere impostata su `CDN` e la versione deve essere impostata sulla versione dello schema, attualmente `1`. Il nodo dei metadati ha una proprietà &quot;envTypes&quot; che indica su quali tipi di ambiente (dev, stage, prod) verrà valutata questa configurazione.

* Infine, crea una pipeline di configurazione della distribuzione di destinazione in Cloud Manager. Consulta [configurazione delle pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [configurazione di pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

Tieni presente che:

* Al momento gli RDE non supportano la pipeline di configurazione.
* Puoi utilizzare `yq` per convalidare localmente la formattazione YAML del file di configurazione (ad es. `yq cdn.yaml`).

## Rotazione dei segreti {#rotating-secrets}

È buona prassi di sicurezza modificare occasionalmente le credenziali. Questa operazione può essere eseguita come esemplificato di seguito, utilizzando l&#39;esempio di una chiave di spigolo, anche se la stessa strategia viene utilizzata per le chiavi di rimozione.

* Inizialmente solo `edgeKey1` è stato definito, in questo caso denominato `${{CDN_EDGEKEY_052824}}`, che come convenzione consigliata, riflette la data di creazione.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* Quando è il momento di ruotare la chiave, crea un nuovo segreto di Cloud Manager, ad esempio `${{CDN_EDGEKEY_041425}}`.
* Nella configurazione, fai riferimento a `edgeKey2` e distribuire.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Una volta che si è certi che la vecchia chiave edge non è più utilizzata, rimuoverla rimuovendo `edgeKey1` dalla configurazione.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Elimina il riferimento segreto precedente (`${{CDN_EDGEKEY_052824}}`) da Cloud Manager e implementa.
* Quando sei pronto per la rotazione successiva, segui la stessa procedura, ma questa volta aggiungerai `edgeKey1` alla configurazione, facendo riferimento a un nuovo segreto dell’ambiente di Cloud Manager denominato, ad esempio, `${{CDN_EDGEKEY_031426}}`.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
