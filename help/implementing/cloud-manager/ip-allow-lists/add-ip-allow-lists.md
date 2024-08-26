---
title: Aggiungi Elenchi consentiti IP
description: Scopri come aggiungere i tuoi Elenchi consentiti IP utilizzando Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1415d07235641262814e81362c806572bcf582ba
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 12%

---


# Aggiungere un elenco IP consentiti {#add-ip-allow-list}

Scopri come aggiungere un Elenco consentiti IP personalizzato utilizzando Cloud Manager.

L&#39;utente con il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione** può aggiungere un Elenco consentiti IP seguendo la procedura riportata di seguito.

{{add-cm-allowlist-frontend-pipeline}}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nella pagina **Panoramica programma**, utilizzando il pannello laterale a sinistra (potrebbe essere necessario fare clic sull&#39;icona dell&#39;hamburger nell&#39;angolo superiore sinistro per visualizzare il pannello), fare clic su **Elenchi consentiti IP**.

   Opzione ![Elenchi consentiti IP nel pannello laterale](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Nell&#39;angolo superiore destro della pagina Elenchi consentiti IP fare clic su **Aggiungi Elenco consentiti IP**.

   ![Finestra di dialogo Aggiungi elenco IP consentiti](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Nella finestra di dialogo **Aggiungi Elenco consentiti IP** immettere nel campo **Nome Elenco consentiti IP** un nome che si desidera utilizzare per fare riferimento all&#39;Elenco consentiti IP. Questo nome ha valore puramente informativo. Assicurati che sia sufficientemente descrittivo da aiutarti a identificare l’elenco.

1. Nel campo **Indirizzo IP / CIDR**, immettere un blocco CIDR IP o IP. Separa più blocchi con una virgola o una tabulazione.

1. Fai clic su **Salva**.

Dopo il salvataggio, l&#39;Elenco consentiti IP appena creato viene visualizzato come riga nella tabella della pagina **Elenchi consentiti IP**.

## Aggiungere l’Elenco consentiti IP di Cloud Manager {#add-cm-allowlist}

La pipeline front-end richiede l’aggiunta anticipata del seguente Elenco consentiti IP di Cloud Manager.

**Elenco consentiti IP Cloud Manager**

`52.254.106.192/28,20.186.185.181,52.254.106.240/28,52.254.107.128/28,52.254.105.192/28,52.254.106.176/28,20.186.185.227,52.254.106.144/28,52.254.107.64/28,20.186.185.239,20.22.83.112,52.254.107.80/28,52.254.107.144/28,52.254.106.224/28,20.14.241.153,52.254.107.0/28,52.254.107.32/28,52.254.106.208/28,40.70.154.136/29,52.254.106.160/28,52.254.107.16/28,52.254.106.0/28,4.152.211.251`

Per evitare interruzioni nell&#39;esecuzione della pipeline front-end, assicurati che questo Elenco consentiti IP di Cloud Manager sia aggiunto e quindi applicato al servizio Author dell&#39;ambiente *prima* che la pipeline venga abilitata.

**Per aggiungere l&#39;Elenco consentiti IP di Cloud Manager:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Nella pagina **Panoramica programma**, utilizzando il pannello laterale a sinistra (potrebbe essere necessario fare clic sull&#39;icona dell&#39;hamburger nell&#39;angolo superiore sinistro per visualizzare il pannello), fare clic su **Elenchi consentiti IP**.

1. Nell&#39;angolo superiore destro della pagina Elenchi consentiti IP fare clic su **Aggiungi Elenco consentiti IP**.

1. Nella finestra di dialogo **Aggiungi Elenco consentiti IP** digitare *`Cloud Manager`* nel campo **Nome Elenco consentiti IP**.

1. Copia il blocco di indirizzi IP di Elenco consentiti di Cloud Manager qui sopra. Ogni indirizzo è già separato da una virgola.

1. Nella finestra di dialogo **Aggiungi Elenco consentiti IP**, incolla il blocco nel campo **Indirizzo IP / CIDR**.

1. Posizionare il cursore subito dopo la prima virgola nell&#39;elenco indirizzi e premere **Invio**.

1. Fai clic su **Salva**.

Ora [applica l&#39;Elenco consentiti IP di Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) agli ambienti del programma.



