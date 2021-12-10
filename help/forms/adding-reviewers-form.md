---
title: Associazione dei revisori per l’invio a un modulo
seo-title: Associating submission reviewers with a form
description: Scopri come associare i revisori dell’invio a un modulo in [!DNL AEM Forms]. I revisori associati esaminano un modulo inviato tramite il portale dei moduli.
seo-description: Learn how to associate submission reviewers with a form in [!DNL AEM Forms]. Associated reviewers review a form submitted via forms portal.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Associazione dei revisori per l’invio a un modulo {#associating-submission-reviewers-with-a-form}

Quando si crea un modulo, è possibile specificare gli utenti che esaminano l’invio del modulo tramite il portale dei moduli e forniscono un feedback. L’organizzazione può raccogliere feedback e lavorare nuovamente sui moduli inviati.

[!DNL AEM Forms] consente di associare un gruppo di revisori a un modulo. Gli utenti aggiunti a un gruppo di revisione di un modulo visualizzano gli invii del modulo e forniscono un feedback.

I gruppi di revisori assegnati a un modulo possono esaminare solo gli invii del modulo specificato.

## Prerequisito {#prerequisite}

### Abilitazione della proprietà dei gruppi di revisori per Adaptive Forms tramite l&#39;editor dello schema dei metadati {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Per associare un gruppo di revisori a un modulo, modificare lo schema metadati di Forms adattivo. Per impostazione predefinita, non è possibile aggiungere un gruppo di revisori a un modulo inviato.

Per modificare lo schema metadati:

1. In modalità di authoring, in Experience Manager, fai clic su **Strumenti** > **Risorse** > **Schemi metadati**.
1. Nella pagina Forms schema , passa a **Forms** > **Forms Authored in AEM.**

   L’URL della pagina è:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Seleziona **Modulo adattivo** e fai clic su **Modifica**.
1. Nella pagina Modifica modulo fare clic su **Avanzate**.
1. Nella scheda Avanzate , trascina **Testo a riga singola** componente disponibile in Genera modulo.
1. Seleziona il componente di testo aggiunto per visualizzarne le impostazioni.

   In Impostazioni, immetti `./jcr:content/metadata/form-submission-reviewer-group` nel campo Mappa su proprietà .

   Il campo del gruppo di revisori per l’invio nelle proprietà Avanzate del modulo adattivo viene attivato con il nome specificato in Etichetta campo.

## Associazione dei revisori per l’invio a un modulo {#associating-submission-reviewers-with-a-form-1}

Per associare i revisori dell’invio a un modulo adattivo, crea un gruppo di revisori e aggiungi gli utenti. Aggiungere il gruppo di revisori creato nel campo del revisore dell’invio del modulo nelle proprietà avanzate del modulo.
I gruppi di utenti consentono di associare diversi set di revisori per l’invio a diversi Forms adattivi. Questa funzione impedisce la revisione dell’invio da parte di un utente non autorizzato.

Prima di eseguire i seguenti passaggi, vedi [Prerequisito](adding-reviewers-form.md#prerequisite).

Per creare un gruppo e aggiungervi membri, vai a **Strumenti** > **Operazioni** > **Sicurezza** > **Gruppi**.
Per ulteriori informazioni, consulta [Amministrazione e servizi utente](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).
Assicurati di aggiungere il gruppo creato come membro del gruppo di utenti predefinito: **moduli-sottomissione-revisori**. Questo gruppo di utenti viene fornito con [!DNL AEM Forms], e assicura che gli utenti vengano aggiunti come revisori per l’invio.

Per associare gruppi di utenti a un modulo adattivo:

1. In modalità di authoring, passa a **Forms** > **Forms e documenti**.
1. Utilizza l’opzione **Seleziona **per selezionare un modulo adattivo, quindi fai clic su **Visualizza proprietà**.
1. Nella finestra Proprietà del modulo, fare clic su **Modifica**, quindi fai clic su **AVANZATO**.
1. Inserire il gruppo nel campo Gruppo di revisori per l&#39;invio e fare clic su **Fine**.

   Il campo del gruppo di revisori per l&#39;invio viene visualizzato con il nome specificato nello schema di metadati modificato di Adaptive Forms.

>[!NOTE]
>
>Replicare utenti e moduli per garantire la disponibilità di utenti e moduli nell’implementazione remota di [!DNL AEM Forms].
>
>Assicurati che tutti gli utenti vengano replicati come membri di revisione dei gruppi di utenti nell&#39;implementazione remota.

