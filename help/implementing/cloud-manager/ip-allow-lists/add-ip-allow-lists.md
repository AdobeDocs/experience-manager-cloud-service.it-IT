---
title: Aggiungi Elenchi consentiti IP
description: Scopri come aggiungere i tuoi Elenchi consentiti IP utilizzando Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 7%

---


# Aggiungere un elenco IP consentiti {#add-ip-allow-list}

Scopri come aggiungere un Elenco consentiti IP personalizzato utilizzando Cloud Manager.

L&#39;utente con il ruolo **Proprietario business** o **Responsabile dell&#39;implementazione** può aggiungere un Elenco consentiti IP seguendo la procedura riportata di seguito.

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

**Per aggiungere un Elenco consentiti IP:**

1. Accedi a Cloud Manager all&#39;indirizzo [experience.adobe.com](https://experience.adobe.com/experiencemanager/).

1. Nel menu a sinistra, fai clic su Cloud Manager, quindi seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Dalla pagina **Panoramica programma**, utilizzando il menu a sinistra (potrebbe essere necessario fare clic sull&#39;icona ![Mostra menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) nell&#39;angolo superiore sinistro per visualizzare il menu), fare clic sull&#39;icona ![Elenco attività](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Elenchi consentiti IP**.

   ![Opzione Elenchi consentiti IP nel menu a sinistra](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Nell&#39;angolo superiore destro della pagina Elenchi consentiti IP fare clic su **Aggiungi Elenco consentiti IP**.

   ![Finestra di dialogo Aggiungi elenco IP consentiti](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Nella finestra di dialogo **Aggiungi Elenco consentiti IP** immettere nel campo **Nome Elenco consentiti IP** un nome che si desidera utilizzare per fare riferimento all&#39;Elenco consentiti IP. Questo nome ha valore puramente informativo. Assicurati che sia sufficientemente descrittivo da aiutarti a identificare l’elenco.

1. Nel campo **Indirizzo IP / CIDR**, immettere fino a 50 indirizzi IP o blocchi CIDR. Puoi aggiungerli in uno dei seguenti modi:

   * Uno alla volta: digitare un indirizzo, quindi premere `Enter`. Ripeti per ogni indirizzo aggiuntivo.
   * Più alla volta: digitare gli indirizzi separati da virgole (,) o tabulazioni, quindi premere `Enter` in modo che ogni indirizzo venga riconosciuto singolarmente.

1. Dopo aver immesso l&#39;ultimo indirizzo IP o blocco CIDR, premere `Enter` per confermare l&#39;input. La voce viene riconosciuta solo dopo aver premuto `Enter` e il pulsante **Salva** diventa attivo.

1. Fai clic su **Salva**.

Dopo il salvataggio, l&#39;Elenco consentiti IP appena creato viene visualizzato come riga nella tabella della pagina **Elenchi consentiti IP**.

