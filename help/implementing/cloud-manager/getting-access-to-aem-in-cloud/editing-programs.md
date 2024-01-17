---
title: Gestione e modifica dei programmi
description: Scopri come modificare i programmi sandbox e di produzione per apportare modifiche alle opzioni dopo averli creati.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: 0d60c19638707262dab7f290f84fa873b694bc22
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 24%

---


# Gestione e modifica dei programmi {#editing-programs}

Il **I miei programmi** Questa pagina fornisce una panoramica di tutti i programmi a cui si ha accesso. Quando si seleziona un singolo programma, **Panoramica del programma** fornisce dettagli sul programma in una panoramica.

Dalla sezione **Panoramica del programma**, gli utenti con le autorizzazioni necessarie possono modificare [programmi di produzione creati nell’organizzazione](creating-production-programs.md) e [programmi sandbox creati nell’organizzazione.](creating-sandbox-programs.md) Modificando un programma è possibile:

* Aggiungere la soluzione Sites a un programma esistente con Assets e viceversa.
* Rimuovere Sites o Assets da un programma esistente con entrambi Sites e Assets.
* Aggiungere una seconda soluzione non utilizzata a un programma esistente o nuovo.
* Eliminare i programmi sandbox.

## Autorizzazioni {#permissions}

Devi essere membro di **Proprietario business** per modificare i programmi o eliminare i programmi sandbox e per accedere alla dashboard delle licenze.

## I miei programmi {#my-programs}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il **I miei programmi** pagina mostra un elenco di tutti i programmi a cui si ha accesso come riquadri.

![Pagina I miei programmi](/help/implementing/cloud-manager/assets/my-programs.png)

### Invito all’azione {#cta}

Nella parte superiore della pagina è riportato un invito all’azione relativo allo stato dell’organizzazione. Ad esempio, se hai configurato correttamente i programmi, potrebbero essere visualizzate le statistiche delle attività degli ultimi 90 giorni, tra cui:

* Numero di [implementazioni](/help/implementing/cloud-manager/deploy-code.md)
* Numero di [problemi di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) identificati
* Numero di build

Oppure, se stai iniziando la configurazione dell’organizzazione, ci potrebbero essere suggerimenti sui passaggi successivi o sulle risorse della documentazione.

### Scheda Programmi {#programs-tab}

Il **Programmi** scheda elenca le schede che rappresentano ogni programma a cui hai accesso. Tocca o fai clic su una scheda per accedere al **Panoramica del programma** pagina del programma per informazioni dettagliate sul programma.

Utilizza le opzioni di ordinamento per trovare meglio il programma necessario.

![Opzioni di ordinamento](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* Ordina per
   * Data di creazione (impostazione predefinita)
   * Nome del programma
   * Stato
* Crescente (predefinito) / Decrescente
* Vista griglia (impostazione predefinita)
* Vista a elenco 

### Scheda Licenza {#license-tab}

Il **Licenza** consente di accedere rapidamente al [Dashboard delle licenze.](/help/implementing/cloud-manager/license-dashboard.md)

## Panoramica del programma {#program-overview}

Dopo aver selezionato un programma da **[I miei programmi](#my-programs)** , Cloud Manager apre la pagina **Panoramica del programma** per il programma selezionato.

![Pagina Panoramica del programma](/help/implementing/cloud-manager/assets/program-overview.png)

Tocca o fai clic sul nome del programma nell’angolo in alto a sinistra della pagina per passare rapidamente a un altro programma o tornare al **[I miei programmi](#my-programs)** pagina. È inoltre possibile [modifica il programma selezionato](#editing) o [aggiungi un programma.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

![Selettore di programma](/help/implementing/cloud-manager/assets/program-switcher.png)

L’invito all’azione nella parte superiore ti fornirà informazioni utili a seconda dello stato del programma. Per un nuovo programma puoi vedere i passaggi successivi offerti e un promemoria della data di pubblicazione, [impostato durante la creazione del programma.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)

![Invito all&#39;azione per un nuovo programma](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

Per un programma live, lo stato dell’ultima implementazione con collegamenti per i dettagli e l’avvio di una nuova implementazione.

![Invito all’azione](/help/implementing/cloud-manager/assets/info-banner.png)

**Ambienti** e **Pipeline** Le schede forniscono una rapida panoramica di entrambi all&#39;interno del programma selezionato.

![Schede](/help/implementing/cloud-manager/assets/environments-pipelines.png)

Il **Prestazioni** offre una panoramica della **[Dashboard CDN.](/help/implementing/cloud-manager/cdn-performance.md)**

![Scheda Prestazioni](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

## Modifica di un programma {#editing}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il giorno **[I miei programmi](#my-programs)** , fare clic sul programma che si desidera modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma nella parte superiore sinistra della pagina e seleziona **Modifica programma**.

   ![Opzione Modifica programma](assets/edit-program-overview.png)

1. Viene visualizzata la pagina **Modifica programma**. Dalla scheda **Generale**, modifica il nome e la descrizione del programma.

   * È necessario selezionare almeno una soluzione per programma.

   ![Scheda Generale](assets/edit-program-prod1.png)

1. Dalla scheda **Soluzioni e componenti aggiuntivi**, modifica le soluzioni del programma.

   ![Selezione delle soluzioni](assets/edit-prg.png)

1. Fai clic sulla freccia che precede il nome della soluzione per visualizzare i componenti aggiuntivi facoltativi, ad esempio per selezionare **Commerce** opzione del componente aggiuntivo in **Sites**.

   ![Modifica dei componenti aggiuntivi](assets/edit-program-add-on.png)

1. Dalla scheda **Impostazioni pubblicazione**, modifica la data di pubblicazione pianificata per il programma.

   ![Modifica delle impostazioni di pubblicazione](assets/edit-program-go-live.png)

   * Questa data è esclusivamente a scopo informativo. Attiva il widget di pubblicazione nella pagina di panoramica del programma. A sua volta, fornisce collegamenti interni alla documentazione sulle best practice as a Cloud Service di Adobe Experience Manager (AEM) per allinearsi al percorso, che culmina in un’esperienza di lancio di successo.
   * Questa scheda non è disponibile per i programmi sandbox.

1. Se i diritti richiesti sono disponibili per il programma, il **Sicurezza** verrà visualizzata la scheda in cui è possibile modificare le opzioni di protezione per il programma.

   ![Modifica impostazioni di protezione](assets/edit-program-security.png)

   * Impossibile abilitare o disabilitare HIPAA dopo [creazione di programmi.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
      * [Ulteriori informazioni](https://www.adobe.com/go/hipaa-ready_it) sull’implementazione della soluzione compatibile HIPAA di Adobe.
   * Una volta attivata, la protezione WAF-DDOS può essere configurata impostando un [pipeline non di produzione.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

1. Clic **Aggiorna** per salvare le modifiche apportate al programma.

Ogni volta che si modifica un programma, incluso l&#39;aggiunta o la rimozione di una soluzione o di un componente aggiuntivo, tali modifiche diventano effettive dopo la distribuzione successiva.

## Eliminazione dei programmi sandbox {#delete-sandbox-program}

L’eliminazione di un programma sandbox comporta la rimozione di tutti gli ambienti e delle relative pipeline associate.

>[!TIP]
>
>In alternativa, gli utenti con i ruoli **Proprietario business** o **Responsabile dell’implementazione** possono eliminare gli ambienti di produzione e di staging al posto dell’intero programma sandbox.

Per eliminare un programma sandbox, effettuare le seguenti operazioni.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Il giorno **[I miei programmi](#my-programs)** , fare clic sul programma che si desidera modificare per visualizzarne i dettagli.

1. Fai clic sul nome del programma nella parte superiore sinistra della pagina e seleziona **Elimina programma**.

   ![Opzione Elimina programma](assets/delete-sandbox1.png)

In alternativa, dalla pagina della panoramica di Cloud Manager, accedi alla scheda del programma, fai clic sul pulsante con i puntini di sospensione e seleziona **Elimina programma**.

![Scheda Elimina sandbox da programma](assets/delete-sandbox2.png)

>[!NOTE]
>
>È possibile eliminare solo i programmi sandbox. I programmi di produzione non possono essere eliminati.
