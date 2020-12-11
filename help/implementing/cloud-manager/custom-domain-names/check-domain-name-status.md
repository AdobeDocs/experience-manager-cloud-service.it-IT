---
title: Verifica dello stato del nome del dominio
description: Verifica dello stato del nome del dominio
translation-type: tm+mt
source-git-commit: f11cb3b56f51046779300626d1deb037dd687309
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Controllo dello stato del nome di dominio {#check-status}

Per determinare se il nome di dominio è stato verificato correttamente, fai clic sull’icona Stato del nome di dominio nella tabella in Ambienti della pagina Impostazioni dominio.

>[!NOTE]
>Cloud Manager attiva automaticamente una verifica TXT quando selezioni Salva nel passaggio di verifica della procedura guidata Aggiungi dominio personalizzato. Per le verifiche successive, devi selezionare attivamente l&#39;icona **verify again** accanto allo stato.

Cloud Manager verificherà la proprietà del dominio tramite il valore TXT e visualizzerà uno dei seguenti messaggi di stato:

* **Il valore**
FailedTXT per la verifica del dominio risulta mancante o rilevato con errori. Seguite le istruzioni e riprovate. Quando è pronto, è necessario selezionare il pulsante 
*verifica* nuovamente accanto allo stato.

* **Verifica dominio in**
corsoVerifica in corso. Questo stato viene generalmente visualizzato dopo la selezione del 
*verifica* nuovamente accanto allo stato.

* **Verificato: verifica della distribuzione**
non riuscitaTXT. Tuttavia, la distribuzione CDN non è riuscita.  rappresentante del Adobe ne verrà informato automaticamente.

* **Dominio verificato e**
distribuitoQuesto stato indica che il nome di dominio personalizzato è pronto per essere utilizzato.
   >[!NOTE]
   >A questo punto, il tuo nome di dominio personalizzato è pronto per essere testato e punta al nome di dominio di Cloud Manager. Per ulteriori informazioni, fare riferimento a [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md).

* **Eliminazione**
del nome di dominio personalizzato in corso.

* **Eliminazione**
non riuscitaEliminazione del nome di dominio personalizzato non riuscita. È necessario riprovare. Per ulteriori informazioni, fare riferimento a [Eliminazione di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md).

