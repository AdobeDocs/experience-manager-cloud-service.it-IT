---
title: Verifica dello stato del nome del dominio
description: Verifica dello stato del nome del dominio
translation-type: tm+mt
source-git-commit: 91b06bcd96fe8a37c3fb20ef90e1684f6d19183f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Verifica dello stato del nome del dominio {#check-status}

Per determinare se il nome di dominio è stato verificato correttamente, fai clic sull’icona Stato del nome di dominio nella tabella in Ambienti della pagina Impostazioni dominio.

>[!NOTE]
>Cloud Manager attiva automaticamente una verifica TXT quando selezioni Salva nel passaggio di verifica della procedura guidata Aggiungi dominio personalizzato. Per le verifiche successive, devi selezionare attivamente l’icona &quot;verifica di nuovo&quot; accanto allo stato. INSERISCI IMMAGINE

Cloud Manager verificherà la proprietà del dominio tramite il valore TXT e visualizzerà uno dei seguenti messaggi di stato:

* **Verifica del dominio non riuscita** Valore TXT mancante o rilevato con errori. Seguite le istruzioni e riprovate. Quando è pronto, è necessario selezionare l&#39;icona &quot;verifica di nuovo&quot; accanto allo stato.

* **Verifica del dominio in corso**. Verifica in corso. Questo stato viene generalmente visualizzato dopo che avete selezionato l’icona &quot;verifica di nuovo&quot; accanto allo stato.

* **Verificato: verifica della distribuzione non riuscita** TXT. Tuttavia, la distribuzione CDN non è riuscita.  rappresentante del Adobe ne verrà informato automaticamente.

* **Dominio verificato e distribuito** Questo stato indica che il nome di dominio personalizzato è pronto per essere utilizzato. Nota: A questo punto, il tuo nome di dominio personalizzato è pronto per essere testato e punta al nome di dominio di Cloud Manager. Per informazioni su come eseguire questa operazione, vedere Configurazione del collegamento INSERT delle impostazioni DNS.

* **È in corso l&#39;eliminazione** del nome di dominio personalizzato.

* **Eliminazione non riuscita** Eliminazione del nome di dominio personalizzato non riuscita. È necessario riprovare. Per ulteriori informazioni sull&#39;argomento, fare clic su Elimina nome di dominio personalizzato.


## Configurazione delle impostazioni DNS {#configure-dns}

Dopo aver verificato e distribuito correttamente il nome di dominio personalizzato, è possibile aggiornare i record DNS per il nome di dominio personalizzato con il provider DNS. In questo modo il sito potrà servire ai visitatori. Di conseguenza, questa attività viene in genere eseguita prima di Go-live.

>[!NOTE]
>L&#39;utente o l&#39;utente dell&#39;organizzazione deve essere in grado di accedere o contattare il provider DNS (la società da cui hai acquistato il dominio) e di effettuare aggiornamenti nelle impostazioni DNS.

A tal fine, devi determinare se devi configurare le impostazioni DNS su un record `CNAME` o Apex che punta il tuo nome di dominio personalizzato al nome di dominio di Cloud Manager. Un record `CNAME` o A, una volta effettuato il provisioning, indirizza tutto il traffico Internet del dominio a ovunque esso sia puntato. Se la posizione non è predisposta per il traffico, si verificherà un&#39;interruzione. Se non è stato testato, potrebbero verificarsi errori nel contenuto. Questo è il motivo per cui questo passaggio viene sempre fatto dopo che il test è completo e il cliente è pronto per il Go-live.

### Record CNAME {#cname-record}

Le sezioni seguenti consentono di determinare quale tipo di record è appropriato per la configurazione DNS.

Un nome o `CNAME` record canonico è un tipo di record DNS che mappa un nome alias a un nome di dominio vero o canonico. I record CNAME vengono generalmente utilizzati per mappare un sottodominio, ad esempio `www.example.com` al dominio in cui risiede il contenuto del sottodominio.

Accedi al Registratore di dominio e crea un record CNAME per indirizzare il nome di dominio personalizzato alla destinazione come mostrato di seguito:

| CNAME | Nome di dominio personalizzato point to Target |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |
