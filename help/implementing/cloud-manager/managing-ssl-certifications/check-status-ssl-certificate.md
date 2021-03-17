---
title: Controllo dello stato di un certificato SSL - Gestione dei certificati SSL
description: Controllo dello stato di un certificato SSL - Gestione dei certificati SSL
translation-type: tm+mt
source-git-commit: e99c8552e2afff677c08c859dd1044287053a40e
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Verifica dello stato di un certificato SSL {#checking-status-an-ssl-certificate}

Lo stato dei certificati SSL può essere compreso immediatamente dalla pagina del certificato SSL.

Puoi identificare lo stato di un certificato SSL dai seguenti schemi di colore:

* ****
VerdeIndica che il certificato è valido per almeno 60 giorni nel futuro.

* ****
OrangeIndica che il certificato scade tra meno di 60 giorni. È ora di verificare di avere un piano per rinnovare il certificato e sostituirlo tramite l’interfaccia utente di Cloud Manager al fine di evitare possibili accessi o interruzioni del sito. Cloud Manager invia notifiche regolari nell’interfaccia utente per avvisarti della scadenza imminente del certificato.

* ****
RossoIndica che, nonostante più notifiche, il certificato SSL è scaduto.

## Configurazioni CDN preesistenti per Elenchi consentiti IP {#pre-existing-cdn}

I clienti con ambienti che includono configurazioni CDN preesistenti per Elenchi consentiti IP, certificati SSL o nomi di dominio personalizzati visualizzeranno il seguente messaggio nella pagina dei dettagli **Elenco consentiti IP** e **Ambiente** . Il messaggio visualizzato nell’interfaccia utente scompare dopo la migrazione completa da parte del cliente di tutte le configurazioni di ambiente preesistenti tramite l’interfaccia utente e potrebbero essere necessari 1-2 giorni lavorativi per far scomparire il messaggio.

>[!NOTE]
>Per visualizzare e gestire le configurazioni preesistenti, è necessario aggiungerle tramite l’interfaccia utente. Per ulteriori informazioni, consulta [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) .

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)