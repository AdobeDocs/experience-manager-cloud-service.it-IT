---
title: 'Configurazione delle impostazioni DNS '
description: Configurazione delle impostazioni DNS
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Configurazione delle impostazioni DNS {#configure-dns}

Dopo aver verificato e distribuito correttamente il nome di dominio personalizzato, è possibile aggiornare i record DNS per il nome di dominio personalizzato con il provider DNS. In questo modo il sito potrà servire ai visitatori. Di conseguenza, questa attività viene in genere eseguita prima di Go-live.

>[!NOTE]
>L&#39;utente o l&#39;utente dell&#39;organizzazione deve essere in grado di accedere o contattare il provider DNS (la società da cui hai acquistato il dominio) e di effettuare aggiornamenti nelle impostazioni DNS.

A tal fine, devi determinare se devi configurare le impostazioni DNS su un record `CNAME` o Apex che punta il nome di dominio personalizzato al nome di dominio di Cloud Manager. Un record `CNAME` o A, una volta effettuato il provisioning, indirizza tutto il traffico Internet per il dominio a ovunque esso stia puntando. Se la posizione non è predisposta per il traffico, si verificherà un&#39;interruzione. Se non è stato testato, potrebbero verificarsi errori nel contenuto. Questo è il motivo per cui questo passaggio viene sempre fatto dopo che il test è completo e il cliente è pronto per il Go-live.

## Record CNAME {#cname-record}

Le sezioni seguenti consentono di determinare quale tipo di record è appropriato per la configurazione DNS.

Un record di nome canonico o `CNAME` è un tipo di record DNS che mappa un nome alias a un nome di dominio vero o canonico. I record CNAME vengono generalmente utilizzati per mappare un sottodominio, ad esempio `www.example.com`, al dominio che ospita il contenuto del sottodominio.

Accedi al Registratore di dominio e crea un record CNAME per indirizzare il nome di dominio personalizzato alla destinazione come mostrato di seguito:

| CNAME | Nome di dominio personalizzato point to Target |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## Record APEX {#apex-record}

Un dominio apex è un dominio personalizzato che non contiene un sottodominio, ad esempio example.com. Un dominio apex è configurato con un record `A`, `ALIAS` o `ANAME` tramite il provider DNS. I domini Apex devono puntare a indirizzi IP specifici.

Aggiungi tutti i seguenti record A alle impostazioni DNS del dominio tramite il provider di dominio:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
