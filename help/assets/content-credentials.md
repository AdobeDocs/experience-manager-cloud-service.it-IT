---
title: Integrazione content credentials
description: I content credentials, integrati in AEM Assets e inclusi nella visualizzazione Assets, possono offrire un contesto nella cronologia di una risorsa, incluso come è stata creata e chi è stato coinvolto nella sua creazione. Come un’etichetta nutrizionale per i contenuti digitali, i Content credentials possono contribuire ad aumentare la trasparenza e a creare fiducia nei confronti del pubblico.
role: User
source-git-commit: 1c0ffe9d6e45f1d6b3574d1ac5611b2c2e2d00e0
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Credenziali del contenuto {#content-credentials}

I brand si preoccupano più che mai della trasparenza dei contenuti, della divulgazione dell’intelligenza artificiale e della prevenzione della manomissione delle risorse. Il Content Authenticity Initiative (CAI) di Adobe crea strumenti conformi allo standard tecnico [Coalition for Content Provenance and Authenticity](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA). I content credentials, un nuovo tipo di metadati crittografati e in grado di evidenziare eventuali manomissioni, possono aiutare gli utenti a comprendere la linea di contenuti e garantire l’integrità delle risorse del marchio. Possono includere un’ampia gamma di dati sulla provenienza che offrono informazioni approfondite sulla storia di un bene digitale.

Tali informazioni possono includere:

* **Emittente o firmatario:** informazioni sull&#39;entità o sulla società che ha emesso la firma digitale per certificare la risorsa.
* **Data problema:** la data in cui le credenziali contenuto sono state applicate alla risorsa.
* **Credito e utilizzo:** informazioni sul produttore della risorsa, tra cui nome, handle per social media o altre informazioni relative all&#39;identità.
* **Processo:** record di eventuali modifiche apportate alla risorsa.
* **Dettagli dispositivo:** informazioni sull&#39;app o sul dispositivo utilizzato per creare o modificare la risorsa.
* **Strumento di intelligenza artificiale utilizzato:** se è stata utilizzata l&#39;intelligenza artificiale generativa per modificare o creare la risorsa, è possibile includere il nome del modello utilizzato.
* **Altre informazioni importanti:** potrebbero essere inclusi anche dati aggiuntivi per offrire più contesto sulla cronologia di una risorsa.

Per una visualizzazione completa, [Verifica](https://contentcredentials.org/verify) può offrire informazioni più complete sulla cronologia delle risorse.

Adobe Experience Manager Assets ora supporta i Content credentials, consentendo agli utenti di visualizzare i Content credentials direttamente nella vista Assets dell’AEM. Esaminando i dettagli della risorsa, qualsiasi immagine con Content credentials (ad esempio quelle create con i servizi GenAI) mostra i dettagli del manifesto in un pannello dedicato. Se la risorsa viene scaricata, pubblicata o condivisa, i Content credentials rimangono intatti con la risorsa.

![risorse](/help/assets/assets/content-credentials.png)

## Accedi ai Content credentials {#access-content-credentials}

1. Vai all&#39;interfaccia utente di visualizzazione di Assets e fai clic su **Assets** nel riquadro a sinistra.
1. Passa a una cartella e seleziona la risorsa desiderata.
1. Fai clic su **Dettagli** e seleziona `Cr pin` dal riquadro più a destra. Nella scheda Content credentials vengono visualizzate le seguenti informazioni sulla risorsa.
   1. **Immagine generata:** Data e ora di applicazione dei Content credentials.
   1. **Riepilogo contenuto:** indica se la risorsa è generata parzialmente o completamente da IA o come è stata modificata.
      ![content credentials](/help/assets/assets/content-credentials1.png)
   1. **Processo:** descrive l&#39;applicazione, il dispositivo e lo strumento di intelligenza artificiale (ad esempio, Adobe Firefly) utilizzati per generare la risorsa, nonché le modifiche apportate successivamente.
      ![processo](/help/assets/assets/CR-Process.png)
   1. **Informazioni sui Content credentials:** Nome dell&#39;emittente con la data e l&#39;ora di emissione.
      ![emittente](/help/assets/assets/CR-issuer.png)
