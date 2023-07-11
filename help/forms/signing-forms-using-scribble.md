---
title: Applicare firme elettroniche a un modulo utilizzando le firme scarabocchio
seo-title: Apply electronic signatures to a form using scribble signatures
description: Firma di moduli tramite scarabocchio
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
source-git-commit: 50f5b34fa9453fd6d8e85290f69194622afeb42c
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# Applicare firme elettroniche a un modulo utilizzando le firme scarabocchio{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

È possibile utilizzare **Firma a mano** componente e **Passaggio di firma** componente per disegnare la firma (a mano libera) in un modulo adattivo. Il componente del passaggio Firma visualizza una versione PDF del Modulo adattivo. Per utilizzare il componente del passaggio Firma, è necessario che sia abilitata l’opzione Documento di record o che sia abilitato un Forms adattivo basato su modello di modulo.

![Finestra di dialogo Simbolo a mano](assets/scribble-signature.png)

## Varie opzioni disponibili nella finestra Firma

* **R:** Fai clic su **Pennello vernice** per disegnare la firma sull&#39;area di lavoro.
* **B:** Fai clic su **Cancella** per cancellare la firma dall&#39;area di lavoro.
* **C:** Fai clic su **Geolocalizzazione** per aggiungere la geolocalizzazione insieme alla firma.
* **D:** Fai clic su **Tastiera** per digitare il proprio nome nell&#39;area di lavoro.

Una volta toccato il pulsante Fine ![aem_forms_save](assets/aem_forms_save.png) nella finestra Firma scarabocchio, non è possibile modificare la firma. Nel caso in cui si desideri modificare la firma, è necessario ignorare la firma corrente e riapporla utilizzando l&#39;opzione Pennello/Tastiera.

Puoi toccare il **Configura** ![icona configura](assets/configure.png) per impostare le proporzioni dell’area di lavoro della firma scarabocchio.
* Quando le proporzioni dell’area di lavoro Firma a mano sono inferiori a 1, le informazioni sulla geolocalizzazione vengono aggiunte nella parte inferiore dell’area di lavoro Firma a mano.


* Quando le proporzioni dell’area di lavoro Firma scarabocchio sono superiori a 1, le informazioni sulla geolocalizzazione vengono aggiunte al lato destro dell’area di lavoro Firma scarabocchio.


![firma scarabocchio-inferiore](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>Le firme vengono sempre salvate in formato PNG.
>

## Configurare un modulo adattivo per utilizzare la firma scarabocchio {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crea un modulo adattivo basato su modello di modulo o con l’opzione Documento di record abilitata. Per informazioni dettagliate, consulta [Creazione di un modulo adattivo](creating-adaptive-form.md).
1. Trascina la selezione **Firma a mano** dal browser componenti al modulo adattivo.
1. Tocca il **Configura** ![configura](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del componente Firma scarabocchio. Configura le proprietà del componente Firma scarabocchio.
1. Trascina il componente Passaggio firma dal browser componenti al modulo adattivo.

   >[!NOTE]
   >
   >Il componente Passaggio di firma occupa l’intera larghezza disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio di firma.

1. Nel browser Contenuti, tocca **Contenitore modulo**, e tocca il **Configura** ![icona configura](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo. Accedi a **Contenitore modulo adattivo** > **Firma elettronica** e deseleziona la **Abilita Adobe Sign** opzione. Tocca Fine ![aem_forms_save](assets/aem_forms_save.png) per salvare le modifiche.

   >[!NOTE]
   >
   >Quando aggiungi un componente Passaggio di firma a un modulo adattivo, l’opzione Abilita Adobe Sign viene selezionata automaticamente.

1. Tocca il **Configura** ![configura](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del passaggio Firma. Configura le seguenti proprietà:

   * **Nome elemento**: specifica il nome del componente.

   * **Titolo:** Specifica un titolo univoco per il componente.
   * **Messaggio modello:** Specificare il messaggio da visualizzare durante il caricamento del PDF della firma. I servizi Adobe Sign impiegano un po’ di tempo per preparare e caricare signature PDF.
   * **Servizio di firma:** Seleziona la **Firma a mano** opzione.

   * **Classe CSS**: specifica la classe CSS della libreria client, se presente. Si consiglia di utilizzare [temi](themes.md) e [stili in linea](inline-style-adaptive-forms.md) anziché Classe CSS.

   Tocca Fine ![aem_forms_save](assets/aem_forms_save.png) per salvare le modifiche. La firma è stata configurata correttamente.

   Ora, quando si compila un modulo, viene visualizzata una versione PDF di Modulo adattivo e vengono fornite le opzioni per la firma del documento PDF. Per informazioni dettagliate, consulta [Firmare un modulo adattivo utilizzando la firma scarabocchio](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Firmare un modulo adattivo utilizzando la firma scarabocchio {#sign-an-adaptive-form-using-scribble-signature}

1. Dopo aver compilato un modulo adattivo e aver raggiunto la pagina Passaggio firma, viene visualizzata la schermata della firma.

   ![Schermata di firma per la pagina EchoSign](assets/esignscribblesign.jpg)

1. Clic **[!UICONTROL Firma]**. Viene visualizzata la finestra di dialogo del segno scarabocchio. Firma il modulo e fai clic su Fine ![aem_forms_save](assets/aem_forms_save.png) per salvare la firma.

   ![Finestra di dialogo Simbolo a mano](assets/scribblewidget.png)

1. Fare clic su Completa per completare il processo di firma.

   ![Completa il processo di firma](assets/scribblecomplete.jpg)

Le firme vengono aggiunte al modulo e il controllo modulo passa al pannello successivo.
