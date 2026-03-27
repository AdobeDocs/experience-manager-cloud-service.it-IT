---
title: Abilitare e configurare l’interfaccia utente di Associa per le comunicazioni interattive
description: Scopri come abilitare Visualizzazione associata e configurare il flusso di lavoro per gli aggiornamenti in Impostazioni di comunicazione interattiva in modo che gli associati possano utilizzare l’interfaccia utente di Associazione.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 7c3e8a2b-5f21-4a1e-9e2d-8a4b6c7d8e9f
source-git-commit: a41459520feb03594212b91e68cfd8e2b1e610c4
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# Abilitare e configurare l’interfaccia utente di Associa per le comunicazioni interattive

>[!NOTE]
>
> La funzionalità di comunicazione interattiva è disponibile nell’ambito del programma di adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

Questo articolo descrive come abilitare l’interfaccia utente Associa per una comunicazione interattiva (IC) e, facoltativamente, configurare un flusso di lavoro AEM per gli invii. Gli autori eseguono questi passaggi nelle **Impostazioni di comunicazione interattiva**.

Per una panoramica dell&#39;interfaccia utente associata e dei ruoli utente, vedere [Associate UI in Interactive Communication Editor](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md).

## Prerequisiti

Prima di abilitare e configurare l’interfaccia utente Associa, assicurati di disporre di:

- **Accesso dell&#39;autore** all&#39;editor di comunicazioni interattive.
- **Comunicazione interattiva** creata con il layout e le associazioni dati richieste.
- **Associate users** aggiunti al gruppo **forms-associates** (necessari affinché gli associati possano accedere all&#39;interfaccia utente Associate).
- **Autori** aggiunti al gruppo **forms-associates** (necessari per consentire agli autori di accedere all&#39;interfaccia utente Associate).

Quando sei pronto a integrare l’interfaccia utente Associa con l’applicazione e a richiamarla sull’istanza Publish, dovrai anche utilizzare un browser con il supporto a comparsa abilitato e l’IC pubblicato. Per i prerequisiti di integrazione completa, consulta [Integrare l&#39;interfaccia utente Associate nell&#39;applicazione](/help/forms/interactive-communication/invoke-associate-ui.md).

## Abilita visualizzazione associata (interfaccia utente associata)

Attiva l&#39;interfaccia utente Associa a livello di documento in modo che le comunicazioni interattive possano essere utilizzate dagli associati.

1. Apri la comunicazione interattiva nell’editor.
1. Dalla barra delle azioni o dalle opzioni del documento superiore, apri **Impostazioni di comunicazione interattiva** (o **Impostazioni**).

   ![Impostazioni di comunicazione interattiva - Associa proprietà con abilita modifica visualizzazione associata](/help/forms/assets/associate-ui-settings.png)

1. Nel pannello a sinistra, accertati che sia selezionato **Associa proprietà**.
1. A destra, seleziona **Abilita modifica visualizzazione associata**.
1. Fai clic su **Applica modifiche**, quindi salva il documento.

   ![Impostazioni di comunicazione interattiva - Associa proprietà con abilita modifica visualizzazione associata](/help/forms/assets/associate-ui-enable-view.png)

Un messaggio può ricordare all&#39;utente di applicare le modifiche e salvare il documento per abilitare Visualizzazione associata. Dopo il salvataggio, l&#39;IC è disponibile per l&#39;uso basato su associazioni.

### Consenti modifica interfaccia utente associata per componente

Una volta abilitata la visualizzazione Associa per il componente di interoperabilità, è necessario attivare **Consenti modifica per associa** per ogni componente che gli associa devono essere in grado di modificare. I componenti senza questa impostazione attivata rimangono di sola lettura nell’interfaccia utente Associate.

1. Nell’editor IC, seleziona il componente (ad esempio, un campo di testo) nell’area di lavoro o nella gerarchia dei componenti.
1. Nel pannello **Proprietà** di destra, espandi **Associa proprietà**.
1. Attivare **Consenti modifica per associato** **Attivato** per il componente.
1. Ripetere l&#39;operazione per ogni componente che associa deve essere modificato, quindi salvare il documento.

![Consenti la modifica tramite associazione nelle proprietà del componente](/help/forms/assets/associate-ui-allow-editing-by-associate.png)

>[!NOTE]
>
> **Associate Properties** include anche opzioni quali **Typography** (font, dimensione e stile per il campo nell&#39;interfaccia utente Associate), **Tooltip** e **Patterns** (convalide). Utilizzate queste opzioni per controllare l&#39;aspetto e il comportamento del componente quando viene associato per modificarlo, ad esempio per impostare i pattern di convalida in modo che gli associati immettano i dati nel formato richiesto.

## Configurare il flusso di lavoro per l’interfaccia utente associata

Per eseguire un flusso di lavoro di AEM quando gli utenti inviano o aggiornano dati dall’interfaccia utente Associa, configura quanto segue:

1. In **Impostazioni comunicazione interattiva**, seleziona **Flusso di lavoro** nel pannello a sinistra (in Proprietà associate).
1. Attiva **Configura flusso di lavoro per l&#39;aggiornamento** **Attiva**.
1. In **Seleziona modello flusso di lavoro**, scegli il modello flusso di lavoro AEM da eseguire (ad esempio, `conversionWorkflow` o un percorso come `/var/workflow/models/submit-workflow-1`).
1. È possibile impostare **Messaggio di successo flusso di lavoro** (mostrato all&#39;utente al termine del flusso di lavoro).
1. È possibile impostare **URL di reindirizzamento** per inviare l&#39;utente a una pagina specifica dopo l&#39;invio.
1. Fai clic su **Applica modifiche** e salva il documento.

   ![Impostazioni comunicazione interattiva - Configurazione del flusso di lavoro per l&#39;interfaccia utente associata](/help/forms/assets/associate-ui-configure-workflow.png)

Quando abiliti un flusso di lavoro, questo viene eseguito ogni volta che gli utenti inviano dalla Associate UI (Interfaccia utente associata). Per informazioni sul funzionamento dell&#39;invio e del flusso di lavoro, sul punto in cui vengono eseguiti, su chi utilizza l&#39;istanza e considerazioni chiave, vedere [Flusso di lavoro di invio per l&#39;interfaccia utente associata](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior). Tale articolo include anche un esempio di flusso di lavoro che genera PDF da invii IC.

## Completare la configurazione dell’interfaccia utente Associa

Dopo aver abilitato Associa vista (Associate View) e aver configurato facoltativamente il flusso di lavoro:

1. **Abilita campi modificabili:** Nelle sezioni obbligatorie del componente di interoperabilità, abilita i campi che gli associati possono modificare. Imposta le convalide e il comportamento obbligatorio/di sola lettura in base alle esigenze.
1. **Pubblica IC** in modo che sia disponibile nell&#39;istanza Publish per gli associati.
1. Condividere il collegamento IC pubblicato con gli associati. Si autenticano (ad esempio, tramite [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) e aprono l&#39;interfaccia utente Associa, immettono o confermano i dati del cliente e generano la comunicazione finale. Se hai configurato un flusso di lavoro, questo viene eseguito all’invio. Per informazioni sul funzionamento di invio e flusso di lavoro, vedere [Flusso di lavoro di invio per l&#39;interfaccia utente associata](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior).

## Consulta anche

- [Associate UI in Interactive Communication Editor](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Integrare l’interfaccia utente di Associa nell’applicazione](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Flusso di lavoro di invio per l&#39;interfaccia utente associata - IC Genera output PDF](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md) - Funzionamento dell&#39;invio e del flusso di lavoro, più un flusso di lavoro di esempio che genera PDF da invii IC.
