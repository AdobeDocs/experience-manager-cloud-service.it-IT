---
title: Verifica stato nome dominio
description: Scopri come verificare che Cloud Manager abbia confermato correttamente il nome di dominio personalizzato.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 17%

---


# Controllare lo stato del nome di dominio {#check-status}

Scopri come verificare che Cloud Manager abbia confermato correttamente il nome di dominio personalizzato.

## Controllare lo stato di un nome di dominio personalizzato {#how-to}

Prima di controllare lo stato del nome di dominio in Cloud Manager, accertati di aver già aggiunto un certificato SSL gestito dal cliente (OV/EV) per il dominio personalizzato, come descritto in [Aggiungere un certificato SSL gestito dal cliente](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md##add-customer-managed-ssl-cert).

**Per controllare lo stato di un nome di dominio personalizzato:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Fai clic su **Impostazioni dominio** nel menu a sinistra.

1. Fai clic sull’icona **Stato** del nome di dominio.

Vengono visualizzati i dettagli dello stato. Il dominio personalizzato è pronto per essere utilizzato quando viene visualizzato lo stato **Dominio verificato e distribuito**. Consulta la [sezione successiva](#statuses) per informazioni dettagliate sui diversi stati e sul loro significato.

>[!NOTE]
>
>Se si utilizza un *certificato SSL gestito (DV) di Adobe* con il dominio, Cloud Manager attiva automaticamente la verifica quando si fa clic su **Verifica** nella finestra di dialogo Verifica dominio quando si [aggiunge un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
>
>Se prevedi di utilizzare un **certificato SSL gestito dal cliente (OV/EV)**, il dominio viene verificato *dopo* che [aggiungi il certificato SSL OV/EV](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).


## Stati di verifica {#statuses}

Cloud Manager verifica la proprietà del dominio tramite il certificato SSL gestito dal cliente (OV/EV). Al termine, viene visualizzato uno dei seguenti messaggi di stato:

| Stato | Descrizione |
| --- | --- |
| Verifica del dominio non riuscita | Il certificato EV/OV gestito dal cliente è mancante o rilevato con errori.<br> Per risolvere il problema, seguire le istruzioni fornite nel messaggio di stato. Al termine dell’operazione, seleziona l’icona **Nuovo tentativo di verifica** accanto allo stato. |
| Verifica del dominio in corso | Verifica in corso.<br>Questo stato viene generalmente visualizzato dopo aver selezionato l&#39;icona **Verifica di nuovo** accanto allo stato. L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS. |
| Verificato - Distribuzione non riuscita | La verifica del certificato EV/OV è riuscita, ma la distribuzione CDN non è riuscita.<br>In questi casi, contatta il tuo rappresentante Adobe. |
| Dominio verificato e implementato | Questo stato indica che il nome di dominio personalizzato è pronto per l’uso.<br>A questo punto, il nome di dominio personalizzato è pronto per essere testato e puntato al nome di dominio Cloud Manager. Per ulteriori informazioni, consulta [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| Eliminazione | È in corso l’eliminazione di un nome di dominio personalizzato. |
| Eliminazione non riuscita | Eliminazione di un nome di dominio personalizzato non riuscita. È necessario riprovare.<br>Per ulteriori informazioni, consulta [Gestire i nomi di dominio personalizzati](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md). |


## Errore del nome di dominio {#domain-error}

Di seguito è riportato un errore comune di verifica del nome di dominio e la sua risoluzione tipica.

### Errore dominio non installato {#domain-not-installed}

<!-- This error may occur during domain validation of the EV/OV certificate even after you have checked that the certificate has been updated appropriately. -->

Quando tenti di aggiungere una mappatura di dominio in Cloud Manager, potresti visualizzare il seguente messaggio di errore:

*Il dominio è già installato in un account Fastly. Rimuovilo prima di aggiungerlo a Cloud Service.*

<!-- This message indicates that the domain is currently associated with a different Fastly account—typically outside of Adobe's control. To proceed, the domain must be disassociated from the other account before it can be added to the Adobe-managed Cloud Service. This issue usually occurs when the same domain is already mapped to a different origin in a non-Adobe Fastly configuration. -->

**Causa errore**
Fastly blocca un dominio all’account che per primo lo registra e altri account devono richiedere l’autorizzazione per registrare un sottodominio. Inoltre, Fastly consente di assegnare un dominio APEX e i sottodomini associati a un unico servizio e account Fastly. Questo errore viene visualizzato se disponi di un account Fastly che collega gli stessi domini e sottodomini APEX utilizzati per i domini AEM Cloud Service.

**Risoluzione degli errori**
L’errore viene corretto come segue:

* Prima di installare il dominio in Cloud Manager, rimuovi il dominio APEX e i sottodomini dall’account esistente.

* Collega il dominio APEX e tutti i sottodomini all’account Fastly AEM as a Cloud Service con questa opzione. Per ulteriori dettagli, vedi [Utilizzo dei domini](https://www.fastly.com/documentation/guides/getting-started/domains/working-with-domains/working-with-domains/) nella documentazione Fastly.

* Se il dominio apex ha più sottodomini per siti AEM as a Cloud Service e non AEM che devono essere collegati a diversi account Fastly, prova a installare il dominio in Cloud Manager. Questo processo consente di gestire le connessioni del sottodominio tra diversi account Fastly. Se l’installazione del dominio non riesce, crea un ticket di assistenza clienti con Fastly in modo che Adobe possa eseguire il follow-up con Fastly a tuo nome.

>[!TIP]
>
>Per risolvere i problemi di delega del dominio con Fastly in genere sono necessari 1-2 giorni lavorativi. Per questo motivo, si consiglia di installare i domini molto prima della loro data di Go Live.

>[!NOTE]
>
>Se il dominio non è stato installato correttamente, non instradare il DNS del sito agli IP di AEM as a Cloud Service.

## Configurazioni CDN preesistenti per i nomi di dominio personalizzati {#pre-existing-cdn}

Se disponi già di una configurazione CDN (Content Delivery Network) per i nomi di dominio personalizzati, viene visualizzato un messaggio informativo sulle pagine **Nomi di dominio personalizzati** e **Ambiente**. Ti incoraggia ad aggiungere queste configurazioni tramite l’interfaccia utente in modo che possano essere gestite e visualizzate all’interno di Cloud Manager.

Il messaggio scompare dopo che tutte le configurazioni dell’ambiente preesistenti sono state migrate utilizzando l’interfaccia utente. Potrebbero essere necessari 1-2 giorni lavorativi affinché il messaggio non venga più visualizzato.

Per ulteriori dettagli, vedere [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Passaggi successivi {#next-steps}

Dopo aver verificato lo stato del dominio in Cloud Manager, configura le impostazioni DNS aggiungendo i record DNS, CNAME o APEX che puntano ad AEM as a Cloud Service. Procedi al documento [Aggiungi un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) per continuare la configurazione del nome di dominio personalizzato.
