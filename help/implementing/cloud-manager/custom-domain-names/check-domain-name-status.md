---
title: Controllo dello stato del nome di dominio
description: Scopri come determinare se il nome di dominio personalizzato è stato verificato correttamente da Cloud Manager.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 64%

---


# Controllo dello stato del nome di dominio {#check-status}

Scopri come determinare se il nome di dominio personalizzato è stato verificato correttamente da Cloud Manager.

## Requisiti {#requirements}

Prima di controllare lo stato del nome di dominio in Cloud Manager, è necessario soddisfare questi requisiti.

* Devi innanzitutto aggiungere un record TXT per il dominio personalizzato come descritto nel documento [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md).

## Controllare lo stato del nome di dominio personalizzato {#how-to}

In Cloud Manager è possibile determinare lo stato del nome di dominio personalizzato.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Fai clic su **Impostazioni dominio** nel pannello di navigazione a sinistra.

1. Fai clic sull’icona **Stato** del nome di dominio.

Vengono visualizzati i dettagli dello stato. Il dominio personalizzato è pronto per essere utilizzato quando viene visualizzato lo stato **Dominio verificato e distribuito**. Consulta la [sezione successiva](#statuses) per informazioni dettagliate sui diversi stati e sul loro significato.

>[!NOTE]
>
>Cloud Manager attiverà automaticamente la verifica quando selezioni **Crea** nel passaggio di verifica della procedura guidata **Aggiungi dominio personalizzato** quando [aggiungi un nuovo nome di dominio personalizzato a Cloud Manager](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). Per le verifiche successive, devi riselezionare attivamente l’icona di verifica accanto allo stato.

## Informazioni sugli stati di verifica {#statuses}

Cloud Manager verificherà la proprietà del dominio tramite il [valore TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) e visualizzerà uno dei seguenti messaggi di stato.

* **Verifica del dominio non riuscita**: il valore TXT è mancante o viene rilevato con errori.

   * Per risolvere il problema, segui le istruzioni fornite nel messaggio di stato.
   * Al termine dell’operazione, seleziona l’icona **Nuovo tentativo di verifica** accanto allo stato.

* **Verifica del dominio in corso**: la verifica è in corso.

   * Questo stato viene generalmente visualizzato dopo aver selezionato l’icona **Nuovo tentativo di verifica** accanto allo stato.
   * L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS.

* **Verificato, distribuzione non riuscita**: la verifica TXT è stata completata correttamente, ma la distribuzione CDN non è riuscita.

   * In questo caso, contatta il rappresentante Adobe.

* **Dominio verificato e distribuito**: questo stato indica che il nome di dominio personalizzato è pronto all’uso.

   * A questo punto, il nome di dominio personalizzato è pronto per la fase di test e per puntare al nome di dominio di Cloud Manager.
   * Per ulteriori informazioni, consulta [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md).

* **Eliminazione in corso**: è in corso l’eliminazione di un nome di dominio personalizzato.

* **Eliminazione non riuscita**: l’eliminazione del nome di dominio personalizzato non è riuscita; è necessario effettuare un nuovo tentativo.

   * Per ulteriori informazioni, consulta [Gestione dei nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).

## Errori dei nomi di dominio {#domain-error}

Di seguito sono riportati alcuni errori comuni di verifica dei nomi di dominio e le relative risoluzioni tipiche.

### Errore del dominio non installato {#domain-not-installed}

Questo errore può verificarsi durante la convalida del dominio del record TXT anche dopo aver verificato che il record sia stato aggiornato in modo appropriato.

#### Causa errore {#cause}

Faslty blocca un dominio all’account iniziale che ne ha effettuato la registrazione, impedendo a qualsiasi altro account di registrare un sottodominio senza richiedere l’autorizzazione. Inoltre, Fastly consente di assegnare un dominio APEX e i sottodomini associati a un unico servizio e account Fastly. Questo errore viene visualizzato se disponi di un account Fastly che collega gli stessi domini e sottodomini APEX utilizzati per i domini AEM Cloud Service.

#### Risoluzione degli errori {#resolution}

L’errore viene corretto come segue:

* Prima di installare il dominio in Cloud Manager, rimuovi il dominio APEX e i sottodomini dall’account esistente.

* Collega il dominio APEX e tutti i sottodomini all’account Fastly AEM as a Cloud Service con questa opzione. Per ulteriori informazioni, consulta [Utilizzo dei domini nella documentazione Fastly](https://docs.fastly.com/en/guides/working-with-domains).

* Se il dominio apex ha più sottodomini per siti AEM as a Cloud Service e non AEM as a Cloud Service che desideri collegare a diversi account Fastly, prova a installare il dominio in Cloud Manager. Se l’installazione del dominio non riesce, crea un ticket di assistenza clienti con Fastly in modo che Adobe possa eseguire il follow-up con Fastly a tuo nome.

>[!TIP]
>
>Per risolvere i problemi di delega del dominio con Fastly in genere sono necessari 1-2 giorni lavorativi. Per questo motivo, si consiglia vivamente di installare i domini molto prima della loro data di Go Live.

>[!NOTE]
>
>Se il dominio non è stato installato correttamente, non instradare il DNS del sito agli IP di AEM as a Cloud Service.

## Configurazioni CDN preesistenti per i nomi di dominio personalizzati {#pre-existing-cdn}

Se disponi di una configurazione CDN preesistente per i nomi di dominio personalizzati, viene visualizzato un messaggio informativo sulle pagine **Nomi di dominio personalizzati** e **Ambiente** che ti invita ad aggiungere queste configurazioni tramite l&#39;interfaccia utente in modo che siano visibili e configurabili in Cloud Manager.

Il messaggio non viene più visualizzato dopo aver eseguito la migrazione di tutte le configurazioni dell’ambiente preesistenti tramite l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi affinché il messaggio non venga più visualizzato.

Per ulteriori dettagli, consulta [Aggiunta di un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Passaggi successivi {#next-steps}

Dopo aver verificato lo stato del dominio in Cloud Manager, dovrai configurare le impostazioni DNS aggiungendo i record DNS CNAME o APEX che puntano ad AEM as a Cloud Service. Procedi al documento [Configurazione delle impostazioni DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) per continuare la configurazione del nome di dominio personalizzato.
