---
title: Debug di moduli HTML5
description: Nell’elenco dei documenti vengono descritti i passaggi per la risoluzione di vari problemi noti.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: HTML5 Forms,Mobile Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# Debug di moduli HTML5 {#debugging-html-forms}

Questo documento include diversi scenari di risoluzione dei problemi. Per ogni scenario, vengono forniti alcuni passaggi per risolvere il problema. Segui questi passaggi e, se il problema persiste, configura il Logger per ottenere e rivedere i registri per gli errori/avvisi. Per ulteriori dettagli sulla registrazione dei moduli di HTML5, vedere [Generazione dei registri per i moduli HTML5](/help/forms/enable-logs.md).

## Problema: durante il rendering del modulo, viene visualizzata la pagina dell’eccezione org.apache.sling.api.SlingException {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

Nei dettagli dell&#39;eccezione, cercare la parola **causata da**.

Il motivo probabile è che uno o più parametri nell’URL non sono corretti.

Verifica i seguenti parametri:

<table>
 <tbody>
  <tr>
   <td><strong>Parametro</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Modello</td>
   <td>Nome file del modello</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>Percorso in cui risiedono il modello e le risorse associate</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Percorso assoluto del file di dati unito al modello.<br /> Nota: il percorso assoluto del file di dati.</td>
  </tr>
  <tr>
   <td>dati</td>
   <td>Byte di dati con codifica UTF-8 uniti al modello.</td>
  </tr>
 </tbody>
</table>

## Problema: impossibile eseguire il rendering di un modulo (viene visualizzato un messaggio di errore) {#problem-unable-to-render-form}

1. Verificare che i parametri specificati siano corretti. Per informazioni dettagliate sui parametri, vedere [Parametri di rendering](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. Accedi a Gestione pacchetti CRX (all’indirizzo https://&lt;server>:&lt;porta>/crx/packmgr/index.jsp) e verifica che i seguenti pacchetti siano installati correttamente:

   * adobe-lc-forms-content-pkg-&lt;versione>.zip
   * adobe-lc-forms-runtime-pkg-&lt;versione>.zip

1. Accedi alla console web CQ (console Felix) all’indirizzo https://&lt;server>:&lt;porta>/system/console/bundles.

   Assicurati che lo stato dei seguenti bundle sia &quot;active&quot;:

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * Adobe XFA Forms Renderer

   (com.adobe.livecycle.adobe-lc-forms-core)

   * Connettore LC Forms XFA di Adobe

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## Problema: rendering del modulo senza stili {#problem-form-renders-without-styles}

1. Nel browser aprire **Strumenti per sviluppatori**. Assicurati che profile.css sia disponibile.
1. Se il file profile.css non è disponibile, accedere a CRX DE all&#39;indirizzo https://&lt;server>:&lt;port>/crx/de.
1. Nella gerarchia delle cartelle a sinistra, passa a /etc/clientlibs/fd/xfaforms/. Apri i file css.txt elencati nelle cartelle.

   * profilo
   * runtime
   * scrollnav
   * barra strumenti
   * xfalib

1. Verifica che i file menzionati all’interno del file css.txt siano presenti in CRX DE lite in /libs/fd/xfaforms/clientlibs/xfalib/css.

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. Se i file menzionati non sono disponibili, installa nuovamente il pacchetto adobe-lc-forms-runtime-pkg-&lt;versione>.zip.

### Problema: si è verificato un errore imprevisto {#problem-unexpected-error-encountered}

1. Nell’URL del modulo, aggiungi un parametro di query debugClientLibs e impostane il valore su true (ad esempio: https://&lt;server>:&lt;porta>/content/xfaforms/profiles/test.html?contentRoot=&lt;percorso>&amp;template=&lt;nome del file xdp>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. Nel browser desktop come chrome, passa a Strumenti di sviluppo > Console.
1. Apri i registri per identificare il tipo di errore. Per informazioni dettagliate sui registri, vedere [registri per HTML5 forms](/help/forms/enable-logs.md).
1. Vai a Strumenti di sviluppo > Console. Utilizza la traccia dello stack per individuare il codice che causa l’errore. Debug dell’errore per risolvere il problema.

   >[!NOTE]
   >
   >Se si tratta di un errore di script, verificare se lo stesso problema si verifica durante il rendering PDF del modulo. In caso affermativo, si verifica un problema nella logica di scripting del modulo.

## Problema: impossibile inviare il modulo {#problem-unable-to-submit-the-form}

1. Assicurati di disporre dei diritti di accesso al server AEM e di essere connesso al server.
1. Verifica che il parametro submitUrl sia corretto.
1. Abilita i registri lato client come indicato in [Registri per i moduli HTML5](/help/forms/enable-logs.md) utilizzando l&#39;opzione di debug **1-a5-b5-c5**. Quindi esegui il rendering del modulo e fai clic su invia. Apri la console di debug del browser e verifica la presenza di un errore.
1. Individuare i registri del server come indicato in [Registri per i moduli HTML5](/help/forms/enable-logs.md). Controlla se si è verificato un errore nei registri del server durante l’invio.

## Problema: i messaggi di errore localizzati non vengono visualizzati {#problem-localized-error-messages-do-not-display}

1. Eseguire il rendering del modulo con il parametro di query aggiuntivo **debugClientLibs=true** nel browser desktop, quindi passare a Strumenti di sviluppo > Risorse e controllare il file I18N.css.
1. Se il file non è disponibile, accedere a CRX DE all&#39;indirizzo https://&lt;server>:&lt;port>/crx/de.
1. Nella gerarchia delle cartelle a sinistra, passa a /libs/fd/xfaforms/clientlibs/I18N e accertati che siano presenti i seguenti file e cartelle:

   * Namespace.js
   * LogMessages.js
   * Cartelle per lingue

1. Se uno dei file o delle cartelle di cui sopra non esiste, installa di nuovo il pacchetto **adobe-lc-forms-runtime-pkg-&lt;versione>.zip**.
1. Passare alla cartella con lo stesso nome della lingua e verificarne il contenuto. La cartella deve contenere i seguenti file:

   * I18N.js
   * js.txt

1. Controlla il contenuto di js.txt e accertati che contenga le seguenti voci.

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problema: immagine non visualizzata {#problem-image-not-showing-up}

1. Verifica che l’URL dell’immagine sia corretto.
1. Verifica se il browser in uso supporta questo tipo di immagine.
1. Nei dettagli dell&#39;eccezione, cercare la parola **causata da**.

   Il motivo probabile è che uno o più parametri nell’URL non sono corretti.

   Verifica i seguenti parametri:
Testo del passaggio

<table>
 <tbody>
  <tr>
   <td><strong>Parametro</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Modello</td>
   <td>Nome file del modello</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>Percorso in cui risiedono il modello e le risorse associate</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Percorso assoluto del file di dati unito al modello.<br /> Nota: il percorso assoluto del file di dati.</td>
  </tr>
  <tr>
   <td>dati</td>
   <td>Byte di dati con codifica UTF-8 uniti al modello.</td>
  </tr>
 </tbody>
</table>

1. Nel browser desktop, vai a Strumenti di sviluppo > Risorse.

   Se l&#39;immagine è visualizzata, selezionare la casella di controllo a sinistra in Frame.
