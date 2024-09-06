---
title: Configurazione delle impostazioni DNS
description: Scopri come configurare le impostazioni DNS per i nomi di dominio personalizzati consente al sito di servire i visitatori.
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 49%

---


# Configurazione delle impostazioni DNS {#configure-dns}

Dopo la verifica e la distribuzione del nome di dominio personalizzato [,](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) è possibile aggiornare i record DNS del nome di dominio personalizzato con il provider DNS. In questo modo il sito diventa disponibile per gli utenti. Pertanto, questa attività viene generalmente eseguita prima della pubblicazione.

## Cosa sono le impostazioni DNS? {#dns-settings}

Una volta eseguito il provisioning di un record `CNAME` o A, tutto il traffico Internet del dominio verrà indirizzato alla posizione a cui punta. Se non si esegue il provisioning di tale posizione per il servizio del traffico, si verifica un’interruzione. Se non si eseguono test, potrebbero essere riscontrati errori nel contenuto. Per questo il passaggio viene eseguito sempre dopo il completamento del test, quanto tutto è pronto per la pubblicazione.

Per configurare queste impostazioni, è necessario determinare se è necessario configurare un record `CNAME` o apex affinché il nome di dominio personalizzato punti al nome di dominio Cloud Manager. Le sezioni seguenti di questo documento ti aiuteranno a determinare quale tipo di record è appropriato per la configurazione DNS.

## Requisiti {#requirements}

È necessario soddisfare questi requisiti prima di configurare i record DNS.

* Se non disponi ancora di questa informazione, identifica l’host o il registrar del dominio.
* È necessario essere in grado di modificare i record DNS per il dominio dell&#39;organizzazione o di contattare la persona appropriata che può farlo.
* È necessario aver già verificato il nome di dominio personalizzato configurato come descritto nel documento [Verifica dello stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Record CNAME {#cname-record}

Un nome canonico o record CNAME è un tipo di record DNS che associa un nome alias a un nome di dominio reale o canonico. I record CNAME vengono in genere utilizzati per associare un sottodominio come `www.example.com` al dominio che ospita il contenuto del sottodominio.

Accedi al tuo registrar di dominio e crea un record `CNAME` per far sì che il nome di dominio personalizzato punti alla destinazione, come indicato nella tabella seguente.

| CNAME | Punto di Target del nome di dominio personalizzato |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Record APEX {#apex-record}

Un dominio apex è un dominio personalizzato che non contiene un sottodominio, ad esempio `example.com`. Un dominio apex è configurato con un record `A`, `ALIAS` o `ANAME` tramite il provider DNS. I domini apex devono puntare a indirizzi IP specifici.

Aggiungi i seguenti `A` record alle impostazioni DNS del dominio tramite il provider di dominio.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## Passaggi successivi {#next-steps}

Dopo aver configurato i record DNS per il nome di dominio personalizzato, sarà necessario verificare tali impostazioni in Cloud Manager. Procedi al documento [Verifica dello stato del record DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) per finalizzare il nome di dominio personalizzato.
