---
title: Controllo dello stato di un certificato SSL - Gestione dei certificati SSL
description: Controllo dello stato di un certificato SSL - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: 295519e8969daec256e5007357b179a30a7932ce
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Verifica dello stato di un certificato SSL {#checking-status-an-ssl-certificate}

Lo stato dei certificati SSL può essere compreso rapidamente dalla pagina del certificato SSL o dalla pagina dei dettagli Ambiente.

Potete identificare lo stato di un certificato SSL utilizzando i seguenti schemi di colori:

* **Verde** Indica che il certificato è valido per almeno 60 giorni nel futuro.

* **Arancione** Indica che il certificato scade entro 60 giorni. È ora di verificare di disporre di un piano per rinnovare il certificato e sostituirlo tramite l&#39;interfaccia utente di Cloud Manager, al fine di evitare possibili accessi o interruzioni del sito. Cloud Manager invierà notifiche regolari nell&#39;interfaccia utente per avvisarvi della scadenza imminente del certificato.

* **Rosso** Indica che, nonostante più notifiche, il certificato SSL è scaduto.