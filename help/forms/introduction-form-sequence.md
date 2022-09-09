---
title: Come si crea una sequenza di moduli a più passaggi?
description: Con [!DNL Experience Manager Forms], è possibile definire una sequenza di pannelli per consentire agli utenti di spostarsi e compilare un modulo adattivo. Approfondisci la profondità adottando un approccio basato su casi d’uso come esempio per creare una sequenza di moduli a più passaggi.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Introduzione alla sequenza di moduli a più passaggi {#introduction-to-multi-step-form-sequence}

La funzione Forms adattiva consente agli autori di moduli di creare con grande facilità un’esperienza di acquisizione dati in più passaggi. Offre supporto integrato per la creazione di più pannelli e l’associazione di ciascun pannello a diversi pattern di navigazione. Gli autori dei moduli possono raggruppare i campi modulo in sezioni logiche e rappresentare un gruppo come pannello. La navigazione tra i pannelli viene controllata mediante il layout del pannello. Gli autori possono scegliere di disporre i pannelli in layout diversi, ad esempio per posizionarli in sequenza utilizzando il layout della procedura guidata o in modo ad hoc utilizzando il layout a schede. Per informazioni sui layout dei pannelli, consulta [Funzionalità di layout di Adaptive Forms](layout-capabilities-adaptive-forms.md).

In una tipica esperienza di compilazione dei moduli, sono necessari più passaggi rispetto all’acquisizione dei dati. L’invio completo di un modulo può comprendere altri passaggi, ad esempio la firma digitale del modulo, la verifica delle informazioni inserite nel modulo, l’elaborazione dei pagamenti e così via. Si differenzia da caso a caso.

Se il tuo caso d’uso richiede una serie di passaggi per l’acquisizione dei dati o se sono previste normative che richiedono l’osservanza di determinati passaggi, [!DNL Experience Manager Forms] fornisce un modo per applicare tale struttura comune nei diversi moduli. L’implementazione premeditata della struttura del modulo definisce la sequenza di passaggi per un modulo. ![Esempio di sequenza di moduli a più passaggi](assets/formpipeline.png)

Esempio di sequenza di moduli a più passaggi

Prendiamo un caso d’uso in cui è necessario creare una sequenza per compilare, verificare, firmare e confermare i passaggi di un modulo. La procedura per creare una sequenza di questo tipo è la seguente:

1. Definire un modello di modulo e aggiungergli il pannello richiesto. Dovrebbe essere disponibile un pannello per ogni passaggio della sequenza. Tuttavia, puoi includere i pannelli secondari all’interno di un pannello.

   In questo esempio, possiamo aggiungere i seguenti pannelli:

   * **[!UICONTROL Riempimento]**: Contiene campi dei moduli per l’acquisizione dei dati. In questo caso è possibile includere pannelli secondari nidificati per creare sezioni per diversi tipi di informazioni, ad esempio personali, familiari, finanziarie e così via.

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL E-sign]**: Contiene il **[!UICONTROL Sign]** che può essere utilizzato in un modulo adattivo basato su XFA. Fornisce i seguenti servizi di firma:

      * Servizi eSign di Adobe Document Cloud
      * Firma scarabocchio
   * **[!UICONTROL Conferma]**: Contiene il **[!UICONTROL Riepilogo]** che visualizza un messaggio di conferma dell’invio del modulo dopo che un utente firma il modulo e raggiunge il passaggio Conferma (riepilogo) nella sequenza. Gli autori possono configurare il testo [!UICONTROL Riepilogo] , mostrare un messaggio di ringraziamento, mostrare un collegamento al PDF generato e così via.



1. Seleziona il layout del pannello principale come **[!UICONTROL Creazione guidata]**.
1. Completare i passaggi successivi per creare il modello di modulo. <!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

Dopo aver definito la sequenza del modulo nel modello di modulo, è possibile utilizzarla per creare moduli che avranno la struttura di base definita come sequenza in posizione, anche se è sempre possibile personalizzare il modulo in base alle proprie esigenze.
