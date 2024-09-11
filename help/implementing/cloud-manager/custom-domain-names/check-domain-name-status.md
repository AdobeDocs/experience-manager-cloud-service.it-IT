---
title: Controllo dello stato del nome di dominio
description: Scopri come verificare che Cloud Manager abbia confermato correttamente il nome di dominio personalizzato.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3ff7b76f7892269f6ca001ff2c079bc693c06d93
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 28%

---


# Controllare lo stato del nome di dominio {#check-status}

Scopri come verificare che Cloud Manager abbia confermato correttamente il nome di dominio personalizzato.

## Requisiti {#requirements}

Rispetta questi requisiti prima di controllare lo stato del nome di dominio in Cloud Manager.

* Aggiungere innanzitutto un record TXT per il dominio personalizzato come descritto nel documento [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Verifica lo stato del nome di dominio personalizzato {#how-to}

In Cloud Manager è possibile determinare lo stato del nome di dominio personalizzato.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Fai clic su **Impostazioni dominio** nel pannello di navigazione a sinistra.

1. Fai clic sull’icona **Stato** del nome di dominio.

Vengono visualizzati i dettagli dello stato. Il dominio personalizzato è pronto per essere utilizzato quando viene visualizzato lo stato **Dominio verificato e distribuito**. Consulta la [sezione successiva](#statuses) per informazioni dettagliate sui diversi stati e sul loro significato.

>[!NOTE]
>
>Cloud Manager attiva automaticamente la verifica quando selezioni **Crea** nel passaggio di verifica della procedura guidata **Aggiungi dominio personalizzato** quando [aggiungi un nuovo nome di dominio personalizzato a Cloud Manager](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). Per le verifiche successive, devi riselezionare attivamente l’icona di verifica accanto allo stato.

## Stati di verifica {#statuses}

Cloud Manager verifica la proprietà del dominio tramite il valore [TXT](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) e visualizza uno dei seguenti messaggi di stato.

| Stato | Descrizione |
| --- | --- |
| Verifica del dominio non riuscita | Il valore TXT è mancante o viene rilevato con errori.<br> Per risolvere il problema, seguire le istruzioni fornite nel messaggio di stato. Al termine dell’operazione, seleziona l’icona **Nuovo tentativo di verifica** accanto allo stato. |
| Verifica del dominio in corso | Verifica in corso.<br>Questo stato viene generalmente visualizzato dopo aver selezionato l&#39;icona **Verifica di nuovo** accanto allo stato. L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS. |
| Verificato - Distribuzione non riuscita | La verifica TXT è riuscita, ma la distribuzione CDN non è riuscita.<br>In questi casi, contatta il rappresentante del tuo Adobe. |
| Dominio verificato e implementato | Questo stato indica che il nome di dominio personalizzato è pronto per l’uso.<br>A questo punto, il nome di dominio personalizzato è pronto per essere testato e puntato al nome di dominio Cloud Manager. Per ulteriori informazioni, consulta [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| Eliminazione in corso | È in corso l’eliminazione di un nome di dominio personalizzato. |
| Eliminazione non riuscita | Eliminazione di un nome di dominio personalizzato non riuscita. È necessario riprovare.<br>Per ulteriori informazioni, consulta [Gestire i nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md). |


## Errori del nome dominio {#domain-error}

Di seguito sono riportati alcuni errori comuni di verifica dei nomi di dominio e le relative risoluzioni tipiche.

### Errore dominio non installato {#domain-not-installed}

Questo errore può verificarsi durante la convalida del dominio del record TXT anche dopo aver verificato che il record sia stato aggiornato in modo appropriato.

#### Causa dell’errore {#cause}

Fastly blocca un dominio all’account che per primo lo registra e altri account devono richiedere l’autorizzazione per registrare un sottodominio. Inoltre, Fastly consente di assegnare un dominio APEX e i sottodomini associati a un unico servizio e account Fastly. Questo errore viene visualizzato se disponi di un account Fastly che collega gli stessi domini e sottodomini APEX utilizzati per i domini AEM Cloud Service.

#### Risoluzione degli errori {#resolution}

L’errore viene corretto come segue:

* Prima di installare il dominio in Cloud Manager, rimuovi il dominio APEX e i sottodomini dall’account esistente.

* Collega il dominio APEX e tutti i sottodomini all’account Fastly AEM as a Cloud Service con questa opzione. Per ulteriori informazioni, consulta [Utilizzo dei domini nella documentazione Fastly](https://docs.fastly.com/en/guides/working-with-domains).

* Se il dominio apex ha più sottodomini per siti AEM as a Cloud Service e non AEM che devono essere collegati a diversi account Fastly, prova a installare il dominio in Cloud Manager. Questo processo consente di gestire le connessioni del sottodominio tra diversi account Fastly. Se l’installazione del dominio non riesce, crea un ticket di assistenza clienti con Fastly in modo che Adobe possa seguire il caso con Fastly per tuo conto.

>[!TIP]
>
>Per risolvere i problemi di delega del dominio con Fastly in genere sono necessari 1-2 giorni lavorativi. Per questo motivo, si consiglia vivamente di installare i domini molto prima della loro data di Go Live.

>[!NOTE]
>
>Se il dominio non è stato installato correttamente, non instradare il DNS del sito agli IP di AEM as a Cloud Service.

## Configurazioni CDN preesistenti per i nomi di dominio personalizzati {#pre-existing-cdn}

Se disponi già di una configurazione CDN per i nomi di dominio personalizzati, viene visualizzato un messaggio informativo sulle pagine **Nomi di dominio personalizzati** e **Ambiente**. Ti incoraggia ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che possano essere gestite e visualizzate all’interno di Cloud Manager.

Il messaggio scompare dopo che tutte le configurazioni dell’ambiente preesistenti sono state migrate utilizzando l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi affinché il messaggio non venga più visualizzato.

Per ulteriori dettagli, vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Passaggi successivi {#next-steps}

Dopo aver verificato lo stato del dominio in Cloud Manager, configura le impostazioni DNS aggiungendo i record DNS, CNAME o APEX che puntano ad AEM as a Cloud Service. Procedi al documento [Aggiungi un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) per continuare la configurazione del nome di dominio personalizzato.
