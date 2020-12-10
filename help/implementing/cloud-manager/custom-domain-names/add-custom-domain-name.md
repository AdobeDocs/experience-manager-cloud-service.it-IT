---
title: Aggiunta di un nome di dominio personalizzato
description: Aggiunta di un nome di dominio personalizzato
translation-type: tm+mt
source-git-commit: 9d5f7d633ac8dfaadf315e85666479c87a0afa04
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# Aggiunta di un nome di dominio personalizzato {#adding-cdn}

Per aggiungere un nome di dominio personalizzato in Cloud Manager, un utente deve essere un proprietario aziendale o un gestore distribuzione.

## Considerazioni importanti {#important-considerations}

* Prima di aggiungere un nome di dominio personalizzato, al programma deve essere installato un certificato SSL valido contenente il nome di dominio personalizzato. Per ulteriori informazioni, fare riferimento a [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

* È possibile aggiungere un solo nome di dominio alla volta. Tuttavia, gli utenti possono aggiungere caratteri jolly, ad esempio `*.wknd.com` come nome di dominio, e ciò consentirebbe a più sottodomini di essere ospitati con un singolo record TXT.

* Ogni ambiente Cloud Manager può ospitare fino a un massimo di 100 domini personalizzati per ambiente. Lo stesso nome di dominio non può essere utilizzato in più di un ambiente.

## Aggiunta di un nome di dominio personalizzato dalla pagina Impostazioni dominio {#adding-cdn-settings}

Per aggiungere un nome di dominio personalizzato dalla pagina Impostazioni dominio, effettuate le seguenti operazioni:

1. Passare alla pagina Impostazioni dominio dalla **Pagina Ambienti**

1. Selezionare **Aggiungi nome di dominio personalizzato** per avviare la procedura guidata di aggiunta del nome di dominio personalizzato.

1. Immettere il nome di dominio personalizzato.

   >[!NOTE]
   >Non includere `http://`, `https://` o spazi durante l&#39;accesso al dominio.

1. Selezionate l’ambiente il cui servizio Pubblica sarà associato al nome del dominio.

1. Selezionate il certificato SSL dall’elenco a discesa e selezionate Continua.

1. Viene visualizzata la schermata Verifica nome dominio per l’ambiente. Per ulteriori informazioni, fare riferimento a [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).
Seguite le istruzioni fornite per dimostrare la proprietà del dominio per l’ambiente in uso.

1. Selezionate Continua.
1. La distribuzione CDN richiede un certificato SSL valido e la verifica TXT completata. Questo è indicato dallo stato **Verified and Deployed**.
1. Passare a Verifica stato nome dominio personalizzato per ulteriori informazioni sui vari stati e su come risolvere il problema.

   >[!NOTE]
   >La prova DNS può richiedere fino a poche ore per il riconoscimento, a causa dei ritardi di propagazione DNS. Cloud Manager verificherà la proprietà e aggiornerà lo stato visibile nella tabella Impostazioni dominio. Per ulteriori informazioni, fare riferimento a Controllo dello stato del nome di dominio.

## Aggiunta di un nome di dominio personalizzato dalla pagina Ambienti {#adding-cdn-environments}

1. Passate alla pagina Dettagli ambiente per l’ambiente di interesse.
1. Utilizzate i campi di input nella parte superiore della tabella Nomi di dominio per inviare il nome di dominio personalizzato, il certificato SSL. Selezionare Aggiungi.
1. Verrà avviata la procedura guidata Aggiungi nome di dominio personalizzato con il nome di ambiente precompilato.
1. Immettere il nome di dominio personalizzato. Nota: Non includete `http://`, `https://` o spazi quando entrate nel vostro dominio. Selezionate Continua.
1. Viene visualizzata la schermata Verifica nome dominio per l’ambiente. Per ulteriori informazioni, fare riferimento a [Verifica del dominio](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md). Seguite le istruzioni fornite per dimostrare la proprietà del dominio per l’ambiente in uso.

1. Selezionate Continua.
1. La distribuzione CDN richiede un certificato SSL valido e la verifica TXT completata. Questo è indicato dallo stato **Verified and Deployed**.

A questo punto, il vostro nome di dominio personalizzato è pronto per essere testato e un `CNAME` per indicarlo. Fare riferimento a Stato nome di dominio per ulteriori informazioni sui vari stati e su come risolvere il problema.

>[!NOTE]
>La prova DNS può richiedere fino a poche ore per il riconoscimento, a causa dei ritardi di propagazione DNS. Cloud Manager verificherà la proprietà e aggiornerà lo stato visibile nella tabella Impostazioni dominio. Per ulteriori informazioni, fare riferimento a Controllo dello stato del nome di dominio.
