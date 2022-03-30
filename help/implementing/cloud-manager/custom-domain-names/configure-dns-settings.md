---
title: 'Configurazione delle impostazioni DNS '
description: Configurazione delle impostazioni DNS
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 60b496024b3d012033309632999851c08f43c5d7
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# Configurazione delle impostazioni DNS {#configure-dns}

Dopo aver verificato e distribuito correttamente il nome di dominio personalizzato, puoi aggiornare i record DNS per il nome di dominio personalizzato con il provider DNS. In questo modo il tuo sito potrà essere utilizzato dai visitatori. Pertanto, questa attività viene generalmente eseguita prima di diventare attiva.

## Cosa sono le impostazioni DNS? {#dns-settings}

A `CNAME` o Un record, una volta eseguito il provisioning, indirizza tutto il traffico Internet per il dominio a ovunque esso punti. Se tale posizione non è fornita per il servizio del traffico, si verificherà un’interruzione. Se non è stato testato, potrebbero esserci errori nel contenuto. Questo è il motivo per cui questo passaggio viene sempre fatto dopo il completamento del test e sei pronto per andare in diretta.

Per configurare queste impostazioni, è necessario determinare se `CNAME` Per puntare il nome di dominio personalizzato al nome di dominio Cloud Manager, è necessario configurare il record o Apex. Le sezioni seguenti ti aiuteranno a determinare quale tipo di record è appropriato per la configurazione DNS.

>[!NOTE]
>
>L’utente o l’utente dell’organizzazione deve essere in grado di accedere o contattare il provider DNS (l’azienda da cui hai acquistato il dominio) e di eseguire aggiornamenti nelle impostazioni DNS.

## Record CNAME {#cname-record}

Un nome canonico o un record CNAME è un tipo di record DNS che mappa un nome alias a un nome di dominio vero o canonico. I record CNAME vengono in genere utilizzati per mappare un sottodominio come `www.example.com` al dominio che ospita il contenuto del sottodominio.

Accedi al tuo registrar di dominio e crea un `CNAME` record per puntare il nome di dominio personalizzato alla destinazione, ad esempio nella tabella seguente.

| CNAME | Nome di dominio personalizzato Punto di destinazione |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Record APEX {#apex-record}

Un dominio apex è un dominio personalizzato che non contiene un sottodominio, ad esempio `example.com`. Un dominio apex è configurato con un `A` , `ALIAS` oppure `ANAME` registra tramite il provider DNS. I domini Apex devono puntare a indirizzi IP specifici.

Aggiungi tutti i seguenti elementi `A` registra le impostazioni DNS del dominio tramite il provider di dominio.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
