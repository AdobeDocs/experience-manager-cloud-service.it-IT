---
title: Aggiungere un nome di dominio personalizzato
description: Scopri come aggiungere un nome di dominio personalizzato utilizzando Impostazioni dominio in Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ff8c7fb21b4d8bcf395d28c194a7351281eef45b
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 17%

---


# Aggiungere un nome di dominio personalizzato {#adding-cdn}

Scopri come aggiungere un nome di dominio personalizzato utilizzando **Impostazioni dominio** in Cloud Manager.

## Requisiti {#requirements}

Prima di aggiungere un nome di dominio personalizzato in Cloud Manager, è necessario soddisfare questi requisiti.

* È necessario aggiungere un certificato SSL di dominio per il dominio che si desidera aggiungere prima di aggiungere un nome di dominio personalizzato come descritto nel documento [Aggiungere un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Per aggiungere un nome di dominio personalizzato in Cloud Manager è necessario avere il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione**.
* Utilizza la rete CDN (Content Delivery Network) Fastly o di altro tipo.

>[!IMPORTANT]
>
>Anche se utilizzi una rete CDN non Adobe, devi comunque aggiungere il dominio a Cloud Manager.

## Dove aggiungere nomi di dominio personalizzati {#where-to-add-cdn}

In Cloud Manager è possibile aggiungere un nome di dominio personalizzato dalle due posizioni seguenti:

* [Pagina Impostazioni dominio](#adding-cdn-settings)
* [Pagina Ambienti](#adding-cdn-environments)

Quando si aggiunge un nome di dominio personalizzato, il dominio viene gestito utilizzando il certificato valido più specifico. Se più certificati hanno lo stesso dominio, viene scelto quello aggiornato più di recente. L’Adobe consiglia di gestire i certificati in modo che non vi siano domini sovrapposti.

I passaggi per entrambi i metodi descritti in questo documento si basano su Fastly. Se utilizzi una rete CDN (Content Delivery Network) diversa, configura il dominio con la rete CDN che hai scelto di utilizzare.

## Aggiungere un nome di dominio personalizzato {#adding-cdn-settings}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nel menu laterale, in **Servizi**, selezionare ![Icona Impostazioni](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) **Impostazioni dominio**.

   ![Finestra Impostazioni dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Nell&#39;angolo superiore destro della pagina **Impostazioni dominio** fare clic su **Aggiungi dominio**.

1. Nella finestra di dialogo **Aggiungi dominio** immettere il nome di dominio personalizzato in uso nel campo **Nome dominio**.
Non includere `http://`, `https://` o spazi durante l’inserimento del dominio.

1. Fai clic su **Crea**.

1. Nella finestra di dialogo **Verifica dominio**, in **Quale tipo di certificato intendi utilizzare con questo dominio?Elenco a discesa**, selezionare una delle opzioni seguenti:

   | Opzione tipo di certificato | Descrizione |
   | --- | --- |
   | Certificato gestito da Adobe | Selezionare questo tipo di certificato se si desidera utilizzare un certificato DV (convalida dominio). Questa opzione è ideale per la maggior parte dei casi e fornisce la convalida di base del dominio. Adobe gestisce e rinnova automaticamente il certificato. |
   | Certificato gestito dal cliente | Selezionare questo tipo di certificato per utilizzare un certificato EV/OV. Questa opzione offre una protezione avanzata con EV (convalida estesa) o OV (convalida organizzazione). Da utilizzare se è necessaria una verifica più rigorosa, livelli di attendibilità più elevati o un controllo personalizzato dei certificati. |

1. Nella finestra di dialogo **Verifica dominio**, in base al tipo di certificato selezionato, eseguire una delle operazioni seguenti:

   | Se hai selezionato il tipo di certificato | Descrizione |
   | --- | ---  |
   | Certificato gestito da Adobe | Completa i [passaggi Adobi del certificato gestito](#adobe-managed-cert-steps) prima di continuare con il passaggio 9. |
   | Certificato gestito dal cliente | Completa i [passaggi del certificato gestito dal cliente](#customer-managed-cert-steps) prima di continuare con il passaggio 9. |

1. Fare clic su **Verifica**.

1. Ora puoi [aggiungere un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

   >[!NOTE]
   >
   >Se utilizzi un certificato SSL gestito dal cliente e un provider CDN gestito dal cliente, puoi saltare l&#39;aggiunta di un certificato SSL e passare direttamente a [Aggiungi una configurazione CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) quando è pronto.


### Adobe di passaggi di certificati gestiti {#adobe-managed-cert-steps}

Se hai selezionato il tipo di certificato *Adobe certificato gestito*, completa i passaggi seguenti nella finestra di dialogo **Verifica dominio**.

![Adobe di passaggi del certificato gestito](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

Per verificare il dominio in uso, è necessario aggiungere e verificare un CNAME.

Una volta eseguito il provisioning di un record `CNAME` o A, tutto il traffico Internet del dominio viene indirizzato alla posizione a cui punta. Se non si esegue il provisioning di tale posizione per il servizio del traffico, si verifica un’interruzione. Se non si eseguono test, potrebbero essere riscontrati errori nel contenuto. Questo è il motivo per cui questo passaggio viene sempre eseguito dopo il completamento del test e sei pronto per andare live.

Per configurare queste impostazioni, determinare se è necessario configurare un record apex o `CNAME` per far sì che il nome di dominio personalizzato punti al nome di dominio Cloud Manager. Le sezioni seguenti di questo documento possono essere utili per determinare il tipo di record appropriato per la configurazione DNS.

>[!NOTE]
>
>Ad Adobe, quando si utilizzano certificati DV (convalida del dominio), sono consentiti solo i siti con convalida ACME.

#### Requisiti {#adobe-managed-cert-dv-requirements}

Rispetta questi requisiti prima di configurare i record DNS.

* Identifica l’host o il registrar del dominio se non lo conosci già.
* Essere in grado di modificare i record DNS per il dominio dell&#39;organizzazione o contattare la persona appropriata che può farlo.
* È necessario aver già verificato il nome di dominio personalizzato configurato come descritto nel documento [Verifica dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

#### Record CNAME {#adobe-managed-cert-cname-record}

Un nome canonico o record CNAME è un tipo di record DNS che associa un nome alias a un nome di dominio reale o canonico. I record CNAME vengono in genere utilizzati per associare un sottodominio come `www.example.com` al dominio che ospita il contenuto del sottodominio.

Accedere al provider di servizi DNS e creare un record `CNAME` per far sì che il nome di dominio personalizzato punti alla destinazione, come indicato nella tabella seguente.

| CNAME | Punto di destinazione dominio personalizzato |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### Record APEX {#adobe-managed-cert-apex-record}

Un dominio apex è un dominio personalizzato che non contiene un sottodominio, ad esempio `example.com`. Un dominio APEX è configurato con un record `A`, `ALIAS` o `ANAME` tramite il provider DNS. I domini apex devono puntare a indirizzi IP specifici.

Aggiungi i seguenti `A` record alle impostazioni DNS del dominio tramite il provider di dominio.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

>[!TIP]
>
>È possibile impostare *CNAME* o *Un record* nel server DNS che gestisce per risparmiare tempo.


### Passaggi del certificato gestito dal cliente {#customer-managed-cert-steps}

Se hai selezionato il tipo di certificato *Certificato gestito dal cliente*, completa i passaggi seguenti.

1. Nella finestra di dialogo **Verifica dominio**, carica un nuovo certificato EV/OV relativo al dominio selezionato.

   ![Verificare il dominio per un certificato EV/OV gestito dal cliente](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png)

1. Fai clic su **OK**.

   Dopo aver caricato un certificato EV/OV valido, lo stato del dominio viene contrassegnato come **Verificato** nella tabella **Impostazioni dominio**.

   ![Tabella delle impostazioni di dominio che mostra uno stato verificato.](/help/implementing/cloud-manager/assets/domain-settings-verified.png)

<!--
![Customer managed certificate steps](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

To verify the domain in use, you are required to add and verify a TXT record.

A text record (also known as a TXT record) is a type of resource record in the Domain Name System (DNS). It lets you associate arbitrary text with a hostname. This text could include human-readable details like server or network information.

Cloud Manager uses a specific TXT record to authorize a domain to be hosted in a CDN service. Create a DNS TXT record in the zone that authorizes Cloud Manager to deploy the CDN service with the custom domain and associate it with the backend service. This association is entirely under your control and authorizes Cloud Manager to serve content from the service to a domain. This authorization may be granted and withdrawn. The TXT record is specific to the domain and the Cloud Manager environment.

#### Requirements {#customer-managed-cert-requirements}

Fulfill these requirements before adding a TXT record.

* Identify your domain host or registrar if you do not know it already.
* Be able to edit the DNS records for your organization's domain, or contact the appropriate person who can.
* First, add a custom domain name as described earlier in this article.

#### Add a TXT record for verification {#customer-managed-cert-verification}

1. In the **Verify domain** dialog box, Cloud Manager displays the name and TXT value to use for verification. Copy this value.

1. Log in to your DNS service provider and find the DNS records section. 

1. Add `aemverification.[yourdomainname]` as the **Name** of the value and add the TXT value exactly as it appears in the **Domain Name** field.

   **TXT record examples**

   | Domain | Name | TXT Value |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Save the TXT record to your domain host.

#### Verify TXT record {#customer-managed-cert-verify}

When you are done, you can verify the result by running the following command.

```shell
dig _aemverification.[yourdomainname] -t txt
```

The expected result should display the TXT value provided on the **Verification** tab of the **Add Domain Name** dialog of the Cloud Manager UI.

For example, if your domain is `example.com`, then run:

```shell
dig TXT _aemverification.example.com -t txt
```


>[!TIP]
>
>There are several [DNS lookup tools](https://www.ultratools.com/tools/dnsLookup) available. Google DoH can be used to look up TXT record entries and identify if the TXT record is missing or erroneous.

-->

>[!NOTE]
>
>L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS.
>
>Cloud Manager verifica la proprietà e aggiorna lo stato, che può essere visualizzato nella tabella **Impostazioni dominio**. Per ulteriori dettagli, vedere [Verifica stato nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->


><!-- The TXT entry and the CNAME or A Record can be set simultaneously on the governing DNS server, thus saving time. -->
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->

