---
title: Aggiungere un nome di dominio personalizzato
description: Scopri come aggiungere un nome di dominio personalizzato con Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: dd696580758e7ab9a5427d47fda4275f9ad7997f
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 20%

---


# Aggiungere un nome di dominio personalizzato {#adding-cdn}

Scopri come aggiungere un nome di dominio personalizzato con Cloud Manager.

## Requisiti {#requirements}

Prima di aggiungere un nome di dominio personalizzato in Cloud Manager, è necessario soddisfare questi requisiti.

* È necessario aggiungere un certificato SSL di dominio per il dominio che si desidera aggiungere prima di aggiungere un nome di dominio personalizzato come descritto nel documento [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Per aggiungere un nome di dominio personalizzato in Cloud Manager è necessario avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.
* Utilizzare la rete CDN Fastly.

>[!IMPORTANT]
>
>Anche se utilizzi una rete CDN non Adobe, devi comunque aggiungere il dominio a Cloud Manager.

## Dove aggiungere i nomi di dominio personalizzati {#}

In Cloud Manager è possibile aggiungere un nome di dominio personalizzato da due posizioni:

* [Dalla pagina Impostazioni dominio](#adding-cdn-settings)
* [Dalla pagina Ambienti](#adding-cdn-environments)

Quando si aggiunge un nome di dominio personalizzato, il dominio viene gestito utilizzando il certificato valido più specifico. Se più certificati hanno lo stesso dominio, viene scelto quello aggiornato più di recente. L’Adobe consiglia di gestire i certificati in modo che non vi siano domini sovrapposti.

I passaggi per entrambi i metodi descritti in questo documento si basano su Fastly. Se utilizzi una rete CDN diversa, configura il dominio con la rete CDN che hai scelto di utilizzare.

## Aggiungere un nome di dominio personalizzato dalla pagina Impostazioni dominio {#adding-cdn-settings}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nel pannello di navigazione a sinistra, seleziona la scheda **Impostazioni dominio**

   ![Finestra Impostazioni dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Nell&#39;angolo superiore destro della pagina **Impostazioni dominio** fare clic su **Aggiungi dominio**.

1. Nella finestra di dialogo **Aggiungi dominio** immettere il nome di dominio personalizzato in uso nel campo **Nome dominio**.
Non includere `http://`, `https://` o spazi durante l’inserimento del dominio.

1. Fai clic su **Crea**.

1. Nella finestra di dialogo **Verifica dominio**, in **Quale tipo di certificato intendi utilizzare con questo dominio?Elenco a discesa**, selezionare una delle opzioni seguenti:

   | Tipo di certificato | Descrizione |
   | --- | --- |
   | Certificato gestito da Adobe | Selezionare se si desidera utilizzare un certificato DV (convalida dominio). Questa opzione è ideale per la maggior parte dei casi e fornisce la convalida di base del dominio. Adobe gestisce e rinnova automaticamente il certificato. |
   | Certificato gestito dal cliente | Seleziona se desideri utilizzare un certificato EV/OV. Questa opzione offre una protezione avanzata con EV (convalida estesa) o OV (convalida organizzazione). Da utilizzare se è necessaria una verifica più rigorosa, livelli di attendibilità più elevati o un controllo personalizzato dei certificati. |

1. Nella finestra di dialogo **Verifica dominio**, in base al tipo di certificato selezionato, eseguire una delle operazioni seguenti:

   | Se hai selezionato il tipo di certificato | Descrizione |
   | --- | ---  |
   | Certificato gestito da Adobe | Completa i [passaggi Adobi del certificato gestito](#abobe-managed-cert-steps) prima di procedere al passaggio successivo. |
   | Certificato gestito dal cliente | Completa i [passaggi del certificato gestito dal cliente](#customer-managed-cert-steps) prima di procedere al passaggio successivo. |

1. Fare clic su **Verifica**.

1. Ora puoi [aggiungere un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

   >[!NOTE]
   >
   >Se utilizzi un certificato SSL gestito autonomamente e un provider CDN gestito autonomamente, puoi saltare questo passaggio e passare direttamente a [Aggiungi una configurazione CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) quando è pronto.



### Adobe di passaggi di certificati gestiti {#adobe-managed-cert-steps}

Se hai selezionato il tipo di certificato *Adobe certificato gestito*, completa i passaggi seguenti nella finestra di dialogo **Verifica dominio**.

![Adobe di passaggi del certificato gestito](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

Per verificare il dominio in uso, è necessario aggiungere e verificare un CNAME.

Una volta eseguito il provisioning di un record `CNAME` o A, tutto il traffico Internet del dominio viene indirizzato alla posizione a cui punta. Se non si esegue il provisioning di tale posizione per il servizio del traffico, si verifica un’interruzione. Se non si eseguono test, potrebbero essere riscontrati errori nel contenuto. Questo è il motivo per cui questo passaggio viene sempre eseguito dopo il completamento del test e sei pronto per andare live.

Per configurare queste impostazioni, determinare se è necessario configurare un record apex o `CNAME` per far sì che il nome di dominio personalizzato punti al nome di dominio Cloud Manager. Le sezioni seguenti di questo documento possono essere utili per determinare il tipo di record appropriato per la configurazione DNS.

>[!NOTE]
>
>Ad Adobe, quando si utilizzano certificati DV (convalida del dominio), sono consentiti solo i siti con convalida ACME.

#### Requisiti {#dv-requirements}

Rispetta questi requisiti prima di configurare i record DNS.

* Identifica l’host o il registrar del dominio se non lo conosci già.
* Essere in grado di modificare i record DNS per il dominio dell&#39;organizzazione o contattare la persona appropriata che può farlo.
* È necessario aver già verificato il nome di dominio personalizzato configurato come descritto nel documento [Verifica dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

#### Record CNAME {#cname-record}

Un nome canonico o record CNAME è un tipo di record DNS che associa un nome alias a un nome di dominio reale o canonico. I record CNAME vengono in genere utilizzati per associare un sottodominio come `www.example.com` al dominio che ospita il contenuto del sottodominio.

Accedere al provider di servizi DNS e creare un record `CNAME` per far sì che il nome di dominio personalizzato punti alla destinazione, come indicato nella tabella seguente.

| CNAME | Punto di destinazione dominio personalizzato |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### Record APEX {#apex-record}

Un dominio apex è un dominio personalizzato che non contiene un sottodominio, ad esempio `example.com`. Un dominio APEX è configurato con un record `A`, `ALIAS` o `ANAME` tramite il provider DNS. I domini apex devono puntare a indirizzi IP specifici.

Aggiungi i seguenti `A` record alle impostazioni DNS del dominio tramite il provider di dominio.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`



### Passaggi del certificato gestito dal cliente {#customer-managed-cert-steps}

Se hai selezionato il tipo di certificato *Certificato gestito dal cliente*, completa i passaggi seguenti nella finestra di dialogo **Verifica dominio**.

![Passaggi del certificato gestito dal cliente](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

Per verificare il dominio in uso, è necessario aggiungere e verificare un record TXT.

Un record di testo (noto anche come record TXT) è un tipo di record di risorse nel DNS (Domain Name System). Ti consente di associare testo arbitrario a un nome host. Questo testo potrebbe includere dettagli leggibili, come informazioni sul server o sulla rete.

Cloud Manager utilizza un record TXT specifico per autorizzare un dominio ad essere ospitato in un servizio CDN. Crea un record TXT DNS nella zona che autorizza Cloud Manager a distribuire il servizio CDN con il dominio personalizzato e associalo al servizio back-end. Questa associazione è interamente sotto il tuo controllo e autorizza Cloud Manager a distribuire contenuti dal servizio a un dominio. Tale autorizzazione può essere concessa e revocata. Il record TXT è specifico del dominio e dell’ambiente Cloud Manager.

## Requisiti {#requirements-customer-cert}

Prima di aggiungere un record TXT, è necessario soddisfare questi requisiti.

* Identifica l’host o il registrar del dominio se non lo conosci già.
* Essere in grado di modificare i record DNS per il dominio dell&#39;organizzazione o contattare la persona appropriata che può farlo.
* Innanzitutto, aggiungi un nome di dominio personalizzato come descritto in precedenza in questo articolo.

## Aggiungi un record TXT per la verifica {#verification}

1. Nella finestra di dialogo **Verifica dominio**, Cloud Manager visualizza il nome e il valore TXT da utilizzare per la verifica. Copia questo valore.

1. Accedi al provider di servizi DNS e individua la sezione relativa ai record DNS.

1. Aggiungi `aemverification.[yourdomainname]` come **Nome** del valore e aggiungi il valore TXT esattamente come visualizzato nel campo **Nome dominio**.

   **Esempi di record TXT**

   | Dominio | Nome | Valore TXT |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Copia l’intero valore visualizzato nell’interfaccia utente di Cloud Manager. Questo valore è specifico del dominio e dell’ambiente. Esempio:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Copia l’intero valore visualizzato nell’interfaccia utente di Cloud Manager. Questo valore è specifico del dominio e dell’ambiente. Esempio:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Salva il record TXT nell’host del dominio.

## Verifica record TXT {#verify}

Al termine dell&#39;operazione, è possibile verificare il risultato eseguendo il comando seguente.

```shell
dig _aemverification.[yourdomainname] -t txt
```

Il risultato previsto deve visualizzare il valore TXT fornito nella scheda **Verifica** della finestra di dialogo **Aggiungi nome dominio** dell&#39;interfaccia utente di Cloud Manager.

Se ad esempio il dominio è `example.com`, esegui:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Sono disponibili diversi [strumenti di ricerca DNS](https://www.ultratools.com/tools/dnsLookup). Google DoH può essere utilizzato per cercare voci di record TXT e identificare se il record TXT è mancante o errato.

>[!NOTE]
>
>L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS.
>
>Cloud Manager verifica la proprietà e aggiorna lo stato, che può essere visualizzato nella tabella Impostazioni dominio. Per ulteriori dettagli, vedere [Verifica stato nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->

>[!TIP]
>
>La voce TXT e il CNAME o un record A possono essere impostati simultaneamente sul server DNS di riferimento, risparmiando così tempo.
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


## Aggiungere un nome di dominio personalizzato dalla pagina Ambienti {#adding-cdn-environments}

I passaggi per aggiungere un nome di dominio personalizzato dalla pagina **Ambienti** sono gli stessi di quando [si aggiunge un nome di dominio personalizzato dalla pagina Impostazioni dominio](#adding-cdn-settings), ma il punto di ingresso è diverso. Per aggiungere un nome di dominio personalizzato dalla pagina **Ambienti**, segui la procedura riportata di seguito.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Passare alla pagina dei dettagli **Dettagli ambienti** per l&#39;ambiente di interesse.

   ![Inserimento del nome di dominio nella pagina Dettagli dell’ambiente](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Inserisci il nome di dominio personalizzato nella tabella **Nomi di dominio**.

   1. Inserisci il nome di dominio personalizzato.
   1. Seleziona il certificato SSL associato al nome dall’elenco a discesa.
   1. Fai clic su **+Aggiungi**.

   ![Aggiungi un nome di dominio personalizzato](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. La finestra di dialogo **Aggiungi nome dominio** si apre nella scheda **Nome dominio**. Continua come faresti per [aggiungere un nome di dominio personalizzato dalla pagina Impostazioni dominio](#adding-cdn-settings). —>
