---
title: Aggiungere una mappatura di dominio
description: Scopri come aggiungere una mappatura di dominio per un sito Edge Delivery o un ambiente Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 7%

---


# Informazioni sull’aggiunta di una mappatura di dominio {#add-domain-mapping}

Per collegare un dominio con un certificato SSL sulla rete CDN gestita da Adobe all’interno del programma, è necessario aggiungere una configurazione CDN (Content Delivery Network).

Per le CDN gestite da Adobe, quando si utilizza un certificato SSL DV, sono consentiti solo i siti con convalida ACME.

>[!IMPORTANT]
>
>Hai [aggiunto un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) e [aggiunto rispettivamente un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)? In caso contrario, è necessario completare queste due attività prima di poter aggiungere una configurazione CDN.

Vedi anche [CDN gestito da Adobe](https://www.aem.live/docs/byo-cdn-adobe-managed).

**Per aggiungere un mapping di dominio:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. A seconda del caso d’uso, effettua una delle seguenti operazioni:

   | Caso d’uso | Passaggi |
   | --- | --- |
   | Desidero aggiungere una configurazione CDN a un sito Edge Delivery *esistente* in Cloud Manager | a. Nel menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Pagine Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Siti Edge Delivery**.<br> b. Nella tabella di Edge Delivery, alla fine di una riga a cui non è associato un dominio, fare clic su ![Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).<br>c. Fare clic su **Configura rete CDN**. |
   | Desidero aggiungere una configurazione CDN in Cloud Manager | a. Nel menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Social network](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mappature dominio**.<br> b. Fare clic su **Aggiungi** nell&#39;angolo superiore destro della pagina Mapping domini. |

1. Nella finestra di dialogo **Mappa dominio a CDN**, seleziona il tipo di CDN e la configurazione associata selezionando una delle opzioni seguenti:

   | Tipo CDN | Dettagli configurazione |
   | --- | --- |
   | CDN gestito da Adobe (scelta consigliata) | In **Dettagli configurazione** eseguire le operazioni seguenti:<br>a. Nell&#39;elenco a discesa **Dominio** selezionare il nome di dominio che si desidera utilizzare.<br>Nessun dominio verificato disponibile nell&#39;elenco a discesa? Consulta [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).<br>b.<!-- In the **SSL certificate** drop-down list, select a certificate that you want to use.<br>No SSL certificates available in the drop-down list? See [Add an SSL certificate](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).--> |
   | Altro provider CDN | Seleziona questa opzione se utilizzi un provider CDN personalizzato e non la rete CDN gestita di Adobe disponibile.<br>In **Dettagli configurazione**, nell&#39;elenco a discesa **Dominio**, selezionare il nome di dominio che si desidera utilizzare.<br>Nessun dominio verificato disponibile nell&#39;elenco a discesa? Consulta [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |

   ![Finestra di dialogo Mappa dominio su CDN con il pulsante di opzione CDN gestito da Adobe selezionato](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png)

   <!-- OLD IMAGE/UI (/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)-->

1. Nel campo **Dominio**, immetti il nome host rivolto al cliente che desideri fornire (ad esempio, `www.example.com`)
1. nell&#39;elenco a discesa **Origin** selezionare una delle opzioni seguenti:

   | Elenco a discesa Origine | Descrizione |
   | --- | --- |
   | Sites | Seleziona un sito Edge Delivery. |
   | Ambiente | Seleziona un ambiente Cloud Service specifico di cui desideri eseguire il targeting nella configurazione di AEM.<br>Nell&#39;elenco a discesa **Livello**, selezionare una delle opzioni seguenti:<br>· Selezionare **Pubblica** per eseguire il targeting di un ambiente di produzione live in cui il contenuto viene distribuito agli utenti finali.<br>· Selezionare **Anteprima** per gli ambienti di staging o non di produzione in cui si esegue il test delle modifiche prima che vengano pubblicate. |

1. Fare clic su **Salva configurazione**.

   Adobe consiglia di testare la mappatura del dominio.

## Testare la mappatura del dominio {#test-domain-mapping}

Puoi verificare che un nuovo mapping di dominio sia attivo sulla rete CDN gestita da Adobe senza attendere la propagazione del DNS pubblico.

Esegui un comando **curl** che esegue l&#39;override della risoluzione DNS e punta direttamente al server Edge CDN:

```bash
curl -svo /dev/null https://www.example.com \
--resolve www.example.com:443:151.101.3.10
```

* Sostituisci `www.example.com` con il tuo dominio.
* L&#39;indirizzo IP `151.101.3.10` è uno degli IP che è possibile utilizzare per accedere ad AEM Cloud Service. Vedere anche [record APEX](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-apex-record).

Il flag `--resolve` forza la richiesta all&#39;IP specificato e restituisce l&#39;esito positivo solo dopo che il certificato e il routing per il dominio sono stati installati correttamente.

