---
title: Verifica dello stato del nome di dominio
description: Scopri come determinare se il nome di dominio personalizzato è stato verificato correttamente da Cloud Manager.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: cc1b0d653706150c616ceafd002dc7594b6c7072
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Verifica dello stato del nome di dominio {#check-status}

In Cloud Manager puoi determinare lo stato del nome di dominio personalizzato.

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Ambienti** dalla schermata **Panoramica** pagina.

1. Fai clic su **Impostazioni di dominio** nel pannello di navigazione a sinistra.

1. Fai clic sul pulsante **Stato** per il nome di dominio.

Cloud Manager verifica la proprietà del dominio tramite il valore TXT e visualizza uno dei seguenti messaggi di stato.

* **Verifica del dominio non riuscita** - Il valore TXT è mancante o viene rilevato con errori.

   * Segui le istruzioni fornite per risolvere il problema.
   * Quando è pronto, è necessario selezionare la **Verifica di nuovo** accanto allo stato .

* **Verifica del dominio in corso** - La verifica è in corso.

   * Questo stato viene generalmente visualizzato dopo aver selezionato **Verifica di nuovo** accanto allo stato .

* **Verificato, Distribuzione non riuscita** - La verifica TXT ha avuto esito positivo, ma la distribuzione CDN non è riuscita.

   * In questi casi, contatta il tuo rappresentante Adobe.

* **Dominio verificato e distribuito** - Questo stato indica che il nome di dominio personalizzato è pronto per essere utilizzato.

   * A questo punto, il nome di dominio personalizzato è pronto per il test e deve essere indirizzato al nome di dominio di Cloud Manager.
   * Fare riferimento al documento [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) per saperne di più.

* **Eliminazione** - È in corso l&#39;eliminazione di un nome di dominio personalizzato.

* **Eliminazione non riuscita** - L&#39;eliminazione del nome di dominio personalizzato non è riuscita e deve essere ritentata.

   * Fare riferimento al documento [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) per saperne di più.

Cloud Manager attiva automaticamente una verifica TXT quando selezioni **Salva** sulla fase di verifica della **Aggiungi dominio personalizzato** procedura guidata. Per le verifiche successive, devi selezionare attivamente l’icona verifica di nuovo accanto allo stato.

## Configurazioni CDN preesistenti per nomi di dominio personalizzati {#pre-existing-cdn}

Se disponi di una configurazione CDN preesistente per i nomi di dominio personalizzati, verrà visualizzato un messaggio informativo sul **ELENCO CONSENTITI IP** e **Ambiente** pagine, ti incoraggiano ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e configurabili in Cloud Manager.

Il messaggio scompare dopo la migrazione di tutte le configurazioni di ambiente preesistenti tramite l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi per far scomparire il messaggio.

Fare riferimento al documento [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) per ulteriori dettagli.

![Messaggio di configurazione CDN preesistente](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)
