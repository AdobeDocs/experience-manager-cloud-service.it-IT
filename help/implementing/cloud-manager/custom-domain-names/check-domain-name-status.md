---
title: Verifica dello stato del nome di dominio
description: Scopri come determinare se il nome di dominio personalizzato è stato verificato correttamente da Cloud Manager.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: ba0226b5ad3852dd5f72dd7e0ace650035f5ac6a
workflow-type: tm+mt
source-wordcount: '637'
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

## Errori nome di dominio {#domain-error}

Questa sezione spiega gli errori che potresti visualizzare e come risolverli.

**Dominio non installato** - Si riceve questo errore durante la convalida del dominio del record TXT anche dopo aver verificato che il record sia stato aggiornato in modo appropriato.

**Spiegazione errore** - Blocca infine un dominio all&#39;account iniziale che lo ha registrato e nessun altro account può registrare un sottodominio senza richiedere l&#39;autorizzazione. Inoltre, Flast ti consente di assegnare un dominio apex e i sottodomini associati a un solo servizio e account Flast. Se disponi di un account Flast esistente che collega lo stesso apex e sottodomini utilizzati per i tuoi domini AEM Cloud Service, verrà visualizzato questo errore.

**Risoluzione degli errori** - L&#39;errore viene corretto come segue:

* Rimuovi l’apex e i sottodomini dall’account esistente prima di installare il dominio in Cloud Manager. Utilizza questa opzione per collegare il dominio apex e tutti i sottodomini all’account Flast AEM as a Cloud Service. Vedi [Utilizzo dei domini nella documentazione finale](https://docs.fastly.com/en/guides/working-with-domains) per ulteriori dettagli.

* Se il dominio apex ha più sottodomini per AEM siti as a Cloud Service e non AEM as a Cloud Service che desideri collegare a diversi account Flast, prova a installare il dominio in Cloud Manager e se l’installazione del dominio non riesce a creare un ticket di assistenza clienti con Flast in modo da poter seguire Flast per tuo conto.

>[!NOTE]
>
>NOTA: Non instradare il DNS del sito a AEM IP as a Cloud Service se il dominio non è stato installato correttamente.

## Configurazioni CDN preesistenti per nomi di dominio personalizzati {#pre-existing-cdn}

Se disponi di una configurazione CDN preesistente per i nomi di dominio personalizzati, verrà visualizzato un messaggio informativo sul **Nomi di dominio personalizzati** e **Ambiente** pagine, ti incoraggiano ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che siano visibili e configurabili in Cloud Manager.

Il messaggio scompare dopo la migrazione di tutte le configurazioni di ambiente preesistenti tramite l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi per far scomparire il messaggio.

Fare riferimento al documento [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) per ulteriori dettagli.
