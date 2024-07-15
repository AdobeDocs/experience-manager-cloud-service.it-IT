---
title: Come si invia un modulo adattivo per la revisione?
description: Condividi un modulo adattivo per la revisione con uno o più revisori.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
source-git-commit: 57e421a865b664c0adb7af93b33bd4b6b32049ab
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Associazione dei revisori di invio a un modulo {#associating-submission-reviewers-with-a-form}

Quando si crea un modulo, è possibile specificare gli utenti che esaminano gli invii del modulo tramite il portale moduli e forniscono feedback. La tua organizzazione può raccogliere feedback e rielaborare i moduli inviati.

[!DNL AEM Forms] consente di associare un gruppo di revisori a un modulo. Gli utenti aggiunti a un gruppo di revisione di un modulo vedranno gli invii di questo modulo e forniranno un feedback.

I gruppi di revisori assegnati a un modulo possono esaminare solo gli invii del modulo specificato.

## Prerequisito {#prerequisite}

### Abilitazione della proprietà dei gruppi di revisori per l’invio per Adaptive Forms tramite l’editor schema metadati {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Per associare un gruppo di revisori a un modulo, modifica lo schema di metadati di Adaptive Forms. Per impostazione predefinita, non è possibile aggiungere un gruppo di revisori a un modulo inviato.

Per modificare lo schema metadati:

1. In modalità Creazione, nell&#39;Experience Manager, fare clic su **Strumenti** > **Assets** > **Schemi metadati**.
1. Nella pagina Forms dello schema, passa a **Forms** > **Forms creato nell&#39;AEM.**

   L’URL della pagina è:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Seleziona **Modulo adattivo** e fai clic su **Modifica**.
1. Nella pagina Modifica modulo fare clic su **Avanzate**.
1. Nella scheda Avanzate, trascina e rilascia il componente **Testo a riga singola** disponibile in Genera modulo.
1. Seleziona il componente testo aggiunto per visualizzarne le impostazioni.

   In Impostazioni, immetti `./jcr:content/metadata/form-submission-reviewer-group` nel campo Mappa su proprietà.

   Il campo gruppo revisore invio nelle proprietà avanzate del modulo adattivo è abilitato con il nome specificato in Etichetta campo.

## Associazione dei revisori di invio a un modulo {#associating-submission-reviewers-with-a-form-1}

Per associare i revisori per l’invio a un modulo adattivo, crea un gruppo di revisori e aggiungi gli utenti. Aggiungi il gruppo di revisori creato nel campo revisore invio modulo nelle proprietà avanzate del modulo.
I gruppi di utenti consentono di associare diversi set di revisori per l’invio a diversi Forms adattivi. Questa funzione impedisce a un utente non autorizzato di inviare un messaggio di revisione.

Prima di eseguire i passaggi seguenti, vedere [Prerequisito](adding-reviewers-form.md#prerequisite).

Per creare un gruppo e aggiungervi membri, passa a **Strumenti** > **Operazioni** > **Sicurezza** > **Gruppi**.
Per ulteriori informazioni, vedere [Amministrazione utenti e servizi](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).
Assicurati di aggiungere il gruppo creato come membro del gruppo di utenti predefinito: **forms-submit-reviewers**. Questo gruppo di utenti viene fornito con [!DNL AEM Forms] e garantisce che gli utenti vengano aggiunti come revisori per l&#39;invio.

Per associare gruppi di utenti a un modulo adattivo:

1. In modalità creazione, passa a **Forms** > **Forms e documenti**.
1. Utilizza l&#39;opzione **Seleziona **per selezionare un modulo adattivo e fai clic su **Visualizza proprietà**.
1. Nella finestra Proprietà del modulo fare clic su **Modifica** e quindi su **AVANZATE**.
1. Immettere il gruppo nel campo gruppo revisore invio e fare clic su **Fine**.

   Viene visualizzato il campo del gruppo di revisori dell’invio con il nome specificato nello schema di metadati modificato di Adaptive Forms.

>[!NOTE]
>
>Replica utenti e moduli per garantire la disponibilità degli utenti e dei moduli nell&#39;implementazione remota di [!DNL AEM Forms].
>
>Assicurati che tutti gli utenti vengano replicati durante la revisione dei membri dei gruppi di utenti nell’implementazione remota.

>[!MORELIKETHIS]
>
>* [Creazione e gestione delle revisioni nei moduli](/help/forms/create-reviews-forms.md)
>* [Creare e gestire revisioni per un modulo adattivo](/help/forms/review-adaptiveforms-in-sites-page.md)