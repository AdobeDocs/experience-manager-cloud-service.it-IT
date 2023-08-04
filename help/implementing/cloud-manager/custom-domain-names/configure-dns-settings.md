---
title: Configurazione delle impostazioni DNS
description: Scopri come configurare le impostazioni DNS per i nomi di dominio personalizzati.
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 9fd7c17fce8c11809eabcc6387cbace0ebdc64a2
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 84%

---

# Configurazione delle impostazioni DNS {#configure-dns}

Dopo aver verificato e distribuito correttamente il nome di dominio personalizzato, è possibile aggiornare il relativo record DNS con il provider DNS. In questo modo il sito diventa disponibile per gli utenti. Pertanto, questa attività viene generalmente eseguita prima della pubblicazione.

## Cosa sono le impostazioni DNS? {#dns-settings}

Dopo aver eseguito il provisioning di un record `CNAME` o A, tutto il traffico Internet del dominio viene indirizzato alla posizione a cui punta. Se non viene eseguito il provisioning di tale posizione per il servizio del traffico, si verifica un’interruzione. Se non si eseguono test, potrebbero essere riscontrati errori nel contenuto. Per questo il passaggio viene eseguito sempre dopo il completamento del test, quanto tutto è pronto per la pubblicazione.

Per configurare queste impostazioni, è necessario determinare se `CNAME` o Il record Apex deve essere configurato in modo che il nome di dominio personalizzato punti al nome di dominio di Cloud Manager. Le sezioni riportate di seguito aiutano a determinare il tipo di record appropriato per la configurazione DNS in uso.

>[!NOTE]
>
>Chi svolge l’operazione deve essere in grado di accedere al provider DNS (l’azienda da cui hai acquistato il dominio) o di contattarlo, nonché di apportare gli aggiornamenti alle impostazioni DNS.

## Record CNAME {#cname-record}

Un nome canonico o record CNAME è un tipo di record DNS che associa un nome alias a un nome di dominio reale o canonico. I record CNAME vengono in genere utilizzati per associare un sottodominio come `www.example.com` al dominio che ospita il contenuto del sottodominio.

Accedi al tuo registrar di dominio e crea un record `CNAME` per far sì che il nome di dominio personalizzato punti alla destinazione, come indicato nella tabella seguente.

| CNAME | Punto di Target del nome di dominio personalizzato |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Record APEX {#apex-record}

Un dominio apex è un dominio personalizzato che non contiene un sottodominio, ad esempio `example.com`. Un dominio apex è configurato con un record `A`, `ALIAS` o `ANAME` tramite il provider DNS. I domini apex devono puntare a indirizzi IP specifici.

Aggiungi tutti i seguenti record `A` alle impostazioni DNS del dominio tramite il provider di dominio.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
