---
title: Utilizzare reCAPTCHA con Edge Delivery Services per AEM Forms as a Cloud Service
description: Utilizzare il servizio reCAPTCHA di Google in un modulo EDS
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
role: Admin, Architect, Developer
source-git-commit: fe45123b3aefddaf02bc8584283941db168ba174
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 24%

---


# Utilizzare reCAPTCHA con Edge Delivery Services per AEM Forms as a Cloud Service

<span>La funzionalità **reCAPTCHA** è inclusa nel programma preliminare. Per richiedere l&#39;accesso alla funzionalità **reCAPTCHA** per i Edge Delivery Services AEM Forms, invia un&#39;e-mail dal tuo indirizzo di lavoro a mailto:aem-forms-ea@adobe.com.</span>

reCAPTCHA è un popolare strumento utilizzato per proteggere i siti web da attività fraudolente, spam e uso improprio. In Edge Delivery Services, il blocco modulo adattivi fornisce la capacità di aggiungere Google reCAPTCHA per distinguere tra esseri umani e bot. Questa funzione consente agli utenti di proteggere il proprio sito web da spam e uso improprio.
Si consideri, ad esempio, un modulo “enquiry” che raccoglie dati quali le date di inizio e di fine del viaggio, il budget della camera, il costo stimato del viaggio e le informazioni sui viaggiatori. In tali casi, esiste il rischio che utenti malintenzionati sfruttino il modulo per scopi quali l’invio di e-mail di phishing o l’invio di contenuti irrilevanti o dannosi tramite spambot. L’integrazione di reCAPTCHA offre maggiore sicurezza verificando che gli invii provengano da utenti autentici, riducendo in modo efficace le voci di spam.

<!-- ![Recaptcha Image](/help/edge/docs/forms/assets/recaptcha-image.png){width="300" align="center"} -->

I Edge Delivery Services supportano solo **Score based(v3)-reCAPTCHA** per il blocco modulo adattivo.

![Recaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png){width="300" align="center"}


Alla fine di questo articolo imparerai a:
* [Abilitare Google reCAPTCHA per un singolo modulo](#enable-google-recaptchas-for-a-single-form)
* [Abilitare reCAPTCHA per tutti i moduli sul sito](#enable-recaptcha-for-all-the-forms)

## Prerequisiti

* Iniziare lo sviluppo di Edge Delivery Services Forms seguendo i passaggi descritti in [Creare un modulo utilizzando il blocco di Forms adattivo](/help/edge/docs/forms/create-forms.md).
* Registra il dominio con [Google reCAPTCHA e ottieni le credenziali](https://www.google.com/recaptcha/admin/create).

## Abilitare Google reCAPTCHA per un singolo modulo {#enable-google-recaptchas-for-a-single-form}

L’abilitazione di Google reCAPTCHA per un singolo modulo comporta l’integrazione del servizio Google reCAPTCHA in un modulo web specifico per evitare abusi automatizzati o invii di spam.

Per abilitare Google reCAPTCHA per un singolo modulo:
1. [Configurare la chiave segreta reCAPTCHA nel file di configurazione del progetto](#configure-secret-key)
1. [Aggiungere la chiave del sito reCAPTCHA al modulo](#add-site-key)

Per iniziare a configurare reCaptcha in Edge Delivery Services Forms, consulta il seguente [foglio di calcolo](/help/edge/docs/forms/assets/recaptcha.xlsx) che include la definizione del modulo.

### Configurare la chiave segreta reCAPTCHA nel file di configurazione del progetto {#configure-secret-key}

Il segreto del sito per il dominio registrato con Google reCAPTCHA viene aggiunto al progetto del file di configurazione (`.helix/config`) nella cartella dei progetti AEM in Microsoft SharePoint o Google Drive. Per aggiungere il segreto del sito al file di configurazione:

1. Vai alla cartella dei progetti AEM su Microsoft® SharePoint o Google Drive.
1. Creare il file `.helix/config.xlsx` nella cartella del progetto AEM nel sito Microsoft SharePoint o il file `.helix/config` nella cartella del progetto AEM nell&#39;unità Google.

   >[!NOTE]
   >
   > Il [file di configurazione del progetto](https://www.aem.live/docs/configuration) è un foglio di calcolo disponibile in `/.helix/config`. Se il file non esiste, crealo.

1. Apri il file `config` e aggiungi le seguenti coppie chiave-valore:

   * **captcha.secret**: valore chiave segreta Google reCAPTCHA
   * **captcha.type**: reCAPTCHA v2

   >[!NOTE]
   >
   >  * È possibile recuperare le chiavi reCAPTCHA dall&#39;[Admin Console reCAPTCHA di Google](https://www.google.com/recaptcha/admin).
   >  * Specificare il valore di **captcha.type** nel file `config` come **reCAPTCHA v2**.

   Fai riferimento alla schermata di un file di configurazione del progetto di seguito:

   ![File di configurazione del progetto](/help/forms/assets/recaptcha-config-file.png)

1. Salva il file `config`.

1. Anteprima e pubblicazione del file `config` tramite [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

### Aggiungere la chiave del sito reCAPTCHA al modulo {#add-site-key}

La Chiave del sito per un dominio registrato con Google reCAPTCHA viene aggiunta al foglio di calcolo del modulo da proteggere. Per aggiungere la chiave del sito a un modulo:

1. Passa alla cartella del progetto AEM in Microsoft® SharePoint o Google Drive e apri il foglio di calcolo. È inoltre possibile creare un nuovo foglio di calcolo per un modulo.
1. Inserisci una riga nel foglio di calcolo per aggiungere un nuovo campo come CAPTCHA, inclusi i seguenti dettagli:
   * **tipo**: captcha
   * **valore**: valore chiave sito reCAPTCHA Google

   Fai riferimento alla schermata seguente, che mostra il foglio di calcolo con il nuovo tipo di riga CAPTCHA:

   ![Foglio di calcolo Recaptcha](/help/edge/docs/forms/assets/recaptcha-spreadsheet.png)

   >[!NOTE]
   >
   >  È possibile recuperare le chiavi reCAPTCHA dall&#39;[Admin Console reCAPTCHA di Google](https://www.google.com/recaptcha/admin).

1. Salvare il foglio di calcolo.
1. Utilizza la [barra laterale di AEM](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima e pubblicare il foglio.

Dopo aver aggiunto una nuova riga nella definizione del modulo, nell’angolo inferiore destro del modulo viene visualizzato un badge reCAPTCHA. In questo modo il modulo è ora protetto da attività fraudolente, spam e uso improprio.

![modulo recaptcha](/help/edge/docs/forms/assets/recaptcha-form.png)

## Abilitare reCAPTCHA per tutti i moduli sul sito{#enable-recaptcha-for-all-the-forms}

Per applicare Google reCAPTCHA a tutti i moduli del sito che utilizzano Adaptive Forms Block, salta i passaggi precedenti e incorpora direttamente il valore `sitekey` nel file `recaptcha.js`. Per includere il valore della chiave del sito nel file `recaptcha.js`:

1. [Aggiorna la chiave del sito Google reCAPTCHA nel file recaptcha.js](#1-update-google-recaptcha-site-key-in-recaptchajs-file)
1. [Distribuire il file e generare il progetto](#2-deploy-the-file-and-build-the-project)
1. [Visualizzare l’anteprima del sito utilizzando la barra laterale AEM](#3-preview-the-site-using-the-aem-sidekick)

### Aggiornamento della chiave del sito Google reCAPTCHA nel file recaptcha.js

1. Apri l’archivio GitHub corrispondente sul computer locale.
1. Passare alla cartella `[../Form Block/integrations]` e aprire il file `recaptcha.js`.
1. Sostituisci `siteKey` con il valore della chiave del sito Google reCAPTCHA.

   ![Recaptcha applica a tutti i moduli](/help/forms/assets/recaptcha-apply-to-all-forms.png)

   >[!NOTE]
   >
   >  È possibile recuperare le chiavi reCAPTCHA dall&#39;[Admin Console reCAPTCHA di Google](https://www.google.com/recaptcha/admin).

1. Salva il file `recaptcha.js`.

### Distribuire il file e generare il progetto

Distribuisci il file `recaptcha.js` aggiornato nel progetto GitHub e verifica che la build sia corretta.

### Visualizzare l’anteprima del sito utilizzando la barra laterale AEM

Utilizza [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima e pubblicare il sito.

Il badge reCAPTCHA inizia a essere visualizzato per tutti i moduli sul sito.

## Consulta anche

{{see-more-forms-eds}}

