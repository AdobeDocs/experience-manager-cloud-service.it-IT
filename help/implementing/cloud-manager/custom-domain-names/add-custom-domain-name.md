---
title: Aggiunta di un nome di dominio personalizzato
description: Aggiunta di un nome di dominio personalizzato
translation-type: tm+mt
source-git-commit: b6b1ef8f97413dc8bf9b1fa7f355a02bdaeebfd8
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Aggiunta di un nome di dominio personalizzato {#adding-cdn}

Per aggiungere un nome di dominio personalizzato in Cloud Manager, un utente deve essere un proprietario aziendale o un gestore distribuzione.

>[!NOTE]
>Prima di aggiungere un nome di dominio personalizzato, al programma deve essere installato un certificato SSL valido contenente il nome di dominio personalizzato. Per ulteriori informazioni, consulta Installazione di un certificato SSL (INSERT LINK).

È possibile aggiungere un solo nome di dominio alla volta. Tuttavia, gli utenti possono aggiungere caratteri jolly, ad esempio `*.wknd.com` come nome di dominio, e ciò consentirebbe a più sottodomini di essere ospitati con un singolo record TXT.
Ogni ambiente Cloud Manager può ospitare fino a un massimo di 50 domini personalizzati per ambiente.
Lo stesso nome di dominio non può essere utilizzato in più di un ambiente.

## Aggiunta di un nome di dominio personalizzato dalla pagina Impostazioni di dominio {#adding-cdn-settings}

Per aggiungere un nome di dominio personalizzato dalla pagina Impostazioni dominio, effettuate le seguenti operazioni:

1. Dalla pagina Ambienti passare alla pagina Impostazioni dominio.

1. Selezionate Aggiungi nome di dominio personalizzatoVerrà avviata la procedura guidata di aggiunta del nome di dominio personalizzato INSERT IMAGE

1. Immettere il nome di dominio personalizzato. Nota: Non includete &#39;http://&#39;, &#39;https://&#39; o spazi quando entrate nel vostro dominio.

1. Selezionate l’ambiente il cui servizio Pubblica sarà associato al nome del dominio.

1. Selezionate il certificato SSL dall’elenco a discesa e selezionate Continua.

1. Viene visualizzata la schermata Verifica nome dominio per l’ambiente. Per ulteriori informazioni, visitare Aggiungi record TXT. INSERISCI IMMAGINE

Seguite le istruzioni fornite per dimostrare la proprietà del dominio per l’ambiente in uso:

1. Selezionate Continua.
1. La distribuzione CDN richiede un certificato SSL valido e la verifica TXT completata. Questo è indicato dallo stato &quot;Verified and Deployed&quot;.  INSERISCI IMMAGINE
1. Fare clic su Controllo del collegamento INSERT del nome di dominio personalizzato per ulteriori informazioni sui vari stati e su come risolvere il problema.

>[!NOTE]
>La prova DNS può richiedere fino a poche ore per il riconoscimento, a causa dei ritardi di propagazione DNS. Cloud Manager verificherà la proprietà e aggiornerà lo stato visibile nella tabella Impostazioni dominio. Vai a Controllo del collegamento INSERT del nome di dominio per saperne di più.

## Aggiunta di un nome di dominio personalizzato dalla pagina Ambienti {#adding-cdn-environments}

1. Passate alla pagina Dettagli ambiente per l’ambiente di interesse.
1. Utilizzate i campi di input nella parte superiore della tabella Nomi di dominio per inviare il nome di dominio personalizzato, il certificato SSL. Selezionare Aggiungi.
1. Verrà avviata la procedura guidata Aggiungi nome di dominio personalizzato con il nome di ambiente precompilato.
1. Immettere il nome di dominio personalizzato. Nota: Non includete `http://`, `https://`né spazi quando entrate nel dominio. Selezionate Continua.
1. Viene visualizzata la schermata Verifica nome dominio per l’ambiente. Fai clic su Verifica dominio (Aggiungi record TXT) per saperne di più. INSERISCI IMMAGINE

Seguite le istruzioni fornite per dimostrare la proprietà del dominio per l’ambiente in uso:

1. Selezionate Continua.
1. La distribuzione CDN richiede un certificato SSL valido e la verifica TXT completata. Questo è indicato dallo stato &quot;Verified and Deployed&quot;.

A questo punto, il vostro nome di dominio personalizzato è pronto per essere testato e `CNAME` puntato. Vai a Stato nome dominio per saperne di più sui vari stati e su come risolvere il problema.

>[!NOTE]
>La prova DNS può richiedere fino a poche ore per il riconoscimento, a causa dei ritardi di propagazione DNS. Cloud Manager verificherà la proprietà e aggiornerà lo stato visibile nella tabella Impostazioni dominio. Vai a Controllo del collegamento INSERT del nome di dominio per saperne di più.
