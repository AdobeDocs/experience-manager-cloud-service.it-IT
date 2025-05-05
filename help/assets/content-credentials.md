---
title: Integrazione con Content Credentials
description: Content Credentials, integrato in AEM Assets e disponibile nella visualizzazione Assets, può offrire un contesto nella cronologia di una risorsa, compreso come è stata creata e chi è stato coinvolto nella sua creazione. Come un’etichetta nutrizionale per i contenuti digitali, Content Credentials può contribuire ad aumentare la trasparenza e a creare fiducia nei confronti del pubblico.
role: User
exl-id: 27c25ae0-4477-40c3-85c8-3e0aa725aba7
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 3%

---

# Content Credentials {#content-credentials}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integrazione di AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuovo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilita Dynamic Media Prime e Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

I brand si preoccupano più che mai della trasparenza dei contenuti, della divulgazione dell’intelligenza artificiale e della prevenzione della manomissione delle risorse. Il Content Authenticity Initiative (CAI) di Adobe crea strumenti conformi allo standard tecnico [Coalition for Content Provenance and Authenticity](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA). Content Credentials, un nuovo tipo di metadati crittografati e in grado di evidenziare eventuali manomissioni, consente agli utenti di comprendere la linea di contenuti e garantire l&#39;integrità delle risorse del marchio. Possono includere un’ampia gamma di dati sulla provenienza che offrono informazioni approfondite sulla storia di un bene digitale.

Tali informazioni possono includere:

* **Emittente o firmatario:** informazioni sull&#39;entità o sulla società che ha emesso la firma digitale per certificare la risorsa.
* **Data problema:** la data in cui il Content Credential è stato applicato alla risorsa.
* **Credito e utilizzo:** informazioni sul produttore della risorsa, tra cui nome, handle per social media o altre informazioni relative all&#39;identità.
* **Processo:** record di eventuali modifiche apportate alla risorsa.
* **Dettagli dispositivo:** informazioni sull&#39;app o sul dispositivo utilizzato per creare o modificare la risorsa.
* **Strumento di intelligenza artificiale utilizzato:** se è stata utilizzata l&#39;intelligenza artificiale generativa per modificare o creare la risorsa, è possibile includere il nome del modello utilizzato.
* **Altre informazioni importanti:** potrebbero essere inclusi anche dati aggiuntivi per offrire più contesto sulla cronologia di una risorsa.

Per una visualizzazione completa, [Verifica](https://contentcredentials.org/verify) può offrire informazioni più complete sulla cronologia delle risorse.

Adobe Experience Manager Assets ora supporta Content Credentials, consentendo agli utenti di visualizzare Content Credentials direttamente nella vista Assets di AEM. Esaminando i dettagli della risorsa, qualsiasi immagine con Content Credentials (ad esempio quelle create con i servizi GenAI) mostra i dettagli del manifesto in un pannello dedicato. Se la risorsa viene scaricata, pubblicata o condivisa, Content Credentials rimane intatto con la risorsa.

![risorse](/help/assets/assets/content-credentials.png)

## Accedere a Content Credentials {#access-content-credentials}

1. Vai all&#39;interfaccia utente di visualizzazione di Assets e fai clic su **Assets** nel riquadro a sinistra.
1. Passa a una cartella e seleziona la risorsa desiderata.
1. Fai clic su **Dettagli** e seleziona `Cr pin` dal riquadro più a destra. Nella scheda Content Credentials sono visualizzate le seguenti informazioni sulla risorsa.
   1. **Immagine generata:** Data e ora di applicazione di Content Credentials.
   1. **Riepilogo contenuto:** indica se la risorsa è generata parzialmente o completamente da IA o come è stata modificata.

      ![credenziali contenuto](/help/assets/assets/content-credentials1.png)
   1. **Processo:** descrive l&#39;applicazione, il dispositivo e lo strumento di intelligenza artificiale (ad esempio Adobe Firefly) utilizzati per generare la risorsa, nonché le modifiche apportate successivamente.

      ![processo](/help/assets/assets/CR-Process.png)
   1. **Informazioni su questo Content Credentials:** Nome dell&#39;emittente insieme alla data e all&#39;ora di emissione.

      ![emittente](/help/assets/assets/CR-issuer.png)
