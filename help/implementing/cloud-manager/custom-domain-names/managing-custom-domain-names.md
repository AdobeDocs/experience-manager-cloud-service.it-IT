---
title: Gestione dei nomi di dominio personalizzati
description: Scopri come visualizzare, aggiornare, sostituire ed eliminare i nomi di dominio personalizzati con Cloud Manager.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 19%

---


# Gestire i nomi di dominio personalizzati {#managing-custom-domain-names}

Cloud Manager consente di modificare, aggiornare, sostituire, verificare ed eliminare i nomi di dominio personalizzati.

## Modificare una configurazione del nome di dominio personalizzato {#view-and-update}

Ad Adobe, in Cloud Manager potrebbe essere utile modificare la configurazione di un nome di dominio personalizzato per i seguenti motivi:

* **Cambio degli ambienti**: applicare la configurazione corretta a seconda che il contenuto venga distribuito agli utenti finali (Publish) o agli utenti interni (Author).
* **Aggiornamenti della sicurezza**: per eseguire l&#39;aggiornamento a un certificato SSL più recente per migliorare la sicurezza o la conformità.
* **Modifica della strategia di distribuzione**: assicurarsi che il certificato SSL corretto venga applicato a un ambiente specifico per la crittografia e l&#39;accesso al sito corretti.

**Per modificare la configurazione di un nome di dominio personalizzato:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nell&#39;angolo superiore sinistro della pagina fare clic su ![Mostra icona](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu sul lato sinistro.

1. Nell&#39;intestazione **Services**, fare clic su **Configurazioni CDN**.

1. Nella pagina **Configurazioni CDN**, fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) alla fine di una riga di cui desideri modificare la CDN.

1. Fai clic su **Modifica**.

1. Nella finestra di dialogo **Modifica configurazione CDN** eseguire le operazioni seguenti:

   * Nell&#39;elenco a discesa **Livello** selezionare il livello (Publish o Anteprima) che si desidera utilizzare.
   * Nell&#39;elenco a discesa **Certificato SSL** selezionare il certificato SSL che si desidera utilizzare.

1. Fai clic su **Aggiorna**.


## Aggiornare il certificato SSL di un nome di dominio personalizzato {#update-cert}

Segui gli stessi passaggi indicati sopra per aggiornare il certificato SSL di un nome di dominio personalizzato.

>[!NOTE]
>
>Il certificato SSL deve essere valido, [già configurato](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) e contenere il nome di dominio personalizzato che si sta aggiornando.


## Verificare un nome di dominio personalizzato {#verify-custom-domain-name}

Vedi anche [Aggiungere un nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla schermata **Panoramica**, accedi alla pagina **Impostazioni dominio**.

1. Identifica la riga del nome di dominio personalizzato che desideri verificare.

1. Fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) all&#39;estrema destra della riga.

1. Scegliere **Verifica** dal menu a discesa.

1. Nella finestra di dialogo **Verifica dominio**, in **Quale tipo di certificato intendi utilizzare con questo dominio?Elenco a discesa**, selezionare una delle opzioni seguenti:

   | Opzione tipo di certificato | Descrizione |
   | --- | --- |
   | Adobe di certificato SSL gestito (DV) | Selezionare questo tipo di certificato se si desidera utilizzare un certificato DV (convalida dominio). Questa opzione è ideale per la maggior parte dei casi e fornisce la convalida di base del dominio. Adobe gestisce e rinnova automaticamente il certificato. |
   | Certificato SSL gestito dal cliente (OV/EV) | Selezionare questo tipo di certificato se si desidera utilizzare un certificato SSL EV/OV per proteggere il dominio. Questa opzione offre una protezione avanzata con OV (convalida organizzazione) o EV (convalida estesa). Da utilizzare se è necessaria una verifica più rigorosa, livelli di attendibilità più elevati o un controllo personalizzato dei certificati. |

1. Nella finestra di dialogo **Verifica dominio**, in base al tipo di certificato selezionato, eseguire una delle operazioni seguenti:

   | Se hai selezionato il tipo di certificato | Descrizione |
   | --- | ---  |
   | Certificato gestito da Adobe | a. Completa i [passaggi Adobi del certificato gestito](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-steps). Dopo aver completato i passaggi della finestra di dialogo **Verifica dominio**, fare clic su **Verifica**.<ul><li>L’elaborazione della verifica DNS può richiedere alcune ore per via dei ritardi di propagazione del DNS.</li><li>Cloud Manager verifica infine la proprietà del nome di dominio e aggiorna lo stato nella tabella **Impostazioni dominio**. Per ulteriori dettagli, vedere [Verifica stato nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).</li>![Verifica stato dominio](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. È ora possibile [aggiungere un certificato SSL (DV) gestito da Adobe](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert).</li></ul> |
   | Certificato gestito dal cliente | a. Fare clic su **OK**.<br> b. Ora puoi [aggiungere un certificato SSL gestito dal cliente (OV/EV)](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert).<br>Dopo aver aggiunto il certificato, il nome di dominio viene contrassegnato come verificato nella tabella **Impostazioni dominio**. Per ulteriori dettagli, vedere [Verifica stato nome di dominio personalizzato](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).</li></ul><br>![Verificare il dominio per un certificato EV/OV gestito dal cliente](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |


## Eliminare un nome di dominio personalizzato da tutti gli ambienti associati {#deleting}

L’utente con il ruolo **Proprietario business** o **Responsabile dell’implementazione** può eliminare un nome di dominio personalizzato con Cloud Manager.

### Eliminare un nome di dominio personalizzato da tutti gli ambienti associati {#delete-cdn-all}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla schermata **Panoramica**, accedi alla pagina **Impostazioni dominio**.

1. Identifica la riga del nome di dominio personalizzato che desideri eliminare.

1. Fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) all&#39;estrema destra della riga.

1. Seleziona **Elimina**.

1. Conferma quanto inserito.


### Eliminare un nome di dominio personalizzato da un ambiente specifico {#delete-cdn-specific}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica**, accedi alla schermata **Ambienti**.

1. Dalla pagina **Ambienti**, accedi a una schermata dei dettagli dell&#39;ambiente di tuo interesse.

1. Nella tabella dei nomi di dominio, identifica la riga del nome di dominio personalizzato che desideri eliminare.

1. Fai clic sull&#39;icona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) all&#39;estrema destra della riga.

1. Seleziona **Elimina**.

1. Conferma quanto inserito.
