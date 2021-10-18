---
title: Configurazione della rete avanzata per AEM as a Cloud Service
description: Scopri come configurare funzionalità di rete avanzate come VPN o un indirizzo IP in uscita flessibile o dedicato per AEM as a Cloud Service
source-git-commit: 47803e6af4ae3c95600c75be58c907da82112e1b
workflow-type: tm+mt
source-wordcount: '2837'
ht-degree: 1%

---


# Configurazione della rete avanzata per AEM as a Cloud Service {#configuring-advanced-networking}

Questo articolo ha lo scopo di presentarti le diverse funzionalità di rete avanzate in AEM as a Cloud Service, inclusi gli indirizzi IP VPN e in uscita che possono essere dedicati o allocati in modo flessibile.

## Panoramica {#overview}

>[!INFO]
>
>La funzionalità di rete avanzata fa parte della versione 2021.9.0 e sarà abilitata per i clienti a metà ottobre.

AEM as a Cloud Service offre diversi tipi di funzionalità di rete avanzate, che possono essere configurate dai clienti utilizzando le API di Cloud Manager. Comprendono:

* [Uscita](#flexible-port-egress)  porta flessibile: configura AEM as a Cloud Service per consentire il traffico in uscita da porte non standard
* [Indirizzo](#dedicated-egress-IP-address)  IP di uscita dedicato: configura il traffico in uscita da AEM as a Cloud Service per l&#39;origine da un IP univoco
* [Virtual Private Network (VPN)](#vpn) : traffico sicuro tra l&#39;infrastruttura di un cliente e AEM as a Cloud Service, per i clienti che dispongono di tecnologia VPN

Questo articolo descrive in dettaglio ciascuna di queste opzioni, incluso come configurarle. Come strategia di configurazione generale, l’endpoint API `/networkInfrastructures` viene richiamato a livello di programma per dichiarare il tipo desiderato di rete avanzata, seguito da una chiamata all’ endpoint `/advancedNetworking` per ogni ambiente per abilitare l’infrastruttura e configurare parametri specifici dell’ambiente. Fai riferimento agli endpoint appropriati nella documentazione API di Cloud Manager per ogni sintassi formale, oltre a richieste di esempio e risposte.

Quando si decide tra l&#39;uscita flessibile della porta e l&#39;indirizzo IP in uscita dedicato, si consiglia di scegliere l&#39;uscita flessibile della porta se non è necessario un indirizzo IP specifico perché l&#39;Adobe può ottimizzare le prestazioni del traffico in uscita flessibile della porta.

>[!INFO]
>
>La rete avanzata non è disponibile per il programma sandbox.

>[!NOTE]
>
>I clienti già dotati di tecnologia di uscita dedicata legacy che devono configurare una di queste opzioni non devono farlo oppure la connettività del sito potrebbe essere interessata. Per assistenza, contatta il supporto Adobe.

## Avanzamento delle porte flessibile {#flexible-port-egress}

Questa funzionalità avanzata di rete consente di configurare AEM as a Cloud Service per incrementare il traffico attraverso porte diverse da HTTP (porta 80) e HTTPS (porta 443), che sono aperte per impostazione predefinita.

### Considerazioni {#flexible-port-egress-considerations}

L&#39;uscita dalla porta flessibile è la scelta consigliata se non hai bisogno di VPN e non hai bisogno di un indirizzo IP di uscita dedicato, in quanto il traffico che non si basa su un&#39;uscita dedicata può raggiungere un throughput più elevato.

### Configurazione {#configuring-flexible-port-egress-provision}

Una volta per programma, viene richiamato l&#39;endpoint POST `/program/<programId>/networkInfrastructures`, semplicemente trasmettendo il valore di `flexiblePortEgress` per il parametro e l&#39;area geografica `kind`. L&#39;endpoint risponde con `network_id`, oltre ad altre informazioni tra cui lo stato . Nei documenti API viene fatto riferimento all’intero set di parametri e alla sintassi esatta.

Una volta effettuata la chiamata, in genere sono necessari circa 15 minuti per il provisioning dell&#39;infrastruttura di rete. Una chiamata all&#39;endpoint [di GET ambiente di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getEnvironment) mostrerebbe lo stato &quot;ready&quot;.

Se la configurazione dell&#39;uscita della porta flessibile con ambito di programma è pronta, l&#39;endpoint `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` deve essere richiamato per ogni ambiente per abilitare la rete a livello di ambiente e per dichiarare eventuali regole di inoltro della porta. I parametri sono configurabili in base all’ambiente per offrire flessibilità.

Le regole di inoltro di porta devono essere dichiarate per tutte le porte diverse da 80/443 specificando il set di host di destinazione (nomi o IP e con porte). Per ogni host di destinazione, i clienti devono mappare la porta di destinazione prevista su una porta da 30000 a 30999.

L&#39;API dovrebbe rispondere in pochi secondi, indicando uno stato di aggiornamento e dopo circa 10 minuti, il metodo `GET` dell&#39;endpoint dovrebbe indicare che la rete avanzata è abilitata.

### Aggiornamenti {#updating-flexible-port-egress-provision}

La configurazione a livello di programma può essere aggiornata richiamando l’ endpoint `PUT /api/program/<program_id>/network/<network_id>` e avrà effetto entro pochi minuti.

>[!NOTE]
>
> Il parametro &quot;kind&quot; (`flexiblePortEgress`, `dedicatedEgressIP` o `VPN`) non può essere modificato. Contatta l’assistenza clienti per descrivere cosa è già stato creato e il motivo della modifica.

È possibile aggiornare le regole di inoltro delle porte per ambiente richiamando nuovamente l&#39;endpoint `PUT /program/{programId}/environment/{environmentId}/advancedNetworking`, assicurandosi di includere l&#39;intero set di parametri di configurazione, anziché un sottoinsieme.

### Eliminazione o disabilitazione dell&#39;avanzamento della porta flessibile {#deleting-disabling-flexible-port-egress-provision}

Per **eliminare** l&#39;infrastruttura di rete, invia un ticket di assistenza clienti, descrivendo cosa è stato creato e perché deve essere eliminato.

Per **disabilitare** l&#39;uscita della porta flessibile da un particolare ambiente, richiamare `DELETE [/program/{programId}/environment/{environmentId}/advancedNetworking]()`.

Per ulteriori informazioni, consulta la [Documentazione API di Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Routing del traffico {#flexible-port-egress-traffic-routing}

Il traffico Http o https verso le destinazioni attraverso le porte 80 o 443 passerà attraverso un proxy preconfigurato, supponendo che venga utilizzata la libreria di rete Java standard. Per il traffico http o https che attraversa altre porte, è necessario configurare un proxy utilizzando le seguenti proprietà.

* `AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST`
* `AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT`

Ad esempio, di seguito è riportato un codice di esempio per inviare una richiesta a `www.example.com:8443`:

```java
String url = "www.example.com:8443"
var proxyHost = System.getenv("AEM_HTTPS_PROXY_HOST");
var proxyPort = Integer.parseInt(System.getenv("AEM_HTTPS_PROXY_PORT"));
HttpClient client = HttpClient.newBuilder()
      .proxy(ProxySelector.of(new InetSocketAddress(proxyHost, proxyPort)))
      .build();
 
HttpRequest request = HttpRequest.newBuilder().uri(URI.create(url)).build();
HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
```

Se utilizzi librerie di rete Java non standard, configura i proxy utilizzando le proprietà riportate sopra per tutto il traffico.

Il traffico non http/s con destinazioni attraverso porte dichiarate nel parametro `portForwards` deve fare riferimento a una proprietà denominata `AEM_PROXY_HOST`, insieme alla porta mappata. Esempio:

```java
DriverManager.getConnection("jdbc:mysql://" + System.getenv("AEM_PROXY_HOST") + ":53306/test");
```

La tabella seguente descrive l’indirizzamento del traffico:

<table>
<thead>
  <tr>
    <th>Traffico</th>
    <th>Condizioni di identificazione</th>
    <th>Porta</th>
    <th>Connessione</th>
    <th>Esempio</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocollo Http o https</b></td>
    <td>Traffico http standard</td>
    <td>80 o 443</td>
    <td>Consentito</td>
    <td></td>
  </tr> 
  <tr>
    <td></td>
    <td>Traffico non standard (su altre porte al di fuori degli 80 o 443) tramite proxy http configurato utilizzando queste variabili di ambiente:<br><ul>
     <li>AEM_HTTP_PROXY_HOST / AEM_HTTPS_PROXY_HOST</li>
     <li>AEM_HTTP_PROXY_PORT / AEM_HTTPS_PROXY_PORT</li>
    </ul>
    <td>Porte esterne 80 o 443</td>
    <td>Consentito</td>
  </tr>
  <tr>
    <td></td>
    <td>Traffico non standard (su altre porte al di fuori delle porte 80 o 443) non utilizzando il proxy http</td>
    <td>Porte esterne 80 o 443</td>
    <td>Bloccato</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Non http o non-https</b></td>
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

**Configurazione di Apache / Dispatcher**

La direttiva `mod_proxy` del livello AEM Cloud Service Apache/Dispatcher può essere configurata utilizzando le proprietà descritte in precedenza.

```
ProxyRemote "http://example.com" "http://${AEM_HTTP_PROXY_HOST}:${AEM_HTTP_PROXY_PORT}"
ProxyPass "/somepath" "http://example.com"
ProxyPassReverse "/somepath" "http://example.com"
```

```
SSLProxyEngine on //needed for https backends
 
ProxyRemote "https://example.com:8443" "http://${AEM_HTTPS_PROXY_HOST}:${AEM_HTTPS_PROXY_PORT}"
ProxyPass "/somepath" "https://example.com:8443"
ProxyPassReverse "/somepath" "https://example.com:8443"
```

## Indirizzo IP Egress dedicato {#dedicated-egress-IP-address}

>[!NOTE]
>
>Se hai effettuato il provisioning con un IP in uscita dedicato prima della versione di settembre 2021 (21/10/20), fai riferimento al [Legacy Dedicated Egress Address Customers](#legacy-dedicated-egress-address-customers).

### Vantaggi {#benefits}

Questo indirizzo IP dedicato può migliorare la sicurezza durante l’integrazione con i fornitori SaaS (come un fornitore di gestione delle relazioni con i clienti) o altre integrazioni al di fuori di AEM as a Cloud Service che offrono un inserì nell&#39;elenco Consentiti di indirizzi IP. Aggiungendo l’indirizzo IP dedicato all’inserire nell&#39;elenco Consentiti, si garantisce che solo il traffico dall’AEM Cloud Service del cliente possa fluire nel servizio esterno. Oltre al traffico proveniente da qualsiasi altro IP consentito.

Senza l’abilitazione della funzione di indirizzo IP dedicato, il traffico proveniente da AEM flussi as a Cloud Service passa attraverso un set di IP condivisi con altri clienti.

### Configurazione {#configuring-dedicated-egress-provision}

>[!INFO]
>
>La funzionalità di inoltro Splunk non è possibile da un indirizzo IP di uscita dedicato.

La configurazione dell&#39;indirizzo IP in uscita dedicato è identica a [porta in uscita flessibile](#configuring-flexible-port-egress-provision).

La differenza principale è che il traffico proverrà sempre da un IP dedicato e univoco. Per trovare quell&#39;IP, utilizza un resolver DNS per identificare l&#39;indirizzo IP associato a `p{PROGRAM_ID}.external.adobeaemcloud.com`. L’indirizzo IP non dovrebbe cambiare, ma se deve cambiare in futuro, verrà fornita una notifica avanzata.

Oltre alle regole di indirizzamento supportate dall&#39;uscita della porta flessibile nell&#39;endpoint `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking`, l&#39;indirizzo IP di uscita dedicato supporta un parametro `nonProxyHosts`. Questo consente di dichiarare un set di host che devono essere indirizzati attraverso un intervallo di indirizzi IP condivisi anziché l’IP dedicato, il che può essere utile in quanto il traffico che passa attraverso gli IP condivisi può essere ulteriormente ottimizzato. Gli URL `nonProxyHost` possono seguire i pattern di `example.com` o `*.example.com`, dove il carattere jolly è supportato solo all’inizio del dominio.

Quando si decide tra l&#39;uscita flessibile della porta e l&#39;indirizzo IP in uscita dedicato, i clienti devono scegliere l&#39;uscita flessibile della porta se non è necessario un indirizzo IP specifico, in quanto l&#39;Adobe può ottimizzare le prestazioni del traffico in uscita flessibile della porta.

### Routing del traffico {#dedcated-egress-ip-traffic-routing}

<table>
<thead>
  <tr>
    <th>Traffico</th>
    <th>Condizione di destinazione</th>
    <th>Porta</th>
    <th>Connessione</th>
    <th>Esempio</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocollo Http o https</b></td>
    <td>Traffico verso Azure o servizi Adobe</td>
    <td>Qualsiasi</td>
    <td>Tramite gli IP del cluster condiviso (non l'IP dedicato)</td>
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
    <td>Tramite la configurazione proxy http, configurata per impostazione predefinita per il traffico http/s utilizzando la libreria client Java HTTP standard</td>
    <td>Qualsiasi</td>
    <td>Attraverso l'IP dedicato in uscita</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora la configurazione proxy http (ad esempio, se viene rimossa esplicitamente dalla libreria client Java HTTP standard o se viene utilizzata una libreria Java che ignora la configurazione proxy standard)</td>
    <td>80 o 443</td>
    <td>Tramite gli IP del cluster condiviso</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>Ignora la configurazione proxy http (ad esempio, se viene rimossa esplicitamente dalla libreria client Java HTTP standard o se viene utilizzata una libreria Java che ignora la configurazione proxy standard)</td>
    <td>Porte esterne 80 o 443</td>
    <td>Bloccato</td>
    <td></td>
  </tr>
  <tr>
    <td><b>Non http o non-https</b></td>
    <td>Il client si connette alla variabile env <code>AEM_PROXY_HOST</code> utilizzando un <code>portOrig</code> dichiarato nel parametro API <code>portForwards</code></td>
    <td>Qualsiasi</td>
    <td>Attraverso l'IP dedicato in uscita</td>
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

## Clienti di indirizzi Egress Dedicati Legacy {#legacy-dedicated-egress-address-customers}

Se hai effettuato il provisioning con un IP in uscita dedicato prima del 2021.09.30, la funzionalità IP in uscita dedicata funzionerà come descritto di seguito.

### Utilizzo delle funzioni {#feature-usage}

La funzione è compatibile con il codice Java o con le librerie che generano traffico in uscita, purché utilizzino le proprietà standard del sistema Java per le configurazioni proxy. In pratica, dovrebbe includere la maggior parte delle librerie comuni.

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
[`HttpClientBuilder.useSystemProperties()`](https://hc.apache.org/httpcomponents-client-4.5.x/current/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html) o utilizza
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

Lo stesso IP dedicato viene applicato a tutti i programmi di un cliente nella propria organizzazione di Adobe e a tutti gli ambienti in ciascuno dei loro programmi. Si applica sia ai servizi di authoring che di pubblicazione.

Sono supportate solo le porte HTTP e HTTPS. Questo include HTTP/1.1 e HTTP/2 se crittografati.

### Considerazioni sul debug {#debugging-considerations}

Per verificare che il traffico sia effettivamente in uscita sull’indirizzo IP dedicato previsto, controlla i registri nel servizio di destinazione, se disponibili. In caso contrario, potrebbe essere utile richiamare un servizio di debug come [https://ifconfig.me/IP](https://ifconfig.me/IP), che restituirà l&#39;indirizzo IP chiamante.

## Virtual Private Network (VPN) {#vpn}

La VPN consente la connessione a un’infrastruttura on-premise o a un centro dati da autore, pubblicazione o anteprima. Ad esempio, per i mezzi di accesso a un database.

Consente inoltre di connettersi a fornitori SaaS come un fornitore CRM che supporta VPN o di connettersi da una rete aziendale a AEM autore, anteprima o pubblicazione as a Cloud Service.

Sono supportati la maggior parte dei dispositivi VPN con tecnologia IPSec. Consulta l&#39;elenco dei dispositivi in [questa pagina](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-devices#devicetable), in base alle informazioni contenute nella colonna **Istruzioni di configurazione RouteBased** . Configura il dispositivo come descritto nella tabella.

### Considerazioni generali {#general-vpn-considerations}

* Il supporto è limitato a una singola connessione VPN
* La funzionalità di inoltro Splunk non è possibile tramite una connessione VPN.

### Creazione {#vpn-creation}

Una volta che per programma viene richiamato l&#39;endpoint POST `/program/<programId>/networkInfrastructures`, passando un payload di informazioni di configurazione tra cui: il valore di &quot;vpn&quot; per il parametro `kind`, la regione, lo spazio di indirizzo (elenco CIDR - notare che questo non può essere modificato in seguito), i resolver DNS (per la risoluzione dei nomi nella rete del cliente) e le informazioni di connessione VPN come la configurazione del gateway, la chiave VPN condivisa e i criteri di sicurezza IP. L&#39;endpoint risponde con `network_id`, oltre ad altre informazioni tra cui lo stato . L&#39;intero set di parametri e la sintassi esatta devono essere indicati nella [documentazione API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/createNetworkInfrastructure).

Una volta effettuata la chiamata, in genere l&#39;infrastruttura di rete richiede tra i 45 e i 60 minuti. Il metodo GET dell’API può essere chiamato per restituire lo stato corrente, che alla fine passerà da `creating` a `ready`. Consulta la documentazione API per tutti gli stati.

Se la configurazione VPN con ambito di programma è pronta, l&#39;endpoint `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` deve essere richiamato per ogni ambiente per abilitare la rete a livello di ambiente e per dichiarare eventuali regole di inoltro porte. I parametri sono configurabili in base all’ambiente per offrire flessibilità.

Per ulteriori informazioni, consulta la [documentazione API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/enableEnvironmentAdvancedNetworkingConfiguration) .

Le regole di inoltro delle porte devono essere dichiarate per qualsiasi traffico TCP non http/s che deve essere instradato attraverso la VPN specificando il set di host di destinazione (nomi o IP e con porte). Per ogni host di destinazione, i clienti devono mappare la porta di destinazione prevista su una porta da 30000 a 30999, dove i valori devono essere univoci in tutti gli ambienti del programma. I clienti possono anche elencare un set di url nel parametro `nonProxyHosts` , che dichiara l’URL per il quale il traffico deve bypassare il routing VPN, ma tramite un intervallo IP condiviso. Segue i pattern di `example.com` o `*.example.com`, dove il carattere jolly è supportato solo all’inizio del dominio.

L’API dovrebbe rispondere in pochi secondi, indicando uno stato di `updating` e dopo circa 10 minuti, una chiamata all’endpoint del GET ambiente di Cloud Manager mostrerebbe uno stato di `ready`, indicando che l’aggiornamento dell’ambiente è stato applicato.

Tieni presente che anche se non sono presenti regole di indirizzamento del traffico dell’ambiente (host o bypass), è comunque necessario chiamare `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` , solo con un payload vuoto.

### Aggiornamento della VPN {#updating-the-vpn}

La configurazione VPN a livello di programma può essere aggiornata richiamando l’endpoint `PUT /api/program/<program_id>/network/<network_id>` .

Lo spazio degli indirizzi non può essere modificato dopo il provisioning VPN iniziale. Se necessario, contatta l’assistenza clienti. Inoltre, il parametro `kind` (`flexiblePortEgress`, `dedicatedEgressIP` o `VPN`) non può essere modificato. Contatta l’assistenza clienti per descrivere cosa è già stato creato e il motivo della modifica.

Le regole di routing per ambiente possono essere aggiornate richiamando nuovamente l&#39;endpoint `PUT /program/{programId}/environment/{environmentId}/advancedNetworking`, assicurandosi di includere l&#39;intero set di parametri di configurazione, anziché un sottoinsieme. In genere, l’applicazione degli aggiornamenti dell’ambiente richiede 5-10 minuti.

### Eliminazione o disabilitazione della VPN {#deleting-or-disabling-the-vpn}

Per eliminare l’infrastruttura di rete, invia un ticket di assistenza clienti, descrivendo cosa è stato creato e perché deve essere eliminato.

Per disabilitare la VPN per un particolare ambiente, invoca `DELETE /program/{programId}/environment/{environmentId}/advancedNetworking`. Maggiori dettagli nella [documentazione API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/disableEnvironmentAdvancedNetworkingConfiguration).

### Routing del traffico {#vpn-traffic-routing}

La tabella seguente descrive l’indirizzamento del traffico.

<table>
<thead>
  <tr>
    <th>Traffico</th>
    <th>Condizione di destinazione</th>
    <th>Porta</th>
    <th>Connessione</th>
    <th>Esempio</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><b>Protocollo Http o https</b></td>
    <td>Traffico verso Azure o servizi Adobe</td>
    <td>Qualsiasi</td>
    <td>Tramite gli IP del cluster condiviso (non l'IP dedicato)</td>
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
    <td>Se l'IP rientra nell'intervallo di spazio <i>Indirizzo gateway VPN</i> e attraverso la configurazione proxy http (configurata per impostazione predefinita per il traffico http/s utilizzando la libreria client Java HTTP standard)</td>
    <td>Qualsiasi</td>
    <td>Tramite la VPN</td>
    <td><code>10.0.0.1:443</code>Può essere anche un nome host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Se l'IP non rientra nell'intervallo <i>spazio degli indirizzi gateway VPN</i> e attraverso la configurazione proxy http (configurata per impostazione predefinita per il traffico http/s utilizzando la libreria client Java HTTP standard)</td>
    <td>Qualsiasi</td>
    <td>Attraverso l'IP dedicato in uscita</td>
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
    <td><b>Non http o non-https</b></td>
    <td>Se l’IP rientra nell’intervallo <i>spazio degli indirizzi del gateway VPN</i> e il client si connette alla variabile env <code>AEM_PROXY_HOST</code> utilizzando un <code>portOrig</code> dichiarato nel parametro API <code>portForwards</code></td>
    <td>Qualsiasi</td>
    <td>Tramite la VPN</td>
    <td><code>10.0.0.1:3306</code>Può essere anche un nome host.</td>
  </tr>
  <tr>
    <td></td>
    <td>Se l'IP non rientra nell'intervallo di indirizzi <i>VPN gateway </i> e il client si connette alla variabile env <code>AEM_PROXY_HOST</code> utilizzando un <code>portOrig</code> dichiarato nel parametro API <code>portForwards</code></td>
    <td>Qualsiasi</td>
    <td>Attraverso l'IP dedicato in uscita</td>
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

### Domini utili per la configurazione{#vpn-useful-domains-for-configuration}

Il diagramma seguente fornisce una rappresentazione visiva di un insieme di domini e IP associati che sono utili per la configurazione e lo sviluppo. La tabella riportata di seguito descrive tali domini e IP.

![Configurazione del dominio VPN](/help/security/assets/AdvancedNetworking.jpg)

<table>
<thead>
  <tr>
    <th>Pattern di dominio</th>
    <th>Egress (dal AEM)</th>
    <th>Ingresso (a AEM) significato</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><code>p{PROGRAM_ID}.external.adobeaemcloud.com</code></td>
    <td>Indirizzo IP di uscita dedicato per il traffico che va verso Internet anziché attraverso reti private </td>
    <td>Le connessioni dalla VPN mostrerebbero alla CDN come provenienti da questo IP. Per consentire solo le connessioni dalla VPN a AEM, configura Cloud Manager per consentire solo questo IP e bloccare tutto il resto. Per ulteriori informazioni, consulta la sezione "Limitare l’ingresso alle connessioni VPN" .</td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}-gateway.external.adobeaemcloud.com</code></td>
    <td>N/D</td>
    <td>IP del gateway VPN sul lato AEM. Il team di progettazione della rete di un cliente può utilizzarlo per consentire solo le connessioni VPN al proprio gateway VPN da un indirizzo IP specifico. </td>
  </tr>
  <tr>
    <td><code>p{PROGRAM_ID}.inner.adobeaemcloud.net</code></td>
    <td>IP del traffico proveniente dal lato AEM della VPN verso il lato cliente. Questo può essere inserito nell'elenco Consentiti nella configurazione del cliente per garantire che le connessioni possano essere effettuate solo da AEM.</td>
    <td>Se il cliente desidera consentire solo l’accesso VPN a AEM, deve configurare le voci DNS CNAME per mappare <code>author-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> e/o <code>publish-p{PROGRAM_ID}-e{ENVIRONMENT_ID}.adobeaemcloud.com</code> a questo.</td>
  </tr>
</tbody>
</table>

### Limita VPN a connessioni in ingresso {#restrict-vpn-to-ingress-connections}

Se desideri consentire solo l’accesso VPN a AEM, in Cloud Manager è possibile configurare gli inserire nell&#39;elenco Consentiti dell’ambiente in modo che solo l’IP definito da `p{PROGRAM_ID}.external.adobeaemcloud.com` possa parlare con l’ambiente. Questa operazione può essere eseguita nello stesso modo di qualsiasi altro inserire nell&#39;elenco Consentiti basato su IP in Cloud Manager.

Se le regole devono essere basate su percorsi, utilizza le direttive http standard a livello di dispatcher per negare o consentire determinati IP. Devono garantire che anche i percorsi desiderati non siano memorizzabili in cache nella rete CDN in modo che la richiesta arrivi sempre all’origine.

**Esempio Di Configurazione Httpd**

```
Order deny,allow
Deny from all
Allow from 192.168.0.1
Header always set Cache-Control private
```

## Transizione tra i tipi di rete avanzati {#transitioning-between-advanced-networking-types}

Poiché il parametro `kind` non può essere modificato, contatta l’assistenza clienti per descrivere cosa è già stato creato e il motivo della modifica.