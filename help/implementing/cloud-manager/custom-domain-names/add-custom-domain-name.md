---
title: Aggiunta di un nome di dominio personalizzato
description: Aggiunta di un nome di dominio personalizzato
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 98c137645351c86da8680a31b4929c588863a981
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 4%

---

# Aggiunta di un nome di dominio personalizzato {#adding-cdn}

Per aggiungere un nome di dominio personalizzato in Cloud Manager, un utente deve essere un proprietario business o un gestore distribuzione.

I seguenti passaggi devono essere completati come indicato nella tabella seguente:

| Incremento |  | Responsabilità | Ulteriori informazioni |
|--- |--- |--- |---|
| Aggiungi certificato SLL | Aggiungi certificato SLL | Cliente | [Aggiunta di un certificato SSL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| Verifica del dominio | Aggiungi record TXT | Cliente | [Aggiunta di un record TXT](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| Verifica stato di verifica del dominio |  | Cliente |  |
|  | Stato: Errore di verifica del dominio | Cliente | [Verifica dello stato del nome di dominio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | Stato: Verificato, Distribuzione non riuscita | Contatta il rappresentante Adobe | [Verifica dello stato del nome di dominio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| Aggiungi record DNS che puntano a AEM as a Cloud Service aggiungendo record CNAME o APEX | Configurare le impostazioni DNS | Cliente | [Configurazione delle impostazioni DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| Verifica lo stato del record DNS |  | Cliente | [Verifica dello stato del record DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Stato: Stato DNS non rilevato | Cliente | [Verifica dello stato del record DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Stato: Il DNS viene risolto in modo errato | Cliente |  |


## Considerazioni importanti {#important-considerations}

* Prima di aggiungere un nome di dominio personalizzato, è necessario installare nel programma un certificato SSL valido contenente il nome di dominio personalizzato. Fai riferimento a [Aggiunta di un certificato SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) per saperne di più.

* Impossibile aggiungere i nomi di dominio agli ambienti mentre è presente una pipeline in esecuzione corrente collegata a tali ambienti.

* È possibile aggiungere un solo nome di dominio alla volta. I domini personalizzati lato autore non sono supportati.

* AEM as a Cloud Service non supporta i domini con caratteri jolly.

* Ogni ambiente Cloud Manager può ospitare fino a un massimo di 500 domini personalizzati per ambiente.

* Lo stesso nome di dominio non può essere utilizzato in più di un ambiente.

## Aggiunta di un nome di dominio personalizzato dalla pagina Impostazioni dominio {#adding-cdn-settings}

Per aggiungere un nome di dominio personalizzato dalla pagina Impostazioni dominio, effettua le seguenti operazioni:

1. Passa a **Ambienti** schermata da **Panoramica** pagina.

1. Fai clic su **Impostazioni di dominio** dal menu di navigazione a sinistra.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Fai clic su **Aggiungi dominio** pulsante per aprire **Aggiungi nome di dominio** finestra di dialogo.

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Immetti il nome di dominio personalizzato in **Nome di dominio**.

   >[!NOTE]
   >Non includere `http://`, `https://`o spazi quando si accede al dominio.

1. Seleziona la **Ambiente** il cui servizio di pubblicazione sarà associato al nome di dominio.

1. Seleziona il servizio come **Pubblica** o **Anteprima**.

   >[!NOTE]
   >I nomi di dominio personalizzati sono ora supportati in Cloud Manager per i programmi Sites per i servizi di pubblicazione e anteprima. Ogni ambiente Cloud Manager può ospitare fino a un massimo di 500 domini personalizzati per ambiente. Per ulteriori informazioni sul servizio di anteprima, consulta [Servizio di anteprima](/help/implementing/cloud-manager/manage-environments.md#preview-service).

1. Seleziona la **Certificato SSL del dominio** dal menu a discesa e seleziona **Continua**.

1. **Aggiungi nome di dominio** viene visualizzata la finestra di dialogo. Verrà visualizzata la finestra Verifica nome di dominio per la schermata Ambiente. Fai riferimento a [Aggiunta di un record TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) per saperne di più.

   Segui le istruzioni fornite per provare la proprietà del dominio per il tuo ambiente:

1. Fai clic su **Crea**.
1. La distribuzione CDN richiede un certificato SSL valido e una verifica TXT corretta. Questo è indicato dallo stato **Verificato e distribuito**.
Passa a [Verifica dello stato del nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) per ulteriori informazioni sui vari stati e su come risolvere il problema.

   >[!NOTE]
   >La bozza DNS può richiedere fino a poche ore per il riconoscimento, a causa di ritardi di propagazione DNS. Cloud Manager verificherà la proprietà e aggiornerà lo stato visualizzato nella tabella delle impostazioni del dominio. Per ulteriori informazioni, consulta Controllo dello stato del nome di dominio .

## Aggiunta di un nome di dominio personalizzato dalla pagina Ambienti {#adding-cdn-environments}

1. Passa alla pagina Dettagli ambienti per l’ambiente di interesse.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Utilizza i campi di input nella parte superiore della tabella Nomi di dominio per inviare il nome di dominio personalizzato e seleziona il certificato SSL dall’elenco a discesa. Fai clic su **+ Aggiungi**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Controlla i campi dalla **Aggiungi nome di dominio** e fai clic su **Continua**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >Non includere `http://`, `https://`o spazi quando si accede al dominio.

1. Viene visualizzata la schermata Verifica del nome di dominio per l’ambiente.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Fai riferimento a [Verifica del dominio](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) per saperne di più. Segui le istruzioni fornite per provare la proprietà del dominio per il tuo ambiente.

1. Fai clic su **Crea**.

1. La distribuzione del nome di dominio personalizzato richiede un certificato SSL valido e una verifica TXT corretta. Questo è indicato dallo stato **Verificato e distribuito**.

A questo punto, il nome di dominio personalizzato è pronto per il test e un `CNAME` per indicarlo. Fai riferimento a [Stato del nome di dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) per ulteriori informazioni sui vari stati e su come risolvere il problema.

>[!NOTE]
>La bozza DNS può richiedere fino a poche ore per il riconoscimento, a causa di ritardi di propagazione DNS. Cloud Manager verificherà la proprietà e aggiornerà lo stato visualizzato nella tabella delle impostazioni del dominio. Per ulteriori informazioni, consulta Controllo dello stato del nome di dominio .
