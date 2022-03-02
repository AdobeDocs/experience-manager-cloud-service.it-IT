---
title: 'Configurazione delle impostazioni DNS '
description: Configurazione delle impostazioni DNS
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 016954bc712a135886a6031deba05d92e7d5099c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 6%

---

# Configurazione delle impostazioni DNS {#configure-dns}

Dopo aver verificato e distribuito correttamente il nome di dominio personalizzato, puoi aggiornare i record DNS per il nome di dominio personalizzato con il provider DNS. In questo modo il tuo sito potrà essere utilizzato dai visitatori. Pertanto, questa attività viene generalmente eseguita prima del lancio.

>[!NOTE]
>L’utente o l’utente dell’organizzazione deve essere in grado di accedere o contattare il provider DNS (l’azienda da cui hai acquistato il dominio) e di eseguire aggiornamenti nelle impostazioni DNS.

A questo scopo, è necessario determinare se è necessario configurare le impostazioni DNS in un `CNAME` o record Apex che punta il nome di dominio personalizzato al nome di dominio Cloud Manager. A `CNAME` o Un record, una volta eseguito il provisioning, indirizza tutto il traffico Internet per il dominio a ovunque esso punti. Se tale posizione non è fornita per il servizio del traffico, si verificherà un’interruzione. Se non è stato testato, potrebbero esserci errori nel contenuto. Questo è il motivo per cui questo passaggio viene sempre fatto dopo il completamento del test e il cliente è pronto per il lancio.

I seguenti passaggi devono essere completati come indicato nella tabella seguente:

| Incremento |  | Responsabilità | Ulteriori informazioni |
|--- |--- |--- |---|
| Aggiungi certificato SSL | Aggiungi certificato SSL | Cliente | [Aggiunta di un certificato SSL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| Verifica del dominio | Aggiungi record TXT | Cliente | [Aggiunta di un record TXT](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| Verifica stato di verifica del dominio |  | Cliente |  |
|  | Stato: Errore di verifica del dominio | Cliente | [Verifica dello stato del nome di dominio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | Stato: Verificato, Distribuzione non riuscita | Contatta il rappresentante Adobe | [Verifica dello stato del nome di dominio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| Aggiungi record DNS che puntano a AEM as a Cloud Service aggiungendo record CNAME o APEX | Configurare le impostazioni DNS | Cliente | [Configurazione delle impostazioni DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| Verifica lo stato del record DNS |  | Cliente | [Verifica dello stato del record DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Stato: Stato DNS non rilevato | Cliente | [Verifica dello stato del record DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Stato: Il DNS viene risolto in modo errato | Cliente |  |


## Record CNAME {#cname-record}

Le sezioni seguenti ti aiuteranno a determinare quale tipo di record è appropriato per la configurazione DNS.

Un nome canonico o `CNAME` record è un tipo di record DNS che associa un nome alias a un nome di dominio vero o canonico. I record CNAME vengono in genere utilizzati per mappare un sottodominio come `www.example.com`  al dominio che ospita il contenuto del sottodominio.

Accedi al Registratore di dominio e crea un record CNAME per puntare il nome di dominio personalizzato alla destinazione come mostrato di seguito:

| CNAME | Nome di dominio personalizzato Punto di destinazione |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## Record APEX {#apex-record}

Un dominio apex è un dominio personalizzato che non contiene un sottodominio, ad esempio example.com. Un dominio apex è configurato con un `A` , `ALIAS` oppure `ANAME` registra tramite il provider DNS. I domini Apex devono puntare a indirizzi IP specifici.

Aggiungi tutti i seguenti record A alle impostazioni DNS del dominio tramite il provider di dominio:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
