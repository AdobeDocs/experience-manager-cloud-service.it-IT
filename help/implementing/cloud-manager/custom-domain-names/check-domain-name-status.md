---
title: Verifica dello stato del nome di dominio
description: Verifica dello stato del nome di dominio
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 4533cbc689d69cbe126791b4426123f890754507
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Verifica dello stato del nome di dominio {#check-status}

Per determinare se il nome di dominio è stato verificato correttamente, fai clic sull’icona Stato del nome di dominio nella tabella Ambienti della pagina Impostazioni dominio .

>[!NOTE]
>Cloud Manager attiva automaticamente una verifica TXT quando selezioni Salva nel passaggio di verifica della procedura guidata Aggiungi dominio personalizzato . Per le verifiche successive, devi selezionare attivamente il **verifica di nuovo** accanto allo stato .

Cloud Manager verificherà la proprietà del dominio tramite il valore TXT e visualizza uno dei seguenti messaggi di stato:

* **Verifica del dominio non riuscita**
Il valore TXT è mancante o viene rilevato con errori. Segui le istruzioni e riprova. Quando è pronto, è necessario selezionare la 
*verifica di nuovo* accanto allo stato .

* **Verifica del dominio in corso**
Verifica in corso. Questo stato viene generalmente visualizzato dopo aver selezionato 
*verifica di nuovo* accanto allo stato .

* **Verificato, Distribuzione non riuscita**
Verifica TXT riuscita. Tuttavia, la distribuzione CDN non è riuscita. Contatta il tuo rappresentante Adobe.

* **Dominio verificato e distribuito**
Questo stato indica che il nome di dominio personalizzato è pronto per essere utilizzato.
   >[!NOTE]
   >A questo punto, il nome di dominio personalizzato è pronto per il test e deve essere indirizzato al nome di dominio di Cloud Manager. Fai riferimento a [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) per saperne di più.

* **Eliminazione**
Eliminazione del nome di dominio personalizzato in corso.

* **Eliminazione non riuscita**
Eliminazione del nome di dominio personalizzato non riuscita. È necessario riprovare. Fai riferimento a [Eliminazione di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) per saperne di più.


## Configurazioni CDN preesistenti per nomi di dominio personalizzati {#pre-existing-cdn}

I clienti con ambienti che includono configurazioni CDN preesistenti per Elenchi consentiti IP, certificati SSL o nomi di dominio personalizzati visualizzeranno il seguente messaggio nel **ELENCO CONSENTITI IP** e **Ambiente** pagina dei dettagli. Il messaggio visualizzato nell’interfaccia utente scompare dopo la migrazione completa da parte del cliente di tutte le configurazioni di ambiente preesistenti tramite l’interfaccia utente e potrebbero essere necessari 1-2 giorni lavorativi per far scomparire il messaggio.

>[!NOTE]
>Per visualizzare e gestire le configurazioni preesistenti, è necessario aggiungerle tramite l’interfaccia utente. Fai riferimento a [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) per ulteriori dettagli.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
