---
title: Configurazione di networking avanzato per AEM as a Cloud Service
description: Scopri come configurare funzionalità di rete avanzate come VPN o un indirizzo IP in uscita flessibile o dedicato per AEM as a Cloud Service
exl-id: 968cb7be-4ed5-47e5-8586-440710e4aaa9
source-git-commit: 8ca2340bf6d39248ed3596828f27745dcaff2c75
workflow-type: ht
source-wordcount: '3053'
ht-degree: 100%

---

# Configurazione di networking avanzato per AEM as a Cloud Service {#configuring-advanced-networking}

Questo articolo mira a presentarti le diverse funzionalità di rete avanzate in AEM as a Cloud Service, tra cui il provisioning self-service di VPN, porte non standard e indirizzi IP in uscita dedicati.

>[!INFO]
>
>Puoi anche trovare una serie di articoli progettati per guidarti attraverso ciascuna delle opzioni di rete avanzate in questa [posizione](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=it).

## Panoramica {#overview}

AEM as a Cloud Service offre diversi tipi di funzionalità di rete avanzate, che possono essere configurate dai clienti utilizzando le API di Cloud Manager. Comprendono:

* [Uscita porta flessibile](#flexible-port-egress) - configura AEM as a Cloud Service per consentire il traffico in uscita da porte non standard
* [Indirizzo IP in uscita dedicato](#dedicated-egress-IP-address) - configura il traffico da AEM as a Cloud Service per l’origine da un IP univoco
* [Virtual Private Network (VPN)](#vpn) - traffico sicuro tra l’infrastruttura di un cliente e AEM as a Cloud Service, per i clienti che dispongono di tecnologia VPN

Questo articolo descrive in dettaglio ciascuna di queste opzioni, incluso come configurarle. Come strategia generale di configurazione, l’endpoint API `/networkInfrastructures` viene richiamato a livello di programma per dichiarare il tipo desiderato di rete avanzata, seguito da una chiamata all’endpoint `/advancedNetworking` per ogni ambiente per abilitare l’infrastruttura e configurare parametri specifici dell’ambiente. Fai riferimento agli endpoint appropriati nella documentazione API di Cloud Manager per ogni sintassi formale, oltre a richieste di esempio e risposte.

Un programma può fornire un’unica variante di rete avanzata. Quando bisogna decidere tra l’uscita flessibile della porta e l’indirizzo IP in uscita dedicato, si consiglia di scegliere l’uscita flessibile della porta se non è necessario un indirizzo IP specifico perché Adobe può ottimizzare le prestazioni del traffico in uscita flessibile della porta.

>[!INFO]
>
>La rete avanzata non è disponibile per il programma sandbox.
>Inoltre, gli ambienti devono essere aggiornati a AEM versione 5958 o successiva.

>[!NOTE]
>
>I clienti già dotati di tecnologia di uscita dedicata legacy che devono configurare una di queste opzioni non dovrebbero farlo oppure la connettività del sito potrebbe essere influenzata. Per assistenza, contatta il supporto Adobe.

## Uscita flessibile della porta {#flexible-port-egress}

Questa funzionalità avanzata di rete consente di configurare AEM as a Cloud Service per incrementare il traffico attraverso porte diverse da HTTP (porta 80) e HTTPS (porta 443), che sono aperte per impostazione predefinita.

### Considerazioni {#flexible-port-egress-considerations}

L’uscita dalla porta flessibile è la scelta consigliata se non hai bisogno di VPN e non hai bisogno di un indirizzo IP di uscita dedicato, in quanto il traffico che non si basa su un’uscita dedicata può raggiungere una produttività più elevata.

### Configurazione {#configuring-flexible-port-egress-provision}

Una volta per programma, l’endpoint POST `/program/<programId>/networkInfrastructures` viene richiamato, passando semplicemente il valore di `flexiblePortEgress` per il parametro `kind` e area geografica. L’endpoint risponde con `network_id`, nonché altre informazioni, compreso lo stato. Per informazioni sull’intero set di parametri e sulla sintassi esatta, nonché altre informazioni importanti (ad esempio, quali parametri non possono essere modificati in un secondo momento), consulta la [documentazione sulle API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure).

Una volta effettuata la chiamata, in genere sono necessari circa 15 minuti per il provisioning dell’infrastruttura di rete. Una chiamata all’[endpoint GET per infrastruttura di rete](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getNetworkInfrastructure) di Cloud Manager mostrerebbe uno stato “ready”.

Se la configurazione dell’uscita della porta flessibile con ambito di programma è pronta, l’endpoint `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` deve essere richiamato per ambiente per abilitare la rete a livello di ambiente e per dichiarare facoltativamente eventuali regole di inoltro porte. I parametri sono configurabili in base all’ambiente per offrire flessibilità.

Le regole di port forwarding devono essere dichiarate per tutte le porte di destinazione diverse da 80/443, ma solo se non si utilizza il protocollo http o https, 
specificando il set di host di destinazione (nomi o IP e con le porte). Per ogni host di destinazione, i clienti devono mappare la porta di destinazione prevista su una porta da 30000 a 30999.

L’API dovrebbe rispondere in pochi secondi, indicando lo stato di aggiornamento e dopo circa 10 minuti, il metodo `GET` dell’endpoint indica che la rete avanzata è abilitata.

### Aggiornamenti {#updating-flexible-port-egress-provision}

È possibile aggiornare la configurazione a livello di programma richiamando l’endpoint `PUT /api/program/<program_id>/network/<network_id>` e entrerà in vigore tra pochi minuti.

>[!NOTE]
>
> Il parametro “tipo” (`flexiblePortEgress`, `dedicatedEgressIP` o `VPN`) non può essere modificato. Contatta l’assistenza clienti per descrivere cosa è già stato creato e il motivo della modifica.

È possibile aggiornare le regole di inoltro delle porte per ambiente richiamando nuovamente l’endpoint `PUT /program/{programId}/environment/{environmentId}/advancedNetworking`, assicurandosi di includere l’intero set di parametri di configurazione, anziché un sottoinsieme.

### Disabilitazione dell’uscita con porta flessibile {#disabling-flexible-port-egress-provision}

Al fine di **disabilitare** l’uscita con porta flessibile da un particolare ambiente, richiama `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

Per ulteriori informazioni sulle API, consulta la [documentazione API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Routing del traffico {#flexible-port-egress-traffic-routing}

Per il traffico http o https che accede a porte diverse da 80 o 443, è necessario configurare un proxy utilizzando le seguenti variabili di ambiente host e porte:

* per HTTP: `AEM_PROXY_HOST` / `AEM_HTTP_PROXY_PORT ` (impostazione predefinita `proxy.tunnel:3128` nelle versioni AEM &lt; 6094)
* per HTTPS: `AEM_PROXY_HOST` / `AEM_HTTPS_PROXY_PORT ` (impostazione predefinita `proxy.tunnel:3128` nelle versioni AEM &lt; 6094)

Ad esempio, di seguito è riportato un codice di esempio per inviare una richiesta a `www.example.com:8443`:

```java
String url = "www.example.com:8443"
String proxyHost = System.getenv().getOrDefault("AEM_PROXY_HOST", "proxy.tunnel");
int proxyPort = Integer.parseInt(System.getenv().getOrDefault("AEM_HTTPS_PROXY_PORT", "3128"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

Se utilizzi librerie di rete Java non standard, configura i proxy utilizzando le proprietà riportate sopra per tutto il traffico.

Il traffico non http/s con destinazioni attraverso porte dichiarate nel parametro `portForwards` deve fare riferimento a una proprietà denominata `AEM_PROXY_HOST`, oltre alla porta mappata. Esempio:

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

La tabella seguente descrive il routing del traffico:

<table>
<thead>
  <tr>
    <th>Traffico</th>
    <th>Condizione di destinazione</th>
    <th>Porta </th>
    <th>Connessione</th>
    <th>Esempio di destinazione esterna</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocollo Http o https</b></td>
    <td>Traffico http/s standard</td>
    <td>80 o 443</td>
    <td>Consentito</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>Traffico non standard (su altre porte diverse da 80 o 443) tramite proxy http configurato utilizzando la variabile di ambiente e il numero di porta proxy seguenti. Non dichiarare la porta di destinazione nel parametro portForwards della chiamata API di Cloud Manager:<br><ul>
     <li>AEM_PROXY_HOST (impostazione predefinita ‘proxy.tunnel’ nelle versioni AEM &lt; 6094)</li>
     <li>AEM_HTTPS_PROXY_PORT (impostazione predefinita porta 3128 nelle versioni AEM &lt; 6094)</li>
    </ul>
    <td>Porte esterne 80 o 443</td>
    <td>Consentito</td>
    <td>example.com:8443</td>
  </tr>
  <tr>
    <td></td>
    <td>Traffico non standard (su altre porte diverse dalle porte 80 o 443) che non utilizza il proxy http</td>
    <td>Porte esterne 80 o 443</td>
    <td>Bloccato</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Non http o non https</b></td>
    <td>Il client si connette alla variabile di ambiente <code>AEM_PROXY_HOST</code> utilizzando un <code>portOrig</code> dichiarato nel parametro API <code>portForwards</code>.</td>
    <td>Qualsiasi</td>
    <td>Consentito</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>Tutto il resto</td>
    <td>Qualsiasi</td>
    <td>Bloccato</td>
    <td><code>db.example.com:5555</code></td>
  </tr>
</tbody>
</table>

**Configurazione di Apache/Dispatcher**

La direttiva `mod_proxy` del livello Apache/Dispatcher di AEM Cloud Service può essere configurata utilizzando le proprietà descritte in precedenza.

```
ProxyRemote "http://example.com:8080" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "http://example.com:8080"
ProxyPassReverse "/somepath" "http://example.com:8080"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_PROXY_HOST}:3128"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## Indirizzo IP in uscita dedicato {#dedicated-egress-IP-address}

>[!NOTE]
>
>Se hai effettuato il provisioning con un IP in uscita dedicato prima della versione di settembre 2021 (10/06/21), fai riferimento a [Clienti di indirizzi in uscita dedicati legacy](#legacy-dedicated-egress-address-customers).

### Vantaggi {#benefits}

Questo indirizzo IP dedicato può migliorare la sicurezza durante l’integrazione con i fornitori SaaS (ad esempio, un fornitore CRM) o altre integrazioni al di fuori di AEM as a Cloud Service che offrono un elenco Consentiti di indirizzi IP. Aggiungendo l’indirizzo IP dedicato all’elenco Consentiti, si garantisce che solo il traffico proveniente dall’istanza di AEM Cloud Service del cliente possa passare al servizio esterno. Verrà aggiunto al traffico proveniente da qualsiasi altro IP consentito.

Se la funzione di indirizzo IP dedicato non è abilitata, il traffico proveniente da AEM as a Cloud Service passa attraverso una serie di IP condivisi con altri clienti.

### Configurazione {#configuring-dedicated-egress-provision}

>[!INFO]
>
>La funzionalità di inoltro Splunk non è possibile da un indirizzo IP in uscita dedicato.

La configurazione dell’indirizzo IP in uscita dedicato è identica all’[uscita da porta flessibile](#configuring-flexible-port-egress-provision).

La differenza principale è che il traffico sarà sempre in uscita da un IP dedicato e univoco. Per trovare tale IP, utilizza un risolutore DNS per identificare l’indirizzo IP associato a `p{PROGRAM_ID}.external.adobeaemcloud.com`. L’indirizzo IP non dovrebbe cambiare, ma se deve cambiare in futuro, verrà fornita una notifica avanzata.

Oltre alle regole di routing supportate dall’uscita da porta flessibile nell’endpoint `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`, l’indirizzo IP in uscita dedicato supporta un parametro `nonProxyHosts`. Questo consente di dichiarare un gruppo di host che devono indirizzare attraverso un intervallo di indirizzi IP condivisi anziché l’indirizzo IP dedicato, il che può essere utile in quanto il traffico in uscita attraverso gli IP condivisi può essere ulteriormente ottimizzato. Gli URL `nonProxyHost` possono seguire i pattern di `example.com` o `*.example.com`, in cui il carattere jolly è supportato solo all’inizio del dominio.

Quando si decide tra uscita da porta flessibile e indirizzo IP in uscita dedicato, i clienti devono scegliere la prima soluzione se non è necessario un indirizzo IP specifico, poiché Adobe può ottimizzare le prestazioni del traffico in uscita da porta flessibile.

### Disabilitazione indirizzo IP di uscita dedicato {#disabling-dedicated-egress-IP-address}

Per **disabilitare** l’indirizzo IP di uscita dedicato da un particolare ambiente, richiama `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

Per ulteriori informazioni sulle API, consulta la [documentazione API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Routing del traffico {#dedcated-egress-ip-traffic-routing}

Il traffico http o https passa attraverso un proxy preconfigurato, a condizione che utilizzi le proprietà standard del sistema Java per le configurazioni proxy.

Il traffico non http/s con destinazioni attraverso porte dichiarate nel parametro `portForwards` deve fare riferimento a una proprietà denominata `AEM_PROXY_HOST`, oltre alla porta mappata. Esempio:

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

<table>
<thead>
  <tr>
    <th>Traffico</th>
    <th>Condizione di destinazione</th>
    <th>Porta </th>
    <th>Connessione</th>
    <th>Esempio di destinazione esterna</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocollo Http o https</b></td>
    <td>Traffico verso Azure o servizi Adobe</td>
    <td>Qualsiasi</td>
    <td>Tramite gli IP del cluster condiviso (non l’IP dedicato)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>Host corrispondente al parametro <code>nonProxyHosts</code></td>
    <td>80 o 443</td>
    <td>Tramite gli IP del cluster condiviso</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Host corrispondente al parametro <code>nonProxyHosts</code></td>
    <td>Porte esterne 80 o 443</td>
    <td>Bloccato</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Tramite la configurazione proxy http, configurata per impostazione predefinita per il traffico http/s utilizzando la libreria client HTTP Java standard</td>
    <td>Qualsiasi</td>
    <td>Attraverso l’IP dedicato in uscita</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora la configurazione proxy http (ad esempio, se viene rimossa esplicitamente dalla libreria client HTTP Java standard o se viene utilizzata una libreria Java che ignora la configurazione proxy standard)</td>
    <td>80 o 443</td>
    <td>Tramite gli IP del cluster condiviso</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora la configurazione proxy http (ad esempio, se viene rimossa esplicitamente dalla libreria client HTTP Java standard o se viene utilizzata una libreria Java che ignora la configurazione proxy standard)</td>
    <td>Porte esterne 80 o 443</td>
    <td>Bloccato</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Non http o non https</b></td>
    <td>Il client si connette alla variabile d’ambiente <code>AEM_PROXY_HOST</code> usando un <code>portOrig</code> dichiarato nel parametro API <code>portForwards</code></td>
    <td>Qualsiasi</td>
    <td>Attraverso l’IP dedicato in uscita</td>
    <td><code>mysql.example.com:3306</code></td>
  </tr>
  <tr>
    <td></td>
    <td>Qualsiasi altra</td>
    <td></td>
    <td>Bloccato</td>
    <td></td>
  </tr>
</tbody>
</table>

## Utilizzo della funzione {#feature-usage}

La funzione è compatibile con il codice o le librerie Java che generano traffico in uscita, purché utilizzino le proprietà standard del sistema Java per le configurazioni proxy. In pratica, dovrebbe essere inclusa la maggior parte delle librerie comuni.

Di seguito è riportato un esempio di codice:

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

Alcune librerie richiedono una configurazione esplicita per utilizzare le proprietà standard del sistema Java per le configurazioni proxy.

Un esempio che utilizza Apache HttpClient, che richiede chiamate esplicite a
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) o l’uso di
[`HttpClients.createSystem()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClients.html#createSystem()):

```java
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();

  HttpClient httpClient = HttpClientBuilder.create().useSystemProperties().build();
  HttpGet request = new HttpGet(finalUrl.toURI());
  request.setHeader("Accept", "application/json");
  request.setHeader("X-API-KEY", apiKey);
  HttpResponse response = httpClient.execute(request);
  String result = EntityUtils.toString(response.getEntity());
}
```

Lo stesso IP dedicato viene applicato a tutti i programmi di un cliente nella sua organizzazione Adobe e per tutti gli ambienti in ciascuno dei suoi programmi. Si applica ai servizi sia di authoring che di pubblicazione.

### Considerazioni sul debug {#debugging-considerations}

Per verificare che il traffico sia effettivamente in uscita all’indirizzo IP dedicato previsto, controlla i registri nel servizio di destinazione, se disponibili. Altrimenti può essere utile richiamare un servizio di debug come [https://ifconfig.me/IP](https://ifconfig.me/IP), che restituirà l’indirizzo IP chiamante.

## Clienti con indirizzi in uscita dedicati legacy {#legacy-dedicated-egress-address-customers}

Se hai effettuato il provisioning con un IP in uscita dedicato prima del 30.09.2021, la funzionalità IP in uscita dedicata supporta solo le porte HTTP e HTTPS.
Questo include HTTP/1.1 e HTTP/2 se crittografati. Inoltre, un endpoint di uscita dedicato può comunicare con qualsiasi destinazione solo tramite HTTP/HTTPS rispettivamente sulle porte 80/443.

## Virtual Private Network (VPN) {#vpn}

La VPN consente la connessione a un’infrastruttura on-premise o a un centro dati dall’ambiente di authoring, pubblicazione o anteprima. Ad esempio, per le procedure di accesso a un database.

Consente inoltre di connettersi ai fornitori SaaS, ad esempio un fornitore di CRM che supporta la VPN o la connessione da una rete aziendale all’ambiente di authoring, anteprima o pubblicazione di AEM as a Cloud Service.

Sono supportati la maggior parte dei dispositivi VPN con tecnologia IPSec. Consulta l’elenco dei dispositivi in [questa pagina](https://docs.microsoft.com/it-it/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable), in base alle informazioni contenute nella colonna delle **istruzioni di configurazione RouteBased**. Configura il dispositivo come descritto nella tabella.

### Considerazioni generali {#general-vpn-considerations}

* Il supporto è limitato a una singola connessione VPN
* La funzionalità di inoltro Splunk non è possibile tramite una connessione VPN.

### Creazione {#vpn-creation}

Una volta per programma, viene richiamato l’endpoint POST `/program/<programId>/networkInfrastructures`, passando in un payload di informazioni di configurazione che includono: il valore di “vpn” per il parametro `kind`, l’area geografica, lo spazio indirizzi (elenco di CIDR - nota che questo valore non potrà essere modificato in seguito), i risolutori DNS (per la risoluzione dei nomi nella rete del cliente) e informazioni sulla connessione VPN, ad esempio la configurazione del gateway, la chiave VPN condivisa e i criteri di sicurezza IP. L&#39;endpoint risponde con `network_id`, nonché altre informazioni, tra cui lo stato. Per il set completo di parametri e la sintassi esatta è necessario fare riferimento alla [documentazione dell’API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure).

Una volta effettuata la chiamata, in genere il provisioning dell’infrastruttura di rete richiede tra i 45 e i 60 minuti. Il metodo GET dell’API può essere chiamato per restituire lo stato corrente, che alla fine passerà da `creating` a `ready`. Consulta la documentazione dell’API per tutti gli stati.

Se la configurazione VPN in ambito di programma è pronta, l’endpoint `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` deve essere richiamato per ambiente per abilitare la rete a livello di ambiente e per dichiarare eventuali regole di port forwarding. I parametri sono configurabili in base all’ambiente per offrire flessibilità.

Per ulteriori informazioni, consulta la [documentazione dell’API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration).

Le regole di port forwarding devono essere dichiarate per tutto il traffico TCP non http/s che deve essere instradato attraverso la VPN specificando il set di host di destinazione (nomi o IP e con le porte). Per ogni host di destinazione, i clienti devono mappare la porta di destinazione prevista a una porta da 30000 a 30999, i cui valori devono essere univoci in tutti gli ambienti del programma. I clienti possono inoltre indicare un set di URL nel parametro `nonProxyHosts`, che dichiara l’URL per cui il traffico deve ignorare il routing VPN e passare attraverso un intervallo IP condiviso. Segue i pattern di `example.com` o `*.example.com`, in cui il carattere jolly è supportato solo all’inizio del dominio.

L’API dovrebbe rispondere in pochi secondi indicando lo stato `updating` e dopo circa 10 minuti, una chiamata all’endpoint GET dell’ambiente di Cloud Manager dovrebbe mostrare lo stato `ready`, indicando che l’aggiornamento è stato applicato all’ambiente.

Tieni presente che anche se non sono presenti regole di routing del traffico dell’ambiente (host o bypass), è comunque necessario chiamare `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`, solo con un payload vuoto.

### Aggiornamento della VPN {#updating-the-vpn}

La configurazione VPN a livello di programma può essere aggiornata richiamando l’endpoint `PUT /api/program/<program_id>/network/<network_id>`.

Lo spazio indirizzi non può essere modificato dopo il provisioning iniziale della VPN. Se necessario, contatta l’Assistenza clienti. Inoltre, il parametro `kind` (`flexiblePortEgress`, `dedicatedEgressIP` o `VPN`) non può essere modificato. Contatta l’assistenza clienti per descrivere cosa è già stato creato e il motivo della modifica.

È possibile aggiornare le regole di routing per ambiente richiamando nuovamente l’endpoint `PUT /program/{programId}/environment/{environmentId}/advancedNetworking`, assicurandosi di includere il set completo di parametri di configurazione, anziché un sottoinsieme. In genere, l’applicazione degli aggiornamenti dell’ambiente richiede 5-10 minuti.

### Disabilitazione della VPN {#disabling-the-vpn}

Per disabilitare la VPN per un particolare ambiente, richiama `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`. Troverai maggiori dettagli nella [documentazione dell’API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Routing del traffico {#vpn-traffic-routing}

La tabella seguente descrive il routing del traffico.

<table>
<thead>
  <tr>
    <th>Traffico</th>
    <th>Condizione di destinazione</th>
    <th>Porta </th>
    <th>Connessione</th>
    <th>Esempio di destinazione esterna</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocollo Http o https</b></td>
    <td>Traffico verso Azure o servizi Adobe</td>
    <td>Qualsiasi</td>
    <td>Tramite gli IP del cluster condiviso (non l’IP dedicato)</td>
    <td>adobe.io<br>api.windows.net</td>
  </tr>
  <tr>
    <td></td>
    <td>Host corrispondente al parametro <code>nonProxyHosts</code></td>
    <td>80 o 443</td>
    <td>Tramite gli IP del cluster condiviso</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Host corrispondente al parametro <code>nonProxyHosts</code></td>
    <td>Porte esterne 80 o 443</td>
    <td>Bloccato</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Se l’IP rientra nell’intervallo di spazio <i>Indirizzo gateway VPN</i> e tramite la configurazione proxy http (configurata per impostazione predefinita per il traffico http/s utilizzando la libreria client Java HTTP standard)</td>
    <td>Qualsiasi</td>
    <td>Tramite la VPN</td>
    <td><code>10.0.0.1:443</code>Può essere anche un nome host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Se l’IP non rientra nell’intervallo <i>Spazio degli indirizzi gateway VPN</i> e attraverso la configurazione proxy http (configurata per impostazione predefinita per il traffico http/s utilizzando la libreria client Java HTTP standard)</td>
    <td>Qualsiasi</td>
    <td>Attraverso l’IP dedicato in uscita</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora la configurazione proxy http (ad esempio, se viene rimossa esplicitamente dalla libreria client Java HTTP standard o se si utilizza una libreria Java che ignora la configurazione proxy standard)
</td>
    <td>80 o 443</td>
    <td>Tramite gli IP del cluster condiviso</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora la configurazione proxy http (ad esempio, se viene rimossa esplicitamente dalla libreria client Java HTTP standard o se si utilizza una libreria Java che ignora la configurazione proxy standard)</td>
    <td>Porte esterne 80 o 443</td>
    <td>Bloccato</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Non http o non https</b></td>
    <td>Se l’IP rientra nell’intervallo <i>Spazio degli indirizzi gateway VPN</i> e il client si connette a <code>AEM_PROXY_HOST</code> variabile env che utilizza un <code>portOrig</code> dichiarato nel parametro di API <code>portForwards</code> </td>
    <td>Qualsiasi</td>
    <td>Tramite la VPN</td>
    <td><code>10.0.0.1:3306</code>Può essere anche un nome host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Se l’IP non rientra nell’intervallo <i>Spazio degli indirizzi gateway VPN</i> e il client si connette a <code>AEM_PROXY_HOST</code> variabile env che utilizza un <code>portOrig</code> dichiarato nel parametro di API <code>portForwards</code></td>
    <td>Qualsiasi</td>
    <td>Attraverso l’IP dedicato in uscita</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Qualsiasi altra</td>
    <td>Qualsiasi</td>
    <td>Bloccato</td>
    <td></td>
  </tr>
</tbody>
</table>

### Domini utili per la configurazione {#vpn-useful-domains-for-configuration}

Il diagramma seguente fornisce una rappresentazione visiva di un insieme di domini e IP associati che sono utili per la configurazione e lo sviluppo. La tabella riportata di seguito descrive tali domini e IP.

![Configurazione del dominio VPN](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>Pattern di dominio</th>
    <th>Significato in uscita (da AEM)</th>
    <th>Significato ingresso (a AEM) </th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>Indirizzo IP di uscita dedicato per il traffico che va verso Internet anziché attraverso reti private </td>
    <td>Le connessioni dalla VPN verrebbero visualizzate in CDN come provenienti da questo IP. Per consentire solo le connessioni dalla VPN a AEM, configura Cloud Manager per consentire solo questo IP e bloccare tutto il resto. Per ulteriori informazioni, consulta la sezione “Limitare l’ingresso alle connessioni VPN”.</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.{REGION}-gateway.external.adobeaemcloud.com</code></td>
    <td>N/D</td>
    <td>IP del gateway VPN sul lato AEM. Il team di progettazione della rete di un cliente può utilizzarlo per consentire solo le connessioni VPN al proprio gateway VPN da un indirizzo IP specifico. </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>IP del traffico proveniente dal lato AEM della VPN verso il lato cliente. Questo può essere aggiunto all’elenco Consentiti nella configurazione del cliente per garantire che le connessioni possano essere effettuate solo da AEM.</td>
    <td>Se il cliente desidera consentire l’accesso VPN ad AEM, deve configurare le voci DNS CNAME per mappare il proprio dominio personalizzato e/o <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> e/o <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> a questo oggetto.</td>
  </tr>
</tbody>
</table>

### Limitare la VPN alle connessioni in ingresso {#restrict-vpn-to-ingress-connections}

Se vuoi consentire solo l’accesso VPN ad AEM, è possibile configurare gli inserimenti nell’elenco Consentiti dell’ambiente in Cloud Manager in modo che solo l’IP definito da `p{PROGRAM_ID}.external.adobeaemcloud.com` è autorizzato a parlare con l’ambiente. Questa operazione può essere eseguita come per qualsiasi altro inserimento nell’elenco Consentiti basato su IP in Cloud Manager.

Se le regole devono essere basate su percorsi, utilizza le direttive http standard a livello di dispatcher per negare o consentire determinati IP. Devono anche garantire che i percorsi desiderati non siano memorizzabili nella cache sulla CDN in modo che la richiesta arrivi sempre all’origine.

**Esempio di configurazione Httpd**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## Eliminazione dell’infrastruttura di rete di un programma {#deleting-network-infrastructure}

Per **eliminare** l’infrastruttura di rete per un programma, richiama `DELETE /program/{program ID}/networkinfrastructure/{networkinfrastructureID}`.

>[!NOTE]
>
> Il comando Elimina eliminerà l’infrastruttura solo se tutte le reti avanzate sono disabilitate.

## Transizione tra tipi di rete avanzati {#transitioning-between-advanced-networking-types}

È possibile migrare tra tipi di rete avanzate seguendo questa procedura:

* Disabilita la rete avanzata in tutti gli ambienti.
* Elimina l’infrastruttura di rete avanzata.
* Crea di nuovo le infrastrutture di rete avanzata con i valori corretti.
* Abilita di nuovo la rete avanzata a livello di ambiente.

>[!WARNING]
>
> Questa procedura comporterà un downtime dei servizi di rete avanzata tra eliminazione e ricreazione.

Se i tempi di inattività dovessero avere un impatto significativo sulle attività aziendali, contatta l’Assistenza clienti e descrivi cosa è già stato creato e il motivo del cambiamento.
