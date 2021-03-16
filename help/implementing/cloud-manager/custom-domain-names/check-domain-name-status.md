---
title: Verifica dello stato del nome di dominio
description: Verifica dello stato del nome di dominio
translation-type: tm+mt
source-git-commit: dbf64ec2b4b7e5c549ef5942b1c7bd0ca75eb66f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# Controllo dello stato del nome di dominio {#check-status}

Per determinare se il nome di dominio è stato verificato correttamente, fai clic sull’icona Stato del nome di dominio nella tabella Ambienti della pagina Impostazioni dominio .

>[!NOTE]
>Cloud Manager attiva automaticamente una verifica TXT quando selezioni Salva nel passaggio di verifica della procedura guidata Aggiungi dominio personalizzato . Per le verifiche successive, devi selezionare attivamente l&#39;icona **verifica nuovamente** accanto allo stato.

Cloud Manager verificherà la proprietà del dominio tramite il valore TXT e visualizza uno dei seguenti messaggi di stato:

* **Il valore**
FailedTXT della verifica del dominio è mancante o viene rilevato con errori. Segui le istruzioni e riprova. Quando è pronto, è necessario selezionare la 
*verifica* nuovamente accanto allo stato .

* **Verifica del dominio In**
corsoVerifica in corso. Questo stato viene generalmente visualizzato dopo aver selezionato 
*verifica* nuovamente accanto allo stato .

* **Verifica: verifica**
TXT della distribuzione non riuscita. Tuttavia, la distribuzione CDN non è riuscita. Un rappresentante di Adobe verrà informato automaticamente.

* **Dominio verificato e**
distribuitoQuesto stato indica che il nome di dominio personalizzato è pronto per essere utilizzato.
   >[!NOTE]
   >A questo punto, il nome di dominio personalizzato è pronto per il test e deve essere indirizzato al nome di dominio di Cloud Manager. Per ulteriori informazioni, consulta [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) .

* ****
Eliminazione in corso del nome di dominio personalizzato.

* **Eliminazione**
non riuscitaEliminazione del nome di dominio personalizzato non riuscita. È necessario riprovare. Per ulteriori informazioni, consulta [Eliminazione di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) .


## Configurazioni CDN preesistenti per Elenchi consentiti IP {#pre-existing-cdn}

I clienti con ambienti che includono configurazioni CDN preesistenti per Elenchi consentiti IP, certificati SSL o nomi di dominio personalizzati visualizzeranno il seguente messaggio nella pagina dei dettagli **Elenco consentiti IP** e **Ambiente** . Il messaggio visualizzato nell’interfaccia utente scompare dopo la migrazione completa da parte del cliente di tutte le configurazioni di ambiente preesistenti tramite l’interfaccia utente e potrebbero essere necessari 1-2 giorni lavorativi per far scomparire il messaggio.

>[!NOTE]
>Per visualizzare e gestire le configurazioni preesistenti, è necessario aggiungerle tramite l’interfaccia utente. Per ulteriori informazioni, consulta [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) .

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)
